---
title: A rendelkezésre állás beolvasása azonosító alapján
description: A megadott termék és SKU rendelkezésre állásának beolvasása a rendelkezésre állási azonosító használatával.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 824303d40e1dcb0405246c8e29562c4527d147fd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767715"
---
# <a name="get-the-availability-by-id"></a><span data-ttu-id="399e4-103">A rendelkezésre állás beolvasása azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="399e4-103">Get the availability by ID</span></span>

<span data-ttu-id="399e4-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="399e4-104">**Applies To**</span></span>

- <span data-ttu-id="399e4-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="399e4-105">Partner Center</span></span>

<span data-ttu-id="399e4-106">A megadott termék és SKU rendelkezésre állásának beolvasása a rendelkezésre állási azonosító használatával.</span><span class="sxs-lookup"><span data-stu-id="399e4-106">Gets the availability for the specified product and SKU using an availability ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="399e4-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="399e4-107">Prerequisites</span></span>

- <span data-ttu-id="399e4-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="399e4-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="399e4-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="399e4-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="399e4-110">A termék azonosítója.</span><span class="sxs-lookup"><span data-stu-id="399e4-110">A product ID.</span></span>

- <span data-ttu-id="399e4-111">SKU-AZONOSÍTÓ.</span><span class="sxs-lookup"><span data-stu-id="399e4-111">A SKU ID.</span></span>

- <span data-ttu-id="399e4-112">Egy rendelkezésre állási azonosító.</span><span class="sxs-lookup"><span data-stu-id="399e4-112">An availability ID.</span></span>

## <a name="c"></a><span data-ttu-id="399e4-113">C\#</span><span class="sxs-lookup"><span data-stu-id="399e4-113">C\#</span></span>

