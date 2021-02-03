---
title: Előfizetés használati adatainak lekérése erőforrás szerint
description: A ResourceUsageRecord-erőforrás segítségével lekérheti az ügyfél erőforrás-használati rekordjait az adott Azure-szolgáltatásokhoz vagy-erőforrásokhoz az aktuális számlázási időszak alatt.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e815430730dd7182380e9efd1fea80f9e84d2ce7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767968"
---
# <a name="get-usage-data-for-subscription-by-resource"></a><span data-ttu-id="f5a63-103">Előfizetés használati adatainak lekérése erőforrás szerint</span><span class="sxs-lookup"><span data-stu-id="f5a63-103">Get usage data for subscription by resource</span></span>

<span data-ttu-id="f5a63-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="f5a63-104">**Applies to:**</span></span>

- <span data-ttu-id="f5a63-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f5a63-105">Partner Center</span></span>
- <span data-ttu-id="f5a63-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f5a63-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f5a63-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f5a63-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f5a63-108">Ez a cikk bemutatja, hogyan kérheti le a **ResourceUsageRecord** -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="f5a63-108">This article describes how to get the **ResourceUsageRecord** resource.</span></span> <span data-ttu-id="f5a63-109">Ez az erőforrás az Azure-csomagban kiépített egyes erőforrások havi összesített összegét jelöli.</span><span class="sxs-lookup"><span data-stu-id="f5a63-109">This resource represents an aggregated total for the month for individual resources provisioned in your Azure plan.</span></span> <span data-ttu-id="f5a63-110">Ezt az erőforrást használhatja az adott Azure-szolgáltatásokhoz vagy-erőforrásokhoz tartozó erőforrás-használati rekordok beszerzésére az aktuális számlázási időszakban.</span><span class="sxs-lookup"><span data-stu-id="f5a63-110">You can use this resource to get a customer's resource usage records for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="f5a63-111">Ez az API olyan adatok visszaadása, amelyek korábban nem voltak elérhetők az Azure-kiadások API-kon keresztül.</span><span class="sxs-lookup"><span data-stu-id="f5a63-111">This API returns data that was not available previously through Azure spending APIs.</span></span>

<span data-ttu-id="f5a63-112">*Ez az útvonal nem támogatja Microsoft Azure (MS-AZR-0145P) előfizetést.*</span><span class="sxs-lookup"><span data-stu-id="f5a63-112">*This route does not support Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5a63-113">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f5a63-113">Prerequisites</span></span>

- <span data-ttu-id="f5a63-114">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="f5a63-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f5a63-115">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="f5a63-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f5a63-116">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f5a63-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f5a63-117">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="f5a63-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f5a63-118">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="f5a63-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f5a63-119">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="f5a63-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f5a63-120">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="f5a63-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f5a63-121">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f5a63-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f5a63-122">Egy előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="f5a63-122">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="f5a63-123">C\#</span><span class="sxs-lookup"><span data-stu-id="f5a63-123">C\#</span></span>

<span data-ttu-id="f5a63-124">Egy adott Azure-szolgáltatáshoz vagy-erőforráshoz tartozó ügyfél erőforrás-használati rekordjainak lekérése az aktuális számlázási időszakban:</span><span class="sxs-lookup"><span data-stu-id="f5a63-124">To get resource usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="f5a63-125">A **IAggregatePartner. Customs** gyűjtemény használatával hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="f5a63-125">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="f5a63-126">Hívja meg az előfizetések tulajdonságot, valamint a **UsageRecords**, majd a **Resources (erőforrások** ) tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="f5a63-126">Call the Subscriptions property, as well as **UsageRecords**, then the **Resources** property.</span></span> <span data-ttu-id="f5a63-127">Fejezze be a Get () vagy a GetAsync () metódus meghívásával.</span><span class="sxs-lookup"><span data-stu-id="f5a63-127">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

<span data-ttu-id="f5a63-128">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="f5a63-128">For an example, see the following:</span></span>

