---
title: Előfizetés használati adatainak lekérése mérő szerint
description: A MeterUsageRecord erőforrás-gyűjtemény használatával beolvashatja az adott Azure-szolgáltatásokra vagy-erőforrásokra vonatkozó használati adatokat az aktuális számlázási időszak alatt.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df981eae8d2caee2dcb7f36696725ec011ead75b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767972"
---
# <a name="get-usage-data-for-subscription-by-meter"></a><span data-ttu-id="baeab-103">Előfizetés használati adatainak lekérése mérő szerint</span><span class="sxs-lookup"><span data-stu-id="baeab-103">Get usage data for subscription by meter</span></span>

<span data-ttu-id="baeab-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="baeab-104">**Applies to:**</span></span>

- <span data-ttu-id="baeab-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="baeab-105">Partner Center</span></span>
- <span data-ttu-id="baeab-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="baeab-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="baeab-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="baeab-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="baeab-108">A **MeterUsageRecord** erőforrás-gyűjtemény használatával beolvashatja az adott Azure-szolgáltatásokra vagy-erőforrásokra vonatkozó használati adatokat az aktuális számlázási időszak alatt.</span><span class="sxs-lookup"><span data-stu-id="baeab-108">You can use the **MeterUsageRecord** resource collection to get meter usage records of a customer for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="baeab-109">Ez az erőforrás-gyűjtemény az aktuális számlázási ciklushoz tartozó összes mérőszám összesített összegét képviseli a teljes Azure-csomagon belül.</span><span class="sxs-lookup"><span data-stu-id="baeab-109">This resource collection represents an aggregated total for each meter for the current billing cycle, across your entire Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baeab-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="baeab-110">Prerequisites</span></span>

- <span data-ttu-id="baeab-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="baeab-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="baeab-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="baeab-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="baeab-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="baeab-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="baeab-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="baeab-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="baeab-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="baeab-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="baeab-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="baeab-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="baeab-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="baeab-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="baeab-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="baeab-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="baeab-119">Egy előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="baeab-119">A subscription ID</span></span>

<span data-ttu-id="baeab-120">*Ez az új útvonal egyenértékű a következővel `subscriptions/{subscription-id}/usagerecords/resources` :, amely továbbra is csak Microsoft Azure (MS-AZR-0145P) előfizetések esetében fog működni.*</span><span class="sxs-lookup"><span data-stu-id="baeab-120">*This new route is equivalent to `subscriptions/{subscription-id}/usagerecords/resources`, which will continue to function only for Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span> <span data-ttu-id="baeab-121">Ez az új útvonal Microsoft Azure (MS-AZR-0145P) előfizetéseket és Azure-csomagokat is támogat.</span><span class="sxs-lookup"><span data-stu-id="baeab-121">This new route will support both Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span> <span data-ttu-id="baeab-122">Ahhoz, hogy ezt az információt megkapja az Azure-csomaghoz, át kell váltania erre az új útvonalra.</span><span class="sxs-lookup"><span data-stu-id="baeab-122">In order to get this information for your Azure plan, you need to switch to this new route.</span></span> <span data-ttu-id="baeab-123">A következő szakaszokban említett tulajdonságok kivételével a válasz megegyezik a régi útvonallal.</span><span class="sxs-lookup"><span data-stu-id="baeab-123">Other than the properties mentioned in the following sections, the response is the same as the old route.</span></span>

## <a name="c"></a><span data-ttu-id="baeab-124">C\#</span><span class="sxs-lookup"><span data-stu-id="baeab-124">C\#</span></span>

<span data-ttu-id="baeab-125">Adott Azure-szolgáltatás vagy-erőforrás díjszabási használati adatainak beolvasása az aktuális számlázási időszakban:</span><span class="sxs-lookup"><span data-stu-id="baeab-125">To get meter usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="baeab-126">A **IAggregatePartner. Customs** gyűjtemény használatával hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="baeab-126">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="baeab-127">Hívja meg az előfizetések tulajdonságot, és a **UsageRecords**, majd a **meters** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="baeab-127">Call the Subscriptions property, and **UsageRecords**, then the **Meters** property.</span></span> <span data-ttu-id="baeab-128">Fejezze be a Get () vagy a GetAsync () metódus meghívásával.</span><span class="sxs-lookup"><span data-stu-id="baeab-128">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

<span data-ttu-id="baeab-129">Példaként tekintse meg a következő mintát:</span><span class="sxs-lookup"><span data-stu-id="baeab-129">For an example, see the following sample:</span></span>

- <span data-ttu-id="baeab-130">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="baeab-130">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="baeab-131">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="baeab-131">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="baeab-132">Osztály: **GetSubscriptionUsageRecordsByMeter.cs**</span><span class="sxs-lookup"><span data-stu-id="baeab-132">Class: **GetSubscriptionUsageRecordsByMeter.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="baeab-133">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="baeab-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="baeab-134">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="baeab-134">Request syntax</span></span>

