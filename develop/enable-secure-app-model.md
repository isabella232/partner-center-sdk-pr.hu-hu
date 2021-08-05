---
title: Biztonságos alkalmazásmodell engedélyezése
description: Biztonságossá Partnerközpont és a vezérlőpult alkalmazásait.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36a81c7b235c68e49bb425b5bd0d4615882f88ef
ms.sourcegitcommit: 07b9a11f5c615ed1e716081392032cea2124bd98
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/04/2021
ms.locfileid: "115104210"
---
# <a name="enabling-the-secure-application-model-framework"></a>A biztonságos alkalmazásmodellek keretrendszerének engedélyezése

A Microsoft egy biztonságos, skálázható keretrendszert vezet be a felhőszolgáltató (CSP) partnerek és a vezérlőpult-szállítók (CPV) hitelesítéséhez a Microsoft Azure Active Directory Multi-Factor Authentication (MFA) architektúrával.

Az új modell használatával megemelheti a biztonsági szinteket az Partnerközpont API-integrációs hívásokhoz. Ez segít az összes félnek (beleértve a Microsoftot, a CSP-partnereket és a CPV-ket) az infrastruktúra és az ügyféladatok biztonsági kockázatokkal szembeni védelmében.

## <a name="scope"></a>Hatókör

Ez a cikk a következő a szereplőkkel kapcsolatos:

- CPV-k
  - A CPV-k olyan független szoftverszállítók, amelyek a CSP-partnerek által a Partner Center API-kkal való integrációhoz használható alkalmazásokat fejlesztenek.
  - A CPV-k nem olyan CSP-partnerek, amelyek közvetlen hozzáféréssel rendelkeznek a Partnerközpont irányítópultjához vagy az API-khoz.

- Közvetett CSP-szolgáltatók és közvetlen CSP-partnerek, akik alkalmazásazonosítót és felhasználóhitelesítést alkalmaznak, és közvetlenül integrálják Partnerközpont API-kkal.

## <a name="security-requirements"></a>Biztonsági követelmények

A biztonsági követelményekkel kapcsolatos részletekért lásd: [Partnerbiztonsági követelmények.](/partner-center/partner-security-requirements)

## <a name="secure-application-model"></a>biztonságos alkalmazásmodell

A Marketplace-alkalmazásoknak CSP-partneri jogosultságokat kell megszemélyesülni a Microsoft API-k meghívása érdekében. Az ilyen bizalmas alkalmazások elleni biztonsági támadások az ügyféladatok biztonságának veszélyeztetése esetén vezethetnek.

Az új hitelesítési keretrendszer áttekintéséhez és részleteihez töltse le a [biztonságos alkalmazásmodell keretrendszer dokumentumát.](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) Ez a dokumentum olyan alapelveket és ajánlott eljárásokat fed le, amelyek segítségével fenntarthatóvá és robusztusvá tehetik a piactéri alkalmazásokat a biztonsági rések ellen.

## <a name="samples"></a>Példák

A következő áttekintő dokumentumok és mintakódok ismertetik, hogyan valósítják meg a partnerek a biztonságos alkalmazásmodell keretrendszert:

