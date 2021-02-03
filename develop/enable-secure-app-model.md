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
# <a name="enabling-the-secure-application-model-framework"></a><span data-ttu-id="e7380-103">A biztonságos alkalmazásmodellek keretrendszerének engedélyezése</span><span class="sxs-lookup"><span data-stu-id="e7380-103">Enabling the Secure Application Model framework</span></span>

<span data-ttu-id="e7380-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="e7380-104">**Applies to:**</span></span>

- <span data-ttu-id="e7380-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="e7380-105">Partner Center</span></span>

<span data-ttu-id="e7380-106">A Microsoft a Microsoft Azure multi-Factor Authentication (MFA) architektúrán keresztül biztonságos, méretezhető keretrendszert biztosít a Cloud Solution Provider (CSP) partnerek és a Vezérlőpult-szállítók (CPV) hitelesítéséhez.</span><span class="sxs-lookup"><span data-stu-id="e7380-106">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>

<span data-ttu-id="e7380-107">Az új modell használatával emelheti meg a partner Center API-integrációs hívások biztonságát.</span><span class="sxs-lookup"><span data-stu-id="e7380-107">You can use the new model to elevate security for Partner Center API integration calls.</span></span> <span data-ttu-id="e7380-108">Ez segíti az összes felet (beleértve a Microsoftot, a CSP-partnereket és a CPVs is) az infrastruktúra és az ügyféladatok biztonsági kockázatokkal szembeni védelméhez.</span><span class="sxs-lookup"><span data-stu-id="e7380-108">This will help all parties (including Microsoft, CSP partners, and CPVs) to protect their infrastructure and customer data from security risks.</span></span>

## <a name="scope"></a><span data-ttu-id="e7380-109">Hatókör</span><span class="sxs-lookup"><span data-stu-id="e7380-109">Scope</span></span>

<span data-ttu-id="e7380-110">Ez a cikk a következő szereplőkkel kapcsolatos:</span><span class="sxs-lookup"><span data-stu-id="e7380-110">This article concerns the following actors:</span></span>

- <span data-ttu-id="e7380-111">CPV-k</span><span class="sxs-lookup"><span data-stu-id="e7380-111">CPVs</span></span>
  - <span data-ttu-id="e7380-112">A CPV-k olyan független szoftverszállítók, amelyek a CSP-partnerek által a Partner Center API-kkal való integrációhoz használható alkalmazásokat fejlesztenek.</span><span class="sxs-lookup"><span data-stu-id="e7380-112">A CPV is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs.</span></span>
  - <span data-ttu-id="e7380-113">A CPV-k nem olyan CSP-partnerek, amelyek közvetlen hozzáféréssel rendelkeznek a Partnerközpont irányítópultjához vagy az API-khoz.</span><span class="sxs-lookup"><span data-stu-id="e7380-113">A CPV isn't a CSP partner with direct access to the Partner Center dashboard or APIs.</span></span>

- <span data-ttu-id="e7380-114">CSP közvetett szolgáltatók és CSP közvetlen partnereink, akik az App ID + felhasználói hitelesítést használják, és közvetlenül integrálhatók a partner Center API-kkal.</span><span class="sxs-lookup"><span data-stu-id="e7380-114">CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.</span></span>

## <a name="security-requirements"></a><span data-ttu-id="e7380-115">Biztonsági követelmények</span><span class="sxs-lookup"><span data-stu-id="e7380-115">Security requirements</span></span>

<span data-ttu-id="e7380-116">A biztonsági követelményekről a [partneri biztonsági követelmények](/partner-center/partner-security-requirements)című témakörben olvashat bővebben.</span><span class="sxs-lookup"><span data-stu-id="e7380-116">For details on security requirements, see [Partner Security Requirements](/partner-center/partner-security-requirements).</span></span>

