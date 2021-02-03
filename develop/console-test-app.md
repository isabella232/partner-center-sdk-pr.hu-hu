---
title: Konzolos tesztalkalmazás
description: Ez a konzol-tesztelési alkalmazás a partner Center API-k által támogatott összes forgatókönyvhöz tartalmaz mintakód-kódot. Teszteléshez is használhatja.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e82bac3ccc22d0e7cf898e5b2d2e002c622584ae
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767995"
---
# <a name="console-test-app"></a><span data-ttu-id="da717-104">Konzolos tesztalkalmazás</span><span class="sxs-lookup"><span data-stu-id="da717-104">Console test app</span></span>

<span data-ttu-id="da717-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="da717-105">**Applies to:**</span></span>

- <span data-ttu-id="da717-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="da717-106">Partner Center</span></span>
- <span data-ttu-id="da717-107">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="da717-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="da717-108">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="da717-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="da717-109">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="da717-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="da717-110">A konzol tesztelési alkalmazás a C# és a Java nyelven érhető el, és a partner Center API-k által támogatott összes forgatókönyvhöz tartalmaz mintakód-kódokat.</span><span class="sxs-lookup"><span data-stu-id="da717-110">The console test app is provided in C# and Java, it provides sample codes for all of the scenarios supported by the Partner Center APIs.</span></span> <span data-ttu-id="da717-111">Teszteléshez is használhatja.</span><span class="sxs-lookup"><span data-stu-id="da717-111">You can also use it for testing.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="da717-112">A kód letöltése</span><span class="sxs-lookup"><span data-stu-id="da717-112">Get the code</span></span>

<span data-ttu-id="da717-113">Töltse le a konzol tesztelési alkalmazásának kódját.</span><span class="sxs-lookup"><span data-stu-id="da717-113">Download the sample code for the console test app.</span></span>

## <a name="net"></a><span data-ttu-id="da717-114">.NET</span><span class="sxs-lookup"><span data-stu-id="da717-114">.NET</span></span>

