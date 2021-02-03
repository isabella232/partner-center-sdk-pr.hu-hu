---
title: Az ügyfél előfizetésének használati összegzésének beolvasása
description: A SubscriptionUsageSummary-erőforrás segítségével lekérheti az adott Azure-szolgáltatás vagy-erőforrás előfizetés-használati összegzését az aktuális számlázási időszak alatt.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30334b6f08829eccf0693b566c11f94cb3ece976
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767967"
---
# <a name="get-usage-summary-for-customers-subscription"></a><span data-ttu-id="0897e-103">Az ügyfél előfizetésének használati összegzésének beolvasása</span><span class="sxs-lookup"><span data-stu-id="0897e-103">Get usage summary for customer's subscription</span></span>

<span data-ttu-id="0897e-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="0897e-104">**Applies to:**</span></span>

- <span data-ttu-id="0897e-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="0897e-105">Partner Center</span></span>
- <span data-ttu-id="0897e-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="0897e-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0897e-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="0897e-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0897e-108">A **SubscriptionUsageSummary** erőforrás segítségével lekérheti az ügyfél előfizetésének használati összegzését.</span><span class="sxs-lookup"><span data-stu-id="0897e-108">You can use the **SubscriptionUsageSummary** resource to get a subscription usage summary for a customer.</span></span> <span data-ttu-id="0897e-109">Ez az erőforrás az adott Azure-szolgáltatás vagy-erőforrás előfizetés-használati összegzését jelenti az aktuális számlázási időszakban.</span><span class="sxs-lookup"><span data-stu-id="0897e-109">This resource represents the subscription usage summary of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0897e-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="0897e-110">Prerequisites</span></span>

- <span data-ttu-id="0897e-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="0897e-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0897e-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="0897e-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0897e-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0897e-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0897e-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="0897e-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0897e-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="0897e-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0897e-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="0897e-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0897e-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="0897e-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0897e-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0897e-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0897e-119">Egy előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="0897e-119">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="0897e-120">C\#</span><span class="sxs-lookup"><span data-stu-id="0897e-120">C\#</span></span>

<span data-ttu-id="0897e-121">Előfizetés-használati összefoglalás beszerzése az ügyfél előfizetéséhez:</span><span class="sxs-lookup"><span data-stu-id="0897e-121">To get a subscription usage summary for a customer's subscription:</span></span>

1. <span data-ttu-id="0897e-122">A **IAggregatePartner. Customs** gyűjtemény használatával hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="0897e-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="0897e-123">Ezután hívja meg az előfizetések tulajdonságot, valamint a **UsageSummary** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="0897e-123">Then call the Subscriptions property, as well as **UsageSummary** property.</span></span> <span data-ttu-id="0897e-124">Fejezze be a Get () vagy a GetAsync () metódus meghívásával.</span><span class="sxs-lookup"><span data-stu-id="0897e-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

<span data-ttu-id="0897e-125">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="0897e-125">For an example, see the following:</span></span>

- <span data-ttu-id="0897e-126">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="0897e-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="0897e-127">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="0897e-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="0897e-128">Osztály: **GetSubscriptionUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="0897e-128">Class: **GetSubscriptionUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="0897e-129">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="0897e-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0897e-130">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="0897e-130">Request syntax</span></span>

| <span data-ttu-id="0897e-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="0897e-131">Method</span></span>  | <span data-ttu-id="0897e-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="0897e-132">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0897e-133">**GET**</span><span class="sxs-lookup"><span data-stu-id="0897e-133">**GET**</span></span> | <span data-ttu-id="0897e-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="0897e-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="0897e-135">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="0897e-135">URI parameters</span></span>

