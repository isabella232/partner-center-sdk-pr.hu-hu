---
title: A rendelkezésre állás lekért azonosítója
description: Lekérte a megadott termék és termékváltozat rendelkezésre állását egy rendelkezésre állási azonosítóval.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c31bc12d8d484cc8042f36aa865145600d9e6738
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760198"
---
# <a name="get-the-availability-by-id"></a><span data-ttu-id="fd29e-103">A rendelkezésre állás lekért azonosítója</span><span class="sxs-lookup"><span data-stu-id="fd29e-103">Get the availability by ID</span></span>

<span data-ttu-id="fd29e-104">Lekérte a megadott termék és termékváltozat rendelkezésre állását egy rendelkezésre állási azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="fd29e-104">Gets the availability for the specified product and SKU using an availability ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd29e-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="fd29e-105">Prerequisites</span></span>

- <span data-ttu-id="fd29e-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fd29e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fd29e-107">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="fd29e-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fd29e-108">Egy termékazonosító.</span><span class="sxs-lookup"><span data-stu-id="fd29e-108">A product ID.</span></span>

- <span data-ttu-id="fd29e-109">Egy termékváltozat-azonosító.</span><span class="sxs-lookup"><span data-stu-id="fd29e-109">A SKU ID.</span></span>

- <span data-ttu-id="fd29e-110">Egy rendelkezésre állási azonosító.</span><span class="sxs-lookup"><span data-stu-id="fd29e-110">An availability ID.</span></span>

## <a name="c"></a><span data-ttu-id="fd29e-111">C\#</span><span class="sxs-lookup"><span data-stu-id="fd29e-111">C\#</span></span>

