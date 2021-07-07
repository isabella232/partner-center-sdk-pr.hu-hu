---
title: Egy partner használati összegzésének lekért táblázata
description: A PartnerUsageSummary erőforrás használatával lekértheti az összes olyan ügyfél partnerhasználati összegzését, aki adott Azure-szolgáltatást vagy -erőforrást vásárolt az aktuális számlázási időszakban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: f003980f1b521ad0ac26dbfd0d4821b9096fdd27
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873904"
---
# <a name="get-a-usage-summary-for-a-partner"></a><span data-ttu-id="99a3b-103">Egy partner használati összegzésének lekért táblázata</span><span class="sxs-lookup"><span data-stu-id="99a3b-103">Get a usage summary for a partner</span></span>

<span data-ttu-id="99a3b-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="99a3b-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="99a3b-105">A **PartnerUsageSummary** erőforrással lekért partneri használati összegzést kaphat az összes olyan ügyfélről, aki adott Azure-szolgáltatást vagy -erőforrást vásárolt az aktuális számlázási időszakban.</span><span class="sxs-lookup"><span data-stu-id="99a3b-105">You can use the **PartnerUsageSummary** resource to get a partner usage summary of all customers that purchased a specific Azure service or resource during the current billing period.</span></span>

<span data-ttu-id="99a3b-106">*Az API által visszaadott összeg nem adja vissza az Azure-csomaghoz használó ügyfelek fogyasztását.*</span><span class="sxs-lookup"><span data-stu-id="99a3b-106">*The total returned by this API will not return consumption for customers that have an Azure plan.*</span></span> <span data-ttu-id="99a3b-107">A jövőben elalasztást tervezünk.</span><span class="sxs-lookup"><span data-stu-id="99a3b-107">Planned for deprecation in the future.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99a3b-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="99a3b-108">Prerequisites</span></span>

- <span data-ttu-id="99a3b-109">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="99a3b-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="99a3b-110">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="99a3b-110">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="99a3b-111">C\#</span><span class="sxs-lookup"><span data-stu-id="99a3b-111">C\#</span></span>

<span data-ttu-id="99a3b-112">Az adott Azure-szolgáltatást vagy -erőforrást az aktuális számlázási időszakban megvásárolt összes ügyfél használati összegzésének lekérte:</span><span class="sxs-lookup"><span data-stu-id="99a3b-112">To get a usage summary for all customers that purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="99a3b-113">Használja az **IAggregatePartnert.**</span><span class="sxs-lookup"><span data-stu-id="99a3b-113">Use your **IAggregatePartner**.</span></span>

2. <span data-ttu-id="99a3b-114">Hívja meg **a UsageSummary** tulajdonságot, majd a **Get() vagy** **a GetAsync() metódust:**</span><span class="sxs-lookup"><span data-stu-id="99a3b-114">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;

    var usageSummary = partnerOperations.UsageSummary.Get();
    ```

<span data-ttu-id="99a3b-115">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="99a3b-115">For an example, see the following:</span></span>

- <span data-ttu-id="99a3b-116">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="99a3b-116">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="99a3b-117">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="99a3b-117">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="99a3b-118">Osztály: **GetPartnerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="99a3b-118">Class: **GetPartnerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="99a3b-119">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="99a3b-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="99a3b-120">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="99a3b-120">Request syntax</span></span>

| <span data-ttu-id="99a3b-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="99a3b-121">Method</span></span>  | <span data-ttu-id="99a3b-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="99a3b-122">Request URI</span></span>                                                         |
|---------|---------------------------------------------------------------------|
| <span data-ttu-id="99a3b-123">**Kap**</span><span class="sxs-lookup"><span data-stu-id="99a3b-123">**GET**</span></span> | <span data-ttu-id="99a3b-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="99a3b-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="99a3b-125">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="99a3b-125">Request headers</span></span>

<span data-ttu-id="99a3b-126">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="99a3b-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="99a3b-127">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="99a3b-127">Request body</span></span>

<span data-ttu-id="99a3b-128">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="99a3b-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="99a3b-129">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="99a3b-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="99a3b-130">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="99a3b-130">REST response</span></span>

<span data-ttu-id="99a3b-131">Ha sikeres, ez a metódus egy **PartnerUsageSummary** erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="99a3b-131">If successful, this method returns a **PartnerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="99a3b-132">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="99a3b-132">Response success and error codes</span></span>

<span data-ttu-id="99a3b-133">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="99a3b-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="99a3b-134">Egy hálózati nyomkövetési eszközzel olvassa be ezt a kódot, a hiba típusát és a további paramétereket.</span><span class="sxs-lookup"><span data-stu-id="99a3b-134">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="99a3b-135">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="99a3b-135">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="99a3b-136">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="99a3b-136">Response example</span></span>

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
