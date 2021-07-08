---
title: A megadott köteg és ügyfél eszközlistájának lekérése
description: Eszközök és eszközadatok gyűjteményének lekérése az ügyfél számára a megadott eszközkötetben.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 28af1f568f755ba4c50cfac21529d6c677656c8e
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874261"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a><span data-ttu-id="5812e-103">A megadott köteg és ügyfél eszközlistájának lekérése</span><span class="sxs-lookup"><span data-stu-id="5812e-103">Get a list of devices for the specified batch and customer</span></span>

<span data-ttu-id="5812e-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="5812e-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="5812e-105">Ez a cikk azt ismerteti, hogyan lehet lekérni egy adott eszközkötetben található eszközgyűjteményt egy adott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="5812e-105">This article describes how to retrieve a collection of devices in a specified device batch for a specified customer.</span></span> <span data-ttu-id="5812e-106">Minden eszközerőforrás az eszköz adatait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="5812e-106">Each device resource contains details about the device.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5812e-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5812e-107">Prerequisites</span></span>

- <span data-ttu-id="5812e-108">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5812e-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5812e-109">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="5812e-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5812e-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5812e-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5812e-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="5812e-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5812e-112">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="5812e-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5812e-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="5812e-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5812e-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="5812e-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5812e-115">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5812e-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5812e-116">Egy eszközkötet-azonosító.</span><span class="sxs-lookup"><span data-stu-id="5812e-116">A device batch identifier.</span></span>

## <a name="c"></a><span data-ttu-id="5812e-117">C\#</span><span class="sxs-lookup"><span data-stu-id="5812e-117">C\#</span></span>

<span data-ttu-id="5812e-118">Egy adott eszközkötetben található eszközök gyűjteményének lekérése a megadott ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="5812e-118">To retrieve a collection of the devices in a specified device batch for the specified customer:</span></span>

1. <span data-ttu-id="5812e-119">Hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával, hogy lekérje a műveletek interfészét a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="5812e-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="5812e-120">A [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) metódus hívásával lekért egy interfészt az eszközkötet-gyűjtési műveletekhez a megadott köteghez.</span><span class="sxs-lookup"><span data-stu-id="5812e-120">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method to get an interface to device batch collection operations for the specified batch.</span></span>

3. <span data-ttu-id="5812e-121">Az [**Eszközök tulajdonság lekérésével**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) illesztőfelületet kap a köteg eszközgyűjteményi műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="5812e-121">Retrieve the [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) property to get an interface to device collection operations for the batch.</span></span>

4. <span data-ttu-id="5812e-122">Az eszközök [**gyűjteményének**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) lekéréséhez hívja meg a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="5812e-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) method to retrieve the collection of devices.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

<span data-ttu-id="5812e-123">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="5812e-123">For an example, see the following:</span></span>

- <span data-ttu-id="5812e-124">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="5812e-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="5812e-125">Project: **Partnerközpont SDK minták**</span><span class="sxs-lookup"><span data-stu-id="5812e-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="5812e-126">Osztály: **GetDevices.cs**</span><span class="sxs-lookup"><span data-stu-id="5812e-126">Class: **GetDevices.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="5812e-127">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="5812e-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5812e-128">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5812e-128">Request syntax</span></span>

| <span data-ttu-id="5812e-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="5812e-129">Method</span></span>  | <span data-ttu-id="5812e-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5812e-130">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5812e-131">**Kap**</span><span class="sxs-lookup"><span data-stu-id="5812e-131">**GET**</span></span> | <span data-ttu-id="5812e-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5812e-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="5812e-133">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="5812e-133">URI parameters</span></span>

<span data-ttu-id="5812e-134">A kérelem létrehozásakor használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="5812e-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="5812e-135">Név</span><span class="sxs-lookup"><span data-stu-id="5812e-135">Name</span></span>           | <span data-ttu-id="5812e-136">Típus</span><span class="sxs-lookup"><span data-stu-id="5812e-136">Type</span></span>   | <span data-ttu-id="5812e-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5812e-137">Required</span></span> | <span data-ttu-id="5812e-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="5812e-138">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="5812e-139">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="5812e-139">customer-id</span></span>    | <span data-ttu-id="5812e-140">sztring</span><span class="sxs-lookup"><span data-stu-id="5812e-140">string</span></span> | <span data-ttu-id="5812e-141">Igen</span><span class="sxs-lookup"><span data-stu-id="5812e-141">Yes</span></span>      | <span data-ttu-id="5812e-142">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="5812e-142">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="5812e-143">devicebatch-id</span><span class="sxs-lookup"><span data-stu-id="5812e-143">devicebatch-id</span></span> | <span data-ttu-id="5812e-144">sztring</span><span class="sxs-lookup"><span data-stu-id="5812e-144">string</span></span> | <span data-ttu-id="5812e-145">Igen</span><span class="sxs-lookup"><span data-stu-id="5812e-145">Yes</span></span>      | <span data-ttu-id="5812e-146">Az eszközkötetet azonosító sztringazonosító.</span><span class="sxs-lookup"><span data-stu-id="5812e-146">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5812e-147">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5812e-147">Request headers</span></span>

<span data-ttu-id="5812e-148">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5812e-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5812e-149">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="5812e-149">Request body</span></span>

<span data-ttu-id="5812e-150">None</span><span class="sxs-lookup"><span data-stu-id="5812e-150">None</span></span>

### <a name="request-example"></a><span data-ttu-id="5812e-151">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5812e-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="5812e-152">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5812e-152">REST response</span></span>

<span data-ttu-id="5812e-153">Ha a művelet sikeres, a válasz törzse az eszközerőforrások [lapszámált gyűjteményét](device-deployment-resources.md#device) tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="5812e-153">If successful, the response body contains a paged collection of [Device](device-deployment-resources.md#device) resources.</span></span> <span data-ttu-id="5812e-154">A gyűjtemény 100 eszközt tartalmaz egy oldalon.</span><span class="sxs-lookup"><span data-stu-id="5812e-154">The collection contains 100 devices in a page.</span></span> <span data-ttu-id="5812e-155">A 100 eszköz következő oldalának lekéréséhez a válasz törzsében szereplő continuationToken-nek szerepelnie kell a következő kérelemben MS-ContinuationToken fejlécként.</span><span class="sxs-lookup"><span data-stu-id="5812e-155">To retrieve the next page of 100 devices, the continuationToken in the response body must be included in the subsequent request as an MS-ContinuationToken header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5812e-156">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5812e-156">Response success and error codes</span></span>

<span data-ttu-id="5812e-157">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="5812e-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5812e-158">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="5812e-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5812e-159">A teljes listát a REST Partnerközpont [hibakódokat.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="5812e-159">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5812e-160">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5812e-160">Response example</span></span>

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
