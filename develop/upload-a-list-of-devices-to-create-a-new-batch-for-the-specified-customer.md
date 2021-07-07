---
title: Eszközök listájának feltöltése új köteg a megadott ügyfél számára történő létrehozásához
description: Az eszközökre vonatkozó információk listájának feltöltése új köteg létrehozásához a megadott ügyfél számára. Ez létrehoz egy eszközkötetet a regisztrációhoz érintés nélküli üzembe helyezéshez, és hozzárendeli az eszközöket és az eszközkötetet a megadott ügyfélhez.
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 285af12034562262c99b2aa3b139e948b0fdd462
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529732"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a><span data-ttu-id="14fe2-104">Eszközök listájának feltöltése új köteg a megadott ügyfél számára történő létrehozásához</span><span class="sxs-lookup"><span data-stu-id="14fe2-104">Upload a list of devices to create a new batch for the specified customer</span></span>

<span data-ttu-id="14fe2-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="14fe2-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="14fe2-106">Az eszközökre vonatkozó információk listájának feltöltése új köteg létrehozásához a megadott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="14fe2-106">How to upload a list of information about devices to create a new batch for the specified customer.</span></span> <span data-ttu-id="14fe2-107">Ez létrehoz egy eszközkötetet a regisztrációhoz érintés nélküli üzembe helyezéshez, és hozzárendeli az eszközöket és az eszközkötetet a megadott ügyfélhez.</span><span class="sxs-lookup"><span data-stu-id="14fe2-107">This creates a device batch for enrollment in zero-touch deployment, and associates the devices and the device batch with the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14fe2-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="14fe2-108">Prerequisites</span></span>

- <span data-ttu-id="14fe2-109">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="14fe2-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="14fe2-110">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="14fe2-110">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="14fe2-111">Kövesse a [biztonságos alkalmazásmodellt,](enable-secure-app-model.md) ha App+User hitelesítést használ Partnerközpont API-okkal.</span><span class="sxs-lookup"><span data-stu-id="14fe2-111">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="14fe2-112">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="14fe2-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="14fe2-113">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="14fe2-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="14fe2-114">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="14fe2-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="14fe2-115">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="14fe2-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="14fe2-116">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="14fe2-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="14fe2-117">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="14fe2-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="14fe2-118">Az egyes eszközökre vonatkozó információkat szolgáltató eszközerőforrások listája.</span><span class="sxs-lookup"><span data-stu-id="14fe2-118">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="14fe2-119">C\#</span><span class="sxs-lookup"><span data-stu-id="14fe2-119">C\#</span></span>

<span data-ttu-id="14fe2-120">Az új eszközkötet létrehozásához szükséges eszközök listájának feltöltése:</span><span class="sxs-lookup"><span data-stu-id="14fe2-120">To upload a list of devices to create a new device batch:</span></span>

