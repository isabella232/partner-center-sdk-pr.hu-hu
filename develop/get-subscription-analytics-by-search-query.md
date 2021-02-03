---
title: Előfizetés-elemzés beszerzése keresési lekérdezés alapján
description: A keresési lekérdezés által szűrt előfizetés-elemzési információk beolvasása.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1046ea3c7e813eedae4890eebf6356337c80ede
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767911"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a><span data-ttu-id="b9953-103">Előfizetés keresési lekérdezés szerint szűrt elemzési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="b9953-103">Get subscription analytics information filtered by a search query</span></span>

<span data-ttu-id="b9953-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="b9953-104">**Applies To**</span></span>

- <span data-ttu-id="b9953-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="b9953-105">Partner Center</span></span>
- <span data-ttu-id="b9953-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="b9953-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b9953-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="b9953-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b9953-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="b9953-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b9953-109">Az előfizetés elemzési információinak beszerzése az ügyfelek számára keresési lekérdezés alapján szűrve.</span><span class="sxs-lookup"><span data-stu-id="b9953-109">How to get subscription analytics information for your customers filtered by a search query.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9953-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b9953-110">Prerequisites</span></span>

- <span data-ttu-id="b9953-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="b9953-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b9953-112">Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="b9953-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="b9953-113">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="b9953-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b9953-114">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b9953-114">Request syntax</span></span>

| <span data-ttu-id="b9953-115">Metódus</span><span class="sxs-lookup"><span data-stu-id="b9953-115">Method</span></span> | <span data-ttu-id="b9953-116">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b9953-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="b9953-117">**GET**</span><span class="sxs-lookup"><span data-stu-id="b9953-117">**GET**</span></span> | <span data-ttu-id="b9953-118">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? Filter = {filter_string}</span><span class="sxs-lookup"><span data-stu-id="b9953-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="b9953-119">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="b9953-119">URI parameters</span></span>

<span data-ttu-id="b9953-120">A következő szükséges elérésiút-paraméter használatával azonosíthatja a szervezetét, és szűrheti a keresést.</span><span class="sxs-lookup"><span data-stu-id="b9953-120">Use the following required path parameter to identify your organization and filter the search.</span></span>

| <span data-ttu-id="b9953-121">Név</span><span class="sxs-lookup"><span data-stu-id="b9953-121">Name</span></span> | <span data-ttu-id="b9953-122">Típus</span><span class="sxs-lookup"><span data-stu-id="b9953-122">Type</span></span> | <span data-ttu-id="b9953-123">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b9953-123">Required</span></span> | <span data-ttu-id="b9953-124">Leírás</span><span class="sxs-lookup"><span data-stu-id="b9953-124">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="b9953-125">filter_string</span><span class="sxs-lookup"><span data-stu-id="b9953-125">filter_string</span></span> | <span data-ttu-id="b9953-126">sztring</span><span class="sxs-lookup"><span data-stu-id="b9953-126">string</span></span> | <span data-ttu-id="b9953-127">Igen</span><span class="sxs-lookup"><span data-stu-id="b9953-127">Yes</span></span> | <span data-ttu-id="b9953-128">Az előfizetés-elemzésre alkalmazni kívánt szűrő.</span><span class="sxs-lookup"><span data-stu-id="b9953-128">The filter to apply to the subscription analytics.</span></span> <span data-ttu-id="b9953-129">Az ebben a paraméterben használandó szintaxis, mezők és operátorok szűrése szintaxis és szűrés mezők szakaszban talál.</span><span class="sxs-lookup"><span data-stu-id="b9953-129">See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter.</span></span> |

### <a name="filter-syntax"></a><span data-ttu-id="b9953-130">Szűrési szintaxis</span><span class="sxs-lookup"><span data-stu-id="b9953-130">Filter syntax</span></span>

<span data-ttu-id="b9953-131">A Filter paraméternek mező, érték és operátor kombinációk sorozatának kell lennie.</span><span class="sxs-lookup"><span data-stu-id="b9953-131">The filter parameter must be composed as a series of field, value, and operator combinations.</span></span> <span data-ttu-id="b9953-132">Több kombináció is egyesíthető a **`and`** vagy **`or`** operátorok használatával.</span><span class="sxs-lookup"><span data-stu-id="b9953-132">Multiple combinations can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="b9953-133">A kódolás nélküli példa a következőképpen néz ki:</span><span class="sxs-lookup"><span data-stu-id="b9953-133">An unencoded example looks like this:</span></span>

