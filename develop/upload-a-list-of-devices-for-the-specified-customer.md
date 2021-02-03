---
title: Eszközök listájának feltöltése a megadott ügyfél meglévő kötegére
description: Az eszközökre vonatkozó információk listájának feltöltése egy meglévő kötegre a megadott ügyfél esetében. Ezzel társítja az eszközöket egy már létrehozott eszköz-köteghez.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d01ac1a42c50416487167070be9d104562300baf
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768371"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a><span data-ttu-id="fbe38-104">Eszközök listájának feltöltése a megadott ügyfél meglévő kötegére</span><span class="sxs-lookup"><span data-stu-id="fbe38-104">Upload a list of devices to an existing batch for the specified customer</span></span>

<span data-ttu-id="fbe38-105">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="fbe38-105">**Applies To**</span></span>

- <span data-ttu-id="fbe38-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="fbe38-106">Partner Center</span></span>
- <span data-ttu-id="fbe38-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="fbe38-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="fbe38-108">Az eszközökre vonatkozó információk listájának feltöltése egy meglévő kötegre a megadott ügyfél esetében.</span><span class="sxs-lookup"><span data-stu-id="fbe38-108">How to upload a list of information about devices to an existing batch for the specified customer.</span></span> <span data-ttu-id="fbe38-109">Ezzel társítja az eszközöket egy már létrehozott eszköz-köteghez.</span><span class="sxs-lookup"><span data-stu-id="fbe38-109">This associates the devices with a device batch already created.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbe38-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="fbe38-110">Prerequisites</span></span>

- <span data-ttu-id="fbe38-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="fbe38-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fbe38-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="fbe38-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fbe38-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fbe38-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fbe38-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="fbe38-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fbe38-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="fbe38-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fbe38-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="fbe38-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fbe38-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="fbe38-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fbe38-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fbe38-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fbe38-119">Az eszköz batch-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="fbe38-119">The device batch identifier.</span></span>

- <span data-ttu-id="fbe38-120">Az egyes eszközökre vonatkozó információkat biztosító eszköz-erőforrások listája.</span><span class="sxs-lookup"><span data-stu-id="fbe38-120">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="fbe38-121">C\#</span><span class="sxs-lookup"><span data-stu-id="fbe38-121">C\#</span></span>

<span data-ttu-id="fbe38-122">Az eszközök listájának egy meglévő eszköz kötegbe való feltöltéséhez először létre kell vennie egy új [lista/DotNet/API/System. Collections. Generic. list -1) típusú [**eszközt**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) , és fel kell töltenie a listát az eszközökkel.</span><span class="sxs-lookup"><span data-stu-id="fbe38-122">To upload a list of devices to an existing device batch, first, instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="fbe38-123">Az egyes eszközök azonosításához legalább az alábbi, feltöltött tulajdonságokat tartalmazó kombinációk szükségesek:</span><span class="sxs-lookup"><span data-stu-id="fbe38-123">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

- <span data-ttu-id="fbe38-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Termék**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="fbe38-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>

