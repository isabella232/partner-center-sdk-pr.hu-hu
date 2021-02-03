---
title: Partnerközpont – hitelesítés
description: A partner Center az Azure AD-t használja a hitelesítéshez, a partner Center API-k használatához pedig helyesen kell konfigurálnia a hitelesítési beállításokat.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.openlocfilehash: 46ef9c6bc151c368281e943b7d24ebc07e34b66d
ms.sourcegitcommit: 64c498d3571f2287305968890578bc7396779621
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/19/2020
ms.locfileid: "97768688"
---
# <a name="partner-center-authentication"></a>Partnerközpont – hitelesítés

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A Partnerközpont az Azure Active Directoryt használja a hitelesítéshez. Amikor a Partner Center API-t, SDK-t vagy PowerShell-modult használja, megfelelően konfigurálnia kell egy Azure AD-alkalmazást, majd hozzáférési jogkivonatot kell kérnie. A partner központtal csak az alkalmazás vagy az App + felhasználói hitelesítés használatával kapott hozzáférési jogkivonatok használhatók. Két fontos elemet azonban figyelembe kell venni

- A többtényezős hitelesítés használata a partner Center API app + User hitelesítéssel történő elérésekor. A módosítással kapcsolatos további információkért lásd a [biztonságos alkalmazás modelljének engedélyezése](enable-secure-app-model.md)című témakört.

- A partner Center API nem támogatja az összes műveletet, csak a hitelesítést. Bizonyos esetekben az App + felhasználói hitelesítés használata szükséges. Az egyes [cikkek](scenarios.md) *előfeltételeinek* címsora alatt olyan dokumentációt talál, amely azt jelzi, hogy az alkalmazás csak hitelesítés, alkalmazás + felhasználó hitelesítése vagy mindkettő támogatott-e.

## <a name="initial-setup"></a>Kezdeti beállítás

1. A kezdéshez meg kell győződnie arról, hogy rendelkezik egy elsődleges partneri központ-fiókkal és egy integrációs homokozó-partneri központtal is. További információ: [a partner Center-fiókok beállítása API-hozzáféréshez](set-up-api-access-in-partner-center.md). Jegyezze fel az Azure HRE-alkalmazás regisztrációs AZONOSÍTÓját és a titkos kulcsot (az ügyfél titkos kulcsának megadása csak az alkalmazás azonosításához szükséges) az elsődleges fiókhoz és az integrációs sandbox-fiókhoz.

2. Jelentkezzen be az Azure AD-be a Azure Portalból. Az **egyéb alkalmazásokra vonatkozó engedélyekben** állítsa be a **Windows Azure Active Directory** jogosultságait a **delegált engedélyekre**, és válassza a **címtárhoz való hozzáférést a bejelentkezett felhasználóként** , majd **Jelentkezzen be és olvassa el a felhasználói profilt**.

3. A Azure Portalban **adja hozzá az alkalmazást**. Keressen rá a "Microsoft partner Center" kifejezésre, amely a Microsoft partner Center alkalmazás. Állítsa be a **delegált engedélyeket** a **partner Center API eléréséhez**. Ha a Microsoft Cloud Germany vagy a partner Center Microsoft Cloud az Egyesült Államok kormánya számára használ partner centert, ez a lépés kötelező. Ha a partner Center globális példányát használja, ez a lépés nem kötelező. A CSP-partnerek a partner Center portálon található app Management szolgáltatással hagyhatják el ezt a lépést a partner Center globális példánya számára.

## <a name="app-only-authentication"></a>Csak az alkalmazás hitelesítése

Ha csak az alkalmazáson belüli hitelesítést szeretné használni a partner Center REST API, a .NET API, a Java API vagy a PowerShell-modul eléréséhez, akkor az alábbi utasításokat kihasználva teheti meg.

## <a name="net-app-only-authentication"></a>.NET (csak alkalmazás hitelesítése)

```csharp
public static IAggregatePartner GetPartnerCenterTokenUsingAppCredentials()
{
    IPartnerCredentials partnerCredentials =
        PartnerCredentials.Instance.GenerateByApplicationCredentials(
            PartnerApplicationConfiguration.ApplicationId,
            PartnerApplicationConfiguration.ApplicationSecret,
            PartnerApplicationConfiguration.ApplicationDomain);

    // Create operations instance with partnerCredentials.
    return PartnerService.Instance.CreatePartnerOperations(partnerCredentials);
}
```

