---
title: Előfizetési elemzések beolvasása dátumok vagy kifejezések szerint csoportosítva
description: Előfizetés-elemzési információk beszerzése dátumok vagy kifejezések szerint csoportosítva.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4a9946027fa89f5a93fff5eede86e36a6be5b721
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767908"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a><span data-ttu-id="fee5a-103">Előfizetési elemzések beolvasása dátumok vagy kifejezések szerint csoportosítva</span><span class="sxs-lookup"><span data-stu-id="fee5a-103">Get subscription analytics grouped by dates or terms</span></span>

<span data-ttu-id="fee5a-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="fee5a-104">**Applies To**</span></span>

- <span data-ttu-id="fee5a-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="fee5a-105">Partner Center</span></span>
- <span data-ttu-id="fee5a-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="fee5a-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="fee5a-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="fee5a-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="fee5a-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="fee5a-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fee5a-109">Az előfizetések elemzési információinak beszerzése az ügyfelek számára dátumok vagy kifejezések szerint csoportosítva.</span><span class="sxs-lookup"><span data-stu-id="fee5a-109">How to get subscription analytics information for your customers grouped by dates or terms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fee5a-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="fee5a-110">Prerequisites</span></span>

- <span data-ttu-id="fee5a-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="fee5a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fee5a-112">Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="fee5a-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="fee5a-113">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="fee5a-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fee5a-114">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="fee5a-114">Request syntax</span></span>

| <span data-ttu-id="fee5a-115">Metódus</span><span class="sxs-lookup"><span data-stu-id="fee5a-115">Method</span></span> | <span data-ttu-id="fee5a-116">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="fee5a-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="fee5a-117">**GET**</span><span class="sxs-lookup"><span data-stu-id="fee5a-117">**GET**</span></span> | <span data-ttu-id="fee5a-118">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? groupby = {groupby_queries}</span><span class="sxs-lookup"><span data-stu-id="fee5a-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="fee5a-119">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="fee5a-119">URI parameters</span></span>

<span data-ttu-id="fee5a-120">Használja a következő szükséges elérésiút-paramétereket a szervezet azonosításához és az eredmények csoportosításához.</span><span class="sxs-lookup"><span data-stu-id="fee5a-120">Use the following required path parameters to identify your organization and to group the results.</span></span>

| <span data-ttu-id="fee5a-121">Név</span><span class="sxs-lookup"><span data-stu-id="fee5a-121">Name</span></span> | <span data-ttu-id="fee5a-122">Típus</span><span class="sxs-lookup"><span data-stu-id="fee5a-122">Type</span></span> | <span data-ttu-id="fee5a-123">Kötelező</span><span class="sxs-lookup"><span data-stu-id="fee5a-123">Required</span></span> | <span data-ttu-id="fee5a-124">Leírás</span><span class="sxs-lookup"><span data-stu-id="fee5a-124">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="fee5a-125">groupby_queries</span><span class="sxs-lookup"><span data-stu-id="fee5a-125">groupby_queries</span></span> | <span data-ttu-id="fee5a-126">karakterláncok és dateTime párok</span><span class="sxs-lookup"><span data-stu-id="fee5a-126">pairs of strings and dateTime</span></span> | <span data-ttu-id="fee5a-127">Igen</span><span class="sxs-lookup"><span data-stu-id="fee5a-127">Yes</span></span> | <span data-ttu-id="fee5a-128">Az eredmény szűrésére szolgáló feltételek és dátumok.</span><span class="sxs-lookup"><span data-stu-id="fee5a-128">The terms and dates to filter the result.</span></span> |

### <a name="groupby-syntax"></a><span data-ttu-id="fee5a-129">GroupBy szintaxisa</span><span class="sxs-lookup"><span data-stu-id="fee5a-129">GroupBy syntax</span></span>

<span data-ttu-id="fee5a-130">A Group By paraméternek vesszővel tagolt, mező típusú értékből kell állnia.</span><span class="sxs-lookup"><span data-stu-id="fee5a-130">The group by parameter must be composed as a series of comma separated, field values.</span></span>

<span data-ttu-id="fee5a-131">A kódolás nélküli példa a következőképpen néz ki:</span><span class="sxs-lookup"><span data-stu-id="fee5a-131">An unencoded example looks like this:</span></span>

```http
?groupby=termField1,dateField1,termField2
```

