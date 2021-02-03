---
title: Egy termék lekérése azonosító alapján
description: A megadott termék-erőforrás beolvasása termékazonosító használatával.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 8aca626597e9ec903ebecca7d55577ba636c518e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767896"
---
# <a name="get-a-product-by-id"></a><span data-ttu-id="b271e-103">Egy termék lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="b271e-103">Get a product by ID</span></span>

<span data-ttu-id="b271e-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="b271e-104">**Applies To**</span></span>

- <span data-ttu-id="b271e-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="b271e-105">Partner Center</span></span>

<span data-ttu-id="b271e-106">A megadott termék-erőforrás beolvasása termékazonosító használatával.</span><span class="sxs-lookup"><span data-stu-id="b271e-106">Gets the specified product resource using a product ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b271e-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b271e-107">Prerequisites</span></span>

- <span data-ttu-id="b271e-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="b271e-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b271e-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="b271e-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b271e-110">A termék azonosítója.</span><span class="sxs-lookup"><span data-stu-id="b271e-110">A product ID.</span></span>

## <a name="c"></a><span data-ttu-id="b271e-111">C\#</span><span class="sxs-lookup"><span data-stu-id="b271e-111">C\#</span></span>

<span data-ttu-id="b271e-112">Ha azonosító alapján szeretne megkeresni egy adott terméket, használja a **IAggregatePartner. Products** gyűjteményt, válassza ki az országot a **ByCountry ()** metódus használatával, majd hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="b271e-112">To find a specific product by ID, use your **IAggregatePartner.Products** collection, select the country by using the **ByCountry()** method, then call the **ById()** method.</span></span> <span data-ttu-id="b271e-113">Végül hívja a **Get ()** vagy a **GetAsync ()** metódust a termék visszaküldéséhez.</span><span class="sxs-lookup"><span data-stu-id="b271e-113">Finally, call the **Get()** or **GetAsync()** method to return the product.</span></span>

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a><span data-ttu-id="b271e-114">Java</span><span class="sxs-lookup"><span data-stu-id="b271e-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="b271e-115">Ha azonosító alapján szeretne megkeresni egy adott terméket, használja a **IAggregatePartner. getProducts** függvényt, válassza ki az országot a **byCountry ()** függvény használatával, majd hívja meg a **byId ()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="b271e-115">To find a specific product by ID, use your **IAggregatePartner.getProducts** function, select the country by using the **byCountry()** function, then call the **byId()** function.</span></span> <span data-ttu-id="b271e-116">Végül hívja meg a **Get ()** függvényt a termék visszaküldéséhez.</span><span class="sxs-lookup"><span data-stu-id="b271e-116">Finally, call the **get()** function to return the product.</span></span>

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a><span data-ttu-id="b271e-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b271e-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="b271e-118">Ha azonosító alapján szeretne megkeresni egy adott terméket, hajtsa végre a [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) parancsot, és határozza meg a **Termékkód** paramétert.</span><span class="sxs-lookup"><span data-stu-id="b271e-118">To find a specific product by ID, execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command and specify the **ProductId** parameter.</span></span> <span data-ttu-id="b271e-119">Ha nincs megadva a **országhívószám** paraméter, a rendszer a viszonteladóhoz társított országot fogja használni.</span><span class="sxs-lookup"><span data-stu-id="b271e-119">The **CountryCode** parameter is options, if it isn't specified then the country associated with the reseller will be used.</span></span>

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a><span data-ttu-id="b271e-120">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="b271e-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b271e-121">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b271e-121">Request syntax</span></span>

| <span data-ttu-id="b271e-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="b271e-122">Method</span></span>  | <span data-ttu-id="b271e-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b271e-123">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="b271e-124">**GET**</span><span class="sxs-lookup"><span data-stu-id="b271e-124">**GET**</span></span> | <span data-ttu-id="b271e-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}? ország = {ország} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b271e-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="b271e-126">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="b271e-126">URI parameter</span></span>

<span data-ttu-id="b271e-127">A megadott termék beolvasásához használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="b271e-127">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="b271e-128">Név</span><span class="sxs-lookup"><span data-stu-id="b271e-128">Name</span></span>                   | <span data-ttu-id="b271e-129">Típus</span><span class="sxs-lookup"><span data-stu-id="b271e-129">Type</span></span>     | <span data-ttu-id="b271e-130">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b271e-130">Required</span></span> | <span data-ttu-id="b271e-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="b271e-131">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="b271e-132">termék azonosítója</span><span class="sxs-lookup"><span data-stu-id="b271e-132">product-id</span></span>             | <span data-ttu-id="b271e-133">sztring</span><span class="sxs-lookup"><span data-stu-id="b271e-133">string</span></span>   | <span data-ttu-id="b271e-134">Igen</span><span class="sxs-lookup"><span data-stu-id="b271e-134">Yes</span></span>      | <span data-ttu-id="b271e-135">A terméket azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="b271e-135">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="b271e-136">ország</span><span class="sxs-lookup"><span data-stu-id="b271e-136">country</span></span>                | <span data-ttu-id="b271e-137">sztring</span><span class="sxs-lookup"><span data-stu-id="b271e-137">string</span></span>   | <span data-ttu-id="b271e-138">Igen</span><span class="sxs-lookup"><span data-stu-id="b271e-138">Yes</span></span>      | <span data-ttu-id="b271e-139">Ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="b271e-139">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="b271e-140">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b271e-140">Request headers</span></span>

<span data-ttu-id="b271e-141">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b271e-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b271e-142">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b271e-142">Request body</span></span>

<span data-ttu-id="b271e-143">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b271e-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b271e-144">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b271e-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="b271e-145">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b271e-145">REST response</span></span>

<span data-ttu-id="b271e-146">Ha ez sikeres, a válasz törzse tartalmazza a [termék](product-resources.md#product) erőforrását.</span><span class="sxs-lookup"><span data-stu-id="b271e-146">If successful, the response body contains a [Product](product-resources.md#product) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b271e-147">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b271e-147">Response success and error codes</span></span>

<span data-ttu-id="b271e-148">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="b271e-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b271e-149">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="b271e-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b271e-150">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b271e-150">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="b271e-151">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="b271e-151">This method returns the following error codes:</span></span>

| <span data-ttu-id="b271e-152">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="b271e-152">HTTP Status Code</span></span>     | <span data-ttu-id="b271e-153">Hibakód</span><span class="sxs-lookup"><span data-stu-id="b271e-153">Error code</span></span>   | <span data-ttu-id="b271e-154">Leírás</span><span class="sxs-lookup"><span data-stu-id="b271e-154">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="b271e-155">404</span><span class="sxs-lookup"><span data-stu-id="b271e-155">404</span></span>                  | <span data-ttu-id="b271e-156">400013</span><span class="sxs-lookup"><span data-stu-id="b271e-156">400013</span></span>       | <span data-ttu-id="b271e-157">A termék nem található.</span><span class="sxs-lookup"><span data-stu-id="b271e-157">Product was not found.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="b271e-158">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b271e-158">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "DZH318Z0BQ3Q",
    "title": "Virtual Machines DSv2 Series",
    "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "VirtualMachines",
            "displayName": "VirtualMachines"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3Q?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
