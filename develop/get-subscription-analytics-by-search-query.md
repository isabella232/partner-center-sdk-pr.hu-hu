---
title: Előfizetés-elemzés lekérdező lekérdezéssel
description: Előfizetés-elemzési információk keresési lekérdezés alapján szűrve való lekérdezhetők.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8df777b9a88206f8b22579f0f445c54d80f7cd64
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548736"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a><span data-ttu-id="3b8aa-103">Előfizetés keresési lekérdezés szerint szűrt elemzési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="3b8aa-103">Get subscription analytics information filtered by a search query</span></span>

<span data-ttu-id="3b8aa-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3b8aa-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3b8aa-105">Előfizetés-elemzési információk lekérdezhetők az ügyfelekről keresési lekérdezés alapján szűrve.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-105">How to get subscription analytics information for your customers filtered by a search query.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b8aa-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="3b8aa-106">Prerequisites</span></span>

- <span data-ttu-id="3b8aa-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3b8aa-108">Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="3b8aa-109">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="3b8aa-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3b8aa-110">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="3b8aa-110">Request syntax</span></span>

| <span data-ttu-id="3b8aa-111">Metódus</span><span class="sxs-lookup"><span data-stu-id="3b8aa-111">Method</span></span> | <span data-ttu-id="3b8aa-112">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="3b8aa-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="3b8aa-113">**Kap**</span><span class="sxs-lookup"><span data-stu-id="3b8aa-113">**GET**</span></span> | <span data-ttu-id="3b8aa-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span><span class="sxs-lookup"><span data-stu-id="3b8aa-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="3b8aa-115">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="3b8aa-115">URI parameters</span></span>

<span data-ttu-id="3b8aa-116">A szervezet azonosításához és a keresés szűréséhez használja a következő szükséges elérésiút-paramétert.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-116">Use the following required path parameter to identify your organization and filter the search.</span></span>

| <span data-ttu-id="3b8aa-117">Név</span><span class="sxs-lookup"><span data-stu-id="3b8aa-117">Name</span></span> | <span data-ttu-id="3b8aa-118">Típus</span><span class="sxs-lookup"><span data-stu-id="3b8aa-118">Type</span></span> | <span data-ttu-id="3b8aa-119">Kötelező</span><span class="sxs-lookup"><span data-stu-id="3b8aa-119">Required</span></span> | <span data-ttu-id="3b8aa-120">Leírás</span><span class="sxs-lookup"><span data-stu-id="3b8aa-120">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="3b8aa-121">filter_string</span><span class="sxs-lookup"><span data-stu-id="3b8aa-121">filter_string</span></span> | <span data-ttu-id="3b8aa-122">sztring</span><span class="sxs-lookup"><span data-stu-id="3b8aa-122">string</span></span> | <span data-ttu-id="3b8aa-123">Igen</span><span class="sxs-lookup"><span data-stu-id="3b8aa-123">Yes</span></span> | <span data-ttu-id="3b8aa-124">Az előfizetés-elemzésre alkalmazandó szűrő.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-124">The filter to apply to the subscription analytics.</span></span> <span data-ttu-id="3b8aa-125">A paraméterben használható szintaxist, mezőket és operátorokat a Szűrőszintaxis és a Szűrőmezők szakaszban láthatja.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-125">See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter.</span></span> |

### <a name="filter-syntax"></a><span data-ttu-id="3b8aa-126">Szűrőszintaxis</span><span class="sxs-lookup"><span data-stu-id="3b8aa-126">Filter syntax</span></span>

<span data-ttu-id="3b8aa-127">A szűrőparaméternek mező-, érték- és operátorkombinációk sorozatának kell lennie.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-127">The filter parameter must be composed as a series of field, value, and operator combinations.</span></span> <span data-ttu-id="3b8aa-128">Több kombináció kombinálható a vagy **`and`** **`or`** operátorok használatával.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-128">Multiple combinations can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="3b8aa-129">Egy nem kódolatlan példa a következő:</span><span class="sxs-lookup"><span data-stu-id="3b8aa-129">An unencoded example looks like this:</span></span>

