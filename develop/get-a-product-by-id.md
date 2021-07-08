---
title: Egy termék lekérése azonosító alapján
description: Lekérte a megadott termékerőforrást egy termékazonosítóval.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 769a4307dc3cebdc7ebbdcf51d9f2b67a9f4b7c2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874023"
---
# <a name="get-a-product-by-id"></a><span data-ttu-id="dd478-103">Egy termék lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="dd478-103">Get a product by ID</span></span>

<span data-ttu-id="dd478-104">Lekérte a megadott termékerőforrást egy termékazonosítóval.</span><span class="sxs-lookup"><span data-stu-id="dd478-104">Gets the specified product resource using a product ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd478-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="dd478-105">Prerequisites</span></span>

- <span data-ttu-id="dd478-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="dd478-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dd478-107">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="dd478-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="dd478-108">Egy termékazonosító.</span><span class="sxs-lookup"><span data-stu-id="dd478-108">A product ID.</span></span>

## <a name="c"></a><span data-ttu-id="dd478-109">C\#</span><span class="sxs-lookup"><span data-stu-id="dd478-109">C\#</span></span>

<span data-ttu-id="dd478-110">Egy adott termék azonosító alapján való megkereséhez használja az **IAggregatePartner.Products** gyűjteményt, válassza ki az országot a **ByCountry()** metódussal, majd hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="dd478-110">To find a specific product by ID, use your **IAggregatePartner.Products** collection, select the country by using the **ByCountry()** method, then call the **ById()** method.</span></span> <span data-ttu-id="dd478-111">Végül hívja meg a **Get() vagy** **a GetAsync()** metódust a termék visszaküldésére.</span><span class="sxs-lookup"><span data-stu-id="dd478-111">Finally, call the **Get()** or **GetAsync()** method to return the product.</span></span>

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a><span data-ttu-id="dd478-112">Java</span><span class="sxs-lookup"><span data-stu-id="dd478-112">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="dd478-113">Ha azonosító alapján keres egy adott terméket, használja az **IAggregatePartner.getProducts** függvényt, válassza ki az országot a **byCountry()** függvény használatával, majd hívja meg a **byId()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="dd478-113">To find a specific product by ID, use your **IAggregatePartner.getProducts** function, select the country by using the **byCountry()** function, then call the **byId()** function.</span></span> <span data-ttu-id="dd478-114">Végül hívja meg a **get()** függvényt a termék visszaküldésére.</span><span class="sxs-lookup"><span data-stu-id="dd478-114">Finally, call the **get()** function to return the product.</span></span>

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a><span data-ttu-id="dd478-115">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd478-115">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="dd478-116">Ha azonosító alapján keres egy adott terméket, hajtsa végre a [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) parancsot, és adja meg a **ProductId paramétert.**</span><span class="sxs-lookup"><span data-stu-id="dd478-116">To find a specific product by ID, execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command and specify the **ProductId** parameter.</span></span> <span data-ttu-id="dd478-117">A **CountryCode** paraméter beállítások, ha nincs megadva, akkor a viszonteladóhoz társított ország lesz használva.</span><span class="sxs-lookup"><span data-stu-id="dd478-117">The **CountryCode** parameter is options, if it isn't specified then the country associated with the reseller will be used.</span></span>

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a><span data-ttu-id="dd478-118">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="dd478-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dd478-119">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="dd478-119">Request syntax</span></span>

| <span data-ttu-id="dd478-120">Metódus</span><span class="sxs-lookup"><span data-stu-id="dd478-120">Method</span></span>  | <span data-ttu-id="dd478-121">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="dd478-121">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="dd478-122">**Kap**</span><span class="sxs-lookup"><span data-stu-id="dd478-122">**GET**</span></span> | <span data-ttu-id="dd478-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{termékazonosító}?country={country} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="dd478-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="dd478-124">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="dd478-124">URI parameter</span></span>

<span data-ttu-id="dd478-125">A megadott termék lekért értékével az alábbi elérésiút-paramétereket használhatja.</span><span class="sxs-lookup"><span data-stu-id="dd478-125">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="dd478-126">Név</span><span class="sxs-lookup"><span data-stu-id="dd478-126">Name</span></span>                   | <span data-ttu-id="dd478-127">Típus</span><span class="sxs-lookup"><span data-stu-id="dd478-127">Type</span></span>     | <span data-ttu-id="dd478-128">Kötelező</span><span class="sxs-lookup"><span data-stu-id="dd478-128">Required</span></span> | <span data-ttu-id="dd478-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="dd478-129">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="dd478-130">termékazonosító</span><span class="sxs-lookup"><span data-stu-id="dd478-130">product-id</span></span>             | <span data-ttu-id="dd478-131">sztring</span><span class="sxs-lookup"><span data-stu-id="dd478-131">string</span></span>   | <span data-ttu-id="dd478-132">Igen</span><span class="sxs-lookup"><span data-stu-id="dd478-132">Yes</span></span>      | <span data-ttu-id="dd478-133">A terméket azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="dd478-133">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="dd478-134">ország</span><span class="sxs-lookup"><span data-stu-id="dd478-134">country</span></span>                | <span data-ttu-id="dd478-135">sztring</span><span class="sxs-lookup"><span data-stu-id="dd478-135">string</span></span>   | <span data-ttu-id="dd478-136">Igen</span><span class="sxs-lookup"><span data-stu-id="dd478-136">Yes</span></span>      | <span data-ttu-id="dd478-137">Egy ország-/régióazonosító.</span><span class="sxs-lookup"><span data-stu-id="dd478-137">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="dd478-138">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="dd478-138">Request headers</span></span>

<span data-ttu-id="dd478-139">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="dd478-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dd478-140">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="dd478-140">Request body</span></span>

<span data-ttu-id="dd478-141">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="dd478-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="dd478-142">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="dd478-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="dd478-143">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="dd478-143">REST response</span></span>

<span data-ttu-id="dd478-144">Ha ez sikeres, a válasz törzse tartalmaz egy [Product erőforrást.](product-resources.md#product)</span><span class="sxs-lookup"><span data-stu-id="dd478-144">If successful, the response body contains a [Product](product-resources.md#product) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dd478-145">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="dd478-145">Response success and error codes</span></span>

<span data-ttu-id="dd478-146">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="dd478-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dd478-147">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="dd478-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dd478-148">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dd478-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="dd478-149">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="dd478-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="dd478-150">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="dd478-150">HTTP Status Code</span></span>     | <span data-ttu-id="dd478-151">Hibakód</span><span class="sxs-lookup"><span data-stu-id="dd478-151">Error code</span></span>   | <span data-ttu-id="dd478-152">Leírás</span><span class="sxs-lookup"><span data-stu-id="dd478-152">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="dd478-153">404</span><span class="sxs-lookup"><span data-stu-id="dd478-153">404</span></span>                  | <span data-ttu-id="dd478-154">400013</span><span class="sxs-lookup"><span data-stu-id="dd478-154">400013</span></span>       | <span data-ttu-id="dd478-155">A termék nem található.</span><span class="sxs-lookup"><span data-stu-id="dd478-155">Product was not found.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="dd478-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="dd478-156">Response example</span></span>

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
