---
title: Használati összefoglalás beszerzése az ügyfél összes előfizetéséhez
description: A CustomerUsageSummary-erőforrás segítségével lekérheti az adott Azure-szolgáltatás vagy-erőforrás ügyfél általi használatát az aktuális számlázási időszak alatt.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c918434367a3514e6a6ad6034b4897c33f51025
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767960"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a><span data-ttu-id="95a08-103">Használati összefoglalás beszerzése az ügyfél összes előfizetéséhez</span><span class="sxs-lookup"><span data-stu-id="95a08-103">Get a usage summary for all of a customer's subscriptions</span></span>

<span data-ttu-id="95a08-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="95a08-104">**Applies to:**</span></span>

- <span data-ttu-id="95a08-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="95a08-105">Partner Center</span></span>
- <span data-ttu-id="95a08-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="95a08-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="95a08-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="95a08-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="95a08-108">A **CustomerUsageSummary** -erőforrás segítségével lekérheti az adott Azure-szolgáltatás vagy-erőforrás ügyfél általi használatát az aktuális számlázási időszak alatt.</span><span class="sxs-lookup"><span data-stu-id="95a08-108">You can use the **CustomerUsageSummary** resource to get a customer's usage of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95a08-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="95a08-109">Prerequisites</span></span>

- <span data-ttu-id="95a08-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="95a08-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="95a08-111">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="95a08-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="95a08-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95a08-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="95a08-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="95a08-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="95a08-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="95a08-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="95a08-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="95a08-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="95a08-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="95a08-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="95a08-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95a08-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="95a08-118">C\#</span><span class="sxs-lookup"><span data-stu-id="95a08-118">C\#</span></span>

<span data-ttu-id="95a08-119">Az ügyfél-előfizetések használati összegzésének beszerzése:</span><span class="sxs-lookup"><span data-stu-id="95a08-119">To get a usage summary for all of a customer's subscriptions:</span></span>

1. <span data-ttu-id="95a08-120">A **IAggregatePartner. Customs** gyűjtemény használatával hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="95a08-120">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="95a08-121">Hívja meg a **UsageSummary** tulajdonságot, amelyet a **Get ()** vagy a **GetAsync ()** metódus követ:</span><span class="sxs-lookup"><span data-stu-id="95a08-121">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

<span data-ttu-id="95a08-122">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="95a08-122">For an example, see the following:</span></span>

- <span data-ttu-id="95a08-123">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="95a08-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="95a08-124">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="95a08-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="95a08-125">Osztály: **GetCustomerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="95a08-125">Class: **GetCustomerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="95a08-126">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="95a08-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="95a08-127">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="95a08-127">Request syntax</span></span>

| <span data-ttu-id="95a08-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="95a08-128">Method</span></span>  | <span data-ttu-id="95a08-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="95a08-129">Request URI</span></span>                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="95a08-130">**GET**</span><span class="sxs-lookup"><span data-stu-id="95a08-130">**GET**</span></span> | <span data-ttu-id="95a08-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="95a08-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="95a08-132">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="95a08-132">URI parameter</span></span>

<span data-ttu-id="95a08-133">Ez a táblázat felsorolja a szükséges lekérdezési paramétert, hogy lekérje az ügyfél névleges használati adatait.</span><span class="sxs-lookup"><span data-stu-id="95a08-133">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="95a08-134">Név</span><span class="sxs-lookup"><span data-stu-id="95a08-134">Name</span></span>                   | <span data-ttu-id="95a08-135">Típus</span><span class="sxs-lookup"><span data-stu-id="95a08-135">Type</span></span>     | <span data-ttu-id="95a08-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="95a08-136">Required</span></span> | <span data-ttu-id="95a08-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="95a08-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="95a08-138">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="95a08-138">**customer-tenant-id**</span></span> | <span data-ttu-id="95a08-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="95a08-139">**guid**</span></span> | <span data-ttu-id="95a08-140">Y</span><span class="sxs-lookup"><span data-stu-id="95a08-140">Y</span></span>        | <span data-ttu-id="95a08-141">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="95a08-141">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="95a08-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="95a08-142">Request headers</span></span>

<span data-ttu-id="95a08-143">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="95a08-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="95a08-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="95a08-144">Request body</span></span>

<span data-ttu-id="95a08-145">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="95a08-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="95a08-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="95a08-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="95a08-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="95a08-147">REST response</span></span>

<span data-ttu-id="95a08-148">Ha ez sikeres, ez a metódus egy **CustomerUsageSummary** -erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="95a08-148">If successful, this method returns a **CustomerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="95a08-149">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="95a08-149">Response success and error codes</span></span>

<span data-ttu-id="95a08-150">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="95a08-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="95a08-151">A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="95a08-151">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="95a08-152">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="95a08-152">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="95a08-153">Válasz példa Microsoft Azure (MS-AZR-0145P) előfizetésre</span><span class="sxs-lookup"><span data-stu-id="95a08-153">Response example for Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="95a08-154">Ebben a példában az ügyfél egy **145P Azure TB** -ajánlatot vásárolt.</span><span class="sxs-lookup"><span data-stu-id="95a08-154">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="95a08-155">*Microsoft Azure (MS-AZR-0145P) előfizetéssel rendelkező ügyfelek esetében nem változik az API-válasz.*</span><span class="sxs-lookup"><span data-stu-id="95a08-155">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

### <a name="response-example-for-azure-plan"></a><span data-ttu-id="95a08-156">Válasz példa az Azure-csomagra</span><span class="sxs-lookup"><span data-stu-id="95a08-156">Response example for Azure plan</span></span>

<span data-ttu-id="95a08-157">Ebben a példában az ügyfél egy Azure-csomagot vásárolt.</span><span class="sxs-lookup"><span data-stu-id="95a08-157">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="95a08-158">*Az Azure-csomagokkal rendelkező ügyfelek esetében az API-válasz módosításai a következők:*</span><span class="sxs-lookup"><span data-stu-id="95a08-158">*For customers with Azure plans, there are the following changes to the API response:*</span></span>

- <span data-ttu-id="95a08-159">a **currencyLocale** helyére a **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="95a08-159">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="95a08-160">a **usdTotalCost** egy új mező</span><span class="sxs-lookup"><span data-stu-id="95a08-160">**usdTotalCost** is a new field</span></span>

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
