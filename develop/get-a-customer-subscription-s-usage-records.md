---
title: Egy ügyfél összes előfizetés-használati rekordjának lekérése
description: A SubscriptionMonthlyUsageRecord erőforrás-gyűjtemény használatával lekérheti az előfizetés-használati rekordokat egy adott Azure-szolgáltatás vagy-erőforrás felhasználója számára az aktuális számlázási időszak alatt.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 765ea16ff58b462d83ae3b8764b8b34c3ef804dc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767971"
---
# <a name="get-subscription-usage-records-for-a-customer"></a><span data-ttu-id="61a0c-103">Előfizetés-használati rekordok beolvasása az ügyfelek számára</span><span class="sxs-lookup"><span data-stu-id="61a0c-103">Get subscription usage records for a customer</span></span>

<span data-ttu-id="61a0c-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="61a0c-104">**Applies to:**</span></span>

- <span data-ttu-id="61a0c-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="61a0c-105">Partner Center</span></span>
- <span data-ttu-id="61a0c-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="61a0c-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="61a0c-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="61a0c-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="61a0c-108">A **SubscriptionMonthlyUsageRecord** erőforrás-gyűjtemény használatával lekérheti az előfizetés-használati rekordokat egy adott Azure-szolgáltatás vagy-erőforrás felhasználója számára az aktuális számlázási időszak alatt.</span><span class="sxs-lookup"><span data-stu-id="61a0c-108">You can use the **SubscriptionMonthlyUsageRecord** resource collection to get subscription usage records for a customer of a specific Azure service or resource during the current billing period.</span></span> <span data-ttu-id="61a0c-109">Ez az erőforrás az ügyfél összes előfizetését képviseli.</span><span class="sxs-lookup"><span data-stu-id="61a0c-109">This resource represents all subscriptions for the customer.</span></span> <span data-ttu-id="61a0c-110">Az Azure-csomaggal rendelkező ügyfelek esetében ez az erőforrás visszaadja a csomagok listáját (nem az egyes Azure-előfizetéseket).</span><span class="sxs-lookup"><span data-stu-id="61a0c-110">For a customer with an Azure plan, this resource returns a list of those plans (not individual Azure subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61a0c-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="61a0c-111">Prerequisites</span></span>

- <span data-ttu-id="61a0c-112">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="61a0c-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="61a0c-113">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="61a0c-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="61a0c-114">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="61a0c-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="61a0c-115">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="61a0c-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="61a0c-116">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="61a0c-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="61a0c-117">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="61a0c-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="61a0c-118">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="61a0c-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="61a0c-119">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="61a0c-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="61a0c-120">C\#</span><span class="sxs-lookup"><span data-stu-id="61a0c-120">C\#</span></span>

<span data-ttu-id="61a0c-121">Egy adott Azure-szolgáltatás vagy-erőforrás ügyfelének előfizetés-használati rekordjainak lekérése az aktuális számlázási időszak alatt:</span><span class="sxs-lookup"><span data-stu-id="61a0c-121">To get subscription usage records for a customer of a specific Azure service or resource during the current billing period.:</span></span>

1. <span data-ttu-id="61a0c-122">A **IAggregatePartner. Customs** gyűjtemény használatával hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="61a0c-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="61a0c-123">Ezután hívja meg az **előfizetések** tulajdonságot, valamint a **UsageRecords** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="61a0c-123">Then call the **Subscriptions** property, as well as **UsageRecords** property.</span></span> <span data-ttu-id="61a0c-124">Fejezze be a Get () vagy a GetAsync () metódus meghívásával.</span><span class="sxs-lookup"><span data-stu-id="61a0c-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

<span data-ttu-id="61a0c-125">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="61a0c-125">For an example, see the following:</span></span>

- <span data-ttu-id="61a0c-126">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="61a0c-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="61a0c-127">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="61a0c-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="61a0c-128">Osztály: **GetSubscriptionUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="61a0c-128">Class: **GetSubscriptionUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="61a0c-129">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="61a0c-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="61a0c-130">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="61a0c-130">Request syntax</span></span>

| <span data-ttu-id="61a0c-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="61a0c-131">Method</span></span>  | <span data-ttu-id="61a0c-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="61a0c-132">Request URI</span></span>                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="61a0c-133">**GET**</span><span class="sxs-lookup"><span data-stu-id="61a0c-133">**GET**</span></span> | <span data-ttu-id="61a0c-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/usagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="61a0c-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="61a0c-135">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="61a0c-135">URI parameter</span></span>

<span data-ttu-id="61a0c-136">Ez a táblázat felsorolja a szükséges lekérdezési paramétert, hogy lekérje az ügyfél névleges használati adatait.</span><span class="sxs-lookup"><span data-stu-id="61a0c-136">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="61a0c-137">Név</span><span class="sxs-lookup"><span data-stu-id="61a0c-137">Name</span></span>                   | <span data-ttu-id="61a0c-138">Típus</span><span class="sxs-lookup"><span data-stu-id="61a0c-138">Type</span></span>     | <span data-ttu-id="61a0c-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="61a0c-139">Required</span></span> | <span data-ttu-id="61a0c-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="61a0c-140">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="61a0c-141">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="61a0c-141">**customer-tenant-id**</span></span> | <span data-ttu-id="61a0c-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="61a0c-142">**guid**</span></span> | <span data-ttu-id="61a0c-143">Y</span><span class="sxs-lookup"><span data-stu-id="61a0c-143">Y</span></span>        | <span data-ttu-id="61a0c-144">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="61a0c-144">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="61a0c-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="61a0c-145">Request headers</span></span>

<span data-ttu-id="61a0c-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="61a0c-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="61a0c-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="61a0c-147">Request body</span></span>

<span data-ttu-id="61a0c-148">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="61a0c-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="61a0c-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="61a0c-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="61a0c-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="61a0c-150">REST response</span></span>

<span data-ttu-id="61a0c-151">Ha ez sikeres, ez a metódus egy **SubscriptionMonthlyUsageRecord** -erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="61a0c-151">If successful, this method returns a **SubscriptionMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="61a0c-152">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="61a0c-152">Response success and error codes</span></span>

<span data-ttu-id="61a0c-153">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="61a0c-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="61a0c-154">A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="61a0c-154">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="61a0c-155">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="61a0c-155">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="61a0c-156">Válasz példa Microsoft Azure (MS-AZR-0145P) előfizetésekre</span><span class="sxs-lookup"><span data-stu-id="61a0c-156">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="61a0c-157">Ebben a példában az ügyfél egy **145P Azure TB** -ajánlatot vásárolt.</span><span class="sxs-lookup"><span data-stu-id="61a0c-157">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="61a0c-158">*Microsoft Azure (MS-AZR-0145P) előfizetéssel rendelkező ügyfelek esetében nem változik az API-válasz.*</span><span class="sxs-lookup"><span data-stu-id="61a0c-158">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="61a0c-159">REST-válaszok – példa az Azure-csomagra</span><span class="sxs-lookup"><span data-stu-id="61a0c-159">REST response example for Azure plan</span></span>

<span data-ttu-id="61a0c-160">Ebben a példában az ügyfél egy Azure-csomagot vásárolt.</span><span class="sxs-lookup"><span data-stu-id="61a0c-160">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="61a0c-161">*Az Azure-csomaggal rendelkező ügyfelek esetében az API-válasz módosításai a következők:*</span><span class="sxs-lookup"><span data-stu-id="61a0c-161">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="61a0c-162">a **currencyLocale** helyére a **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="61a0c-162">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="61a0c-163">a **usdTotalCost** egy új mező</span><span class="sxs-lookup"><span data-stu-id="61a0c-163">**usdTotalCost** is a new field</span></span>

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