- <span data-ttu-id="f5a63-129">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f5a63-129">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="f5a63-130">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="f5a63-130">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="f5a63-131">Osztály: **GetSubscriptionUsageRecordsByResource.cs**</span><span class="sxs-lookup"><span data-stu-id="f5a63-131">Class: **GetSubscriptionUsageRecordsByResource.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="f5a63-132">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="f5a63-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f5a63-133">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f5a63-133">Request syntax</span></span>

| <span data-ttu-id="f5a63-134">Metódus</span><span class="sxs-lookup"><span data-stu-id="f5a63-134">Method</span></span>  | <span data-ttu-id="f5a63-135">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f5a63-135">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f5a63-136">**GET**</span><span class="sxs-lookup"><span data-stu-id="f5a63-136">**GET**</span></span> | <span data-ttu-id="f5a63-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/resourceusagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="f5a63-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="f5a63-138">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="f5a63-138">URI parameters</span></span>

<span data-ttu-id="f5a63-139">Ez a táblázat felsorolja a szükséges lekérdezési paramétereket, hogy megkapják az ügyfél névleges használati adatait.</span><span class="sxs-lookup"><span data-stu-id="f5a63-139">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="f5a63-140">Név</span><span class="sxs-lookup"><span data-stu-id="f5a63-140">Name</span></span>                   | <span data-ttu-id="f5a63-141">Típus</span><span class="sxs-lookup"><span data-stu-id="f5a63-141">Type</span></span>     | <span data-ttu-id="f5a63-142">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f5a63-142">Required</span></span> | <span data-ttu-id="f5a63-143">Leírás</span><span class="sxs-lookup"><span data-stu-id="f5a63-143">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="f5a63-144">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="f5a63-144">**customer-tenant-id**</span></span> | <span data-ttu-id="f5a63-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="f5a63-145">**guid**</span></span> | <span data-ttu-id="f5a63-146">Y</span><span class="sxs-lookup"><span data-stu-id="f5a63-146">Y</span></span>        | <span data-ttu-id="f5a63-147">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="f5a63-147">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="f5a63-148">**előfizetés-azonosító**</span><span class="sxs-lookup"><span data-stu-id="f5a63-148">**subscription-id**</span></span>    | <span data-ttu-id="f5a63-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="f5a63-149">**guid**</span></span> | <span data-ttu-id="f5a63-150">Y</span><span class="sxs-lookup"><span data-stu-id="f5a63-150">Y</span></span>        | <span data-ttu-id="f5a63-151">A partner Center [előfizetési erőforrás](subscription-resources.md#subscription)azonosítójának megfelelő GUID, amely egy Microsoft Azure (MS-AZR-0145P) előfizetést vagy egy Azure-csomagot jelöl.</span><span class="sxs-lookup"><span data-stu-id="f5a63-151">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="f5a63-152">*Az Azure-csomag előfizetési erőforrásai esetében adja meg az **előfizetési azonosítóként** szolgáló **díjcsomag azonosítóját** ebben az útvonalban.*</span><span class="sxs-lookup"><span data-stu-id="f5a63-152">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f5a63-153">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f5a63-153">Request headers</span></span>

<span data-ttu-id="f5a63-154">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f5a63-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f5a63-155">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f5a63-155">Request body</span></span>

<span data-ttu-id="f5a63-156">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="f5a63-156">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f5a63-157">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f5a63-157">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="f5a63-158">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f5a63-158">REST response</span></span>

<span data-ttu-id="f5a63-159">Ha ez sikeres, ez a metódus **egy \<ResourceUsageRecord> PagedResourceCollection** -erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="f5a63-159">If successful, this method returns a **PagedResourceCollection\<ResourceUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f5a63-160">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f5a63-160">Response success and error codes</span></span>

<span data-ttu-id="f5a63-161">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="f5a63-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f5a63-162">A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="f5a63-162">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="f5a63-163">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f5a63-163">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f5a63-164">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f5a63-164">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlement-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
