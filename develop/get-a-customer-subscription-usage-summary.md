---
title: Az ügyfél előfizetésének használati összegzése
description: A SubscriptionUsageSummary erőforrással lekértheti egy adott Azure-szolgáltatás vagy -erőforrás előfizetés-használati összegzését az aktuális számlázási időszakban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 362e72e1b54a62a114564d4dc48a082bcdeea012
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874669"
---
# <a name="get-usage-summary-for-customers-subscription"></a><span data-ttu-id="81f0f-103">Az ügyfél előfizetésének használati összegzése</span><span class="sxs-lookup"><span data-stu-id="81f0f-103">Get usage summary for customer's subscription</span></span>

<span data-ttu-id="81f0f-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="81f0f-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="81f0f-105">A **SubscriptionUsageSummary** erőforrással lekért egy előfizetés használati összefoglalását egy ügyfélhez.</span><span class="sxs-lookup"><span data-stu-id="81f0f-105">You can use the **SubscriptionUsageSummary** resource to get a subscription usage summary for a customer.</span></span> <span data-ttu-id="81f0f-106">Ez az erőforrás egy adott Azure-szolgáltatás vagy -erőforrás előfizetés-használati összegzését jelöli az aktuális számlázási időszakban.</span><span class="sxs-lookup"><span data-stu-id="81f0f-106">This resource represents the subscription usage summary of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81f0f-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="81f0f-107">Prerequisites</span></span>

- <span data-ttu-id="81f0f-108">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="81f0f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="81f0f-109">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="81f0f-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="81f0f-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="81f0f-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="81f0f-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="81f0f-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="81f0f-112">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="81f0f-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="81f0f-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="81f0f-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="81f0f-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="81f0f-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="81f0f-115">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="81f0f-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="81f0f-116">Előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="81f0f-116">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="81f0f-117">C\#</span><span class="sxs-lookup"><span data-stu-id="81f0f-117">C\#</span></span>

<span data-ttu-id="81f0f-118">Az ügyfél előfizetésének előfizetés-használati összegzése:</span><span class="sxs-lookup"><span data-stu-id="81f0f-118">To get a subscription usage summary for a customer's subscription:</span></span>

1. <span data-ttu-id="81f0f-119">Az **IAggregatePartner.Customers gyűjtemény** használatával hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="81f0f-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="81f0f-120">Ezután hívja meg a Subscriptions tulajdonságot és **a UsageSummary tulajdonságot.**</span><span class="sxs-lookup"><span data-stu-id="81f0f-120">Then call the Subscriptions property and the **UsageSummary** property.</span></span> <span data-ttu-id="81f0f-121">Befejezésként hívja meg a Get() vagy a GetAsync() metódust.</span><span class="sxs-lookup"><span data-stu-id="81f0f-121">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

<span data-ttu-id="81f0f-122">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="81f0f-122">For an example, see the following:</span></span>

- <span data-ttu-id="81f0f-123">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="81f0f-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="81f0f-124">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="81f0f-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="81f0f-125">Osztály: **GetSubscriptionUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="81f0f-125">Class: **GetSubscriptionUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="81f0f-126">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="81f0f-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="81f0f-127">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="81f0f-127">Request syntax</span></span>

| <span data-ttu-id="81f0f-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="81f0f-128">Method</span></span>  | <span data-ttu-id="81f0f-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="81f0f-129">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="81f0f-130">**Kap**</span><span class="sxs-lookup"><span data-stu-id="81f0f-130">**GET**</span></span> | <span data-ttu-id="81f0f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="81f0f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="81f0f-132">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="81f0f-132">URI parameters</span></span>

