---
title: Partnerlicencek használati adatainak lekérése
description: A partnerlicencek használati információinak összesítése az összes ügyfélre vonatkozó összesítéssel.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f3d05d61ac4f2c90b0d8a4bfd93fe24e94bd5c1b
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445595"
---
# <a name="get-partner-licenses-usage-information"></a><span data-ttu-id="d9489-103">Partnerlicencek használati adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="d9489-103">Get partner licenses usage information</span></span>

<span data-ttu-id="d9489-104">A partnerlicencek használati információinak összesítése az összes ügyfélre vonatkozó összesítéssel.</span><span class="sxs-lookup"><span data-stu-id="d9489-104">How to get partner licenses usage information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="d9489-105">Ezt a forgatókönyvet a [Get licenses usage information (Licencek használati információinak lekért információja) alapján lehet szuperlökni.](get-licenses-usage-information.md)</span><span class="sxs-lookup"><span data-stu-id="d9489-105">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9489-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d9489-106">Prerequisites</span></span>

<span data-ttu-id="d9489-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d9489-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d9489-108">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="d9489-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d9489-109">C\#</span><span class="sxs-lookup"><span data-stu-id="d9489-109">C\#</span></span>

<span data-ttu-id="d9489-110">A licencek üzembe helyezésével kapcsolatos összesített adatok lekéréséhez először szerezze be a partnerszintű elemzési adatgyűjtési műveletek felületét az [**IAggregatePartner.Analytics tulajdonságból.**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics)</span><span class="sxs-lookup"><span data-stu-id="d9489-110">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="d9489-111">Ezután a [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) (Licencek) tulajdonságból olvassa be a partnerszintű licencelemzési gyűjtemény felületét.</span><span class="sxs-lookup"><span data-stu-id="d9489-111">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="d9489-112">Végül hívja meg a [**Usage.Get metódust**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) a licenchasználat összesített adatainak lehívására.</span><span class="sxs-lookup"><span data-stu-id="d9489-112">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="d9489-113">Ha a metódus sikeres, a [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) objektumok gyűjteményét fogja kapni.</span><span class="sxs-lookup"><span data-stu-id="d9489-113">If the method succeeds, you'll get a collection of [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesUsageAnalytics = partnerOperations.Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="d9489-114">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d9489-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d9489-115">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d9489-115">Request syntax</span></span>

| <span data-ttu-id="d9489-116">Metódus</span><span class="sxs-lookup"><span data-stu-id="d9489-116">Method</span></span>  | <span data-ttu-id="d9489-117">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d9489-117">Request URI</span></span>                                                                      |
|---------|----------------------------------------------------------------------------------|
| <span data-ttu-id="d9489-118">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d9489-118">**GET**</span></span> | <span data-ttu-id="d9489-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d9489-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d9489-120">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d9489-120">Request headers</span></span>

<span data-ttu-id="d9489-121">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d9489-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d9489-122">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d9489-122">Request body</span></span>

<span data-ttu-id="d9489-123">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d9489-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d9489-124">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d9489-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d9489-125">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d9489-125">REST response</span></span>

<span data-ttu-id="d9489-126">Ha a válasz törzse sikeres, a [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) erőforrások gyűjteményét tartalmazza, amelyek információt nyújtanak a használt licencekkel kapcsolatban.</span><span class="sxs-lookup"><span data-stu-id="d9489-126">If successful, the response body contains a collection of [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) resources that provide information about the licenses used.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d9489-127">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d9489-127">Response success and error codes</span></span>

<span data-ttu-id="d9489-128">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d9489-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d9489-129">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d9489-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d9489-130">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d9489-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d9489-131">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d9489-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1156
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CV: wk0/vjugzEe0Z9cv.0
MS-ServerId: 101112012
Date: Wed, 15 Mar 2017 01:18:26 GMT

{
    "totalCount": 5,
    "items": [{
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Microsoft Dynamics CRM",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