## <a name="secure-application-model"></a><span data-ttu-id="e7380-117">Biztonságos alkalmazás modellje</span><span class="sxs-lookup"><span data-stu-id="e7380-117">Secure Application Model</span></span>

<span data-ttu-id="e7380-118">A Marketplace-alkalmazásoknak a Microsoft API-k meghívásához a CSP-partneri jogosultságokat kell megszemélyesíteni.</span><span class="sxs-lookup"><span data-stu-id="e7380-118">Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs.</span></span> <span data-ttu-id="e7380-119">Ezen érzékeny alkalmazások biztonsági támadásai veszélyeztethetik a vásárlói adatokat.</span><span class="sxs-lookup"><span data-stu-id="e7380-119">Security attacks on these sensitive applications can lead to the compromise of customer data.</span></span>

<span data-ttu-id="e7380-120">Az új hitelesítési keretrendszer áttekintését és részleteit a [Secure Application Model Framework](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) -dokumentumból töltheti le.</span><span class="sxs-lookup"><span data-stu-id="e7380-120">For an overview and details of the new authentication framework, download the [Secure Application Model framework](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) document.</span></span> <span data-ttu-id="e7380-121">Ez a dokumentum az alapelveket és ajánlott eljárásokat ismerteti, amelyekkel a Piactéri alkalmazások fenntartható és robusztus védelmet jelentenek a biztonsági veszélyekkel szemben.</span><span class="sxs-lookup"><span data-stu-id="e7380-121">This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.</span></span>

## <a name="samples"></a><span data-ttu-id="e7380-122">Példák</span><span class="sxs-lookup"><span data-stu-id="e7380-122">Samples</span></span>

<span data-ttu-id="e7380-123">A következő áttekintő dokumentumok és mintakód azt ismertetik, hogy a partnerek hogyan tudják megvalósítani a biztonságos alkalmazás modelljének keretrendszerét:</span><span class="sxs-lookup"><span data-stu-id="e7380-123">The following overview documents and sample code describe how partners can implement the Secure Application Model framework:</span></span>

