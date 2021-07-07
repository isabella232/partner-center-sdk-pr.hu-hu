---
title: Konzolos tesztalkalmazás
description: Ez a konzoltesztalkalmazás mintakódot biztosít a Partnerközpont API-k által támogatott összes forgatókönyvhöz. Teszteléshez is használhatja.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b35167104deeede50107d59fca6112c10dc7b4bf
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974029"
---
# <a name="console-test-app"></a><span data-ttu-id="1ea66-104">Konzolos tesztalkalmazás</span><span class="sxs-lookup"><span data-stu-id="1ea66-104">Console test app</span></span>

<span data-ttu-id="1ea66-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1ea66-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1ea66-106">A konzol tesztalkalmazása C# és Java nyelven van megtéve, és mintakódokat biztosít a Partnerközpont API-k által támogatott összes forgatókönyvhöz.</span><span class="sxs-lookup"><span data-stu-id="1ea66-106">The console test app is provided in C# and Java, it provides sample codes for all of the scenarios supported by the Partner Center APIs.</span></span> <span data-ttu-id="1ea66-107">Teszteléshez is használhatja.</span><span class="sxs-lookup"><span data-stu-id="1ea66-107">You can also use it for testing.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="1ea66-108">A kód letöltése</span><span class="sxs-lookup"><span data-stu-id="1ea66-108">Get the code</span></span>

<span data-ttu-id="1ea66-109">Töltse le a konzoltesztalkalmazás mintakódját.</span><span class="sxs-lookup"><span data-stu-id="1ea66-109">Download the sample code for the console test app.</span></span>

## <a name="net"></a><span data-ttu-id="1ea66-110">.NET</span><span class="sxs-lookup"><span data-stu-id="1ea66-110">.NET</span></span>

