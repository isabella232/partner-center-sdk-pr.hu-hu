---
title: Eszköz kötegelt feltöltési állapotának lekérése
description: Eszköz kötegelt feltöltési állapotának lekért állapota egy adott ügyfél számára.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd8726af41fe4399797f39a0790cf962fde64acc
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548481"
---
# <a name="get-the-status-of-a-device-batch-upload"></a><span data-ttu-id="2e2f9-103">Eszköz kötegelt feltöltési állapotának lekérése</span><span class="sxs-lookup"><span data-stu-id="2e2f9-103">Get the status of a device batch upload</span></span>

<span data-ttu-id="2e2f9-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="2e2f9-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="2e2f9-105">Eszköz kötegelt feltöltési állapotának lekért állapota egy adott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="2e2f9-105">How to get the status of a device batch upload for a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e2f9-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2e2f9-106">Prerequisites</span></span>

- <span data-ttu-id="2e2f9-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2e2f9-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2e2f9-108">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="2e2f9-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2e2f9-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2e2f9-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2e2f9-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="2e2f9-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2e2f9-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="2e2f9-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2e2f9-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="2e2f9-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2e2f9-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="2e2f9-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2e2f9-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2e2f9-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2e2f9-115">A Hely fejlécben az eszközkötet beküldtekor visszaadott kötegkövetési azonosítót.</span><span class="sxs-lookup"><span data-stu-id="2e2f9-115">The batch tracking identifier returned in the Location header when the device batch was submitted.</span></span> <span data-ttu-id="2e2f9-116">További információ: [Eszközök listájának feltöltése a megadott ügyfél számára.](upload-a-list-of-devices-for-the-specified-customer.md)</span><span class="sxs-lookup"><span data-stu-id="2e2f9-116">For more information, see [Upload a list of devices for the specified customer](upload-a-list-of-devices-for-the-specified-customer.md).</span></span>

## <a name="c"></a><span data-ttu-id="2e2f9-117">C\#</span><span class="sxs-lookup"><span data-stu-id="2e2f9-117">C\#</span></span>

<span data-ttu-id="2e2f9-118">Az eszköz kötegelt feltöltési állapotának lekéréséhez először hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával, hogy lekérje a megadott ügyfél műveleteinek interfészét.</span><span class="sxs-lookup"><span data-stu-id="2e2f9-118">To get the status of a device batch upload, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="2e2f9-119">Ezután hívja meg a [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) metódust a kötegkövetési azonosítóval a kötegelt feltöltési állapotműveletek interfészének lehívása érdekében.</span><span class="sxs-lookup"><span data-stu-id="2e2f9-119">Then, call the [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) method with the batch tracking ID to get an interface to batch upload status operations.</span></span> <span data-ttu-id="2e2f9-120">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) vagy [**GetAsync metódust**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) az állapot lekéréshez.</span><span class="sxs-lookup"><span data-stu-id="2e2f9-120">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) method to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

<span data-ttu-id="2e2f9-121">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="2e2f9-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2e2f9-122">**Project**: Partnerközpont SDK **Osztály:** GetBatchUploadStatus.cs</span><span class="sxs-lookup"><span data-stu-id="2e2f9-122">**Project**: Partner Center SDK Samples **Class**: GetBatchUploadStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2e2f9-123">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="2e2f9-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2e2f9-124">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="2e2f9-124">Request syntax</span></span>

| <span data-ttu-id="2e2f9-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="2e2f9-125">Method</span></span>  | <span data-ttu-id="2e2f9-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2e2f9-126">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e2f9-127">**Kap**</span><span class="sxs-lookup"><span data-stu-id="2e2f9-127">**GET**</span></span> | <span data-ttu-id="2e2f9-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfél-azonosító}/batchJobStatus/{batchtracking-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2e2f9-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/batchJobStatus/{batchtracking-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2e2f9-129">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="2e2f9-129">URI parameter</span></span>

<span data-ttu-id="2e2f9-130">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="2e2f9-130">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="2e2f9-131">Név</span><span class="sxs-lookup"><span data-stu-id="2e2f9-131">Name</span></span>             | <span data-ttu-id="2e2f9-132">Típus</span><span class="sxs-lookup"><span data-stu-id="2e2f9-132">Type</span></span>   | <span data-ttu-id="2e2f9-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2e2f9-133">Required</span></span> | <span data-ttu-id="2e2f9-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="2e2f9-134">Description</span></span>                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e2f9-135">ügyfélazonosító</span><span class="sxs-lookup"><span data-stu-id="2e2f9-135">customer-id</span></span>      | <span data-ttu-id="2e2f9-136">sztring</span><span class="sxs-lookup"><span data-stu-id="2e2f9-136">string</span></span> | <span data-ttu-id="2e2f9-137">Igen</span><span class="sxs-lookup"><span data-stu-id="2e2f9-137">Yes</span></span>      | <span data-ttu-id="2e2f9-138">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="2e2f9-138">A GUID-formatted string that identifies the customer.</span></span>                                                                                                                          |
| <span data-ttu-id="2e2f9-139">batchtracking-id</span><span class="sxs-lookup"><span data-stu-id="2e2f9-139">batchtracking-id</span></span> | <span data-ttu-id="2e2f9-140">sztring</span><span class="sxs-lookup"><span data-stu-id="2e2f9-140">string</span></span> | <span data-ttu-id="2e2f9-141">Igen</span><span class="sxs-lookup"><span data-stu-id="2e2f9-141">Yes</span></span>      | <span data-ttu-id="2e2f9-142">Egy GUID formátumú azonosító, amely az eszközkötet feltöltési állapotának lekérésére használatos.</span><span class="sxs-lookup"><span data-stu-id="2e2f9-142">A GUID-formatted identifier that is used to retrieve a device batch upload status.</span></span> <span data-ttu-id="2e2f9-143">Ezt az azonosítót az eszközkötet sikeres beküldtekor a Hely fejlécben kell visszaadni.</span><span class="sxs-lookup"><span data-stu-id="2e2f9-143">This ID is returned in the Location header when the device batch is successfully submitted.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2e2f9-144">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2e2f9-144">Request headers</span></span>

<span data-ttu-id="2e2f9-145">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2e2f9-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2e2f9-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2e2f9-146">Request body</span></span>

<span data-ttu-id="2e2f9-147">None</span><span class="sxs-lookup"><span data-stu-id="2e2f9-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="2e2f9-148">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="2e2f9-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="2e2f9-149">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2e2f9-149">REST response</span></span>

<span data-ttu-id="2e2f9-150">Ha ez sikeres, a válasz tartalmaz egy [BatchUploadDetails erőforrást.](device-deployment-resources.md#batchuploaddetails)</span><span class="sxs-lookup"><span data-stu-id="2e2f9-150">If successful, the response contains a [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2e2f9-151">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2e2f9-151">Response success and error codes</span></span>

<span data-ttu-id="2e2f9-152">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="2e2f9-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2e2f9-153">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="2e2f9-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2e2f9-154">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2e2f9-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2e2f9-155">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2e2f9-155">Response example</span></span>

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
