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
# <a name="partner-center-authentication"></a><span data-ttu-id="8bc62-103">Partnerközpont – hitelesítés</span><span class="sxs-lookup"><span data-stu-id="8bc62-103">Partner Center authentication</span></span>

<span data-ttu-id="8bc62-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="8bc62-104">**Applies to:**</span></span>

- <span data-ttu-id="8bc62-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="8bc62-105">Partner Center</span></span>
- <span data-ttu-id="8bc62-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="8bc62-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8bc62-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="8bc62-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8bc62-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="8bc62-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8bc62-109">A Partnerközpont az Azure Active Directoryt használja a hitelesítéshez.</span><span class="sxs-lookup"><span data-stu-id="8bc62-109">Partner Center uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="8bc62-110">Amikor a Partner Center API-t, SDK-t vagy PowerShell-modult használja, megfelelően konfigurálnia kell egy Azure AD-alkalmazást, majd hozzáférési jogkivonatot kell kérnie.</span><span class="sxs-lookup"><span data-stu-id="8bc62-110">When interacting with the Partner Center API, SDK, or PowerShell module you must correctly configure an Azure AD application and then request an access token.</span></span> <span data-ttu-id="8bc62-111">A partner központtal csak az alkalmazás vagy az App + felhasználói hitelesítés használatával kapott hozzáférési jogkivonatok használhatók.</span><span class="sxs-lookup"><span data-stu-id="8bc62-111">Access tokens obtained using app only or app + user authentication can be used with the Partner Center.</span></span> <span data-ttu-id="8bc62-112">Két fontos elemet azonban figyelembe kell venni</span><span class="sxs-lookup"><span data-stu-id="8bc62-112">However, there are two important items that need to be considered</span></span>