<span data-ttu-id="1ea66-111">[Töltse le a mintakódot,](https://go.microsoft.com/fwlink/p/?LinkId=746682) és szükség szerint módosítsa.</span><span class="sxs-lookup"><span data-stu-id="1ea66-111">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=746682) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ea66-112">Az alkalmazás létrehozása előtt frissítse a App.config-fájlban található értékeket, hogy azok a hitelesítés során létrehozott Azure [AD-Partnerközpont tükrözzék.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1ea66-112">Before you build the application, update the values in the *App.config* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1ea66-113">Pontosabban az integrációs tesztfiók beállításait kell használnia a fejlesztés korai szakaszában vagy éles környezetben való teszteléshez.</span><span class="sxs-lookup"><span data-stu-id="1ea66-113">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="1ea66-114">A **forgatókönyvfájl ScenarioSettings** *App.config* meg olyan paramétereket, amelyek automatikusan át lesznek állítva a futtatott forgatókönyvekbe.</span><span class="sxs-lookup"><span data-stu-id="1ea66-114">Under **ScenarioSettings** in the *App.config* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="1ea66-115">A futtatott forgatókönyvek listájának módosításához megjegyzésbe kell tenni a sorokat az **IPartnerScenario \[ \] mainScenarios** vagy a *Program.cs* fájlban található egyedi **Forgatókönyv** lekért metódusban.</span><span class="sxs-lookup"><span data-stu-id="1ea66-115">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.cs* file.</span></span>

## <a name="java"></a><span data-ttu-id="1ea66-116">Java</span><span class="sxs-lookup"><span data-stu-id="1ea66-116">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="1ea66-117">[Töltse le a mintakódot,](https://go.microsoft.com/fwlink/p/?LinkId=2026887) és szükség szerint módosítsa.</span><span class="sxs-lookup"><span data-stu-id="1ea66-117">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=2026887) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ea66-118">Az alkalmazás létrehozása előtt frissítse a fájlban *SamplesConfigurations.js* a fájlban található értékeket, hogy tükrözzék a hitelesítés során létrehozott Azure AD Partnerközpont adatokat. [](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1ea66-118">Before you build the application, update the values in the *SamplesConfigurations.json* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1ea66-119">Pontosabban az integrációs tesztfiók beállításait kell használnia a fejlesztés korai szakaszában vagy éles környezetben való teszteléshez.</span><span class="sxs-lookup"><span data-stu-id="1ea66-119">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="1ea66-120">A **Fájlon** találhatóSamplesConfiguration.js *ScenarioSettings* alatt olyan paramétereket állíthat be, amelyek automatikusan át lesznek állítva a futtatott forgatókönyvekbe.</span><span class="sxs-lookup"><span data-stu-id="1ea66-120">Under **ScenarioSettings** in the *SamplesConfiguration.json* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="1ea66-121">A futtatott forgatókönyvek listájának módosításához megjegyzésbe kell tenni a sorokat az **IPartnerScenario \[ \] mainScenarios** vagy a *Program.java* fájlban található egyedi **Forgatókönyv** lekért metódusban.</span><span class="sxs-lookup"><span data-stu-id="1ea66-121">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.java* file.</span></span>

## <a name="what-to-change"></a><span data-ttu-id="1ea66-122">Mi a módosítás?</span><span class="sxs-lookup"><span data-stu-id="1ea66-122">What to change</span></span>

<span data-ttu-id="1ea66-123">Az alábbi listák segítségével meghatározhatja, hogy mit módosíthat a mintakódban.</span><span class="sxs-lookup"><span data-stu-id="1ea66-123">Use the following lists to determine what to change or not change in the sample code.</span></span>

### <a name="partnerservicesettings"></a><span data-ttu-id="1ea66-124">PartnerServiceSettings</span><span class="sxs-lookup"><span data-stu-id="1ea66-124">PartnerServiceSettings</span></span>

<span data-ttu-id="1ea66-125">A **PartnerServiceSettings beállításnál** ne módosítsa a következőt:</span><span class="sxs-lookup"><span data-stu-id="1ea66-125">For **PartnerServiceSettings**, don't change:</span></span>

- <span data-ttu-id="1ea66-126">**PartnerServiceApiEndpoint**</span><span class="sxs-lookup"><span data-stu-id="1ea66-126">**PartnerServiceApiEndpoint**</span></span>
- <span data-ttu-id="1ea66-127">**AuthenticationAuthorityEndpoint**</span><span class="sxs-lookup"><span data-stu-id="1ea66-127">**AuthenticationAuthorityEndpoint**</span></span>
- <span data-ttu-id="1ea66-128">**GraphEndpoint**</span><span class="sxs-lookup"><span data-stu-id="1ea66-128">**GraphEndpoint**</span></span>
- <span data-ttu-id="1ea66-129">**CommonDomain (Tartomány)**</span><span class="sxs-lookup"><span data-stu-id="1ea66-129">**CommonDomain**</span></span>

<span data-ttu-id="1ea66-130">Ezek a beállítások mind szükségesek a minta API-hívások megfelelő működéséhez.</span><span class="sxs-lookup"><span data-stu-id="1ea66-130">All of these settings are necessary for the sample API calls to properly function.</span></span>

### <a name="userauthentication"></a><span data-ttu-id="1ea66-131">UserAuthentication (Felhasználói hitelesítés)</span><span class="sxs-lookup"><span data-stu-id="1ea66-131">UserAuthentication</span></span>

<span data-ttu-id="1ea66-132">A **UserAuthentication** esetén a következőt kell módosítania:</span><span class="sxs-lookup"><span data-stu-id="1ea66-132">For **UserAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="1ea66-133">**ApplicationId** (Azure Active Directory bejelentkezéshez használt alkalmazásazonosító)</span><span class="sxs-lookup"><span data-stu-id="1ea66-133">**ApplicationId** (your Azure Active Directory application ID used for login)</span></span>
- <span data-ttu-id="1ea66-134">**Felhasználónév** (az Active Directory-felhasználóneve)</span><span class="sxs-lookup"><span data-stu-id="1ea66-134">**UserName** (your active directory username)</span></span>
- <span data-ttu-id="1ea66-135">**Jelszó** (az Active Directory-jelszó).</span><span class="sxs-lookup"><span data-stu-id="1ea66-135">**Password** (your active directory password).</span></span>

<span data-ttu-id="1ea66-136">Ne módosítsa:</span><span class="sxs-lookup"><span data-stu-id="1ea66-136">Don't change:</span></span>

- <span data-ttu-id="1ea66-137">**ResourceUrl**</span><span class="sxs-lookup"><span data-stu-id="1ea66-137">**ResourceUrl**</span></span>
- <span data-ttu-id="1ea66-138">**RedirectUrl**</span><span class="sxs-lookup"><span data-stu-id="1ea66-138">**RedirectUrl**</span></span>

### <a name="appauthentication"></a><span data-ttu-id="1ea66-139">AppAuthentication</span><span class="sxs-lookup"><span data-stu-id="1ea66-139">AppAuthentication</span></span>

<span data-ttu-id="1ea66-140">Az **AppAuthentication** esetén a következőt kell módosítania:</span><span class="sxs-lookup"><span data-stu-id="1ea66-140">For **AppAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="1ea66-141">**ApplicationId** (az alkalmazás bejelentkezéshez használt Active Directory-alkalmazásazonosítója)</span><span class="sxs-lookup"><span data-stu-id="1ea66-141">**ApplicationId** (your active directory application ID used for application login)</span></span>
- <span data-ttu-id="1ea66-142">**ApplicationSecret** (az alkalmazásba való bejelentkezéshez használt Active Directory-alkalmazás titkos adatokat használ)</span><span class="sxs-lookup"><span data-stu-id="1ea66-142">**ApplicationSecret** (your active directory application secret used for application login)</span></span>
- <span data-ttu-id="1ea66-143">**Tartomány** (az az Active Directory-tartomány, amelyen az alkalmazás üzemel)</span><span class="sxs-lookup"><span data-stu-id="1ea66-143">**Domain** (your active directory domain on which the application is hosted)</span></span>

### <a name="scenariosettings"></a><span data-ttu-id="1ea66-144">ScenarioSettings (Forgatókönyv-beállítások)</span><span class="sxs-lookup"><span data-stu-id="1ea66-144">ScenarioSettings</span></span>

<span data-ttu-id="1ea66-145">A **ScenarioSettings esetében** ne módosítsa a következőt:</span><span class="sxs-lookup"><span data-stu-id="1ea66-145">For **ScenarioSettings**, don't change:</span></span>

- <span data-ttu-id="1ea66-146">**CustomerDomainSuffix** (az új ügyfél létrehozásakor használt tartomány-utótag)</span><span class="sxs-lookup"><span data-stu-id="1ea66-146">**CustomerDomainSuffix** (the domain suffix used when creating a new customer)</span></span>

<span data-ttu-id="1ea66-147">Nem kötelező beállítások.</span><span class="sxs-lookup"><span data-stu-id="1ea66-147">Optional settings.</span></span> <span data-ttu-id="1ea66-148">Ha üresen hagyja, akkor szükség esetén meg kell határoznia ezt az információt a forgatókönyvek futtatásakor:</span><span class="sxs-lookup"><span data-stu-id="1ea66-148">If left blank, this information will need to be inputted when running a scenario where necessary):</span></span>

