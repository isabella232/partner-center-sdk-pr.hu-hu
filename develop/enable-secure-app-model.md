---
title: Biztonságos alkalmazásmodell engedélyezése
description: Gondoskodjon a partneri központ és a Vezérlőpult alkalmazásainak biztonságossá tételéről.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 3e153e1e7d4e38580d8cb39a3996e56365ff5fbe
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768076"
---
# <a name="enabling-the-secure-application-model-framework"></a>A biztonságos alkalmazásmodellek keretrendszerének engedélyezése

**A következőkre vonatkozik:**

- Partnerközpont

A Microsoft a Microsoft Azure multi-Factor Authentication (MFA) architektúrán keresztül biztonságos, méretezhető keretrendszert biztosít a Cloud Solution Provider (CSP) partnerek és a Vezérlőpult-szállítók (CPV) hitelesítéséhez.

Az új modell használatával emelheti meg a partner Center API-integrációs hívások biztonságát. Ez segíti az összes felet (beleértve a Microsoftot, a CSP-partnereket és a CPVs is) az infrastruktúra és az ügyféladatok biztonsági kockázatokkal szembeni védelméhez.

## <a name="scope"></a>Hatókör

Ez a cikk a következő szereplőkkel kapcsolatos:

- CPV-k
  - A CPV-k olyan független szoftverszállítók, amelyek a CSP-partnerek által a Partner Center API-kkal való integrációhoz használható alkalmazásokat fejlesztenek.
  - A CPV-k nem olyan CSP-partnerek, amelyek közvetlen hozzáféréssel rendelkeznek a Partnerközpont irányítópultjához vagy az API-khoz.

- CSP közvetett szolgáltatók és CSP közvetlen partnereink, akik az App ID + felhasználói hitelesítést használják, és közvetlenül integrálhatók a partner Center API-kkal.

## <a name="security-requirements"></a>Biztonsági követelmények

A biztonsági követelményekről a [partneri biztonsági követelmények](/partner-center/partner-security-requirements)című témakörben olvashat bővebben.

## <a name="secure-application-model"></a>Biztonságos alkalmazás modellje

A Marketplace-alkalmazásoknak a Microsoft API-k meghívásához a CSP-partneri jogosultságokat kell megszemélyesíteni. Ezen érzékeny alkalmazások biztonsági támadásai veszélyeztethetik a vásárlói adatokat.

Az új hitelesítési keretrendszer áttekintését és részleteit a [Secure Application Model Framework](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) -dokumentumból töltheti le. Ez a dokumentum az alapelveket és ajánlott eljárásokat ismerteti, amelyekkel a Piactéri alkalmazások fenntartható és robusztus védelmet jelentenek a biztonsági veszélyekkel szemben.

## <a name="samples"></a>Példák

A következő áttekintő dokumentumok és mintakód azt ismertetik, hogy a partnerek hogyan tudják megvalósítani a biztonságos alkalmazás modelljének keretrendszerét:

