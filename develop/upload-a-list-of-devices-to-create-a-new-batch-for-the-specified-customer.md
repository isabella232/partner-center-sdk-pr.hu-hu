---
title: Eszközök listájának feltöltése új köteg a megadott ügyfél számára történő létrehozásához
description: Az eszközökre vonatkozó információk listájának feltöltése egy új köteg létrehozásához a megadott ügyfél számára. Ezzel létrehoz egy batch szolgáltatást a beléptetéshez a nulla érintéses telepítésben, és társítja az eszközöket és az eszköz kötegét a megadott ügyféllel.
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0b48971b862418136c42e78ae973a5aea27404a1
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768367"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a><span data-ttu-id="c77af-104">Eszközök listájának feltöltése új köteg a megadott ügyfél számára történő létrehozásához</span><span class="sxs-lookup"><span data-stu-id="c77af-104">Upload a list of devices to create a new batch for the specified customer</span></span>

<span data-ttu-id="c77af-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="c77af-105">**Applies to:**</span></span>

- <span data-ttu-id="c77af-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="c77af-106">Partner Center</span></span>
- <span data-ttu-id="c77af-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="c77af-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="c77af-108">Az eszközökre vonatkozó információk listájának feltöltése egy új köteg létrehozásához a megadott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="c77af-108">How to upload a list of information about devices to create a new batch for the specified customer.</span></span> <span data-ttu-id="c77af-109">Ezzel létrehoz egy batch szolgáltatást a beléptetéshez a nulla érintéses telepítésben, és társítja az eszközöket és az eszköz kötegét a megadott ügyféllel.</span><span class="sxs-lookup"><span data-stu-id="c77af-109">This creates a device batch for enrollment in zero-touch deployment, and associates the devices and the device batch with the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c77af-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c77af-110">Prerequisites</span></span>

- <span data-ttu-id="c77af-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="c77af-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c77af-112">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="c77af-112">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="c77af-113">Kövesse a [Secure app modelt](enable-secure-app-model.md) , ha app + felhasználói hitelesítést használ a partner Center API-kkal.</span><span class="sxs-lookup"><span data-stu-id="c77af-113">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="c77af-114">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c77af-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c77af-115">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="c77af-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c77af-116">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="c77af-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c77af-117">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="c77af-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c77af-118">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="c77af-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c77af-119">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c77af-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="c77af-120">Az egyes eszközökre vonatkozó információkat biztosító eszköz-erőforrások listája.</span><span class="sxs-lookup"><span data-stu-id="c77af-120">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="c77af-121">C\#</span><span class="sxs-lookup"><span data-stu-id="c77af-121">C\#</span></span>

<span data-ttu-id="c77af-122">Eszközök listájának feltöltése új eszköz köteg létrehozásához:</span><span class="sxs-lookup"><span data-stu-id="c77af-122">To upload a list of devices to create a new device batch:</span></span>

