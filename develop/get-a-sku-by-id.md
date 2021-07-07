---
title: Egy termékváltozat lekérése azonosító alapján
description: Lekért egy termékváltozatot a megadott termékváltozat-azonosítóval.
ms.date: 01/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9516a87a438a0a84a6f6069c1f9b2a2e97e90fba
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873853"
---
# <a name="get-a-sku-by-id"></a><span data-ttu-id="f7122-103">Egy termékváltozat lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="f7122-103">Get a SKU by ID</span></span>

<span data-ttu-id="f7122-104">Lekért egy termékváltozatot a megadott termékváltozat-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="f7122-104">Gets a SKU for the specified product using the specified SKU ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7122-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f7122-105">Prerequisites</span></span>

- <span data-ttu-id="f7122-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f7122-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f7122-107">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="f7122-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f7122-108">Egy termékazonosító.</span><span class="sxs-lookup"><span data-stu-id="f7122-108">A product ID.</span></span>

- <span data-ttu-id="f7122-109">Egy termékváltozat-azonosító.</span><span class="sxs-lookup"><span data-stu-id="f7122-109">A SKU ID.</span></span>

## <a name="c"></a><span data-ttu-id="f7122-110">C\#</span><span class="sxs-lookup"><span data-stu-id="f7122-110">C\#</span></span>

<span data-ttu-id="f7122-111">Egy adott termékváltozat részleteinek lekért lépéseit [](get-a-product-by-id.md) a Termék lekérte azonosító alapján lépéseit követve szerezze be az adott termék műveleteihez szükséges felületet.</span><span class="sxs-lookup"><span data-stu-id="f7122-111">To get the details of a specific SKU, start by following the steps in [Get a product by ID](get-a-product-by-id.md) to get the interface for a specific product's operations.</span></span> <span data-ttu-id="f7122-112">Az eredményül kapott felületen válassza a **Skus (Skus)** tulajdonságot a rendelkezésre álló SKUs-műveletekkel való interfész beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="f7122-112">From the resulting interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span> <span data-ttu-id="f7122-113">Adja át a termékváltozat azonosítóját a **ById()** metódusnak, és hívja meg a **Get()** vagy **a GetAsync()** metódust a termékváltozat részleteinek lekéréshez.</span><span class="sxs-lookup"><span data-stu-id="f7122-113">Pass the SKU ID to the **ById()** method, and call **Get()** or **GetAsync()** to retrieve the SKU details.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="rest-request"></a><span data-ttu-id="f7122-114">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="f7122-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f7122-115">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f7122-115">Request syntax</span></span>

| <span data-ttu-id="f7122-116">Metódus</span><span class="sxs-lookup"><span data-stu-id="f7122-116">Method</span></span>  | <span data-ttu-id="f7122-117">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f7122-117">Request URI</span></span>                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f7122-118">**Kap**</span><span class="sxs-lookup"><span data-stu-id="f7122-118">**GET**</span></span> | <span data-ttu-id="f7122-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{termékazonosító}/termékváltozatok/{termékváltozat}?country={országkód} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f7122-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="f7122-120">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="f7122-120">URI parameter</span></span>

<span data-ttu-id="f7122-121">Az alábbi elérési út és lekérdezési paraméterek használatával lekérdezheti a megadott termékváltozatot a megadott termékváltozat-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="f7122-121">Use the following path and query parameters to get a SKU for the specified product using the specified SKU ID.</span></span>

