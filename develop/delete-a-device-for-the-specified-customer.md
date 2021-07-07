---
title: Eszköz törlése a megadott ügyfélnél
description: Megadott ügyfélhez tartozó eszköz törlése.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1e05ceb8615d6f84c1df101c542342f9a6eb04b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973077"
---
# <a name="delete-a-device-for-the-specified-customer"></a><span data-ttu-id="e558e-103">Eszköz törlése a megadott ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="e558e-103">Delete a device for the specified customer</span></span>

<span data-ttu-id="e558e-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="e558e-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="e558e-105">Ez a cikk egy adott ügyfélhez tartozó eszköz törlését ismerteti.</span><span class="sxs-lookup"><span data-stu-id="e558e-105">This article explains how to delete a device that belongs to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e558e-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="e558e-106">Prerequisites</span></span>

- <span data-ttu-id="e558e-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e558e-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e558e-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="e558e-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e558e-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e558e-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e558e-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="e558e-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e558e-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e558e-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e558e-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e558e-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e558e-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="e558e-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e558e-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e558e-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e558e-115">Az eszköz kötegazonosítója.</span><span class="sxs-lookup"><span data-stu-id="e558e-115">The device batch identifier.</span></span>

- <span data-ttu-id="e558e-116">Az eszköz azonosítója.</span><span class="sxs-lookup"><span data-stu-id="e558e-116">The device identifier.</span></span>

## <a name="c"></a><span data-ttu-id="e558e-117">C\#</span><span class="sxs-lookup"><span data-stu-id="e558e-117">C\#</span></span>

<span data-ttu-id="e558e-118">Eszköz törlése a megadott ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="e558e-118">To delete a device for the specified customer:</span></span>

1. <span data-ttu-id="e558e-119">Hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóval az ügyfélen folytatott műveletek interfészének lekérése érdekében.</span><span class="sxs-lookup"><span data-stu-id="e558e-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the customer.</span></span>

2. <span data-ttu-id="e558e-120">Hívja meg [**a DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) metódust az eszköz kötegazonosítójának használatával, hogy lekért egy interfészt a megadott köteg műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="e558e-120">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span>

3. <span data-ttu-id="e558e-121">Hívja meg [**a Devices.ById metódust,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) hogy lekért egy interfészt a művelethez a megadott eszközön.</span><span class="sxs-lookup"><span data-stu-id="e558e-121">Call the [**Devices.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) method to get an interface to operation on the specified device.</span></span>

4. <span data-ttu-id="e558e-122">Az eszköz [**kötegből**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) való törléséhez hívja meg a Delete vagy [**a DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="e558e-122">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) method to delete the device from the batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

<span data-ttu-id="e558e-123">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e558e-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e558e-124">**Project**: Partnerközpont SDK **Osztály:** DeleteDevice.cs</span><span class="sxs-lookup"><span data-stu-id="e558e-124">**Project**: Partner Center SDK Samples **Class**: DeleteDevice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e558e-125">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="e558e-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e558e-126">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="e558e-126">Request syntax</span></span>

| <span data-ttu-id="e558e-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="e558e-127">Method</span></span>     | <span data-ttu-id="e558e-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="e558e-128">Request URI</span></span>                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e558e-129">DELETE</span><span class="sxs-lookup"><span data-stu-id="e558e-129">DELETE</span></span>     | <span data-ttu-id="e558e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/deviceBatches/{devicebatch-id}/devices/{eszközazonosító} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e558e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="e558e-131">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="e558e-131">URI parameters</span></span>

<span data-ttu-id="e558e-132">A kérelem létrehozásakor használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="e558e-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="e558e-133">Név</span><span class="sxs-lookup"><span data-stu-id="e558e-133">Name</span></span>           | <span data-ttu-id="e558e-134">Típus</span><span class="sxs-lookup"><span data-stu-id="e558e-134">Type</span></span>   | <span data-ttu-id="e558e-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e558e-135">Required</span></span> | <span data-ttu-id="e558e-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="e558e-136">Description</span></span>                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| <span data-ttu-id="e558e-137">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="e558e-137">customer-id</span></span>    | <span data-ttu-id="e558e-138">sztring</span><span class="sxs-lookup"><span data-stu-id="e558e-138">string</span></span> | <span data-ttu-id="e558e-139">Igen</span><span class="sxs-lookup"><span data-stu-id="e558e-139">Yes</span></span>      | <span data-ttu-id="e558e-140">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="e558e-140">A GUID-formatted string that identifies the customer.</span></span>              |
| <span data-ttu-id="e558e-141">devicebatch-id</span><span class="sxs-lookup"><span data-stu-id="e558e-141">devicebatch-id</span></span> | <span data-ttu-id="e558e-142">sztring</span><span class="sxs-lookup"><span data-stu-id="e558e-142">string</span></span> | <span data-ttu-id="e558e-143">Igen</span><span class="sxs-lookup"><span data-stu-id="e558e-143">Yes</span></span>      | <span data-ttu-id="e558e-144">Az eszközt tartalmazó köteg eszközkötet-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="e558e-144">The device batch identifier of the batch that contains the device.</span></span> |
| <span data-ttu-id="e558e-145">eszközazonosító</span><span class="sxs-lookup"><span data-stu-id="e558e-145">device-id</span></span>      | <span data-ttu-id="e558e-146">sztring</span><span class="sxs-lookup"><span data-stu-id="e558e-146">string</span></span> | <span data-ttu-id="e558e-147">Igen</span><span class="sxs-lookup"><span data-stu-id="e558e-147">Yes</span></span>      | <span data-ttu-id="e558e-148">Az eszköz azonosítója.</span><span class="sxs-lookup"><span data-stu-id="e558e-148">The device identifier.</span></span>                                             |

### <a name="request-headers"></a><span data-ttu-id="e558e-149">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="e558e-149">Request headers</span></span>

<span data-ttu-id="e558e-150">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e558e-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e558e-151">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="e558e-151">Request body</span></span>

<span data-ttu-id="e558e-152">None</span><span class="sxs-lookup"><span data-stu-id="e558e-152">None</span></span>

### <a name="request-example"></a><span data-ttu-id="e558e-153">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="e558e-153">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="e558e-154">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="e558e-154">REST response</span></span>

<span data-ttu-id="e558e-155">Ha a válasz sikeres, a **204 Nincs** tartalom állapotkódot adja vissza.</span><span class="sxs-lookup"><span data-stu-id="e558e-155">If successful, the response returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e558e-156">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="e558e-156">Response success and error codes</span></span>

<span data-ttu-id="e558e-157">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="e558e-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e558e-158">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="e558e-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e558e-159">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e558e-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e558e-160">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="e558e-160">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
