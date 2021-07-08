---
title: Előfizetés használati adatainak lekérése erőforrás szerint
description: A ResourceUsageRecord erőforrás használatával lekérte egy ügyfél erőforrás-használati rekordjait adott Azure-szolgáltatásokra vagy -erőforrásokra vonatkozóan az aktuális számlázási időszakban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 50edb9de1d09363b242c080a76c683732f05a5de
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874839"
---
# <a name="get-usage-data-for-subscription-by-resource"></a><span data-ttu-id="4534a-103">Előfizetés használati adatainak lekérése erőforrás szerint</span><span class="sxs-lookup"><span data-stu-id="4534a-103">Get usage data for subscription by resource</span></span>

<span data-ttu-id="4534a-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4534a-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4534a-105">Ez a cikk a **ResourceUsageRecord erőforrás leépítését** ismerteti.</span><span class="sxs-lookup"><span data-stu-id="4534a-105">This article describes how to get the **ResourceUsageRecord** resource.</span></span> <span data-ttu-id="4534a-106">Ez az erőforrás az Azure-csomagban kiépített egyes erőforrások havi összesített összegeként szolgál.</span><span class="sxs-lookup"><span data-stu-id="4534a-106">This resource represents an aggregated total for the month for individual resources provisioned in your Azure plan.</span></span> <span data-ttu-id="4534a-107">Ezzel az erőforrással lekérte az ügyfél erőforrás-használati rekordjait adott Azure-szolgáltatásokhoz vagy -erőforrásokhoz az aktuális számlázási időszakban.</span><span class="sxs-lookup"><span data-stu-id="4534a-107">You can use this resource to get a customer's resource usage records for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="4534a-108">Ez az API olyan adatokat ad vissza, amelyek korábban nem voltak elérhetők az Azure-beli költési API-kon keresztül.</span><span class="sxs-lookup"><span data-stu-id="4534a-108">This API returns data that was not available previously through Azure spending APIs.</span></span>

<span data-ttu-id="4534a-109">*Ez az útvonal nem támogatja Microsoft Azure (MS-AZR-0145P) előfizetéseket.*</span><span class="sxs-lookup"><span data-stu-id="4534a-109">*This route does not support Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4534a-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4534a-110">Prerequisites</span></span>

- <span data-ttu-id="4534a-111">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4534a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4534a-112">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="4534a-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4534a-113">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4534a-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4534a-114">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="4534a-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4534a-115">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4534a-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4534a-116">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4534a-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4534a-117">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="4534a-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4534a-118">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4534a-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4534a-119">Egy előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="4534a-119">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="4534a-120">C\#</span><span class="sxs-lookup"><span data-stu-id="4534a-120">C\#</span></span>

<span data-ttu-id="4534a-121">Egy adott Azure-szolgáltatás vagy -erőforrás erőforrás-használati rekordjainak lekért adatai az aktuális számlázási időszakban:</span><span class="sxs-lookup"><span data-stu-id="4534a-121">To get resource usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="4534a-122">Az **IAggregatePartner.Customers gyűjtemény** használatával hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="4534a-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="4534a-123">Hívja meg a Subscriptions (Előfizetések) és **a UsageRecords**(Használati adatok) tulajdonságot, majd a **Resources (Erőforrások)** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="4534a-123">Call the Subscriptions property and **UsageRecords**, and then the **Resources** property.</span></span> <span data-ttu-id="4534a-124">Befejezésként hívja meg a Get() vagy a GetAsync() metódust.</span><span class="sxs-lookup"><span data-stu-id="4534a-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

<span data-ttu-id="4534a-125">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="4534a-125">For an example, see the following:</span></span>

- <span data-ttu-id="4534a-126">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="4534a-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="4534a-127">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="4534a-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="4534a-128">Osztály: **GetSubscriptionUsageRecordsByResource.cs**</span><span class="sxs-lookup"><span data-stu-id="4534a-128">Class: **GetSubscriptionUsageRecordsByResource.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="4534a-129">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="4534a-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4534a-130">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4534a-130">Request syntax</span></span>

| <span data-ttu-id="4534a-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="4534a-131">Method</span></span>  | <span data-ttu-id="4534a-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4534a-132">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4534a-133">**Kap**</span><span class="sxs-lookup"><span data-stu-id="4534a-133">**GET**</span></span> | <span data-ttu-id="4534a-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/resourceusagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4534a-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="4534a-135">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="4534a-135">URI parameters</span></span>

<span data-ttu-id="4534a-136">Ez a táblázat felsorolja az ügyfél minősített használati információinak lekérdezhető lekérdezési paramétereit.</span><span class="sxs-lookup"><span data-stu-id="4534a-136">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="4534a-137">Név</span><span class="sxs-lookup"><span data-stu-id="4534a-137">Name</span></span>                   | <span data-ttu-id="4534a-138">Típus</span><span class="sxs-lookup"><span data-stu-id="4534a-138">Type</span></span>     | <span data-ttu-id="4534a-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="4534a-139">Required</span></span> | <span data-ttu-id="4534a-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="4534a-140">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="4534a-141">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="4534a-141">**customer-tenant-id**</span></span> | <span data-ttu-id="4534a-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="4534a-142">**guid**</span></span> | <span data-ttu-id="4534a-143">Y</span><span class="sxs-lookup"><span data-stu-id="4534a-143">Y</span></span>        | <span data-ttu-id="4534a-144">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="4534a-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="4534a-145">**subscription-id (előfizetés-azonosító)**</span><span class="sxs-lookup"><span data-stu-id="4534a-145">**subscription-id**</span></span>    | <span data-ttu-id="4534a-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="4534a-146">**guid**</span></span> | <span data-ttu-id="4534a-147">Y</span><span class="sxs-lookup"><span data-stu-id="4534a-147">Y</span></span>        | <span data-ttu-id="4534a-148">Egy Partnerközpont-előfizetési erőforrás azonosítójának megfelelő [](subscription-resources.md#subscription)GUID, amely egy Microsoft Azure-előfizetést (MS-AZR-0145P) vagy egy Azure-csomagot jelent.</span><span class="sxs-lookup"><span data-stu-id="4534a-148">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="4534a-149">*Az Azure-csomag előfizetési  erőforrásaihoz ebben az útvonalban adja meg a csomagazonosítót **előfizetés-azonosítóként.***</span><span class="sxs-lookup"><span data-stu-id="4534a-149">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4534a-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4534a-150">Request headers</span></span>

<span data-ttu-id="4534a-151">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4534a-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4534a-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="4534a-152">Request body</span></span>

<span data-ttu-id="4534a-153">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="4534a-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4534a-154">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4534a-154">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="4534a-155">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4534a-155">REST response</span></span>

<span data-ttu-id="4534a-156">Ha sikeres, ez a metódus egy **PagedResourceCollection \<ResourceUsageRecord>** erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="4534a-156">If successful, this method returns a **PagedResourceCollection\<ResourceUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4534a-157">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4534a-157">Response success and error codes</span></span>

<span data-ttu-id="4534a-158">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="4534a-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4534a-159">Ezt a kódot, a hibatípust és a további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="4534a-159">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="4534a-160">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="4534a-160">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4534a-161">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4534a-161">Response example</span></span>

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