- [A CPV áttekintő dokumentuma](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [A CSP áttekintő dokumentuma](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [.NET-minták](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Java-minták](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [REST-utasítások és minták](#rest)
- [PowerShell-utasítások és minták](#powershell)

## <a name="rest"></a>REST

A következő lépésekkel végezheti el a REST-hívásokat a biztonságos alkalmazás modelljének keretrendszerével a mintakód használatával:

1. [Webalkalmazás létrehozása](#create-a-web-app)

2. [Engedélyezési kód beszerzése](#get-authorization-code)

3. [Frissítési jogkivonat beszerzése](#get-refresh-token)

4. [Hozzáférési jogkivonat lekérése](#get-access-token)

5. [Partner Center API-hívás kezdeményezése](#make-partner-center-api-calls)

> [!TIP]
> A partner Center PowerShell-modul használatával beszerezhet egy engedélyezési kódot és egy frissítési jogkivonatot. Ezt a lehetőséget a 2. és a 3. lépés helyett is kiválaszthatja. További információkért lásd a [PowerShell szakaszt és példákat](#powershell).

### <a name="create-a-web-app"></a>Webalkalmazás létrehozása

A REST-hívások előtt létre kell hoznia és regisztrálnia kell egy webalkalmazást a partner Centerben.

1. Jelentkezzen be az [Azure Portalra](https://portal.azure.com).

2. Hozzon létre egy Azure Active Directory (Azure AD) alkalmazást.

3. Az *alkalmazás követelményeitől függően* delegált alkalmazási engedélyeket adhat a következő erőforrásokhoz. Szükség esetén további delegált engedélyeket adhat hozzá az alkalmazás erőforrásaihoz.

   1. **Microsoft partner Center** (egyes bérlők ezt a **SampleBECApp** mutatják)

   2. **Azure felügyeleti API** -k (ha Azure API-k meghívását tervezi)

   3. **Microsoft Azure Active Directory**

4. Győződjön meg arról, hogy az alkalmazás kezdőlapjának URL-címe olyan végpontra van beállítva, amelyben egy élő webalkalmazás fut. Az alkalmazásnak el kell fogadnia az [engedélyezési kódot](#get-authorization-code) az Azure ad bejelentkezési hívását. Például a [következő szakaszban](#get-authorization-code)szereplő példában a webalkalmazás fut `https://localhost:44395/` .

5. Jegyezze fel a következő információkat a webalkalmazás beállításaiban az Azure AD-ben:

   - Alkalmazásazonosító
   - Alkalmazás titkos kódja

> [!NOTE]
> Azt javasoljuk, hogy az [alkalmazás titkos tanúsítványát használja](/azure/active-directory/develop/active-directory-certificate-credentials). A Azure Portalban azonban létrehozhat egy alkalmazás-kulcsot is. A [következő szakaszban](#get-authorization-code) szereplő mintakód egy alkalmazás kulcsát használja.

### <a name="get-authorization-code"></a>Hozzáférési kód lekérése

Ahhoz, hogy a webalkalmazás el tudja fogadni az Azure AD bejelentkezési hívását, be kell szereznie egy engedélyezési kódot:

1. Jelentkezzen be az Azure AD-be a következő URL-címen: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) . Ügyeljen arra, hogy a felhasználói fiókkal jelentkezzen be, amelyből a partneri központ API-hívásait (például egy felügyeleti ügynököt vagy egy értékesítési ügynököt) kell használnia.

2. Cserélje le az **Application-ID-** t az Azure ad-alkalmazás azonosítójával (GUID).

3. Ha a rendszer kéri, jelentkezzen be a felhasználói fiókjával, és állítsa be az MFA-t.

4. Ha a rendszer kéri, adjon meg további MFA-információkat (telefonszám vagy e-mail-cím) a bejelentkezés ellenőrzéséhez.

5. Miután bejelentkezett, a böngésző átirányítja a hívást a Web App-végpontra az Ön engedélyezési kódjával. Az alábbi mintakód például átirányítja a következőre: `https://localhost:44395/` .

#### <a name="authorization-code-call-trace"></a>Engedélyezési kód hívásának nyomkövetése

```http
POST https://localhost:44395/ HTTP/1.1
Origin: https://login.microsoftonline.com
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Referrer: https://login.microsoftonline.com/kmsi
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: OpenIdConnect.nonce.hOMjjrivcxzuI4YqAw4uYC%2F%2BILFk4%2FCx3kHTHP3lBvA%3D=dHVyRXdlbk9WVUZFdlFONVdiY01nNEpUc0JRR0RiYWFLTHhQYlRGNl9VeXJqNjdLTGV3cFpIWFg1YmpnWVdQUURtN0dvMkdHS2kzTm02NGdQS09veVNEbTZJMDk1TVVNYkczYmstQmlKUzFQaTBFMEdhNVJGVHlES2d3WGlCSlVlN1c2UE9sd2kzckNrVGN2RFNULWdHY2JET3RDQUxSaXRfLXZQdG00RnlUM0E1TUo1YWNKOWxvQXRwSkhRYklQbmZUV3d3eHVfNEpMUUthMFlQUFgzS01RS2NvMXYtbnV4UVJOYkl4TTN0cw%3D%3D

code=AuthorizationCodeValue&id_token=IdTokenValue&<rest of properties for state>
```

### <a name="get-refresh-token"></a>Frissítési jogkivonat beolvasása

A frissítési jogkivonat lekéréséhez az engedélyezési kódot kell használnia:

1. Tegye fel az Azure AD bejelentkezési végpontját `https://login.microsoftonline.com/CSPTenantID/oauth2/token` az engedélyezési kóddal. Példaként tekintse meg a következő [mintát](#sample-refresh-call).

2. Jegyezze fel a visszaadott frissítési tokent.

3. A frissítési token tárolása Azure Key Vaultban. További információkért tekintse meg a [Key Vault API dokumentációját](/rest/api/keyvault/).

> [!IMPORTANT]
> A frissítési jogkivonatot [titkos kulcsként kell tárolni](/rest/api/keyvault/setsecret/setsecret) a Key Vaultban.

#### <a name="sample-refresh-call"></a>Példa frissítési hívásra

Helyőrző kérése:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

Kérés törzse:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

Helyőrző válasza:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Válasz törzse:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a>Hozzáférési jogkivonat lekérése

Ahhoz, hogy hívásokat lehessen kezdeményezni a partner Center API-khoz, be kell szereznie egy hozzáférési jogkivonatot. Hozzáférési jogkivonat beszerzéséhez frissítési jogkivonatot kell használnia, mert a hozzáférési jogkivonat általában nagyon korlátozott élettartammal rendelkezik (például kevesebb mint egy óra).

Helyőrző kérése:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

Kérés törzse:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

Helyőrző válasza:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Válasz törzse:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a>A partner Center API-hívások készítése

A partner Center API-k meghívásához a hozzáférési jogkivonatot kell használnia. Tekintse meg a következő példát.

#### <a name="example-partner-center-api-call"></a>Példa a partner Center API-hívására

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

A [partner Center PowerShell-modul](https://www.powershellgallery.com/packages/PartnerCenter) használatával csökkentheti a szükséges infrastruktúrát a hozzáférési token engedélyezési kódjának cseréjéhez. Ez a módszer nem kötelező a [partneri központ Rest-hívásainak](#rest)készítéséhez.

További információ erről a folyamatról: [Secure app Model](/powershell/partnercenter/secure-app-model) PowerShell-dokumentáció.

1. Telepítse az Azure AD és a partner Center PowerShell-modulokat.

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. A **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** parancs használatával hajtsa végre az engedélyezési folyamatot, és rögzítse a szükséges frissítési jogkivonatot.

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > A **New-PartnerAccessToken** paranccsal a **ServicePrincipal** paramétert használja a rendszer, mert a **web/API** típusú Azure ad-alkalmazás használatban van. Az ilyen típusú alkalmazásokhoz szükséges, hogy az ügyfél-azonosító és a titkos kulcs szerepeljen a hozzáférési jogkivonat kérelmében. A **Get-hitelesítőadat** parancs meghívásakor a rendszer kérni fogja a Felhasználónév és a jelszó megadását. Adja meg az alkalmazás azonosítóját felhasználónévként. Jelszóként adja meg az alkalmazás titkos kulcsát. A **New-PartnerAccessToken** parancs meghívásakor a rendszer kérni fogja a hitelesítő adatok újbóli megadását. Adja meg a használt szolgáltatásfiók hitelesítő adatait. Ennek a szolgáltatásfiók-fióknak megfelelő engedélyekkel rendelkező partnernek kell lennie.

3. Másolja a frissítési jogkivonat értékét.

    ```powershell
    $token.RefreshToken | clip
    ```

A frissítési jogkivonat értékét biztonságos tárházban kell tárolnia, például Azure Key Vault. A Secure Application modul PowerShell használatával történő kihasználása a [multi-Factor Authentication](/powershell/partnercenter/multi-factor-auth) című cikkben található.