<span data-ttu-id="0897e-136">Ez a táblázat felsorolja a szükséges lekérdezési paramétereket, hogy megkapják az ügyfél névleges használati adatait.</span><span class="sxs-lookup"><span data-stu-id="0897e-136">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="0897e-137">Név</span><span class="sxs-lookup"><span data-stu-id="0897e-137">Name</span></span>                   | <span data-ttu-id="0897e-138">Típus</span><span class="sxs-lookup"><span data-stu-id="0897e-138">Type</span></span>     | <span data-ttu-id="0897e-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="0897e-139">Required</span></span> | <span data-ttu-id="0897e-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="0897e-140">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="0897e-141">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="0897e-141">**customer-tenant-id**</span></span> | <span data-ttu-id="0897e-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="0897e-142">**guid**</span></span> | <span data-ttu-id="0897e-143">Y</span><span class="sxs-lookup"><span data-stu-id="0897e-143">Y</span></span>        | <span data-ttu-id="0897e-144">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="0897e-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="0897e-145">**előfizetés-azonosító**</span><span class="sxs-lookup"><span data-stu-id="0897e-145">**subscription-id**</span></span>    | <span data-ttu-id="0897e-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="0897e-146">**guid**</span></span> | <span data-ttu-id="0897e-147">Y</span><span class="sxs-lookup"><span data-stu-id="0897e-147">Y</span></span>        | <span data-ttu-id="0897e-148">Egy előfizetés azonosítójának megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="0897e-148">A GUID corresponding to the identifier of a subscription.</span></span> <span data-ttu-id="0897e-149">Az Azure-csomag esetében ez az az Azure-csomagot jelképező, megfelelő partner Center- [előfizetési erőforrás](subscription-resources.md#subscription)azonosítója.</span><span class="sxs-lookup"><span data-stu-id="0897e-149">For an Azure plan, this is the identifier of the corresponding Partner Center [subscription resource](subscription-resources.md#subscription), which represents the Azure plan.</span></span> <span data-ttu-id="0897e-150">*Az Azure-csomag előfizetési erőforrásai esetében adja meg az **előfizetési azonosítóként** szolgáló **díjcsomag azonosítóját** ebben az útvonalban.*</span><span class="sxs-lookup"><span data-stu-id="0897e-150">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0897e-151">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="0897e-151">Request headers</span></span>

<span data-ttu-id="0897e-152">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0897e-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0897e-153">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="0897e-153">Request body</span></span>

<span data-ttu-id="0897e-154">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="0897e-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0897e-155">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="0897e-155">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="0897e-156">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="0897e-156">REST response</span></span>

<span data-ttu-id="0897e-157">Ha ez sikeres, ez a metódus egy **SubscriptionUsageSummary** -erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="0897e-157">If successful, this method returns a **SubscriptionUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0897e-158">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="0897e-158">Response success and error codes</span></span>

<span data-ttu-id="0897e-159">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="0897e-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0897e-160">A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="0897e-160">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="0897e-161">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0897e-161">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="0897e-162">Válasz példa Microsoft Azure (MS-AZR-0145P) előfizetésekre</span><span class="sxs-lookup"><span data-stu-id="0897e-162">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="0897e-163">Ebben a példában az ügyfél egy **145P Azure TB** -ajánlatot vásárolt.</span><span class="sxs-lookup"><span data-stu-id="0897e-163">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="0897e-164">*Microsoft Azure (MS-AZR-0145P) előfizetéssel rendelkező ügyfelek esetében nem változik az API-válasz.*</span><span class="sxs-lookup"><span data-stu-id="0897e-164">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="0897e-165">REST-válaszok – példa az Azure-csomagra</span><span class="sxs-lookup"><span data-stu-id="0897e-165">REST response example for Azure plan</span></span>

<span data-ttu-id="0897e-166">Ebben a példában az ügyfél egy Azure-csomagot vásárolt.</span><span class="sxs-lookup"><span data-stu-id="0897e-166">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="0897e-167">*Az Azure-csomagokkal rendelkező ügyfelek esetében az alábbi API-válaszok változnak:*</span><span class="sxs-lookup"><span data-stu-id="0897e-167">*For customers with Azure plans, there are the following API response changes:*</span></span>

- <span data-ttu-id="0897e-168">a **currencyLocale** helyére a **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="0897e-168">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="0897e-169">a **usdTotalCost** egy új mező</span><span class="sxs-lookup"><span data-stu-id="0897e-169">**usdTotalCost** is a new field</span></span>

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