1. <span data-ttu-id="c77af-123">A rendszer létrehoz egy új [lista/DotNet/API/System. Collections. Generic. list -1) típusú [**eszközt**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) , és feltölti a listát az eszközökkel.</span><span class="sxs-lookup"><span data-stu-id="c77af-123">Instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="c77af-124">Az egyes eszközök azonosításához legalább az alábbi, feltöltött tulajdonságokat tartalmazó kombinációk szükségesek:</span><span class="sxs-lookup"><span data-stu-id="c77af-124">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

   - <span data-ttu-id="c77af-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Termék**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="c77af-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>
   - <span data-ttu-id="c77af-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="c77af-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="c77af-127">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Termék**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="c77af-127">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="c77af-128">Csak [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .</span><span class="sxs-lookup"><span data-stu-id="c77af-128">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>
   - <span data-ttu-id="c77af-129">Csak a [**termék**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .</span><span class="sxs-lookup"><span data-stu-id="c77af-129">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>
   - <span data-ttu-id="c77af-130">[**Serialnumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**Modelname**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="c77af-130">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

2. <span data-ttu-id="c77af-131">Hozzon létre egy [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) objektumot, és állítsa az [**kötegazonosító**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) tulajdonságot a választott egyedi névre, és az [**eszközök**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) tulajdonságot a feltölteni kívánt eszközök listájára.</span><span class="sxs-lookup"><span data-stu-id="c77af-131">Instantiate a [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) object and set the [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) property to a unique name of your choosing, and the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of devices to upload.</span></span>

3. <span data-ttu-id="c77af-132">Dolgozza fel az eszköz batch-létrehozási kérését úgy, hogy meghívja a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, hogy lekérje az adott ügyfélen végrehajtott műveletekhez tartozó felületet.</span><span class="sxs-lookup"><span data-stu-id="c77af-132">Process the device batch creation request by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span>

4. <span data-ttu-id="c77af-133">Hívja meg a [**DeviceBatches. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) metódust az eszköz batch-létrehozási kérésével a köteg létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="c77af-133">Call the [**DeviceBatches.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) method with the device batch creation request to create the batch.</span></span>

```csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash123",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "1R9-ZNP67"
    }
};

DeviceBatchCreationRequest
    newDeviceBatch = new DeviceBatchCreationRequest
{
    BatchId = "SDKTestDeviceBatch",
    Devices = devicesToBeUploaded
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Create(newDeviceBatch);
```

<span data-ttu-id="c77af-134">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c77af-134">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c77af-135">**Projekt**: partner Center SDK Samples **osztály**: CreateDeviceBatch.cs</span><span class="sxs-lookup"><span data-stu-id="c77af-135">**Project**: Partner Center SDK Samples **Class**: CreateDeviceBatch.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c77af-136">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="c77af-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c77af-137">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="c77af-137">Request syntax</span></span>

| <span data-ttu-id="c77af-138">Metódus</span><span class="sxs-lookup"><span data-stu-id="c77af-138">Method</span></span>   | <span data-ttu-id="c77af-139">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="c77af-139">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="c77af-140">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="c77af-140">**POST**</span></span> | <span data-ttu-id="c77af-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches http/1.1</span><span class="sxs-lookup"><span data-stu-id="c77af-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="c77af-142">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="c77af-142">URI parameter</span></span>

<span data-ttu-id="c77af-143">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="c77af-143">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="c77af-144">Név</span><span class="sxs-lookup"><span data-stu-id="c77af-144">Name</span></span>        | <span data-ttu-id="c77af-145">Típus</span><span class="sxs-lookup"><span data-stu-id="c77af-145">Type</span></span>   | <span data-ttu-id="c77af-146">Kötelező</span><span class="sxs-lookup"><span data-stu-id="c77af-146">Required</span></span> | <span data-ttu-id="c77af-147">Leírás</span><span class="sxs-lookup"><span data-stu-id="c77af-147">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="c77af-148">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="c77af-148">customer-id</span></span> | <span data-ttu-id="c77af-149">sztring</span><span class="sxs-lookup"><span data-stu-id="c77af-149">string</span></span> | <span data-ttu-id="c77af-150">Igen</span><span class="sxs-lookup"><span data-stu-id="c77af-150">Yes</span></span>      | <span data-ttu-id="c77af-151">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="c77af-151">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c77af-152">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="c77af-152">Request headers</span></span>

<span data-ttu-id="c77af-153">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c77af-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c77af-154">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="c77af-154">Request body</span></span>

<span data-ttu-id="c77af-155">A kérelem törzsének tartalmaznia kell egy [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="c77af-155">The request body must contain a [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="c77af-156">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="c77af-156">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
    "BatchId": "SDKTestDeviceBatch",
    "Devices": [{
            "Id": null,
            "SerialNumber": "1R9-ZNP67",
            "ProductKey": "00329-00000-0003-AA606",
            "HardwareHash": "DummyHash123",
            "Policies": null,
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DeviceBatchCreationRequest"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="c77af-157">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="c77af-157">REST response</span></span>

<span data-ttu-id="c77af-158">Ha a művelet sikeres, a válasz egy olyan **Location** fejlécet tartalmaz, amely rendelkezik egy URI-val, amely az eszköz feltöltési állapotának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="c77af-158">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="c77af-159">Mentse ezt az URI-t más kapcsolódó REST API-kkal való használatra.</span><span class="sxs-lookup"><span data-stu-id="c77af-159">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c77af-160">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="c77af-160">Response success and error codes</span></span>

<span data-ttu-id="c77af-161">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="c77af-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c77af-162">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="c77af-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c77af-163">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="c77af-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="c77af-164">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="c77af-164">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/beba2053-5401-46ff-9223-7e841ed78fbf
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2017 20:35:35 GMT
```