| <span data-ttu-id="baeab-135">Metódus</span><span class="sxs-lookup"><span data-stu-id="baeab-135">Method</span></span>  | <span data-ttu-id="baeab-136">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="baeab-136">Request URI</span></span>                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="baeab-137">**GET**</span><span class="sxs-lookup"><span data-stu-id="baeab-137">**GET**</span></span> | <span data-ttu-id="baeab-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/meterusagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="baeab-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="baeab-139">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="baeab-139">URI parameters</span></span>

<span data-ttu-id="baeab-140">Ez a táblázat felsorolja a szükséges lekérdezési paramétereket, hogy megkapják az ügyfél névleges használati adatait.</span><span class="sxs-lookup"><span data-stu-id="baeab-140">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="baeab-141">Név</span><span class="sxs-lookup"><span data-stu-id="baeab-141">Name</span></span>                   | <span data-ttu-id="baeab-142">Típus</span><span class="sxs-lookup"><span data-stu-id="baeab-142">Type</span></span>     | <span data-ttu-id="baeab-143">Kötelező</span><span class="sxs-lookup"><span data-stu-id="baeab-143">Required</span></span> | <span data-ttu-id="baeab-144">Leírás</span><span class="sxs-lookup"><span data-stu-id="baeab-144">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="baeab-145">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="baeab-145">**customer-tenant-id**</span></span> | <span data-ttu-id="baeab-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="baeab-146">**guid**</span></span> | <span data-ttu-id="baeab-147">Y</span><span class="sxs-lookup"><span data-stu-id="baeab-147">Y</span></span>        | <span data-ttu-id="baeab-148">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="baeab-148">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="baeab-149">**előfizetés-azonosító**</span><span class="sxs-lookup"><span data-stu-id="baeab-149">**subscription-id**</span></span>    | <span data-ttu-id="baeab-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="baeab-150">**guid**</span></span> | <span data-ttu-id="baeab-151">Y</span><span class="sxs-lookup"><span data-stu-id="baeab-151">Y</span></span>        | <span data-ttu-id="baeab-152">A partner Center [előfizetési erőforrás](subscription-resources.md#subscription)azonosítójának megfelelő GUID, amely egy Microsoft Azure (MS-AZR-0145P) előfizetést vagy egy Azure-csomagot jelöl.</span><span class="sxs-lookup"><span data-stu-id="baeab-152">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="baeab-153">*Az Azure-csomag előfizetési erőforrásai esetében adja meg az **előfizetési azonosítóként** szolgáló **díjcsomag azonosítóját** ebben az útvonalban.*</span><span class="sxs-lookup"><span data-stu-id="baeab-153">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="baeab-154">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="baeab-154">Request headers</span></span>

<span data-ttu-id="baeab-155">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="baeab-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="baeab-156">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="baeab-156">Request body</span></span>

<span data-ttu-id="baeab-157">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="baeab-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="baeab-158">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="baeab-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="baeab-159">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="baeab-159">REST response</span></span>

<span data-ttu-id="baeab-160">Ha ez sikeres, ez a metódus **egy \<MeterUsageRecord> PagedResourceCollection** -erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="baeab-160">If successful, this method returns a **PagedResourceCollection\<MeterUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="baeab-161">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="baeab-161">Response success and error codes</span></span>

<span data-ttu-id="baeab-162">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="baeab-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="baeab-163">A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="baeab-163">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="baeab-164">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="baeab-164">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="baeab-165">Válasz példa Microsoft Azure (MS-AZR-0145P) előfizetésekre</span><span class="sxs-lookup"><span data-stu-id="baeab-165">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="baeab-166">Ebben a példában az ügyfél megvásárolta az **Azure TB 145P**.</span><span class="sxs-lookup"><span data-stu-id="baeab-166">In this example, the customer purchased **145P Azure PayG**.</span></span>

<span data-ttu-id="baeab-167">*Microsoft Azure (MS-AZR-0145P) előfizetéssel rendelkező ügyfelek esetében nem változik az API-válasz.*</span><span class="sxs-lookup"><span data-stu-id="baeab-167">*For customers with a Microsoft Azure (MS-AZR-0145P) subscription, there will be no change to API response.*</span></span>

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

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="baeab-168">REST-válaszok – példa az Azure-csomagra</span><span class="sxs-lookup"><span data-stu-id="baeab-168">REST response example for Azure plan</span></span>

<span data-ttu-id="baeab-169">Ebben a példában az ügyfél egy Azure-csomagot vásárolt.</span><span class="sxs-lookup"><span data-stu-id="baeab-169">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="baeab-170">*Az Azure-csomaggal rendelkező ügyfelek esetében az API-válasz módosításai a következők:*</span><span class="sxs-lookup"><span data-stu-id="baeab-170">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="baeab-171">a **currencyLocale** helyére a **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="baeab-171">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="baeab-172">a **usdTotalCost** egy új mező</span><span class="sxs-lookup"><span data-stu-id="baeab-172">**usdTotalCost** is a new field</span></span>

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