<span data-ttu-id="fd29e-112">Egy adott rendelkezésre [](product-resources.md#availability)állás részleteinek lekért [](get-a-sku-by-id.md) lépéseit a Termékváltozat lekért azonosítója alapján lépéseit követve szerezze be az adott [termékváltozat](product-resources.md#sku) műveleteihez szükséges felületet.</span><span class="sxs-lookup"><span data-stu-id="fd29e-112">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="fd29e-113">Az eredményül kapott felületen válassza az **Availabilities (Rendelkezésre** állások) tulajdonságot a rendelkezésre álláshoz elérhető műveletekkel való interfész beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="fd29e-113">From the resulting interface, select the **Availabilities** property to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="fd29e-114">Ezt követően adja át a rendelkezésre állási azonosítót a **ById()** metódusnak az adott rendelkezésre álláshoz szükséges műveletek lekérése érdekében, majd hívja meg a **Get()** vagy **a GetAsync()** metódust a rendelkezésre állási adatok lekérése érdekében.</span><span class="sxs-lookup"><span data-stu-id="fd29e-114">After that, pass the availability ID to the **ById()** method to get the operations for that specific availability and then call **Get()** or **GetAsync()** to retrieve the availability details.</span></span>

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a><span data-ttu-id="fd29e-115">Java</span><span class="sxs-lookup"><span data-stu-id="fd29e-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="fd29e-116">Egy adott rendelkezésre [](product-resources.md#availability)állás részleteinek lekért [](get-a-sku-by-id.md) lépéseit a Termékváltozat lekért azonosítója alapján lépéseit követve szerezze be az adott [termékváltozat](product-resources.md#sku) műveleteihez szükséges felületet.</span><span class="sxs-lookup"><span data-stu-id="fd29e-116">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="fd29e-117">Az eredményül kapott felületen válassza a **getAvailabilities** függvényt a rendelkezésre álláshoz elérhető műveletekkel való felület beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="fd29e-117">From the resulting interface, select the **getAvailabilities** function to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="fd29e-118">Ezután adja át a rendelkezésre állási azonosítót a **byId()** függvénynek az adott rendelkezésre álláshoz szükséges műveletek lekérése érdekében, majd hívja meg a get() függvényt a rendelkezésre állási adatok **lekérése** érdekében.</span><span class="sxs-lookup"><span data-stu-id="fd29e-118">After that, pass the availability ID to the **byId()** function to get the operations for that specific availability and then call the **get()** function to retrieve the availability details.</span></span>

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a><span data-ttu-id="fd29e-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd29e-119">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="fd29e-120">Egy adott rendelkezésre [](product-resources.md#availability)állás részleteinek lekérése érdekében hajtsa végre a [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) paramétert, és adja meg az **AvailabilityId,** **CountryCode,** **ProductId** és **SkuId** paramétereket a rendelkezésre állási adatok lekérése érdekében.</span><span class="sxs-lookup"><span data-stu-id="fd29e-120">To get details of a specific [availability](product-resources.md#availability), execute the [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) and specify the **AvailabilityId**, **CountryCode**, **ProductId**, and **SkuId** parameters to retrieve the availability details.</span></span>

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a><span data-ttu-id="fd29e-121">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="fd29e-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fd29e-122">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="fd29e-122">Request syntax</span></span>

| <span data-ttu-id="fd29e-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="fd29e-123">Method</span></span>  | <span data-ttu-id="fd29e-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="fd29e-124">Request URI</span></span> |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fd29e-125">**Kap**</span><span class="sxs-lookup"><span data-stu-id="fd29e-125">**GET**</span></span> | <span data-ttu-id="fd29e-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{termékazonosító}/termékváltozatok/{sku-id}/availabilities/{availability-id}?country={országkód} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fd29e-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1</span></span>         |

### <a name="uri-parameter"></a><span data-ttu-id="fd29e-127">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="fd29e-127">URI parameter</span></span>

<span data-ttu-id="fd29e-128">Az alábbi elérési út és lekérdezési paraméterek használatával lekérdezheti az adott rendelkezésre állást egy rendelkezésre állási azonosító használatával.</span><span class="sxs-lookup"><span data-stu-id="fd29e-128">Use the following path and query parameters to get a specific availability using an availability ID.</span></span>

| <span data-ttu-id="fd29e-129">Név</span><span class="sxs-lookup"><span data-stu-id="fd29e-129">Name</span></span>                   | <span data-ttu-id="fd29e-130">Típus</span><span class="sxs-lookup"><span data-stu-id="fd29e-130">Type</span></span>     | <span data-ttu-id="fd29e-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="fd29e-131">Required</span></span> | <span data-ttu-id="fd29e-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="fd29e-132">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="fd29e-133">termékazonosító</span><span class="sxs-lookup"><span data-stu-id="fd29e-133">product-id</span></span>             | <span data-ttu-id="fd29e-134">sztring</span><span class="sxs-lookup"><span data-stu-id="fd29e-134">string</span></span>   | <span data-ttu-id="fd29e-135">Igen</span><span class="sxs-lookup"><span data-stu-id="fd29e-135">Yes</span></span>      | <span data-ttu-id="fd29e-136">Egy GUID formátumú sztring, amely azonosítja a terméket.</span><span class="sxs-lookup"><span data-stu-id="fd29e-136">A GUID formatted string that identifies the product.</span></span>            |
| <span data-ttu-id="fd29e-137">sku-id</span><span class="sxs-lookup"><span data-stu-id="fd29e-137">sku-id</span></span>                 | <span data-ttu-id="fd29e-138">sztring</span><span class="sxs-lookup"><span data-stu-id="fd29e-138">string</span></span>   | <span data-ttu-id="fd29e-139">Igen</span><span class="sxs-lookup"><span data-stu-id="fd29e-139">Yes</span></span>      | <span data-ttu-id="fd29e-140">Egy GUID formátumú sztring, amely azonosítja a termékváltozatot.</span><span class="sxs-lookup"><span data-stu-id="fd29e-140">A GUID formatted string that identifies the SKU.</span></span>                |
| <span data-ttu-id="fd29e-141">rendelkezésre állási azonosító</span><span class="sxs-lookup"><span data-stu-id="fd29e-141">availability-id</span></span>        | <span data-ttu-id="fd29e-142">sztring</span><span class="sxs-lookup"><span data-stu-id="fd29e-142">string</span></span>   | <span data-ttu-id="fd29e-143">Igen</span><span class="sxs-lookup"><span data-stu-id="fd29e-143">Yes</span></span>      | <span data-ttu-id="fd29e-144">Egy GUID formátumú sztring, amely a rendelkezésre állást azonosítja.</span><span class="sxs-lookup"><span data-stu-id="fd29e-144">A GUID formatted string that identifies the availability.</span></span>       |
| <span data-ttu-id="fd29e-145">országkód</span><span class="sxs-lookup"><span data-stu-id="fd29e-145">country-code</span></span>           | <span data-ttu-id="fd29e-146">sztring</span><span class="sxs-lookup"><span data-stu-id="fd29e-146">string</span></span>   | <span data-ttu-id="fd29e-147">Igen</span><span class="sxs-lookup"><span data-stu-id="fd29e-147">Yes</span></span>      | <span data-ttu-id="fd29e-148">Egy ország-/régióazonosító.</span><span class="sxs-lookup"><span data-stu-id="fd29e-148">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="fd29e-149">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="fd29e-149">Request headers</span></span>

<span data-ttu-id="fd29e-150">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fd29e-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fd29e-151">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="fd29e-151">Request body</span></span>

<span data-ttu-id="fd29e-152">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="fd29e-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fd29e-153">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="fd29e-153">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="fd29e-154">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="fd29e-154">REST response</span></span>

<span data-ttu-id="fd29e-155">Ha ez sikeres, a válasz törzse tartalmaz egy [rendelkezésre állási erőforrást.](product-resources.md#availability)</span><span class="sxs-lookup"><span data-stu-id="fd29e-155">If successful, the response body contains an [Availability](product-resources.md#availability) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fd29e-156">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="fd29e-156">Response success and error codes</span></span>

<span data-ttu-id="fd29e-157">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="fd29e-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fd29e-158">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="fd29e-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fd29e-159">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fd29e-159">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="fd29e-160">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="fd29e-160">This method returns the following error codes:</span></span>

| <span data-ttu-id="fd29e-161">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="fd29e-161">HTTP Status Code</span></span>     | <span data-ttu-id="fd29e-162">Hibakód</span><span class="sxs-lookup"><span data-stu-id="fd29e-162">Error code</span></span>   | <span data-ttu-id="fd29e-163">Leírás</span><span class="sxs-lookup"><span data-stu-id="fd29e-163">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fd29e-164">404</span><span class="sxs-lookup"><span data-stu-id="fd29e-164">404</span></span>                  | <span data-ttu-id="fd29e-165">400013</span><span class="sxs-lookup"><span data-stu-id="fd29e-165">400013</span></span>       | <span data-ttu-id="fd29e-166">A termék nem található.</span><span class="sxs-lookup"><span data-stu-id="fd29e-166">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="fd29e-167">404</span><span class="sxs-lookup"><span data-stu-id="fd29e-167">404</span></span>                  | <span data-ttu-id="fd29e-168">400018</span><span class="sxs-lookup"><span data-stu-id="fd29e-168">400018</span></span>       | <span data-ttu-id="fd29e-169">A termékváltozat nem található.</span><span class="sxs-lookup"><span data-stu-id="fd29e-169">SKU was not found.</span></span>                                                                                        |
| <span data-ttu-id="fd29e-170">404</span><span class="sxs-lookup"><span data-stu-id="fd29e-170">404</span></span>                  | <span data-ttu-id="fd29e-171">400019</span><span class="sxs-lookup"><span data-stu-id="fd29e-171">400019</span></span>       | <span data-ttu-id="fd29e-172">A rendelkezésre állás nem található.</span><span class="sxs-lookup"><span data-stu-id="fd29e-172">Availability not found.</span></span>                                                                                   |

### <a name="response-example"></a><span data-ttu-id="fd29e-173">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="fd29e-173">Response example</span></span>

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