## <a name="java-app-only-authentication"></a>Java (csak az alkalmazás hitelesítése)

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

```java
public IAggregatePartner getAppPartnerOperations()
{
    IPartnerCredentials appCredentials =
        PartnerCredentials.getInstance().generateByApplicationCredentials(
        PartnerApplicationConfiguration.getApplicationId(),
        PartnerApplicationConfiguration.getApplicationSecret(),
        PartnerApplicationConfiguration.getApplicationDomain());

    return PartnerService.getInstance().createPartnerOperations( appCredentials );
}
```

## <a name="rest-app-only-authentication"></a>REST (csak az alkalmazás hitelesítése)

### <a name="rest-request"></a>REST-kérelem

```http
POST https://login.microsoftonline.com/{tenantId}/oauth2/token HTTP/1.1
Accept: application/json
return-client-request-id: true
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Host: login.microsoftonline.com
Content-Length: 194
Expect: 100-continue

resource=https%3A%2F%2Fgraph.windows.net&client_id={client-id-here}&client_secret={client-secret-here}&grant_type=client_credentials
```

### <a name="rest-response"></a>REST-válasz

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a>Alkalmazás + felhasználói hitelesítés

A rendszer az [erőforrás-tulajdonosi jelszó hitelesítő adatainak megadását](https://tools.ietf.org/html/rfc6749#section-4.3) használta a Partner Center REST API, a .NET API, a Java API vagy a PowerShell-modul használatához szükséges hozzáférési jogkivonat igényléséhez. Ezt a módszert használták hozzáférési token igénylésére a Azure Active Directory ügyfél-azonosító és felhasználói hitelesítő adatok használatával. Ez a megközelítés azonban többé nem fog működni, mivel a partneri központ többtényezős hitelesítést igényel az alkalmazás és a felhasználó hitelesítésének használatakor. Ahhoz, hogy megfeleljen ennek a követelménynek, a Microsoft egy biztonságos, méretezhető keretrendszert vezetett be a Cloud Solution Provider (CSP) partnerek és a Vezérlőpult-szállítók (CPV) többtényezős hitelesítés használatával történő hitelesítéséhez. Ezt a keretrendszert a biztonságos alkalmazás modelljének nevezzük, amely egy engedélyezési folyamatból és egy hozzáférési tokenre vonatkozó kérelemből áll, amely frissítési tokent használ.

### <a name="partner-consent"></a>Partneri beleegyezett

A partneri hozzájárulási folyamat egy interaktív folyamat, amelyben a partner a többtényezős hitelesítés használatával hitelesíti a hitelesítést, jóváhagyja az alkalmazást, és egy frissítési tokent biztonságos tárházban (például Azure Key Vault) tárolja. Javasoljuk, hogy ehhez a folyamathoz egy dedikált fiókot kell használni integrációs célokra.

> [!IMPORTANT]
> A megfelelő multi-Factor Authentication megoldást engedélyezni kell a partneri engedélyezési folyamat során használt szolgáltatásfiók számára. Ha nem, akkor az eredményül kapott frissítési jogkivonat nem fog megfelelni a biztonsági követelményeknek.

### <a name="samples-for-app--user-authentication"></a>Minták az App + felhasználói hitelesítéshez

A partneri engedélyezési folyamat számos módon elvégezhető. Annak érdekében, hogy a partnerek megértsék az egyes szükséges műveletek elvégzését, a következő mintákat fejlesztettük ki. Ha a megfelelő megoldást alkalmazza a környezetében, fontos, hogy olyan megoldást fejlesszen ki, amely a kódolási szabványokkal és biztonsági házirendekkel kapcsolatos.

## <a name="net-appuser-authentication"></a>.NET (alkalmazás + felhasználói hitelesítés)

A [partneri](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) belefoglalási minta projekt bemutatja, hogyan használhatja a ASP.NET használatával kifejlesztett webhelyeket a belefoglalási engedély rögzítéséhez, a frissítési token igényléséhez és a Azure Key Vault biztonságos tárolásához. A következő lépések végrehajtásával hozza létre a minta szükséges előfeltételeit.

1. Hozzon létre egy Azure Key Vault példányt a Azure Portal vagy a következő PowerShell-parancsok használatával. A parancs végrehajtása előtt ügyeljen arra, hogy a paraméterek értékét ennek megfelelően módosítsa. A tár nevének egyedinek kell lennie.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    A Azure Key Vault létrehozásával kapcsolatos további információkért lásd [: gyors üzembe helyezés és a titkos kód beolvasása Azure Key Vault használatával a Azure Portal vagy a](/azure/key-vault/quick-create-portal) gyors útmutató: a [PowerShell használatával állítsa be és kérje le a Azure Key Vault titkos kulcsot](/azure/key-vault/quick-create-powershell). Ezután állítson be és kérjen le egy titkos kulcsot.

2. Hozzon létre egy Azure AD-alkalmazást és egy kulcsot a Azure Portal vagy az alábbi parancsok használatával.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Ügyeljen arra, hogy jegyezze fel az alkalmazás azonosítóját és a titkos értékeket, mivel ezeket az alábbi lépésekben fogjuk használni.

3. Adja meg az újonnan létrehozott Azure AD-alkalmazást az Azure Portal vagy a következő parancsok használatával a titkok olvasása engedélyekkel.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Hozzon létre egy, a partner Centerhez konfigurált Azure AD-alkalmazást. A lépés végrehajtásához hajtsa végre a következő műveleteket.

    - Tallózással keresse meg a partner Center irányítópultjának [app Management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) szolgáltatását
    - Az új Azure AD-alkalmazás létrehozásához kattintson az *új webalkalmazás hozzáadása* elemre.

    Ügyeljen arra, hogy az *alkalmazás azonosítóját*, a * fiók azonosítóját * * és a *kulcs* értékeit dokumentálja, mert ezek az alábbi lépésekben lesznek felhasználva.

5. A [partner-központ-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) adattár klónozása a Visual Studióval vagy a következő paranccsal.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. Nyissa meg a címtárban található *PartnerConsent* projektet `Partner-Center-DotNet-Samples\secure-app-model\keyvault` .

7. A [web.configban](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config) található Alkalmazásbeállítások feltöltése

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!--
        Endpoint address for the instance of Azure KeyVault. This is
        the DNS Name for the instance of Key Vault that you provisioned.
     -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- App ID that is given access for KeyVault to store refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate
        to your environment. The following application secret is for sample
        application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

    > [!IMPORTANT]
    > A bizalmas adatokat, például az alkalmazás-titkokat nem szabad a konfigurációs fájlokban tárolni. Itt azért történt, mert ez egy minta alkalmazás. Éles környezetben erősen ajánlott tanúsítványalapú hitelesítést használni. További információ: [tanúsítvány hitelesítő adatai az alkalmazás hitelesítéséhez]( /azure/active-directory/develop/active-directory-certificate-credentials).

8. A minta projekt futtatásakor a rendszer felszólítja a hitelesítésre. A sikeres hitelesítés után a rendszer egy hozzáférési jogkivonatot kér az Azure AD-től. Az Azure AD által visszaadott adatok közé tartozik a Azure Key Vault konfigurált példányán tárolt frissítési jogkivonat.

## <a name="java-appuser-authentication"></a>Java (alkalmazás + felhasználói hitelesítés)

A [partneri](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) belefoglalási minta projekt bemutatja, hogyan használhatók a JSP használatával fejlesztett webhelyek a belefoglalási engedély rögzítése, a frissítési token igénylése és a biztonságos tár Azure Key Vault. A következő művelet végrehajtásával hozza létre a minta szükséges előfeltételeit.

1. Hozzon létre egy Azure Key Vault példányt a Azure Portal vagy a következő PowerShell-parancsok használatával. A parancs végrehajtása előtt ügyeljen arra, hogy a paraméterek értékét ennek megfelelően módosítsa. A tár nevének egyedinek kell lennie.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    A Azure Key Vault létrehozásával kapcsolatos további információkért lásd [: gyors üzembe helyezés és a titkos kód beolvasása Azure Key Vault használatával a Azure Portal vagy a](/azure/key-vault/quick-create-portal) gyors útmutató: a [PowerShell használatával állítsa be és kérje le a Azure Key Vault titkos kulcsot](/azure/key-vault/quick-create-powershell).

2. Hozzon létre egy Azure AD-alkalmazást és egy kulcsot a Azure Portal vagy az alábbi parancsok használatával.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Ügyeljen arra, hogy dokumentálja az alkalmazás azonosítóját és a titkos értékeket, mivel ezeket az alábbi lépésekben fogjuk használni.

3. Adja meg az újonnan létrehozott Azure AD-alkalmazást az Azure Portal vagy a következő parancsok használatával a titkok olvasása engedélyekkel.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Hozzon létre egy, a partner Centerhez konfigurált Azure AD-alkalmazást. A lépés végrehajtásához hajtsa végre az alábbi lépéseket.

    - Tallózással keresse meg a partner Center irányítópultjának [app Management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) szolgáltatását
    - Az új Azure AD-alkalmazás létrehozásához kattintson az *új webalkalmazás hozzáadása* elemre.

    Ügyeljen arra, hogy az *alkalmazás azonosítóját*, a * fiók azonosítóját * * és a *kulcs* értékeit dokumentálja, mert ezek az alábbi lépésekben lesznek felhasználva.

5. A [partner-központ-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) adattár klónozása az alábbi paranccsal

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. Nyissa meg a címtárban található *PartnerConsent* projektet `Partner-Center-Java-Samples\secure-app-model\keyvault` .

7. Az [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) fájlban található Alkalmazásbeállítások feltöltése

    ```xml
    <filter>
        <filter-name>AuthenticationFilter</filter-name>
        <filter-class>com.microsoft.store.samples.partnerconsent.security.AuthenticationFilter</filter-class>
        <init-param>
            <param-name>client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_base_url</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_certifcate_path</param-name>
            <param-value></param-value>
        </init-param>
    </filter>
    ```

    > [!IMPORTANT]
    > A bizalmas adatokat, például az alkalmazás titkos adatait nem szabad a konfigurációs fájlokban tárolni. Itt azért történt, mert ez egy minta alkalmazás. Éles környezetben a tanúsítvány alapú hitelesítés használatát javasoljuk. További információ: [Key Vault tanúsítványalapú hitelesítés](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).

8. A minta projekt futtatásakor a rendszer felszólítja a hitelesítésre. A sikeres hitelesítés után a rendszer egy hozzáférési jogkivonatot kér az Azure AD-től. Az Azure AD által visszaadott adatok közé tartozik a Azure Key Vault konfigurált példányán tárolt frissítési jogkivonat.

## <a name="cloud-solution-provider-authentication"></a>Felhőalapú megoldás-szolgáltató hitelesítése

A felhőalapú megoldás-szolgáltató partnerei használhatják a [partneri engedélyezési](#partner-consent) folyamat során beszerzett frissítési jogkivonatot.

### <a name="samples-for-cloud-solution-provider-authentication"></a>Minták a felhőalapú megoldás-szolgáltató hitelesítéséhez

Annak érdekében, hogy a partnerek megértsék az egyes szükséges műveletek elvégzését, a következő mintákat fejlesztettük ki. Ha a megfelelő megoldást alkalmazza a környezetében, fontos, hogy olyan megoldást fejlesszen ki, amely a kódolási szabványokkal és biztonsági házirendekkel kapcsolatos.

## <a name="net-csp-authentication"></a>.NET (CSP hitelesítés)

1. Ha még nem tette meg, hajtsa végre a [partneri engedélyezési folyamatot](#partner-consent).

2. A [partner-központ-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) adattár klónozása a Visual Studio vagy a következő parancs használatával

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Nyissa meg a `CSPApplication` `Partner-Center-DotNet-Samples\secure-app-model\keyvault` címtárban található projektet.

4. Frissítse az [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) fájlban található Alkalmazásbeállítások közül.

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. Állítsa be a [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) fájlban található **PartnerId** és **Vevőkód** változók megfelelő értékeit.

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Ha ezt a mintát futtatja, a beolvassa a partneri engedélyezési folyamat során beszerzett frissítési jogkivonatot. Ezt követően hozzáférési tokent kér a partner Center SDK-val kapcsolatban a partner nevében. Végezetül pedig hozzáférési tokent kér, hogy a megadott ügyfél nevében kommunikáljon Microsoft Graph.

## <a name="java-csp-authentication"></a>Java (CSP hitelesítés)

1. Ha még nem tette meg, hajtsa végre a [partneri engedélyezési folyamatot](#partner-consent).

2. A [partner-központ-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) adattár klónozása a Visual Studióval vagy a következő paranccsal

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Nyissa meg a `cspsample` `Partner-Center-Java-Samples\secure-app-model\keyvault` címtárban található projektet.

4. Frissítse az [alkalmazás. properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) fájljában található Alkalmazásbeállítások közül.

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. Ha ezt a mintát futtatja, a beolvassa a partneri engedélyezési folyamat során beszerzett frissítési jogkivonatot. Ezt követően hozzáférési tokent kér a partner Center SDK-val kapcsolatban a partner nevében.

6. Nem kötelező – a *RunAzureTask* és a *RunGraphTask* függvény meghívása, ha szeretné megtekinteni, hogyan lehet kommunikálni Azure Resource Manager és Microsoft Graph az ügyfél nevében.

## <a name="control-panel-provider-authentication"></a>Vezérlőpult-szolgáltató hitelesítése

A Vezérlőpult-gyártóknak az általuk támogatott partnerekkel kell rendelkezniük a [partneri beleegyező](#partner-consent) folyamat végrehajtásához. Ha a művelet befejeződött, a rendszer az adott folyamaton keresztül beszerzett frissítési tokent használja a partner Center REST API és a .NET API eléréséhez.

### <a name="samples-for-cloud-panel-provider-authentication"></a>Minták a Cloud panel szolgáltatójának hitelesítéséhez

Annak érdekében, hogy a Vezérlőpult gyártói hogyan tudják elvégezni az egyes szükséges műveleteket, a következő mintákat fejlesztettük ki. Ha a megfelelő megoldást alkalmazza a környezetében, fontos, hogy olyan megoldást fejlesszen ki, amely a kódolási szabványokkal és biztonsági házirendekkel kapcsolatos.

## <a name="net-cpv-authentication"></a>.NET (CPV-hitelesítés)

1. Dolgozzon ki és helyezzen üzembe egy folyamatot a felhőalapú megoldás-szolgáltató partnerei számára a megfelelő engedély megadásához. További információ: [partneri beleegyezett](#partner-consent).

    > [!IMPORTANT]
    > A felhőalapú megoldás-szolgáltatói partnertől származó felhasználói hitelesítő adatokat nem szabad tárolni. A partneri engedélyezési folyamat során beszerzett frissítési tokent a Microsoft API-k használatával való interakcióhoz szükséges hozzáférési jogkivonatok igénylésére kell tárolni.

2. A [partner-központ-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) adattár klónozása a Visual Studio vagy a következő parancs használatával

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Nyissa meg a `CPVApplication` `Partner-Center-DotNet-Samples\secure-app-model\keyvault` címtárban található projektet.

4. Frissítse az [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) fájlban található Alkalmazásbeállítások közül.

    ```xml
    <!-- AppID that represents Control panel vendor application -->
    <add key="ida:CPVApplicationId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CPVApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. Állítsa be a [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) fájlban található **PartnerId** és **Vevőkód** változók megfelelő értékeit.

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Ha ezt a mintát futtatja, az beolvassa a megadott partner frissítési jogkivonatát. Ezután hozzáférési jogkivonatot kér a partneri központ és az Azure AD Graph eléréséhez a partner nevében. A következő feladat az, hogy az engedélyek törlését és létrehozását engedélyezi az ügyfél bérlője számára. Mivel a Vezérlőpult gyártója és az ügyfél között nincs kapcsolat, ezeket az engedélyeket hozzá kell adni a partner Center API-val. Az alábbi példa azt szemlélteti, hogyan valósítható meg.

    ```csharp
    JObject contents = new JObject
    {
        // Provide your application display name
        ["displayName"] = "CPV Marketplace",

        // Provide your application id
        ["applicationId"] = CPVApplicationId,

        // Provide your application grants
        ["applicationGrants"] = new JArray(
            JObject.Parse("{\"enterpriseApplicationId\": \"00000002-0000-0000-c000-000000000000\", \"scope\":\"Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All\"}"), // for Azure AD Graph access,  Directory.Read.All
            JObject.Parse("{\"enterpriseApplicationId\": \"797f4846-ba00-4fd7-ba43-dac1f8f63013\", \"scope\":\"user_impersonation\"}")) // for Azure Resource Manager access
    };

    /**
     * The following steps have to be performed once per customer tenant if your application is
     * a control panel vendor application and requires customer tenant Azure AD Graph access.
     **/

    // delete the previous grant into customer tenant
    JObject consentDeletion = await ApiCalls.DeleteAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents/{1}", CustomerId, CPVApplicationId));

    // create new grants for the application given the setting in application grants payload.
    JObject consentCreation = await ApiCalls.PostAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents", CustomerId),
        contents.ToString());
    ```

Az engedélyek létrejötte után a minta az ügyfél nevében hajt végre műveleteket az Azure AD Graph használatával.

## <a name="java-cpv-authentication"></a>Java (CPV-hitelesítés)

1. Dolgozzon ki és helyezzen üzembe egy folyamatot a felhőalapú megoldás-szolgáltató partnerei számára a megfelelő engedély megadásához. További információkat és példákat a [partneri megállapodásban](#partner-consent)talál.

    > [!IMPORTANT]
    > A felhőalapú megoldás-szolgáltatói partnertől származó felhasználói hitelesítő adatokat nem szabad tárolni. A partneri engedélyezési folyamat során beszerzett frissítési tokent a Microsoft API-k használatával való interakcióhoz szükséges hozzáférési jogkivonatok igénylésére kell tárolni.

2. A [partner-központ-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) adattár klónozása az alábbi paranccsal

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Nyissa meg a `cpvsample` `Partner-Center-Java-Samples\secure-app-model\keyvault` címtárban található projektet.

4. Frissítse az [alkalmazás. properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) fájljában található Alkalmazásbeállítások közül.

    ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    partnercenter.displayName=
    ```

    A értékének a `partnercenter.displayName` Marketplace-alkalmazás megjelenítendő nevének kell lennie.

5. Állítsa be a [program. Java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) fájljában található **partnerId** és **Vevőkód** változók megfelelő értékeit.

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. Ha ezt a mintát futtatja, az beolvassa a megadott partner frissítési jogkivonatát. Ezt követően hozzáférési jogkivonatot kér a partner központhoz való hozzáféréshez a partner nevében. A következő feladat az, hogy az engedélyek törlését és létrehozását engedélyezi az ügyfél bérlője számára. Mivel a Vezérlőpult gyártója és az ügyfél között nincs kapcsolat, ezeket az engedélyeket hozzá kell adni a partner Center API-val. Az alábbi példa az engedélyek megadását mutatja be.

    ```java
    ApplicationGrant azureAppGrant = new ApplicationGrant();

    azureAppGrant.setEnterpriseApplication("797f4846-ba00-4fd7-ba43-dac1f8f63013");
    azureAppGrant.setScope("user_impersonation");

    ApplicationGrant graphAppGrant = new ApplicationGrant();

    graphAppGrant.setEnterpriseApplication("00000002-0000-0000-c000-000000000000");
    graphAppGrant.setScope("Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All");

    ApplicationConsent consent = new ApplicationConsent();

    consent.setApplicationGrants(Arrays.asList(azureAppGrant, graphAppGrant));
    consent.setApplicationId(properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID));
    consent.setDisplayName(properties.getProperty(PropertyName.PARTNER_CENTER_DISPLAY_NAME));

    // Deletes the existing grant into the customer it is present.
    partnerOperations.getServiceClient().delete(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents/{1}",
            customerId,
            properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID)));

    // Consent to the defined applications and the respective scopes.
    partnerOperations.getServiceClient().post(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents",
            customerId),
        consent);
    ```

Ha szeretné megtekinteni a *RunAzureTask* és a *RunGraphTask* függvényt, ha meg szeretné tekinteni, hogyan lehet kommunikálni a Azure Resource Manager és Microsoft Graph az ügyfél nevében.
