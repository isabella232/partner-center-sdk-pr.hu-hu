---
title: Eszközök listájának feltöltése a megadott ügyfél meglévő kötegére
description: Az eszközökre vonatkozó információk listájának feltöltése egy meglévő kötegbe a megadott ügyfél számára. Ez egy már létrehozott eszközkötethez társítja az eszközöket.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3fa9cff39113130c54cecfaef1f8ca28e0ac5adf
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530310"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a><span data-ttu-id="ffc38-104">Eszközök listájának feltöltése a megadott ügyfél meglévő kötegére</span><span class="sxs-lookup"><span data-stu-id="ffc38-104">Upload a list of devices to an existing batch for the specified customer</span></span>

<span data-ttu-id="ffc38-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="ffc38-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="ffc38-106">Az eszközökre vonatkozó információk listájának feltöltése egy meglévő kötegbe a megadott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="ffc38-106">How to upload a list of information about devices to an existing batch for the specified customer.</span></span> <span data-ttu-id="ffc38-107">Ez egy már létrehozott eszközkötethez társítja az eszközöket.</span><span class="sxs-lookup"><span data-stu-id="ffc38-107">This associates the devices with a device batch already created.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffc38-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="ffc38-108">Prerequisites</span></span>

- <span data-ttu-id="ffc38-109">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ffc38-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ffc38-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="ffc38-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ffc38-111">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ffc38-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ffc38-112">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="ffc38-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ffc38-113">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="ffc38-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ffc38-114">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="ffc38-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ffc38-115">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="ffc38-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ffc38-116">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ffc38-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ffc38-117">Az eszköz kötegazonosítója.</span><span class="sxs-lookup"><span data-stu-id="ffc38-117">The device batch identifier.</span></span>

- <span data-ttu-id="ffc38-118">Az egyes eszközökre vonatkozó információkat szolgáltató eszközerőforrások listája.</span><span class="sxs-lookup"><span data-stu-id="ffc38-118">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="ffc38-119">C\#</span><span class="sxs-lookup"><span data-stu-id="ffc38-119">C\#</span></span>

<span data-ttu-id="ffc38-120">Az eszközök listájának meglévő eszközkötetre való feltöltéséhez először példányosítenie kell egy új [List/dotnet/api/system.collections.generic.list-1) típusú eszközt, és töltse fel a listát az eszközökkel. [](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device)</span><span class="sxs-lookup"><span data-stu-id="ffc38-120">To upload a list of devices to an existing device batch, first, instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="ffc38-121">Az egyes eszközök azonosításához legalább a következő tulajdonságkombinációk szükségesek:</span><span class="sxs-lookup"><span data-stu-id="ffc38-121">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

- <span data-ttu-id="ffc38-122">[**HardwareHash (Hardverhash)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey (Termékkulcs).**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)</span><span class="sxs-lookup"><span data-stu-id="ffc38-122">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>

- <span data-ttu-id="ffc38-123">[**HardwareHash (Hardverhash)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)( Sorozatszám).</span><span class="sxs-lookup"><span data-stu-id="ffc38-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="ffc38-124">[**HardwareHash (Hardverhash)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey (Termékkulcs)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)( Sorozatszám).</span><span class="sxs-lookup"><span data-stu-id="ffc38-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="ffc38-125">[**Csak HardverHash.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)</span><span class="sxs-lookup"><span data-stu-id="ffc38-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>

- <span data-ttu-id="ffc38-126">[**Csak ProductKey.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)</span><span class="sxs-lookup"><span data-stu-id="ffc38-126">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>

- <span data-ttu-id="ffc38-127">[**SerialNumber (Sorozatszám)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName ( Modellnév).**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname)</span><span class="sxs-lookup"><span data-stu-id="ffc38-127">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

