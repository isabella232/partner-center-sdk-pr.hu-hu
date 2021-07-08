---
title: Szolgáltatáskérési adatok lekérése azonosító alapján.
description: Egy meglévő ügyfélszolgálati kérelem részleteinek lekérése azonosító alapján.
ms.date: 02/06/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 66488cf9592d630cb1f0237d379e8df5ead6a3a8
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548770"
---
# <a name="get-service-request-details-by-id"></a><span data-ttu-id="4fc2d-103">Szolgáltatáskérés részleteinek lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="4fc2d-103">Get service request details by ID</span></span>

<span data-ttu-id="4fc2d-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4fc2d-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4fc2d-105">Meglévő ügyfélszolgálati kérelem részleteinek lekérése a szolgáltatáskérés azonosítójának használatával.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-105">How to retrieve the details of an existing customer service request using the service request identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fc2d-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4fc2d-106">Prerequisites</span></span>

- <span data-ttu-id="4fc2d-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4fc2d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4fc2d-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4fc2d-109">Egy szolgáltatáskérés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-109">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="4fc2d-110">C\#</span><span class="sxs-lookup"><span data-stu-id="4fc2d-110">C\#</span></span>

<span data-ttu-id="4fc2d-111">Egy meglévő ügyfélszolgálati kérelem részleteinek lekéréshez hívja meg az [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) metódust, és adja át a [**ServiceRequest.Id-t**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) az adott [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) objektum azonosításához és az ahhoz való visszaküldéshez.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-111">To retrieve the details of an existing customer service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method, and pass in a [**ServiceRequest.Id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) to identify and return an interface to the specific [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="4fc2d-112">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="4fc2d-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4fc2d-113">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4fc2d-113">Request syntax</span></span>

| <span data-ttu-id="4fc2d-114">Metódus</span><span class="sxs-lookup"><span data-stu-id="4fc2d-114">Method</span></span>    | <span data-ttu-id="4fc2d-115">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4fc2d-115">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="4fc2d-116">**Kap**</span><span class="sxs-lookup"><span data-stu-id="4fc2d-116">**GET**</span></span> | <span data-ttu-id="4fc2d-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4fc2d-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="4fc2d-118">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="4fc2d-118">URI parameter</span></span>

<span data-ttu-id="4fc2d-119">A megadott szolgáltatáskérés lekéréshez használja a következő URI-paramétert.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-119">Use the following URI parameter to get the specified service request.</span></span>

| <span data-ttu-id="4fc2d-120">Név</span><span class="sxs-lookup"><span data-stu-id="4fc2d-120">Name</span></span>                  | <span data-ttu-id="4fc2d-121">Típus</span><span class="sxs-lookup"><span data-stu-id="4fc2d-121">Type</span></span>     | <span data-ttu-id="4fc2d-122">Kötelező</span><span class="sxs-lookup"><span data-stu-id="4fc2d-122">Required</span></span> | <span data-ttu-id="4fc2d-123">Leírás</span><span class="sxs-lookup"><span data-stu-id="4fc2d-123">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="4fc2d-124">**servicerequest-id**</span><span class="sxs-lookup"><span data-stu-id="4fc2d-124">**servicerequest-id**</span></span> | <span data-ttu-id="4fc2d-125">**guid**</span><span class="sxs-lookup"><span data-stu-id="4fc2d-125">**guid**</span></span> | <span data-ttu-id="4fc2d-126">Y</span><span class="sxs-lookup"><span data-stu-id="4fc2d-126">Y</span></span>        | <span data-ttu-id="4fc2d-127">A szolgáltatáskérést azonosító GUID.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-127">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4fc2d-128">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4fc2d-128">Request headers</span></span>

<span data-ttu-id="4fc2d-129">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4fc2d-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4fc2d-130">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="4fc2d-130">Request body</span></span>

<span data-ttu-id="4fc2d-131">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4fc2d-132">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4fc2d-132">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="4fc2d-133">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4fc2d-133">REST response</span></span>

<span data-ttu-id="4fc2d-134">Ha a művelet sikeres, ez a metódus egy **szolgáltatáskérési** erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-134">If successful, this method returns a **Service Request** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4fc2d-135">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4fc2d-135">Response success and error codes</span></span>

<span data-ttu-id="4fc2d-136">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4fc2d-137">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4fc2d-138">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="4fc2d-138">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4fc2d-139">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4fc2d-139">Response example</span></span>

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
