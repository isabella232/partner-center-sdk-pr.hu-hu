---
title: Az összes előfizetés elemzési adatainak lekérése
description: Az összes előfizetés-elemzési információ lekért adatai.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: e1f16c92569a02bc51c96a85ecb642fbeb76a9a7
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760249"
---
# <a name="get-all-subscription-analytics-information"></a><span data-ttu-id="eac78-103">Az összes előfizetés elemzési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="eac78-103">Get all subscription analytics information</span></span>

<span data-ttu-id="eac78-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="eac78-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="eac78-105">Ez a cikk azt ismerteti, hogyan lehet lekért összes előfizetési elemzési információt lekért ügyfelek számára.</span><span class="sxs-lookup"><span data-stu-id="eac78-105">This article describes how to get all the subscription analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eac78-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="eac78-106">Prerequisites</span></span>

- <span data-ttu-id="eac78-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="eac78-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="eac78-108">Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="eac78-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="eac78-109">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="eac78-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="eac78-110">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="eac78-110">Request syntax</span></span>

| <span data-ttu-id="eac78-111">Metódus</span><span class="sxs-lookup"><span data-stu-id="eac78-111">Method</span></span> | <span data-ttu-id="eac78-112">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="eac78-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="eac78-113">**Kap**</span><span class="sxs-lookup"><span data-stu-id="eac78-113">**GET**</span></span> | <span data-ttu-id="eac78-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="eac78-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="eac78-115">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="eac78-115">URI parameters</span></span>

<span data-ttu-id="eac78-116">A következő táblázat a választható paramétereket és azok leírását sorolja fel:</span><span class="sxs-lookup"><span data-stu-id="eac78-116">The following table lists optional parameters and their descriptions:</span></span>

