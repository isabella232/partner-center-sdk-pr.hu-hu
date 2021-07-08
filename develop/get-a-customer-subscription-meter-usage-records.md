---
title: Előfizetés használati adatainak lekérése mérő szerint
description: A MeterUsageRecord erőforrás-gyűjtemény használatával lekértheti egy adott Azure-szolgáltatás vagy -erőforrás adott Azure-szolgáltatásainak vagy erőforrásainak fogyasztásmérő-használati rekordjait az aktuális számlázási időszakban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0bd6143c80059bd140a4c4332ab4ec19c54d99f1
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874856"
---
# <a name="get-usage-data-for-subscription-by-meter"></a><span data-ttu-id="a84ab-103">Előfizetés használati adatainak lekérése mérő szerint</span><span class="sxs-lookup"><span data-stu-id="a84ab-103">Get usage data for subscription by meter</span></span>

<span data-ttu-id="a84ab-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a84ab-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a84ab-105">A **MeterUsageRecord** erőforrás-gyűjtemény használatával lekértheti egy adott Azure-szolgáltatás vagy -erőforrás adott Azure-szolgáltatásainak vagy erőforrásainak fogyasztásmérő-használati rekordjait az aktuális számlázási időszakban.</span><span class="sxs-lookup"><span data-stu-id="a84ab-105">You can use the **MeterUsageRecord** resource collection to get meter usage records of a customer for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="a84ab-106">Ez az erőforrás-gyűjtemény az egyes mérők összesített összegzését jelöli az aktuális számlázási ciklusban a teljes Azure-csomagra.</span><span class="sxs-lookup"><span data-stu-id="a84ab-106">This resource collection represents an aggregated total for each meter for the current billing cycle, across your entire Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a84ab-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="a84ab-107">Prerequisites</span></span>

- <span data-ttu-id="a84ab-108">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a84ab-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a84ab-109">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="a84ab-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="a84ab-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a84ab-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a84ab-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="a84ab-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a84ab-112">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a84ab-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a84ab-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a84ab-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a84ab-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="a84ab-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a84ab-115">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a84ab-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a84ab-116">Egy előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="a84ab-116">A subscription ID</span></span>

<span data-ttu-id="a84ab-117">*Ez az új útvonal egyenértékű a értékével, amely továbbra is csak Microsoft Azure `subscriptions/{subscription-id}/usagerecords/resources` (MS-AZR-0145P) előfizetések esetében fog működni.*</span><span class="sxs-lookup"><span data-stu-id="a84ab-117">*This new route is equivalent to `subscriptions/{subscription-id}/usagerecords/resources`, which will continue to function only for Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span> <span data-ttu-id="a84ab-118">Ez az új útvonal a Microsoft Azure (MS-AZR-0145P) előfizetéseket és az Azure-csomagokat is támogatja.</span><span class="sxs-lookup"><span data-stu-id="a84ab-118">This new route will support both Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span> <span data-ttu-id="a84ab-119">Ahhoz, hogy ezt az információt le tudja kapni az Azure-csomaghoz, át kell váltania erre az új útvonalra.</span><span class="sxs-lookup"><span data-stu-id="a84ab-119">In order to get this information for your Azure plan, you need to switch to this new route.</span></span> <span data-ttu-id="a84ab-120">A következő szakaszokban említett tulajdonságokon kívül a válasz ugyanaz, mint a régi útvonal.</span><span class="sxs-lookup"><span data-stu-id="a84ab-120">Other than the properties mentioned in the following sections, the response is the same as the old route.</span></span>

## <a name="c"></a><span data-ttu-id="a84ab-121">C\#</span><span class="sxs-lookup"><span data-stu-id="a84ab-121">C\#</span></span>

<span data-ttu-id="a84ab-122">Egy adott Azure-szolgáltatás vagy -erőforrás adott Azure-szolgáltatásának vagy -erőforrásának fogyasztásmérő-használati rekordjaihoz az aktuális számlázási időszakban:</span><span class="sxs-lookup"><span data-stu-id="a84ab-122">To get meter usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="a84ab-123">Az **IAggregatePartner.Customers gyűjtemény** használatával hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="a84ab-123">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="a84ab-124">Hívja meg a Subscriptions (Előfizetések) tulajdonságot, a **UsageRecords**(Használati adatok) tulajdonságot, majd a **Meters (Mérők)** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="a84ab-124">Call the Subscriptions property, and **UsageRecords**, then the **Meters** property.</span></span> <span data-ttu-id="a84ab-125">Befejezésként hívja meg a Get() vagy a GetAsync() metódust.</span><span class="sxs-lookup"><span data-stu-id="a84ab-125">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

<span data-ttu-id="a84ab-126">Példaként tekintse meg a következő mintát:</span><span class="sxs-lookup"><span data-stu-id="a84ab-126">For an example, see the following sample:</span></span>

- <span data-ttu-id="a84ab-127">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="a84ab-127">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="a84ab-128">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="a84ab-128">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="a84ab-129">Osztály: **GetSubscriptionUsageRecordsByMeter.cs**</span><span class="sxs-lookup"><span data-stu-id="a84ab-129">Class: **GetSubscriptionUsageRecordsByMeter.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="a84ab-130">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="a84ab-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a84ab-131">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="a84ab-131">Request syntax</span></span>

