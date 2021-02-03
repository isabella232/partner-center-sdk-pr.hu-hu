---
title: Egy termékváltozat lekérése azonosító alapján
description: Beolvas egy SKU-t a megadott termékhez a megadott SKU-azonosító használatával.
ms.date: 01/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 54ef72413d2d2b9e7154e82e4bbdd7427a79a2dd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767935"
---
# <a name="get-a-sku-by-id"></a><span data-ttu-id="f516a-103">Egy termékváltozat lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="f516a-103">Get a SKU by ID</span></span>

<span data-ttu-id="f516a-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="f516a-104">**Applies To**</span></span>

- <span data-ttu-id="f516a-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f516a-105">Partner Center</span></span>

<span data-ttu-id="f516a-106">Beolvas egy SKU-t a megadott termékhez a megadott SKU-azonosító használatával.</span><span class="sxs-lookup"><span data-stu-id="f516a-106">Gets a SKU for the specified product using the specified SKU ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f516a-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f516a-107">Prerequisites</span></span>

- <span data-ttu-id="f516a-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="f516a-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f516a-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="f516a-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f516a-110">A termék azonosítója.</span><span class="sxs-lookup"><span data-stu-id="f516a-110">A product ID.</span></span>

- <span data-ttu-id="f516a-111">SKU-AZONOSÍTÓ.</span><span class="sxs-lookup"><span data-stu-id="f516a-111">A SKU ID.</span></span>

## <a name="c"></a><span data-ttu-id="f516a-112">C\#</span><span class="sxs-lookup"><span data-stu-id="f516a-112">C\#</span></span>

<span data-ttu-id="f516a-113">Egy adott SKU részleteinek beszerzéséhez először kövesse a [termék beolvasása azonosító](get-a-product-by-id.md) alapján az adott termék műveleteinek felületét.</span><span class="sxs-lookup"><span data-stu-id="f516a-113">To get the details of a specific SKU, start by following the steps in [Get a product by ID](get-a-product-by-id.md) to get the interface for a specific product's operations.</span></span> <span data-ttu-id="f516a-114">Az eredményül kapott felületen válassza a **SKU** tulajdonságot, hogy beszerezze a csatolót az SKU-hoz elérhető műveletekkel.</span><span class="sxs-lookup"><span data-stu-id="f516a-114">From the resulting interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span> <span data-ttu-id="f516a-115">Adja át az SKU AZONOSÍTÓját a **ById ()** metódusnak, és hívja a **Get ()** vagy a **GetAsync ()** függvényt az SKU részleteinek lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="f516a-115">Pass the SKU ID to the **ById()** method, and call **Get()** or **GetAsync()** to retrieve the SKU details.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="rest-request"></a><span data-ttu-id="f516a-116">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="f516a-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f516a-117">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f516a-117">Request syntax</span></span>

| <span data-ttu-id="f516a-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="f516a-118">Method</span></span>  | <span data-ttu-id="f516a-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f516a-119">Request URI</span></span>                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f516a-120">**GET**</span><span class="sxs-lookup"><span data-stu-id="f516a-120">**GET**</span></span> | <span data-ttu-id="f516a-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs/{SKU-ID}? ország = {országkód} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f516a-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="f516a-122">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="f516a-122">URI parameter</span></span>

<span data-ttu-id="f516a-123">A következő elérési út és lekérdezési paraméterek használatával szerezzen be egy SKU-t a megadott termékhez a megadott SKU-azonosító használatával.</span><span class="sxs-lookup"><span data-stu-id="f516a-123">Use the following path and query parameters to get a SKU for the specified product using the specified SKU ID.</span></span>