- <span data-ttu-id="1ea66-149">**CustomerIdToDelete** (a törléshez használt ügyfél azonosítója)</span><span class="sxs-lookup"><span data-stu-id="1ea66-149">**CustomerIdToDelete** (the ID of the customer used for deletion)</span></span>
- <span data-ttu-id="1ea66-150">**DefaultCustomerId** (az ügyfélhez kapcsolódó forgatókönyvekben használt ügyfélazonosító)</span><span class="sxs-lookup"><span data-stu-id="1ea66-150">**DefaultCustomerId** (the customer ID to use in customer-related scenarios)</span></span>
- <span data-ttu-id="1ea66-151">**DefaultInvoiceID** (a számlázási forgatókönyvekben használt számlaazonosító)</span><span class="sxs-lookup"><span data-stu-id="1ea66-151">**DefaultInvoiceID** (the invoice ID to use in invoice scenarios)</span></span>
- <span data-ttu-id="1ea66-152">**PartnerMpnId** (a közvetett partneri forgatókönyvekben használt partner MPN-azonosítója)</span><span class="sxs-lookup"><span data-stu-id="1ea66-152">**PartnerMpnId** (the partner MPN ID to use in indirect partner scenarios)</span></span>
- <span data-ttu-id="1ea66-153">**DefaultServiceRequestId** (a szolgáltatáskérési forgatókönyvekben használt szolgáltatáskérés-azonosító)</span><span class="sxs-lookup"><span data-stu-id="1ea66-153">**DefaultServiceRequestId** (the service request ID to use in service request scenarios)</span></span>
- <span data-ttu-id="1ea66-154">**DefaultSupportTopicID** (a támogatási témakör szolgáltatáskérési forgatókönyvekben használható azonosítója)</span><span class="sxs-lookup"><span data-stu-id="1ea66-154">**DefaultSupportTopicID** (the support topic ID to use in service request scenarios)</span></span>
- <span data-ttu-id="1ea66-155">**DefaultOfferID** (az ajánlati forgatókönyvekben használt ajánlatazonosító)</span><span class="sxs-lookup"><span data-stu-id="1ea66-155">**DefaultOfferID** (the offer ID to use in offer scenarios)</span></span>
- <span data-ttu-id="1ea66-156">**DefaultOrderID** (a megrendelési forgatókönyvekben használni szükséges rendelésazonosító)</span><span class="sxs-lookup"><span data-stu-id="1ea66-156">**DefaultOrderID** (the order ID to use in order scenarios)</span></span>
- <span data-ttu-id="1ea66-157">**DefaultSubscriptionID** (előfizetési forgatókönyvekben használni szükséges előfizetés-azonosító)</span><span class="sxs-lookup"><span data-stu-id="1ea66-157">**DefaultSubscriptionID** (the subscription ID to use in subscription scenarios)</span></span>

