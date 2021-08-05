---
title: Partnerközpont – hitelesítés
description: Partnerközpont Azure AD-t használ a hitelesítéshez, az Partnerközpont API-khoz pedig megfelelően kell konfigurálnia a hitelesítési beállításokat.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 75d60ca983cd5b8fe53134ec7481319b153e128a
ms.sourcegitcommit: 07b9a11f5c615ed1e716081392032cea2124bd98
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/04/2021
ms.locfileid: "115104193"
---
# <a name="partner-center-authentication"></a>Partnerközpont – hitelesítés

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A Partnerközpont az Azure Active Directoryt használja a hitelesítéshez. Amikor a Partner Center API-t, SDK-t vagy PowerShell-modult használja, megfelelően konfigurálnia kell egy Azure AD-alkalmazást, majd hozzáférési jogkivonatot kell kérnie. A csak alkalmazással vagy alkalmazás+ felhasználóhitelesítéssel kapott hozzáférési jogkivonatok használhatók a Partnerközpont. Van azonban két fontos elem, amit figyelembe kell venni

- Többtényezős hitelesítés használata a Partnerközpont API alkalmazás- és felhasználóhitelesítéssel való elérésekor. További információ erről a változásról: [Biztonságos alkalmazásmodell engedélyezése.](enable-secure-app-model.md)

- A Partnerközpont API nem támogatja az alkalmazások hitelesítését. Bizonyos esetekben alkalmazás- és felhasználóhitelesítést kell használnia. Az egyes *cikk Előfeltételek* fejléce alatt találja a dokumentációt, [](scenarios.md)amely azt jelzi, hogy csak az alkalmazás hitelesítése, az alkalmazás és a felhasználó hitelesítése támogatott-e, vagy mindkettő támogatott.

## <a name="initial-setup"></a>Kezdeti beállítás

