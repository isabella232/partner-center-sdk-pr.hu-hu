---
title: Az összes előfizetés elemzési adatainak lekérése
description: Az előfizetés-elemzési információk beszerzése.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: f32fb99ad52939ae8e9de26276588d3022f18fbc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767711"
---
# <a name="get-all-subscription-analytics-information"></a><span data-ttu-id="1dd46-103">Az összes előfizetés elemzési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="1dd46-103">Get all subscription analytics information</span></span>

<span data-ttu-id="1dd46-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="1dd46-104">**Applies to:**</span></span>

- <span data-ttu-id="1dd46-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="1dd46-105">Partner Center</span></span>
- <span data-ttu-id="1dd46-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="1dd46-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="1dd46-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="1dd46-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="1dd46-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="1dd46-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1dd46-109">Ez a cikk azt ismerteti, hogyan kérhető le az összes előfizetés-elemzési információ az ügyfelek számára.</span><span class="sxs-lookup"><span data-stu-id="1dd46-109">This article describes how to get all the subscription analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dd46-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="1dd46-110">Prerequisites</span></span>

- <span data-ttu-id="1dd46-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="1dd46-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1dd46-112">Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="1dd46-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="1dd46-113">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="1dd46-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1dd46-114">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="1dd46-114">Request syntax</span></span>

| <span data-ttu-id="1dd46-115">Metódus</span><span class="sxs-lookup"><span data-stu-id="1dd46-115">Method</span></span> | <span data-ttu-id="1dd46-116">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="1dd46-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="1dd46-117">**GET**</span><span class="sxs-lookup"><span data-stu-id="1dd46-117">**GET**</span></span> | <span data-ttu-id="1dd46-118">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions http/1.1</span><span class="sxs-lookup"><span data-stu-id="1dd46-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="1dd46-119">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="1dd46-119">URI parameters</span></span>

<span data-ttu-id="1dd46-120">Az alábbi táblázat a választható paramétereket és azok leírásait tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="1dd46-120">The following table lists optional parameters and their descriptions:</span></span>