1. <span data-ttu-id="14fe2-121">Példányositszon egy Új [List/dotnet/api/system.collections.generic.list-1) típusú eszközt, és töltse fel a listát az eszközökkel. [](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device)</span><span class="sxs-lookup"><span data-stu-id="14fe2-121">Instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="14fe2-122">Az egyes eszközök azonosításához legalább a következő tulajdonságkombinációk szükségesek:</span><span class="sxs-lookup"><span data-stu-id="14fe2-122">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

   - <span data-ttu-id="14fe2-123">[**Hardverhash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey (Termékkulcs).**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)</span><span class="sxs-lookup"><span data-stu-id="14fe2-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>
   - <span data-ttu-id="14fe2-124">[**Hardverhash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)( Sorozatszám).</span><span class="sxs-lookup"><span data-stu-id="14fe2-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="14fe2-125">[**Hardverhash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey (Termékkulcs)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)( Sorozatszám).</span><span class="sxs-lookup"><span data-stu-id="14fe2-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="14fe2-126">[**Csak HardverHash.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)</span><span class="sxs-lookup"><span data-stu-id="14fe2-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>
   - <span data-ttu-id="14fe2-127">[**Csak ProductKey.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)</span><span class="sxs-lookup"><span data-stu-id="14fe2-127">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>
   - <span data-ttu-id="14fe2-128">[**SerialNumber (Sorozatszám)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="14fe2-128">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

2. <span data-ttu-id="14fe2-129">Példányositsa a [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) objektumot, és állítsa a [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) tulajdonságot egy ön által választott egyedi névre, az [**Eszközök**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) tulajdonságot pedig a feltöltenie kell az eszközök listájára.</span><span class="sxs-lookup"><span data-stu-id="14fe2-129">Instantiate a [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) object and set the [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) property to a unique name of your choosing, and the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of devices to upload.</span></span>

3. <span data-ttu-id="14fe2-130">Az eszközkötet-létrehozási kérés feldolgozásához hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóval, hogy lekérni tudja a műveletek interfészét a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="14fe2-130">Process the device batch creation request by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span>

4. <span data-ttu-id="14fe2-131">A köteg létrehozásához hívja meg a [**DeviceBatches.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) vagy [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) metódust az eszközkötet-létrehozási kéréssel.</span><span class="sxs-lookup"><span data-stu-id="14fe2-131">Call the [**DeviceBatches.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) method with the device batch creation request to create the batch.</span></span>

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

<span data-ttu-id="14fe2-132">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="14fe2-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="14fe2-133">**Project**: Partnerközpont SDK **Osztály:** CreateDeviceBatch.cs</span><span class="sxs-lookup"><span data-stu-id="14fe2-133">**Project**: Partner Center SDK Samples **Class**: CreateDeviceBatch.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="14fe2-134">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="14fe2-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="14fe2-135">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="14fe2-135">Request syntax</span></span>

| <span data-ttu-id="14fe2-136">Metódus</span><span class="sxs-lookup"><span data-stu-id="14fe2-136">Method</span></span>   | <span data-ttu-id="14fe2-137">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="14fe2-137">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="14fe2-138">**Post**</span><span class="sxs-lookup"><span data-stu-id="14fe2-138">**POST**</span></span> | <span data-ttu-id="14fe2-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/deviceBatches HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="14fe2-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="14fe2-140">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="14fe2-140">URI parameter</span></span>

<span data-ttu-id="14fe2-141">A kérelem létrehozásakor használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="14fe2-141">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="14fe2-142">Név</span><span class="sxs-lookup"><span data-stu-id="14fe2-142">Name</span></span>        | <span data-ttu-id="14fe2-143">Típus</span><span class="sxs-lookup"><span data-stu-id="14fe2-143">Type</span></span>   | <span data-ttu-id="14fe2-144">Kötelező</span><span class="sxs-lookup"><span data-stu-id="14fe2-144">Required</span></span> | <span data-ttu-id="14fe2-145">Leírás</span><span class="sxs-lookup"><span data-stu-id="14fe2-145">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="14fe2-146">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="14fe2-146">customer-id</span></span> | <span data-ttu-id="14fe2-147">sztring</span><span class="sxs-lookup"><span data-stu-id="14fe2-147">string</span></span> | <span data-ttu-id="14fe2-148">Igen</span><span class="sxs-lookup"><span data-stu-id="14fe2-148">Yes</span></span>      | <span data-ttu-id="14fe2-149">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="14fe2-149">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="14fe2-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="14fe2-150">Request headers</span></span>

<span data-ttu-id="14fe2-151">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="14fe2-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="14fe2-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="14fe2-152">Request body</span></span>

<span data-ttu-id="14fe2-153">A kérelem törzsének tartalmaznia kell egy [DeviceBatchCreationRequest erőforrást.](device-deployment-resources.md#devicebatchcreationrequest)</span><span class="sxs-lookup"><span data-stu-id="14fe2-153">The request body must contain a [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="14fe2-154">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="14fe2-154">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="14fe2-155">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="14fe2-155">REST response</span></span>

<span data-ttu-id="14fe2-156">Ha a válasz sikeres, a válasz tartalmaz egy **Location** fejlécet, amely tartalmaz egy URI-t, amely az eszköz feltöltési állapotának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="14fe2-156">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="14fe2-157">Mentse ezt az URI-t a többi kapcsolódó REST API-val való használathoz.</span><span class="sxs-lookup"><span data-stu-id="14fe2-157">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="14fe2-158">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="14fe2-158">Response success and error codes</span></span>

<span data-ttu-id="14fe2-159">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="14fe2-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="14fe2-160">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="14fe2-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="14fe2-161">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="14fe2-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="14fe2-162">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="14fe2-162">Response example</span></span>

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
