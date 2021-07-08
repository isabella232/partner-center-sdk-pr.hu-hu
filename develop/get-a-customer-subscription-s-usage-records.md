---
title: Egy ügyfél összes előfizetés-használati rekordjának lekérése
description: A SubscriptionMonthlyUsageRecord erőforrás-gyűjtemény használatával lekért előfizetési használati rekordok egy adott Azure-szolgáltatás vagy -erőforrás ügyfele számára az aktuális számlázási időszakban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 976abd86f34c1c27184f277ffc89fbc65f16bb37
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874686"
---
# <a name="get-subscription-usage-records-for-a-customer"></a><span data-ttu-id="0bce0-103">Ügyfél előfizetés-használati rekordjainak lekért száma</span><span class="sxs-lookup"><span data-stu-id="0bce0-103">Get subscription usage records for a customer</span></span>

<span data-ttu-id="0bce0-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0bce0-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0bce0-105">A **SubscriptionMonthlyUsageRecord** erőforrás-gyűjtemény használatával lekért előfizetési használati rekordok egy adott Azure-szolgáltatás vagy -erőforrás ügyfele számára az aktuális számlázási időszakban.</span><span class="sxs-lookup"><span data-stu-id="0bce0-105">You can use the **SubscriptionMonthlyUsageRecord** resource collection to get subscription usage records for a customer of a specific Azure service or resource during the current billing period.</span></span> <span data-ttu-id="0bce0-106">Ez az erőforrás az ügyfél összes előfizetését képviseli.</span><span class="sxs-lookup"><span data-stu-id="0bce0-106">This resource represents all subscriptions for the customer.</span></span> <span data-ttu-id="0bce0-107">Az Azure-csomaggal rendelkezik ügyfelek számára ez az erőforrás a csomagok listáját adja vissza (nem az egyes Azure-előfizetésekét).</span><span class="sxs-lookup"><span data-stu-id="0bce0-107">For a customer with an Azure plan, this resource returns a list of those plans (not individual Azure subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bce0-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="0bce0-108">Prerequisites</span></span>

- <span data-ttu-id="0bce0-109">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0bce0-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0bce0-110">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="0bce0-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0bce0-111">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0bce0-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0bce0-112">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="0bce0-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0bce0-113">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="0bce0-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0bce0-114">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="0bce0-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0bce0-115">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="0bce0-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0bce0-116">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0bce0-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0bce0-117">C\#</span><span class="sxs-lookup"><span data-stu-id="0bce0-117">C\#</span></span>

<span data-ttu-id="0bce0-118">Ha egy adott Azure-szolgáltatás vagy -erőforrás ügyfele előfizetés-használati rekordjait le kell kapnia az aktuális számlázási időszakban, tegye a következőket:</span><span class="sxs-lookup"><span data-stu-id="0bce0-118">To get subscription usage records for a customer of a specific Azure service or resource during the current billing period, do the following steps:</span></span>

1. <span data-ttu-id="0bce0-119">Az **IAggregatePartner.Customers gyűjtemény** használatával hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="0bce0-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="0bce0-120">Ezután hívja meg **a Subscriptions** tulajdonságot és **a UsageRecords tulajdonságot.**</span><span class="sxs-lookup"><span data-stu-id="0bce0-120">Then call the **Subscriptions** property and the **UsageRecords** property.</span></span> <span data-ttu-id="0bce0-121">Befejezésként hívja meg a Get() vagy a GetAsync() metódust.</span><span class="sxs-lookup"><span data-stu-id="0bce0-121">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

<span data-ttu-id="0bce0-122">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="0bce0-122">For an example, see the following:</span></span>

- <span data-ttu-id="0bce0-123">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="0bce0-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="0bce0-124">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="0bce0-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="0bce0-125">Osztály: **GetSubscriptionUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="0bce0-125">Class: **GetSubscriptionUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="0bce0-126">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="0bce0-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0bce0-127">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="0bce0-127">Request syntax</span></span>

| <span data-ttu-id="0bce0-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="0bce0-128">Method</span></span>  | <span data-ttu-id="0bce0-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="0bce0-129">Request URI</span></span>                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0bce0-130">**Kap**</span><span class="sxs-lookup"><span data-stu-id="0bce0-130">**GET**</span></span> | <span data-ttu-id="0bce0-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0bce0-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="0bce0-132">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="0bce0-132">URI parameter</span></span>

<span data-ttu-id="0bce0-133">Ez a táblázat felsorolja az ügyfél minősített használati információinak lekérdezhető lekérdezési paraméterét.</span><span class="sxs-lookup"><span data-stu-id="0bce0-133">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="0bce0-134">Név</span><span class="sxs-lookup"><span data-stu-id="0bce0-134">Name</span></span>                   | <span data-ttu-id="0bce0-135">Típus</span><span class="sxs-lookup"><span data-stu-id="0bce0-135">Type</span></span>     | <span data-ttu-id="0bce0-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="0bce0-136">Required</span></span> | <span data-ttu-id="0bce0-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="0bce0-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="0bce0-138">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="0bce0-138">**customer-tenant-id**</span></span> | <span data-ttu-id="0bce0-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="0bce0-139">**guid**</span></span> | <span data-ttu-id="0bce0-140">Y</span><span class="sxs-lookup"><span data-stu-id="0bce0-140">Y</span></span>        | <span data-ttu-id="0bce0-141">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="0bce0-141">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0bce0-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="0bce0-142">Request headers</span></span>

<span data-ttu-id="0bce0-143">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0bce0-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0bce0-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="0bce0-144">Request body</span></span>

<span data-ttu-id="0bce0-145">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="0bce0-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0bce0-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="0bce0-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="0bce0-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="0bce0-147">REST response</span></span>

<span data-ttu-id="0bce0-148">Ha sikeres, ez a metódus egy **SubscriptionMonthlyUsageRecord** erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="0bce0-148">If successful, this method returns a **SubscriptionMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0bce0-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="0bce0-149">Response success and error codes</span></span>

<span data-ttu-id="0bce0-150">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="0bce0-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0bce0-151">Ezt a kódot, a hibatípust és a további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="0bce0-151">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="0bce0-152">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0bce0-152">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="0bce0-153">Válasz példa Microsoft Azure (MS-AZR-0145P) előfizetésre</span><span class="sxs-lookup"><span data-stu-id="0bce0-153">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="0bce0-154">Ebben a példában az ügyfél megvásárolt egy **145P-s Azure PayG-ajánlatot.**</span><span class="sxs-lookup"><span data-stu-id="0bce0-154">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="0bce0-155">*A Microsoft Azure (MS-AZR-0145P) előfizetéssel nem lesz változás az API-válaszban.*</span><span class="sxs-lookup"><span data-stu-id="0bce0-155">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="0bce0-156">PÉLDA REST-válaszra az Azure-csomaghoz</span><span class="sxs-lookup"><span data-stu-id="0bce0-156">REST response example for Azure plan</span></span>

<span data-ttu-id="0bce0-157">Ebben a példában az ügyfél megvásárolt egy Azure-csomag.</span><span class="sxs-lookup"><span data-stu-id="0bce0-157">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="0bce0-158">*Az Azure-csomagokat használó ügyfelek esetében az API-válasz a következő változásokat tartalmazza:*</span><span class="sxs-lookup"><span data-stu-id="0bce0-158">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="0bce0-159">**A currencyLocale** helyett **a currencyCode található**</span><span class="sxs-lookup"><span data-stu-id="0bce0-159">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="0bce0-160">**A usdTotalCost** egy új mező</span><span class="sxs-lookup"><span data-stu-id="0bce0-160">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 2,
    "items": [
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-7d58-6654-69fa-0797198155d3",
            "id": "11111111-7d58-6654-69fa-0797198155d3",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        },
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "id": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
