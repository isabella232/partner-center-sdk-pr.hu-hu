---
title: Az összes ügyfél használati rekordjainak lekért száma
description: A CustomerMonthlyUsageRecord erőforrás-gyűjtemény használatával lekért használati rekordok minden olyan ügyfélhez, aki egy adott Azure-szolgáltatást vagy -erőforrást vásárolt.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6b3fb0e1989336810f2afcc2a5bfc3a1d2849b7f
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874890"
---
# <a name="get-usage-records-for-all-customers"></a><span data-ttu-id="1504c-103">Az összes ügyfél használati rekordjainak lekért száma</span><span class="sxs-lookup"><span data-stu-id="1504c-103">Get usage records for all customers</span></span>

<span data-ttu-id="1504c-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1504c-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1504c-105">A partnerek a **CustomerMonthlyUsageRecord erőforrás-gyűjtemény** használatával lekért használati adatokat kaphatnak minden ügyfélhez.</span><span class="sxs-lookup"><span data-stu-id="1504c-105">Partners can use the **CustomerMonthlyUsageRecord** resource collection to get usage records for all their customers.</span></span> <span data-ttu-id="1504c-106">Ez az erőforrás az összes ügyfél használati adatait képviseli.</span><span class="sxs-lookup"><span data-stu-id="1504c-106">This resource represents usage records for all customers.</span></span> <span data-ttu-id="1504c-107">Ide tartoznak azok az ügyfelek, akik Microsoft Azure (MS-AZR-0145P) előfizetéssel vagy Azure-csomaggal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="1504c-107">That includes those customers with a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1504c-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="1504c-108">Prerequisites</span></span>

- <span data-ttu-id="1504c-109">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1504c-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1504c-110">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="1504c-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1504c-111">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1504c-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1504c-112">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="1504c-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1504c-113">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="1504c-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1504c-114">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="1504c-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1504c-115">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="1504c-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1504c-116">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1504c-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1504c-117">C\#</span><span class="sxs-lookup"><span data-stu-id="1504c-117">C\#</span></span>

<span data-ttu-id="1504c-118">Az adott Azure-szolgáltatást vagy -erőforrást az aktuális számlázási időszakban megvásároló összes ügyfél összes használati rekordját le kell kapnia:</span><span class="sxs-lookup"><span data-stu-id="1504c-118">To get all the usage records for all customers who purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="1504c-119">Az **IAggregatePartner.Customers gyűjtemény** használatával hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="1504c-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="1504c-120">Hívja **meg a UsageRecords** tulajdonságot, majd hívja meg a **Get() vagy** a **GetAsync() metódust.**</span><span class="sxs-lookup"><span data-stu-id="1504c-120">Call **UsageRecords** property, then call the **Get()** or **GetAsync()** method.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    var usageRecords = partnerOperations.Customers.UsageRecords.Get();
    ```

<span data-ttu-id="1504c-121">Példaként tekintse meg a következő mintát:</span><span class="sxs-lookup"><span data-stu-id="1504c-121">For an example, see the following sample:</span></span>

- <span data-ttu-id="1504c-122">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1504c-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="1504c-123">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="1504c-123">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="1504c-124">Osztály: **GetCustomerUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="1504c-124">Class: **GetCustomerUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="1504c-125">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="1504c-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1504c-126">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="1504c-126">Request syntax</span></span>

| <span data-ttu-id="1504c-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="1504c-127">Method</span></span>  | <span data-ttu-id="1504c-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="1504c-128">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="1504c-129">**Kap**</span><span class="sxs-lookup"><span data-stu-id="1504c-129">**GET**</span></span> | <span data-ttu-id="1504c-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/usagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1504c-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/usagerecords HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1504c-131">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="1504c-131">Request headers</span></span>

<span data-ttu-id="1504c-132">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1504c-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1504c-133">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="1504c-133">Request body</span></span>

<span data-ttu-id="1504c-134">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="1504c-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1504c-135">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="1504c-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="1504c-136">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="1504c-136">REST response</span></span>

<span data-ttu-id="1504c-137">Ha sikeres, ez a metódus egy **CustomerMonthlyUsageRecord** erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="1504c-137">If successful, this method returns a **CustomerMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1504c-138">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="1504c-138">Response success and error codes</span></span>

<span data-ttu-id="1504c-139">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="1504c-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1504c-140">Ezt a kódot, a hibatípust és a további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="1504c-140">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="1504c-141">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1504c-141">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1504c-142">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="1504c-142">Response example</span></span>

<span data-ttu-id="1504c-143">Az **isUpgraded** tulajdonság használatával azonosíthatja az Azure-csomagokkal kapcsolatos ügyfeleket.</span><span class="sxs-lookup"><span data-stu-id="1504c-143">You can use the **isUpgraded** property to identify customers who have an Azure plan.</span></span> <span data-ttu-id="1504c-144">Ha az **isUpgraded** értéke **igaz,** az azt jelenti, hogy az ügyfelek Azure-csomagokkal vannak.</span><span class="sxs-lookup"><span data-stu-id="1504c-144">If the value for **isUpgraded** is **true**, it means the customers have Azure plans.</span></span>

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