<span data-ttu-id="ffc38-128">Ezután hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóval a megadott ügyfél műveleteinek interfészének lekérése érdekében.</span><span class="sxs-lookup"><span data-stu-id="ffc38-128">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="ffc38-129">Ezután hívja meg a [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) metódust az eszköz kötegazonosítójának használatával, hogy lekérte a megadott köteg műveleteinek interfészét.</span><span class="sxs-lookup"><span data-stu-id="ffc38-129">Next, call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span> <span data-ttu-id="ffc38-130">Végül hívja meg a [**Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) vagy [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) metódust az eszközök listájával, hogy hozzáadja az eszközöket az eszközkötemhez.</span><span class="sxs-lookup"><span data-stu-id="ffc38-130">Finally, call the [**Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) method with the list of devices to add the devices to the device batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash1234",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    },

    new Device
    {
        HardwareHash = "DummyHash12345",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    }
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Create(devicesToBeUploaded);
```

<span data-ttu-id="ffc38-131">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ffc38-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ffc38-132">**Project**: Partnerközpont SDK **Osztály:** CreateDevices.cs</span><span class="sxs-lookup"><span data-stu-id="ffc38-132">**Project**: Partner Center SDK Samples **Class**: CreateDevices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ffc38-133">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="ffc38-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ffc38-134">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="ffc38-134">Request syntax</span></span>

| <span data-ttu-id="ffc38-135">Metódus</span><span class="sxs-lookup"><span data-stu-id="ffc38-135">Method</span></span>   | <span data-ttu-id="ffc38-136">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="ffc38-136">Request URI</span></span>                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ffc38-137">**Post**</span><span class="sxs-lookup"><span data-stu-id="ffc38-137">**POST**</span></span> | <span data-ttu-id="ffc38-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ffc38-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ffc38-139">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="ffc38-139">URI parameter</span></span>

<span data-ttu-id="ffc38-140">A kérelem létrehozásakor használja a következő elérési utat és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="ffc38-140">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="ffc38-141">Név</span><span class="sxs-lookup"><span data-stu-id="ffc38-141">Name</span></span>           | <span data-ttu-id="ffc38-142">Típus</span><span class="sxs-lookup"><span data-stu-id="ffc38-142">Type</span></span>   | <span data-ttu-id="ffc38-143">Kötelező</span><span class="sxs-lookup"><span data-stu-id="ffc38-143">Required</span></span> | <span data-ttu-id="ffc38-144">Leírás</span><span class="sxs-lookup"><span data-stu-id="ffc38-144">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="ffc38-145">ügyfélazonosító</span><span class="sxs-lookup"><span data-stu-id="ffc38-145">customer-id</span></span>    | <span data-ttu-id="ffc38-146">sztring</span><span class="sxs-lookup"><span data-stu-id="ffc38-146">string</span></span> | <span data-ttu-id="ffc38-147">Igen</span><span class="sxs-lookup"><span data-stu-id="ffc38-147">Yes</span></span>      | <span data-ttu-id="ffc38-148">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="ffc38-148">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="ffc38-149">devicebatch-id</span><span class="sxs-lookup"><span data-stu-id="ffc38-149">devicebatch-id</span></span> | <span data-ttu-id="ffc38-150">sztring</span><span class="sxs-lookup"><span data-stu-id="ffc38-150">string</span></span> | <span data-ttu-id="ffc38-151">Igen</span><span class="sxs-lookup"><span data-stu-id="ffc38-151">Yes</span></span>      | <span data-ttu-id="ffc38-152">Az eszközkötetet azonosító sztringazonosító.</span><span class="sxs-lookup"><span data-stu-id="ffc38-152">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ffc38-153">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="ffc38-153">Request headers</span></span>

<span data-ttu-id="ffc38-154">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ffc38-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ffc38-155">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="ffc38-155">Request body</span></span>

<span data-ttu-id="ffc38-156">A kérelem törzsének eszközobjektumok [tömböt kell tartalmaznia.](device-deployment-resources.md#device)</span><span class="sxs-lookup"><span data-stu-id="ffc38-156">The request body must contain an array of [Device](device-deployment-resources.md#device) objects.</span></span> <span data-ttu-id="ffc38-157">Az eszköz azonosítására a következő mezőkombinációk fogadhatóak el:</span><span class="sxs-lookup"><span data-stu-id="ffc38-157">The following combinations of fields for identifying a device are accepted:</span></span>

- <span data-ttu-id="ffc38-158">hardwareHash + productKey.</span><span class="sxs-lookup"><span data-stu-id="ffc38-158">hardwareHash + productKey.</span></span>
- <span data-ttu-id="ffc38-159">hardwareHash + serialNumber.</span><span class="sxs-lookup"><span data-stu-id="ffc38-159">hardwareHash + serialNumber.</span></span>
- <span data-ttu-id="ffc38-160">hardwareHash + productKey + serialNumber.</span><span class="sxs-lookup"><span data-stu-id="ffc38-160">hardwareHash + productKey + serialNumber.</span></span>
- <span data-ttu-id="ffc38-161">csak hardwareHash.</span><span class="sxs-lookup"><span data-stu-id="ffc38-161">hardwareHash only.</span></span>
- <span data-ttu-id="ffc38-162">Csak productKey.</span><span class="sxs-lookup"><span data-stu-id="ffc38-162">productKey only.</span></span>
- <span data-ttu-id="ffc38-163">serialNumber + oemManufacturerName + modelName.</span><span class="sxs-lookup"><span data-stu-id="ffc38-163">serialNumber + oemManufacturerName + modelName.</span></span>

### <a name="request-example"></a><span data-ttu-id="ffc38-164">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ffc38-164">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches/Test/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 482
Expect: 100-continue

[{
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash1234",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }, {
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash12345",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }
]
```

## <a name="rest-response"></a><span data-ttu-id="ffc38-165">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="ffc38-165">REST response</span></span>

<span data-ttu-id="ffc38-166">Ha ez sikeres, a válasz tartalmaz egy **Location** fejlécet, amely rendelkezik egy URI-azonosítóval, amely az eszköz feltöltési állapotának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="ffc38-166">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="ffc38-167">Mentse ezt az URI-t a többi kapcsolódó REST API-val való használathoz.</span><span class="sxs-lookup"><span data-stu-id="ffc38-167">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ffc38-168">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="ffc38-168">Response success and error codes</span></span>

<span data-ttu-id="ffc38-169">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="ffc38-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ffc38-170">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="ffc38-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ffc38-171">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ffc38-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ffc38-172">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ffc38-172">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/16c00110-e79a-433d-aa28-f69dd60df671
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CV: OBkGN9pSN0a5xvua.0
MS-ServerId: 101112012
Date: Thu, 28 Sep 2017 20:08:46 GMT
```
