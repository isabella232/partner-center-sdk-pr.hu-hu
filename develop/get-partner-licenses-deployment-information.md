---
title: Partnerlicencek üzembehelyezési adatainak lekérése
description: A partneri licencek központi telepítési információinak beszerzése az összes ügyfél belefoglalásához.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 229f63d4df4f59cd0fde2bd0fc5e3f10cf6b25c0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768432"
---
# <a name="get-partner-licenses-deployment-information"></a><span data-ttu-id="7659e-103">Partnerlicencek üzembehelyezési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="7659e-103">Get partner licenses deployment information</span></span>

<span data-ttu-id="7659e-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="7659e-104">**Applies To**</span></span>

- <span data-ttu-id="7659e-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="7659e-105">Partner Center</span></span>

<span data-ttu-id="7659e-106">A partneri licencek központi telepítési információinak beszerzése az összes ügyfél belefoglalásához.</span><span class="sxs-lookup"><span data-stu-id="7659e-106">How to get partner licenses deployment information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="7659e-107">Ezt a forgatókönyvet a [licencek telepítési információi](get-licenses-deployment-information.md)felülírt.</span><span class="sxs-lookup"><span data-stu-id="7659e-107">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7659e-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="7659e-108">Prerequisites</span></span>

<span data-ttu-id="7659e-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="7659e-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7659e-110">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="7659e-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="7659e-111">C\#</span><span class="sxs-lookup"><span data-stu-id="7659e-111">C\#</span></span>

<span data-ttu-id="7659e-112">Ha összesített adatokat szeretne lekérdezni a licencek központi telepítéséről, először szerezzen be egy felületet a partner szintű elemzési gyűjtési műveletekhez a [**IAggregatePartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="7659e-112">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="7659e-113">Ezután kérjen le egy felületet a partner szintű licencek Analytics-gyűjteményhez a [**licencek**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="7659e-113">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="7659e-114">Végül hívja meg a [**Deployment. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) metódust a licencek összesített adatainak beolvasásához.</span><span class="sxs-lookup"><span data-stu-id="7659e-114">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="7659e-115">Ha a metódus sikeresen beolvassa a [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) -objektumok gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="7659e-115">If the method succeeds you'll get a collection of [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="7659e-116">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="7659e-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7659e-117">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="7659e-117">Request syntax</span></span>

| <span data-ttu-id="7659e-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="7659e-118">Method</span></span>  | <span data-ttu-id="7659e-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="7659e-119">Request URI</span></span>                                                                           |
|---------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="7659e-120">**GET**</span><span class="sxs-lookup"><span data-stu-id="7659e-120">**GET**</span></span> | <span data-ttu-id="7659e-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/licenses/Deployment http/1.1</span><span class="sxs-lookup"><span data-stu-id="7659e-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7659e-122">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="7659e-122">Request headers</span></span>

<span data-ttu-id="7659e-123">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7659e-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7659e-124">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="7659e-124">Request body</span></span>

<span data-ttu-id="7659e-125">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="7659e-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7659e-126">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="7659e-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7659e-127">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="7659e-127">REST response</span></span>

<span data-ttu-id="7659e-128">Ha ez sikeres, a válasz törzse olyan [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) -erőforrások gyűjteményét tartalmazza, amelyek a telepített licencekre vonatkozó információkat biztosítanak.</span><span class="sxs-lookup"><span data-stu-id="7659e-128">If successful, the response body contains a collection of [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7659e-129">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="7659e-129">Response success and error codes</span></span>

<span data-ttu-id="7659e-130">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="7659e-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7659e-131">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="7659e-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7659e-132">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="7659e-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7659e-133">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="7659e-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 102030524
Date: Tue, 14 Mar 2017 17:55:01 GMT

{
    "totalCount": 2,
    "items": [{
            "proratedDeploymentPercent": 0.0,
            "licensesSold": 343,
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }, {
            "proratedDeploymentPercent": 1.0,
            "licensesSold": 4464,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