<span data-ttu-id="da717-115">[Töltse le a mintakód](https://go.microsoft.com/fwlink/p/?LinkId=746682) , és szükség szerint módosítsa.</span><span class="sxs-lookup"><span data-stu-id="da717-115">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=746682) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da717-116">Az alkalmazás létrehozása előtt frissítse a *App.config* fájl értékeit, hogy azok tükrözzék a [partner Center-hitelesítésben](partner-center-authentication.md)létrehozott Azure ad-hitelesítési adatokat.</span><span class="sxs-lookup"><span data-stu-id="da717-116">Before you build the application, update the values in the *App.config* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="da717-117">A korai fejlesztés vagy az éles környezetben történő tesztelés során az integrációs munkafolyamatok fiókjának beállításait kell használnia.</span><span class="sxs-lookup"><span data-stu-id="da717-117">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="da717-118">A *App.config* fájl **ScenarioSettings** részén megadhatja azokat a paramétereket, amelyek automatikusan átkerülnek a futtatott forgatókönyvekben.</span><span class="sxs-lookup"><span data-stu-id="da717-118">Under **ScenarioSettings** in the *App.config* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="da717-119">A futtatott forgatókönyvek listájának módosításához a **IPartnerScenario \[ \] mainScenarios** vagy a *program.cs* -fájlban található egyéni Get- **forgatókönyvek** metódusban talál megjegyzéseket.</span><span class="sxs-lookup"><span data-stu-id="da717-119">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.cs* file.</span></span>

## <a name="java"></a><span data-ttu-id="da717-120">Java</span><span class="sxs-lookup"><span data-stu-id="da717-120">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="da717-121">[Töltse le a mintakód](https://go.microsoft.com/fwlink/p/?LinkId=2026887) , és szükség szerint módosítsa.</span><span class="sxs-lookup"><span data-stu-id="da717-121">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=2026887) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da717-122">Az alkalmazás létrehozása előtt frissítse a fájlban lévő *SamplesConfigurations.js* értékeit, hogy azok tükrözzék a [partner Center-hitelesítésben](partner-center-authentication.md)létrehozott Azure ad-hitelesítési adatokat.</span><span class="sxs-lookup"><span data-stu-id="da717-122">Before you build the application, update the values in the *SamplesConfigurations.json* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="da717-123">A korai fejlesztés vagy az éles környezetben történő tesztelés során az integrációs munkafolyamatok fiókjának beállításait kell használnia.</span><span class="sxs-lookup"><span data-stu-id="da717-123">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="da717-124">A fájl *SamplesConfiguration.js* **ScenarioSettings** alatt megadhatja azokat a paramétereket, amelyek automatikusan átkerülnek a futtatott forgatókönyvekben.</span><span class="sxs-lookup"><span data-stu-id="da717-124">Under **ScenarioSettings** in the *SamplesConfiguration.json* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="da717-125">A futtatott forgatókönyvek listájának módosításához a **IPartnerScenario \[ \] MainScenarios** vagy a *program. Java* fájlban található egyéni **Get-forgatókönyvek** metódusban talál megjegyzéseket.</span><span class="sxs-lookup"><span data-stu-id="da717-125">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.java* file.</span></span>

## <a name="what-to-change"></a><span data-ttu-id="da717-126">Mi a változás?</span><span class="sxs-lookup"><span data-stu-id="da717-126">What to change</span></span>

<span data-ttu-id="da717-127">A következő listában megadhatja, hogy mit kell módosítani, vagy nem változik a mintakód.</span><span class="sxs-lookup"><span data-stu-id="da717-127">Use the following lists to determine what to change or not change in the sample code.</span></span>

### <a name="partnerservicesettings"></a><span data-ttu-id="da717-128">PartnerServiceSettings</span><span class="sxs-lookup"><span data-stu-id="da717-128">PartnerServiceSettings</span></span>

<span data-ttu-id="da717-129">A **PartnerServiceSettings** esetében ne módosítsa a következőt:</span><span class="sxs-lookup"><span data-stu-id="da717-129">For **PartnerServiceSettings**, don't change:</span></span>

- <span data-ttu-id="da717-130">**PartnerServiceApiEndpoint**</span><span class="sxs-lookup"><span data-stu-id="da717-130">**PartnerServiceApiEndpoint**</span></span>
- <span data-ttu-id="da717-131">**AuthenticationAuthorityEndpoint**</span><span class="sxs-lookup"><span data-stu-id="da717-131">**AuthenticationAuthorityEndpoint**</span></span>
- <span data-ttu-id="da717-132">**GraphEndpoint**</span><span class="sxs-lookup"><span data-stu-id="da717-132">**GraphEndpoint**</span></span>
- <span data-ttu-id="da717-133">**CommonDomain**</span><span class="sxs-lookup"><span data-stu-id="da717-133">**CommonDomain**</span></span>

<span data-ttu-id="da717-134">Ezen beállítások mindegyike szükséges ahhoz, hogy a minta API-hívások megfelelően működjenek.</span><span class="sxs-lookup"><span data-stu-id="da717-134">All of these settings are necessary for the sample API calls to properly function.</span></span>

### <a name="userauthentication"></a><span data-ttu-id="da717-135">UserAuthentication</span><span class="sxs-lookup"><span data-stu-id="da717-135">UserAuthentication</span></span>

<span data-ttu-id="da717-136">A **UserAuthentication** esetében módosítania kell a következőt:</span><span class="sxs-lookup"><span data-stu-id="da717-136">For **UserAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="da717-137">**ApplicationId** (a bejelentkezéshez használt Azure Active Directory-alkalmazás azonosítója)</span><span class="sxs-lookup"><span data-stu-id="da717-137">**ApplicationId** (your Azure Active Directory application ID used for login)</span></span>
- <span data-ttu-id="da717-138">**Username** (az Active Directory-beli Felhasználónév)</span><span class="sxs-lookup"><span data-stu-id="da717-138">**UserName** (your active directory username)</span></span>
- <span data-ttu-id="da717-139">**Jelszó** (az Active Directory-jelszó).</span><span class="sxs-lookup"><span data-stu-id="da717-139">**Password** (your active directory password).</span></span>

<span data-ttu-id="da717-140">Ne módosítsa:</span><span class="sxs-lookup"><span data-stu-id="da717-140">Don't change:</span></span>

- <span data-ttu-id="da717-141">**ResourceUrl**</span><span class="sxs-lookup"><span data-stu-id="da717-141">**ResourceUrl**</span></span>
- <span data-ttu-id="da717-142">**RedirectUrl**</span><span class="sxs-lookup"><span data-stu-id="da717-142">**RedirectUrl**</span></span>

### <a name="appauthentication"></a><span data-ttu-id="da717-143">AppAuthentication</span><span class="sxs-lookup"><span data-stu-id="da717-143">AppAuthentication</span></span>

<span data-ttu-id="da717-144">A **AppAuthentication** esetében módosítania kell a következőt:</span><span class="sxs-lookup"><span data-stu-id="da717-144">For **AppAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="da717-145">**ApplicationId** (az alkalmazás-bejelentkezéshez használt Active Directory-alkalmazás azonosítója)</span><span class="sxs-lookup"><span data-stu-id="da717-145">**ApplicationId** (your active directory application ID used for application login)</span></span>
- <span data-ttu-id="da717-146">**ApplicationSecret** (az alkalmazás-bejelentkezéshez használt Active Directory-alkalmazás titka)</span><span class="sxs-lookup"><span data-stu-id="da717-146">**ApplicationSecret** (your active directory application secret used for application login)</span></span>
- <span data-ttu-id="da717-147">**Tartomány** (az Active Directory-tartomány, amelyen az alkalmazás fut)</span><span class="sxs-lookup"><span data-stu-id="da717-147">**Domain** (your active directory domain on which the application is hosted)</span></span>

### <a name="scenariosettings"></a><span data-ttu-id="da717-148">ScenarioSettings</span><span class="sxs-lookup"><span data-stu-id="da717-148">ScenarioSettings</span></span>

<span data-ttu-id="da717-149">A **ScenarioSettings** esetében ne módosítsa a következőt:</span><span class="sxs-lookup"><span data-stu-id="da717-149">For **ScenarioSettings**, don't change:</span></span>

- <span data-ttu-id="da717-150">**CustomerDomainSuffix** (az új ügyfél létrehozásakor használt tartomány utótagja)</span><span class="sxs-lookup"><span data-stu-id="da717-150">**CustomerDomainSuffix** (the domain suffix used when creating a new customer)</span></span>

<span data-ttu-id="da717-151">Választható beállítások.</span><span class="sxs-lookup"><span data-stu-id="da717-151">Optional settings.</span></span> <span data-ttu-id="da717-152">Ha a mezőt üresen hagyja, akkor ezeket az információkat meg kell adni, ha szükség van a forgatókönyv futtatására:</span><span class="sxs-lookup"><span data-stu-id="da717-152">If left blank, this information will need to be inputted when running a scenario where necessary):</span></span>