| <span data-ttu-id="1dd46-121">Paraméter</span><span class="sxs-lookup"><span data-stu-id="1dd46-121">Parameter</span></span> | <span data-ttu-id="1dd46-122">Típus</span><span class="sxs-lookup"><span data-stu-id="1dd46-122">Type</span></span> |  <span data-ttu-id="1dd46-123">Leírás</span><span class="sxs-lookup"><span data-stu-id="1dd46-123">Description</span></span> |
|-----------|------|--------------|
| <span data-ttu-id="1dd46-124">top</span><span class="sxs-lookup"><span data-stu-id="1dd46-124">top</span></span> | <span data-ttu-id="1dd46-125">int</span><span class="sxs-lookup"><span data-stu-id="1dd46-125">int</span></span> | <span data-ttu-id="1dd46-126">A kérelemben visszaadni kívánt adatsorok száma.</span><span class="sxs-lookup"><span data-stu-id="1dd46-126">The number of rows of data to return in the request.</span></span> <span data-ttu-id="1dd46-127">Ha az érték nincs megadva, a maximális érték és az alapértelmezett érték `10000` .</span><span class="sxs-lookup"><span data-stu-id="1dd46-127">If the value isn't specified, the maximum value and the default value are `10000`.</span></span> <span data-ttu-id="1dd46-128">Ha több sor van a lekérdezésben, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldalának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="1dd46-128">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="1dd46-129">kihagyása</span><span class="sxs-lookup"><span data-stu-id="1dd46-129">skip</span></span> | <span data-ttu-id="1dd46-130">int</span><span class="sxs-lookup"><span data-stu-id="1dd46-130">int</span></span> | <span data-ttu-id="1dd46-131">A lekérdezésben kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="1dd46-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="1dd46-132">Használja ezt a paramétert a nagy adathalmazokon keresztüli lapra.</span><span class="sxs-lookup"><span data-stu-id="1dd46-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="1dd46-133">Például, `top=10000` és `skip=0` lekérdezi az első 10000 sort, `top=10000` és `skip=10000` lekéri a következő 10000 sort.</span><span class="sxs-lookup"><span data-stu-id="1dd46-133">For example, `top=10000` and `skip=0` retrieves the first 10000 rows of data, `top=10000` and `skip=10000` retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="1dd46-134">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="1dd46-134">filter</span></span> | <span data-ttu-id="1dd46-135">sztring</span><span class="sxs-lookup"><span data-stu-id="1dd46-135">string</span></span> | <span data-ttu-id="1dd46-136">Egy vagy több olyan utasítás, amely a válasz sorait szűri.</span><span class="sxs-lookup"><span data-stu-id="1dd46-136">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="1dd46-137">Minden szűrő-utasítás tartalmaz egy mezőnevet a válasz törzsében, valamint egy olyan értéket, amely a **`eq`** , a **`ne`** vagy bizonyos mezőkhöz társítva van **`contains`** .</span><span class="sxs-lookup"><span data-stu-id="1dd46-137">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="1dd46-138">Az utasítások kombinálhatók a vagy a használatával **`and`** **`or`** .</span><span class="sxs-lookup"><span data-stu-id="1dd46-138">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="1dd46-139">A karakterlánc-értékeket szimpla idézőjelek között kell megadni a **Filter** paraméterben.</span><span class="sxs-lookup"><span data-stu-id="1dd46-139">String values must be surrounded by single quotes in the **filter** parameter.</span></span> <span data-ttu-id="1dd46-140">Tekintse meg a következő szakaszt a szűrhető mezők és a mezők által támogatott operátorok listájához.</span><span class="sxs-lookup"><span data-stu-id="1dd46-140">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="1dd46-141">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="1dd46-141">aggregationLevel</span></span> | <span data-ttu-id="1dd46-142">sztring</span><span class="sxs-lookup"><span data-stu-id="1dd46-142">string</span></span> | <span data-ttu-id="1dd46-143">Meghatározza azt az időtartományt, amely esetében az összesített adatokat le kell olvasni.</span><span class="sxs-lookup"><span data-stu-id="1dd46-143">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="1dd46-144">A következő karakterláncok egyike lehet: **nap**, **hét** vagy **hónap**.</span><span class="sxs-lookup"><span data-stu-id="1dd46-144">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="1dd46-145">Ha az érték nincs megadva, az alapértelmezett érték a **dateRange**.</span><span class="sxs-lookup"><span data-stu-id="1dd46-145">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="1dd46-146">Ez a paraméter csak akkor érvényes, ha a **groupBy** paraméter részeként egy Date mezőt ad át.</span><span class="sxs-lookup"><span data-stu-id="1dd46-146">This parameter applies only when a date field is passed as part of the **groupBy** parameter.</span></span> |
| <span data-ttu-id="1dd46-147">groupBy</span><span class="sxs-lookup"><span data-stu-id="1dd46-147">groupBy</span></span> | <span data-ttu-id="1dd46-148">sztring</span><span class="sxs-lookup"><span data-stu-id="1dd46-148">string</span></span> | <span data-ttu-id="1dd46-149">Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítést.</span><span class="sxs-lookup"><span data-stu-id="1dd46-149">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1dd46-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="1dd46-150">Request headers</span></span>

<span data-ttu-id="1dd46-151">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1dd46-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1dd46-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="1dd46-152">Request body</span></span>

<span data-ttu-id="1dd46-153">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="1dd46-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1dd46-154">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="1dd46-154">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="1dd46-155">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="1dd46-155">REST response</span></span>

<span data-ttu-id="1dd46-156">Ha ez sikeres, a válasz törzse az [**előfizetési**](partner-center-analytics-resources.md#subscription-resource) erőforrások gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="1dd46-156">If successful, the response body contains a collection of [**Subscription**](partner-center-analytics-resources.md#subscription-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1dd46-157">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="1dd46-157">Response success and error codes</span></span>

<span data-ttu-id="1dd46-158">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="1dd46-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1dd46-159">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="1dd46-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1dd46-160">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1dd46-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1dd46-161">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="1dd46-161">Response example</span></span>

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a><span data-ttu-id="1dd46-162">Lásd még</span><span class="sxs-lookup"><span data-stu-id="1dd46-162">See also</span></span>

- [<span data-ttu-id="1dd46-163">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="1dd46-163">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