1. Először is győződjön meg arról, hogy elsődleges Partnerközpont fiókkal és integrációs Partnerközpont fiókkal. További információ: [Set up Partnerközpont accounts for API access (Api Partnerközpont fiókok beállítása.](set-up-api-access-in-partner-center.md) Jegyezze fel az Azure AAD-alkalmazás regisztrációs azonosítóját és titkos kulcsát (csak az alkalmazás azonosításához szükséges titkos ügyfélkét) az elsődleges fiókhoz és az integrációs védőfalhoz is.

2. Jelentkezzen be az Azure AD-be a Azure Portal. A **más alkalmazásokra** vonatkozó engedélyekben  állítsa a Windows Azure Active Directory engedélyét Delegált engedélyekre, és jelölje be a **Hozzáférés** a címtárhoz bejelentkezett felhasználóként és a Bejelentkezés és felhasználói profil olvasása **lehetőséget.**

3. A Azure Portal adja **hozzá az alkalmazást.** Keressen rá a "Microsoft Partnerközpont" kifejezésre, amely a Microsoft Partnerközpont alkalmazás. Állítsa a **Delegált engedélyeket** **hozzáférési Partnerközpont API-hoz.** Ha a Microsoft Cloud Germany Partnerközpont vagy Partnerközpont-Microsoft Cloud for US Government használ, ez a lépés kötelező. Ha globális példányt Partnerközpont használ, ez a lépés nem kötelező. A CSP-partnerek a Partnerközpont portál Alkalmazáskezelés funkcióját használva megkerülhetik ezt a lépést Partnerközpont globális példányon.

## <a name="app-only-authentication"></a>Csak alkalmazáshitelesítés

Ha csak alkalmazásos hitelesítést szeretne használni a Partnerközpont REST API, a .NET API, a Java API vagy a PowerShell modul eléréséhez, akkor ezt az alábbi utasítások segítségével tegye meg.

## <a name="net-app-only-authentication"></a>.NET (csak alkalmazáson belüli hitelesítés)

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

## <a name="java-app-only-authentication"></a>Java (csak alkalmazáson belüli hitelesítés)

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

## <a name="rest-app-only-authentication"></a>REST (csak alkalmazáson belüli hitelesítés)

### <a name="rest-request"></a>REST-kérés

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

## <a name="app--user-authentication"></a>Alkalmazás és felhasználó hitelesítése

Korábban az [](https://tools.ietf.org/html/rfc6749#section-4.3) erőforrás-tulajdonosi hitelesítő adatok megadását használták arra, hogy hozzáférési jogkivonatot kérjenek a Partnerközpont REST API, .NET API, Java API vagy PowerShell modullal való használathoz. Ezzel a módszerrel hozzáférési jogkivonatot kért Azure Active Directory ügyfél-azonosító és felhasználói hitelesítő adatok használatával. Ez a megközelítés azonban nem fog működni, Partnerközpont többtényezős hitelesítést igényel az alkalmazás és a felhasználó hitelesítése során. Ennek a követelménynek a teljesítéséhez a Microsoft biztonságos, skálázható keretrendszert vezetett be a Felhőszolgáltató-partnerek és a vezérlőpult-szállítók (CPV) többtényezős hitelesítéssel való hitelesítéséhez. Ez a keretrendszer az úgynevezett biztonságos alkalmazásmodell, és egy hozzájárulási folyamatból és egy hozzáférési jogkivonat frissítési jogkivonattal való hozzáférési jogkivonatra vonatkozó kérésből áll.

### <a name="partner-consent"></a>Partneri jóváhagyás

A partner hozzájárulási folyamata egy interaktív folyamat, amelyben a partner többtényezős hitelesítéssel hitelesít, elfogadja az alkalmazást, és egy frissítési jogkivonatot tárol egy biztonságos adattárban, például a Azure Key Vault. Javasoljuk, hogy ehhez a folyamathoz egy dedikált fiókot kell használni az integrációhoz.

> [!IMPORTANT]
> Engedélyezni kell a megfelelő többtényezős hitelesítési megoldást a partner-hozzájárulási folyamatban használt szolgáltatásfiókhoz. Ha nem, akkor az eredményül kapott frissítési jogkivonat nem fog megfelelni a biztonsági követelményeknek.

### <a name="samples-for-app--user-authentication"></a>Minták alkalmazás- és felhasználóhitelesítéshez

A partneri hozzájárulási folyamat többféleképpen is elvégezhető. A következő mintákat fejlesztettük ki, hogy segítsen a partnereknek megérteni az egyes szükséges műveletek elvégzésének mikéntját. Amikor a megfelelő megoldást implementálja a környezetében, fontos, hogy olyan megoldást fejlessze ki, amely megfelel a kódolási szabványoknak és a biztonsági szabályzatoknak.

## <a name="net-appuser-authentication"></a>.NET (alkalmazás+felhasználói hitelesítés)

A [partneri hozzájárulási](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) mintaprojekt bemutatja, hogyan használhatja a ASP.NET használatával fejlesztett webhelyet a hozzájárulás rögzítésére, frissítési jogkivonat kérésére és biztonságos tárolására a Azure Key Vault. A mintához szükséges előfeltételek létrehozásához hajtsa végre az alábbi lépéseket.

1. Hozza létre a Azure Key Vault egy példányát a Azure Portal vagy az alábbi PowerShell-parancsokkal. A parancs végrehajtása előtt ennek megfelelően módosítsa a paraméterértékeket. A tároló nevének egyedinek kell lennie.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    További információ a Azure Key Vault létrehozásáról: Rövid [útmutató:](/azure/key-vault/quick-create-portal) Titkos adat beállítása és lekérése az Azure Key Vault-ból a Azure Portal vagy rövid útmutató: Titkos adat beállítása és lekérése a Azure Key Vault-ból [a PowerShell](/azure/key-vault/quick-create-powershell)használatával. Ezután állítson be és lekér egy titkos adatokat.

2. Hozzon létre egy Azure AD-alkalmazást és egy kulcsot a Azure Portal vagy az alábbi parancsokkal.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Jegyezze fel az alkalmazásazonosítót és a titkos értékeket, mert az alábbi lépésekben használni fogja őket.

3. Adja meg az újonnan létrehozott Azure AD-alkalmazásnak a titkos kulcsok olvasására vonatkozó engedélyeket a Azure Portal vagy az alábbi parancsokkal.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Hozzon létre egy Azure AD-alkalmazást, amely a Partnerközpont. A lépés végrehajtásához hajtsa végre a következő műveleteket.

    - Keresse meg [az](https://partner.microsoft.com/pcv/apiintegration/appmanagement) irányítópult Alkalmazáskezelés Partnerközpont funkcióját
    - Új Azure *AD-alkalmazás létrehozásához válassza* az Új webalkalmazás hozzáadása lehetőséget.

    Mindenképpen dokumentálja az *alkalmazásazonosítót,* a  *fiókazonosítót** és a kulcsértékeket, mert az alábbi lépésekben használni fogja őket.

5. Klónozza [a Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) adattárat az Visual Studio paranccsal.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. Nyissa meg a címtárban található *PartnerConsent* `Partner-Center-DotNet-Samples\secure-app-model\keyvault` projektet.

7. Töltse ki az alkalmazásbeállításokat a [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)

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
    > A bizalmas adatokat, például az alkalmazás titkos adatait nem szabad konfigurációs fájlokban tárolni. Ez azért történt, mert ez egy mintaalkalmazás. Éles alkalmazása esetén határozottan javasoljuk, hogy tanúsítványalapú hitelesítést használjon. További információ: [Tanúsítványhitelesítványok alkalmazáshitelesítéshez.]( /azure/active-directory/develop/active-directory-certificate-credentials)

8. A mintaprojekt futtatásakor a rendszer kérni fogja a hitelesítést. A sikeres hitelesítést követően a rendszer hozzáférési jogkivonatot kér az Azure AD-től. Az Azure AD által visszaadott információ tartalmaz egy frissítési jogkivonatot, amely a szolgáltatás konfigurált példányában Azure Key Vault.

## <a name="java-appuser-authentication"></a>Java (alkalmazás+felhasználó hitelesítése)

A [partneri hozzájárulási](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) mintaprojekt bemutatja, hogyan használható egy JSP-vel fejlesztett webhely a hozzájárulás rögzítéséhez, a frissítési jogkivonat kéréséhez és a biztonságos Azure Key Vault. A mintához szükséges előfeltételek létrehozásához hajtsa végre a következőket.

1. Hozza létre a Azure Key Vault egy példányát a Azure Portal vagy az alábbi PowerShell-parancsokkal. A parancs végrehajtása előtt ennek megfelelően módosítsa a paraméterértékeket. A tároló nevének egyedinek kell lennie.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    További információ a Azure Key Vault létrehozásáról: Rövid [útmutató:](/azure/key-vault/quick-create-portal) Titkos adat beállítása és lekérése az Azure Key Vault-ból a Azure Portal vagy rövid útmutató: Titkos adat beállítása és lekérése a Azure Key Vault-ból [a PowerShell](/azure/key-vault/quick-create-powershell)használatával.

2. Hozzon létre egy Azure AD-alkalmazást és egy kulcsot a Azure Portal vagy az alábbi parancsokkal.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Mindenképpen dokumentálja az alkalmazásazonosítót és a titkos értékeket, mert az alábbi lépésekben használni fogja őket.

3. Adja meg az újonnan létrehozott Azure AD-alkalmazásnak a titkos kulcsok olvasására vonatkozó engedélyeket a Azure Portal vagy az alábbi parancsokkal.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Hozzon létre egy Azure AD-alkalmazást, amely a Partnerközpont. A lépés végrehajtásához hajtsa végre a következőt.

    - Keresse meg [az](https://partner.microsoft.com/pcv/apiintegration/appmanagement) irányítópult Alkalmazáskezelés Partnerközpont funkcióját
    - Új Azure *AD-alkalmazás létrehozásához válassza* az Új webalkalmazás hozzáadása lehetőséget.

    Mindenképpen dokumentálja az *alkalmazásazonosítót,* a  *fiókazonosítót** és a kulcsértékeket, mert az alábbi lépésekben használni fogja őket.

5. Klónozza [a Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) adattárat a következő paranccsal

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. Nyissa meg a címtárban található *PartnerConsent* `Partner-Center-Java-Samples\secure-app-model\keyvault` projektet.

7. Töltse ki az alkalmazásbeállításokat, amelyek a [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) fájlban találhatók

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
    > A bizalmas adatokat, például az alkalmazás titkos adatait nem szabad konfigurációs fájlokban tárolni. Ez azért történt, mert ez egy mintaalkalmazás. Éles alkalmazása használata során határozottan javasoljuk, hogy tanúsítványalapú hitelesítést használjon. További információ: [tanúsítványhitelesítés Key Vault.](https://github.com/Azure-Samples/key-vault-java-certificate-authentication)

8. A mintaprojekt futtatásakor a rendszer kérni fogja a hitelesítést. A sikeres hitelesítést követően a rendszer hozzáférési jogkivonatot kér az Azure AD-től. Az Azure AD által visszaadott információ tartalmaz egy frissítési jogkivonatot, amely a szolgáltatás konfigurált példányában Azure Key Vault.

## <a name="cloud-solution-provider-authentication"></a>Felhőszolgáltató hitelesítés

Felhőszolgáltató a partnerek a partner-hozzájárulási folyamat során kapott frissítési [jogkivonatot is használhatjak.](#partner-consent)

### <a name="samples-for-cloud-solution-provider-authentication"></a>Minták Felhőszolgáltató hitelesítéshez

A következő mintákat fejlesztettük ki, hogy segítsen a partnereknek megérteni az egyes szükséges műveletek elvégzésének mikéntját. Amikor a megfelelő megoldást implementálja a környezetében, fontos, hogy olyan megoldást fejlessze ki, amely megfelel a kódolási szabványoknak és a biztonsági szabályzatoknak.

## <a name="net-csp-authentication"></a>.NET (CSP-hitelesítés)

1. Ha még nem tette meg, hajtsa végre a [partneri hozzájárulási folyamatot.](#partner-consent)

2. Klónozza [a Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) adattárat az Visual Studio paranccsal

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Nyissa meg `CSPApplication` a könyvtárban található `Partner-Center-DotNet-Samples\secure-app-model\keyvault` projektet.

4. Frissítse az alkalmazásbeállításokat a [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) fájlban.

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

5. Állítsa be a Megfelelő értékeket a **Program.cs fájlban** található PartnerId és **CustomerId** [változókhoz.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs)

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. A mintaprojekt futtatásakor az le tudja szerezni a partneri hozzájárulási folyamat során kapott frissítési jogkivonatot. Ezután lekért egy hozzáférési jogkivonatot, amely Partnerközpont SDK partner nevében használja az adatbázist. Végül egy hozzáférési jogkivonatot kér a Microsoft Graph a megadott ügyfél nevében.

## <a name="java-csp-authentication"></a>Java (CSP-hitelesítés)

1. Ha még nem tette meg, hajtsa végre a [partneri hozzájárulási folyamatot.](#partner-consent)

2. Klónozza [a Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) adattárat a Visual Studio vagy a következő paranccsal

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Nyissa meg `cspsample` a könyvtárban található `Partner-Center-Java-Samples\secure-app-model\keyvault` projektet.

4. Frissítse az [application.properties fájlban](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) található alkalmazásbeállításokat.

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. A mintaprojekt futtatásakor az le tudja szerezni a partneri hozzájárulási folyamat során kapott frissítési jogkivonatot. Ezután lekért egy hozzáférési jogkivonatot, amely Partnerközpont SDK partner nevében használja az adatbázist.

6. Nem kötelező – a *RunAzureTask* és *a RunGraphTask* függvényhívások értesítésének visszaírása, ha meg szeretné tudni, hogyan kommunikálhat az Azure Resource Manager és a Microsoft Graph az ügyfél nevében.

## <a name="control-panel-provider-authentication"></a>Vezérlőpult szolgáltató hitelesítése

A vezérlőpult szállítóinak minden támogatott partnerrel el kell végezniük a [partneri hozzájárulási](#partner-consent) folyamatot. Ha ez befejeződött, a rendszer a folyamat során megszerzett frissítési jogkivonattal fér hozzá a Partnerközpont REST API .NET API-hoz.

### <a name="samples-for-cloud-panel-provider-authentication"></a>Felhőpanel-szolgáltatói hitelesítés mintái

A következő mintákat azért fejlesztettük ki, hogy segítsük a vezérlőpultok gyártóit az egyes szükséges műveletek elvégzésében. Amikor a megfelelő megoldást implementálja a környezetében, fontos, hogy olyan megoldást fejlessze ki, amely megfelel a kódolási szabványoknak és a biztonsági szabályzatoknak.

## <a name="net-cpv-authentication"></a>.NET (CPV-hitelesítés)

1. Fejlessze ki és telepítsen egy folyamatot, Felhőszolgáltató a megfelelő hozzájárulással. További információért tekintse meg a [partneri jóváhagyással kapcsolatos példát.](#partner-consent)

    > [!IMPORTANT]
    > A Felhőszolgáltató hitelesítő adatait nem szabad tárolni. A partner-hozzájárulási folyamat során kapott frissítési jogkivonatot tárolni kell, és arra kell használni, hogy hozzáférési jogkivonatokat kérjen bármely Microsoft API-val való interakcióhoz.

2. Klónozza [a Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) adattárat az Visual Studio paranccsal

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Nyissa meg `CPVApplication` a könyvtárban található `Partner-Center-DotNet-Samples\secure-app-model\keyvault` projektet.

4. Frissítse az alkalmazásbeállításokat a [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) fájlban.

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

5. Állítsa be a Megfelelő értékeket a **Program.cs fájlban** található PartnerId és **CustomerId** [változókhoz.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs)

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. A mintaprojekt futtatásakor a program le tudja szerezni a megadott partner frissítési jogkivonatát. Ezután egy hozzáférési jogkivonatot kér a Partnerközpont és az Azure AD-Graph eléréséhez a partner nevében. A következő feladat, amit végrehajt, az engedélyengedélyek törlése és létrehozása az ügyfélbérlőben. Mivel a vezérlőpult szállítója és az ügyfél között nincs kapcsolat, ezeket az engedélyeket a Partnerközpont API-val kell hozzáadni. Az alábbi példa bemutatja, hogyan valósíthatja meg ezt.

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

Az engedélyek létrejötte után a minta műveleteket hajt végre az Azure AD Graph az ügyfél nevében.

## <a name="java-cpv-authentication"></a>Java (CPV-hitelesítés)

1. Fejlessze ki és telepítsen egy folyamatot, Felhőszolgáltató a megfelelő hozzájárulással. További információért és egy példáért tekintse meg a [partneri jóváhagyást.](#partner-consent)

    > [!IMPORTANT]
    > A Felhőszolgáltató hitelesítő adatait nem szabad tárolni. A partner-hozzájárulási folyamat során kapott frissítési jogkivonatot tárolni kell, és arra kell használni, hogy hozzáférési jogkivonatokat kérjen bármely Microsoft API-val való interakcióhoz.

2. Klónozza [a Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) adattárat a következő paranccsal

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Nyissa meg `cpvsample` a könyvtárban található `Partner-Center-Java-Samples\secure-app-model\keyvault` projektet.

4. Frissítse az [application.properties fájlban](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) található alkalmazásbeállításokat.

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

    A értékének `partnercenter.displayName` a Marketplace-alkalmazás megjelenített nevének kell lennie.

5. Állítsa be a [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) fájlban található **partnerId** és **customerId** változók megfelelő értékeit.

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. A mintaprojekt futtatásakor a program le tudja szerezni a megadott partner frissítési jogkivonatát. Ezután egy hozzáférési jogkivonatot kér a Partnerközpont eléréséhez a partner nevében. A következő feladat, amit végrehajt, az engedélyengedélyek törlése és létrehozása az ügyfélbérlőben. Mivel a vezérlőpult szállítója és az ügyfél között nincs kapcsolat, ezeket az engedélyeket a Partnerközpont API-val kell hozzáadni. Az alábbi példa az engedélyek megadását mutatja be.

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

A *RunAzureTask* és *a RunGraphTask* függvényhívások értesítésének visszaírása, ha látni szeretné, hogyan kommunikálhat az Azure Resource Manager és a Microsoft Graph az ügyfél nevében.
