---
title: Szolgáltatáskérés frissítése
description: Egy meglévő ügyfélszolgálati kérelem frissítése, Felhőszolgáltató az ügyfél nevében nyújtott be egy kérelmet a Microsoftnak.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: efa7b2a98b6f95a763ca6e3811c43cc655c18e2b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530089"
---
# <a name="update-a-service-request"></a><span data-ttu-id="b170b-103">Szolgáltatáskérés frissítése</span><span class="sxs-lookup"><span data-stu-id="b170b-103">Update a service request</span></span>

<span data-ttu-id="b170b-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b170b-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b170b-105">Egy meglévő ügyfélszolgálati kérelem frissítése, Felhőszolgáltató az ügyfél nevében nyújtott be egy kérelmet a Microsoftnak.</span><span class="sxs-lookup"><span data-stu-id="b170b-105">How to update an existing customer service request that a Cloud Solution Provider has filed with Microsoft on the customer's behalf.</span></span>

<span data-ttu-id="b170b-106">A Partnerközpont a művelet végrehajtásához először ki kell [választania egy ügyfelet.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="b170b-106">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="b170b-107">Ezután válassza a **Szolgáltatáskezelés lehetőséget** a bal oldali oldalsávon.</span><span class="sxs-lookup"><span data-stu-id="b170b-107">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="b170b-108">A Támogatási **kérelmek fejléc alatt** válassza ki a kérdéses szolgáltatáskérést.</span><span class="sxs-lookup"><span data-stu-id="b170b-108">Under the **Support requests** header, select the service request in question.</span></span> <span data-ttu-id="b170b-109">A befejezéshez módosításokat kell végeznie a szolgáltatáskérésen, majd válassza a Küldés **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="b170b-109">To finish, make the desired changes to the service request then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b170b-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b170b-110">Prerequisites</span></span>

- <span data-ttu-id="b170b-111">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b170b-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b170b-112">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="b170b-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b170b-113">Egy szolgáltatáskérés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="b170b-113">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="b170b-114">C\#</span><span class="sxs-lookup"><span data-stu-id="b170b-114">C\#</span></span>

<span data-ttu-id="b170b-115">Az ügyfél szolgáltatáskérésének frissítéséhez hívja meg az [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) metódust a szolgáltatáskérés azonosítójával, hogy azonosítsa és visszaadja a szolgáltatáskérési felületet.</span><span class="sxs-lookup"><span data-stu-id="b170b-115">To update a customer's service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method with the service request ID to identify and return the service request interface.</span></span> <span data-ttu-id="b170b-116">Ezután hívja meg az [**IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) vagy [**a PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) metódust a szolgáltatáskérés frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="b170b-116">Then call the [**IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) method to update the service request.</span></span> <span data-ttu-id="b170b-117">A frissített értékekhez hozzon létre egy új, üres [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) objektumot, és csak a módosítani kívánt tulajdonságértékeket állítsa be.</span><span class="sxs-lookup"><span data-stu-id="b170b-117">To provide the updated values, create a new, empty [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object and set only the property values that you want to change.</span></span> <span data-ttu-id="b170b-118">Ezután adja át ezt az objektumot a Patch vagy PatchAsync metódus hívásában.</span><span class="sxs-lookup"><span data-stu-id="b170b-118">Then pass that object in the call to the Patch or PatchAsync method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

<span data-ttu-id="b170b-119">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="b170b-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b170b-120">**Project**: Partnerközpont SDK **osztály:** UpdatePartnerServiceRequest.cs</span><span class="sxs-lookup"><span data-stu-id="b170b-120">**Project**: Partner Center SDK Samples **Class**: UpdatePartnerServiceRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b170b-121">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="b170b-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b170b-122">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b170b-122">Request syntax</span></span>

| <span data-ttu-id="b170b-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="b170b-123">Method</span></span>    | <span data-ttu-id="b170b-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b170b-124">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="b170b-125">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="b170b-125">**PATCH**</span></span> | <span data-ttu-id="b170b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b170b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b170b-127">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="b170b-127">URI parameter</span></span>

<span data-ttu-id="b170b-128">A szolgáltatáskérés frissítéséhez használja a következő URI-paramétert.</span><span class="sxs-lookup"><span data-stu-id="b170b-128">Use the following URI parameter to update the service request.</span></span>

| <span data-ttu-id="b170b-129">Név</span><span class="sxs-lookup"><span data-stu-id="b170b-129">Name</span></span>                  | <span data-ttu-id="b170b-130">Típus</span><span class="sxs-lookup"><span data-stu-id="b170b-130">Type</span></span>     | <span data-ttu-id="b170b-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b170b-131">Required</span></span> | <span data-ttu-id="b170b-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="b170b-132">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="b170b-133">**servicerequest-id**</span><span class="sxs-lookup"><span data-stu-id="b170b-133">**servicerequest-id**</span></span> | <span data-ttu-id="b170b-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="b170b-134">**guid**</span></span> | <span data-ttu-id="b170b-135">Y</span><span class="sxs-lookup"><span data-stu-id="b170b-135">Y</span></span>        | <span data-ttu-id="b170b-136">A szolgáltatáskérést azonosító GUID.</span><span class="sxs-lookup"><span data-stu-id="b170b-136">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b170b-137">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b170b-137">Request headers</span></span>

<span data-ttu-id="b170b-138">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b170b-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b170b-139">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b170b-139">Request body</span></span>

<span data-ttu-id="b170b-140">A kérelem törzsének tartalmaznia kell egy [ServiceRequest erőforrást.](service-request-resources.md)</span><span class="sxs-lookup"><span data-stu-id="b170b-140">The request body should contain a [ServiceRequest](service-request-resources.md) resource.</span></span> <span data-ttu-id="b170b-141">Az egyetlen kötelező érték a frissíthető érték.</span><span class="sxs-lookup"><span data-stu-id="b170b-141">The only required values are those to be updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="b170b-142">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b170b-142">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b170b-143">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b170b-143">REST response</span></span>

<span data-ttu-id="b170b-144">Ha a művelet sikeres, ez a metódus egy **szolgáltatáskérési** erőforrást ad vissza, amely frissített tulajdonságokkal rendelkezik a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="b170b-144">If successful, this method returns a **Service Request** resource with updated properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b170b-145">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b170b-145">Response success and error codes</span></span>

<span data-ttu-id="b170b-146">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="b170b-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b170b-147">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="b170b-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b170b-148">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b170b-148">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b170b-149">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b170b-149">Response example</span></span>

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