| <span data-ttu-id="f7122-122">Név</span><span class="sxs-lookup"><span data-stu-id="f7122-122">Name</span></span>                   | <span data-ttu-id="f7122-123">Típus</span><span class="sxs-lookup"><span data-stu-id="f7122-123">Type</span></span>     | <span data-ttu-id="f7122-124">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f7122-124">Required</span></span> | <span data-ttu-id="f7122-125">Leírás</span><span class="sxs-lookup"><span data-stu-id="f7122-125">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="f7122-126">termékazonosító</span><span class="sxs-lookup"><span data-stu-id="f7122-126">product-id</span></span>             | <span data-ttu-id="f7122-127">sztring</span><span class="sxs-lookup"><span data-stu-id="f7122-127">string</span></span>   | <span data-ttu-id="f7122-128">Igen</span><span class="sxs-lookup"><span data-stu-id="f7122-128">Yes</span></span>      | <span data-ttu-id="f7122-129">A terméket azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="f7122-129">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="f7122-130">sku-id</span><span class="sxs-lookup"><span data-stu-id="f7122-130">sku-id</span></span>                 | <span data-ttu-id="f7122-131">sztring</span><span class="sxs-lookup"><span data-stu-id="f7122-131">string</span></span>   | <span data-ttu-id="f7122-132">Igen</span><span class="sxs-lookup"><span data-stu-id="f7122-132">Yes</span></span>      | <span data-ttu-id="f7122-133">A termékváltozatot azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="f7122-133">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="f7122-134">országkód</span><span class="sxs-lookup"><span data-stu-id="f7122-134">country-code</span></span>           | <span data-ttu-id="f7122-135">sztring</span><span class="sxs-lookup"><span data-stu-id="f7122-135">string</span></span>   | <span data-ttu-id="f7122-136">Igen</span><span class="sxs-lookup"><span data-stu-id="f7122-136">Yes</span></span>      | <span data-ttu-id="f7122-137">Egy ország-/régióazonosító.</span><span class="sxs-lookup"><span data-stu-id="f7122-137">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="f7122-138">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f7122-138">Request headers</span></span>

<span data-ttu-id="f7122-139">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f7122-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f7122-140">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f7122-140">Request body</span></span>

<span data-ttu-id="f7122-141">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="f7122-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f7122-142">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f7122-142">Request example</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3V/skus/00G1?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f7122-143">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f7122-143">REST response</span></span>

<span data-ttu-id="f7122-144">Ha a művelet sikeres, a válasz törzse tartalmaz [egy SKU-erőforrást.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="f7122-144">If successful, the response body contains a [SKU](product-resources.md#sku) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f7122-145">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f7122-145">Response success and error codes</span></span>

<span data-ttu-id="f7122-146">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="f7122-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f7122-147">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="f7122-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f7122-148">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f7122-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="f7122-149">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="f7122-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="f7122-150">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="f7122-150">HTTP Status Code</span></span>     | <span data-ttu-id="f7122-151">Hibakód</span><span class="sxs-lookup"><span data-stu-id="f7122-151">Error code</span></span>   | <span data-ttu-id="f7122-152">Leírás</span><span class="sxs-lookup"><span data-stu-id="f7122-152">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f7122-153">404</span><span class="sxs-lookup"><span data-stu-id="f7122-153">404</span></span>                  | <span data-ttu-id="f7122-154">400013</span><span class="sxs-lookup"><span data-stu-id="f7122-154">400013</span></span>       | <span data-ttu-id="f7122-155">A termék nem található.</span><span class="sxs-lookup"><span data-stu-id="f7122-155">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="f7122-156">404</span><span class="sxs-lookup"><span data-stu-id="f7122-156">404</span></span>                  | <span data-ttu-id="f7122-157">400018</span><span class="sxs-lookup"><span data-stu-id="f7122-157">400018</span></span>       | <span data-ttu-id="f7122-158">A termékváltozat nem található.</span><span class="sxs-lookup"><span data-stu-id="f7122-158">Sku was not found.</span></span>                                                                                        |

### <a name="response-example"></a><span data-ttu-id="f7122-159">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f7122-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23,956eae17-7650-4470-94d2-4f61b9b02a23
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f,e0ae69a5-6322-4d7e-809d-59e02b51d71f
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNWXHNrdXNcMDBHMQ==?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 17:43:25 GMT
Content-Length: 1108

{
    "id": "00G1",
    "productId": "DZH318Z0BQ3V",
    "title": "Reserved VM Instance, Standard_D32s_v3, US West 2, 3 Years",
    "description": "Reserved Virtual Machines Instance, Standard_D32s_v3, US West 2, 3 Years",
    "minimumQuantity": 1,
    "maximumQuantity": 999999999,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "AzureSubscriptionRegistration",
        "InventoryCheck"
    ],
    "inventoryVariables": [
        "CustomerId",
        "AzureSubscriptionId"
    ],
    "provisioningVariables": [
        "Scope",
        "SubscriptionId"
    ],
    "dynamicAttributes": {
        "armSkuName": "Standard_D32s_v3",
        "cores": "32",
        "ram": "128",
        "skuDisplayName": "D32s v3",
        "category": "General purpose",
        "armRegionName": "westus2",
        "duration": "3Years",
        "region": "US West 2",
        "diskType": "Ssd"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1/availabilities?country=us",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1?country=us",
            "method": "GET",
            "headers": []
        }
    }
}
```