| <span data-ttu-id="eac78-117">Paraméter</span><span class="sxs-lookup"><span data-stu-id="eac78-117">Parameter</span></span> | <span data-ttu-id="eac78-118">Típus</span><span class="sxs-lookup"><span data-stu-id="eac78-118">Type</span></span> |  <span data-ttu-id="eac78-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="eac78-119">Description</span></span> |
|-----------|------|--------------|
| <span data-ttu-id="eac78-120">top</span><span class="sxs-lookup"><span data-stu-id="eac78-120">top</span></span> | <span data-ttu-id="eac78-121">int</span><span class="sxs-lookup"><span data-stu-id="eac78-121">int</span></span> | <span data-ttu-id="eac78-122">A kérelemben visszaadni kívánt adatsorok száma.</span><span class="sxs-lookup"><span data-stu-id="eac78-122">The number of rows of data to return in the request.</span></span> <span data-ttu-id="eac78-123">Ha az érték nincs megadva, a maximális érték és az alapértelmezett érték `10000` .</span><span class="sxs-lookup"><span data-stu-id="eac78-123">If the value isn't specified, the maximum value and the default value are `10000`.</span></span> <span data-ttu-id="eac78-124">Ha a lekérdezés több sort tartalmaz, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldal lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="eac78-124">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="eac78-125">Ugrál</span><span class="sxs-lookup"><span data-stu-id="eac78-125">skip</span></span> | <span data-ttu-id="eac78-126">int</span><span class="sxs-lookup"><span data-stu-id="eac78-126">int</span></span> | <span data-ttu-id="eac78-127">A lekérdezésben kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="eac78-127">The number of rows to skip in the query.</span></span> <span data-ttu-id="eac78-128">Ezzel a paraméterrel nagy adatkészletek között lapokat laposszunk.</span><span class="sxs-lookup"><span data-stu-id="eac78-128">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="eac78-129">A például lekéri az első 10000 adatsort, és lekéri a következő `top=10000` `skip=0` `top=10000` `skip=10000` 10000 adatsort.</span><span class="sxs-lookup"><span data-stu-id="eac78-129">For example, `top=10000` and `skip=0` retrieves the first 10000 rows of data, `top=10000` and `skip=10000` retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="eac78-130">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="eac78-130">filter</span></span> | <span data-ttu-id="eac78-131">sztring</span><span class="sxs-lookup"><span data-stu-id="eac78-131">string</span></span> | <span data-ttu-id="eac78-132">Egy vagy több utasítás, amely szűri a válasz sorait.</span><span class="sxs-lookup"><span data-stu-id="eac78-132">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="eac78-133">Minden filter utasítás tartalmaz egy mezőnevet a válasz törzséből, valamint egy értéket, amely a , vagy egyes mezőkhöz, a operátorhoz **`eq`** **`ne`** van **`contains`** társítva.</span><span class="sxs-lookup"><span data-stu-id="eac78-133">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="eac78-134">Az utasítások kombinálhatók a vagy **`and`** a **`or`** használatával.</span><span class="sxs-lookup"><span data-stu-id="eac78-134">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="eac78-135">A sztringértékeket a szűrőparaméterben idézőjelek közé **kell tenni.**</span><span class="sxs-lookup"><span data-stu-id="eac78-135">String values must be surrounded by single quotes in the **filter** parameter.</span></span> <span data-ttu-id="eac78-136">A következő szakaszban felsoroljuk a szűrhető mezőket, valamint az ezekhez a mezőkhöz támogatott operátorokat.</span><span class="sxs-lookup"><span data-stu-id="eac78-136">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="eac78-137">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="eac78-137">aggregationLevel</span></span> | <span data-ttu-id="eac78-138">sztring</span><span class="sxs-lookup"><span data-stu-id="eac78-138">string</span></span> | <span data-ttu-id="eac78-139">Megadja az összesített adatok lekérésének időtartományát.</span><span class="sxs-lookup"><span data-stu-id="eac78-139">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="eac78-140">A következő sztringek egyike lehet: **day,** **week**, vagy **month.**</span><span class="sxs-lookup"><span data-stu-id="eac78-140">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="eac78-141">Ha az érték nincs megadva, az alapértelmezett érték **a dateRange.**</span><span class="sxs-lookup"><span data-stu-id="eac78-141">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="eac78-142">Ez a paraméter csak akkor érvényes, ha egy dátummezőt ad át a **groupBy paraméter** részeként.</span><span class="sxs-lookup"><span data-stu-id="eac78-142">This parameter applies only when a date field is passed as part of the **groupBy** parameter.</span></span> |
| <span data-ttu-id="eac78-143">groupBy</span><span class="sxs-lookup"><span data-stu-id="eac78-143">groupBy</span></span> | <span data-ttu-id="eac78-144">sztring</span><span class="sxs-lookup"><span data-stu-id="eac78-144">string</span></span> | <span data-ttu-id="eac78-145">Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítőt.</span><span class="sxs-lookup"><span data-stu-id="eac78-145">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="eac78-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="eac78-146">Request headers</span></span>

<span data-ttu-id="eac78-147">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="eac78-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="eac78-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="eac78-148">Request body</span></span>

<span data-ttu-id="eac78-149">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="eac78-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="eac78-150">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="eac78-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="eac78-151">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="eac78-151">REST response</span></span>

<span data-ttu-id="eac78-152">Ha a művelet sikeres, a válasz törzse előfizetési erőforrások [**gyűjteményét**](partner-center-analytics-resources.md#subscription-resource) tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="eac78-152">If successful, the response body contains a collection of [**Subscription**](partner-center-analytics-resources.md#subscription-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="eac78-153">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="eac78-153">Response success and error codes</span></span>

<span data-ttu-id="eac78-154">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="eac78-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="eac78-155">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="eac78-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="eac78-156">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="eac78-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="eac78-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="eac78-157">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="eac78-158">Lásd még</span><span class="sxs-lookup"><span data-stu-id="eac78-158">See also</span></span>

- [<span data-ttu-id="eac78-159">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="eac78-159">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