- <span data-ttu-id="8bc62-113">A többtényezős hitelesítés használata a partner Center API app + User hitelesítéssel történő elérésekor.</span><span class="sxs-lookup"><span data-stu-id="8bc62-113">Use multi-factor authentication when accessing the Partner Center API using app + user authentication.</span></span> <span data-ttu-id="8bc62-114">A módosítással kapcsolatos további információkért lásd a [biztonságos alkalmazás modelljének engedélyezése](enable-secure-app-model.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="8bc62-114">For more information regarding this change, see [Enable secure application model](enable-secure-app-model.md).</span></span>

- <span data-ttu-id="8bc62-115">A partner Center API nem támogatja az összes műveletet, csak a hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="8bc62-115">Not all of the operations the Partner Center API support app only authentication.</span></span> <span data-ttu-id="8bc62-116">Bizonyos esetekben az App + felhasználói hitelesítés használata szükséges.</span><span class="sxs-lookup"><span data-stu-id="8bc62-116">There are certain scenarios where you'll be required to use app + user authentication.</span></span> <span data-ttu-id="8bc62-117">Az egyes [cikkek](scenarios.md) *előfeltételeinek* címsora alatt olyan dokumentációt talál, amely azt jelzi, hogy az alkalmazás csak hitelesítés, alkalmazás + felhasználó hitelesítése vagy mindkettő támogatott-e.</span><span class="sxs-lookup"><span data-stu-id="8bc62-117">Under the *Prerequisites* heading on each [article](scenarios.md), you'll find documentation that states whether app only authentication, app + user authentication, or both are supported.</span></span>

## <a name="initial-setup"></a><span data-ttu-id="8bc62-118">Kezdeti beállítás</span><span class="sxs-lookup"><span data-stu-id="8bc62-118">Initial setup</span></span>

1. <span data-ttu-id="8bc62-119">A kezdéshez meg kell győződnie arról, hogy rendelkezik egy elsődleges partneri központ-fiókkal és egy integrációs homokozó-partneri központtal is.</span><span class="sxs-lookup"><span data-stu-id="8bc62-119">To begin, you need to make sure that you have both a primary Partner Center account, and an integration sandbox Partner Center account.</span></span> <span data-ttu-id="8bc62-120">További információ: [a partner Center-fiókok beállítása API-hozzáféréshez](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="8bc62-120">For more information, see [Set up Partner Center accounts for API access](set-up-api-access-in-partner-center.md).</span></span> <span data-ttu-id="8bc62-121">Jegyezze fel az Azure HRE-alkalmazás regisztrációs AZONOSÍTÓját és a titkos kulcsot (az ügyfél titkos kulcsának megadása csak az alkalmazás azonosításához szükséges) az elsődleges fiókhoz és az integrációs sandbox-fiókhoz.</span><span class="sxs-lookup"><span data-stu-id="8bc62-121">Make note of the Azure AAD App registration ID and Secret (client secret is required for App only identification) for both your primary account and your integration sandbox account.</span></span>

2. <span data-ttu-id="8bc62-122">Jelentkezzen be az Azure AD-be a Azure Portalból.</span><span class="sxs-lookup"><span data-stu-id="8bc62-122">Sign in to Azure AD from the Azure portal.</span></span> <span data-ttu-id="8bc62-123">Az **egyéb alkalmazásokra vonatkozó engedélyekben** állítsa be a **Windows Azure Active Directory** jogosultságait a **delegált engedélyekre**, és válassza a **címtárhoz való hozzáférést a bejelentkezett felhasználóként** , majd **Jelentkezzen be és olvassa el a felhasználói profilt**.</span><span class="sxs-lookup"><span data-stu-id="8bc62-123">In **permissions to other applications**, set permissions for **Windows Azure Active Directory** to **Delegated Permissions**, and select both **Access the directory as the signed-in user** and **Sign in and read user profile**.</span></span>

3. <span data-ttu-id="8bc62-124">A Azure Portalban **adja hozzá az alkalmazást**.</span><span class="sxs-lookup"><span data-stu-id="8bc62-124">In the Azure portal, **Add application**.</span></span> <span data-ttu-id="8bc62-125">Keressen rá a "Microsoft partner Center" kifejezésre, amely a Microsoft partner Center alkalmazás.</span><span class="sxs-lookup"><span data-stu-id="8bc62-125">Search for "Microsoft Partner Center", which is the Microsoft Partner Center application.</span></span> <span data-ttu-id="8bc62-126">Állítsa be a **delegált engedélyeket** a **partner Center API eléréséhez**.</span><span class="sxs-lookup"><span data-stu-id="8bc62-126">Set the **Delegated Permissions** to **Access Partner Center API**.</span></span> <span data-ttu-id="8bc62-127">Ha a Microsoft Cloud Germany vagy a partner Center Microsoft Cloud az Egyesült Államok kormánya számára használ partner centert, ez a lépés kötelező.</span><span class="sxs-lookup"><span data-stu-id="8bc62-127">If you are using Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government, this step is mandatory.</span></span> <span data-ttu-id="8bc62-128">Ha a partner Center globális példányát használja, ez a lépés nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="8bc62-128">If you are using Partner Center global instance, this step is optional.</span></span> <span data-ttu-id="8bc62-129">A CSP-partnerek a partner Center portálon található app Management szolgáltatással hagyhatják el ezt a lépést a partner Center globális példánya számára.</span><span class="sxs-lookup"><span data-stu-id="8bc62-129">CSP Partners can use the App Management feature in the Partner Center portal to bypass this step for Partner Center global instance.</span></span>

## <a name="app-only-authentication"></a><span data-ttu-id="8bc62-130">Csak az alkalmazás hitelesítése</span><span class="sxs-lookup"><span data-stu-id="8bc62-130">App-only authentication</span></span>

<span data-ttu-id="8bc62-131">Ha csak az alkalmazáson belüli hitelesítést szeretné használni a partner Center REST API, a .NET API, a Java API vagy a PowerShell-modul eléréséhez, akkor az alábbi utasításokat kihasználva teheti meg.</span><span class="sxs-lookup"><span data-stu-id="8bc62-131">If you would like to use app-only authentication to access the Partner Center REST API, .NET API, Java API, or PowerShell module then you can do so by leveraging the following instructions.</span></span>

## <a name="net-app-only-authentication"></a><span data-ttu-id="8bc62-132">.NET (csak alkalmazás hitelesítése)</span><span class="sxs-lookup"><span data-stu-id="8bc62-132">.NET (app-only authentication)</span></span>

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

## <a name="java-app-only-authentication"></a><span data-ttu-id="8bc62-133">Java (csak az alkalmazás hitelesítése)</span><span class="sxs-lookup"><span data-stu-id="8bc62-133">Java (app-only authentication)</span></span>

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

## <a name="rest-app-only-authentication"></a><span data-ttu-id="8bc62-134">REST (csak az alkalmazás hitelesítése)</span><span class="sxs-lookup"><span data-stu-id="8bc62-134">REST (app-only authentication)</span></span>

### <a name="rest-request"></a><span data-ttu-id="8bc62-135">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="8bc62-135">REST request</span></span>

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

### <a name="rest-response"></a><span data-ttu-id="8bc62-136">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="8bc62-136">REST response</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a><span data-ttu-id="8bc62-137">Alkalmazás + felhasználói hitelesítés</span><span class="sxs-lookup"><span data-stu-id="8bc62-137">App + User authentication</span></span>

<span data-ttu-id="8bc62-138">A rendszer az [erőforrás-tulajdonosi jelszó hitelesítő adatainak megadását](https://tools.ietf.org/html/rfc6749#section-4.3) használta a Partner Center REST API, a .NET API, a Java API vagy a PowerShell-modul használatához szükséges hozzáférési jogkivonat igényléséhez.</span><span class="sxs-lookup"><span data-stu-id="8bc62-138">Historically the [resource owner password credentials grant](https://tools.ietf.org/html/rfc6749#section-4.3) has been used to request an access token for use with the Partner Center REST API, .NET API, Java API, or PowerShell module.</span></span> <span data-ttu-id="8bc62-139">Ezt a módszert használták hozzáférési token igénylésére a Azure Active Directory ügyfél-azonosító és felhasználói hitelesítő adatok használatával.</span><span class="sxs-lookup"><span data-stu-id="8bc62-139">That method was used to request an access token from Azure Active Directory using a client identifier and user credentials.</span></span> <span data-ttu-id="8bc62-140">Ez a megközelítés azonban többé nem fog működni, mivel a partneri központ többtényezős hitelesítést igényel az alkalmazás és a felhasználó hitelesítésének használatakor.</span><span class="sxs-lookup"><span data-stu-id="8bc62-140">However, this approach will no longer work because Partner Center requires multi-factor authentication, when using app + user authentication.</span></span> <span data-ttu-id="8bc62-141">Ahhoz, hogy megfeleljen ennek a követelménynek, a Microsoft egy biztonságos, méretezhető keretrendszert vezetett be a Cloud Solution Provider (CSP) partnerek és a Vezérlőpult-szállítók (CPV) többtényezős hitelesítés használatával történő hitelesítéséhez.</span><span class="sxs-lookup"><span data-stu-id="8bc62-141">To comply with this requirement Microsoft has introduced a secure, scalable framework for authenticating Cloud Solution Provider (CSP) partners and control panel vendors (CPV) using multi-factor authentication.</span></span> <span data-ttu-id="8bc62-142">Ezt a keretrendszert a biztonságos alkalmazás modelljének nevezzük, amely egy engedélyezési folyamatból és egy hozzáférési tokenre vonatkozó kérelemből áll, amely frissítési tokent használ.</span><span class="sxs-lookup"><span data-stu-id="8bc62-142">This framework is known as the Secure Application Model, and it is composed of a consent process and a request for an access token using a refresh token.</span></span>

### <a name="partner-consent"></a><span data-ttu-id="8bc62-143">Partneri beleegyezett</span><span class="sxs-lookup"><span data-stu-id="8bc62-143">Partner consent</span></span>

<span data-ttu-id="8bc62-144">A partneri hozzájárulási folyamat egy interaktív folyamat, amelyben a partner a többtényezős hitelesítés használatával hitelesíti a hitelesítést, jóváhagyja az alkalmazást, és egy frissítési tokent biztonságos tárházban (például Azure Key Vault) tárolja.</span><span class="sxs-lookup"><span data-stu-id="8bc62-144">The partner consent process is an interactive process where the partner authenticates using multi-factor authentication, consents to the application, and a refresh token is stored in a secure repository such as Azure Key Vault.</span></span> <span data-ttu-id="8bc62-145">Javasoljuk, hogy ehhez a folyamathoz egy dedikált fiókot kell használni integrációs célokra.</span><span class="sxs-lookup"><span data-stu-id="8bc62-145">We recommend that a dedicated account for integration purposes be used for this process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8bc62-146">A megfelelő multi-Factor Authentication megoldást engedélyezni kell a partneri engedélyezési folyamat során használt szolgáltatásfiók számára.</span><span class="sxs-lookup"><span data-stu-id="8bc62-146">The appropriate multi-factor authentication solution should be enabled for the service account used in the partner consent process.</span></span> <span data-ttu-id="8bc62-147">Ha nem, akkor az eredményül kapott frissítési jogkivonat nem fog megfelelni a biztonsági követelményeknek.</span><span class="sxs-lookup"><span data-stu-id="8bc62-147">If it isn't then the resulting refresh token will not be compliant with security requirements.</span></span>

### <a name="samples-for-app--user-authentication"></a><span data-ttu-id="8bc62-148">Minták az App + felhasználói hitelesítéshez</span><span class="sxs-lookup"><span data-stu-id="8bc62-148">Samples for App + User authentication</span></span>

<span data-ttu-id="8bc62-149">A partneri engedélyezési folyamat számos módon elvégezhető.</span><span class="sxs-lookup"><span data-stu-id="8bc62-149">The partner consent process can be performed in a number of ways.</span></span> <span data-ttu-id="8bc62-150">Annak érdekében, hogy a partnerek megértsék az egyes szükséges műveletek elvégzését, a következő mintákat fejlesztettük ki.</span><span class="sxs-lookup"><span data-stu-id="8bc62-150">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="8bc62-151">Ha a megfelelő megoldást alkalmazza a környezetében, fontos, hogy olyan megoldást fejlesszen ki, amely a kódolási szabványokkal és biztonsági házirendekkel kapcsolatos.</span><span class="sxs-lookup"><span data-stu-id="8bc62-151">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-appuser-authentication"></a><span data-ttu-id="8bc62-152">.NET (alkalmazás + felhasználói hitelesítés)</span><span class="sxs-lookup"><span data-stu-id="8bc62-152">.NET (app+user authentication)</span></span>

<span data-ttu-id="8bc62-153">A [partneri](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) belefoglalási minta projekt bemutatja, hogyan használhatja a ASP.NET használatával kifejlesztett webhelyeket a belefoglalási engedély rögzítéséhez, a frissítési token igényléséhez és a Azure Key Vault biztonságos tárolásához.</span><span class="sxs-lookup"><span data-stu-id="8bc62-153">The [partner consent](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using ASP.NET to capture consent, request a refresh token, and securely store it in Azure Key Vault.</span></span> <span data-ttu-id="8bc62-154">A következő lépések végrehajtásával hozza létre a minta szükséges előfeltételeit.</span><span class="sxs-lookup"><span data-stu-id="8bc62-154">Perform the following steps to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="8bc62-155">Hozzon létre egy Azure Key Vault példányt a Azure Portal vagy a következő PowerShell-parancsok használatával.</span><span class="sxs-lookup"><span data-stu-id="8bc62-155">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="8bc62-156">A parancs végrehajtása előtt ügyeljen arra, hogy a paraméterek értékét ennek megfelelően módosítsa.</span><span class="sxs-lookup"><span data-stu-id="8bc62-156">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="8bc62-157">A tár nevének egyedinek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="8bc62-157">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="8bc62-158">A Azure Key Vault létrehozásával kapcsolatos további információkért lásd [: gyors üzembe helyezés és a titkos kód beolvasása Azure Key Vault használatával a Azure Portal vagy a](/azure/key-vault/quick-create-portal) gyors útmutató: a [PowerShell használatával állítsa be és kérje le a Azure Key Vault titkos kulcsot](/azure/key-vault/quick-create-powershell).</span><span class="sxs-lookup"><span data-stu-id="8bc62-158">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span> <span data-ttu-id="8bc62-159">Ezután állítson be és kérjen le egy titkos kulcsot.</span><span class="sxs-lookup"><span data-stu-id="8bc62-159">Then set and retrieve a secret.</span></span>

2. <span data-ttu-id="8bc62-160">Hozzon létre egy Azure AD-alkalmazást és egy kulcsot a Azure Portal vagy az alábbi parancsok használatával.</span><span class="sxs-lookup"><span data-stu-id="8bc62-160">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="8bc62-161">Ügyeljen arra, hogy jegyezze fel az alkalmazás azonosítóját és a titkos értékeket, mivel ezeket az alábbi lépésekben fogjuk használni.</span><span class="sxs-lookup"><span data-stu-id="8bc62-161">Be sure to make note of the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="8bc62-162">Adja meg az újonnan létrehozott Azure AD-alkalmazást az Azure Portal vagy a következő parancsok használatával a titkok olvasása engedélyekkel.</span><span class="sxs-lookup"><span data-stu-id="8bc62-162">Grant the newly create Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="8bc62-163">Hozzon létre egy, a partner Centerhez konfigurált Azure AD-alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="8bc62-163">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="8bc62-164">A lépés végrehajtásához hajtsa végre a következő műveleteket.</span><span class="sxs-lookup"><span data-stu-id="8bc62-164">Perform the following actions to complete this step.</span></span>

    - <span data-ttu-id="8bc62-165">Tallózással keresse meg a partner Center irányítópultjának [app Management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) szolgáltatását</span><span class="sxs-lookup"><span data-stu-id="8bc62-165">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="8bc62-166">Az új Azure AD-alkalmazás létrehozásához kattintson az *új webalkalmazás hozzáadása* elemre.</span><span class="sxs-lookup"><span data-stu-id="8bc62-166">Click *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="8bc62-167">Ügyeljen arra, hogy az *alkalmazás azonosítóját*, a \* fiók azonosítóját \* \* és a *kulcs* értékeit dokumentálja, mert ezek az alábbi lépésekben lesznek felhasználva.</span><span class="sxs-lookup"><span data-stu-id="8bc62-167">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="8bc62-168">A [partner-központ-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) adattár klónozása a Visual Studióval vagy a következő paranccsal.</span><span class="sxs-lookup"><span data-stu-id="8bc62-168">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command.</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. <span data-ttu-id="8bc62-169">Nyissa meg a címtárban található *PartnerConsent* projektet `Partner-Center-DotNet-Samples\secure-app-model\keyvault` .</span><span class="sxs-lookup"><span data-stu-id="8bc62-169">Open the *PartnerConsent* project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="8bc62-170">A [web.configban](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config) található Alkalmazásbeállítások feltöltése</span><span class="sxs-lookup"><span data-stu-id="8bc62-170">Populate the application settings found in the [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span></span>

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
    > <span data-ttu-id="8bc62-171">A bizalmas adatokat, például az alkalmazás-titkokat nem szabad a konfigurációs fájlokban tárolni.</span><span class="sxs-lookup"><span data-stu-id="8bc62-171">Sensitive information such as application secrets should not be stored in configuration files.</span></span> <span data-ttu-id="8bc62-172">Itt azért történt, mert ez egy minta alkalmazás.</span><span class="sxs-lookup"><span data-stu-id="8bc62-172">It was done here because this is a sample application.</span></span> <span data-ttu-id="8bc62-173">Éles környezetben erősen ajánlott tanúsítványalapú hitelesítést használni.</span><span class="sxs-lookup"><span data-stu-id="8bc62-173">With your production application we strongly recommend that you use certificate-based authentication.</span></span> <span data-ttu-id="8bc62-174">További információ: [tanúsítvány hitelesítő adatai az alkalmazás hitelesítéséhez]( /azure/active-directory/develop/active-directory-certificate-credentials).</span><span class="sxs-lookup"><span data-stu-id="8bc62-174">For more information, see [Certificate credentials for application authentication]( /azure/active-directory/develop/active-directory-certificate-credentials).</span></span>

8. <span data-ttu-id="8bc62-175">A minta projekt futtatásakor a rendszer felszólítja a hitelesítésre.</span><span class="sxs-lookup"><span data-stu-id="8bc62-175">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="8bc62-176">A sikeres hitelesítés után a rendszer egy hozzáférési jogkivonatot kér az Azure AD-től.</span><span class="sxs-lookup"><span data-stu-id="8bc62-176">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="8bc62-177">Az Azure AD által visszaadott adatok közé tartozik a Azure Key Vault konfigurált példányán tárolt frissítési jogkivonat.</span><span class="sxs-lookup"><span data-stu-id="8bc62-177">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="java-appuser-authentication"></a><span data-ttu-id="8bc62-178">Java (alkalmazás + felhasználói hitelesítés)</span><span class="sxs-lookup"><span data-stu-id="8bc62-178">Java (app+user authentication)</span></span>

<span data-ttu-id="8bc62-179">A [partneri](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) belefoglalási minta projekt bemutatja, hogyan használhatók a JSP használatával fejlesztett webhelyek a belefoglalási engedély rögzítése, a frissítési token igénylése és a biztonságos tár Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8bc62-179">The [partner consent](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using JSP to capture consent, request a refresh token, and secure store in Azure Key Vault.</span></span> <span data-ttu-id="8bc62-180">A következő művelet végrehajtásával hozza létre a minta szükséges előfeltételeit.</span><span class="sxs-lookup"><span data-stu-id="8bc62-180">Perform the following to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="8bc62-181">Hozzon létre egy Azure Key Vault példányt a Azure Portal vagy a következő PowerShell-parancsok használatával.</span><span class="sxs-lookup"><span data-stu-id="8bc62-181">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="8bc62-182">A parancs végrehajtása előtt ügyeljen arra, hogy a paraméterek értékét ennek megfelelően módosítsa.</span><span class="sxs-lookup"><span data-stu-id="8bc62-182">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="8bc62-183">A tár nevének egyedinek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="8bc62-183">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="8bc62-184">A Azure Key Vault létrehozásával kapcsolatos további információkért lásd [: gyors üzembe helyezés és a titkos kód beolvasása Azure Key Vault használatával a Azure Portal vagy a](/azure/key-vault/quick-create-portal) gyors útmutató: a [PowerShell használatával állítsa be és kérje le a Azure Key Vault titkos kulcsot](/azure/key-vault/quick-create-powershell).</span><span class="sxs-lookup"><span data-stu-id="8bc62-184">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span>

2. <span data-ttu-id="8bc62-185">Hozzon létre egy Azure AD-alkalmazást és egy kulcsot a Azure Portal vagy az alábbi parancsok használatával.</span><span class="sxs-lookup"><span data-stu-id="8bc62-185">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="8bc62-186">Ügyeljen arra, hogy dokumentálja az alkalmazás azonosítóját és a titkos értékeket, mivel ezeket az alábbi lépésekben fogjuk használni.</span><span class="sxs-lookup"><span data-stu-id="8bc62-186">Be sure to document the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="8bc62-187">Adja meg az újonnan létrehozott Azure AD-alkalmazást az Azure Portal vagy a következő parancsok használatával a titkok olvasása engedélyekkel.</span><span class="sxs-lookup"><span data-stu-id="8bc62-187">Grant the newly created Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="8bc62-188">Hozzon létre egy, a partner Centerhez konfigurált Azure AD-alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="8bc62-188">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="8bc62-189">A lépés végrehajtásához hajtsa végre az alábbi lépéseket.</span><span class="sxs-lookup"><span data-stu-id="8bc62-189">Perform the following to complete this step.</span></span>

    - <span data-ttu-id="8bc62-190">Tallózással keresse meg a partner Center irányítópultjának [app Management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) szolgáltatását</span><span class="sxs-lookup"><span data-stu-id="8bc62-190">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="8bc62-191">Az új Azure AD-alkalmazás létrehozásához kattintson az *új webalkalmazás hozzáadása* elemre.</span><span class="sxs-lookup"><span data-stu-id="8bc62-191">Click *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="8bc62-192">Ügyeljen arra, hogy az *alkalmazás azonosítóját*, a \* fiók azonosítóját \* \* és a *kulcs* értékeit dokumentálja, mert ezek az alábbi lépésekben lesznek felhasználva.</span><span class="sxs-lookup"><span data-stu-id="8bc62-192">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="8bc62-193">A [partner-központ-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) adattár klónozása az alábbi paranccsal</span><span class="sxs-lookup"><span data-stu-id="8bc62-193">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. <span data-ttu-id="8bc62-194">Nyissa meg a címtárban található *PartnerConsent* projektet `Partner-Center-Java-Samples\secure-app-model\keyvault` .</span><span class="sxs-lookup"><span data-stu-id="8bc62-194">Open the *PartnerConsent* project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="8bc62-195">Az [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) fájlban található Alkalmazásbeállítások feltöltése</span><span class="sxs-lookup"><span data-stu-id="8bc62-195">Populate the application settings found in the [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) file</span></span>

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
    > <span data-ttu-id="8bc62-196">A bizalmas adatokat, például az alkalmazás titkos adatait nem szabad a konfigurációs fájlokban tárolni.</span><span class="sxs-lookup"><span data-stu-id="8bc62-196">Sensitive information such as application secrets should not be stored in configurations files.</span></span> <span data-ttu-id="8bc62-197">Itt azért történt, mert ez egy minta alkalmazás.</span><span class="sxs-lookup"><span data-stu-id="8bc62-197">It was done here because this is a sample application.</span></span> <span data-ttu-id="8bc62-198">Éles környezetben a tanúsítvány alapú hitelesítés használatát javasoljuk.</span><span class="sxs-lookup"><span data-stu-id="8bc62-198">With your production application, we strongly recommend that you use certificate based authenticate.</span></span> <span data-ttu-id="8bc62-199">További információ: [Key Vault tanúsítványalapú hitelesítés](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span><span class="sxs-lookup"><span data-stu-id="8bc62-199">For more information, see [Key Vault Certificate authentication](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span></span>

8. <span data-ttu-id="8bc62-200">A minta projekt futtatásakor a rendszer felszólítja a hitelesítésre.</span><span class="sxs-lookup"><span data-stu-id="8bc62-200">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="8bc62-201">A sikeres hitelesítés után a rendszer egy hozzáférési jogkivonatot kér az Azure AD-től.</span><span class="sxs-lookup"><span data-stu-id="8bc62-201">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="8bc62-202">Az Azure AD által visszaadott adatok közé tartozik a Azure Key Vault konfigurált példányán tárolt frissítési jogkivonat.</span><span class="sxs-lookup"><span data-stu-id="8bc62-202">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="cloud-solution-provider-authentication"></a><span data-ttu-id="8bc62-203">Felhőalapú megoldás-szolgáltató hitelesítése</span><span class="sxs-lookup"><span data-stu-id="8bc62-203">Cloud Solution Provider authentication</span></span>

<span data-ttu-id="8bc62-204">A felhőalapú megoldás-szolgáltató partnerei használhatják a [partneri engedélyezési](#partner-consent) folyamat során beszerzett frissítési jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="8bc62-204">Cloud Solution Provider partners can use the refresh token obtained through the [partner consent](#partner-consent) process.</span></span>

### <a name="samples-for-cloud-solution-provider-authentication"></a><span data-ttu-id="8bc62-205">Minták a felhőalapú megoldás-szolgáltató hitelesítéséhez</span><span class="sxs-lookup"><span data-stu-id="8bc62-205">Samples for Cloud Solution Provider authentication</span></span>

<span data-ttu-id="8bc62-206">Annak érdekében, hogy a partnerek megértsék az egyes szükséges műveletek elvégzését, a következő mintákat fejlesztettük ki.</span><span class="sxs-lookup"><span data-stu-id="8bc62-206">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="8bc62-207">Ha a megfelelő megoldást alkalmazza a környezetében, fontos, hogy olyan megoldást fejlesszen ki, amely a kódolási szabványokkal és biztonsági házirendekkel kapcsolatos.</span><span class="sxs-lookup"><span data-stu-id="8bc62-207">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-csp-authentication"></a><span data-ttu-id="8bc62-208">.NET (CSP hitelesítés)</span><span class="sxs-lookup"><span data-stu-id="8bc62-208">.NET (CSP authentication)</span></span>

1. <span data-ttu-id="8bc62-209">Ha még nem tette meg, hajtsa végre a [partneri engedélyezési folyamatot](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="8bc62-209">If you have not already done so, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="8bc62-210">A [partner-központ-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) adattár klónozása a Visual Studio vagy a következő parancs használatával</span><span class="sxs-lookup"><span data-stu-id="8bc62-210">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="8bc62-211">Nyissa meg a `CSPApplication` `Partner-Center-DotNet-Samples\secure-app-model\keyvault` címtárban található projektet.</span><span class="sxs-lookup"><span data-stu-id="8bc62-211">Open the `CSPApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="8bc62-212">Frissítse az [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) fájlban található Alkalmazásbeállítások közül.</span><span class="sxs-lookup"><span data-stu-id="8bc62-212">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="8bc62-213">Állítsa be a [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) fájlban található **PartnerId** és **Vevőkód** változók megfelelő értékeit.</span><span class="sxs-lookup"><span data-stu-id="8bc62-213">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="8bc62-214">Ha ezt a mintát futtatja, a beolvassa a partneri engedélyezési folyamat során beszerzett frissítési jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="8bc62-214">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="8bc62-215">Ezt követően hozzáférési tokent kér a partner Center SDK-val kapcsolatban a partner nevében.</span><span class="sxs-lookup"><span data-stu-id="8bc62-215">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span> <span data-ttu-id="8bc62-216">Végezetül pedig hozzáférési tokent kér, hogy a megadott ügyfél nevében kommunikáljon Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="8bc62-216">Finally, it requests an access token to interact with Microsoft Graph on behalf of the specified customer.</span></span>

## <a name="java-csp-authentication"></a><span data-ttu-id="8bc62-217">Java (CSP hitelesítés)</span><span class="sxs-lookup"><span data-stu-id="8bc62-217">Java (CSP authentication)</span></span>

1. <span data-ttu-id="8bc62-218">Ha még nem tette meg, hajtsa végre a [partneri engedélyezési folyamatot](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="8bc62-218">If you have not done so already, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="8bc62-219">A [partner-központ-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) adattár klónozása a Visual Studióval vagy a következő paranccsal</span><span class="sxs-lookup"><span data-stu-id="8bc62-219">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="8bc62-220">Nyissa meg a `cspsample` `Partner-Center-Java-Samples\secure-app-model\keyvault` címtárban található projektet.</span><span class="sxs-lookup"><span data-stu-id="8bc62-220">Open the `cspsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="8bc62-221">Frissítse az [alkalmazás. properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) fájljában található Alkalmazásbeállítások közül.</span><span class="sxs-lookup"><span data-stu-id="8bc62-221">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) file.</span></span>

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. <span data-ttu-id="8bc62-222">Ha ezt a mintát futtatja, a beolvassa a partneri engedélyezési folyamat során beszerzett frissítési jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="8bc62-222">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="8bc62-223">Ezt követően hozzáférési tokent kér a partner Center SDK-val kapcsolatban a partner nevében.</span><span class="sxs-lookup"><span data-stu-id="8bc62-223">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span>

6. <span data-ttu-id="8bc62-224">Nem kötelező – a *RunAzureTask* és a *RunGraphTask* függvény meghívása, ha szeretné megtekinteni, hogyan lehet kommunikálni Azure Resource Manager és Microsoft Graph az ügyfél nevében.</span><span class="sxs-lookup"><span data-stu-id="8bc62-224">Optional - uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>

## <a name="control-panel-provider-authentication"></a><span data-ttu-id="8bc62-225">Vezérlőpult-szolgáltató hitelesítése</span><span class="sxs-lookup"><span data-stu-id="8bc62-225">Control Panel Provider authentication</span></span>

<span data-ttu-id="8bc62-226">A Vezérlőpult-gyártóknak az általuk támogatott partnerekkel kell rendelkezniük a [partneri beleegyező](#partner-consent) folyamat végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="8bc62-226">Control panel vendors need to have each partner they support perform the [partner consent](#partner-consent) process.</span></span> <span data-ttu-id="8bc62-227">Ha a művelet befejeződött, a rendszer az adott folyamaton keresztül beszerzett frissítési tokent használja a partner Center REST API és a .NET API eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="8bc62-227">Once that is completed the refresh token obtained through that process is used to access the Partner Center REST API and .NET API.</span></span>

### <a name="samples-for-cloud-panel-provider-authentication"></a><span data-ttu-id="8bc62-228">Minták a Cloud panel szolgáltatójának hitelesítéséhez</span><span class="sxs-lookup"><span data-stu-id="8bc62-228">Samples for Cloud Panel Provider authentication</span></span>

<span data-ttu-id="8bc62-229">Annak érdekében, hogy a Vezérlőpult gyártói hogyan tudják elvégezni az egyes szükséges műveleteket, a következő mintákat fejlesztettük ki.</span><span class="sxs-lookup"><span data-stu-id="8bc62-229">To help control panel vendors understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="8bc62-230">Ha a megfelelő megoldást alkalmazza a környezetében, fontos, hogy olyan megoldást fejlesszen ki, amely a kódolási szabványokkal és biztonsági házirendekkel kapcsolatos.</span><span class="sxs-lookup"><span data-stu-id="8bc62-230">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-cpv-authentication"></a><span data-ttu-id="8bc62-231">.NET (CPV-hitelesítés)</span><span class="sxs-lookup"><span data-stu-id="8bc62-231">.NET (CPV authentication)</span></span>

1. <span data-ttu-id="8bc62-232">Dolgozzon ki és helyezzen üzembe egy folyamatot a felhőalapú megoldás-szolgáltató partnerei számára a megfelelő engedély megadásához.</span><span class="sxs-lookup"><span data-stu-id="8bc62-232">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="8bc62-233">További információ: [partneri beleegyezett](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="8bc62-233">For more information an example, see [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8bc62-234">A felhőalapú megoldás-szolgáltatói partnertől származó felhasználói hitelesítő adatokat nem szabad tárolni.</span><span class="sxs-lookup"><span data-stu-id="8bc62-234">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="8bc62-235">A partneri engedélyezési folyamat során beszerzett frissítési tokent a Microsoft API-k használatával való interakcióhoz szükséges hozzáférési jogkivonatok igénylésére kell tárolni.</span><span class="sxs-lookup"><span data-stu-id="8bc62-235">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="8bc62-236">A [partner-központ-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) adattár klónozása a Visual Studio vagy a következő parancs használatával</span><span class="sxs-lookup"><span data-stu-id="8bc62-236">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="8bc62-237">Nyissa meg a `CPVApplication` `Partner-Center-DotNet-Samples\secure-app-model\keyvault` címtárban található projektet.</span><span class="sxs-lookup"><span data-stu-id="8bc62-237">Open the `CPVApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="8bc62-238">Frissítse az [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) fájlban található Alkalmazásbeállítások közül.</span><span class="sxs-lookup"><span data-stu-id="8bc62-238">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="8bc62-239">Állítsa be a [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) fájlban található **PartnerId** és **Vevőkód** változók megfelelő értékeit.</span><span class="sxs-lookup"><span data-stu-id="8bc62-239">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="8bc62-240">Ha ezt a mintát futtatja, az beolvassa a megadott partner frissítési jogkivonatát.</span><span class="sxs-lookup"><span data-stu-id="8bc62-240">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="8bc62-241">Ezután hozzáférési jogkivonatot kér a partneri központ és az Azure AD Graph eléréséhez a partner nevében.</span><span class="sxs-lookup"><span data-stu-id="8bc62-241">Then, it requests an access token to access Partner Center and Azure AD Graph on behalf of the partner.</span></span> <span data-ttu-id="8bc62-242">A következő feladat az, hogy az engedélyek törlését és létrehozását engedélyezi az ügyfél bérlője számára.</span><span class="sxs-lookup"><span data-stu-id="8bc62-242">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="8bc62-243">Mivel a Vezérlőpult gyártója és az ügyfél között nincs kapcsolat, ezeket az engedélyeket hozzá kell adni a partner Center API-val.</span><span class="sxs-lookup"><span data-stu-id="8bc62-243">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="8bc62-244">Az alábbi példa azt szemlélteti, hogyan valósítható meg.</span><span class="sxs-lookup"><span data-stu-id="8bc62-244">The following example shows how to accomplish that.</span></span>

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

<span data-ttu-id="8bc62-245">Az engedélyek létrejötte után a minta az ügyfél nevében hajt végre műveleteket az Azure AD Graph használatával.</span><span class="sxs-lookup"><span data-stu-id="8bc62-245">After these permissions have been established, the sample performs operations using Azure AD Graph on behalf of the customer.</span></span>

## <a name="java-cpv-authentication"></a><span data-ttu-id="8bc62-246">Java (CPV-hitelesítés)</span><span class="sxs-lookup"><span data-stu-id="8bc62-246">Java (CPV authentication)</span></span>

1. <span data-ttu-id="8bc62-247">Dolgozzon ki és helyezzen üzembe egy folyamatot a felhőalapú megoldás-szolgáltató partnerei számára a megfelelő engedély megadásához.</span><span class="sxs-lookup"><span data-stu-id="8bc62-247">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="8bc62-248">További információkat és példákat a [partneri megállapodásban](#partner-consent)talál.</span><span class="sxs-lookup"><span data-stu-id="8bc62-248">For more information and an example, see the [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8bc62-249">A felhőalapú megoldás-szolgáltatói partnertől származó felhasználói hitelesítő adatokat nem szabad tárolni.</span><span class="sxs-lookup"><span data-stu-id="8bc62-249">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="8bc62-250">A partneri engedélyezési folyamat során beszerzett frissítési tokent a Microsoft API-k használatával való interakcióhoz szükséges hozzáférési jogkivonatok igénylésére kell tárolni.</span><span class="sxs-lookup"><span data-stu-id="8bc62-250">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="8bc62-251">A [partner-központ-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) adattár klónozása az alábbi paranccsal</span><span class="sxs-lookup"><span data-stu-id="8bc62-251">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="8bc62-252">Nyissa meg a `cpvsample` `Partner-Center-Java-Samples\secure-app-model\keyvault` címtárban található projektet.</span><span class="sxs-lookup"><span data-stu-id="8bc62-252">Open the `cpvsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="8bc62-253">Frissítse az [alkalmazás. properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) fájljában található Alkalmazásbeállítások közül.</span><span class="sxs-lookup"><span data-stu-id="8bc62-253">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) file.</span></span>

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

    <span data-ttu-id="8bc62-254">A értékének a `partnercenter.displayName` Marketplace-alkalmazás megjelenítendő nevének kell lennie.</span><span class="sxs-lookup"><span data-stu-id="8bc62-254">The value for the `partnercenter.displayName` should be the display name of your marketplace application.</span></span>

5. <span data-ttu-id="8bc62-255">Állítsa be a [program. Java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) fájljában található **partnerId** és **Vevőkód** változók megfelelő értékeit.</span><span class="sxs-lookup"><span data-stu-id="8bc62-255">Set the appropriate values for the **partnerId** and **customerId** variables found in the [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) file.</span></span>

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. <span data-ttu-id="8bc62-256">Ha ezt a mintát futtatja, az beolvassa a megadott partner frissítési jogkivonatát.</span><span class="sxs-lookup"><span data-stu-id="8bc62-256">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="8bc62-257">Ezt követően hozzáférési jogkivonatot kér a partner központhoz való hozzáféréshez a partner nevében.</span><span class="sxs-lookup"><span data-stu-id="8bc62-257">Then, it requests an access token to access Partner Center on behalf of the partner.</span></span> <span data-ttu-id="8bc62-258">A következő feladat az, hogy az engedélyek törlését és létrehozását engedélyezi az ügyfél bérlője számára.</span><span class="sxs-lookup"><span data-stu-id="8bc62-258">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="8bc62-259">Mivel a Vezérlőpult gyártója és az ügyfél között nincs kapcsolat, ezeket az engedélyeket hozzá kell adni a partner Center API-val.</span><span class="sxs-lookup"><span data-stu-id="8bc62-259">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="8bc62-260">Az alábbi példa az engedélyek megadását mutatja be.</span><span class="sxs-lookup"><span data-stu-id="8bc62-260">The following example shows how to grant the permissions.</span></span>

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

<span data-ttu-id="8bc62-261">Ha szeretné megtekinteni a *RunAzureTask* és a *RunGraphTask* függvényt, ha meg szeretné tekinteni, hogyan lehet kommunikálni a Azure Resource Manager és Microsoft Graph az ügyfél nevében.</span><span class="sxs-lookup"><span data-stu-id="8bc62-261">Uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>