<span data-ttu-id="81f0f-133">Ez a táblázat felsorolja az ügyfél minősített használati információinak lekérdezhető lekérdezési paramétereit.</span><span class="sxs-lookup"><span data-stu-id="81f0f-133">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="81f0f-134">Név</span><span class="sxs-lookup"><span data-stu-id="81f0f-134">Name</span></span>                   | <span data-ttu-id="81f0f-135">Típus</span><span class="sxs-lookup"><span data-stu-id="81f0f-135">Type</span></span>     | <span data-ttu-id="81f0f-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="81f0f-136">Required</span></span> | <span data-ttu-id="81f0f-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="81f0f-137">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="81f0f-138">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="81f0f-138">**customer-tenant-id**</span></span> | <span data-ttu-id="81f0f-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="81f0f-139">**guid**</span></span> | <span data-ttu-id="81f0f-140">Y</span><span class="sxs-lookup"><span data-stu-id="81f0f-140">Y</span></span>        | <span data-ttu-id="81f0f-141">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="81f0f-141">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="81f0f-142">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="81f0f-142">**subscription-id**</span></span>    | <span data-ttu-id="81f0f-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="81f0f-143">**guid**</span></span> | <span data-ttu-id="81f0f-144">Y</span><span class="sxs-lookup"><span data-stu-id="81f0f-144">Y</span></span>        | <span data-ttu-id="81f0f-145">Egy előfizetés azonosítójának megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="81f0f-145">A GUID corresponding to the identifier of a subscription.</span></span> <span data-ttu-id="81f0f-146">Azure-csomag esetén ez az azure-Partnerközpont előfizetési [](subscription-resources.md#subscription)erőforrás azonosítója.</span><span class="sxs-lookup"><span data-stu-id="81f0f-146">For an Azure plan, this is the identifier of the corresponding Partner Center [subscription resource](subscription-resources.md#subscription), which represents the Azure plan.</span></span> <span data-ttu-id="81f0f-147">*Az Azure-csomag előfizetési erőforrásaihoz adja meg a **csomagazonosítót** **előfizetés-azonosítóként** ebben az útvonalban.*</span><span class="sxs-lookup"><span data-stu-id="81f0f-147">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="81f0f-148">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="81f0f-148">Request headers</span></span>

<span data-ttu-id="81f0f-149">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="81f0f-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="81f0f-150">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="81f0f-150">Request body</span></span>

<span data-ttu-id="81f0f-151">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="81f0f-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="81f0f-152">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="81f0f-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="81f0f-153">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="81f0f-153">REST response</span></span>

<span data-ttu-id="81f0f-154">Ha sikeres, ez a metódus egy **SubscriptionUsageSummary** erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="81f0f-154">If successful, this method returns a **SubscriptionUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="81f0f-155">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="81f0f-155">Response success and error codes</span></span>

<span data-ttu-id="81f0f-156">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="81f0f-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="81f0f-157">Egy hálózati nyomkövetési eszközzel olvassa be ezt a kódot, a hiba típusát és a további paramétereket.</span><span class="sxs-lookup"><span data-stu-id="81f0f-157">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="81f0f-158">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="81f0f-158">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="81f0f-159">Példa válasz Microsoft Azure (MS-AZR-0145P) előfizetésre</span><span class="sxs-lookup"><span data-stu-id="81f0f-159">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="81f0f-160">Ebben a példában az ügyfél megvásárolt egy **145P Azure PayG-ajánlatot.**</span><span class="sxs-lookup"><span data-stu-id="81f0f-160">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="81f0f-161">*A Microsoft Azure (MS-AZR-0145P) előfizetéssel nem változik az API-válasz.*</span><span class="sxs-lookup"><span data-stu-id="81f0f-161">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "id": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "resourceName": "Microsoft Azure",
    "name": "Microsoft Azure",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="81f0f-162">PÉLDA REST-válaszra az Azure-csomaghoz</span><span class="sxs-lookup"><span data-stu-id="81f0f-162">REST response example for Azure plan</span></span>

<span data-ttu-id="81f0f-163">Ebben a példában az ügyfél megvásárolt egy Azure-csomag.</span><span class="sxs-lookup"><span data-stu-id="81f0f-163">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="81f0f-164">*Az Azure-csomaggal használó ügyfelek esetében a következő API-válaszváltozások hatnak:*</span><span class="sxs-lookup"><span data-stu-id="81f0f-164">*For customers with Azure plans, there are the following API response changes:*</span></span>

- <span data-ttu-id="81f0f-165">**A currencyLocale** helyett **a currencyCode található**</span><span class="sxs-lookup"><span data-stu-id="81f0f-165">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="81f0f-166">**Az usdTotalCost** egy új mező</span><span class="sxs-lookup"><span data-stu-id="81f0f-166">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac1
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "11111111-dca5-6f31-d3a6-dbbfad9be0fc",
    "resourceName": "Azure plan",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```
