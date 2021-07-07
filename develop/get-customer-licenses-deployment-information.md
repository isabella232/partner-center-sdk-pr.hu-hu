---
title: Ügyféllicencek üzembehelyezési adatainak lekérése
description: Licencek üzembe helyezési elemzésének le szolgáltatása egy adott ügyfél számára.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 91fe9da185aa59025d4dc8263257b207edb4a5be
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446462"
---
# <a name="get-customer-licenses-deployment-information"></a><span data-ttu-id="dc460-103">Ügyféllicencek üzembehelyezési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="dc460-103">Get customer licenses deployment information</span></span>

<span data-ttu-id="dc460-104">Licencek üzembe helyezési elemzésének le szolgáltatása egy adott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="dc460-104">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="dc460-105">Ezt a forgatókönyvet a Licencek le get deployment information (Licencek üzembe helyezési [információinak le szolgáltatása) szuperküldi le.](get-licenses-deployment-information.md)</span><span class="sxs-lookup"><span data-stu-id="dc460-105">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc460-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="dc460-106">Prerequisites</span></span>

<span data-ttu-id="dc460-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="dc460-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dc460-108">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="dc460-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="dc460-109">C\#</span><span class="sxs-lookup"><span data-stu-id="dc460-109">C\#</span></span>

<span data-ttu-id="dc460-110">Egy adott ügyfél üzembe helyezésével kapcsolatos összesített adatok lekéréséhez először hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="dc460-110">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="dc460-111">Ezután szerezze be az ügyfélszintű elemzési gyűjtemény műveleteinek felületét az [**Analytics tulajdonságból.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics)</span><span class="sxs-lookup"><span data-stu-id="dc460-111">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="dc460-112">Ezután a [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) (Licencek) tulajdonságból olvassa be az ügyfélszintű licencelemzési gyűjtemény felületét.</span><span class="sxs-lookup"><span data-stu-id="dc460-112">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="dc460-113">Végül hívja meg a [**Deployment.Get metódust**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) a licencek üzembe helyezésével kapcsolatos összesített adatok lehívására.</span><span class="sxs-lookup"><span data-stu-id="dc460-113">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="dc460-114">Ha a metódus sikeres, a [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) objektumok gyűjteményét fogja kapni.</span><span class="sxs-lookup"><span data-stu-id="dc460-114">If the method succeeds, you'll get a collection of [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="dc460-115">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="dc460-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dc460-116">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="dc460-116">Request syntax</span></span>

| <span data-ttu-id="dc460-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="dc460-117">Method</span></span>  | <span data-ttu-id="dc460-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="dc460-118">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dc460-119">**Kap**</span><span class="sxs-lookup"><span data-stu-id="dc460-119">**GET**</span></span> | <span data-ttu-id="dc460-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/analytics/licenses/deployment HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="dc460-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="dc460-121">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="dc460-121">URI parameter</span></span>

<span data-ttu-id="dc460-122">Az ügyfél azonosításához használja a következő elérésiút-paramétert.</span><span class="sxs-lookup"><span data-stu-id="dc460-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="dc460-123">Név</span><span class="sxs-lookup"><span data-stu-id="dc460-123">Name</span></span>        | <span data-ttu-id="dc460-124">Típus</span><span class="sxs-lookup"><span data-stu-id="dc460-124">Type</span></span> | <span data-ttu-id="dc460-125">Kötelező</span><span class="sxs-lookup"><span data-stu-id="dc460-125">Required</span></span> | <span data-ttu-id="dc460-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="dc460-126">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="dc460-127">ügyfélazonosító</span><span class="sxs-lookup"><span data-stu-id="dc460-127">customer-id</span></span> | <span data-ttu-id="dc460-128">guid</span><span class="sxs-lookup"><span data-stu-id="dc460-128">guid</span></span> | <span data-ttu-id="dc460-129">Igen</span><span class="sxs-lookup"><span data-stu-id="dc460-129">Yes</span></span>      | <span data-ttu-id="dc460-130">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="dc460-130">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="dc460-131">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="dc460-131">Request headers</span></span>

<span data-ttu-id="dc460-132">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="dc460-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dc460-133">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="dc460-133">Request body</span></span>

<span data-ttu-id="dc460-134">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="dc460-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="dc460-135">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="dc460-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="dc460-136">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="dc460-136">REST response</span></span>

<span data-ttu-id="dc460-137">Ha a válasz törzse sikeres, a [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) erőforrások gyűjteményét tartalmazza, amelyek információt nyújtanak az üzembe helyezett licencekkel kapcsolatban.</span><span class="sxs-lookup"><span data-stu-id="dc460-137">If successful, the response body contains a collection of [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dc460-138">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="dc460-138">Response success and error codes</span></span>

<span data-ttu-id="dc460-139">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="dc460-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dc460-140">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="dc460-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dc460-141">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="dc460-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dc460-142">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="dc460-142">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1012
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CV: deEp2Wy6DUitMCYA.0
MS-ServerId: 102030524
Date: Wed, 15 Mar 2017 01:19:18 GMT

{
    "totalCount": 3,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 1,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 5,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 2,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