<span data-ttu-id="fee5a-132">A következő táblázat a Group By által támogatott mezők listáját tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="fee5a-132">The following table shows a list of the supported fields for group by.</span></span>

| <span data-ttu-id="fee5a-133">Mező</span><span class="sxs-lookup"><span data-stu-id="fee5a-133">Field</span></span> | <span data-ttu-id="fee5a-134">Típus</span><span class="sxs-lookup"><span data-stu-id="fee5a-134">Type</span></span> | <span data-ttu-id="fee5a-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="fee5a-135">Description</span></span> |
|-------|------|-------------|
| <span data-ttu-id="fee5a-136">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="fee5a-136">customerTenantId</span></span> | <span data-ttu-id="fee5a-137">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-137">string</span></span> | <span data-ttu-id="fee5a-138">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfél bérlőjét.</span><span class="sxs-lookup"><span data-stu-id="fee5a-138">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="fee5a-139">Customername (</span><span class="sxs-lookup"><span data-stu-id="fee5a-139">customerName</span></span> | <span data-ttu-id="fee5a-140">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-140">string</span></span> | <span data-ttu-id="fee5a-141">Az ügyfél neve.</span><span class="sxs-lookup"><span data-stu-id="fee5a-141">The name of the customer.</span></span> |
| <span data-ttu-id="fee5a-142">customerMarket</span><span class="sxs-lookup"><span data-stu-id="fee5a-142">customerMarket</span></span> | <span data-ttu-id="fee5a-143">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-143">string</span></span> | <span data-ttu-id="fee5a-144">Az az ország/régió, amelyben az ügyfél üzleti tevékenységet végez.</span><span class="sxs-lookup"><span data-stu-id="fee5a-144">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="fee5a-145">id</span><span class="sxs-lookup"><span data-stu-id="fee5a-145">id</span></span> | <span data-ttu-id="fee5a-146">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-146">string</span></span> | <span data-ttu-id="fee5a-147">Egy GUID-formázott karakterlánc, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="fee5a-147">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="fee5a-148">status</span><span class="sxs-lookup"><span data-stu-id="fee5a-148">status</span></span> | <span data-ttu-id="fee5a-149">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-149">string</span></span> | <span data-ttu-id="fee5a-150">Az előfizetés állapota.</span><span class="sxs-lookup"><span data-stu-id="fee5a-150">The subscription status.</span></span> <span data-ttu-id="fee5a-151">A támogatott értékek a következők: "ACTIVE", "FELFÜGGESZTett" vagy "kiépített".</span><span class="sxs-lookup"><span data-stu-id="fee5a-151">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="fee5a-152">productName</span><span class="sxs-lookup"><span data-stu-id="fee5a-152">productName</span></span> | <span data-ttu-id="fee5a-153">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-153">string</span></span> | <span data-ttu-id="fee5a-154">A termék neve.</span><span class="sxs-lookup"><span data-stu-id="fee5a-154">The name of the product.</span></span> |
| <span data-ttu-id="fee5a-155">Ügynökparamétert</span><span class="sxs-lookup"><span data-stu-id="fee5a-155">subscriptionType</span></span> | <span data-ttu-id="fee5a-156">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-156">string</span></span> | <span data-ttu-id="fee5a-157">Az előfizetés típusa.</span><span class="sxs-lookup"><span data-stu-id="fee5a-157">The subscription type.</span></span> <span data-ttu-id="fee5a-158">Megjegyzés: Ez a mező megkülönbözteti a kis-és nagybetűket.</span><span class="sxs-lookup"><span data-stu-id="fee5a-158">Note: This field is case sensitive.</span></span> <span data-ttu-id="fee5a-159">A támogatott értékek a következők: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="fee5a-159">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="fee5a-160">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="fee5a-160">autoRenewEnabled</span></span> | <span data-ttu-id="fee5a-161">Logikai</span><span class="sxs-lookup"><span data-stu-id="fee5a-161">Boolean</span></span> | <span data-ttu-id="fee5a-162">Egy érték, amely azt jelzi, hogy az előfizetés automatikusan megújul-e.</span><span class="sxs-lookup"><span data-stu-id="fee5a-162">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="fee5a-163">partnerId</span><span class="sxs-lookup"><span data-stu-id="fee5a-163">partnerId</span></span>  | <span data-ttu-id="fee5a-164">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-164">string</span></span> | <span data-ttu-id="fee5a-165">Az MPN-azonosító.</span><span class="sxs-lookup"><span data-stu-id="fee5a-165">The MPN ID.</span></span> <span data-ttu-id="fee5a-166">Közvetlen viszonteladó esetén ez a paraméter lesz a partner MPN-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="fee5a-166">For a direct reseller, this parameter will be the MPN ID of the partner.</span></span> <span data-ttu-id="fee5a-167">Közvetett viszonteladó esetén ez a paraméter a közvetett viszonteladó MPN-azonosítója lesz.</span><span class="sxs-lookup"><span data-stu-id="fee5a-167">For an indirect reseller, this parameter will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="fee5a-168">friendlyName</span><span class="sxs-lookup"><span data-stu-id="fee5a-168">friendlyName</span></span> | <span data-ttu-id="fee5a-169">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-169">string</span></span> | <span data-ttu-id="fee5a-170">Az előfizetés neve.</span><span class="sxs-lookup"><span data-stu-id="fee5a-170">The name of the subscription.</span></span> |
| <span data-ttu-id="fee5a-171">partnerName</span><span class="sxs-lookup"><span data-stu-id="fee5a-171">partnerName</span></span> | <span data-ttu-id="fee5a-172">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-172">string</span></span> | <span data-ttu-id="fee5a-173">Annak a partnernek a neve, akivel az előfizetést megvásárolták</span><span class="sxs-lookup"><span data-stu-id="fee5a-173">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="fee5a-174">providerName</span><span class="sxs-lookup"><span data-stu-id="fee5a-174">providerName</span></span> | <span data-ttu-id="fee5a-175">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-175">string</span></span> | <span data-ttu-id="fee5a-176">Ha az előfizetési tranzakció a közvetett viszonteladóhoz kapcsolódik, a szolgáltató neve az a közvetett szolgáltató, aki megvásárolta az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="fee5a-176">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>
| <span data-ttu-id="fee5a-177">creationDate</span><span class="sxs-lookup"><span data-stu-id="fee5a-177">creationDate</span></span> | <span data-ttu-id="fee5a-178">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="fee5a-178">string in UTC date time format</span></span> | <span data-ttu-id="fee5a-179">Az előfizetés létrehozásának dátuma.</span><span class="sxs-lookup"><span data-stu-id="fee5a-179">The date the subscription was created.</span></span> |
| <span data-ttu-id="fee5a-180">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="fee5a-180">effectiveStartDate</span></span> | <span data-ttu-id="fee5a-181">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="fee5a-181">string in UTC date time format</span></span> | <span data-ttu-id="fee5a-182">Az előfizetés megkezdésének dátuma.</span><span class="sxs-lookup"><span data-stu-id="fee5a-182">The date the subscription starts.</span></span> |
| <span data-ttu-id="fee5a-183">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="fee5a-183">commitmentEndDate</span></span> | <span data-ttu-id="fee5a-184">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="fee5a-184">string in UTC date time format</span></span> | <span data-ttu-id="fee5a-185">Az előfizetés befejezésének dátuma.</span><span class="sxs-lookup"><span data-stu-id="fee5a-185">The date the subscription ends.</span></span> |
| <span data-ttu-id="fee5a-186">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="fee5a-186">currentStateEndDate</span></span> | <span data-ttu-id="fee5a-187">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="fee5a-187">string in UTC date time format</span></span> | <span data-ttu-id="fee5a-188">Az előfizetés aktuális állapotának változási dátuma.</span><span class="sxs-lookup"><span data-stu-id="fee5a-188">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="fee5a-189">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="fee5a-189">trialToPaidConversionDate</span></span> | <span data-ttu-id="fee5a-190">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="fee5a-190">string in UTC date time format</span></span> | <span data-ttu-id="fee5a-191">Az előfizetés próbaverzióról fizetettre való konvertálása dátuma.</span><span class="sxs-lookup"><span data-stu-id="fee5a-191">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="fee5a-192">Az alapértelmezett érték null.</span><span class="sxs-lookup"><span data-stu-id="fee5a-192">The default value is null.</span></span> |
| <span data-ttu-id="fee5a-193">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="fee5a-193">trialStartDate</span></span> | <span data-ttu-id="fee5a-194">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="fee5a-194">string in UTC date time format</span></span> | <span data-ttu-id="fee5a-195">Az előfizetés Próbaidőszakának elindításának dátuma.</span><span class="sxs-lookup"><span data-stu-id="fee5a-195">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="fee5a-196">Az alapértelmezett érték null.</span><span class="sxs-lookup"><span data-stu-id="fee5a-196">The default value is null.</span></span> |
| <span data-ttu-id="fee5a-197">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="fee5a-197">lastUsageDate</span></span> | <span data-ttu-id="fee5a-198">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="fee5a-198">string in UTC date time format</span></span> | <span data-ttu-id="fee5a-199">Az előfizetés legutóbbi használatának dátuma.</span><span class="sxs-lookup"><span data-stu-id="fee5a-199">The date that the subscription was last used.</span></span> <span data-ttu-id="fee5a-200">Az alapértelmezett érték null.</span><span class="sxs-lookup"><span data-stu-id="fee5a-200">The default value is null.</span></span> |
| <span data-ttu-id="fee5a-201">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="fee5a-201">deprovisionedDate</span></span> | <span data-ttu-id="fee5a-202">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="fee5a-202">string in UTC date time format</span></span> | <span data-ttu-id="fee5a-203">Az előfizetés megszüntetésének dátuma.</span><span class="sxs-lookup"><span data-stu-id="fee5a-203">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="fee5a-204">Az alapértelmezett érték null.</span><span class="sxs-lookup"><span data-stu-id="fee5a-204">The default value is null.</span></span> |
| <span data-ttu-id="fee5a-205">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="fee5a-205">lastRenewalDate</span></span> | <span data-ttu-id="fee5a-206">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="fee5a-206">string in UTC date time format</span></span> | <span data-ttu-id="fee5a-207">Az előfizetés utolsó megújításának dátuma.</span><span class="sxs-lookup"><span data-stu-id="fee5a-207">The date that the subscription was last renewed.</span></span> <span data-ttu-id="fee5a-208">Az alapértelmezett érték null.</span><span class="sxs-lookup"><span data-stu-id="fee5a-208">The default value is null.</span></span> |