- [<span data-ttu-id="e7380-124">A CPV áttekintő dokumentuma</span><span class="sxs-lookup"><span data-stu-id="e7380-124">CPV overview document</span></span>](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [<span data-ttu-id="e7380-125">A CSP áttekintő dokumentuma</span><span class="sxs-lookup"><span data-stu-id="e7380-125">CSP overview document</span></span>](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [<span data-ttu-id="e7380-126">.NET-minták</span><span class="sxs-lookup"><span data-stu-id="e7380-126">.NET Samples</span></span>](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [<span data-ttu-id="e7380-127">Java-minták</span><span class="sxs-lookup"><span data-stu-id="e7380-127">Java Samples</span></span>](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [<span data-ttu-id="e7380-128">REST-utasítások és minták</span><span class="sxs-lookup"><span data-stu-id="e7380-128">REST instructions and samples</span></span>](#rest)
- [<span data-ttu-id="e7380-129">PowerShell-utasítások és minták</span><span class="sxs-lookup"><span data-stu-id="e7380-129">PowerShell instructions and samples</span></span>](#powershell)

## <a name="rest"></a><span data-ttu-id="e7380-130">REST</span><span class="sxs-lookup"><span data-stu-id="e7380-130">REST</span></span>

<span data-ttu-id="e7380-131">A következő lépésekkel végezheti el a REST-hívásokat a biztonságos alkalmazás modelljének keretrendszerével a mintakód használatával:</span><span class="sxs-lookup"><span data-stu-id="e7380-131">To to make REST calls with the Secure Application Model framework with sample code, follow these steps:</span></span>

1. [<span data-ttu-id="e7380-132">Webalkalmazás létrehozása</span><span class="sxs-lookup"><span data-stu-id="e7380-132">Create a web app</span></span>](#create-a-web-app)

2. [<span data-ttu-id="e7380-133">Engedélyezési kód beszerzése</span><span class="sxs-lookup"><span data-stu-id="e7380-133">Get an authorization code</span></span>](#get-authorization-code)

3. [<span data-ttu-id="e7380-134">Frissítési jogkivonat beszerzése</span><span class="sxs-lookup"><span data-stu-id="e7380-134">Get a refresh token</span></span>](#get-refresh-token)

4. [<span data-ttu-id="e7380-135">Hozzáférési jogkivonat lekérése</span><span class="sxs-lookup"><span data-stu-id="e7380-135">Get an access token</span></span>](#get-access-token)

5. [<span data-ttu-id="e7380-136">Partner Center API-hívás kezdeményezése</span><span class="sxs-lookup"><span data-stu-id="e7380-136">Make a Partner Center API call</span></span>](#make-partner-center-api-calls)

> [!TIP]
> <span data-ttu-id="e7380-137">A partner Center PowerShell-modul használatával beszerezhet egy engedélyezési kódot és egy frissítési jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="e7380-137">You can use the Partner Center PowerShell module to get an authorization code and a refresh token.</span></span> <span data-ttu-id="e7380-138">Ezt a lehetőséget a 2. és a 3. lépés helyett is kiválaszthatja.</span><span class="sxs-lookup"><span data-stu-id="e7380-138">You can choose this option in place of steps 2 and 3.</span></span> <span data-ttu-id="e7380-139">További információkért lásd a [PowerShell szakaszt és példákat](#powershell).</span><span class="sxs-lookup"><span data-stu-id="e7380-139">For more information, see the [PowerShell section and examples](#powershell).</span></span>

### <a name="create-a-web-app"></a><span data-ttu-id="e7380-140">Webalkalmazás létrehozása</span><span class="sxs-lookup"><span data-stu-id="e7380-140">Create a web app</span></span>

<span data-ttu-id="e7380-141">A REST-hívások előtt létre kell hoznia és regisztrálnia kell egy webalkalmazást a partner Centerben.</span><span class="sxs-lookup"><span data-stu-id="e7380-141">You must create and register a web app in Partner Center before making REST calls.</span></span>

1. <span data-ttu-id="e7380-142">Jelentkezzen be az [Azure Portalra](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e7380-142">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e7380-143">Hozzon létre egy Azure Active Directory (Azure AD) alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="e7380-143">Create an Azure Active Directory (Azure AD) app.</span></span>

3. <span data-ttu-id="e7380-144">Az *alkalmazás követelményeitől függően* delegált alkalmazási engedélyeket adhat a következő erőforrásokhoz.</span><span class="sxs-lookup"><span data-stu-id="e7380-144">Give delegated application permissions to the following resources, *depending on your application's requirements*.</span></span> <span data-ttu-id="e7380-145">Szükség esetén további delegált engedélyeket adhat hozzá az alkalmazás erőforrásaihoz.</span><span class="sxs-lookup"><span data-stu-id="e7380-145">If necessary, you can add more delegated permissions for application resources.</span></span>

   1. <span data-ttu-id="e7380-146">**Microsoft partner Center** (egyes bérlők ezt a **SampleBECApp** mutatják)</span><span class="sxs-lookup"><span data-stu-id="e7380-146">**Microsoft Partner Center** (some tenants show this as **SampleBECApp**)</span></span>

   2. <span data-ttu-id="e7380-147">**Azure felügyeleti API** -k (ha Azure API-k meghívását tervezi)</span><span class="sxs-lookup"><span data-stu-id="e7380-147">**Azure Management APIs** (if you are planning to call Azure APIs)</span></span>

   3. <span data-ttu-id="e7380-148">**Microsoft Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="e7380-148">**Windows Azure Active Directory**</span></span>

4. <span data-ttu-id="e7380-149">Győződjön meg arról, hogy az alkalmazás kezdőlapjának URL-címe olyan végpontra van beállítva, amelyben egy élő webalkalmazás fut.</span><span class="sxs-lookup"><span data-stu-id="e7380-149">Make sure that the home URL of your app is set to an endpoint where a live web app is running.</span></span> <span data-ttu-id="e7380-150">Az alkalmazásnak el kell fogadnia az [engedélyezési kódot](#get-authorization-code) az Azure ad bejelentkezési hívását.</span><span class="sxs-lookup"><span data-stu-id="e7380-150">This app will need to accept the [authorization code](#get-authorization-code) from the Azure AD login call.</span></span> <span data-ttu-id="e7380-151">Például a [következő szakaszban](#get-authorization-code)szereplő példában a webalkalmazás fut `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="e7380-151">For example, in the example code in [the following section](#get-authorization-code), the web app is running at `https://localhost:44395/`.</span></span>

5. <span data-ttu-id="e7380-152">Jegyezze fel a következő információkat a webalkalmazás beállításaiban az Azure AD-ben:</span><span class="sxs-lookup"><span data-stu-id="e7380-152">Note the following information from your web app's settings in Azure AD:</span></span>

   - <span data-ttu-id="e7380-153">Alkalmazásazonosító</span><span class="sxs-lookup"><span data-stu-id="e7380-153">Application ID</span></span>
   - <span data-ttu-id="e7380-154">Alkalmazás titkos kódja</span><span class="sxs-lookup"><span data-stu-id="e7380-154">Application secret</span></span>

> [!NOTE]
> <span data-ttu-id="e7380-155">Azt javasoljuk, hogy az [alkalmazás titkos tanúsítványát használja](/azure/active-directory/develop/active-directory-certificate-credentials).</span><span class="sxs-lookup"><span data-stu-id="e7380-155">It is recommended to [use a certificate as your application secret](/azure/active-directory/develop/active-directory-certificate-credentials).</span></span> <span data-ttu-id="e7380-156">A Azure Portalban azonban létrehozhat egy alkalmazás-kulcsot is.</span><span class="sxs-lookup"><span data-stu-id="e7380-156">However, you can also create an application key in the Azure portal.</span></span> <span data-ttu-id="e7380-157">A [következő szakaszban](#get-authorization-code) szereplő mintakód egy alkalmazás kulcsát használja.</span><span class="sxs-lookup"><span data-stu-id="e7380-157">The sample code in [the following section](#get-authorization-code) uses an application key.</span></span>

### <a name="get-authorization-code"></a><span data-ttu-id="e7380-158">Hozzáférési kód lekérése</span><span class="sxs-lookup"><span data-stu-id="e7380-158">Get authorization code</span></span>

<span data-ttu-id="e7380-159">Ahhoz, hogy a webalkalmazás el tudja fogadni az Azure AD bejelentkezési hívását, be kell szereznie egy engedélyezési kódot:</span><span class="sxs-lookup"><span data-stu-id="e7380-159">You must get an authorization code for your web app to accept from the Azure AD login call:</span></span>

1. <span data-ttu-id="e7380-160">Jelentkezzen be az Azure AD-be a következő URL-címen: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) .</span><span class="sxs-lookup"><span data-stu-id="e7380-160">Log in to Azure AD at the following URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1).</span></span> <span data-ttu-id="e7380-161">Ügyeljen arra, hogy a felhasználói fiókkal jelentkezzen be, amelyből a partneri központ API-hívásait (például egy felügyeleti ügynököt vagy egy értékesítési ügynököt) kell használnia.</span><span class="sxs-lookup"><span data-stu-id="e7380-161">Be sure to log in with the user account from which you will make Partner Center API calls (such as an admin agent or sales agent account).</span></span>

2. <span data-ttu-id="e7380-162">Cserélje le az **Application-ID-** t az Azure ad-alkalmazás azonosítójával (GUID).</span><span class="sxs-lookup"><span data-stu-id="e7380-162">Replace **Application-Id** with your Azure AD app ID (GUID).</span></span>

3. <span data-ttu-id="e7380-163">Ha a rendszer kéri, jelentkezzen be a felhasználói fiókjával, és állítsa be az MFA-t.</span><span class="sxs-lookup"><span data-stu-id="e7380-163">When prompted, log in with your user account with MFA configured.</span></span>

4. <span data-ttu-id="e7380-164">Ha a rendszer kéri, adjon meg további MFA-információkat (telefonszám vagy e-mail-cím) a bejelentkezés ellenőrzéséhez.</span><span class="sxs-lookup"><span data-stu-id="e7380-164">When prompted, enter additional MFA information (phone number or email address) to verify your login.</span></span>

5. <span data-ttu-id="e7380-165">Miután bejelentkezett, a böngésző átirányítja a hívást a Web App-végpontra az Ön engedélyezési kódjával.</span><span class="sxs-lookup"><span data-stu-id="e7380-165">After you are logged in, the browser will redirect the call to your web app endpoint with your authorization code.</span></span> <span data-ttu-id="e7380-166">Az alábbi mintakód például átirányítja a következőre: `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="e7380-166">For example, the following sample code redirects to `https://localhost:44395/`.</span></span>

#### <a name="authorization-code-call-trace"></a><span data-ttu-id="e7380-167">Engedélyezési kód hívásának nyomkövetése</span><span class="sxs-lookup"><span data-stu-id="e7380-167">Authorization code call trace</span></span>

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

### <a name="get-refresh-token"></a><span data-ttu-id="e7380-168">Frissítési jogkivonat beolvasása</span><span class="sxs-lookup"><span data-stu-id="e7380-168">Get refresh token</span></span>

<span data-ttu-id="e7380-169">A frissítési jogkivonat lekéréséhez az engedélyezési kódot kell használnia:</span><span class="sxs-lookup"><span data-stu-id="e7380-169">You must then use your authorization code to get a refresh token:</span></span>

1. <span data-ttu-id="e7380-170">Tegye fel az Azure AD bejelentkezési végpontját `https://login.microsoftonline.com/CSPTenantID/oauth2/token` az engedélyezési kóddal.</span><span class="sxs-lookup"><span data-stu-id="e7380-170">Make a POST call to the Azure AD login endpoint `https://login.microsoftonline.com/CSPTenantID/oauth2/token` with the authorization code.</span></span> <span data-ttu-id="e7380-171">Példaként tekintse meg a következő [mintát](#sample-refresh-call).</span><span class="sxs-lookup"><span data-stu-id="e7380-171">For an example, see the following [sample call](#sample-refresh-call).</span></span>

2. <span data-ttu-id="e7380-172">Jegyezze fel a visszaadott frissítési tokent.</span><span class="sxs-lookup"><span data-stu-id="e7380-172">Note the refresh token that is returned.</span></span>

3. <span data-ttu-id="e7380-173">A frissítési token tárolása Azure Key Vaultban.</span><span class="sxs-lookup"><span data-stu-id="e7380-173">Store the refresh token in Azure Key Vault.</span></span> <span data-ttu-id="e7380-174">További információkért tekintse meg a [Key Vault API dokumentációját](/rest/api/keyvault/).</span><span class="sxs-lookup"><span data-stu-id="e7380-174">For more information, see the [Key Vault API documentation](/rest/api/keyvault/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7380-175">A frissítési jogkivonatot [titkos kulcsként kell tárolni](/rest/api/keyvault/setsecret/setsecret) a Key Vaultban.</span><span class="sxs-lookup"><span data-stu-id="e7380-175">The refresh token must be [stored as a secret](/rest/api/keyvault/setsecret/setsecret) in Key Vault.</span></span>

#### <a name="sample-refresh-call"></a><span data-ttu-id="e7380-176">Példa frissítési hívásra</span><span class="sxs-lookup"><span data-stu-id="e7380-176">Sample refresh call</span></span>

<span data-ttu-id="e7380-177">Helyőrző kérése:</span><span class="sxs-lookup"><span data-stu-id="e7380-177">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

<span data-ttu-id="e7380-178">Kérés törzse:</span><span class="sxs-lookup"><span data-stu-id="e7380-178">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

<span data-ttu-id="e7380-179">Helyőrző válasza:</span><span class="sxs-lookup"><span data-stu-id="e7380-179">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="e7380-180">Válasz törzse:</span><span class="sxs-lookup"><span data-stu-id="e7380-180">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a><span data-ttu-id="e7380-181">Hozzáférési jogkivonat lekérése</span><span class="sxs-lookup"><span data-stu-id="e7380-181">Get access token</span></span>

<span data-ttu-id="e7380-182">Ahhoz, hogy hívásokat lehessen kezdeményezni a partner Center API-khoz, be kell szereznie egy hozzáférési jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="e7380-182">You must obtain an access token before you can make calls to the Partner Center APIs.</span></span> <span data-ttu-id="e7380-183">Hozzáférési jogkivonat beszerzéséhez frissítési jogkivonatot kell használnia, mert a hozzáférési jogkivonat általában nagyon korlátozott élettartammal rendelkezik (például kevesebb mint egy óra).</span><span class="sxs-lookup"><span data-stu-id="e7380-183">You must use a refresh token to obtain an access token because access token generally have a very limited lifetime (for example, less than an hour).</span></span>

<span data-ttu-id="e7380-184">Helyőrző kérése:</span><span class="sxs-lookup"><span data-stu-id="e7380-184">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

<span data-ttu-id="e7380-185">Kérés törzse:</span><span class="sxs-lookup"><span data-stu-id="e7380-185">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

<span data-ttu-id="e7380-186">Helyőrző válasza:</span><span class="sxs-lookup"><span data-stu-id="e7380-186">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="e7380-187">Válasz törzse:</span><span class="sxs-lookup"><span data-stu-id="e7380-187">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a><span data-ttu-id="e7380-188">A partner Center API-hívások készítése</span><span class="sxs-lookup"><span data-stu-id="e7380-188">Make Partner Center API calls</span></span>

<span data-ttu-id="e7380-189">A partner Center API-k meghívásához a hozzáférési jogkivonatot kell használnia.</span><span class="sxs-lookup"><span data-stu-id="e7380-189">You must use your access token to call the Partner Center APIs.</span></span> <span data-ttu-id="e7380-190">Tekintse meg a következő példát.</span><span class="sxs-lookup"><span data-stu-id="e7380-190">See the following example call.</span></span>

#### <a name="example-partner-center-api-call"></a><span data-ttu-id="e7380-191">Példa a partner Center API-hívására</span><span class="sxs-lookup"><span data-stu-id="e7380-191">Example Partner Center API call</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a><span data-ttu-id="e7380-192">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7380-192">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="e7380-193">A [partner Center PowerShell-modul](https://www.powershellgallery.com/packages/PartnerCenter) használatával csökkentheti a szükséges infrastruktúrát a hozzáférési token engedélyezési kódjának cseréjéhez.</span><span class="sxs-lookup"><span data-stu-id="e7380-193">You can use the [Partner Center PowerShell module](https://www.powershellgallery.com/packages/PartnerCenter) to reduce the required infrastructure to exchange an authorization code for an access token.</span></span> <span data-ttu-id="e7380-194">Ez a módszer nem kötelező a [partneri központ Rest-hívásainak](#rest)készítéséhez.</span><span class="sxs-lookup"><span data-stu-id="e7380-194">This method is optional for making [Partner Center REST calls](#rest).</span></span>

<span data-ttu-id="e7380-195">További információ erről a folyamatról: [Secure app Model](/powershell/partnercenter/secure-app-model) PowerShell-dokumentáció.</span><span class="sxs-lookup"><span data-stu-id="e7380-195">For more information on this process, see [Secure App Model](/powershell/partnercenter/secure-app-model) PowerShell documentation.</span></span>

1. <span data-ttu-id="e7380-196">Telepítse az Azure AD és a partner Center PowerShell-modulokat.</span><span class="sxs-lookup"><span data-stu-id="e7380-196">Install the Azure AD and Partner Center PowerShell modules.</span></span>

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. <span data-ttu-id="e7380-197">A **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** parancs használatával hajtsa végre az engedélyezési folyamatot, és rögzítse a szükséges frissítési jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="e7380-197">Use the **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** command to perform the consent process and capture the required refresh token.</span></span>

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > <span data-ttu-id="e7380-198">A **New-PartnerAccessToken** paranccsal a **ServicePrincipal** paramétert használja a rendszer, mert a **web/API** típusú Azure ad-alkalmazás használatban van.</span><span class="sxs-lookup"><span data-stu-id="e7380-198">The **ServicePrincipal** parameter is used with the **New-PartnerAccessToken** command because an Azure AD app with a type of **Web/API** is being used.</span></span> <span data-ttu-id="e7380-199">Az ilyen típusú alkalmazásokhoz szükséges, hogy az ügyfél-azonosító és a titkos kulcs szerepeljen a hozzáférési jogkivonat kérelmében.</span><span class="sxs-lookup"><span data-stu-id="e7380-199">This type of app requires that a client identifier and secret be included in the access token request.</span></span> <span data-ttu-id="e7380-200">A **Get-hitelesítőadat** parancs meghívásakor a rendszer kérni fogja a Felhasználónév és a jelszó megadását.</span><span class="sxs-lookup"><span data-stu-id="e7380-200">When the **Get-Credential** command is invoked, you will be prompted to enter a username and password.</span></span> <span data-ttu-id="e7380-201">Adja meg az alkalmazás azonosítóját felhasználónévként.</span><span class="sxs-lookup"><span data-stu-id="e7380-201">Enter the application identifier as the username.</span></span> <span data-ttu-id="e7380-202">Jelszóként adja meg az alkalmazás titkos kulcsát.</span><span class="sxs-lookup"><span data-stu-id="e7380-202">Enter the application secret as the password.</span></span> <span data-ttu-id="e7380-203">A **New-PartnerAccessToken** parancs meghívásakor a rendszer kérni fogja a hitelesítő adatok újbóli megadását.</span><span class="sxs-lookup"><span data-stu-id="e7380-203">When the **New-PartnerAccessToken** command is invoked, you will be prompted to enter credentials again.</span></span> <span data-ttu-id="e7380-204">Adja meg a használt szolgáltatásfiók hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="e7380-204">Enter the credentials for the service account that you are using.</span></span> <span data-ttu-id="e7380-205">Ennek a szolgáltatásfiók-fióknak megfelelő engedélyekkel rendelkező partnernek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="e7380-205">This service account should be a partner account with appropriate permissions.</span></span>

3. <span data-ttu-id="e7380-206">Másolja a frissítési jogkivonat értékét.</span><span class="sxs-lookup"><span data-stu-id="e7380-206">Copy the refresh token value.</span></span>

    ```powershell
    $token.RefreshToken | clip
    ```

<span data-ttu-id="e7380-207">A frissítési jogkivonat értékét biztonságos tárházban kell tárolnia, például Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e7380-207">You should store the refresh token value in a secure repository, such as Azure Key Vault.</span></span> <span data-ttu-id="e7380-208">A Secure Application modul PowerShell használatával történő kihasználása a [multi-Factor Authentication](/powershell/partnercenter/multi-factor-auth) című cikkben található.</span><span class="sxs-lookup"><span data-stu-id="e7380-208">For more information on how to leverage the secure application module with PowerShell, see the [multi-factor authentication](/powershell/partnercenter/multi-factor-auth) article.</span></span>
