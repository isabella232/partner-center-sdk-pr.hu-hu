---
title: Biztonságos alkalmazásmodell engedélyezése
description: Biztonságossá Partnerközpont és a vezérlőpulton található alkalmazásokat.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 19a1c39576a4f897df2d1205e3501839f6580831
ms.sourcegitcommit: e0077b2724d128ab20cb05696e5e5b1cde8e5214
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/07/2021
ms.locfileid: "113481667"
---
# <a name="enabling-the-secure-application-model-framework"></a><span data-ttu-id="4512c-103">A biztonságos alkalmazásmodellek keretrendszerének engedélyezése</span><span class="sxs-lookup"><span data-stu-id="4512c-103">Enabling the Secure Application Model framework</span></span>

<span data-ttu-id="4512c-104">A Microsoft egy biztonságos, skálázható keretrendszert vezet be a felhőszolgáltató (CSP) partnerek és a vezérlőpult-szállítók (CPV) hitelesítéséhez a Microsoft Azure Active Directory Multi-Factor Authentication (MFA) architektúrán keresztül.</span><span class="sxs-lookup"><span data-stu-id="4512c-104">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure Active Directory Multi-Factor Authentication (MFA) architecture.</span></span>

<span data-ttu-id="4512c-105">Az új modell használatával megemelheti a biztonsági szinteket a Partnerközpont API-integrációs hívásokhoz.</span><span class="sxs-lookup"><span data-stu-id="4512c-105">You can use the new model to elevate security for Partner Center API integration calls.</span></span> <span data-ttu-id="4512c-106">Ez segít az összes félnek (beleértve a Microsoftot, a CSP-partnereket és a CPV-ket is) az infrastruktúra és az ügyféladatok biztonsági kockázatokkal szembeni védelmében.</span><span class="sxs-lookup"><span data-stu-id="4512c-106">This will help all parties (including Microsoft, CSP partners, and CPVs) to protect their infrastructure and customer data from security risks.</span></span>

## <a name="scope"></a><span data-ttu-id="4512c-107">Hatókör</span><span class="sxs-lookup"><span data-stu-id="4512c-107">Scope</span></span>

<span data-ttu-id="4512c-108">Ez a cikk a következő a szereplőkkel kapcsolatos:</span><span class="sxs-lookup"><span data-stu-id="4512c-108">This article concerns the following actors:</span></span>

- <span data-ttu-id="4512c-109">CPV-k</span><span class="sxs-lookup"><span data-stu-id="4512c-109">CPVs</span></span>
  - <span data-ttu-id="4512c-110">A CPV-k olyan független szoftverszállítók, amelyek a CSP-partnerek által a Partner Center API-kkal való integrációhoz használható alkalmazásokat fejlesztenek.</span><span class="sxs-lookup"><span data-stu-id="4512c-110">A CPV is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs.</span></span>
  - <span data-ttu-id="4512c-111">A CPV-k nem olyan CSP-partnerek, amelyek közvetlen hozzáféréssel rendelkeznek a Partnerközpont irányítópultjához vagy az API-khoz.</span><span class="sxs-lookup"><span data-stu-id="4512c-111">A CPV isn't a CSP partner with direct access to the Partner Center dashboard or APIs.</span></span>

- <span data-ttu-id="4512c-112">Közvetett CSP-szolgáltatók és közvetlen CSP-partnerek, akik alkalmazásazonosítót + felhasználóhitelesítést használnak, és közvetlenül Partnerközpont API-kkal.</span><span class="sxs-lookup"><span data-stu-id="4512c-112">CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.</span></span>

## <a name="security-requirements"></a><span data-ttu-id="4512c-113">Biztonsági követelmények</span><span class="sxs-lookup"><span data-stu-id="4512c-113">Security requirements</span></span>