### <a name="filter-fields"></a><span data-ttu-id="fee5a-209">Mezők szűrése</span><span class="sxs-lookup"><span data-stu-id="fee5a-209">Filter fields</span></span>

<span data-ttu-id="fee5a-210">A következő táblázat az opcionális szűrési mezőket és azok leírásait tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="fee5a-210">The following table lists optional filter fields and their descriptions:</span></span>

| <span data-ttu-id="fee5a-211">Mező</span><span class="sxs-lookup"><span data-stu-id="fee5a-211">Field</span></span> | <span data-ttu-id="fee5a-212">Típus</span><span class="sxs-lookup"><span data-stu-id="fee5a-212">Type</span></span> |  <span data-ttu-id="fee5a-213">Leírás</span><span class="sxs-lookup"><span data-stu-id="fee5a-213">Description</span></span> |
|-------|------|--------------|
| <span data-ttu-id="fee5a-214">top</span><span class="sxs-lookup"><span data-stu-id="fee5a-214">top</span></span> | <span data-ttu-id="fee5a-215">int</span><span class="sxs-lookup"><span data-stu-id="fee5a-215">int</span></span> | <span data-ttu-id="fee5a-216">A kérelemben visszaadni kívánt adatsorok száma.</span><span class="sxs-lookup"><span data-stu-id="fee5a-216">The number of rows of data to return in the request.</span></span> <span data-ttu-id="fee5a-217">Ha az érték nincs megadva, a maximális érték és az alapértelmezett érték 10000.</span><span class="sxs-lookup"><span data-stu-id="fee5a-217">If the value isn't specified, the maximum value and the default value are 10000.</span></span> <span data-ttu-id="fee5a-218">Ha több sor van a lekérdezésben, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldalának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="fee5a-218">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="fee5a-219">kihagyása</span><span class="sxs-lookup"><span data-stu-id="fee5a-219">skip</span></span> | <span data-ttu-id="fee5a-220">int</span><span class="sxs-lookup"><span data-stu-id="fee5a-220">int</span></span> | <span data-ttu-id="fee5a-221">A lekérdezésben kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="fee5a-221">The number of rows to skip in the query.</span></span> <span data-ttu-id="fee5a-222">Használja ezt a paramétert a nagy adathalmazokon keresztüli lapra.</span><span class="sxs-lookup"><span data-stu-id="fee5a-222">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="fee5a-223">Például a Top = 10000 és a skip = 0 lekérdezi az első 10000 adatsort, a Top = 10000 és a skip = 10000 lekéri a következő 10000 sort.</span><span class="sxs-lookup"><span data-stu-id="fee5a-223">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="fee5a-224">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="fee5a-224">filter</span></span> | <span data-ttu-id="fee5a-225">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-225">string</span></span> | <span data-ttu-id="fee5a-226">Egy vagy több olyan utasítás, amely a válasz sorait szűri.</span><span class="sxs-lookup"><span data-stu-id="fee5a-226">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="fee5a-227">Minden szűrő-utasítás tartalmaz egy mezőnevet a válasz törzsében, valamint egy olyan értéket, amely a **`eq`** , a **`ne`** vagy bizonyos mezőkhöz társítva van **`contains`** .</span><span class="sxs-lookup"><span data-stu-id="fee5a-227">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="fee5a-228">Az utasítások kombinálhatók a vagy a használatával **`and`** **`or`** .</span><span class="sxs-lookup"><span data-stu-id="fee5a-228">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="fee5a-229">A karakterlánc-értékeket szimpla idézőjelek között kell megadni a Filter paraméterben.</span><span class="sxs-lookup"><span data-stu-id="fee5a-229">String values must be surrounded by single quotes in the filter parameter.</span></span> <span data-ttu-id="fee5a-230">Tekintse meg a következő szakaszt a szűrhető mezők és a mezők által támogatott operátorok listájához.</span><span class="sxs-lookup"><span data-stu-id="fee5a-230">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="fee5a-231">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="fee5a-231">aggregationLevel</span></span> | <span data-ttu-id="fee5a-232">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-232">string</span></span> | <span data-ttu-id="fee5a-233">Meghatározza azt az időtartományt, amely esetében az összesített adatokat le kell olvasni.</span><span class="sxs-lookup"><span data-stu-id="fee5a-233">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="fee5a-234">A következő karakterláncok egyike lehet: **nap**, **hét** vagy **hónap**.</span><span class="sxs-lookup"><span data-stu-id="fee5a-234">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="fee5a-235">Ha az érték nincs megadva, az alapértelmezett érték a **dateRange**.</span><span class="sxs-lookup"><span data-stu-id="fee5a-235">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="fee5a-236">**Megjegyzés**: Ez a paraméter csak akkor érvényes, ha a groupBy paraméter részeként egy Date mezőt ad át.</span><span class="sxs-lookup"><span data-stu-id="fee5a-236">**Note**: This parameter applies only when a date field is passed as part of the groupBy parameter.</span></span> |
| <span data-ttu-id="fee5a-237">groupBy</span><span class="sxs-lookup"><span data-stu-id="fee5a-237">groupBy</span></span> | <span data-ttu-id="fee5a-238">sztring</span><span class="sxs-lookup"><span data-stu-id="fee5a-238">string</span></span> | <span data-ttu-id="fee5a-239">Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítést.</span><span class="sxs-lookup"><span data-stu-id="fee5a-239">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fee5a-240">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="fee5a-240">Request headers</span></span>

<span data-ttu-id="fee5a-241">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fee5a-241">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fee5a-242">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="fee5a-242">Request body</span></span>

<span data-ttu-id="fee5a-243">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="fee5a-243">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fee5a-244">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="fee5a-244">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="fee5a-245">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="fee5a-245">REST response</span></span>

<span data-ttu-id="fee5a-246">Ha ez sikeres, a válasz törzse az [előfizetési](partner-center-analytics-resources.md#subscription-resource) erőforrások gyűjteményét tartalmazza a megadott feltételek és dátumok szerint csoportosítva.</span><span class="sxs-lookup"><span data-stu-id="fee5a-246">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources grouped by the specified terms and dates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fee5a-247">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="fee5a-247">Response success and error codes</span></span>

<span data-ttu-id="fee5a-248">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="fee5a-248">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fee5a-249">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="fee5a-249">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fee5a-250">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fee5a-250">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fee5a-251">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="fee5a-251">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a><span data-ttu-id="fee5a-252">Lásd még</span><span class="sxs-lookup"><span data-stu-id="fee5a-252">See also</span></span>

[<span data-ttu-id="fee5a-253">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="fee5a-253">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