- <span data-ttu-id="3b8aa-130">Karakterlánc: `?filter=Field operator 'Value'`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-130">String: `?filter=Field operator 'Value'`</span></span>
- <span data-ttu-id="3b8aa-131">Logikai: `?filter=Field operator Value`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-131">Boolean: `?filter=Field operator Value`</span></span>
- <span data-ttu-id="3b8aa-132">Tartalmaz `?filter=contains(field,'value')`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-132">Contains `?filter=contains(field,'value')`</span></span>

### <a name="filter-fields"></a><span data-ttu-id="3b8aa-133">Mezők szűrése</span><span class="sxs-lookup"><span data-stu-id="3b8aa-133">Filter fields</span></span>

<span data-ttu-id="3b8aa-134">A kérés szűrőparamétere egy vagy több olyan utasításokat tartalmaz, amelyek szűrik a válasz sorait.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-134">The filter parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="3b8aa-135">Minden utasítás tartalmaz egy mezőt és egy értéket, amely a vagy az **`eq`** **`ne`** operátorhoz van társítva.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-135">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators.</span></span> <span data-ttu-id="3b8aa-136">Egyes mezők a **`contains`** , , , és **`gt`** **`lt`** **`ge`** **`le`** operátorokat is támogatják.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-136">Some fields also support the **`contains`**, **`gt`**, **`lt`**, **`ge`**, and **`le`** operators.</span></span> <span data-ttu-id="3b8aa-137">Az utasítások vagy operátorok **`and`** használatával **`or`** kombinálhatók.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-137">Statements can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="3b8aa-138">Az alábbiakban példákat talál a szűrősringek használatára:</span><span class="sxs-lookup"><span data-stu-id="3b8aa-138">The following are examples of filter strings:</span></span>

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

<span data-ttu-id="3b8aa-139">Az alábbi táblázat a szűrőparaméter támogatott mezőit és támogató operátorait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-139">The following table shows a list of the supported fields and support operators for the filter parameter.</span></span> <span data-ttu-id="3b8aa-140">A sztringértékeket idézőjelek közé kell tenni.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-140">String values must be surrounded by single quotes.</span></span>

