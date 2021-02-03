---
title: Eszköz törlése a megadott ügyfélnél
description: Egy adott ügyfélhez tartozó eszköz törlése.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 69b5440f2cf07d3cb4ecd5addf429acd64530257
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768132"
---
# <a name="delete-a-device-for-the-specified-customer"></a><span data-ttu-id="baa73-103">Eszköz törlése a megadott ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="baa73-103">Delete a device for the specified customer</span></span>

<span data-ttu-id="baa73-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="baa73-104">**Applies to:**</span></span>

- <span data-ttu-id="baa73-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="baa73-105">Partner Center</span></span>
- <span data-ttu-id="baa73-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="baa73-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="baa73-107">Ez a cikk azt ismerteti, hogyan törölhet egy adott ügyfélhez tartozó eszközt.</span><span class="sxs-lookup"><span data-stu-id="baa73-107">This article explains how to delete a device that belongs to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baa73-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="baa73-108">Prerequisites</span></span>

- <span data-ttu-id="baa73-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="baa73-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="baa73-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="baa73-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="baa73-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="baa73-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="baa73-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="baa73-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="baa73-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="baa73-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="baa73-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="baa73-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="baa73-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="baa73-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="baa73-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="baa73-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="baa73-117">Az eszköz batch-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="baa73-117">The device batch identifier.</span></span>

- <span data-ttu-id="baa73-118">Az eszköz azonosítója.</span><span class="sxs-lookup"><span data-stu-id="baa73-118">The device identifier.</span></span>

## <a name="c"></a><span data-ttu-id="baa73-119">C\#</span><span class="sxs-lookup"><span data-stu-id="baa73-119">C\#</span></span>

<span data-ttu-id="baa73-120">Eszköz törlése a megadott ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="baa73-120">To delete a device for the specified customer:</span></span>

1. <span data-ttu-id="baa73-121">Hívja meg a [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérjen le egy felületet az ügyfélen végzett műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="baa73-121">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the customer.</span></span>

2. <span data-ttu-id="baa73-122">Hívja meg a [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) metódust az eszköz batch-azonosítójával, és szerezzen be egy illesztőfelületet a megadott köteg műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="baa73-122">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span>

3. <span data-ttu-id="baa73-123">A [**Devices. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) metódus meghívásával lekérheti az adott eszközön a művelethez szükséges felületet.</span><span class="sxs-lookup"><span data-stu-id="baa73-123">Call the [**Devices.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) method to get an interface to operation on the specified device.</span></span>

4. <span data-ttu-id="baa73-124">A [**delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) vagy a [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) metódus meghívásával törölje az eszközt a kötegből.</span><span class="sxs-lookup"><span data-stu-id="baa73-124">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) method to delete the device from the batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

<span data-ttu-id="baa73-125">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="baa73-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="baa73-126">**Projekt**: partner Center SDK Samples **osztály**: DeleteDevice.cs</span><span class="sxs-lookup"><span data-stu-id="baa73-126">**Project**: Partner Center SDK Samples **Class**: DeleteDevice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="baa73-127">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="baa73-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="baa73-128">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="baa73-128">Request syntax</span></span>

| <span data-ttu-id="baa73-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="baa73-129">Method</span></span>     | <span data-ttu-id="baa73-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="baa73-130">Request URI</span></span>                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="baa73-131">DELETE</span><span class="sxs-lookup"><span data-stu-id="baa73-131">DELETE</span></span>     | <span data-ttu-id="baa73-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices/{Device-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="baa73-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="baa73-133">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="baa73-133">URI parameters</span></span>

<span data-ttu-id="baa73-134">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="baa73-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="baa73-135">Név</span><span class="sxs-lookup"><span data-stu-id="baa73-135">Name</span></span>           | <span data-ttu-id="baa73-136">Típus</span><span class="sxs-lookup"><span data-stu-id="baa73-136">Type</span></span>   | <span data-ttu-id="baa73-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="baa73-137">Required</span></span> | <span data-ttu-id="baa73-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="baa73-138">Description</span></span>                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| <span data-ttu-id="baa73-139">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="baa73-139">customer-id</span></span>    | <span data-ttu-id="baa73-140">sztring</span><span class="sxs-lookup"><span data-stu-id="baa73-140">string</span></span> | <span data-ttu-id="baa73-141">Igen</span><span class="sxs-lookup"><span data-stu-id="baa73-141">Yes</span></span>      | <span data-ttu-id="baa73-142">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="baa73-142">A GUID-formatted string that identifies the customer.</span></span>              |
| <span data-ttu-id="baa73-143">devicebatch-azonosító</span><span class="sxs-lookup"><span data-stu-id="baa73-143">devicebatch-id</span></span> | <span data-ttu-id="baa73-144">sztring</span><span class="sxs-lookup"><span data-stu-id="baa73-144">string</span></span> | <span data-ttu-id="baa73-145">Igen</span><span class="sxs-lookup"><span data-stu-id="baa73-145">Yes</span></span>      | <span data-ttu-id="baa73-146">Az eszközt tartalmazó köteg eszközének batch-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="baa73-146">The device batch identifier of the batch that contains the device.</span></span> |
| <span data-ttu-id="baa73-147">eszköz azonosítója</span><span class="sxs-lookup"><span data-stu-id="baa73-147">device-id</span></span>      | <span data-ttu-id="baa73-148">sztring</span><span class="sxs-lookup"><span data-stu-id="baa73-148">string</span></span> | <span data-ttu-id="baa73-149">Igen</span><span class="sxs-lookup"><span data-stu-id="baa73-149">Yes</span></span>      | <span data-ttu-id="baa73-150">Az eszköz azonosítója.</span><span class="sxs-lookup"><span data-stu-id="baa73-150">The device identifier.</span></span>                                             |

### <a name="request-headers"></a><span data-ttu-id="baa73-151">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="baa73-151">Request headers</span></span>

<span data-ttu-id="baa73-152">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="baa73-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="baa73-153">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="baa73-153">Request body</span></span>

<span data-ttu-id="baa73-154">Nincs</span><span class="sxs-lookup"><span data-stu-id="baa73-154">None</span></span>

### <a name="request-example"></a><span data-ttu-id="baa73-155">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="baa73-155">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices/7b11cd8b-dd1e-4840-8c4a-84215e4de782 HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="baa73-156">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="baa73-156">REST response</span></span>

<span data-ttu-id="baa73-157">Ha a művelet sikeres, a válasz egy 204-as **tartalmat** ad vissza.</span><span class="sxs-lookup"><span data-stu-id="baa73-157">If successful, the response returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="baa73-158">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="baa73-158">Response success and error codes</span></span>

<span data-ttu-id="baa73-159">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="baa73-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="baa73-160">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="baa73-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="baa73-161">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="baa73-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="baa73-162">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="baa73-162">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