- <span data-ttu-id="b9953-134">Karakterlánc `?filter=Field operator 'Value'`</span><span class="sxs-lookup"><span data-stu-id="b9953-134">String: `?filter=Field operator 'Value'`</span></span>
- <span data-ttu-id="b9953-135">Logikai `?filter=Field operator Value`</span><span class="sxs-lookup"><span data-stu-id="b9953-135">Boolean: `?filter=Field operator Value`</span></span>
- <span data-ttu-id="b9953-136">Tartalmaz `?filter=contains(field,'value')`</span><span class="sxs-lookup"><span data-stu-id="b9953-136">Contains `?filter=contains(field,'value')`</span></span>

### <a name="filter-fields"></a><span data-ttu-id="b9953-137">Mezők szűrése</span><span class="sxs-lookup"><span data-stu-id="b9953-137">Filter fields</span></span>

<span data-ttu-id="b9953-138">A kérelem Filter paraméterében egy vagy több olyan utasítás található, amely a válasz sorait szűri.</span><span class="sxs-lookup"><span data-stu-id="b9953-138">The filter parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="b9953-139">Minden utasítás tartalmaz egy mezőt és egy értéket, amely társítva van a **`eq`** vagy **`ne`** operátorokhoz.</span><span class="sxs-lookup"><span data-stu-id="b9953-139">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators.</span></span> <span data-ttu-id="b9953-140">Egyes mezők a,, **`contains`** , **`gt`** **`lt`** **`ge`** és **`le`** operátorokat is támogatják.</span><span class="sxs-lookup"><span data-stu-id="b9953-140">Some fields also support the **`contains`**, **`gt`**, **`lt`**, **`ge`**, and **`le`** operators.</span></span> <span data-ttu-id="b9953-141">Az utasítások kombinálhatók a **`and`** vagy **`or`** operátorok használatával.</span><span class="sxs-lookup"><span data-stu-id="b9953-141">Statements can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="b9953-142">A következő példák a szűrési karakterláncokra mutatnak:</span><span class="sxs-lookup"><span data-stu-id="b9953-142">The following are examples of filter strings:</span></span>

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

<span data-ttu-id="b9953-143">A következő táblázat a Filter paraméter támogatott mezőinek és támogatási operátorának listáját tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="b9953-143">The following table shows a list of the supported fields and support operators for the filter parameter.</span></span> <span data-ttu-id="b9953-144">A karakterlánc-értékeket szimpla idézőjelek között kell megadni.</span><span class="sxs-lookup"><span data-stu-id="b9953-144">String values must be surrounded by single quotes.</span></span>

