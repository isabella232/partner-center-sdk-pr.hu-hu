---
title: Partnerközpont – hitelesítés
description: Partnerközpont Azure AD-t használ a hitelesítéshez, a Partnerközpont API-khoz pedig megfelelően kell konfigurálnia a hitelesítési beállításokat.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.openlocfilehash: e54feba7ea727bb7f7eff8de76dcdf28c8a453ee
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548073"
---
# <a name="partner-center-authentication"></a><span data-ttu-id="46aae-103">Partnerközpont – hitelesítés</span><span class="sxs-lookup"><span data-stu-id="46aae-103">Partner Center authentication</span></span>

<span data-ttu-id="46aae-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="46aae-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="46aae-105">A Partnerközpont az Azure Active Directoryt használja a hitelesítéshez.</span><span class="sxs-lookup"><span data-stu-id="46aae-105">Partner Center uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="46aae-106">Amikor a Partner Center API-t, SDK-t vagy PowerShell-modult használja, megfelelően konfigurálnia kell egy Azure AD-alkalmazást, majd hozzáférési jogkivonatot kell kérnie.</span><span class="sxs-lookup"><span data-stu-id="46aae-106">When interacting with the Partner Center API, SDK, or PowerShell module you must correctly configure an Azure AD application and then request an access token.</span></span> <span data-ttu-id="46aae-107">A csak alkalmazással vagy alkalmazás+ felhasználóhitelesítéssel kapott hozzáférési jogkivonatok használhatók a Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="46aae-107">Access tokens obtained using app only or app + user authentication can be used with the Partner Center.</span></span> <span data-ttu-id="46aae-108">Van azonban két fontos elem, amit figyelembe kell venni</span><span class="sxs-lookup"><span data-stu-id="46aae-108">However, there are two important items that need to be considered</span></span>

- <span data-ttu-id="46aae-109">Többtényezős hitelesítés használata a Partnerközpont API alkalmazás- és felhasználóhitelesítéssel való elérésekor.</span><span class="sxs-lookup"><span data-stu-id="46aae-109">Use multi-factor authentication when accessing the Partner Center API using app + user authentication.</span></span> <span data-ttu-id="46aae-110">További információ erről a változásról: [Biztonságos alkalmazásmodell engedélyezése.](enable-secure-app-model.md)</span><span class="sxs-lookup"><span data-stu-id="46aae-110">For more information regarding this change, see [Enable secure application model](enable-secure-app-model.md).</span></span>

- <span data-ttu-id="46aae-111">A Partnerközpont API nem támogatja az alkalmazások hitelesítését.</span><span class="sxs-lookup"><span data-stu-id="46aae-111">Not all of the operations the Partner Center API support app only authentication.</span></span> <span data-ttu-id="46aae-112">Bizonyos esetekben alkalmazás- és felhasználóhitelesítést kell használnia.</span><span class="sxs-lookup"><span data-stu-id="46aae-112">There are certain scenarios where you'll be required to use app + user authentication.</span></span> <span data-ttu-id="46aae-113">Az egyes *cikk Előfeltételek* fejléce alatt találja a dokumentációt, [](scenarios.md)amely azt jelzi, hogy a rendszer csak alkalmazás-, alkalmazás- és felhasználóhitelesítést, vagy mindkettőt támogatja.</span><span class="sxs-lookup"><span data-stu-id="46aae-113">Under the *Prerequisites* heading on each [article](scenarios.md), you'll find documentation that states whether app only authentication, app + user authentication, or both are supported.</span></span>

## <a name="initial-setup"></a><span data-ttu-id="46aae-114">Kezdeti beállítás</span><span class="sxs-lookup"><span data-stu-id="46aae-114">Initial setup</span></span>

