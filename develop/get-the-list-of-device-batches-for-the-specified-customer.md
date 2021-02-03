---
title: A megadott ügyfél eszközköteglistájának lekérése
description: Eszköz kötegek gyűjteményének beolvasása a megadott ügyfélhez.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea5797bbaff4d4eafd1e63428556ab784bcb0ee2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768415"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a><span data-ttu-id="0c5f3-103">A megadott ügyfél eszközköteglistájának lekérése</span><span class="sxs-lookup"><span data-stu-id="0c5f3-103">Get a list of device batches for the specified customer</span></span>

<span data-ttu-id="0c5f3-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="0c5f3-104">**Applies To**</span></span>

- <span data-ttu-id="0c5f3-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="0c5f3-105">Partner Center</span></span>
- <span data-ttu-id="0c5f3-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="0c5f3-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="0c5f3-107">Eszköz kötegek gyűjteményének beolvasása a megadott ügyfélhez.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-107">How to retrieve a collection of device batches for the specified customer.</span></span>

<span data-ttu-id="0c5f3-108">Minden eszköz kötege összegző állapotinformációkat tartalmaz azokról az eszközökről, amelyeket a rendszer nulla érintéses telepítésben regisztrált.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-108">Each device batch contains summary status information about devices that have been enrolled in zero-touch deployment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c5f3-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="0c5f3-109">Prerequisites</span></span>

- <span data-ttu-id="0c5f3-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0c5f3-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0c5f3-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0c5f3-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0c5f3-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="0c5f3-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0c5f3-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0c5f3-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0c5f3-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0c5f3-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0c5f3-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0c5f3-118">C\#</span><span class="sxs-lookup"><span data-stu-id="0c5f3-118">C\#</span></span>

<span data-ttu-id="0c5f3-119">A megadott ügyfélhez tartozó kötegek gyűjtésének lekéréséhez először hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérje le a felületet a műveletekre a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-119">To get the collection of device batches for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="0c5f3-120">Ezután kérje le a [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) tulajdonság értékét, hogy lekérje az eszközhöz tartozó Batch-gyűjtemény műveleteit.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-120">Then, retrieve the value of the [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) property to get an interface to device batch collection operations.</span></span> <span data-ttu-id="0c5f3-121">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) metódust a gyűjtemény lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

<span data-ttu-id="0c5f3-122">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0c5f3-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0c5f3-123">**Projekt**: partner Center SDK Samples **osztály**: GetDevicesBatches.cs</span><span class="sxs-lookup"><span data-stu-id="0c5f3-123">**Project**: Partner Center SDK Samples **Class**: GetDevicesBatches.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0c5f3-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="0c5f3-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0c5f3-125">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="0c5f3-125">Request syntax</span></span>

| <span data-ttu-id="0c5f3-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="0c5f3-126">Method</span></span>  | <span data-ttu-id="0c5f3-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="0c5f3-127">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="0c5f3-128">**GET**</span><span class="sxs-lookup"><span data-stu-id="0c5f3-128">**GET**</span></span> | <span data-ttu-id="0c5f3-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches http/1.1</span><span class="sxs-lookup"><span data-stu-id="0c5f3-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0c5f3-130">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="0c5f3-130">URI parameter</span></span>

<span data-ttu-id="0c5f3-131">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-131">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="0c5f3-132">Név</span><span class="sxs-lookup"><span data-stu-id="0c5f3-132">Name</span></span>        | <span data-ttu-id="0c5f3-133">Típus</span><span class="sxs-lookup"><span data-stu-id="0c5f3-133">Type</span></span>   | <span data-ttu-id="0c5f3-134">Kötelező</span><span class="sxs-lookup"><span data-stu-id="0c5f3-134">Required</span></span> | <span data-ttu-id="0c5f3-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="0c5f3-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="0c5f3-136">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="0c5f3-136">customer-id</span></span> | <span data-ttu-id="0c5f3-137">sztring</span><span class="sxs-lookup"><span data-stu-id="0c5f3-137">string</span></span> | <span data-ttu-id="0c5f3-138">Igen</span><span class="sxs-lookup"><span data-stu-id="0c5f3-138">Yes</span></span>      | <span data-ttu-id="0c5f3-139">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-139">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0c5f3-140">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="0c5f3-140">Request headers</span></span>

<span data-ttu-id="0c5f3-141">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0c5f3-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0c5f3-142">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="0c5f3-142">Request body</span></span>

<span data-ttu-id="0c5f3-143">Nincs</span><span class="sxs-lookup"><span data-stu-id="0c5f3-143">None</span></span>

### <a name="request-example"></a><span data-ttu-id="0c5f3-144">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="0c5f3-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="0c5f3-145">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="0c5f3-145">REST response</span></span>

<span data-ttu-id="0c5f3-146">Ha ez sikeres, a válasz törzse tartalmazza a [DeviceBatch](device-deployment-resources.md#devicebatch) -erőforrások gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-146">If successful, the response body contains the collection of [DeviceBatch](device-deployment-resources.md#devicebatch) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0c5f3-147">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="0c5f3-147">Response success and error codes</span></span>

<span data-ttu-id="0c5f3-148">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0c5f3-149">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0c5f3-150">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="0c5f3-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0c5f3-151">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="0c5f3-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 339
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "Test batch",
            "status": "finished",
            "creationDate": "2017-07-25T01:51:00",
            "devicesCount": 5,
            "devicesLink": {
                "uri": "/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/Test batch/devices",
                "method": "GET",
                "headers": []
            },
            "attributes": {
                "objectType": "DeviceBatch"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
