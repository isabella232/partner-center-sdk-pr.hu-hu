---
title: Szolgáltatáskérés frissítése
description: Egy meglévő ügyfélszolgálati kérelem frissítése, amelyet a felhőalapú megoldás szolgáltatója a Microsoftnál az ügyfél nevében nyújtott be.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1df0d1f5fa4630b346d1c8b9cffabb86ce34cfb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768368"
---
# <a name="update-a-service-request"></a><span data-ttu-id="c98ed-103">Szolgáltatáskérés frissítése</span><span class="sxs-lookup"><span data-stu-id="c98ed-103">Update a service request</span></span>

<span data-ttu-id="c98ed-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="c98ed-104">**Applies To**</span></span>

- <span data-ttu-id="c98ed-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="c98ed-105">Partner Center</span></span>
- <span data-ttu-id="c98ed-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="c98ed-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c98ed-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="c98ed-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c98ed-108">Egy meglévő ügyfélszolgálati kérelem frissítése, amelyet a felhőalapú megoldás szolgáltatója a Microsoftnál az ügyfél nevében nyújtott be.</span><span class="sxs-lookup"><span data-stu-id="c98ed-108">How to update an existing customer service request that a Cloud Solution Provider has filed with Microsoft on the customer's behalf.</span></span>

<span data-ttu-id="c98ed-109">A partner Center irányítópultján ezt a műveletet a [felhasználó kiválasztásával](get-a-customer-by-name.md)végezheti el.</span><span class="sxs-lookup"><span data-stu-id="c98ed-109">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="c98ed-110">Ezután válassza a **Service Management** elemet a bal oldali oldalsávon.</span><span class="sxs-lookup"><span data-stu-id="c98ed-110">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="c98ed-111">A **támogatási kérelmek** fejléc alatt válassza ki a szóban forgó szolgáltatási kérelmet.</span><span class="sxs-lookup"><span data-stu-id="c98ed-111">Under the **Support requests** header, select the service request in question.</span></span> <span data-ttu-id="c98ed-112">A befejezéshez végezze el a kívánt módosításokat a szolgáltatási kérelemben, majd válassza a **Küldés lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="c98ed-112">To finish, make the desired changes to the service request then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c98ed-113">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c98ed-113">Prerequisites</span></span>

- <span data-ttu-id="c98ed-114">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="c98ed-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c98ed-115">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="c98ed-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c98ed-116">Egy szolgáltatási kérelem azonosítója.</span><span class="sxs-lookup"><span data-stu-id="c98ed-116">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="c98ed-117">C\#</span><span class="sxs-lookup"><span data-stu-id="c98ed-117">C\#</span></span>

<span data-ttu-id="c98ed-118">Az ügyfél szolgáltatási kérelmének frissítéséhez hívja meg a [**IServiceRequestCollection. ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) metódust a szolgáltatási kérelem azonosítójával, és adja vissza a szolgáltatáskérelem felületét.</span><span class="sxs-lookup"><span data-stu-id="c98ed-118">To update a customer's service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method with the service request id to identify and return the service request interface.</span></span> <span data-ttu-id="c98ed-119">Ezután hívja meg a [**IServiceRequest. patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) vagy a [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) metódust a szolgáltatáskérelem frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="c98ed-119">Then call the [**IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) method to update the service request.</span></span> <span data-ttu-id="c98ed-120">A frissített értékek megadásához hozzon létre egy új, üres [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) objektumot, és csak a módosítani kívánt tulajdonságértékek legyenek beállítva.</span><span class="sxs-lookup"><span data-stu-id="c98ed-120">To provide the updated values, create a new, empty [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object and set only the property values that you want to change.</span></span> <span data-ttu-id="c98ed-121">Ezután adja át ezt az objektumot a patch vagy a PatchAsync metódus meghívásával.</span><span class="sxs-lookup"><span data-stu-id="c98ed-121">Then pass that object in the call to the Patch or PatchAsync method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

<span data-ttu-id="c98ed-122">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c98ed-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c98ed-123">**Projekt**: partner Center SDK Samples **osztály**: UpdatePartnerServiceRequest.cs</span><span class="sxs-lookup"><span data-stu-id="c98ed-123">**Project**: Partner Center SDK Samples **Class**: UpdatePartnerServiceRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c98ed-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="c98ed-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c98ed-125">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="c98ed-125">Request syntax</span></span>

| <span data-ttu-id="c98ed-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="c98ed-126">Method</span></span>    | <span data-ttu-id="c98ed-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="c98ed-127">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="c98ed-128">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="c98ed-128">**PATCH**</span></span> | <span data-ttu-id="c98ed-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{ServiceRequest-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c98ed-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="c98ed-130">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="c98ed-130">URI parameter</span></span>

<span data-ttu-id="c98ed-131">A szolgáltatási kérelem frissítéséhez használja a következő URI-paramétert.</span><span class="sxs-lookup"><span data-stu-id="c98ed-131">Use the following URI parameter to update the service request.</span></span>

| <span data-ttu-id="c98ed-132">Név</span><span class="sxs-lookup"><span data-stu-id="c98ed-132">Name</span></span>                  | <span data-ttu-id="c98ed-133">Típus</span><span class="sxs-lookup"><span data-stu-id="c98ed-133">Type</span></span>     | <span data-ttu-id="c98ed-134">Kötelező</span><span class="sxs-lookup"><span data-stu-id="c98ed-134">Required</span></span> | <span data-ttu-id="c98ed-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="c98ed-135">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="c98ed-136">**ServiceRequest-azonosító**</span><span class="sxs-lookup"><span data-stu-id="c98ed-136">**servicerequest-id**</span></span> | <span data-ttu-id="c98ed-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="c98ed-137">**guid**</span></span> | <span data-ttu-id="c98ed-138">Y</span><span class="sxs-lookup"><span data-stu-id="c98ed-138">Y</span></span>        | <span data-ttu-id="c98ed-139">A szolgáltatási kérelmet azonosító GUID.</span><span class="sxs-lookup"><span data-stu-id="c98ed-139">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c98ed-140">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="c98ed-140">Request headers</span></span>

<span data-ttu-id="c98ed-141">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c98ed-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c98ed-142">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="c98ed-142">Request body</span></span>

<span data-ttu-id="c98ed-143">A kérelem törzsének tartalmaznia kell egy [ServiceRequest](service-request-resources.md) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="c98ed-143">The request body should contain a [ServiceRequest](service-request-resources.md) resource.</span></span> <span data-ttu-id="c98ed-144">Az egyetlen szükséges érték a frissítendő.</span><span class="sxs-lookup"><span data-stu-id="c98ed-144">The only required values are those to be updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="c98ed-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="c98ed-145">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 508
Expect: 100-continue

{
    "Id": null,
    "Title": null,
    "Description": null,
    "Severity": "unknown",
    "SupportTopicId": null,
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": {
        "CreatedByName": null,
        "CreatedDate": null,
        "Text": "Sample Note"
    },
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="c98ed-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="c98ed-146">REST response</span></span>

<span data-ttu-id="c98ed-147">Ha ez sikeres, ez a metódus egy **Szolgáltatáskérelem** -erőforrást ad vissza, amely frissített tulajdonságokkal rendelkezik a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="c98ed-147">If successful, this method returns a **Service Request** resource with updated properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c98ed-148">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="c98ed-148">Response success and error codes</span></span>

<span data-ttu-id="c98ed-149">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="c98ed-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c98ed-150">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="c98ed-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c98ed-151">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="c98ed-151">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c98ed-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="c98ed-152">Response example</span></span>

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