<span data-ttu-id="399e4-114">Egy adott [rendelkezésre állás](product-resources.md#availability)részleteinek beszerzéséhez először a [SKU BEszerzése azonosítóval](get-a-sku-by-id.md) című cikkben ismertetett lépéseket követve szerezheti be egy adott [SKU](product-resources.md#sku) műveleteinek felületét.</span><span class="sxs-lookup"><span data-stu-id="399e4-114">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="399e4-115">Az eredményül kapott felületen válassza a beszerzések tulajdonságot, hogy beszerezze **az elérhető** műveletekkel rendelkező felületet.</span><span class="sxs-lookup"><span data-stu-id="399e4-115">From the resulting interface, select the **Availabilities** property to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="399e4-116">Ezután adja át a rendelkezésre állási azonosítót a **ById ()** metódusnak, hogy lekérje az adott rendelkezésre állásra vonatkozó műveleteket, majd hívja a **Get ()** vagy a **GetAsync ()** függvényt a rendelkezésre állási adatok lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="399e4-116">After that, pass the availability ID to the **ById()** method to get the operations for that specific availability and then call **Get()** or **GetAsync()** to retrieve the availability details.</span></span>

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a><span data-ttu-id="399e4-117">Java</span><span class="sxs-lookup"><span data-stu-id="399e4-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="399e4-118">Egy adott [rendelkezésre állás](product-resources.md#availability)részleteinek beszerzéséhez először a [SKU BEszerzése azonosítóval](get-a-sku-by-id.md) című cikkben ismertetett lépéseket követve szerezheti be egy adott [SKU](product-resources.md#sku) műveleteinek felületét.</span><span class="sxs-lookup"><span data-stu-id="399e4-118">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="399e4-119">Az eredményül kapott felületről válassza a **getAvailabilities** függvényt, és szerezzen be egy felületet a rendelkezésre álláshoz elérhető műveletekkel.</span><span class="sxs-lookup"><span data-stu-id="399e4-119">From the resulting interface, select the **getAvailabilities** function to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="399e4-120">Ezután adja át a rendelkezésre állási azonosítót a **byId ()** függvénynek, hogy lekérje az adott rendelkezésre álláshoz tartozó műveleteket, majd a **Get ()** függvény meghívásával kérje le a rendelkezésre állási adatokat.</span><span class="sxs-lookup"><span data-stu-id="399e4-120">After that, pass the availability ID to the **byId()** function to get the operations for that specific availability and then call the **get()** function to retrieve the availability details.</span></span>

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a><span data-ttu-id="399e4-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="399e4-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="399e4-122">Egy adott [rendelkezésre állás](product-resources.md#availability)részleteinek beszerzéséhez hajtsa végre a [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) , és adja meg a **AvailabilityId**, a **országhívószám**, a **Termékkód** és a **SkuId** paramétereket a rendelkezésre állási adatok lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="399e4-122">To get details of a specific [availability](product-resources.md#availability), execute the [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) and specify the **AvailabilityId**, **CountryCode**, **ProductId**, and **SkuId** parameters to retrieve the availability details.</span></span>

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a><span data-ttu-id="399e4-123">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="399e4-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="399e4-124">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="399e4-124">Request syntax</span></span>

| <span data-ttu-id="399e4-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="399e4-125">Method</span></span>  | <span data-ttu-id="399e4-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="399e4-126">Request URI</span></span> |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="399e4-127">**GET**</span><span class="sxs-lookup"><span data-stu-id="399e4-127">**GET**</span></span> | <span data-ttu-id="399e4-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities/{Availability-ID}? ország = {országkód} http/1.1</span><span class="sxs-lookup"><span data-stu-id="399e4-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1</span></span>         |

### <a name="uri-parameter"></a><span data-ttu-id="399e4-129">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="399e4-129">URI parameter</span></span>

<span data-ttu-id="399e4-130">A következő elérési út és lekérdezési paraméterek használatával a rendelkezésre állási AZONOSÍTÓval kaphat egy adott rendelkezésre állást.</span><span class="sxs-lookup"><span data-stu-id="399e4-130">Use the following path and query parameters to get a specific availability using an availability ID.</span></span>

| <span data-ttu-id="399e4-131">Név</span><span class="sxs-lookup"><span data-stu-id="399e4-131">Name</span></span>                   | <span data-ttu-id="399e4-132">Típus</span><span class="sxs-lookup"><span data-stu-id="399e4-132">Type</span></span>     | <span data-ttu-id="399e4-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="399e4-133">Required</span></span> | <span data-ttu-id="399e4-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="399e4-134">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="399e4-135">termék azonosítója</span><span class="sxs-lookup"><span data-stu-id="399e4-135">product-id</span></span>             | <span data-ttu-id="399e4-136">sztring</span><span class="sxs-lookup"><span data-stu-id="399e4-136">string</span></span>   | <span data-ttu-id="399e4-137">Igen</span><span class="sxs-lookup"><span data-stu-id="399e4-137">Yes</span></span>      | <span data-ttu-id="399e4-138">Egy GUID formátumú karakterlánc, amely azonosítja a terméket.</span><span class="sxs-lookup"><span data-stu-id="399e4-138">A GUID formatted string that identifies the product.</span></span>            |
| <span data-ttu-id="399e4-139">SKU-azonosító</span><span class="sxs-lookup"><span data-stu-id="399e4-139">sku-id</span></span>                 | <span data-ttu-id="399e4-140">sztring</span><span class="sxs-lookup"><span data-stu-id="399e4-140">string</span></span>   | <span data-ttu-id="399e4-141">Igen</span><span class="sxs-lookup"><span data-stu-id="399e4-141">Yes</span></span>      | <span data-ttu-id="399e4-142">Egy GUID formátumú karakterlánc, amely azonosítja az SKU-t.</span><span class="sxs-lookup"><span data-stu-id="399e4-142">A GUID formatted string that identifies the SKU.</span></span>                |
| <span data-ttu-id="399e4-143">rendelkezésre állás – azonosító</span><span class="sxs-lookup"><span data-stu-id="399e4-143">availability-id</span></span>        | <span data-ttu-id="399e4-144">sztring</span><span class="sxs-lookup"><span data-stu-id="399e4-144">string</span></span>   | <span data-ttu-id="399e4-145">Igen</span><span class="sxs-lookup"><span data-stu-id="399e4-145">Yes</span></span>      | <span data-ttu-id="399e4-146">Egy GUID formátumú karakterlánc, amely azonosítja a rendelkezésre állást.</span><span class="sxs-lookup"><span data-stu-id="399e4-146">A GUID formatted string that identifies the availability.</span></span>       |
| <span data-ttu-id="399e4-147">országkód</span><span class="sxs-lookup"><span data-stu-id="399e4-147">country-code</span></span>           | <span data-ttu-id="399e4-148">sztring</span><span class="sxs-lookup"><span data-stu-id="399e4-148">string</span></span>   | <span data-ttu-id="399e4-149">Igen</span><span class="sxs-lookup"><span data-stu-id="399e4-149">Yes</span></span>      | <span data-ttu-id="399e4-150">Ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="399e4-150">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="399e4-151">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="399e4-151">Request headers</span></span>

<span data-ttu-id="399e4-152">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="399e4-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="399e4-153">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="399e4-153">Request body</span></span>

<span data-ttu-id="399e4-154">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="399e4-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="399e4-155">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="399e4-155">Request example</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="399e4-156">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="399e4-156">REST response</span></span>

<span data-ttu-id="399e4-157">Ha ez sikeres, a válasz törzse [rendelkezésre állási](product-resources.md#availability) erőforrást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="399e4-157">If successful, the response body contains an [Availability](product-resources.md#availability) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="399e4-158">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="399e4-158">Response success and error codes</span></span>

<span data-ttu-id="399e4-159">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="399e4-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="399e4-160">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="399e4-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="399e4-161">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="399e4-161">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="399e4-162">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="399e4-162">This method returns the following error codes:</span></span>

| <span data-ttu-id="399e4-163">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="399e4-163">HTTP Status Code</span></span>     | <span data-ttu-id="399e4-164">Hibakód</span><span class="sxs-lookup"><span data-stu-id="399e4-164">Error code</span></span>   | <span data-ttu-id="399e4-165">Leírás</span><span class="sxs-lookup"><span data-stu-id="399e4-165">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="399e4-166">404</span><span class="sxs-lookup"><span data-stu-id="399e4-166">404</span></span>                  | <span data-ttu-id="399e4-167">400013</span><span class="sxs-lookup"><span data-stu-id="399e4-167">400013</span></span>       | <span data-ttu-id="399e4-168">A termék nem található.</span><span class="sxs-lookup"><span data-stu-id="399e4-168">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="399e4-169">404</span><span class="sxs-lookup"><span data-stu-id="399e4-169">404</span></span>                  | <span data-ttu-id="399e4-170">400018</span><span class="sxs-lookup"><span data-stu-id="399e4-170">400018</span></span>       | <span data-ttu-id="399e4-171">Az SKU nem található.</span><span class="sxs-lookup"><span data-stu-id="399e4-171">Sku was not found.</span></span>                                                                                        |
| <span data-ttu-id="399e4-172">404</span><span class="sxs-lookup"><span data-stu-id="399e4-172">404</span></span>                  | <span data-ttu-id="399e4-173">400019</span><span class="sxs-lookup"><span data-stu-id="399e4-173">400019</span></span>       | <span data-ttu-id="399e4-174">A rendelkezésre állás nem található.</span><span class="sxs-lookup"><span data-stu-id="399e4-174">Availability not found.</span></span>                                                                                   |

### <a name="response-example"></a><span data-ttu-id="399e4-175">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="399e4-175">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
    "defaultCurrency": {
        "code": "USD",
        "symbol": "$"
    },
    "segment": "commercial",
    "country": "US",
    "isPurchasable": true,
    "isRenewable": false,
    "terms": [{
        "duration": "P1Y",
        "description": "1 Year Prepaid"
    }],
    "product": { ... },
    "sku": { ... },
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