<span data-ttu-id="1ea66-158">Nem kötelező módosítani.</span><span class="sxs-lookup"><span data-stu-id="1ea66-158">Optional to change.</span></span> <span data-ttu-id="1ea66-159">Ezek a beállítások határozzák meg az oldalankénti bejegyzések mennyiségét lapszámozási tartalom leolvasásakor:</span><span class="sxs-lookup"><span data-stu-id="1ea66-159">All of these settings specify the amount of entries per page when retrieving paged content:</span></span>

- <span data-ttu-id="1ea66-160">**CustomerPageSize (CustomerPageSize)**</span><span class="sxs-lookup"><span data-stu-id="1ea66-160">**CustomerPageSize**</span></span>
- <span data-ttu-id="1ea66-161">**InvoicePageSize (Számlaoldalak megszagorizálása**</span><span class="sxs-lookup"><span data-stu-id="1ea66-161">**InvoicePageSize**</span></span>
- <span data-ttu-id="1ea66-162">**ServiceRequestPageSize**</span><span class="sxs-lookup"><span data-stu-id="1ea66-162">**ServiceRequestPageSize**</span></span>
- <span data-ttu-id="1ea66-163">**DefaultOfferPageSize**</span><span class="sxs-lookup"><span data-stu-id="1ea66-163">**DefaultOfferPageSize**</span></span>
- <span data-ttu-id="1ea66-164">**SubscriptionPageSize (Előfizetés lapja)**</span><span class="sxs-lookup"><span data-stu-id="1ea66-164">**SubscriptionPageSize**</span></span>