| <span data-ttu-id="3b8aa-141">Paraméter</span><span class="sxs-lookup"><span data-stu-id="3b8aa-141">Parameter</span></span> | <span data-ttu-id="3b8aa-142">Támogatott operátorok</span><span class="sxs-lookup"><span data-stu-id="3b8aa-142">Supported operators</span></span> | <span data-ttu-id="3b8aa-143">Leírás</span><span class="sxs-lookup"><span data-stu-id="3b8aa-143">Description</span></span> |
|-----------|---------------------|-------------|
| <span data-ttu-id="3b8aa-144">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="3b8aa-144">autoRenewEnabled</span></span> | <span data-ttu-id="3b8aa-145">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-145">`eq`, `ne`</span></span> | <span data-ttu-id="3b8aa-146">Egy érték, amely jelzi, hogy az előfizetés automatikusan megújul-e.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-146">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="3b8aa-147">commitmentEndDate (kötelezettségvállalási deddátum)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-147">commitmentEndDate</span></span> | <span data-ttu-id="3b8aa-148">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-148">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="3b8aa-149">Az előfizetés végének dátuma.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-149">The date the subscription ends.</span></span> |
| <span data-ttu-id="3b8aa-150">creationDate (Létrehozás dátuma)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-150">creationDate</span></span> | <span data-ttu-id="3b8aa-151">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-151">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="3b8aa-152">Az előfizetés létrehozási dátuma.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-152">The date the subscription was created.</span></span> |
| <span data-ttu-id="3b8aa-153">currentStateEndDate (aktuális állapot: Dátum)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-153">currentStateEndDate</span></span> | <span data-ttu-id="3b8aa-154">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-154">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="3b8aa-155">Az a dátum, amikor az előfizetés aktuális állapota megváltozik.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-155">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="3b8aa-156">customerMarket</span><span class="sxs-lookup"><span data-stu-id="3b8aa-156">customerMarket</span></span> | <span data-ttu-id="3b8aa-157">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-157">`eq`, `ne`</span></span> | <span data-ttu-id="3b8aa-158">Az az ország/régió, ahol az ügyfél üzleti tevékenységhez tartozik.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-158">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="3b8aa-159">customerName (ügyfél neve)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-159">customerName</span></span> | `contains` | <span data-ttu-id="3b8aa-160">Az ügyfél neve.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-160">The name of the customer.</span></span> |
| <span data-ttu-id="3b8aa-161">customerTenantId (customerTenantId)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-161">customerTenantId</span></span> | <span data-ttu-id="3b8aa-162">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-162">`eq`, `ne`</span></span> | <span data-ttu-id="3b8aa-163">Egy GUID-formátumú sztring, amely azonosítja az ügyfélbérlőt.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-163">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="3b8aa-164">megszüntetésDate</span><span class="sxs-lookup"><span data-stu-id="3b8aa-164">deprovisionedDate</span></span> | <span data-ttu-id="3b8aa-165">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-165">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="3b8aa-166">Az előfizetés megszüntetésének dátuma.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-166">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="3b8aa-167">Az alapértelmezett érték a null.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-167">The default value is null.</span></span> |
| <span data-ttu-id="3b8aa-168">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="3b8aa-168">effectiveStartDate</span></span> | <span data-ttu-id="3b8aa-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="3b8aa-170">Az előfizetés kezdési dátuma.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-170">The date the subscription starts.</span></span> |
| <span data-ttu-id="3b8aa-171">friendlyName (rövid név)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-171">friendlyName</span></span> | `contains` | <span data-ttu-id="3b8aa-172">Az előfizetés neve.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-172">The name of the subscription.</span></span> |
| <span data-ttu-id="3b8aa-173">id</span><span class="sxs-lookup"><span data-stu-id="3b8aa-173">id</span></span> | <span data-ttu-id="3b8aa-174">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-174">`eq`, `ne`</span></span> | <span data-ttu-id="3b8aa-175">Egy GUID-formátumú sztring, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-175">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="3b8aa-176">lastRenewalDate (lastRenewalDate)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-176">lastRenewalDate</span></span> | <span data-ttu-id="3b8aa-177">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-177">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="3b8aa-178">Az előfizetés utolsó megújításának dátuma.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-178">The date that the subscription was last renewed.</span></span> <span data-ttu-id="3b8aa-179">Az alapértelmezett érték a null.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-179">The default value is null.</span></span> |
| <span data-ttu-id="3b8aa-180">lastUsageDate (lastUsageDate)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-180">lastUsageDate</span></span> | <span data-ttu-id="3b8aa-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="3b8aa-182">Az előfizetés utolsó felhasznált dátuma.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-182">The date that the subscription was last used.</span></span> <span data-ttu-id="3b8aa-183">Az alapértelmezett érték a null.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-183">The default value is null.</span></span> |
| <span data-ttu-id="3b8aa-184">partnerazonosító</span><span class="sxs-lookup"><span data-stu-id="3b8aa-184">partnerId</span></span> | <span data-ttu-id="3b8aa-185">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-185">`eq`, `ne`</span></span> | <span data-ttu-id="3b8aa-186">Az MPN-azonosító.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-186">The MPN ID.</span></span> <span data-ttu-id="3b8aa-187">Közvetlen viszonteladó esetén ez az érték a partner MPN-azonosítója lesz.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-187">For a direct reseller, this value will be the MPN ID of the partner.</span></span> <span data-ttu-id="3b8aa-188">Közvetett viszonteladó esetén ez az érték a közvetett viszonteladó MPN-azonosítója lesz.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-188">For an indirect reseller, this value will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="3b8aa-189">partnerName</span><span class="sxs-lookup"><span data-stu-id="3b8aa-189">partnerName</span></span> | <span data-ttu-id="3b8aa-190">sztring</span><span class="sxs-lookup"><span data-stu-id="3b8aa-190">string</span></span> | <span data-ttu-id="3b8aa-191">Annak a partnernek a neve, aki számára az előfizetést megvásárolták</span><span class="sxs-lookup"><span data-stu-id="3b8aa-191">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="3b8aa-192">Productname</span><span class="sxs-lookup"><span data-stu-id="3b8aa-192">productName</span></span> | <span data-ttu-id="3b8aa-193">`contains`, `eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-193">`contains`, `eq`, `ne`</span></span> | <span data-ttu-id="3b8aa-194">A termék neve.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-194">The name of the product.</span></span> |
| <span data-ttu-id="3b8aa-195">providerName (szolgáltató neve)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-195">providerName</span></span> | <span data-ttu-id="3b8aa-196">sztring</span><span class="sxs-lookup"><span data-stu-id="3b8aa-196">string</span></span> | <span data-ttu-id="3b8aa-197">Ha az előfizetési tranzakció a közvetett viszonteladóra történik, a szolgáltató neve az a közvetett szolgáltató, aki megvásárolta az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-197">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>|
| <span data-ttu-id="3b8aa-198">status</span><span class="sxs-lookup"><span data-stu-id="3b8aa-198">status</span></span> | <span data-ttu-id="3b8aa-199">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-199">`eq`, `ne`</span></span> | <span data-ttu-id="3b8aa-200">Az előfizetés állapota.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-200">The subscription status.</span></span> <span data-ttu-id="3b8aa-201">A támogatott értékek: "ACTIVE", "SUSPENDED" vagy "DEPROVISIONED".</span><span class="sxs-lookup"><span data-stu-id="3b8aa-201">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="3b8aa-202">subscriptionType (előfizetés típusa)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-202">subscriptionType</span></span> | <span data-ttu-id="3b8aa-203">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-203">`eq`, `ne`</span></span> | <span data-ttu-id="3b8aa-204">Az előfizetés típusa.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-204">The subscription type.</span></span> <span data-ttu-id="3b8aa-205">**Megjegyzés:** Ez a mező megkülönbözteti a kis- és nagybetűket.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-205">**Note**: This field is case-sensitive.</span></span> <span data-ttu-id="3b8aa-206">Támogatott értékek: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="3b8aa-206">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="3b8aa-207">trialStartDate (próbaindításidátum)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-207">trialStartDate</span></span> | <span data-ttu-id="3b8aa-208">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-208">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="3b8aa-209">Az előfizetés próbaidőszakának elindulásának dátuma.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-209">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="3b8aa-210">Az alapértelmezett érték a null.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-210">The default value is null.</span></span> |
| <span data-ttu-id="3b8aa-211">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="3b8aa-211">trialToPaidConversionDate</span></span> | <span data-ttu-id="3b8aa-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="3b8aa-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="3b8aa-213">Az a dátum, amikor az előfizetés próbaverzióról fizetősre vált.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-213">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="3b8aa-214">Az alapértelmezett érték a null.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-214">The default value is null.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3b8aa-215">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="3b8aa-215">Request headers</span></span>

<span data-ttu-id="3b8aa-216">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-216">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3b8aa-217">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="3b8aa-217">Request body</span></span>

<span data-ttu-id="3b8aa-218">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-218">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3b8aa-219">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="3b8aa-219">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="3b8aa-220">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="3b8aa-220">REST response</span></span>

<span data-ttu-id="3b8aa-221">Ha ez sikeres, a válasz törzse a szűrési feltételeknek megfelelő [előfizetési](partner-center-analytics-resources.md#subscription-resource) erőforrások gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-221">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources that meet the filter criteria.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3b8aa-222">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="3b8aa-222">Response success and error codes</span></span>

<span data-ttu-id="3b8aa-223">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-223">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3b8aa-224">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="3b8aa-224">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3b8aa-225">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3b8aa-225">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3b8aa-226">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="3b8aa-226">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="3b8aa-227">Lásd még</span><span class="sxs-lookup"><span data-stu-id="3b8aa-227">See also</span></span>

- [<span data-ttu-id="3b8aa-228">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="3b8aa-228">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
