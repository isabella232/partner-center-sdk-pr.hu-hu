---
title: Partnerlicencek használati adatainak lekérése
description: A partneri licencek használati információinak beszerzése az összes ügyfél belefoglalásához.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93d003fb269a3421b8efd8cebe8f396f97599a10
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768476"
---
# <a name="get-partner-licenses-usage-information"></a><span data-ttu-id="6764d-103">Partnerlicencek használati adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="6764d-103">Get partner licenses usage information</span></span>

<span data-ttu-id="6764d-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="6764d-104">**Applies To**</span></span>

- <span data-ttu-id="6764d-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="6764d-105">Partner Center</span></span>

<span data-ttu-id="6764d-106">A partneri licencek használati információinak beszerzése az összes ügyfél belefoglalásához.</span><span class="sxs-lookup"><span data-stu-id="6764d-106">How to get partner licenses usage information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="6764d-107">Ezt a forgatókönyvet a [licencek használati adatainak](get-licenses-usage-information.md)felülírt.</span><span class="sxs-lookup"><span data-stu-id="6764d-107">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6764d-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6764d-108">Prerequisites</span></span>

<span data-ttu-id="6764d-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="6764d-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6764d-110">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="6764d-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="6764d-111">C\#</span><span class="sxs-lookup"><span data-stu-id="6764d-111">C\#</span></span>

<span data-ttu-id="6764d-112">Ha összesített adatokat szeretne lekérdezni a licencek központi telepítéséről, először szerezzen be egy felületet a partner szintű elemzési gyűjtési műveletekhez a [**IAggregatePartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="6764d-112">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="6764d-113">Ezután kérjen le egy felületet a partner szintű licencek Analytics-gyűjteményhez a [**licencek**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="6764d-113">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="6764d-114">Végül hívja meg a [**használati. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) metódust, hogy beolvassa az összesített adatokat a licencek használatáról.</span><span class="sxs-lookup"><span data-stu-id="6764d-114">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="6764d-115">Ha a metódus sikeresen beolvassa a [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) -objektumok gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="6764d-115">If the method succeeds you'll get a collection of [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesUsageAnalytics = partnerOperations.Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="6764d-116">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="6764d-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6764d-117">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="6764d-117">Request syntax</span></span>

| <span data-ttu-id="6764d-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="6764d-118">Method</span></span>  | <span data-ttu-id="6764d-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="6764d-119">Request URI</span></span>                                                                      |
|---------|----------------------------------------------------------------------------------|
| <span data-ttu-id="6764d-120">**GET**</span><span class="sxs-lookup"><span data-stu-id="6764d-120">**GET**</span></span> | <span data-ttu-id="6764d-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/licenses/Usage http/1.1</span><span class="sxs-lookup"><span data-stu-id="6764d-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6764d-122">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="6764d-122">Request headers</span></span>

<span data-ttu-id="6764d-123">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6764d-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6764d-124">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="6764d-124">Request body</span></span>

<span data-ttu-id="6764d-125">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="6764d-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6764d-126">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="6764d-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="6764d-127">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="6764d-127">REST response</span></span>

<span data-ttu-id="6764d-128">Ha a művelet sikeres, a válasz törzse [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) -erőforrások gyűjteményét tartalmazza, amelyek a felhasznált licencekre vonatkozó információkat biztosítanak.</span><span class="sxs-lookup"><span data-stu-id="6764d-128">If successful, the response body contains a collection of [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) resources that provide information about the licenses used.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6764d-129">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="6764d-129">Response success and error codes</span></span>

<span data-ttu-id="6764d-130">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="6764d-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6764d-131">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="6764d-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6764d-132">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="6764d-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6764d-133">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="6764d-133">Response example</span></span>

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