- [CPV áttekintő dokumentum](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [A CSP áttekintő dokumentuma](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [.NET-minták](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Java-minták](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [REST-utasítások és -minták](#rest)
- [PowerShell-utasítások és -minták](#powershell)

## <a name="rest"></a>REST

Ha REST-hívásokat biztonságos alkalmazásmodell a mintakóddal, kövesse az alábbi lépéseket:

1. [Webalkalmazás létrehozása](#create-a-web-app)

2. [Engedélyezési kód le kérése](#get-authorization-code)

3. [Frissítési jogkivonat beszerzése](#get-refresh-token)

4. [Hozzáférési jogkivonat lekérése](#get-access-token)

5. [Partner Center API-hívás kezdeményezése](#make-partner-center-api-calls)

> [!TIP]
> A PowerShell-Partnerközpont használatával lekért egy engedélyezési kódot és egy frissítési jogkivonatot. Ezt a lehetőséget a 2. és a 3. lépés után választhatja. További információkért tekintse meg a [PowerShell szakaszt és példákat.](#powershell)

### <a name="create-a-web-app"></a>Webalkalmazás létrehozása

REST-hívások előtt létre kell hoznia és regisztrálnia Partnerközpont webalkalmazást.

1. Jelentkezzen be az [Azure Portalra](https://portal.azure.com).

2. Hozzon létre Azure Active Directory (Azure AD) alkalmazást.

3. Adjon delegált alkalmazásengedélyeket a következő erőforrásoknak az alkalmazás *követelményeitől függően.* Szükség esetén további delegált engedélyeket adhat hozzá az alkalmazás-erőforrásokhoz.

   1. **Microsoft Partnerközpont** (egyes bérlők **sampleBECApp** alkalmazásként mutatják be)

   2. **Azure Management API-k** (ha az Azure API-k meghívását tervezi)

   3. **Microsoft Azure Active Directory**

4. Győződjön meg arról, hogy az alkalmazás kezdőlapjának URL-címe egy olyan végpontra van beállítva, ahol egy élő webalkalmazás fut. Az alkalmazásnak el [](#get-authorization-code) kell fogadnia az Azure AD bejelentkezési hívásból származó engedélyezési kódot. A következő szakaszban található [példakódban](#get-authorization-code)például a webalkalmazás a következő webhelyen fut: `https://localhost:44395/` .

5. Jegyezze fel a következő információkat a webalkalmazás Azure AD-beállításaiból:

   - Alkalmazásazonosító
   - Alkalmazás titkos kódja

> [!NOTE]
> Javasoljuk, hogy [a tanúsítványt használja titkos alkalmazás titkos ként.](/azure/active-directory/develop/active-directory-certificate-credentials) Azonban alkalmazáskulcsot is létrehozhat a Azure Portal. A következő szakaszban található [mintakód egy](#get-authorization-code) alkalmazáskulcsot használ.

### <a name="get-authorization-code"></a>Hozzáférési kód lekérése

Az Azure AD bejelentkezési hívásból való elfogadáshoz be kell szereznie egy engedélyezési kódot a webalkalmazáshoz:

1. Jelentkezzen be az Azure AD-be a következő URL-címen: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) . Jelentkezzen be azzal a felhasználói fiókkal, amelyről API Partnerközpont hívásokat fog kezdeményezni (például rendszergazdai ügynök vagy értékesítési ügynök fiókja).

2. Cserélje **le az Application-Id** (Alkalmazásazonosító) helyére az Azure AD-alkalmazás azonosítóját (GUID).

3. Amikor a rendszer kéri, jelentkezzen be a felhasználói fiókjával, konfigurált MFA-val.

4. Amikor a rendszer kéri, adjon meg további MFA-adatokat (telefonszám vagy e-mail-cím) a bejelentkezés ellenőrzéséhez.

5. Miután bejelentkezett, a böngésző átirányítja a hívást a webalkalmazás végpontjára az engedélyezési kóddal. A következő mintakód például a következőre mutat: `https://localhost:44395/` .

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

### <a name="get-refresh-token"></a>Frissítési jogkivonat beszerzése

Ezután az engedélyezési kóddal le kell szereznie egy frissítési jogkivonatot:

1. Az engedélyezési kóddal post hívást kell hívni az Azure AD bejelentkezési `https://login.microsoftonline.com/CSPTenantID/oauth2/token` végpontra. Példaként tekintse meg a következő [mintahívást:](#sample-refresh-call).

2. Jegyezze fel a visszaadott frissítési jogkivonatot.

3. Tárolja a frissítési jogkivonatot a Azure Key Vault. További információt a Key Vault [API dokumentációjában talál.](/rest/api/keyvault/)

> [!IMPORTANT]
> A frissítési jogkivonatot [titkos kulcsként kell tárolni](/rest/api/keyvault/setsecret/setsecret) a Key Vaultban.

#### <a name="sample-refresh-call"></a>Példa frissítési hívásra

Helyőrző kérés:

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

Helyőrző válasz:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Válasz törzse:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a>Hozzáférési jogkivonat beszerzése

Mielőtt hívásokat kezdeményezhet a Partnerközpont API-khoz, be kell szereznie egy hozzáférési jogkivonatot. A hozzáférési jogkivonat beszerzéséhez frissítési jogkivonatot kell használnia, mivel a hozzáférési jogkivonatok élettartama általában nagyon korlátozott (például egy óránál rövidebb).

Helyőrző kérés:

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

Helyőrző válasz:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Válasz törzse:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a>API Partnerközpont hívások

A hozzáférési jogkivonatot kell használnia a Partnerközpont API-k meghívása érdekében. Lásd az alábbi példahívást.

#### <a name="example-partner-center-api-call"></a>Példa Partnerközpont API-hívásra

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Az Partnerközpont [PowerShell-modullal](https://www.powershellgallery.com/packages/PartnerCenter) csökkentheti a hozzáférési jogkivonat engedélyezési kódjának cseréjéhez szükséges infrastruktúrát. Ez a metódus nem kötelező a [REST Partnerközpont hívások készítésnél.](#rest)

További információ erről a folyamatról: [Biztonságos alkalmazásmodell](/powershell/partnercenter/secure-app-model) PowerShell-dokumentáció.

1. Telepítse az Azure AD-t, és Partnerközpont PowerShell-modulokat.

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. A **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** paranccsal hajtsa végre a hozzájárulási folyamatot, és rögzítse a szükséges frissítési jogkivonatot.

    ```powershell
    $credential = Get-Credential

    $token = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > A **ServicePrincipal** paramétert a **New-PartnerAccessToken** paranccsal együtt használjuk, mert a rendszer egy **Web/API típusú** Azure AD-alkalmazást használ. Az ilyen típusú alkalmazás megköveteli, hogy a hozzáférési jogkivonat kérése tartalmazni fog egy ügyfél-azonosítót és egy titkos secret-et. A **Get-Credential** parancs meghívatáskor a rendszer felkéri, hogy adjon meg egy felhasználónevet és egy jelszót. Felhasználónévként adja meg az alkalmazásazonosítót. Jelszóként adja meg az alkalmazás titkos jelszavát. A **New-PartnerAccessToken** parancs meghívatáskor a rendszer újra kérni fogja a hitelesítő adatok megadását. Adja meg a használt szolgáltatásfiók hitelesítő adatait. Ennek a szolgáltatásfióknak megfelelő engedélyekkel rendelkező partnerfióknak kell lennie.

3. Másolja ki a frissítési jogkivonat értékét.

    ```powershell
    $token.RefreshToken | clip
    ```

A frissítési jogkivonat értékét egy biztonságos adattárban kell tárolni, például egy Azure Key Vault. A biztonságos alkalmazásmodul PowerShell-rel való használatával kapcsolatos további információkért tekintse meg a [többtényezős hitelesítéssel kapcsolatos cikket.](/powershell/partnercenter/multi-factor-auth)
