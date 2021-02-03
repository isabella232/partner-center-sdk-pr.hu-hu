---
title: A megadott köteg és ügyfél eszközlistájának lekérése
description: Eszközök és eszközök részleteinek beolvasása a megadott eszköz-kötegben az ügyfelek számára.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 36fe3b97612adfd26c1b498f31b90f743bf774cb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768240"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a><span data-ttu-id="f9617-103">A megadott köteg és ügyfél eszközlistájának lekérése</span><span class="sxs-lookup"><span data-stu-id="f9617-103">Get a list of devices for the specified batch and customer</span></span>

<span data-ttu-id="f9617-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="f9617-104">**Applies to:**</span></span>

- <span data-ttu-id="f9617-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f9617-105">Partner Center</span></span>
- <span data-ttu-id="f9617-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f9617-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="f9617-107">Ez a cikk azt ismerteti, hogyan kérhető le egy adott eszközhöz tartozó eszközök gyűjteménye egy adott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="f9617-107">This article describes how to retrieve a collection of devices in a specified device batch for a specified customer.</span></span> <span data-ttu-id="f9617-108">Minden eszköz erőforrása az eszköz részletes adatait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="f9617-108">Each device resource contains details about the device.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9617-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f9617-109">Prerequisites</span></span>

- <span data-ttu-id="f9617-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="f9617-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f9617-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="f9617-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f9617-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f9617-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f9617-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="f9617-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f9617-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="f9617-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f9617-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="f9617-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f9617-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="f9617-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f9617-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f9617-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f9617-118">Egy eszköz batch-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="f9617-118">A device batch identifier.</span></span>

## <a name="c"></a><span data-ttu-id="f9617-119">C\#</span><span class="sxs-lookup"><span data-stu-id="f9617-119">C\#</span></span>

<span data-ttu-id="f9617-120">Az eszközök gyűjteményének lekérése egy megadott eszköz-kötegben a megadott ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="f9617-120">To retrieve a collection of the devices in a specified device batch for the specified customer:</span></span>

1. <span data-ttu-id="f9617-121">Hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérje le a felületet a műveletekre a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="f9617-121">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="f9617-122">Hívja meg a [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) metódust, hogy lekérje a megadott kötegre vonatkozó illesztőfelületet az eszköz batch-gyűjtési műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="f9617-122">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method to get an interface to device batch collection operations for the specified batch.</span></span>

3. <span data-ttu-id="f9617-123">Kérje le az [**Devices (eszközök**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) ) tulajdonságot, és kérje meg, hogy csatolja a köteg eszköz-gyűjtemény műveleteit.</span><span class="sxs-lookup"><span data-stu-id="f9617-123">Retrieve the [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) property to get an interface to device collection operations for the batch.</span></span>

4. <span data-ttu-id="f9617-124">Az eszközök gyűjteményének lekéréséhez hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="f9617-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) method to retrieve the collection of devices.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

<span data-ttu-id="f9617-125">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="f9617-125">For an example, see the following:</span></span>

- <span data-ttu-id="f9617-126">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f9617-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="f9617-127">Projekt: **partner Center SDK-minták**</span><span class="sxs-lookup"><span data-stu-id="f9617-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="f9617-128">Osztály: **GetDevices.cs**</span><span class="sxs-lookup"><span data-stu-id="f9617-128">Class: **GetDevices.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="f9617-129">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="f9617-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f9617-130">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f9617-130">Request syntax</span></span>

| <span data-ttu-id="f9617-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="f9617-131">Method</span></span>  | <span data-ttu-id="f9617-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f9617-132">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f9617-133">**GET**</span><span class="sxs-lookup"><span data-stu-id="f9617-133">**GET**</span></span> | <span data-ttu-id="f9617-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices http/1.1</span><span class="sxs-lookup"><span data-stu-id="f9617-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="f9617-135">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="f9617-135">URI parameters</span></span>

