---
title: Előfizetés-elemzések lekért dátumai vagy feltételei szerint csoportosítva
description: Előfizetés-elemzési információk lekért dátumok vagy kifejezések szerint csoportosítva.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8192a9863d53ec8697a7341cd38c69200614bd4a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548719"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a><span data-ttu-id="441ec-103">Előfizetés-elemzések lekért dátumai vagy feltételei szerint csoportosítva</span><span class="sxs-lookup"><span data-stu-id="441ec-103">Get subscription analytics grouped by dates or terms</span></span>

<span data-ttu-id="441ec-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="441ec-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="441ec-105">Hogyan lehet lekért előfizetési elemzési adatokat az ügyfelekről dátumok vagy kifejezések szerint csoportosítva.</span><span class="sxs-lookup"><span data-stu-id="441ec-105">How to get subscription analytics information for your customers grouped by dates or terms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="441ec-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="441ec-106">Prerequisites</span></span>

- <span data-ttu-id="441ec-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="441ec-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="441ec-108">Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="441ec-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="441ec-109">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="441ec-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="441ec-110">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="441ec-110">Request syntax</span></span>

| <span data-ttu-id="441ec-111">Metódus</span><span class="sxs-lookup"><span data-stu-id="441ec-111">Method</span></span> | <span data-ttu-id="441ec-112">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="441ec-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="441ec-113">**Kap**</span><span class="sxs-lookup"><span data-stu-id="441ec-113">**GET**</span></span> | <span data-ttu-id="441ec-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span><span class="sxs-lookup"><span data-stu-id="441ec-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="441ec-115">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="441ec-115">URI parameters</span></span>

<span data-ttu-id="441ec-116">Használja a következő kötelező elérésiút-paramétereket a szervezet azonosításához és az eredmények csoportosításához.</span><span class="sxs-lookup"><span data-stu-id="441ec-116">Use the following required path parameters to identify your organization and to group the results.</span></span>

| <span data-ttu-id="441ec-117">Név</span><span class="sxs-lookup"><span data-stu-id="441ec-117">Name</span></span> | <span data-ttu-id="441ec-118">Típus</span><span class="sxs-lookup"><span data-stu-id="441ec-118">Type</span></span> | <span data-ttu-id="441ec-119">Kötelező</span><span class="sxs-lookup"><span data-stu-id="441ec-119">Required</span></span> | <span data-ttu-id="441ec-120">Leírás</span><span class="sxs-lookup"><span data-stu-id="441ec-120">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="441ec-121">groupby_queries</span><span class="sxs-lookup"><span data-stu-id="441ec-121">groupby_queries</span></span> | <span data-ttu-id="441ec-122">sztringpárok és dateTime</span><span class="sxs-lookup"><span data-stu-id="441ec-122">pairs of strings and dateTime</span></span> | <span data-ttu-id="441ec-123">Igen</span><span class="sxs-lookup"><span data-stu-id="441ec-123">Yes</span></span> | <span data-ttu-id="441ec-124">Az eredmény szűréséhez megadott kifejezések és dátumok.</span><span class="sxs-lookup"><span data-stu-id="441ec-124">The terms and dates to filter the result.</span></span> |

### <a name="groupby-syntax"></a><span data-ttu-id="441ec-125">GroupBy-szintaxis</span><span class="sxs-lookup"><span data-stu-id="441ec-125">GroupBy syntax</span></span>

<span data-ttu-id="441ec-126">A csoportosítási paraméternek vesszővel elválasztott mezőértékek sorozataként kell össze lennie.</span><span class="sxs-lookup"><span data-stu-id="441ec-126">The group by parameter must be composed as a series of comma separated, field values.</span></span>

<span data-ttu-id="441ec-127">Egy nem kódolatlan példa a következő:</span><span class="sxs-lookup"><span data-stu-id="441ec-127">An unencoded example looks like this:</span></span>

```http
?groupby=termField1,dateField1,termField2
```

<span data-ttu-id="441ec-128">Az alábbi táblázat a csoportosítási csoportok támogatott mezőinek listáját tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="441ec-128">The following table shows a list of the supported fields for group by.</span></span>

