---
title: A megadott ügyfél eszközköteglistájának lekérése
description: Eszközköteik gyűjteményének lekérése a megadott ügyfél számára.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9d020bbfa1faef0be423d2fef2d8982465dfa21f
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548416"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a><span data-ttu-id="a33e8-103">A megadott ügyfél eszközköteglistájának lekérése</span><span class="sxs-lookup"><span data-stu-id="a33e8-103">Get a list of device batches for the specified customer</span></span>

<span data-ttu-id="a33e8-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="a33e8-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="a33e8-105">Eszközköteik gyűjteményének lekérése a megadott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="a33e8-105">How to retrieve a collection of device batches for the specified customer.</span></span>

<span data-ttu-id="a33e8-106">Minden eszközkötem összegző állapotinformációt tartalmaz az érintés nélküli üzembe helyezésben regisztrált eszközökről.</span><span class="sxs-lookup"><span data-stu-id="a33e8-106">Each device batch contains summary status information about devices that have been enrolled in zero-touch deployment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a33e8-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="a33e8-107">Prerequisites</span></span>

- <span data-ttu-id="a33e8-108">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a33e8-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a33e8-109">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="a33e8-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a33e8-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a33e8-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a33e8-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="a33e8-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a33e8-112">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a33e8-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a33e8-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a33e8-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a33e8-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="a33e8-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a33e8-115">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a33e8-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="a33e8-116">C\#</span><span class="sxs-lookup"><span data-stu-id="a33e8-116">C\#</span></span>

<span data-ttu-id="a33e8-117">A megadott ügyfél eszközkötem-gyűjteményének lekéréséhez először hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával, hogy lekérje a műveletek interfészét a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="a33e8-117">To get the collection of device batches for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="a33e8-118">Ezután lekéri a [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) tulajdonság értékét az eszközkötet-gyűjtési műveletek interfészének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="a33e8-118">Then, retrieve the value of the [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) property to get an interface to device batch collection operations.</span></span> <span data-ttu-id="a33e8-119">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) vagy [**GetAsync metódust**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) a gyűjtemény lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="a33e8-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

<span data-ttu-id="a33e8-120">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="a33e8-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a33e8-121">**Project**: Partnerközpont SDK **Osztály:** GetDevicesBatches.cs</span><span class="sxs-lookup"><span data-stu-id="a33e8-121">**Project**: Partner Center SDK Samples **Class**: GetDevicesBatches.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a33e8-122">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="a33e8-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a33e8-123">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="a33e8-123">Request syntax</span></span>

| <span data-ttu-id="a33e8-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="a33e8-124">Method</span></span>  | <span data-ttu-id="a33e8-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="a33e8-125">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="a33e8-126">**Kap**</span><span class="sxs-lookup"><span data-stu-id="a33e8-126">**GET**</span></span> | <span data-ttu-id="a33e8-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/deviceBatches HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a33e8-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a33e8-128">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="a33e8-128">URI parameter</span></span>

<span data-ttu-id="a33e8-129">A kérelem létrehozásakor használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="a33e8-129">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="a33e8-130">Név</span><span class="sxs-lookup"><span data-stu-id="a33e8-130">Name</span></span>        | <span data-ttu-id="a33e8-131">Típus</span><span class="sxs-lookup"><span data-stu-id="a33e8-131">Type</span></span>   | <span data-ttu-id="a33e8-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="a33e8-132">Required</span></span> | <span data-ttu-id="a33e8-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="a33e8-133">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="a33e8-134">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="a33e8-134">customer-id</span></span> | <span data-ttu-id="a33e8-135">sztring</span><span class="sxs-lookup"><span data-stu-id="a33e8-135">string</span></span> | <span data-ttu-id="a33e8-136">Igen</span><span class="sxs-lookup"><span data-stu-id="a33e8-136">Yes</span></span>      | <span data-ttu-id="a33e8-137">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="a33e8-137">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a33e8-138">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="a33e8-138">Request headers</span></span>

<span data-ttu-id="a33e8-139">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a33e8-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a33e8-140">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="a33e8-140">Request body</span></span>

<span data-ttu-id="a33e8-141">None</span><span class="sxs-lookup"><span data-stu-id="a33e8-141">None</span></span>

### <a name="request-example"></a><span data-ttu-id="a33e8-142">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="a33e8-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="a33e8-143">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="a33e8-143">REST response</span></span>

<span data-ttu-id="a33e8-144">Ha a művelet sikeres, a válasz törzse tartalmazza a [DeviceBatch-erőforrások gyűjteményét.](device-deployment-resources.md#devicebatch)</span><span class="sxs-lookup"><span data-stu-id="a33e8-144">If successful, the response body contains the collection of [DeviceBatch](device-deployment-resources.md#devicebatch) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a33e8-145">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="a33e8-145">Response success and error codes</span></span>

<span data-ttu-id="a33e8-146">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="a33e8-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a33e8-147">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="a33e8-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a33e8-148">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a33e8-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a33e8-149">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="a33e8-149">Response example</span></span>

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