| <span data-ttu-id="b9953-145">Paraméter</span><span class="sxs-lookup"><span data-stu-id="b9953-145">Parameter</span></span> | <span data-ttu-id="b9953-146">Támogatott operátorok</span><span class="sxs-lookup"><span data-stu-id="b9953-146">Supported operators</span></span> | <span data-ttu-id="b9953-147">Leírás</span><span class="sxs-lookup"><span data-stu-id="b9953-147">Description</span></span> |
|-----------|---------------------|-------------|
| <span data-ttu-id="b9953-148">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="b9953-148">autoRenewEnabled</span></span> | <span data-ttu-id="b9953-149">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b9953-149">`eq`, `ne`</span></span> | <span data-ttu-id="b9953-150">Egy érték, amely azt jelzi, hogy az előfizetés automatikusan megújul-e.</span><span class="sxs-lookup"><span data-stu-id="b9953-150">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="b9953-151">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="b9953-151">commitmentEndDate</span></span> | <span data-ttu-id="b9953-152">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b9953-152">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="b9953-153">Az előfizetés befejezésének dátuma.</span><span class="sxs-lookup"><span data-stu-id="b9953-153">The date the subscription ends.</span></span> |
| <span data-ttu-id="b9953-154">creationDate</span><span class="sxs-lookup"><span data-stu-id="b9953-154">creationDate</span></span> | <span data-ttu-id="b9953-155">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b9953-155">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="b9953-156">Az előfizetés létrehozásának dátuma.</span><span class="sxs-lookup"><span data-stu-id="b9953-156">The date the subscription was created.</span></span> |
| <span data-ttu-id="b9953-157">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="b9953-157">currentStateEndDate</span></span> | <span data-ttu-id="b9953-158">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b9953-158">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="b9953-159">Az előfizetés aktuális állapotának változási dátuma.</span><span class="sxs-lookup"><span data-stu-id="b9953-159">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="b9953-160">customerMarket</span><span class="sxs-lookup"><span data-stu-id="b9953-160">customerMarket</span></span> | <span data-ttu-id="b9953-161">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b9953-161">`eq`, `ne`</span></span> | <span data-ttu-id="b9953-162">Az az ország/régió, amelyben az ügyfél üzleti tevékenységet végez.</span><span class="sxs-lookup"><span data-stu-id="b9953-162">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="b9953-163">Customername (</span><span class="sxs-lookup"><span data-stu-id="b9953-163">customerName</span></span> | `contains` | <span data-ttu-id="b9953-164">Az ügyfél neve.</span><span class="sxs-lookup"><span data-stu-id="b9953-164">The name of the customer.</span></span> |
| <span data-ttu-id="b9953-165">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="b9953-165">customerTenantId</span></span> | <span data-ttu-id="b9953-166">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b9953-166">`eq`, `ne`</span></span> | <span data-ttu-id="b9953-167">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfél bérlőjét.</span><span class="sxs-lookup"><span data-stu-id="b9953-167">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="b9953-168">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="b9953-168">deprovisionedDate</span></span> | <span data-ttu-id="b9953-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b9953-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="b9953-170">Az előfizetés megszüntetésének dátuma.</span><span class="sxs-lookup"><span data-stu-id="b9953-170">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="b9953-171">Az alapértelmezett érték null.</span><span class="sxs-lookup"><span data-stu-id="b9953-171">The default value is null.</span></span> |
| <span data-ttu-id="b9953-172">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="b9953-172">effectiveStartDate</span></span> | <span data-ttu-id="b9953-173">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b9953-173">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="b9953-174">Az előfizetés megkezdésének dátuma.</span><span class="sxs-lookup"><span data-stu-id="b9953-174">The date the subscription starts.</span></span> |
| <span data-ttu-id="b9953-175">friendlyName</span><span class="sxs-lookup"><span data-stu-id="b9953-175">friendlyName</span></span> | `contains` | <span data-ttu-id="b9953-176">Az előfizetés neve.</span><span class="sxs-lookup"><span data-stu-id="b9953-176">The name of the subscription.</span></span> |
| <span data-ttu-id="b9953-177">id</span><span class="sxs-lookup"><span data-stu-id="b9953-177">id</span></span> | <span data-ttu-id="b9953-178">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b9953-178">`eq`, `ne`</span></span> | <span data-ttu-id="b9953-179">Egy GUID-formázott karakterlánc, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="b9953-179">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="b9953-180">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="b9953-180">lastRenewalDate</span></span> | <span data-ttu-id="b9953-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b9953-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="b9953-182">Az előfizetés utolsó megújításának dátuma.</span><span class="sxs-lookup"><span data-stu-id="b9953-182">The date that the subscription was last renewed.</span></span> <span data-ttu-id="b9953-183">Az alapértelmezett érték null.</span><span class="sxs-lookup"><span data-stu-id="b9953-183">The default value is null.</span></span> |
| <span data-ttu-id="b9953-184">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="b9953-184">lastUsageDate</span></span> | <span data-ttu-id="b9953-185">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b9953-185">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="b9953-186">Az előfizetés legutóbbi használatának dátuma.</span><span class="sxs-lookup"><span data-stu-id="b9953-186">The date that the subscription was last used.</span></span> <span data-ttu-id="b9953-187">Az alapértelmezett érték null.</span><span class="sxs-lookup"><span data-stu-id="b9953-187">The default value is null.</span></span> |
| <span data-ttu-id="b9953-188">partnerId</span><span class="sxs-lookup"><span data-stu-id="b9953-188">partnerId</span></span> | <span data-ttu-id="b9953-189">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b9953-189">`eq`, `ne`</span></span> | <span data-ttu-id="b9953-190">Az MPN-azonosító.</span><span class="sxs-lookup"><span data-stu-id="b9953-190">The MPN ID.</span></span> <span data-ttu-id="b9953-191">Közvetlen viszonteladó esetén ez az érték lesz a partner MPN-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="b9953-191">For a direct reseller, this value will be the MPN ID of the partner.</span></span> <span data-ttu-id="b9953-192">Közvetett viszonteladó esetén ez az érték lesz a közvetett viszonteladó MPN-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="b9953-192">For an indirect reseller, this value will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="b9953-193">partnerName</span><span class="sxs-lookup"><span data-stu-id="b9953-193">partnerName</span></span> | <span data-ttu-id="b9953-194">sztring</span><span class="sxs-lookup"><span data-stu-id="b9953-194">string</span></span> | <span data-ttu-id="b9953-195">Annak a partnernek a neve, akivel az előfizetést megvásárolták</span><span class="sxs-lookup"><span data-stu-id="b9953-195">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="b9953-196">productName</span><span class="sxs-lookup"><span data-stu-id="b9953-196">productName</span></span> | <span data-ttu-id="b9953-197">`contains`, `eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b9953-197">`contains`, `eq`, `ne`</span></span> | <span data-ttu-id="b9953-198">A termék neve.</span><span class="sxs-lookup"><span data-stu-id="b9953-198">The name of the product.</span></span> |
| <span data-ttu-id="b9953-199">providerName</span><span class="sxs-lookup"><span data-stu-id="b9953-199">providerName</span></span> | <span data-ttu-id="b9953-200">sztring</span><span class="sxs-lookup"><span data-stu-id="b9953-200">string</span></span> | <span data-ttu-id="b9953-201">Ha az előfizetési tranzakció a közvetett viszonteladóhoz kapcsolódik, a szolgáltató neve az a közvetett szolgáltató, aki megvásárolta az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="b9953-201">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>|
| <span data-ttu-id="b9953-202">status</span><span class="sxs-lookup"><span data-stu-id="b9953-202">status</span></span> | <span data-ttu-id="b9953-203">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b9953-203">`eq`, `ne`</span></span> | <span data-ttu-id="b9953-204">Az előfizetés állapota.</span><span class="sxs-lookup"><span data-stu-id="b9953-204">The subscription status.</span></span> <span data-ttu-id="b9953-205">A támogatott értékek a következők: "ACTIVE", "FELFÜGGESZTett" vagy "kiépített".</span><span class="sxs-lookup"><span data-stu-id="b9953-205">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="b9953-206">Ügynökparamétert</span><span class="sxs-lookup"><span data-stu-id="b9953-206">subscriptionType</span></span> | <span data-ttu-id="b9953-207">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="b9953-207">`eq`, `ne`</span></span> | <span data-ttu-id="b9953-208">Az előfizetés típusa.</span><span class="sxs-lookup"><span data-stu-id="b9953-208">The subscription type.</span></span> <span data-ttu-id="b9953-209">**Megjegyzés**: Ez a mező megkülönbözteti a kis-és nagybetűket.</span><span class="sxs-lookup"><span data-stu-id="b9953-209">**Note**: This field is case-sensitive.</span></span> <span data-ttu-id="b9953-210">A támogatott értékek a következők: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="b9953-210">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="b9953-211">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="b9953-211">trialStartDate</span></span> | <span data-ttu-id="b9953-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b9953-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="b9953-213">Az előfizetés Próbaidőszakának elindításának dátuma.</span><span class="sxs-lookup"><span data-stu-id="b9953-213">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="b9953-214">Az alapértelmezett érték null.</span><span class="sxs-lookup"><span data-stu-id="b9953-214">The default value is null.</span></span> |
| <span data-ttu-id="b9953-215">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="b9953-215">trialToPaidConversionDate</span></span> | <span data-ttu-id="b9953-216">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="b9953-216">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="b9953-217">Az előfizetés próbaverzióról fizetettre való konvertálása dátuma.</span><span class="sxs-lookup"><span data-stu-id="b9953-217">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="b9953-218">Az alapértelmezett érték null.</span><span class="sxs-lookup"><span data-stu-id="b9953-218">The default value is null.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b9953-219">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b9953-219">Request headers</span></span>

<span data-ttu-id="b9953-220">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b9953-220">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b9953-221">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b9953-221">Request body</span></span>

<span data-ttu-id="b9953-222">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b9953-222">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b9953-223">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b9953-223">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="b9953-224">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b9953-224">REST response</span></span>

<span data-ttu-id="b9953-225">Ha a művelet sikeres, a válasz törzse olyan [előfizetési](partner-center-analytics-resources.md#subscription-resource) erőforrások gyűjteményét tartalmazza, amelyek megfelelnek a szűrési feltételeknek.</span><span class="sxs-lookup"><span data-stu-id="b9953-225">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources that meet the filter criteria.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b9953-226">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b9953-226">Response success and error codes</span></span>

<span data-ttu-id="b9953-227">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="b9953-227">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b9953-228">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="b9953-228">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b9953-229">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b9953-229">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b9953-230">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b9953-230">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123

{
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="see-also"></a><span data-ttu-id="b9953-231">Lásd még</span><span class="sxs-lookup"><span data-stu-id="b9953-231">See also</span></span>

- [<span data-ttu-id="b9953-232">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="b9953-232">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