- <span data-ttu-id="da717-153">**CustomerIdToDelete** (a törléshez használt ügyfél azonosítója)</span><span class="sxs-lookup"><span data-stu-id="da717-153">**CustomerIdToDelete** (the ID of the customer used for deletion)</span></span>
- <span data-ttu-id="da717-154">**DefaultCustomerId** (az ügyfélhez kapcsolódó forgatókönyvekben használandó ügyfél-azonosító)</span><span class="sxs-lookup"><span data-stu-id="da717-154">**DefaultCustomerId** (the customer ID to use in customer-related scenarios)</span></span>
- <span data-ttu-id="da717-155">**DefaultInvoiceID** (a számlázási helyzetekben használandó számlázási azonosító)</span><span class="sxs-lookup"><span data-stu-id="da717-155">**DefaultInvoiceID** (the invoice ID to use in invoice scenarios)</span></span>
- <span data-ttu-id="da717-156">**PartnerMpnId** (a partner MPN-azonosítóját használja a közvetett partneri forgatókönyvekben való használatra)</span><span class="sxs-lookup"><span data-stu-id="da717-156">**PartnerMpnId** (the partner MPN ID to use in indirect partner scenarios)</span></span>
- <span data-ttu-id="da717-157">**DefaultServiceRequestId** (a szolgáltatási kérelem azonosítójának használata a szolgáltatás kérelmezési forgatókönyvében)</span><span class="sxs-lookup"><span data-stu-id="da717-157">**DefaultServiceRequestId** (the service request ID to use in service request scenarios)</span></span>
- <span data-ttu-id="da717-158">**DefaultSupportTopicID** (a szolgáltatási kérelemben használni kívánt támogatási témakör azonosítója)</span><span class="sxs-lookup"><span data-stu-id="da717-158">**DefaultSupportTopicID** (the support topic ID to use in service request scenarios)</span></span>
- <span data-ttu-id="da717-159">**DefaultOfferID** (az ajánlati forgatókönyvekben használandó ajánlat azonosítója)</span><span class="sxs-lookup"><span data-stu-id="da717-159">**DefaultOfferID** (the offer ID to use in offer scenarios)</span></span>
- <span data-ttu-id="da717-160">**DefaultOrderID** (a sorrendben használandó sorrend-azonosító)</span><span class="sxs-lookup"><span data-stu-id="da717-160">**DefaultOrderID** (the order ID to use in order scenarios)</span></span>
- <span data-ttu-id="da717-161">**DefaultSubscriptionID** (az ELŐfizetési azonosítók az előfizetési forgatókönyvekben használhatók)</span><span class="sxs-lookup"><span data-stu-id="da717-161">**DefaultSubscriptionID** (the subscription ID to use in subscription scenarios)</span></span>

<span data-ttu-id="da717-162">A módosítás nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="da717-162">Optional to change.</span></span> <span data-ttu-id="da717-163">Az összes beállítás a lapozható tartalom beolvasása során az egyes lapokon megjelenő bejegyzések mennyiségét határozza meg:</span><span class="sxs-lookup"><span data-stu-id="da717-163">All of these settings specify the amount of entries per page when retrieving paged content:</span></span>

- <span data-ttu-id="da717-164">**CustomerPageSize**</span><span class="sxs-lookup"><span data-stu-id="da717-164">**CustomerPageSize**</span></span>
- <span data-ttu-id="da717-165">**InvoicePageSize**</span><span class="sxs-lookup"><span data-stu-id="da717-165">**InvoicePageSize**</span></span>
- <span data-ttu-id="da717-166">**ServiceRequestPageSize**</span><span class="sxs-lookup"><span data-stu-id="da717-166">**ServiceRequestPageSize**</span></span>
- <span data-ttu-id="da717-167">**DefaultOfferPageSize**</span><span class="sxs-lookup"><span data-stu-id="da717-167">**DefaultOfferPageSize**</span></span>
- <span data-ttu-id="da717-168">**SubscriptionPageSize**</span><span class="sxs-lookup"><span data-stu-id="da717-168">**SubscriptionPageSize**</span></span>
