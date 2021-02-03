---
title: Egy partner használati összegzésének beolvasása
description: A PartnerUsageSummary-erőforrás használatával lekérheti az összes olyan ügyfél partneri használati összefoglalását, amely az aktuális számlázási időszakban megvásárolt egy adott Azure-szolgáltatást vagy erőforrást.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: ba1885f46043a75274595239fe61ce3ef0998acf
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767899"
---
# <a name="get-a-usage-summary-for-a-partner"></a><span data-ttu-id="ffb57-103">Egy partner használati összegzésének beolvasása</span><span class="sxs-lookup"><span data-stu-id="ffb57-103">Get a usage summary for a partner</span></span>

<span data-ttu-id="ffb57-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="ffb57-104">**Applies to:**</span></span>

- <span data-ttu-id="ffb57-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="ffb57-105">Partner Center</span></span>
- <span data-ttu-id="ffb57-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="ffb57-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ffb57-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="ffb57-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ffb57-108">A **PartnerUsageSummary** -erőforrás használatával lekérheti az összes olyan ügyfél partneri használati összefoglalását, amely az aktuális számlázási időszakban megvásárolt egy adott Azure-szolgáltatást vagy erőforrást.</span><span class="sxs-lookup"><span data-stu-id="ffb57-108">You can use the **PartnerUsageSummary** resource to get a partner usage summary of all customers that purchased a specific Azure service or resource during the current billing period.</span></span>

<span data-ttu-id="ffb57-109">*Az API által visszaadott összeg nem adja vissza az Azure-csomaggal rendelkező ügyfelek felhasználását.*</span><span class="sxs-lookup"><span data-stu-id="ffb57-109">*The total returned by this API will not return consumption for customers that have an Azure plan.*</span></span> <span data-ttu-id="ffb57-110">A jövőben várhatóan elavulttá válik.</span><span class="sxs-lookup"><span data-stu-id="ffb57-110">Planned for deprecation in the future.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffb57-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="ffb57-111">Prerequisites</span></span>

- <span data-ttu-id="ffb57-112">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="ffb57-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ffb57-113">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="ffb57-113">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="ffb57-114">C\#</span><span class="sxs-lookup"><span data-stu-id="ffb57-114">C\#</span></span>

<span data-ttu-id="ffb57-115">Az adott Azure-szolgáltatást vagy-erőforrást az aktuális számlázási időszak alatt megvásárolt összes ügyfél használati összegzésének lekéréséhez:</span><span class="sxs-lookup"><span data-stu-id="ffb57-115">To get a usage summary for all customers that purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="ffb57-116">Használja a **IAggregatePartner**.</span><span class="sxs-lookup"><span data-stu-id="ffb57-116">Use your **IAggregatePartner**.</span></span>

2. <span data-ttu-id="ffb57-117">Hívja meg a **UsageSummary** tulajdonságot, amelyet a **Get ()** vagy a **GetAsync ()** metódus követ:</span><span class="sxs-lookup"><span data-stu-id="ffb57-117">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;

    var usageSummary = partnerOperations.UsageSummary.Get();
    ```

<span data-ttu-id="ffb57-118">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="ffb57-118">For an example, see the following:</span></span>

- <span data-ttu-id="ffb57-119">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ffb57-119">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="ffb57-120">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="ffb57-120">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="ffb57-121">Osztály: **GetPartnerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="ffb57-121">Class: **GetPartnerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="ffb57-122">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="ffb57-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ffb57-123">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="ffb57-123">Request syntax</span></span>

| <span data-ttu-id="ffb57-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="ffb57-124">Method</span></span>  | <span data-ttu-id="ffb57-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="ffb57-125">Request URI</span></span>                                                         |
|---------|---------------------------------------------------------------------|
| <span data-ttu-id="ffb57-126">**GET**</span><span class="sxs-lookup"><span data-stu-id="ffb57-126">**GET**</span></span> | <span data-ttu-id="ffb57-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="ffb57-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ffb57-128">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="ffb57-128">Request headers</span></span>

<span data-ttu-id="ffb57-129">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ffb57-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ffb57-130">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="ffb57-130">Request body</span></span>

<span data-ttu-id="ffb57-131">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="ffb57-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ffb57-132">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ffb57-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="ffb57-133">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="ffb57-133">REST response</span></span>

<span data-ttu-id="ffb57-134">Ha ez sikeres, ez a metódus egy **PartnerUsageSummary** -erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="ffb57-134">If successful, this method returns a **PartnerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ffb57-135">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="ffb57-135">Response success and error codes</span></span>

<span data-ttu-id="ffb57-136">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="ffb57-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ffb57-137">A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="ffb57-137">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="ffb57-138">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ffb57-138">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ffb57-139">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ffb57-139">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "customersOverBudget": 1,
    "customersTrendingOver": 0,
    "customersWithUsageBasedSubscription": 11,
    "resourceId": "11111111-4574-4539-bc42-0e539b9684c0",
    "id": "11111111-4574-4539-bc42-0e539b9684c0",
    "resourceName": "PLAMUATT2NETNEW",
    "name": "PLAMUATT2NETNEW",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerUsageSummary"
    }
}
```