| <span data-ttu-id="441ec-129">Mező</span><span class="sxs-lookup"><span data-stu-id="441ec-129">Field</span></span> | <span data-ttu-id="441ec-130">Típus</span><span class="sxs-lookup"><span data-stu-id="441ec-130">Type</span></span> | <span data-ttu-id="441ec-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="441ec-131">Description</span></span> |
|-------|------|-------------|
| <span data-ttu-id="441ec-132">customerTenantId (customerTenantId)</span><span class="sxs-lookup"><span data-stu-id="441ec-132">customerTenantId</span></span> | <span data-ttu-id="441ec-133">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-133">string</span></span> | <span data-ttu-id="441ec-134">Egy GUID-formátumú sztring, amely azonosítja az ügyfélbérlőt.</span><span class="sxs-lookup"><span data-stu-id="441ec-134">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="441ec-135">customerName (ügyfél neve)</span><span class="sxs-lookup"><span data-stu-id="441ec-135">customerName</span></span> | <span data-ttu-id="441ec-136">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-136">string</span></span> | <span data-ttu-id="441ec-137">Az ügyfél neve.</span><span class="sxs-lookup"><span data-stu-id="441ec-137">The name of the customer.</span></span> |
| <span data-ttu-id="441ec-138">customerMarket</span><span class="sxs-lookup"><span data-stu-id="441ec-138">customerMarket</span></span> | <span data-ttu-id="441ec-139">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-139">string</span></span> | <span data-ttu-id="441ec-140">Az az ország/régió, ahol az ügyfél üzleti tevékenységhez tartozik.</span><span class="sxs-lookup"><span data-stu-id="441ec-140">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="441ec-141">id</span><span class="sxs-lookup"><span data-stu-id="441ec-141">id</span></span> | <span data-ttu-id="441ec-142">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-142">string</span></span> | <span data-ttu-id="441ec-143">Egy GUID-formátumú sztring, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="441ec-143">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="441ec-144">status</span><span class="sxs-lookup"><span data-stu-id="441ec-144">status</span></span> | <span data-ttu-id="441ec-145">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-145">string</span></span> | <span data-ttu-id="441ec-146">Az előfizetés állapota.</span><span class="sxs-lookup"><span data-stu-id="441ec-146">The subscription status.</span></span> <span data-ttu-id="441ec-147">A támogatott értékek: "ACTIVE", "SUSPENDED" vagy "DEPROVISIONED".</span><span class="sxs-lookup"><span data-stu-id="441ec-147">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="441ec-148">Productname</span><span class="sxs-lookup"><span data-stu-id="441ec-148">productName</span></span> | <span data-ttu-id="441ec-149">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-149">string</span></span> | <span data-ttu-id="441ec-150">A termék neve.</span><span class="sxs-lookup"><span data-stu-id="441ec-150">The name of the product.</span></span> |
| <span data-ttu-id="441ec-151">subscriptionType (előfizetés típusa)</span><span class="sxs-lookup"><span data-stu-id="441ec-151">subscriptionType</span></span> | <span data-ttu-id="441ec-152">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-152">string</span></span> | <span data-ttu-id="441ec-153">Az előfizetés típusa.</span><span class="sxs-lookup"><span data-stu-id="441ec-153">The subscription type.</span></span> <span data-ttu-id="441ec-154">Megjegyzés: Ez a mező megkülönbözteti a kis- és nagybetűket.</span><span class="sxs-lookup"><span data-stu-id="441ec-154">Note: This field is case-sensitive.</span></span> <span data-ttu-id="441ec-155">Támogatott értékek: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="441ec-155">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="441ec-156">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="441ec-156">autoRenewEnabled</span></span> | <span data-ttu-id="441ec-157">Logikai</span><span class="sxs-lookup"><span data-stu-id="441ec-157">Boolean</span></span> | <span data-ttu-id="441ec-158">Egy érték, amely jelzi, hogy az előfizetés automatikusan megújul-e.</span><span class="sxs-lookup"><span data-stu-id="441ec-158">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="441ec-159">partnerazonosító</span><span class="sxs-lookup"><span data-stu-id="441ec-159">partnerId</span></span>  | <span data-ttu-id="441ec-160">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-160">string</span></span> | <span data-ttu-id="441ec-161">Az MPN-azonosító.</span><span class="sxs-lookup"><span data-stu-id="441ec-161">The MPN ID.</span></span> <span data-ttu-id="441ec-162">Közvetlen viszonteladó esetén ez a paraméter a partner MPN-azonosítója lesz.</span><span class="sxs-lookup"><span data-stu-id="441ec-162">For a direct reseller, this parameter will be the MPN ID of the partner.</span></span> <span data-ttu-id="441ec-163">Közvetett viszonteladó esetén ez a paraméter a közvetett viszonteladó MPN-azonosítója lesz.</span><span class="sxs-lookup"><span data-stu-id="441ec-163">For an indirect reseller, this parameter will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="441ec-164">friendlyName (rövid név)</span><span class="sxs-lookup"><span data-stu-id="441ec-164">friendlyName</span></span> | <span data-ttu-id="441ec-165">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-165">string</span></span> | <span data-ttu-id="441ec-166">Az előfizetés neve.</span><span class="sxs-lookup"><span data-stu-id="441ec-166">The name of the subscription.</span></span> |
| <span data-ttu-id="441ec-167">partnerName</span><span class="sxs-lookup"><span data-stu-id="441ec-167">partnerName</span></span> | <span data-ttu-id="441ec-168">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-168">string</span></span> | <span data-ttu-id="441ec-169">Annak a partnernek a neve, aki számára az előfizetést megvásárolták</span><span class="sxs-lookup"><span data-stu-id="441ec-169">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="441ec-170">providerName (szolgáltató neve)</span><span class="sxs-lookup"><span data-stu-id="441ec-170">providerName</span></span> | <span data-ttu-id="441ec-171">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-171">string</span></span> | <span data-ttu-id="441ec-172">Ha az előfizetési tranzakció a közvetett viszonteladóra történik, a szolgáltató neve az a közvetett szolgáltató, aki megvásárolta az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="441ec-172">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>
| <span data-ttu-id="441ec-173">creationDate (Létrehozás dátuma)</span><span class="sxs-lookup"><span data-stu-id="441ec-173">creationDate</span></span> | <span data-ttu-id="441ec-174">sztring UTC dátum-idő formátumban</span><span class="sxs-lookup"><span data-stu-id="441ec-174">string in UTC date time format</span></span> | <span data-ttu-id="441ec-175">Az előfizetés létrehozási dátuma.</span><span class="sxs-lookup"><span data-stu-id="441ec-175">The date the subscription was created.</span></span> |
| <span data-ttu-id="441ec-176">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="441ec-176">effectiveStartDate</span></span> | <span data-ttu-id="441ec-177">sztring UTC dátum-idő formátumban</span><span class="sxs-lookup"><span data-stu-id="441ec-177">string in UTC date time format</span></span> | <span data-ttu-id="441ec-178">Az előfizetés kezdési dátuma.</span><span class="sxs-lookup"><span data-stu-id="441ec-178">The date the subscription starts.</span></span> |
| <span data-ttu-id="441ec-179">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="441ec-179">commitmentEndDate</span></span> | <span data-ttu-id="441ec-180">sztring UTC dátum-idő formátumban</span><span class="sxs-lookup"><span data-stu-id="441ec-180">string in UTC date time format</span></span> | <span data-ttu-id="441ec-181">Az előfizetés végének dátuma.</span><span class="sxs-lookup"><span data-stu-id="441ec-181">The date the subscription ends.</span></span> |
| <span data-ttu-id="441ec-182">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="441ec-182">currentStateEndDate</span></span> | <span data-ttu-id="441ec-183">sztring UTC dátum-idő formátumban</span><span class="sxs-lookup"><span data-stu-id="441ec-183">string in UTC date time format</span></span> | <span data-ttu-id="441ec-184">Az a dátum, amikor az előfizetés aktuális állapota megváltozik.</span><span class="sxs-lookup"><span data-stu-id="441ec-184">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="441ec-185">trialToPaidConversionDate (trialToPaidConversionDate)</span><span class="sxs-lookup"><span data-stu-id="441ec-185">trialToPaidConversionDate</span></span> | <span data-ttu-id="441ec-186">sztring UTC dátum-idő formátumban</span><span class="sxs-lookup"><span data-stu-id="441ec-186">string in UTC date time format</span></span> | <span data-ttu-id="441ec-187">Az a dátum, amikor az előfizetés próbaverzióról fizetősre vált.</span><span class="sxs-lookup"><span data-stu-id="441ec-187">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="441ec-188">Az alapértelmezett érték a null.</span><span class="sxs-lookup"><span data-stu-id="441ec-188">The default value is null.</span></span> |
| <span data-ttu-id="441ec-189">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="441ec-189">trialStartDate</span></span> | <span data-ttu-id="441ec-190">sztring UTC dátum-idő formátumban</span><span class="sxs-lookup"><span data-stu-id="441ec-190">string in UTC date time format</span></span> | <span data-ttu-id="441ec-191">Az előfizetés próbaidőszakának elindulásának dátuma.</span><span class="sxs-lookup"><span data-stu-id="441ec-191">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="441ec-192">Az alapértelmezett érték a null.</span><span class="sxs-lookup"><span data-stu-id="441ec-192">The default value is null.</span></span> |
| <span data-ttu-id="441ec-193">lastUsageDate (lastUsageDate)</span><span class="sxs-lookup"><span data-stu-id="441ec-193">lastUsageDate</span></span> | <span data-ttu-id="441ec-194">sztring UTC dátum-idő formátumban</span><span class="sxs-lookup"><span data-stu-id="441ec-194">string in UTC date time format</span></span> | <span data-ttu-id="441ec-195">Az előfizetés utolsó használt dátuma.</span><span class="sxs-lookup"><span data-stu-id="441ec-195">The date that the subscription was last used.</span></span> <span data-ttu-id="441ec-196">Az alapértelmezett érték a null.</span><span class="sxs-lookup"><span data-stu-id="441ec-196">The default value is null.</span></span> |
| <span data-ttu-id="441ec-197">megszüntetésDate</span><span class="sxs-lookup"><span data-stu-id="441ec-197">deprovisionedDate</span></span> | <span data-ttu-id="441ec-198">sztring UTC dátum-idő formátumban</span><span class="sxs-lookup"><span data-stu-id="441ec-198">string in UTC date time format</span></span> | <span data-ttu-id="441ec-199">Az előfizetés megszüntetésének dátuma.</span><span class="sxs-lookup"><span data-stu-id="441ec-199">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="441ec-200">Az alapértelmezett érték a null.</span><span class="sxs-lookup"><span data-stu-id="441ec-200">The default value is null.</span></span> |
| <span data-ttu-id="441ec-201">lastRenewalDate (lastRenewalDate)</span><span class="sxs-lookup"><span data-stu-id="441ec-201">lastRenewalDate</span></span> | <span data-ttu-id="441ec-202">sztring UTC dátum-idő formátumban</span><span class="sxs-lookup"><span data-stu-id="441ec-202">string in UTC date time format</span></span> | <span data-ttu-id="441ec-203">Az előfizetés utolsó megújításának dátuma.</span><span class="sxs-lookup"><span data-stu-id="441ec-203">The date that the subscription was last renewed.</span></span> <span data-ttu-id="441ec-204">Az alapértelmezett érték a null.</span><span class="sxs-lookup"><span data-stu-id="441ec-204">The default value is null.</span></span> |