- <span data-ttu-id="fbe38-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="fbe38-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="fbe38-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Termék**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="fbe38-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="fbe38-127">Csak [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .</span><span class="sxs-lookup"><span data-stu-id="fbe38-127">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>

- <span data-ttu-id="fbe38-128">Csak a [**termék**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .</span><span class="sxs-lookup"><span data-stu-id="fbe38-128">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>

- <span data-ttu-id="fbe38-129">[**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**Modelname**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="fbe38-129">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

<span data-ttu-id="fbe38-130">Ezután hívja meg a [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérje le a felületet a műveletekre a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="fbe38-130">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="fbe38-131">Ezután hívja meg a [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) metódust az eszköz batch-azonosítójával, és szerezzen be egy illesztőfelületet a megadott köteg műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="fbe38-131">Next, call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span> <span data-ttu-id="fbe38-132">Végül hívja meg az [**eszközöket. hozzon létre**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) vagy [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) metódust az eszközök listájával, és adja hozzá az eszközöket az eszköz kötegéhez.</span><span class="sxs-lookup"><span data-stu-id="fbe38-132">Finally, call the [**Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) method with the list of devices to add the devices to the device batch.</span></span>

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

<span data-ttu-id="fbe38-133">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fbe38-133">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fbe38-134">**Projekt**: partner Center SDK Samples **osztály**: CreateDevices.cs</span><span class="sxs-lookup"><span data-stu-id="fbe38-134">**Project**: Partner Center SDK Samples **Class**: CreateDevices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fbe38-135">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="fbe38-135">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fbe38-136">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="fbe38-136">Request syntax</span></span>

| <span data-ttu-id="fbe38-137">Metódus</span><span class="sxs-lookup"><span data-stu-id="fbe38-137">Method</span></span>   | <span data-ttu-id="fbe38-138">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="fbe38-138">Request URI</span></span>                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fbe38-139">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="fbe38-139">**POST**</span></span> | <span data-ttu-id="fbe38-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices http/1.1</span><span class="sxs-lookup"><span data-stu-id="fbe38-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fbe38-141">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="fbe38-141">URI parameter</span></span>

<span data-ttu-id="fbe38-142">A kérelem létrehozásakor használja az alábbi elérési utat és a lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="fbe38-142">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="fbe38-143">Név</span><span class="sxs-lookup"><span data-stu-id="fbe38-143">Name</span></span>           | <span data-ttu-id="fbe38-144">Típus</span><span class="sxs-lookup"><span data-stu-id="fbe38-144">Type</span></span>   | <span data-ttu-id="fbe38-145">Kötelező</span><span class="sxs-lookup"><span data-stu-id="fbe38-145">Required</span></span> | <span data-ttu-id="fbe38-146">Leírás</span><span class="sxs-lookup"><span data-stu-id="fbe38-146">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="fbe38-147">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="fbe38-147">customer-id</span></span>    | <span data-ttu-id="fbe38-148">sztring</span><span class="sxs-lookup"><span data-stu-id="fbe38-148">string</span></span> | <span data-ttu-id="fbe38-149">Igen</span><span class="sxs-lookup"><span data-stu-id="fbe38-149">Yes</span></span>      | <span data-ttu-id="fbe38-150">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="fbe38-150">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="fbe38-151">devicebatch-azonosító</span><span class="sxs-lookup"><span data-stu-id="fbe38-151">devicebatch-id</span></span> | <span data-ttu-id="fbe38-152">sztring</span><span class="sxs-lookup"><span data-stu-id="fbe38-152">string</span></span> | <span data-ttu-id="fbe38-153">Igen</span><span class="sxs-lookup"><span data-stu-id="fbe38-153">Yes</span></span>      | <span data-ttu-id="fbe38-154">Az eszköz kötegét azonosító karakterlánc-azonosító.</span><span class="sxs-lookup"><span data-stu-id="fbe38-154">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fbe38-155">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="fbe38-155">Request headers</span></span>

<span data-ttu-id="fbe38-156">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fbe38-156">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fbe38-157">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="fbe38-157">Request body</span></span>

<span data-ttu-id="fbe38-158">A kérelem törzsének tartalmaznia kell az [eszközbeállítások](device-deployment-resources.md#device) tömbjét.</span><span class="sxs-lookup"><span data-stu-id="fbe38-158">The request body must contain an array of [Device](device-deployment-resources.md#device) objects.</span></span> <span data-ttu-id="fbe38-159">Az eszközök azonosítására szolgáló mezők alábbi kombinációit fogadja el:</span><span class="sxs-lookup"><span data-stu-id="fbe38-159">The following combinations of fields for identifying a device are accepted:</span></span>

- <span data-ttu-id="fbe38-160">hardwareHash + termék.</span><span class="sxs-lookup"><span data-stu-id="fbe38-160">hardwareHash + productKey.</span></span>
- <span data-ttu-id="fbe38-161">hardwareHash + serialNumber.</span><span class="sxs-lookup"><span data-stu-id="fbe38-161">hardwareHash + serialNumber.</span></span>
- <span data-ttu-id="fbe38-162">hardwareHash + termék + serialNumber.</span><span class="sxs-lookup"><span data-stu-id="fbe38-162">hardwareHash + productKey + serialNumber.</span></span>
- <span data-ttu-id="fbe38-163">csak hardwareHash.</span><span class="sxs-lookup"><span data-stu-id="fbe38-163">hardwareHash only.</span></span>
- <span data-ttu-id="fbe38-164">csak a termék.</span><span class="sxs-lookup"><span data-stu-id="fbe38-164">productKey only.</span></span>
- <span data-ttu-id="fbe38-165">serialNumber + oemManufacturerName + modelName.</span><span class="sxs-lookup"><span data-stu-id="fbe38-165">serialNumber + oemManufacturerName + modelName.</span></span>

### <a name="request-example"></a><span data-ttu-id="fbe38-166">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="fbe38-166">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="fbe38-167">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="fbe38-167">REST response</span></span>

<span data-ttu-id="fbe38-168">Ha a művelet sikeres, a válasz egy olyan **Location** fejlécet tartalmaz, amely rendelkezik egy URI-val, amely az eszköz feltöltési állapotának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="fbe38-168">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="fbe38-169">Mentse ezt az URI-t más kapcsolódó REST API-kkal való használatra.</span><span class="sxs-lookup"><span data-stu-id="fbe38-169">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fbe38-170">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="fbe38-170">Response success and error codes</span></span>

<span data-ttu-id="fbe38-171">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="fbe38-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fbe38-172">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="fbe38-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fbe38-173">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="fbe38-173">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fbe38-174">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="fbe38-174">Response example</span></span>

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
