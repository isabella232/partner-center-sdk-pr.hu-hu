---
title: Használati rekordok beolvasása az összes ügyfél számára
description: A CustomerMonthlyUsageRecord erőforrás-gyűjtemény használatával lekérheti az összes olyan ügyfél használati adatait, akik egy adott Azure-szolgáltatást vagy-erőforrást vásároltak.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: da829a6de3690a9b1117ce9dfa58fbe381cafd81
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767980"
---
# <a name="get-usage-records-for-all-customers"></a><span data-ttu-id="73e03-103">Használati rekordok beolvasása az összes ügyfél számára</span><span class="sxs-lookup"><span data-stu-id="73e03-103">Get usage records for all customers</span></span>

<span data-ttu-id="73e03-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="73e03-104">**Applies to:**</span></span>

- <span data-ttu-id="73e03-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="73e03-105">Partner Center</span></span>
- <span data-ttu-id="73e03-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="73e03-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="73e03-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="73e03-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="73e03-108">A partnerek a **CustomerMonthlyUsageRecord** erőforrás-gyűjtemény használatával lekérhetik az összes ügyfelet használó használati rekordokat.</span><span class="sxs-lookup"><span data-stu-id="73e03-108">Partners can use the **CustomerMonthlyUsageRecord** resource collection to get usage records for all their customers.</span></span> <span data-ttu-id="73e03-109">Ez az erőforrás az összes ügyfél használati rekordjait jelképezi.</span><span class="sxs-lookup"><span data-stu-id="73e03-109">This resource represents usage records for all customers.</span></span> <span data-ttu-id="73e03-110">Ezek az ügyfelek Microsoft Azure (MS-AZR-0145P) előfizetéssel vagy egy Azure-csomaggal rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="73e03-110">That includes those customers with a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73e03-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="73e03-111">Prerequisites</span></span>

- <span data-ttu-id="73e03-112">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="73e03-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="73e03-113">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="73e03-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="73e03-114">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="73e03-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="73e03-115">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="73e03-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="73e03-116">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="73e03-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="73e03-117">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="73e03-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="73e03-118">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="73e03-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="73e03-119">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="73e03-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="73e03-120">C\#</span><span class="sxs-lookup"><span data-stu-id="73e03-120">C\#</span></span>

<span data-ttu-id="73e03-121">Az adott Azure-szolgáltatást vagy-erőforrást az aktuális számlázási időszak alatt megvásárolt összes ügyfél összes használati rekordjának lekérése:</span><span class="sxs-lookup"><span data-stu-id="73e03-121">To get all the usage records for all customers who purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="73e03-122">A **IAggregatePartner. Customs** gyűjtemény használatával hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="73e03-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="73e03-123">Hívja meg a **UsageRecords** tulajdonságot, majd hívja meg a **Get ()** vagy a **GetAsync ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="73e03-123">Call **UsageRecords** property, then call the **Get()** or **GetAsync()** method.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    var usageRecords = partnerOperations.Customers.UsageRecords.Get();
    ```

<span data-ttu-id="73e03-124">Példaként tekintse meg a következő mintát:</span><span class="sxs-lookup"><span data-stu-id="73e03-124">For an example, see the following sample:</span></span>

- <span data-ttu-id="73e03-125">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="73e03-125">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="73e03-126">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="73e03-126">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="73e03-127">Osztály: **GetCustomerUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="73e03-127">Class: **GetCustomerUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="73e03-128">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="73e03-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="73e03-129">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="73e03-129">Request syntax</span></span>

| <span data-ttu-id="73e03-130">Metódus</span><span class="sxs-lookup"><span data-stu-id="73e03-130">Method</span></span>  | <span data-ttu-id="73e03-131">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="73e03-131">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="73e03-132">**GET**</span><span class="sxs-lookup"><span data-stu-id="73e03-132">**GET**</span></span> | <span data-ttu-id="73e03-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/usagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="73e03-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/usagerecords HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="73e03-134">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="73e03-134">Request headers</span></span>

<span data-ttu-id="73e03-135">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="73e03-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="73e03-136">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="73e03-136">Request body</span></span>

<span data-ttu-id="73e03-137">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="73e03-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="73e03-138">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="73e03-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="73e03-139">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="73e03-139">REST response</span></span>

<span data-ttu-id="73e03-140">Ha ez sikeres, ez a metódus egy **CustomerMonthlyUsageRecord** -erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="73e03-140">If successful, this method returns a **CustomerMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="73e03-141">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="73e03-141">Response success and error codes</span></span>

<span data-ttu-id="73e03-142">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="73e03-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="73e03-143">A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="73e03-143">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="73e03-144">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="73e03-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="73e03-145">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="73e03-145">Response example</span></span>

<span data-ttu-id="73e03-146">A **isUpgraded** tulajdonsággal azonosíthatók azok az ügyfelek, akik Azure-csomaggal rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="73e03-146">You can use the **isUpgraded** property to identify customers who have an Azure plan.</span></span> <span data-ttu-id="73e03-147">Ha a **isUpgraded** értéke **igaz**, az azt jelenti, hogy az ügyfelek rendelkeznek Azure-csomagokkal.</span><span class="sxs-lookup"><span data-stu-id="73e03-147">If the value for **isUpgraded** is **true**, it means the customers have Azure plans.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 25,
    "items": [
        {
            "budget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "customerSpendingBudget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 0,
            "isUpgraded": false,
            "resourceId": "11111111-1843-4b3b-872f-206e08a08e51",
            "id": "11111111-1843-4b3b-872f-206e08a08e51",
            "resourceName": "LEGACY AZURE CUSTOMER SE",
            "name": "LEGACY AZURE CUSTOMER SE",
            "totalCost": 0,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-08-01T23:00:16.57+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
        {
            "budget": {
                "amount": 20,
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 602.84,
            "isUpgraded": true,
            "resourceId": "11111111-6fb9-4b05-8f15-b3d72e0596e6",
            "id": "11111111-6fb9-4b05-8f15-b3d72e0596e6",
            "resourceName": "Modern Azure Customer SE",
            "name": "Modern Azure Customer SE",
            "totalCost": 120.5682999999995904716,
            "currencyCode": "SEK",
            "usdTotalCost": 12.39999999999999985235,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
        {
            "budget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 0,
            "isUpgraded": true,
            "resourceId": "11111111-5892-4326-8541-9da1fdb233fb",
            "id": "11111111-5892-4326-8541-9da1fdb233fb",
            "resourceName": "Test_Test_MA20190829_14",
            "name": "Test_Test_MA20190829_14",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
           {
            "budget": {
                "amount": 97,
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 28.08,
            "isUpgraded": true,
            "resourceId": "11111111-641b-4c53-b7fc-0f2bfca8a581",
            "id": "11111111-641b-4c53-b7fc-0f2bfca8a581",
            "resourceName": "Modern Azure Customer UK",
            "name": "Modern Azure Customer UK",
            "totalCost": 27.23292827625710931604,
            "currencyCode": "GBP",
            "usdTotalCost": 33.280000000000001044,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
