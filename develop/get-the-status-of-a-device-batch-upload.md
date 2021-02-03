---
title: Eszköz kötegelt feltöltési állapotának lekérése
description: Egy adott ügyfélhez tartozó Batch-feltöltés állapotának beolvasása.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fb887ba257d6fbe68f95ae4b59d701ac4c934860
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768404"
---
# <a name="get-the-status-of-a-device-batch-upload"></a><span data-ttu-id="5f03c-103">Eszköz kötegelt feltöltési állapotának lekérése</span><span class="sxs-lookup"><span data-stu-id="5f03c-103">Get the status of a device batch upload</span></span>

<span data-ttu-id="5f03c-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="5f03c-104">**Applies To**</span></span>

- <span data-ttu-id="5f03c-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="5f03c-105">Partner Center</span></span>
- <span data-ttu-id="5f03c-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5f03c-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="5f03c-107">Egy adott ügyfélhez tartozó Batch-feltöltés állapotának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="5f03c-107">How to get the status of a device batch upload for a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f03c-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5f03c-108">Prerequisites</span></span>

- <span data-ttu-id="5f03c-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="5f03c-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5f03c-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="5f03c-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5f03c-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5f03c-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5f03c-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="5f03c-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5f03c-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="5f03c-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5f03c-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="5f03c-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5f03c-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="5f03c-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5f03c-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5f03c-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5f03c-117">Az eszköz kötegének elküldésekor a hely fejlécében visszaadott batch követési azonosító.</span><span class="sxs-lookup"><span data-stu-id="5f03c-117">The batch tracking identifier returned in the Location header when the device batch was submitted.</span></span> <span data-ttu-id="5f03c-118">További információ: a [megadott ügyfélhez tartozó eszközök listájának feltöltése](upload-a-list-of-devices-for-the-specified-customer.md).</span><span class="sxs-lookup"><span data-stu-id="5f03c-118">For more information, see [Upload a list of devices for the specified customer](upload-a-list-of-devices-for-the-specified-customer.md).</span></span>

## <a name="c"></a><span data-ttu-id="5f03c-119">C\#</span><span class="sxs-lookup"><span data-stu-id="5f03c-119">C\#</span></span>

<span data-ttu-id="5f03c-120">Egy eszköz batch-feltöltési állapotának lekéréséhez először hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, hogy lekérje az adott ügyfélen végrehajtott műveletekhez szükséges felületet.</span><span class="sxs-lookup"><span data-stu-id="5f03c-120">To get the status of a device batch upload, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="5f03c-121">Ezután hívja meg a [**BatchUploadStatus. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) metódust a Batch Tracking ID-vel, és szerezzen be egy felületet a Batch feltöltési állapotának műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="5f03c-121">Then, call the [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) method with the batch tracking ID to get an interface to batch upload status operations.</span></span> <span data-ttu-id="5f03c-122">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) metódust az állapot lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="5f03c-122">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) method to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

<span data-ttu-id="5f03c-123">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5f03c-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5f03c-124">**Projekt**: partner Center SDK Samples **osztály**: GetBatchUploadStatus.cs</span><span class="sxs-lookup"><span data-stu-id="5f03c-124">**Project**: Partner Center SDK Samples **Class**: GetBatchUploadStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5f03c-125">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="5f03c-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5f03c-126">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5f03c-126">Request syntax</span></span>

| <span data-ttu-id="5f03c-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="5f03c-127">Method</span></span>  | <span data-ttu-id="5f03c-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5f03c-128">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5f03c-129">**GET**</span><span class="sxs-lookup"><span data-stu-id="5f03c-129">**GET**</span></span> | <span data-ttu-id="5f03c-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/batchJobStatus/{batchtracking-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="5f03c-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/batchJobStatus/{batchtracking-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5f03c-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="5f03c-131">URI parameter</span></span>

<span data-ttu-id="5f03c-132">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="5f03c-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="5f03c-133">Név</span><span class="sxs-lookup"><span data-stu-id="5f03c-133">Name</span></span>             | <span data-ttu-id="5f03c-134">Típus</span><span class="sxs-lookup"><span data-stu-id="5f03c-134">Type</span></span>   | <span data-ttu-id="5f03c-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5f03c-135">Required</span></span> | <span data-ttu-id="5f03c-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="5f03c-136">Description</span></span>                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5f03c-137">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="5f03c-137">customer-id</span></span>      | <span data-ttu-id="5f03c-138">sztring</span><span class="sxs-lookup"><span data-stu-id="5f03c-138">string</span></span> | <span data-ttu-id="5f03c-139">Igen</span><span class="sxs-lookup"><span data-stu-id="5f03c-139">Yes</span></span>      | <span data-ttu-id="5f03c-140">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="5f03c-140">A GUID-formatted string that identifies the customer.</span></span>                                                                                                                          |
| <span data-ttu-id="5f03c-141">batchtracking-azonosító</span><span class="sxs-lookup"><span data-stu-id="5f03c-141">batchtracking-id</span></span> | <span data-ttu-id="5f03c-142">sztring</span><span class="sxs-lookup"><span data-stu-id="5f03c-142">string</span></span> | <span data-ttu-id="5f03c-143">Igen</span><span class="sxs-lookup"><span data-stu-id="5f03c-143">Yes</span></span>      | <span data-ttu-id="5f03c-144">GUID-formázott azonosító, amely az eszköz batch-feltöltési állapotának lekérésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="5f03c-144">A GUID-formatted identifier that is used to retrieve a device batch upload status.</span></span> <span data-ttu-id="5f03c-145">A rendszer ezt az azonosítót adja vissza a Location (hely) fejlécben, amikor az eszköz kötege sikeresen elküldve.</span><span class="sxs-lookup"><span data-stu-id="5f03c-145">This ID is returned in the Location header when the device batch is successfully submitted.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5f03c-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5f03c-146">Request headers</span></span>

<span data-ttu-id="5f03c-147">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5f03c-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5f03c-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="5f03c-148">Request body</span></span>

<span data-ttu-id="5f03c-149">Nincs</span><span class="sxs-lookup"><span data-stu-id="5f03c-149">None</span></span>

### <a name="request-example"></a><span data-ttu-id="5f03c-150">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5f03c-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="5f03c-151">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5f03c-151">REST response</span></span>

<span data-ttu-id="5f03c-152">Ha ez sikeres, a válasz [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) -erőforrást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="5f03c-152">If successful, the response contains a [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5f03c-153">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5f03c-153">Response success and error codes</span></span>

<span data-ttu-id="5f03c-154">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="5f03c-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5f03c-155">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="5f03c-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5f03c-156">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="5f03c-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5f03c-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5f03c-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 400
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "batchTrackingId": "0127ed8e-ff72-4983-a3d8-e8d8bd378932",
    "status": "finished",
    "startedTime": "2017-07-25T10:00:00",
    "completedTime": "2017-07-25T10:10:00",
    "devicesStatus": [{
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "status": "finished_with_errors",
            "errorCode": "808",
            "errorDescription": "ZtdDeviceAssignedToOtherTenant",
            "attributes": {
                "objectType": "DeviceUploadDetails"
            }
        }
    ],
    "attributes": {
        "objectType": "BatchUploadDetails"
    }
}
```