| <span data-ttu-id="a84ab-132">Metódus</span><span class="sxs-lookup"><span data-stu-id="a84ab-132">Method</span></span>  | <span data-ttu-id="a84ab-133">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="a84ab-133">Request URI</span></span>                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a84ab-134">**Kap**</span><span class="sxs-lookup"><span data-stu-id="a84ab-134">**GET**</span></span> | <span data-ttu-id="a84ab-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfél-bérlő-azonosító}/subscriptions/{előfizetés-azonosító}/meterusagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a84ab-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="a84ab-136">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="a84ab-136">URI parameters</span></span>

<span data-ttu-id="a84ab-137">Ez a táblázat felsorolja az ügyfél minősített használati információinak lekérdezhető lekérdezési paramétereit.</span><span class="sxs-lookup"><span data-stu-id="a84ab-137">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="a84ab-138">Név</span><span class="sxs-lookup"><span data-stu-id="a84ab-138">Name</span></span>                   | <span data-ttu-id="a84ab-139">Típus</span><span class="sxs-lookup"><span data-stu-id="a84ab-139">Type</span></span>     | <span data-ttu-id="a84ab-140">Kötelező</span><span class="sxs-lookup"><span data-stu-id="a84ab-140">Required</span></span> | <span data-ttu-id="a84ab-141">Leírás</span><span class="sxs-lookup"><span data-stu-id="a84ab-141">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="a84ab-142">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="a84ab-142">**customer-tenant-id**</span></span> | <span data-ttu-id="a84ab-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="a84ab-143">**guid**</span></span> | <span data-ttu-id="a84ab-144">Y</span><span class="sxs-lookup"><span data-stu-id="a84ab-144">Y</span></span>        | <span data-ttu-id="a84ab-145">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="a84ab-145">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="a84ab-146">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="a84ab-146">**subscription-id**</span></span>    | <span data-ttu-id="a84ab-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="a84ab-147">**guid**</span></span> | <span data-ttu-id="a84ab-148">Y</span><span class="sxs-lookup"><span data-stu-id="a84ab-148">Y</span></span>        | <span data-ttu-id="a84ab-149">Egy Partnerközpont-előfizetési erőforrás azonosítójának megfelelő [](subscription-resources.md#subscription)GUID, amely egy Microsoft Azure-előfizetést (MS-AZR-0145P) vagy egy Azure-csomagot képvisel.</span><span class="sxs-lookup"><span data-stu-id="a84ab-149">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="a84ab-150">*Az Azure-csomag előfizetési erőforrásaihoz adja meg a **csomagazonosítót** **előfizetés-azonosítóként** ebben az útvonalban.*</span><span class="sxs-lookup"><span data-stu-id="a84ab-150">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a84ab-151">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="a84ab-151">Request headers</span></span>

<span data-ttu-id="a84ab-152">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a84ab-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a84ab-153">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="a84ab-153">Request body</span></span>

<span data-ttu-id="a84ab-154">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="a84ab-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a84ab-155">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="a84ab-155">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="a84ab-156">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="a84ab-156">REST response</span></span>

<span data-ttu-id="a84ab-157">Ha ez a metódus sikeres, egy **PagedResourceCollection \<MeterUsageRecord>** erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="a84ab-157">If successful, this method returns a **PagedResourceCollection\<MeterUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a84ab-158">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="a84ab-158">Response success and error codes</span></span>

<span data-ttu-id="a84ab-159">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="a84ab-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a84ab-160">Ezt a kódot, a hibatípust és a további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="a84ab-160">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="a84ab-161">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a84ab-161">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="a84ab-162">Példa válasz Microsoft Azure (MS-AZR-0145P) előfizetésre</span><span class="sxs-lookup"><span data-stu-id="a84ab-162">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="a84ab-163">Ebben a példában az ügyfél **145P Azure PayG-t vásárolt.**</span><span class="sxs-lookup"><span data-stu-id="a84ab-163">In this example, the customer purchased **145P Azure PayG**.</span></span>

<span data-ttu-id="a84ab-164">*A Microsoft Azure (MS-AZR-0145P) előfizetéssel nem változik az API-válasz.*</span><span class="sxs-lookup"><span data-stu-id="a84ab-164">*For customers with a Microsoft Azure (MS-AZR-0145P) subscription, there will be no change to API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "offerId": "MS-AZR-0145P",
            "resourceId": "11111111-F347-41B6-B02C-187B1B778A43",
            "id": "11111111-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/{customer-tenant-id}/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="a84ab-165">PÉLDA REST-válaszra az Azure-csomaghoz</span><span class="sxs-lookup"><span data-stu-id="a84ab-165">REST response example for Azure plan</span></span>

<span data-ttu-id="a84ab-166">Ebben a példában az ügyfél megvásárolt egy Azure-csomag.</span><span class="sxs-lookup"><span data-stu-id="a84ab-166">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="a84ab-167">*Az Azure-csomaggal használó ügyfelek esetében az API-válasz a következő változásokat tartalmazza:*</span><span class="sxs-lookup"><span data-stu-id="a84ab-167">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="a84ab-168">**A currencyLocale** helyett **a currencyCode található**</span><span class="sxs-lookup"><span data-stu-id="a84ab-168">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="a84ab-169">**Az usdTotalCost** egy új mező</span><span class="sxs-lookup"><span data-stu-id="a84ab-169">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