1. <span data-ttu-id="46aae-115">Először győződjön meg arról, hogy elsődleges Partnerközpont fiókkal és egy integrációs Partnerközpont fiókkal.</span><span class="sxs-lookup"><span data-stu-id="46aae-115">To begin, you need to make sure that you have both a primary Partner Center account, and an integration sandbox Partner Center account.</span></span> <span data-ttu-id="46aae-116">További információ: [Set up Partnerközpont accounts for API access](set-up-api-access-in-partner-center.md)(Api Partnerközpont fiókok beállítása.</span><span class="sxs-lookup"><span data-stu-id="46aae-116">For more information, see [Set up Partner Center accounts for API access](set-up-api-access-in-partner-center.md).</span></span> <span data-ttu-id="46aae-117">Jegyezze fel az Azure AAD-alkalmazás regisztrációs azonosítóját és a titkos adatokat (csak az alkalmazásazonosításhoz szükséges titkos ügyféltitk szükséges) az elsődleges fiókhoz és az integrációs védőfali fiókhoz is.</span><span class="sxs-lookup"><span data-stu-id="46aae-117">Make note of the Azure AAD App registration ID and Secret (client secret is required for App only identification) for both your primary account and your integration sandbox account.</span></span>

2. <span data-ttu-id="46aae-118">Jelentkezzen be az Azure AD-be a Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="46aae-118">Sign in to Azure AD from the Azure portal.</span></span> <span data-ttu-id="46aae-119">A **más alkalmazások** engedélyei között állítsa be a **Windows Azure Active Directory** engedélyeinek delegált engedélyek beállítását, és válassza a **Hozzáférés** a címtárhoz bejelentkezett felhasználóként és a Bejelentkezés és felhasználói profil olvasása **lehetőséget.** </span><span class="sxs-lookup"><span data-stu-id="46aae-119">In **permissions to other applications**, set permissions for **Windows Azure Active Directory** to **Delegated Permissions**, and select both **Access the directory as the signed-in user** and **Sign in and read user profile**.</span></span>

3. <span data-ttu-id="46aae-120">A Azure Portal adja **hozzá az alkalmazást.**</span><span class="sxs-lookup"><span data-stu-id="46aae-120">In the Azure portal, **Add application**.</span></span> <span data-ttu-id="46aae-121">Keressen rá a "Microsoft Partnerközpont" kifejezésre, amely a Microsoft Partnerközpont alkalmazás.</span><span class="sxs-lookup"><span data-stu-id="46aae-121">Search for "Microsoft Partner Center", which is the Microsoft Partner Center application.</span></span> <span data-ttu-id="46aae-122">Állítsa a **Delegált engedélyeket** **Access (Hozzáférés) Partnerközpont API-hoz.**</span><span class="sxs-lookup"><span data-stu-id="46aae-122">Set the **Delegated Permissions** to **Access Partner Center API**.</span></span> <span data-ttu-id="46aae-123">Ha microsoftos felhőszolgáltatáshoz Partnerközpont Microsoft Cloud Germany vagy Partnerközpont for Microsoft Cloud for US Government, ez a lépés kötelező.</span><span class="sxs-lookup"><span data-stu-id="46aae-123">If you are using Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government, this step is mandatory.</span></span> <span data-ttu-id="46aae-124">Ha globális példányt Partnerközpont használ, ez a lépés nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="46aae-124">If you are using Partner Center global instance, this step is optional.</span></span> <span data-ttu-id="46aae-125">A CSP-partnerek a Partnerközpont portál Alkalmazáskezelés funkcióját használva megkerülhetik ezt a lépést Partnerközpont globális példányra.</span><span class="sxs-lookup"><span data-stu-id="46aae-125">CSP Partners can use the App Management feature in the Partner Center portal to bypass this step for Partner Center global instance.</span></span>

## <a name="app-only-authentication"></a><span data-ttu-id="46aae-126">Csak alkalmazáshitelesítés</span><span class="sxs-lookup"><span data-stu-id="46aae-126">App-only authentication</span></span>

<span data-ttu-id="46aae-127">Ha csak alkalmazásos hitelesítést szeretne használni az Partnerközpont REST API, a .NET API, a Java API vagy a PowerShell modul eléréséhez, akkor ezt az alábbi utasítások segítségével tegye meg.</span><span class="sxs-lookup"><span data-stu-id="46aae-127">If you would like to use app-only authentication to access the Partner Center REST API, .NET API, Java API, or PowerShell module then you can do so by using the following instructions.</span></span>

## <a name="net-app-only-authentication"></a><span data-ttu-id="46aae-128">.NET (csak alkalmazáshitelesítés)</span><span class="sxs-lookup"><span data-stu-id="46aae-128">.NET (app-only authentication)</span></span>

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

## <a name="java-app-only-authentication"></a><span data-ttu-id="46aae-129">Java (csak alkalmazáshitelesítés)</span><span class="sxs-lookup"><span data-stu-id="46aae-129">Java (app-only authentication)</span></span>

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

## <a name="rest-app-only-authentication"></a><span data-ttu-id="46aae-130">REST (csak alkalmazáshitelesítés)</span><span class="sxs-lookup"><span data-stu-id="46aae-130">REST (app-only authentication)</span></span>

### <a name="rest-request"></a><span data-ttu-id="46aae-131">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="46aae-131">REST request</span></span>

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

### <a name="rest-response"></a><span data-ttu-id="46aae-132">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="46aae-132">REST response</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a><span data-ttu-id="46aae-133">Alkalmazás- és felhasználóhitelesítés</span><span class="sxs-lookup"><span data-stu-id="46aae-133">App + User authentication</span></span>

<span data-ttu-id="46aae-134">Korábban a [](https://tools.ietf.org/html/rfc6749#section-4.3) rendszer az erőforrás-tulajdonosi jelszó-hitelesítő adatokat megadó jogkivonat kérésére használta a Partnerközpont REST API, .NET API, Java API vagy PowerShell modullal való használatra.</span><span class="sxs-lookup"><span data-stu-id="46aae-134">Historically, the [resource owner password credentials grant](https://tools.ietf.org/html/rfc6749#section-4.3) has been used to request an access token for use with the Partner Center REST API, .NET API, Java API, or PowerShell module.</span></span> <span data-ttu-id="46aae-135">Ezzel a módszerrel hozzáférési jogkivonatot kértek a Azure Active Directory ügyfél-azonosító és felhasználói hitelesítő adatok használatával.</span><span class="sxs-lookup"><span data-stu-id="46aae-135">That method was used to request an access token from Azure Active Directory using a client identifier and user credentials.</span></span> <span data-ttu-id="46aae-136">Ez a megközelítés azonban nem fog működni, Partnerközpont többtényezős hitelesítést igényel, ha alkalmazás- és felhasználóhitelesítést használ.</span><span class="sxs-lookup"><span data-stu-id="46aae-136">However, this approach will no longer work because Partner Center requires multi-factor authentication, when using app + user authentication.</span></span> <span data-ttu-id="46aae-137">Ennek a követelménynek a teljesítéséhez a Microsoft biztonságos, skálázható keretrendszert vezetett be a Felhőszolgáltató-partnerek és a vezérlőpult-szállítók (CPV) többtényezős hitelesítéssel való hitelesítéséhez.</span><span class="sxs-lookup"><span data-stu-id="46aae-137">To comply with this requirement Microsoft has introduced a secure, scalable framework for authenticating Cloud Solution Provider (CSP) partners and control panel vendors (CPV) using multi-factor authentication.</span></span> <span data-ttu-id="46aae-138">Ez a keretrendszer az úgynevezett biztonságos alkalmazásmodell, és egy hozzájárulási folyamatból és egy hozzáférési jogkivonatra vonatkozó kérelemből áll, amely egy frissítési jogkivonatot használ.</span><span class="sxs-lookup"><span data-stu-id="46aae-138">This framework is known as the Secure Application Model, and it is composed of a consent process and a request for an access token using a refresh token.</span></span>

### <a name="partner-consent"></a><span data-ttu-id="46aae-139">Partneri hozzájárulás</span><span class="sxs-lookup"><span data-stu-id="46aae-139">Partner consent</span></span>

<span data-ttu-id="46aae-140">A partner hozzájárulási folyamata egy interaktív folyamat, amelyben a partner többtényezős hitelesítéssel hitelesít, hozzájárul az alkalmazáshoz, és egy frissítési jogkivonatot tárol egy biztonságos adattárban, például a Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="46aae-140">The partner consent process is an interactive process where the partner authenticates using multi-factor authentication, consents to the application, and a refresh token is stored in a secure repository such as Azure Key Vault.</span></span> <span data-ttu-id="46aae-141">Javasoljuk, hogy ehhez a folyamathoz egy dedikált fiókot kell használni az integrációhoz.</span><span class="sxs-lookup"><span data-stu-id="46aae-141">We recommend that a dedicated account for integration purposes be used for this process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46aae-142">Engedélyezni kell a megfelelő többtényezős hitelesítési megoldást a partneri hozzájárulási folyamatban használt szolgáltatásfiókhoz.</span><span class="sxs-lookup"><span data-stu-id="46aae-142">The appropriate multi-factor authentication solution should be enabled for the service account used in the partner consent process.</span></span> <span data-ttu-id="46aae-143">Ha nem, akkor az eredményül kapott frissítési jogkivonat nem fog megfelelni a biztonsági követelményeknek.</span><span class="sxs-lookup"><span data-stu-id="46aae-143">If it isn't then the resulting refresh token will not be compliant with security requirements.</span></span>

### <a name="samples-for-app--user-authentication"></a><span data-ttu-id="46aae-144">Minták alkalmazás- és felhasználóhitelesítéshez</span><span class="sxs-lookup"><span data-stu-id="46aae-144">Samples for App + User authentication</span></span>

<span data-ttu-id="46aae-145">A partneri hozzájárulási folyamat többféleképpen is elvégezhető.</span><span class="sxs-lookup"><span data-stu-id="46aae-145">The partner consent process can be performed in a number of ways.</span></span> <span data-ttu-id="46aae-146">Az alábbi mintákat azért fejlesztettük ki, hogy segítsük a partnereket az egyes szükséges műveletek elvégzésében.</span><span class="sxs-lookup"><span data-stu-id="46aae-146">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="46aae-147">Amikor a megfelelő megoldást implementálja a környezetében, fontos, hogy olyan megoldást fejlessze ki, amely megfelel a kódolási szabványoknak és a biztonsági szabályzatoknak.</span><span class="sxs-lookup"><span data-stu-id="46aae-147">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-appuser-authentication"></a><span data-ttu-id="46aae-148">.NET (alkalmazás+felhasználóhitelesítés)</span><span class="sxs-lookup"><span data-stu-id="46aae-148">.NET (app+user authentication)</span></span>

<span data-ttu-id="46aae-149">A [partneri hozzájárulási](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) mintaprojekt bemutatja, hogyan használhatja a ASP.NET használatával fejlesztett webhelyet a hozzájárulás rögzítéséhez, frissítési jogkivonat kéréséhez és biztonságos Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="46aae-149">The [partner consent](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using ASP.NET to capture consent, request a refresh token, and securely store it in Azure Key Vault.</span></span> <span data-ttu-id="46aae-150">A mintához szükséges előfeltételek létrehozásához hajtsa végre az alábbi lépéseket.</span><span class="sxs-lookup"><span data-stu-id="46aae-150">Perform the following steps to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="46aae-151">Hozzon létre egy Azure Key Vault a Azure Portal vagy az alábbi PowerShell-parancsokkal.</span><span class="sxs-lookup"><span data-stu-id="46aae-151">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="46aae-152">A parancs végrehajtása előtt mindenképpen módosítsa ennek megfelelően a paraméterértékeket.</span><span class="sxs-lookup"><span data-stu-id="46aae-152">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="46aae-153">A tároló nevének egyedinek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="46aae-153">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="46aae-154">További információ az Azure Key Vault létrehozásáról: Rövid [útmutató:](/azure/key-vault/quick-create-portal) Titkos adat beállítása és lekérése az Azure Key Vault-ból a Azure Portal vagy rövid útmutató: Titkos adat beállítása és lekérése a Azure Key Vault-ről a [PowerShell](/azure/key-vault/quick-create-powershell)használatával.</span><span class="sxs-lookup"><span data-stu-id="46aae-154">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span> <span data-ttu-id="46aae-155">Ezután állítson be és lekér egy titkos adatokat.</span><span class="sxs-lookup"><span data-stu-id="46aae-155">Then set and retrieve a secret.</span></span>

2. <span data-ttu-id="46aae-156">Hozzon létre egy Azure AD-alkalmazást és egy kulcsot a Azure Portal vagy az alábbi parancsokkal.</span><span class="sxs-lookup"><span data-stu-id="46aae-156">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="46aae-157">Jegyezze fel az alkalmazásazonosítót és a titkos értékeket, mert az alábbi lépésekben használni fogja őket.</span><span class="sxs-lookup"><span data-stu-id="46aae-157">Be sure to make note of the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="46aae-158">Adja meg az újonnan létrehozott Azure AD-alkalmazásnak a titkos kulcsok olvasási engedélyét a Azure Portal vagy az alábbi parancsokkal.</span><span class="sxs-lookup"><span data-stu-id="46aae-158">Grant the newly create Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="46aae-159">Hozzon létre egy Azure AD-alkalmazást, amely a Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="46aae-159">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="46aae-160">A lépés végrehajtásához hajtsa végre a következő műveleteket.</span><span class="sxs-lookup"><span data-stu-id="46aae-160">Perform the following actions to complete this step.</span></span>

    - <span data-ttu-id="46aae-161">Tallózással [keresse](https://partner.microsoft.com/pcv/apiintegration/appmanagement) meg az irányítópult alkalmazáskezelési Partnerközpont funkcióját</span><span class="sxs-lookup"><span data-stu-id="46aae-161">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="46aae-162">Új *Azure AD-alkalmazás létrehozásához válassza* az Új webalkalmazás hozzáadása lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="46aae-162">Select *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="46aae-163">Mindenképpen dokumentálja az *alkalmazásazonosító,* a  *Fiókazonosító*\* és a Kulcs értékét, mert az alábbi lépésekben használni fogja őket.</span><span class="sxs-lookup"><span data-stu-id="46aae-163">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="46aae-164">Klónozza [a Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) adattárat az Visual Studio paranccsal.</span><span class="sxs-lookup"><span data-stu-id="46aae-164">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command.</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. <span data-ttu-id="46aae-165">Nyissa meg a könyvtárban található *PartnerConsent* `Partner-Center-DotNet-Samples\secure-app-model\keyvault` projektet.</span><span class="sxs-lookup"><span data-stu-id="46aae-165">Open the *PartnerConsent* project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="46aae-166">Töltse ki az alkalmazásban található [ alkalmazásbeállításokatweb.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span><span class="sxs-lookup"><span data-stu-id="46aae-166">Populate the application settings found in the [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span></span>

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
    > <span data-ttu-id="46aae-167">A bizalmas adatokat, például az alkalmazás titkos adatait nem szabad konfigurációs fájlokban tárolni.</span><span class="sxs-lookup"><span data-stu-id="46aae-167">Sensitive information such as application secrets should not be stored in configuration files.</span></span> <span data-ttu-id="46aae-168">Ez azért történt, mert ez egy mintaalkalmazás.</span><span class="sxs-lookup"><span data-stu-id="46aae-168">It was done here because this is a sample application.</span></span> <span data-ttu-id="46aae-169">Éles alkalmazása esetén határozottan javasoljuk, hogy tanúsítványalapú hitelesítést használjon.</span><span class="sxs-lookup"><span data-stu-id="46aae-169">With your production application we strongly recommend that you use certificate-based authentication.</span></span> <span data-ttu-id="46aae-170">További információ: [Tanúsítvány hitelesítő adatai alkalmazáshitelesítéshez.]( /azure/active-directory/develop/active-directory-certificate-credentials)</span><span class="sxs-lookup"><span data-stu-id="46aae-170">For more information, see [Certificate credentials for application authentication]( /azure/active-directory/develop/active-directory-certificate-credentials).</span></span>

8. <span data-ttu-id="46aae-171">A mintaprojekt futtatásakor a rendszer kérni fogja a hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="46aae-171">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="46aae-172">A sikeres hitelesítést követően a rendszer hozzáférési jogkivonatot kér az Azure AD-től.</span><span class="sxs-lookup"><span data-stu-id="46aae-172">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="46aae-173">Az Azure AD által visszaadott információ tartalmaz egy frissítési jogkivonatot, amely a szolgáltatás konfigurált példányában Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="46aae-173">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="java-appuser-authentication"></a><span data-ttu-id="46aae-174">Java (alkalmazás-+felhasználóhitelesítés)</span><span class="sxs-lookup"><span data-stu-id="46aae-174">Java (app+user authentication)</span></span>

<span data-ttu-id="46aae-175">A [partneri hozzájárulási](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) mintaprojekt bemutatja, hogyan használhatja a JSP használatával fejlesztett webhelyet a hozzájárulás rögzítéséhez, frissítési jogkivonat kéréséhez és biztonságos tárolóhoz a Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="46aae-175">The [partner consent](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using JSP to capture consent, request a refresh token, and secure store in Azure Key Vault.</span></span> <span data-ttu-id="46aae-176">A mintához szükséges előfeltételek létrehozásához hajtsa végre az alábbi lépéseket.</span><span class="sxs-lookup"><span data-stu-id="46aae-176">Perform the following to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="46aae-177">Hozzon létre egy Azure Key Vault a Azure Portal vagy az alábbi PowerShell-parancsokkal.</span><span class="sxs-lookup"><span data-stu-id="46aae-177">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="46aae-178">A parancs végrehajtása előtt mindenképpen módosítsa ennek megfelelően a paraméterértékeket.</span><span class="sxs-lookup"><span data-stu-id="46aae-178">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="46aae-179">A tároló nevének egyedinek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="46aae-179">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="46aae-180">További információ az Azure Key Vault létrehozásáról: Rövid [útmutató:](/azure/key-vault/quick-create-portal) Titkos adat beállítása és lekérése az Azure Key Vault-ból a Azure Portal vagy rövid útmutató: Titkos adat beállítása és lekérése a Azure Key Vault-ről a [PowerShell](/azure/key-vault/quick-create-powershell)használatával.</span><span class="sxs-lookup"><span data-stu-id="46aae-180">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span>

2. <span data-ttu-id="46aae-181">Hozzon létre egy Azure AD-alkalmazást és egy kulcsot a Azure Portal vagy az alábbi parancsokkal.</span><span class="sxs-lookup"><span data-stu-id="46aae-181">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="46aae-182">Mindenképpen dokumentálja az alkalmazásazonosítót és a titkos értékeket, mert az alábbi lépésekben használni fogja őket.</span><span class="sxs-lookup"><span data-stu-id="46aae-182">Be sure to document the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="46aae-183">Adja meg az újonnan létrehozott Azure AD-alkalmazásnak a titkos kulcsok olvasási engedélyét a Azure Portal vagy az alábbi parancsokkal.</span><span class="sxs-lookup"><span data-stu-id="46aae-183">Grant the newly created Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="46aae-184">Hozzon létre egy Azure AD-alkalmazást, amely a Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="46aae-184">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="46aae-185">A lépés végrehajtásához hajtsa végre a következőket.</span><span class="sxs-lookup"><span data-stu-id="46aae-185">Perform the following to complete this step.</span></span>

    - <span data-ttu-id="46aae-186">Tallózással [keresse](https://partner.microsoft.com/pcv/apiintegration/appmanagement) meg az irányítópult alkalmazáskezelési Partnerközpont funkcióját</span><span class="sxs-lookup"><span data-stu-id="46aae-186">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="46aae-187">Új *Azure AD-alkalmazás létrehozásához válassza* az Új webalkalmazás hozzáadása lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="46aae-187">Select *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="46aae-188">Mindenképpen dokumentálja az *alkalmazásazonosító,* a  *Fiókazonosító*\* és a Kulcs értékét, mert az alábbi lépésekben használni fogja őket.</span><span class="sxs-lookup"><span data-stu-id="46aae-188">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="46aae-189">Klónozza [a Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) adattárat a következő paranccsal</span><span class="sxs-lookup"><span data-stu-id="46aae-189">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. <span data-ttu-id="46aae-190">Nyissa meg a könyvtárban található *PartnerConsent* `Partner-Center-Java-Samples\secure-app-model\keyvault` projektet.</span><span class="sxs-lookup"><span data-stu-id="46aae-190">Open the *PartnerConsent* project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="46aae-191">Töltse ki az alkalmazásbeállításokat, amelyek a [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) találhatók</span><span class="sxs-lookup"><span data-stu-id="46aae-191">Populate the application settings found in the [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) file</span></span>

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
    > <span data-ttu-id="46aae-192">A bizalmas adatokat, például az alkalmazás titkos adatait nem szabad konfigurációs fájlokban tárolni.</span><span class="sxs-lookup"><span data-stu-id="46aae-192">Sensitive information such as application secrets should not be stored in configurations files.</span></span> <span data-ttu-id="46aae-193">Ez azért történt, mert ez egy mintaalkalmazás.</span><span class="sxs-lookup"><span data-stu-id="46aae-193">It was done here because this is a sample application.</span></span> <span data-ttu-id="46aae-194">Éles alkalmazása használata során erősen ajánlott tanúsítványalapú hitelesítést használni.</span><span class="sxs-lookup"><span data-stu-id="46aae-194">With your production application, we strongly recommend that you use certificate based authenticate.</span></span> <span data-ttu-id="46aae-195">További információ: [tanúsítványhitelesítés Key Vault.](https://github.com/Azure-Samples/key-vault-java-certificate-authentication)</span><span class="sxs-lookup"><span data-stu-id="46aae-195">For more information, see [Key Vault Certificate authentication](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span></span>

8. <span data-ttu-id="46aae-196">A mintaprojekt futtatásakor a rendszer kérni fogja a hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="46aae-196">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="46aae-197">A sikeres hitelesítést követően a rendszer hozzáférési jogkivonatot kér az Azure AD-től.</span><span class="sxs-lookup"><span data-stu-id="46aae-197">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="46aae-198">Az Azure AD által visszaadott információ tartalmaz egy frissítési jogkivonatot, amely a szolgáltatás konfigurált példányában Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="46aae-198">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="cloud-solution-provider-authentication"></a><span data-ttu-id="46aae-199">Felhőszolgáltató hitelesítés</span><span class="sxs-lookup"><span data-stu-id="46aae-199">Cloud Solution Provider authentication</span></span>

<span data-ttu-id="46aae-200">Felhőszolgáltató a partnerek a partneri hozzájárulási folyamat során kapott frissítési [jogkivonatot is](#partner-consent) használhatjak.</span><span class="sxs-lookup"><span data-stu-id="46aae-200">Cloud Solution Provider partners can use the refresh token obtained through the [partner consent](#partner-consent) process.</span></span>

### <a name="samples-for-cloud-solution-provider-authentication"></a><span data-ttu-id="46aae-201">Minták Felhőszolgáltató hitelesítéshez</span><span class="sxs-lookup"><span data-stu-id="46aae-201">Samples for Cloud Solution Provider authentication</span></span>

<span data-ttu-id="46aae-202">Az alábbi mintákat azért fejlesztettük ki, hogy segítsük a partnereket az egyes szükséges műveletek elvégzésében.</span><span class="sxs-lookup"><span data-stu-id="46aae-202">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="46aae-203">Amikor a megfelelő megoldást implementálja a környezetében, fontos, hogy olyan megoldást fejlessze ki, amely megfelel a kódolási szabványoknak és a biztonsági szabályzatoknak.</span><span class="sxs-lookup"><span data-stu-id="46aae-203">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-csp-authentication"></a><span data-ttu-id="46aae-204">.NET (CSP-hitelesítés)</span><span class="sxs-lookup"><span data-stu-id="46aae-204">.NET (CSP authentication)</span></span>

1. <span data-ttu-id="46aae-205">Ha még nem tette meg, hajtsa végre a [partneri hozzájárulási folyamatot.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="46aae-205">If you have not already done so, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="46aae-206">Klónozza [a Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) adattárat az Visual Studio paranccsal</span><span class="sxs-lookup"><span data-stu-id="46aae-206">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="46aae-207">Nyissa meg `CSPApplication` a könyvtárban található `Partner-Center-DotNet-Samples\secure-app-model\keyvault` projektet.</span><span class="sxs-lookup"><span data-stu-id="46aae-207">Open the `CSPApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="46aae-208">Frissítse a fájlban található [ alkalmazásbeállításokatApp.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) fájlt.</span><span class="sxs-lookup"><span data-stu-id="46aae-208">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="46aae-209">Állítsa be a Megfelelő értékeket a **Program.cs fájlban** található PartnerId és **CustomerId** [változókhoz.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="46aae-209">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="46aae-210">A mintaprojekt futtatásakor az le tudja szerezni a partneri hozzájárulási folyamat során kapott frissítési jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="46aae-210">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="46aae-211">Ezután egy hozzáférési jogkivonatot kér a Partnerközpont SDK partner nevében történő kommunikációhoz.</span><span class="sxs-lookup"><span data-stu-id="46aae-211">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span> <span data-ttu-id="46aae-212">Végül egy hozzáférési jogkivonatot kér, amely a microsoftos Graph a megadott ügyfél nevében.</span><span class="sxs-lookup"><span data-stu-id="46aae-212">Finally, it requests an access token to interact with Microsoft Graph on behalf of the specified customer.</span></span>

## <a name="java-csp-authentication"></a><span data-ttu-id="46aae-213">Java (CSP-hitelesítés)</span><span class="sxs-lookup"><span data-stu-id="46aae-213">Java (CSP authentication)</span></span>

1. <span data-ttu-id="46aae-214">Ha még nem tette meg, hajtsa végre a [partneri hozzájárulási folyamatot.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="46aae-214">If you have not done so already, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="46aae-215">Klónozza [a Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) adattárat a Visual Studio vagy a következő paranccsal</span><span class="sxs-lookup"><span data-stu-id="46aae-215">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="46aae-216">Nyissa meg `cspsample` a könyvtárban található `Partner-Center-Java-Samples\secure-app-model\keyvault` projektet.</span><span class="sxs-lookup"><span data-stu-id="46aae-216">Open the `cspsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="46aae-217">Frissítse az [application.properties fájlban](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) található alkalmazásbeállításokat.</span><span class="sxs-lookup"><span data-stu-id="46aae-217">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) file.</span></span>

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. <span data-ttu-id="46aae-218">A mintaprojekt futtatásakor az le tudja szerezni a partneri hozzájárulási folyamat során kapott frissítési jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="46aae-218">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="46aae-219">Ezután egy hozzáférési jogkivonatot kér a Partnerközpont SDK partner nevében történő kommunikációhoz.</span><span class="sxs-lookup"><span data-stu-id="46aae-219">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span>

6. <span data-ttu-id="46aae-220">Nem kötelező – a *RunAzureTask* és *a RunGraphTask* függvényhívások a Azure Resource Manager és a Microsoft Graph ügyfél nevében történő interakcióját szeretné látni.</span><span class="sxs-lookup"><span data-stu-id="46aae-220">Optional - uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>

## <a name="control-panel-provider-authentication"></a><span data-ttu-id="46aae-221">Vezérlőpult szolgáltató hitelesítése</span><span class="sxs-lookup"><span data-stu-id="46aae-221">Control Panel Provider authentication</span></span>

<span data-ttu-id="46aae-222">A vezérlőpult szállítóinak minden támogatott partnerrel el kell végezniük a [partneri hozzájárulási](#partner-consent) folyamatot.</span><span class="sxs-lookup"><span data-stu-id="46aae-222">Control panel vendors need to have each partner they support perform the [partner consent](#partner-consent) process.</span></span> <span data-ttu-id="46aae-223">Ha ez befejeződött, a rendszer az ezzel a folyamattal megszerzett frissítési jogkivonattal fér hozzá a Partnerközpont REST API .NET API-hoz.</span><span class="sxs-lookup"><span data-stu-id="46aae-223">Once that is completed the refresh token obtained through that process is used to access the Partner Center REST API and .NET API.</span></span>

### <a name="samples-for-cloud-panel-provider-authentication"></a><span data-ttu-id="46aae-224">Felhőpanel-szolgáltatói hitelesítés mintái</span><span class="sxs-lookup"><span data-stu-id="46aae-224">Samples for Cloud Panel Provider authentication</span></span>

<span data-ttu-id="46aae-225">A következő mintákat azért fejlesztettük ki, hogy segítsük a vezérlőpultok gyártóit az egyes szükséges műveletek elvégzésében.</span><span class="sxs-lookup"><span data-stu-id="46aae-225">To help control panel vendors understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="46aae-226">Amikor a megfelelő megoldást implementálja a környezetében, fontos, hogy olyan megoldást fejlessze ki, amely megfelel a kódolási szabványoknak és a biztonsági szabályzatoknak.</span><span class="sxs-lookup"><span data-stu-id="46aae-226">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-cpv-authentication"></a><span data-ttu-id="46aae-227">.NET (CPV-hitelesítés)</span><span class="sxs-lookup"><span data-stu-id="46aae-227">.NET (CPV authentication)</span></span>

1. <span data-ttu-id="46aae-228">Dolgozzon ki és telepítsen egy folyamatot, amely Felhőszolgáltató a megfelelő hozzájárulás érdekében.</span><span class="sxs-lookup"><span data-stu-id="46aae-228">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="46aae-229">További információért tekintse meg a [partneri jóváhagyással kapcsolatos példát.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="46aae-229">For more information an example, see [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="46aae-230">A Felhőszolgáltató hitelesítő adatait nem szabad tárolni.</span><span class="sxs-lookup"><span data-stu-id="46aae-230">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="46aae-231">A partneri hozzájárulási folyamat során kapott frissítési jogkivonatot tárolni kell, és arra kell használni, hogy hozzáférési jogkivonatokat kérjen bármely Microsoft API-val való interakcióhoz.</span><span class="sxs-lookup"><span data-stu-id="46aae-231">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="46aae-232">Klónozza [a Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) adattárat az Visual Studio paranccsal</span><span class="sxs-lookup"><span data-stu-id="46aae-232">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="46aae-233">Nyissa meg `CPVApplication` a könyvtárban található `Partner-Center-DotNet-Samples\secure-app-model\keyvault` projektet.</span><span class="sxs-lookup"><span data-stu-id="46aae-233">Open the `CPVApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="46aae-234">Frissítse a fájlban található [ alkalmazásbeállításokatApp.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) fájlt.</span><span class="sxs-lookup"><span data-stu-id="46aae-234">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="46aae-235">Állítsa be a Megfelelő értékeket a **Program.cs fájlban** található PartnerId és **CustomerId** [változókhoz.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="46aae-235">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="46aae-236">A mintaprojekt futtatásakor a program le tudja szerezni a megadott partner frissítési jogkivonatát.</span><span class="sxs-lookup"><span data-stu-id="46aae-236">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="46aae-237">Ezután hozzáférési jogkivonatot kér a Partnerközpont és az Azure AD-Graph eléréséhez a partner nevében.</span><span class="sxs-lookup"><span data-stu-id="46aae-237">Then, it requests an access token to access Partner Center and Azure AD Graph on behalf of the partner.</span></span> <span data-ttu-id="46aae-238">A következő feladat az engedélyengedélyek törlése és létrehozása az ügyfélbérlőben.</span><span class="sxs-lookup"><span data-stu-id="46aae-238">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="46aae-239">Mivel a vezérlőpult szállítója és az ügyfél között nincs kapcsolat, ezeket az engedélyeket a Partnerközpont API-val kell hozzáadni.</span><span class="sxs-lookup"><span data-stu-id="46aae-239">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="46aae-240">Az alábbi példa ezt mutatja be.</span><span class="sxs-lookup"><span data-stu-id="46aae-240">The following example shows how to accomplish that.</span></span>

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

<span data-ttu-id="46aae-241">Az engedélyek létrejötte után a minta az Azure AD-Graph az ügyfél nevében hajt végre műveleteket.</span><span class="sxs-lookup"><span data-stu-id="46aae-241">After these permissions have been established, the sample performs operations using Azure AD Graph on behalf of the customer.</span></span>

## <a name="java-cpv-authentication"></a><span data-ttu-id="46aae-242">Java (CPV-hitelesítés)</span><span class="sxs-lookup"><span data-stu-id="46aae-242">Java (CPV authentication)</span></span>

1. <span data-ttu-id="46aae-243">Dolgozzon ki és telepítsen egy folyamatot, amely Felhőszolgáltató a megfelelő hozzájárulás érdekében.</span><span class="sxs-lookup"><span data-stu-id="46aae-243">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="46aae-244">További információért és egy példáért tekintse meg a [partneri jóváhagyást.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="46aae-244">For more information and an example, see the [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="46aae-245">A Felhőszolgáltató hitelesítő adatait nem szabad tárolni.</span><span class="sxs-lookup"><span data-stu-id="46aae-245">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="46aae-246">A partneri hozzájárulási folyamat során kapott frissítési jogkivonatot tárolni kell, és arra kell használni, hogy hozzáférési jogkivonatokat kérjen bármely Microsoft API-val való interakcióhoz.</span><span class="sxs-lookup"><span data-stu-id="46aae-246">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="46aae-247">Klónozza [a Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) adattárat a következő paranccsal</span><span class="sxs-lookup"><span data-stu-id="46aae-247">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="46aae-248">Nyissa meg `cpvsample` a könyvtárban található `Partner-Center-Java-Samples\secure-app-model\keyvault` projektet.</span><span class="sxs-lookup"><span data-stu-id="46aae-248">Open the `cpvsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="46aae-249">Frissítse az [application.properties fájlban](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) található alkalmazásbeállításokat.</span><span class="sxs-lookup"><span data-stu-id="46aae-249">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) file.</span></span>

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

    <span data-ttu-id="46aae-250">A értékének `partnercenter.displayName` a Marketplace-alkalmazás megjelenített nevének kell lennie.</span><span class="sxs-lookup"><span data-stu-id="46aae-250">The value for the `partnercenter.displayName` should be the display name of your marketplace application.</span></span>

5. <span data-ttu-id="46aae-251">Állítsa be a Megfelelő értékeket a [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) fájlban található **partnerId** és **customerId** változókhoz.</span><span class="sxs-lookup"><span data-stu-id="46aae-251">Set the appropriate values for the **partnerId** and **customerId** variables found in the [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) file.</span></span>

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. <span data-ttu-id="46aae-252">A mintaprojekt futtatásakor a program le tudja szerezni a megadott partner frissítési jogkivonatát.</span><span class="sxs-lookup"><span data-stu-id="46aae-252">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="46aae-253">Ezután egy hozzáférési jogkivonatot kér a Partnerközpont eléréséhez a partner nevében.</span><span class="sxs-lookup"><span data-stu-id="46aae-253">Then, it requests an access token to access Partner Center on behalf of the partner.</span></span> <span data-ttu-id="46aae-254">A következő feladat az engedélyengedélyek törlése és létrehozása az ügyfélbérlőben.</span><span class="sxs-lookup"><span data-stu-id="46aae-254">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="46aae-255">Mivel a vezérlőpult szállítója és az ügyfél között nincs kapcsolat, ezeket az engedélyeket a Partnerközpont API-val kell hozzáadni.</span><span class="sxs-lookup"><span data-stu-id="46aae-255">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="46aae-256">Az alábbi példa bemutatja, hogyan adhatja meg az engedélyeket.</span><span class="sxs-lookup"><span data-stu-id="46aae-256">The following example shows how to grant the permissions.</span></span>

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

<span data-ttu-id="46aae-257">A *RunAzureTask* és *a RunGraphTask* függvényhívások a Azure Resource Manager és a Microsoft Graph ügyfél nevében történő interakcióját szeretné látni.</span><span class="sxs-lookup"><span data-stu-id="46aae-257">Uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>
