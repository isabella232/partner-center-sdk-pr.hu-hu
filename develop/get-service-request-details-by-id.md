---
title: A szolgáltatási kérelem részleteinek beolvasása azonosító alapján.
description: Meglévő ügyfél-szolgáltatási kérelem adatainak beolvasása azonosító alapján.
ms.date: 02/06/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c79fd3f5e5609a1893891e9b2a8078f8678497b3
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768475"
---
# <a name="get-service-request-details-by-id"></a><span data-ttu-id="ea0c9-103">Szolgáltatáskérés részleteinek lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="ea0c9-103">Get service request details by ID</span></span>

<span data-ttu-id="ea0c9-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="ea0c9-104">**Applies To**</span></span>

- <span data-ttu-id="ea0c9-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="ea0c9-105">Partner Center</span></span>
- <span data-ttu-id="ea0c9-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="ea0c9-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ea0c9-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="ea0c9-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ea0c9-108">Egy meglévő ügyfél-szolgáltatási kérelem részleteinek beolvasása a szolgáltatási kérelem azonosítójának használatával.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-108">How to retrieve the details of an existing customer service request using the service request identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea0c9-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="ea0c9-109">Prerequisites</span></span>

- <span data-ttu-id="ea0c9-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ea0c9-111">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ea0c9-112">Egy szolgáltatási kérelem azonosítója.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-112">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="ea0c9-113">C\#</span><span class="sxs-lookup"><span data-stu-id="ea0c9-113">C\#</span></span>

<span data-ttu-id="ea0c9-114">Egy meglévő ügyfél-szolgáltatási kérelem részleteinek lekéréséhez hívja meg a [**IServiceRequestCollection. ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) metódust, és adjon meg egy [**ServiceRequest.id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) az adott [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) objektumhoz tartozó felület azonosításához és visszaküldéséhez.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-114">To retrieve the details of an existing customer service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method, and pass in a [**ServiceRequest.Id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) to identify and return an interface to the specific [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest as ServiceRequest;

ServiceRequest serviceRequestDetails = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Get();

Console.WriteLine(string.Format("The primary contact for the service request {0} is {1} {2}.",
    serviceRequestDetails.Title,
    serviceRequestDetails.PrimaryContact.FirstName,
    serviceRequestDetails.PrimaryContact.LastName,
));
```

## <a name="rest-request"></a><span data-ttu-id="ea0c9-115">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="ea0c9-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ea0c9-116">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="ea0c9-116">Request syntax</span></span>

| <span data-ttu-id="ea0c9-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="ea0c9-117">Method</span></span>    | <span data-ttu-id="ea0c9-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="ea0c9-118">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="ea0c9-119">**GET**</span><span class="sxs-lookup"><span data-stu-id="ea0c9-119">**GET**</span></span> | <span data-ttu-id="ea0c9-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{ServiceRequest-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="ea0c9-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="ea0c9-121">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="ea0c9-121">URI parameter</span></span>

<span data-ttu-id="ea0c9-122">A megadott Szolgáltatáskérelem beszerzéséhez használja a következő URI-paramétert.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-122">Use the following URI parameter to get the specified service request.</span></span>

| <span data-ttu-id="ea0c9-123">Név</span><span class="sxs-lookup"><span data-stu-id="ea0c9-123">Name</span></span>                  | <span data-ttu-id="ea0c9-124">Típus</span><span class="sxs-lookup"><span data-stu-id="ea0c9-124">Type</span></span>     | <span data-ttu-id="ea0c9-125">Kötelező</span><span class="sxs-lookup"><span data-stu-id="ea0c9-125">Required</span></span> | <span data-ttu-id="ea0c9-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="ea0c9-126">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="ea0c9-127">**ServiceRequest-azonosító**</span><span class="sxs-lookup"><span data-stu-id="ea0c9-127">**servicerequest-id**</span></span> | <span data-ttu-id="ea0c9-128">**guid**</span><span class="sxs-lookup"><span data-stu-id="ea0c9-128">**guid**</span></span> | <span data-ttu-id="ea0c9-129">Y</span><span class="sxs-lookup"><span data-stu-id="ea0c9-129">Y</span></span>        | <span data-ttu-id="ea0c9-130">A szolgáltatási kérelmet azonosító GUID.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-130">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ea0c9-131">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="ea0c9-131">Request headers</span></span>

<span data-ttu-id="ea0c9-132">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ea0c9-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ea0c9-133">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="ea0c9-133">Request body</span></span>

<span data-ttu-id="ea0c9-134">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ea0c9-135">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ea0c9-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="ea0c9-136">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="ea0c9-136">REST response</span></span>

<span data-ttu-id="ea0c9-137">Ha ez sikeres, ez a metódus egy **szolgáltatási kérelem** erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-137">If successful, this method returns a **Service Request** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ea0c9-138">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="ea0c9-138">Response success and error codes</span></span>

<span data-ttu-id="ea0c9-139">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ea0c9-140">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ea0c9-141">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-141">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ea0c9-142">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ea0c9-142">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 566
Content-Type: application/json; charset=utf-8
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CV: rjLONPum/Uq94UQA.0
MS-ServerId: 030011719
Date: Mon, 09 Jan 2017 23:31:15 GMT

{
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "supportTopicName": "Cannot manage my profile",
    "id": "616122292874576",
    "status": "open",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1"
    },
    "productId": "15960",
    "createdDate": "2016-12-22T20:31:17.24Z",
    "lastModifiedDate": "2017-01-09T23:31:15.373Z",
    "lastClosedDate": "0001-01-01T00:00:00",
    "notes": [{
            "createdByName": "Account",
            "createdDate": "2017-01-09T23:31:15.373",
            "text": "Sample Note"
        }
    ],
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```
