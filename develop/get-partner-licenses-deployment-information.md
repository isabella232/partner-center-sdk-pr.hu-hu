---
title: Partnerlicencek üzembehelyezési adatainak lekérése
description: A partnerlicencek üzembe helyezési információinak összesítése az összes ügyfélre.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2464242fc6dc4e7464511eac5d4197630e22fac0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445976"
---
# <a name="get-partner-licenses-deployment-information"></a><span data-ttu-id="13d39-103">Partnerlicencek üzembehelyezési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="13d39-103">Get partner licenses deployment information</span></span>

<span data-ttu-id="13d39-104">A partnerlicencek üzembe helyezési információinak összesítése az összes ügyfélre.</span><span class="sxs-lookup"><span data-stu-id="13d39-104">How to get partner licenses deployment information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="13d39-105">Ezt a forgatókönyvet a Licencek le get deployment information (Licencek üzembe helyezési [információinak le szolgáltatása) szuperküldi le.](get-licenses-deployment-information.md)</span><span class="sxs-lookup"><span data-stu-id="13d39-105">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13d39-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="13d39-106">Prerequisites</span></span>

<span data-ttu-id="13d39-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="13d39-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="13d39-108">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="13d39-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="13d39-109">C\#</span><span class="sxs-lookup"><span data-stu-id="13d39-109">C\#</span></span>

<span data-ttu-id="13d39-110">A licencek üzembe helyezésével kapcsolatos összesített adatok lekéréséhez először szerezze be a partnerszintű elemzési gyűjtemény műveleteinek felületét az [**IAggregatePartner.Analytics tulajdonságból.**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics)</span><span class="sxs-lookup"><span data-stu-id="13d39-110">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="13d39-111">Ezután a [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) (Licencek) tulajdonságból olvassa be a partnerszintű licencelemzési gyűjtemény felületét.</span><span class="sxs-lookup"><span data-stu-id="13d39-111">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="13d39-112">Végül hívja meg a [**Deployment.Get metódust**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) a licencek üzembe helyezésével kapcsolatos összesített adatok lehívására.</span><span class="sxs-lookup"><span data-stu-id="13d39-112">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="13d39-113">Ha a metódus sikeres, a [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) objektumok gyűjteményét fogja kapni.</span><span class="sxs-lookup"><span data-stu-id="13d39-113">If the method succeeds, you'll get a collection of [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="13d39-114">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="13d39-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="13d39-115">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="13d39-115">Request syntax</span></span>

| <span data-ttu-id="13d39-116">Metódus</span><span class="sxs-lookup"><span data-stu-id="13d39-116">Method</span></span>  | <span data-ttu-id="13d39-117">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="13d39-117">Request URI</span></span>                                                                           |
|---------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="13d39-118">**Kap**</span><span class="sxs-lookup"><span data-stu-id="13d39-118">**GET**</span></span> | <span data-ttu-id="13d39-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="13d39-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="13d39-120">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="13d39-120">Request headers</span></span>

<span data-ttu-id="13d39-121">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="13d39-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="13d39-122">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="13d39-122">Request body</span></span>

<span data-ttu-id="13d39-123">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="13d39-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="13d39-124">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="13d39-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="13d39-125">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="13d39-125">REST response</span></span>

<span data-ttu-id="13d39-126">Ha a válasz törzse sikeres, a [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) erőforrások gyűjteményét tartalmazza, amelyek információt nyújtanak az üzembe helyezett licencekkel kapcsolatban.</span><span class="sxs-lookup"><span data-stu-id="13d39-126">If successful, the response body contains a collection of [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="13d39-127">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="13d39-127">Response success and error codes</span></span>

<span data-ttu-id="13d39-128">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="13d39-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="13d39-129">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="13d39-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="13d39-130">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="13d39-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="13d39-131">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="13d39-131">Response example</span></span>

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