<span data-ttu-id="f9617-136">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="f9617-136">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="f9617-137">Név</span><span class="sxs-lookup"><span data-stu-id="f9617-137">Name</span></span>           | <span data-ttu-id="f9617-138">Típus</span><span class="sxs-lookup"><span data-stu-id="f9617-138">Type</span></span>   | <span data-ttu-id="f9617-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f9617-139">Required</span></span> | <span data-ttu-id="f9617-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="f9617-140">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="f9617-141">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="f9617-141">customer-id</span></span>    | <span data-ttu-id="f9617-142">sztring</span><span class="sxs-lookup"><span data-stu-id="f9617-142">string</span></span> | <span data-ttu-id="f9617-143">Igen</span><span class="sxs-lookup"><span data-stu-id="f9617-143">Yes</span></span>      | <span data-ttu-id="f9617-144">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="f9617-144">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="f9617-145">devicebatch-azonosító</span><span class="sxs-lookup"><span data-stu-id="f9617-145">devicebatch-id</span></span> | <span data-ttu-id="f9617-146">sztring</span><span class="sxs-lookup"><span data-stu-id="f9617-146">string</span></span> | <span data-ttu-id="f9617-147">Igen</span><span class="sxs-lookup"><span data-stu-id="f9617-147">Yes</span></span>      | <span data-ttu-id="f9617-148">Az eszköz kötegét azonosító karakterlánc-azonosító.</span><span class="sxs-lookup"><span data-stu-id="f9617-148">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f9617-149">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f9617-149">Request headers</span></span>

<span data-ttu-id="f9617-150">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f9617-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f9617-151">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f9617-151">Request body</span></span>

<span data-ttu-id="f9617-152">Nincs</span><span class="sxs-lookup"><span data-stu-id="f9617-152">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f9617-153">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f9617-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f9617-154">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f9617-154">REST response</span></span>

<span data-ttu-id="f9617-155">Ha ez sikeres, a válasz törzse az [eszköz](device-deployment-resources.md#device) erőforrásainak lapozható gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="f9617-155">If successful, the response body contains a paged collection of [Device](device-deployment-resources.md#device) resources.</span></span> <span data-ttu-id="f9617-156">A gyűjtemény 100 eszközt tartalmaz egy oldalon.</span><span class="sxs-lookup"><span data-stu-id="f9617-156">The collection contains 100 devices in a page.</span></span> <span data-ttu-id="f9617-157">Az 100-es eszközök következő oldalának lekéréséhez a Continuationtoken argumentumot használja található MS-ContinuationToken-fejlécnek szerepelnie kell a következő kérelemben.</span><span class="sxs-lookup"><span data-stu-id="f9617-157">To retrieve the next page of 100 devices, the continuationToken in the response body must be included in the subsequent request as an MS-ContinuationToken header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f9617-158">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f9617-158">Response success and error codes</span></span>

<span data-ttu-id="f9617-159">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="f9617-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f9617-160">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="f9617-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f9617-161">Teljes listát a következő témakörben talál: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="f9617-161">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f9617-162">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f9617-162">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1742
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 2,
    "items":
    [{
            "id": "7c141ea9-2816-4e15-a819-53f6856499ff",
            "serialNumber": "2R9-ZNP67",
            "productKey": "00329-00000-0003-AA6069",
            "modelName": "Precision WorkStation T7500",
            "oemManufacturerName":"Dell Inc.",
            "policies":[{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate":"2017-08-09T14:43:26.0092288-07:00",
            " attributes": {
                "objectType": "Device"
            }
        }, {
            "id": "e528a62f-5031-49f4-bea7-5fafe47388fd",
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "modelName": "HP Z420 Workstation",
            "oemManufacturerName": "Hewlett-Packard",
            "policies": [{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate": "2017-08-09T14:35:51.3126144-07:00",
            "attributes": {
                "objectType": "Device"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