<span data-ttu-id="4512c-114">A biztonsági követelményekkel kapcsolatos részletekért lásd: [Partnerbiztonsági követelmények.](/partner-center/partner-security-requirements)</span><span class="sxs-lookup"><span data-stu-id="4512c-114">For details on security requirements, see [Partner Security Requirements](/partner-center/partner-security-requirements).</span></span>

## <a name="secure-application-model"></a><span data-ttu-id="4512c-115">biztonságos alkalmazásmodell</span><span class="sxs-lookup"><span data-stu-id="4512c-115">Secure Application Model</span></span>

<span data-ttu-id="4512c-116">A Marketplace-alkalmazásoknak CSP-partneri jogosultságokat kell megszemélyesülni a Microsoft API-k meghívása érdekében.</span><span class="sxs-lookup"><span data-stu-id="4512c-116">Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs.</span></span> <span data-ttu-id="4512c-117">Az ilyen bizalmas alkalmazásokat veszélyeztető biztonsági támadások az ügyféladatok feltörése esetén vezethetnek.</span><span class="sxs-lookup"><span data-stu-id="4512c-117">Security attacks on these sensitive applications can lead to the compromise of customer data.</span></span>

<span data-ttu-id="4512c-118">Az új hitelesítési keretrendszer áttekintéséhez és részleteihez töltse le a biztonságos alkalmazásmodell [keretrendszer dokumentumát.](https://assetsprod.microsoft.com/secure-application-model-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="4512c-118">For an overview and details of the new authentication framework, download the [Secure Application Model framework](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) document.</span></span> <span data-ttu-id="4512c-119">Ez a dokumentum azokat az alapelveket és ajánlott eljárásokat foglalja magában, amelyek segítségével fenntarthatóvá és robusztusvá teszi a piactéri alkalmazásokat a biztonsági rések ellen.</span><span class="sxs-lookup"><span data-stu-id="4512c-119">This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.</span></span>

## <a name="samples"></a><span data-ttu-id="4512c-120">Példák</span><span class="sxs-lookup"><span data-stu-id="4512c-120">Samples</span></span>

<span data-ttu-id="4512c-121">A következő áttekintő dokumentumok és mintakódok ismertetik, hogyan valósítják meg a partnerek a biztonságos alkalmazásmodell keretrendszert:</span><span class="sxs-lookup"><span data-stu-id="4512c-121">The following overview documents and sample code describe how partners can implement the Secure Application Model framework:</span></span>

- [<span data-ttu-id="4512c-122">CPV áttekintő dokumentum</span><span class="sxs-lookup"><span data-stu-id="4512c-122">CPV overview document</span></span>](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [<span data-ttu-id="4512c-123">A CSP áttekintő dokumentuma</span><span class="sxs-lookup"><span data-stu-id="4512c-123">CSP overview document</span></span>](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [<span data-ttu-id="4512c-124">.NET-minták</span><span class="sxs-lookup"><span data-stu-id="4512c-124">.NET Samples</span></span>](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [<span data-ttu-id="4512c-125">Java-minták</span><span class="sxs-lookup"><span data-stu-id="4512c-125">Java Samples</span></span>](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [<span data-ttu-id="4512c-126">REST-utasítások és -minták</span><span class="sxs-lookup"><span data-stu-id="4512c-126">REST instructions and samples</span></span>](#rest)
- [<span data-ttu-id="4512c-127">PowerShell-utasítások és -minták</span><span class="sxs-lookup"><span data-stu-id="4512c-127">PowerShell instructions and samples</span></span>](#powershell)

## <a name="rest"></a><span data-ttu-id="4512c-128">REST</span><span class="sxs-lookup"><span data-stu-id="4512c-128">REST</span></span>

<span data-ttu-id="4512c-129">Ha REST-hívásokat biztonságos alkalmazásmodell kódmintával, kövesse az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="4512c-129">To to make REST calls with the Secure Application Model framework with sample code, follow these steps:</span></span>

1. [<span data-ttu-id="4512c-130">Webalkalmazás létrehozása</span><span class="sxs-lookup"><span data-stu-id="4512c-130">Create a web app</span></span>](#create-a-web-app)

2. [<span data-ttu-id="4512c-131">Engedélyezési kód le kérése</span><span class="sxs-lookup"><span data-stu-id="4512c-131">Get an authorization code</span></span>](#get-authorization-code)

3. [<span data-ttu-id="4512c-132">Frissítési jogkivonat beszerzése</span><span class="sxs-lookup"><span data-stu-id="4512c-132">Get a refresh token</span></span>](#get-refresh-token)

4. [<span data-ttu-id="4512c-133">Hozzáférési jogkivonat lekérése</span><span class="sxs-lookup"><span data-stu-id="4512c-133">Get an access token</span></span>](#get-access-token)

5. [<span data-ttu-id="4512c-134">Partner Center API-hívás kezdeményezése</span><span class="sxs-lookup"><span data-stu-id="4512c-134">Make a Partner Center API call</span></span>](#make-partner-center-api-calls)

> [!TIP]
> <span data-ttu-id="4512c-135">A PowerShell Partnerközpont modul használatával lekért egy engedélyezési kódot és egy frissítési jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="4512c-135">You can use the Partner Center PowerShell module to get an authorization code and a refresh token.</span></span> <span data-ttu-id="4512c-136">Ezt a lehetőséget a 2. és a 3. lépés után választhatja ki.</span><span class="sxs-lookup"><span data-stu-id="4512c-136">You can choose this option in place of steps 2 and 3.</span></span> <span data-ttu-id="4512c-137">További információkért lásd a [PowerShell szakaszt és példákat.](#powershell)</span><span class="sxs-lookup"><span data-stu-id="4512c-137">For more information, see the [PowerShell section and examples](#powershell).</span></span>

### <a name="create-a-web-app"></a><span data-ttu-id="4512c-138">Webalkalmazás létrehozása</span><span class="sxs-lookup"><span data-stu-id="4512c-138">Create a web app</span></span>

<span data-ttu-id="4512c-139">REST-hívások előtt létre kell hoznia és regisztrálnia Partnerközpont webalkalmazást.</span><span class="sxs-lookup"><span data-stu-id="4512c-139">You must create and register a web app in Partner Center before making REST calls.</span></span>

1. <span data-ttu-id="4512c-140">Jelentkezzen be az [Azure Portalra](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4512c-140">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4512c-141">Hozzon létre Azure Active Directory (Azure AD) alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="4512c-141">Create an Azure Active Directory (Azure AD) app.</span></span>

3. <span data-ttu-id="4512c-142">Adjon delegált alkalmazásengedélyeket a következő erőforrásoknak az alkalmazás *követelményeitől függően.*</span><span class="sxs-lookup"><span data-stu-id="4512c-142">Give delegated application permissions to the following resources, *depending on your application's requirements*.</span></span> <span data-ttu-id="4512c-143">Szükség esetén további delegált engedélyeket adhat hozzá az alkalmazás-erőforrásokhoz.</span><span class="sxs-lookup"><span data-stu-id="4512c-143">If necessary, you can add more delegated permissions for application resources.</span></span>

   1. <span data-ttu-id="4512c-144">**Microsoft Partnerközpont** (egyes bérlők **SampleBECApp-alkalmazásként mutatják be)**</span><span class="sxs-lookup"><span data-stu-id="4512c-144">**Microsoft Partner Center** (some tenants show this as **SampleBECApp**)</span></span>

   2. <span data-ttu-id="4512c-145">**Azure Management API-k** (ha az Azure API-k hívását tervezi)</span><span class="sxs-lookup"><span data-stu-id="4512c-145">**Azure Management APIs** (if you are planning to call Azure APIs)</span></span>

   3. <span data-ttu-id="4512c-146">**Microsoft Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="4512c-146">**Windows Azure Active Directory**</span></span>

4. <span data-ttu-id="4512c-147">Győződjön meg arról, hogy az alkalmazás kezdőlapjának URL-címe olyan végpontra van beállítva, ahol egy élő webalkalmazás fut.</span><span class="sxs-lookup"><span data-stu-id="4512c-147">Make sure that the home URL of your app is set to an endpoint where a live web app is running.</span></span> <span data-ttu-id="4512c-148">Az alkalmazásnak el [](#get-authorization-code) kell fogadnia az Azure AD bejelentkezési hívásból származó hitelesítési kódot.</span><span class="sxs-lookup"><span data-stu-id="4512c-148">This app will need to accept the [authorization code](#get-authorization-code) from the Azure AD login call.</span></span> <span data-ttu-id="4512c-149">A következő szakaszban található [példakódban például](#get-authorization-code)a webalkalmazás a következő webhelyen fut: `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="4512c-149">For example, in the example code in [the following section](#get-authorization-code), the web app is running at `https://localhost:44395/`.</span></span>

5. <span data-ttu-id="4512c-150">Jegyezze fel a következő információkat a webalkalmazás Azure AD-beállításaiból:</span><span class="sxs-lookup"><span data-stu-id="4512c-150">Note the following information from your web app's settings in Azure AD:</span></span>

   - <span data-ttu-id="4512c-151">Alkalmazásazonosító</span><span class="sxs-lookup"><span data-stu-id="4512c-151">Application ID</span></span>
   - <span data-ttu-id="4512c-152">Alkalmazás titkos kódja</span><span class="sxs-lookup"><span data-stu-id="4512c-152">Application secret</span></span>

> [!NOTE]
> <span data-ttu-id="4512c-153">Ajánlott tanúsítványt [használni titkos alkalmazásként.](/azure/active-directory/develop/active-directory-certificate-credentials)</span><span class="sxs-lookup"><span data-stu-id="4512c-153">It is recommended to [use a certificate as your application secret](/azure/active-directory/develop/active-directory-certificate-credentials).</span></span> <span data-ttu-id="4512c-154">Azonban létrehozhat alkalmazáskulcsot is a Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4512c-154">However, you can also create an application key in the Azure portal.</span></span> <span data-ttu-id="4512c-155">A következő szakaszban [található mintakód egy](#get-authorization-code) alkalmazáskulcsot használ.</span><span class="sxs-lookup"><span data-stu-id="4512c-155">The sample code in [the following section](#get-authorization-code) uses an application key.</span></span>

### <a name="get-authorization-code"></a><span data-ttu-id="4512c-156">Hozzáférési kód lekérése</span><span class="sxs-lookup"><span data-stu-id="4512c-156">Get authorization code</span></span>

<span data-ttu-id="4512c-157">Az Azure AD bejelentkezési hívásból való elfogadáshoz be kell szereznie egy engedélyezési kódot a webalkalmazáshoz:</span><span class="sxs-lookup"><span data-stu-id="4512c-157">You must get an authorization code for your web app to accept from the Azure AD login call:</span></span>

1. <span data-ttu-id="4512c-158">Jelentkezzen be az Azure AD-be a következő URL-címen: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) .</span><span class="sxs-lookup"><span data-stu-id="4512c-158">Log in to Azure AD at the following URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1).</span></span> <span data-ttu-id="4512c-159">Jelentkezzen be azzal a felhasználói fiókkal, amelyről API Partnerközpont hívásokat fog kezdeményezni (például rendszergazdai ügynök vagy értékesítési ügynök fiókja).</span><span class="sxs-lookup"><span data-stu-id="4512c-159">Be sure to log in with the user account from which you will make Partner Center API calls (such as an admin agent or sales agent account).</span></span>

2. <span data-ttu-id="4512c-160">Cserélje **le az Application-Id** helyére az Azure AD-alkalmazás azonosítóját (GUID).</span><span class="sxs-lookup"><span data-stu-id="4512c-160">Replace **Application-Id** with your Azure AD app ID (GUID).</span></span>

3. <span data-ttu-id="4512c-161">Amikor a rendszer kéri, jelentkezzen be a felhasználói fiókjával, konfigurált MFA-val.</span><span class="sxs-lookup"><span data-stu-id="4512c-161">When prompted, log in with your user account with MFA configured.</span></span>

4. <span data-ttu-id="4512c-162">Amikor a rendszer kéri, adjon meg további MFA-adatokat (telefonszám vagy e-mail-cím) a bejelentkezés ellenőrzéséhez.</span><span class="sxs-lookup"><span data-stu-id="4512c-162">When prompted, enter additional MFA information (phone number or email address) to verify your login.</span></span>

5. <span data-ttu-id="4512c-163">Miután bejelentkezett, a böngésző átirányítja a hívást a webalkalmazás végpontjára az engedélyezési kóddal.</span><span class="sxs-lookup"><span data-stu-id="4512c-163">After you are logged in, the browser will redirect the call to your web app endpoint with your authorization code.</span></span> <span data-ttu-id="4512c-164">A következő mintakód például a következőre mutat: `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="4512c-164">For example, the following sample code redirects to `https://localhost:44395/`.</span></span>

#### <a name="authorization-code-call-trace"></a><span data-ttu-id="4512c-165">Engedélyezési kód hívásának nyomkövetése</span><span class="sxs-lookup"><span data-stu-id="4512c-165">Authorization code call trace</span></span>

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

### <a name="get-refresh-token"></a><span data-ttu-id="4512c-166">Frissítési jogkivonat beszerzése</span><span class="sxs-lookup"><span data-stu-id="4512c-166">Get refresh token</span></span>

<span data-ttu-id="4512c-167">Ezután az engedélyezési kóddal le kell szereznie egy frissítési jogkivonatot:</span><span class="sxs-lookup"><span data-stu-id="4512c-167">You must then use your authorization code to get a refresh token:</span></span>

1. <span data-ttu-id="4512c-168">Post-hívást kell hívnia az Azure AD bejelentkezési végpontjára `https://login.microsoftonline.com/CSPTenantID/oauth2/token` az engedélyezési kóddal.</span><span class="sxs-lookup"><span data-stu-id="4512c-168">Make a POST call to the Azure AD login endpoint `https://login.microsoftonline.com/CSPTenantID/oauth2/token` with the authorization code.</span></span> <span data-ttu-id="4512c-169">Példaként tekintse meg a következő [mintahívást.](#sample-refresh-call)</span><span class="sxs-lookup"><span data-stu-id="4512c-169">For an example, see the following [sample call](#sample-refresh-call).</span></span>

2. <span data-ttu-id="4512c-170">Jegyezze fel a visszaadott frissítési jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="4512c-170">Note the refresh token that is returned.</span></span>

3. <span data-ttu-id="4512c-171">Tárolja a frissítési jogkivonatot Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4512c-171">Store the refresh token in Azure Key Vault.</span></span> <span data-ttu-id="4512c-172">További információt a Key Vault [API dokumentációjában talál.](/rest/api/keyvault/)</span><span class="sxs-lookup"><span data-stu-id="4512c-172">For more information, see the [Key Vault API documentation](/rest/api/keyvault/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4512c-173">A frissítési jogkivonatot [titkos kulcsként kell tárolni](/rest/api/keyvault/setsecret/setsecret) a Key Vaultban.</span><span class="sxs-lookup"><span data-stu-id="4512c-173">The refresh token must be [stored as a secret](/rest/api/keyvault/setsecret/setsecret) in Key Vault.</span></span>

#### <a name="sample-refresh-call"></a><span data-ttu-id="4512c-174">Példa frissítési hívásra</span><span class="sxs-lookup"><span data-stu-id="4512c-174">Sample refresh call</span></span>

<span data-ttu-id="4512c-175">Helyőrző kérés:</span><span class="sxs-lookup"><span data-stu-id="4512c-175">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

<span data-ttu-id="4512c-176">Kérés törzse:</span><span class="sxs-lookup"><span data-stu-id="4512c-176">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

<span data-ttu-id="4512c-177">Helyőrző válasz:</span><span class="sxs-lookup"><span data-stu-id="4512c-177">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="4512c-178">Válasz törzse:</span><span class="sxs-lookup"><span data-stu-id="4512c-178">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a><span data-ttu-id="4512c-179">Hozzáférési jogkivonat beszerzése</span><span class="sxs-lookup"><span data-stu-id="4512c-179">Get access token</span></span>

<span data-ttu-id="4512c-180">Mielőtt hívásokat kezdeményezhet a Partnerközpont API-khoz, be kell szereznie egy hozzáférési jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="4512c-180">You must obtain an access token before you can make calls to the Partner Center APIs.</span></span> <span data-ttu-id="4512c-181">A hozzáférési jogkivonat beszerzéséhez frissítési jogkivonatot kell használnia, mivel a hozzáférési jogkivonatok élettartama általában nagyon korlátozott (például egy óránál rövidebb).</span><span class="sxs-lookup"><span data-stu-id="4512c-181">You must use a refresh token to obtain an access token because access tokens generally have a very limited lifetime (for example, less than an hour).</span></span>

<span data-ttu-id="4512c-182">Helyőrző kérés:</span><span class="sxs-lookup"><span data-stu-id="4512c-182">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

<span data-ttu-id="4512c-183">Kérés törzse:</span><span class="sxs-lookup"><span data-stu-id="4512c-183">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

<span data-ttu-id="4512c-184">Helyőrző válasz:</span><span class="sxs-lookup"><span data-stu-id="4512c-184">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="4512c-185">Válasz törzse:</span><span class="sxs-lookup"><span data-stu-id="4512c-185">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a><span data-ttu-id="4512c-186">API Partnerközpont hívások hívása</span><span class="sxs-lookup"><span data-stu-id="4512c-186">Make Partner Center API calls</span></span>

<span data-ttu-id="4512c-187">A hozzáférési jogkivonatot kell használnia a Partnerközpont API-k meghívása érdekében.</span><span class="sxs-lookup"><span data-stu-id="4512c-187">You must use your access token to call the Partner Center APIs.</span></span> <span data-ttu-id="4512c-188">Lásd az alábbi példahívást.</span><span class="sxs-lookup"><span data-stu-id="4512c-188">See the following example call.</span></span>

#### <a name="example-partner-center-api-call"></a><span data-ttu-id="4512c-189">Példa Partnerközpont API-hívásra</span><span class="sxs-lookup"><span data-stu-id="4512c-189">Example Partner Center API call</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a><span data-ttu-id="4512c-190">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4512c-190">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="4512c-191">A [PowerShell-Partnerközpont használatával](https://www.powershellgallery.com/packages/PartnerCenter) csökkentheti a hozzáférési jogkivonat engedélyezési kódjának cseréjéhez szükséges infrastruktúrát.</span><span class="sxs-lookup"><span data-stu-id="4512c-191">You can use the [Partner Center PowerShell module](https://www.powershellgallery.com/packages/PartnerCenter) to reduce the required infrastructure to exchange an authorization code for an access token.</span></span> <span data-ttu-id="4512c-192">Ez a metódus nem kötelező a [REST Partnerközpont hívások készítésnél.](#rest)</span><span class="sxs-lookup"><span data-stu-id="4512c-192">This method is optional for making [Partner Center REST calls](#rest).</span></span>

<span data-ttu-id="4512c-193">További információ erről a folyamatról: [Biztonságos alkalmazásmodell](/powershell/partnercenter/secure-app-model) PowerShell dokumentációja.</span><span class="sxs-lookup"><span data-stu-id="4512c-193">For more information on this process, see [Secure App Model](/powershell/partnercenter/secure-app-model) PowerShell documentation.</span></span>

1. <span data-ttu-id="4512c-194">Telepítse az Azure AD-t, és Partnerközpont PowerShell-modulokat.</span><span class="sxs-lookup"><span data-stu-id="4512c-194">Install the Azure AD and Partner Center PowerShell modules.</span></span>

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. <span data-ttu-id="4512c-195">Használja a **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** parancsot a hozzájárulási folyamat végrehajtásához és a szükséges frissítési jogkivonat rögzítéséhez.</span><span class="sxs-lookup"><span data-stu-id="4512c-195">Use the **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** command to perform the consent process and capture the required refresh token.</span></span>

    ```powershell
    $credential = Get-Credential

    $token = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > <span data-ttu-id="4512c-196">A **ServicePrincipal** paramétert a **New-PartnerAccessToken** paranccsal együtt használjuk, mert egy **Web/API** típusú Azure AD-alkalmazás van használatban.</span><span class="sxs-lookup"><span data-stu-id="4512c-196">The **ServicePrincipal** parameter is used with the **New-PartnerAccessToken** command because an Azure AD app with a type of **Web/API** is being used.</span></span> <span data-ttu-id="4512c-197">Az ilyen típusú alkalmazás megköveteli, hogy a hozzáférési jogkivonat-kérelem tartalmazni fog egy ügyfél-azonosítót és egy titkos ügyfélszámítógépet.</span><span class="sxs-lookup"><span data-stu-id="4512c-197">This type of app requires that a client identifier and secret be included in the access token request.</span></span> <span data-ttu-id="4512c-198">A **Get-Credential** parancs meghívatáskor a rendszer felkéri, hogy adjon meg egy felhasználónevet és egy jelszót.</span><span class="sxs-lookup"><span data-stu-id="4512c-198">When the **Get-Credential** command is invoked, you will be prompted to enter a username and password.</span></span> <span data-ttu-id="4512c-199">Felhasználónévként adja meg az alkalmazásazonosítót.</span><span class="sxs-lookup"><span data-stu-id="4512c-199">Enter the application identifier as the username.</span></span> <span data-ttu-id="4512c-200">Jelszóként adja meg az alkalmazás titkos jelszavát.</span><span class="sxs-lookup"><span data-stu-id="4512c-200">Enter the application secret as the password.</span></span> <span data-ttu-id="4512c-201">A **New-PartnerAccessToken** parancs meghívatáskor a rendszer újra kérni fogja a hitelesítő adatok megadását.</span><span class="sxs-lookup"><span data-stu-id="4512c-201">When the **New-PartnerAccessToken** command is invoked, you will be prompted to enter credentials again.</span></span> <span data-ttu-id="4512c-202">Adja meg a használt szolgáltatásfiók hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="4512c-202">Enter the credentials for the service account that you are using.</span></span> <span data-ttu-id="4512c-203">Ennek a szolgáltatásfióknak megfelelő engedélyekkel rendelkező partnerfióknak kell lennie.</span><span class="sxs-lookup"><span data-stu-id="4512c-203">This service account should be a partner account with appropriate permissions.</span></span>

3. <span data-ttu-id="4512c-204">Másolja ki a frissítési jogkivonat értékét.</span><span class="sxs-lookup"><span data-stu-id="4512c-204">Copy the refresh token value.</span></span>

    ```powershell
    $token.RefreshToken | clip
    ```

<span data-ttu-id="4512c-205">A frissítési jogkivonat értékét egy biztonságos adattárban kell tárolni, például egy Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4512c-205">You should store the refresh token value in a secure repository, such as Azure Key Vault.</span></span> <span data-ttu-id="4512c-206">A biztonságos alkalmazásmodul PowerShell-rel való használatával kapcsolatos további információkért tekintse meg a [többtényezős hitelesítéssel kapcsolatos cikket.](/powershell/partnercenter/multi-factor-auth)</span><span class="sxs-lookup"><span data-stu-id="4512c-206">For more information on how to leverage the secure application module with PowerShell, see the [multi-factor authentication](/powershell/partnercenter/multi-factor-auth) article.</span></span>