| <span data-ttu-id="f516a-124">Név</span><span class="sxs-lookup"><span data-stu-id="f516a-124">Name</span></span>                   | <span data-ttu-id="f516a-125">Típus</span><span class="sxs-lookup"><span data-stu-id="f516a-125">Type</span></span>     | <span data-ttu-id="f516a-126">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f516a-126">Required</span></span> | <span data-ttu-id="f516a-127">Leírás</span><span class="sxs-lookup"><span data-stu-id="f516a-127">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="f516a-128">termék azonosítója</span><span class="sxs-lookup"><span data-stu-id="f516a-128">product-id</span></span>             | <span data-ttu-id="f516a-129">sztring</span><span class="sxs-lookup"><span data-stu-id="f516a-129">string</span></span>   | <span data-ttu-id="f516a-130">Igen</span><span class="sxs-lookup"><span data-stu-id="f516a-130">Yes</span></span>      | <span data-ttu-id="f516a-131">A terméket azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="f516a-131">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="f516a-132">SKU-azonosító</span><span class="sxs-lookup"><span data-stu-id="f516a-132">sku-id</span></span>                 | <span data-ttu-id="f516a-133">sztring</span><span class="sxs-lookup"><span data-stu-id="f516a-133">string</span></span>   | <span data-ttu-id="f516a-134">Igen</span><span class="sxs-lookup"><span data-stu-id="f516a-134">Yes</span></span>      | <span data-ttu-id="f516a-135">Egy karakterlánc, amely azonosítja az SKU-t.</span><span class="sxs-lookup"><span data-stu-id="f516a-135">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="f516a-136">országkód</span><span class="sxs-lookup"><span data-stu-id="f516a-136">country-code</span></span>           | <span data-ttu-id="f516a-137">sztring</span><span class="sxs-lookup"><span data-stu-id="f516a-137">string</span></span>   | <span data-ttu-id="f516a-138">Igen</span><span class="sxs-lookup"><span data-stu-id="f516a-138">Yes</span></span>      | <span data-ttu-id="f516a-139">Ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="f516a-139">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="f516a-140">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f516a-140">Request headers</span></span>

<span data-ttu-id="f516a-141">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f516a-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f516a-142">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f516a-142">Request body</span></span>

<span data-ttu-id="f516a-143">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="f516a-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f516a-144">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f516a-144">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f516a-145">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f516a-145">REST response</span></span>

<span data-ttu-id="f516a-146">Ha ez sikeres, a válasz törzse [SKU](product-resources.md#sku) -erőforrást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="f516a-146">If successful, the response body contains a [SKU](product-resources.md#sku) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f516a-147">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f516a-147">Response success and error codes</span></span>

<span data-ttu-id="f516a-148">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="f516a-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f516a-149">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="f516a-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f516a-150">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f516a-150">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="f516a-151">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="f516a-151">This method returns the following error codes:</span></span>

| <span data-ttu-id="f516a-152">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="f516a-152">HTTP Status Code</span></span>     | <span data-ttu-id="f516a-153">Hibakód</span><span class="sxs-lookup"><span data-stu-id="f516a-153">Error code</span></span>   | <span data-ttu-id="f516a-154">Leírás</span><span class="sxs-lookup"><span data-stu-id="f516a-154">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f516a-155">404</span><span class="sxs-lookup"><span data-stu-id="f516a-155">404</span></span>                  | <span data-ttu-id="f516a-156">400013</span><span class="sxs-lookup"><span data-stu-id="f516a-156">400013</span></span>       | <span data-ttu-id="f516a-157">A termék nem található.</span><span class="sxs-lookup"><span data-stu-id="f516a-157">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="f516a-158">404</span><span class="sxs-lookup"><span data-stu-id="f516a-158">404</span></span>                  | <span data-ttu-id="f516a-159">400018</span><span class="sxs-lookup"><span data-stu-id="f516a-159">400018</span></span>       | <span data-ttu-id="f516a-160">Az SKU nem található.</span><span class="sxs-lookup"><span data-stu-id="f516a-160">Sku was not found.</span></span>                                                                                        |

### <a name="response-example"></a><span data-ttu-id="f516a-161">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f516a-161">Response example</span></span>

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
