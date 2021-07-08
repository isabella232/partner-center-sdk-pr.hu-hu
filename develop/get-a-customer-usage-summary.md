---
title: Egy ügyfél összes előfizetésének használati összegzése
description: A CustomerUsageSummary erőforrással lekértheti egy adott Azure-szolgáltatás vagy -erőforrás ügyfélhasználatát az aktuális számlázási időszakban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 88c69637c94b9263ede6924cf2dd09513aa00f70
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874618"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a><span data-ttu-id="02a33-103">Egy ügyfél összes előfizetésének használati összegzése</span><span class="sxs-lookup"><span data-stu-id="02a33-103">Get a usage summary for all of a customer's subscriptions</span></span>

<span data-ttu-id="02a33-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="02a33-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="02a33-105">A **CustomerUsageSummary** erőforrással lekértheti egy adott Azure-szolgáltatás vagy -erőforrás ügyfélhasználatát az aktuális számlázási időszakban.</span><span class="sxs-lookup"><span data-stu-id="02a33-105">You can use the **CustomerUsageSummary** resource to get a customer's usage of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02a33-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="02a33-106">Prerequisites</span></span>

- <span data-ttu-id="02a33-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="02a33-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="02a33-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="02a33-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="02a33-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="02a33-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="02a33-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="02a33-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="02a33-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="02a33-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="02a33-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="02a33-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="02a33-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="02a33-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="02a33-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="02a33-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="02a33-115">C\#</span><span class="sxs-lookup"><span data-stu-id="02a33-115">C\#</span></span>

<span data-ttu-id="02a33-116">Az ügyfél összes előfizetésének használati összegzése:</span><span class="sxs-lookup"><span data-stu-id="02a33-116">To get a usage summary for all of a customer's subscriptions:</span></span>

1. <span data-ttu-id="02a33-117">Az **IAggregatePartner.Customers gyűjtemény** használatával hívja meg a **ById()** metódust.</span><span class="sxs-lookup"><span data-stu-id="02a33-117">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="02a33-118">Hívja meg **a UsageSummary** tulajdonságot, majd a **Get() vagy** **a GetAsync() metódust:**</span><span class="sxs-lookup"><span data-stu-id="02a33-118">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

<span data-ttu-id="02a33-119">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="02a33-119">For an example, see the following:</span></span>

- <span data-ttu-id="02a33-120">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="02a33-120">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="02a33-121">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="02a33-121">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="02a33-122">Osztály: **GetCustomerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="02a33-122">Class: **GetCustomerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="02a33-123">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="02a33-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="02a33-124">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="02a33-124">Request syntax</span></span>

| <span data-ttu-id="02a33-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="02a33-125">Method</span></span>  | <span data-ttu-id="02a33-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="02a33-126">Request URI</span></span>                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="02a33-127">**Kap**</span><span class="sxs-lookup"><span data-stu-id="02a33-127">**GET**</span></span> | <span data-ttu-id="02a33-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="02a33-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="02a33-129">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="02a33-129">URI parameter</span></span>

<span data-ttu-id="02a33-130">Ez a táblázat felsorolja az ügyfél minősített használati információinak lekérdezhető lekérdezési paraméterét.</span><span class="sxs-lookup"><span data-stu-id="02a33-130">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="02a33-131">Név</span><span class="sxs-lookup"><span data-stu-id="02a33-131">Name</span></span>                   | <span data-ttu-id="02a33-132">Típus</span><span class="sxs-lookup"><span data-stu-id="02a33-132">Type</span></span>     | <span data-ttu-id="02a33-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="02a33-133">Required</span></span> | <span data-ttu-id="02a33-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="02a33-134">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="02a33-135">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="02a33-135">**customer-tenant-id**</span></span> | <span data-ttu-id="02a33-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="02a33-136">**guid**</span></span> | <span data-ttu-id="02a33-137">Y</span><span class="sxs-lookup"><span data-stu-id="02a33-137">Y</span></span>        | <span data-ttu-id="02a33-138">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="02a33-138">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="02a33-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="02a33-139">Request headers</span></span>

<span data-ttu-id="02a33-140">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="02a33-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="02a33-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="02a33-141">Request body</span></span>

<span data-ttu-id="02a33-142">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="02a33-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="02a33-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="02a33-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="02a33-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="02a33-144">REST response</span></span>

<span data-ttu-id="02a33-145">Ha sikeres, ez a metódus egy **CustomerUsageSummary** erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="02a33-145">If successful, this method returns a **CustomerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="02a33-146">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="02a33-146">Response success and error codes</span></span>

<span data-ttu-id="02a33-147">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="02a33-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="02a33-148">Egy hálózati nyomkövetési eszközzel olvassa be ezt a kódot, a hiba típusát és a további paramétereket.</span><span class="sxs-lookup"><span data-stu-id="02a33-148">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="02a33-149">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="02a33-149">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="02a33-150">Példa válasz Microsoft Azure (MS-AZR-0145P) előfizetésre</span><span class="sxs-lookup"><span data-stu-id="02a33-150">Response example for Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="02a33-151">Ebben a példában az ügyfél megvásárolt egy **145P Azure PayG-ajánlatot.**</span><span class="sxs-lookup"><span data-stu-id="02a33-151">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="02a33-152">*A Microsoft Azure (MS-AZR-0145P) előfizetéssel nem változik az API-válasz.*</span><span class="sxs-lookup"><span data-stu-id="02a33-152">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget":{
        "ammount":300.000000,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "id":"65726577-C208-40FD-9735-8C85AC9CAC68",
    "name":"600 test",
    "billingStartDate":"2016-02-06T00:00:00-08:00",
    "billingEndDate":"2016-03-05T00:00:00-08:00",
    "totalCost":0.0,
    "currencyLocale":"en-US",
    "lastModifiedDate":"2016-02-26T09:42:54.5130558+00:00",
    "links":{
        "self":{
            "uri":"/customers/{customer-tenant-id}/usagesummary",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"CustomerUsageSummary"
    }
}
```

### <a name="response-example-for-azure-plan"></a><span data-ttu-id="02a33-153">Azure-csomag válasz példája</span><span class="sxs-lookup"><span data-stu-id="02a33-153">Response example for Azure plan</span></span>

<span data-ttu-id="02a33-154">Ebben a példában az ügyfél megvásárolt egy Azure-csomag.</span><span class="sxs-lookup"><span data-stu-id="02a33-154">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="02a33-155">*Az Azure-csomaggal használó ügyfelek esetében az API-válasz a következő változásokat tartalmazza:*</span><span class="sxs-lookup"><span data-stu-id="02a33-155">*For customers with Azure plans, there are the following changes to the API response:*</span></span>

- <span data-ttu-id="02a33-156">**A currencyLocale** helyett **a currencyCode található**</span><span class="sxs-lookup"><span data-stu-id="02a33-156">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="02a33-157">**Az usdTotalCost** egy új mező</span><span class="sxs-lookup"><span data-stu-id="02a33-157">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget": {
        "amount": 97,
        "attributes": {
            "objectType": "SpendingBudget"
        }
    },
    "resourceId": "44908a11-641b-4c53-b7fc-0f2bfca8a581",
    "resourceName": "Modern Azure Customer UK",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "attributes": {
        "objectType": "CustomerUsageSummary"
    }
}
```
