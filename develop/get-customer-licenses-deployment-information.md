---
title: Ügyféllicencek üzembehelyezési adatainak lekérése
description: A licencek üzembe helyezési információinak beszerzése egy adott ügyfél számára.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 3a39c6c908048305ff2dabf85a29d7ddc3628500
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768444"
---
# <a name="get-customer-licenses-deployment-information"></a><span data-ttu-id="af1df-103">Ügyféllicencek üzembehelyezési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="af1df-103">Get customer licenses deployment information</span></span>

<span data-ttu-id="af1df-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="af1df-104">**Applies To**</span></span>

- <span data-ttu-id="af1df-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="af1df-105">Partner Center</span></span>

<span data-ttu-id="af1df-106">A licencek üzembe helyezési információinak beszerzése egy adott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="af1df-106">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="af1df-107">Ezt a forgatókönyvet a [licencek telepítési információi](get-licenses-deployment-information.md)felülírt.</span><span class="sxs-lookup"><span data-stu-id="af1df-107">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af1df-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="af1df-108">Prerequisites</span></span>

<span data-ttu-id="af1df-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="af1df-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="af1df-110">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="af1df-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="af1df-111">C\#</span><span class="sxs-lookup"><span data-stu-id="af1df-111">C\#</span></span>

<span data-ttu-id="af1df-112">Ha egy adott ügyfélhez tartozó összesített adatokat szeretné lekérni az üzemelő példányon, először hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójának használatával, és azonosítsa az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="af1df-112">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="af1df-113">Ezután szerezzen be egy felületet az ügyfél szintű elemzési gyűjtési műveletekhez az [**analitikai**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="af1df-113">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="af1df-114">Ezután kérjen le egy felületet az ügyfél szintű licencek Analytics-gyűjteményhez a [**licencek**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="af1df-114">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="af1df-115">Végül hívja meg a [**Deployment. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) metódust a licencek összesített adatainak beolvasásához.</span><span class="sxs-lookup"><span data-stu-id="af1df-115">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="af1df-116">Ha a metódus sikeresen beolvassa a [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) -objektumok gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="af1df-116">If the method succeeds you'll get a collection of [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="af1df-117">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="af1df-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="af1df-118">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="af1df-118">Request syntax</span></span>

| <span data-ttu-id="af1df-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="af1df-119">Method</span></span>  | <span data-ttu-id="af1df-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="af1df-120">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="af1df-121">**GET**</span><span class="sxs-lookup"><span data-stu-id="af1df-121">**GET**</span></span> | <span data-ttu-id="af1df-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Analytics/licenses/Deployment http/1.1</span><span class="sxs-lookup"><span data-stu-id="af1df-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="af1df-123">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="af1df-123">URI parameter</span></span>

<span data-ttu-id="af1df-124">Az ügyfél azonosításához használja a következő Path paramétert.</span><span class="sxs-lookup"><span data-stu-id="af1df-124">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="af1df-125">Név</span><span class="sxs-lookup"><span data-stu-id="af1df-125">Name</span></span>        | <span data-ttu-id="af1df-126">Típus</span><span class="sxs-lookup"><span data-stu-id="af1df-126">Type</span></span> | <span data-ttu-id="af1df-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="af1df-127">Required</span></span> | <span data-ttu-id="af1df-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="af1df-128">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="af1df-129">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="af1df-129">customer-id</span></span> | <span data-ttu-id="af1df-130">guid</span><span class="sxs-lookup"><span data-stu-id="af1df-130">guid</span></span> | <span data-ttu-id="af1df-131">Igen</span><span class="sxs-lookup"><span data-stu-id="af1df-131">Yes</span></span>      | <span data-ttu-id="af1df-132">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="af1df-132">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="af1df-133">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="af1df-133">Request headers</span></span>

<span data-ttu-id="af1df-134">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="af1df-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="af1df-135">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="af1df-135">Request body</span></span>

<span data-ttu-id="af1df-136">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="af1df-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="af1df-137">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="af1df-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="af1df-138">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="af1df-138">REST response</span></span>

<span data-ttu-id="af1df-139">Ha ez sikeres, a válasz törzse olyan [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) -erőforrások gyűjteményét tartalmazza, amelyek a telepített licencekre vonatkozó információkat biztosítanak.</span><span class="sxs-lookup"><span data-stu-id="af1df-139">If successful, the response body contains a collection of [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="af1df-140">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="af1df-140">Response success and error codes</span></span>

<span data-ttu-id="af1df-141">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="af1df-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="af1df-142">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="af1df-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="af1df-143">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="af1df-143">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="af1df-144">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="af1df-144">Response example</span></span>

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