### <a name="filter-fields"></a><span data-ttu-id="441ec-205">Mezők szűrése</span><span class="sxs-lookup"><span data-stu-id="441ec-205">Filter fields</span></span>

<span data-ttu-id="441ec-206">A következő táblázat a nem kötelező szűrőmezőket és azok leírását tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="441ec-206">The following table lists optional filter fields and their descriptions:</span></span>

| <span data-ttu-id="441ec-207">Mező</span><span class="sxs-lookup"><span data-stu-id="441ec-207">Field</span></span> | <span data-ttu-id="441ec-208">Típus</span><span class="sxs-lookup"><span data-stu-id="441ec-208">Type</span></span> |  <span data-ttu-id="441ec-209">Leírás</span><span class="sxs-lookup"><span data-stu-id="441ec-209">Description</span></span> |
|-------|------|--------------|
| <span data-ttu-id="441ec-210">top</span><span class="sxs-lookup"><span data-stu-id="441ec-210">top</span></span> | <span data-ttu-id="441ec-211">int</span><span class="sxs-lookup"><span data-stu-id="441ec-211">int</span></span> | <span data-ttu-id="441ec-212">A kérelemben visszaadni kívánt adatsorok száma.</span><span class="sxs-lookup"><span data-stu-id="441ec-212">The number of rows of data to return in the request.</span></span> <span data-ttu-id="441ec-213">Ha az érték nincs megadva, a maximális érték és az alapértelmezett érték 10000.</span><span class="sxs-lookup"><span data-stu-id="441ec-213">If the value isn't specified, the maximum value and the default value are 10000.</span></span> <span data-ttu-id="441ec-214">Ha a lekérdezés több sort tartalmaz, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldal lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="441ec-214">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="441ec-215">Ugrál</span><span class="sxs-lookup"><span data-stu-id="441ec-215">skip</span></span> | <span data-ttu-id="441ec-216">int</span><span class="sxs-lookup"><span data-stu-id="441ec-216">int</span></span> | <span data-ttu-id="441ec-217">A lekérdezésben kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="441ec-217">The number of rows to skip in the query.</span></span> <span data-ttu-id="441ec-218">Ezzel a paraméterrel nagy adatkészletek között lapokat laposszunk.</span><span class="sxs-lookup"><span data-stu-id="441ec-218">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="441ec-219">Például a top=10000 és a skip=0 lekéri az első 10000 adatsort, a top=10000 és a skip=10000 pedig a következő 10000 adatsort.</span><span class="sxs-lookup"><span data-stu-id="441ec-219">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="441ec-220">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="441ec-220">filter</span></span> | <span data-ttu-id="441ec-221">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-221">string</span></span> | <span data-ttu-id="441ec-222">Egy vagy több utasítás, amely szűri a válasz sorait.</span><span class="sxs-lookup"><span data-stu-id="441ec-222">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="441ec-223">Minden filter utasítás tartalmaz egy mezőnevet a válasz törzséből, valamint egy értéket, amely a , vagy bizonyos mezőkhöz, az operátorhoz **`eq`** **`ne`** van **`contains`** társítva.</span><span class="sxs-lookup"><span data-stu-id="441ec-223">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="441ec-224">Az utasítások kombinálhatók a vagy **`and`** a **`or`** használatával.</span><span class="sxs-lookup"><span data-stu-id="441ec-224">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="441ec-225">A sztringértékeket a szűrőparaméterben idézőjelek közé kell tenni.</span><span class="sxs-lookup"><span data-stu-id="441ec-225">String values must be surrounded by single quotes in the filter parameter.</span></span> <span data-ttu-id="441ec-226">A következő szakaszban felsoroljuk a szűrhető mezőket, valamint az ezekhez a mezőkhöz támogatott operátorokat.</span><span class="sxs-lookup"><span data-stu-id="441ec-226">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="441ec-227">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="441ec-227">aggregationLevel</span></span> | <span data-ttu-id="441ec-228">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-228">string</span></span> | <span data-ttu-id="441ec-229">Megadja az összesített adatok lekérésének időtartományát.</span><span class="sxs-lookup"><span data-stu-id="441ec-229">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="441ec-230">A következő sztringek egyike lehet: **day,** **week**, vagy **month.**</span><span class="sxs-lookup"><span data-stu-id="441ec-230">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="441ec-231">Ha az érték nincs megadva, az alapértelmezett érték **a dateRange.**</span><span class="sxs-lookup"><span data-stu-id="441ec-231">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="441ec-232">**Megjegyzés:** Ez a paraméter csak akkor érvényes, ha egy dátummezőt ad át a groupBy paraméter részeként.</span><span class="sxs-lookup"><span data-stu-id="441ec-232">**Note**: This parameter applies only when a date field is passed as part of the groupBy parameter.</span></span> |
| <span data-ttu-id="441ec-233">groupBy</span><span class="sxs-lookup"><span data-stu-id="441ec-233">groupBy</span></span> | <span data-ttu-id="441ec-234">sztring</span><span class="sxs-lookup"><span data-stu-id="441ec-234">string</span></span> | <span data-ttu-id="441ec-235">Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítőt.</span><span class="sxs-lookup"><span data-stu-id="441ec-235">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="441ec-236">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="441ec-236">Request headers</span></span>

<span data-ttu-id="441ec-237">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="441ec-237">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="441ec-238">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="441ec-238">Request body</span></span>

<span data-ttu-id="441ec-239">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="441ec-239">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="441ec-240">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="441ec-240">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="441ec-241">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="441ec-241">REST response</span></span>

<span data-ttu-id="441ec-242">Ha ez sikeres, a válasz [](partner-center-analytics-resources.md#subscription-resource) törzse a megadott feltételek és dátumok szerint csoportosított előfizetési erőforrások gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="441ec-242">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources grouped by the specified terms and dates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="441ec-243">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="441ec-243">Response success and error codes</span></span>

<span data-ttu-id="441ec-244">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="441ec-244">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="441ec-245">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="441ec-245">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="441ec-246">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="441ec-246">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="441ec-247">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="441ec-247">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="441ec-248">Lásd még</span><span class="sxs-lookup"><span data-stu-id="441ec-248">See also</span></span>

[<span data-ttu-id="441ec-249">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="441ec-249">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
