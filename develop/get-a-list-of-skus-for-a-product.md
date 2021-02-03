---
title: Egy termék termékváltozatait tartalmazó lista lekérése (ország alapján)
description: A partner Center API-k használatával lekérheti és szűrheti az SKU-k egy adott termék ország szerinti gyűjteményét.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9d5ec9172ed92d33e6ff291eafd523cbc13bfbbd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767936"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a><span data-ttu-id="2a429-103">Egy termék termékváltozatait tartalmazó lista lekérése (ország alapján)</span><span class="sxs-lookup"><span data-stu-id="2a429-103">Get a list of SKUs for a product (by country)</span></span>

<span data-ttu-id="2a429-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="2a429-104">**Applies to:**</span></span>

- <span data-ttu-id="2a429-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="2a429-105">Partner Center</span></span>

<span data-ttu-id="2a429-106">A partner Center API-k használatával egy adott termékhez tartozó SKU-k gyűjteményét is beszerezheti egy adott országban.</span><span class="sxs-lookup"><span data-stu-id="2a429-106">You can get a collection of SKUs available in a country for a specific product using Partner Center APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a429-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2a429-107">Prerequisites</span></span>

- <span data-ttu-id="2a429-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="2a429-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2a429-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="2a429-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2a429-110">A termék azonosítója.</span><span class="sxs-lookup"><span data-stu-id="2a429-110">A product identifier.</span></span>

## <a name="c"></a><span data-ttu-id="2a429-111">C\#</span><span class="sxs-lookup"><span data-stu-id="2a429-111">C\#</span></span>

<span data-ttu-id="2a429-112">A termékhez tartozó SKU-termékek listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="2a429-112">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="2a429-113">Szerezzen be egy felületet egy adott termék műveleteihez a [termék beolvasása azonosító alapján](get-a-product-by-id.md)című rész lépéseit követve.</span><span class="sxs-lookup"><span data-stu-id="2a429-113">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="2a429-114">A csatolón válassza a **SKUs** tulajdonságot, hogy beszerezze a csatolót az SKU-hoz elérhető műveletekkel.</span><span class="sxs-lookup"><span data-stu-id="2a429-114">From the interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="2a429-115">Hívja meg a **Get ()** vagy a **GetAsync ()** metódust, hogy lekérje a termékhez rendelkezésre álló SKU-gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="2a429-115">Call the **Get()** or **GetAsync()** method to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="2a429-116">Választható Válassza ki a foglalási hatókört a **ByReservationScope ()** metódus használatával.</span><span class="sxs-lookup"><span data-stu-id="2a429-116">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

5. <span data-ttu-id="2a429-117">Választható A **Get (** ) vagy a **GetAsync ()** hívása előtt a **ByTargetSegment ()** metódus használatával szűrheti a SKU-ket a célként megadott szegmens alapján.</span><span class="sxs-lookup"><span data-stu-id="2a429-117">(Optional) Use the **ByTargetSegment()** method to filter the SKUs by target segment before calling **Get()** or **GetAsync()**.</span></span>

``` csharp
IAggregatePartner partnerOperations;

string countryCode;
string productId;
string productIdForAzureReservation;
string targetSegment;

// Get the available SKUs.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.Get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ByTargetSegment(targetSegment).Get();

// Get the skus for an Azure reservation product which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.Get();

// Get the skus for an Azure reservation product which are applicable to Azure plans only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a><span data-ttu-id="2a429-118">Java</span><span class="sxs-lookup"><span data-stu-id="2a429-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="2a429-119">A termékhez tartozó SKU-termékek listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="2a429-119">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="2a429-120">Szerezzen be egy felületet egy adott termék műveleteihez a [termék beolvasása azonosító alapján](get-a-product-by-id.md)című rész lépéseit követve.</span><span class="sxs-lookup"><span data-stu-id="2a429-120">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="2a429-121">A csatolón válassza a **getSkus** függvényt, és szerezzen be egy felületet az SKU-hoz elérhető műveletekkel.</span><span class="sxs-lookup"><span data-stu-id="2a429-121">From the interface, select the **getSkus** function to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="2a429-122">A **Get ()** függvény meghívásával lekérheti a termékhez rendelkezésre álló SKU-gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="2a429-122">Call the **get()** function to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="2a429-123">Választható A **Get ()** függvény hívása előtt a **byTargetSegment ()** függvénnyel szűrheti az SKU-ket a célként megadott szegmens alapján.</span><span class="sxs-lookup"><span data-stu-id="2a429-123">(Optional) Use the **byTargetSegment()** function to filter the SKUs by target segment before calling the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

// String countryCode;
// String productId;
// String targetSegment;

// Get the available SKUs.
ResourceCollection<Sku> skus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byTargetSegment(targetSegment).get();
```

## <a name="powershell"></a><span data-ttu-id="2a429-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a429-124">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="2a429-125">A termékhez tartozó SKU-termékek listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="2a429-125">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="2a429-126">Futtassa a [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) parancsot.</span><span class="sxs-lookup"><span data-stu-id="2a429-126">Execute the [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) command.</span></span>

2. <span data-ttu-id="2a429-127">Választható A **szegmens** paraméter megadásával szűrheti az SKU-ket a célként megadott szegmens alapján.</span><span class="sxs-lookup"><span data-stu-id="2a429-127">(Optional) Specify the **Segment** parameter to filter the SKUs by target segment.</span></span>

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a><span data-ttu-id="2a429-128">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="2a429-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2a429-129">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="2a429-129">Request syntax</span></span>

| <span data-ttu-id="2a429-130">Metódus</span><span class="sxs-lookup"><span data-stu-id="2a429-130">Method</span></span>  | <span data-ttu-id="2a429-131">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2a429-131">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2a429-132">**GET**</span><span class="sxs-lookup"><span data-stu-id="2a429-132">**GET**</span></span> | <span data-ttu-id="2a429-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs? ország = {országkód} &targetSegment = {Target-szegmens} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2a429-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="2a429-134">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="2a429-134">URI parameters</span></span>

<span data-ttu-id="2a429-135">A következő elérési út és lekérdezési paraméterek segítségével szerezzen be egy termék SKU-listáját.</span><span class="sxs-lookup"><span data-stu-id="2a429-135">Use the following path and query parameters to get a list of SKUs for a product.</span></span>

| <span data-ttu-id="2a429-136">Név</span><span class="sxs-lookup"><span data-stu-id="2a429-136">Name</span></span>                   | <span data-ttu-id="2a429-137">Típus</span><span class="sxs-lookup"><span data-stu-id="2a429-137">Type</span></span>     | <span data-ttu-id="2a429-138">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2a429-138">Required</span></span> | <span data-ttu-id="2a429-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="2a429-139">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="2a429-140">termék azonosítója</span><span class="sxs-lookup"><span data-stu-id="2a429-140">product-id</span></span>             | <span data-ttu-id="2a429-141">sztring</span><span class="sxs-lookup"><span data-stu-id="2a429-141">string</span></span>   | <span data-ttu-id="2a429-142">Igen</span><span class="sxs-lookup"><span data-stu-id="2a429-142">Yes</span></span>      | <span data-ttu-id="2a429-143">A terméket azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="2a429-143">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="2a429-144">országkód</span><span class="sxs-lookup"><span data-stu-id="2a429-144">country-code</span></span>           | <span data-ttu-id="2a429-145">sztring</span><span class="sxs-lookup"><span data-stu-id="2a429-145">string</span></span>   | <span data-ttu-id="2a429-146">Igen</span><span class="sxs-lookup"><span data-stu-id="2a429-146">Yes</span></span>      | <span data-ttu-id="2a429-147">Ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="2a429-147">A country/region ID.</span></span>                                            |
| <span data-ttu-id="2a429-148">cél szegmens</span><span class="sxs-lookup"><span data-stu-id="2a429-148">target-segment</span></span>         | <span data-ttu-id="2a429-149">sztring</span><span class="sxs-lookup"><span data-stu-id="2a429-149">string</span></span>   | <span data-ttu-id="2a429-150">No</span><span class="sxs-lookup"><span data-stu-id="2a429-150">No</span></span>       | <span data-ttu-id="2a429-151">A szűréshez használt cél szegmenst azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="2a429-151">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="2a429-152">reservationScope</span><span class="sxs-lookup"><span data-stu-id="2a429-152">reservationScope</span></span> | <span data-ttu-id="2a429-153">sztring</span><span class="sxs-lookup"><span data-stu-id="2a429-153">string</span></span>   | <span data-ttu-id="2a429-154">No</span><span class="sxs-lookup"><span data-stu-id="2a429-154">No</span></span> | <span data-ttu-id="2a429-155">Ha egy Azure-beli foglalási termékhez tartozó SKU-ket szeretne lekérdezni, akkor a AzurePlan vonatkozó SKU-lista lekéréséhez válassza a következőt: `reservationScope=AzurePlan` .</span><span class="sxs-lookup"><span data-stu-id="2a429-155">When querying for a list of SKUs for an Azure Reservation product, specify `reservationScope=AzurePlan` to get a list of SKUs which are applicable to AzurePlan.</span></span> <span data-ttu-id="2a429-156">Zárja be ezt a paramétert egy olyan Azure-beli foglalási termék SKU-listájának lekéréséhez, amely Microsoft Azure (MS-AZR-0145P) előfizetésekre alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="2a429-156">Exclude this parameter to get a list of SKUs for an Azure Reservation products which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="2a429-157">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2a429-157">Request headers</span></span>

<span data-ttu-id="2a429-158">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2a429-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2a429-159">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2a429-159">Request body</span></span>

<span data-ttu-id="2a429-160">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="2a429-160">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="2a429-161">Példák kérése</span><span class="sxs-lookup"><span data-stu-id="2a429-161">Request examples</span></span>

<span data-ttu-id="2a429-162">Egy adott termék SKU-listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="2a429-162">Get a list of SKUs for a given product:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="2a429-163">Egy Azure-beli foglalási termék SKU-i listájának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="2a429-163">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="2a429-164">Csak az Azure-csomagokra érvényes SKU-ket és nem Microsoft Azure (MS-AZR-0145P) előfizetéseket tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="2a429-164">Only include the SKUs which are applicable to Azure plans and not Microsoft Azure (MS-AZR-0145P) subscriptions:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="2a429-165">Egy Azure-beli foglalási termék SKU-i listájának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="2a429-165">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="2a429-166">Csak a Microsoft Azure (MS-AZR-0145P) előfizetésekre és nem Azure-csomagokra alkalmazandó SKU-ket foglalja bele:</span><span class="sxs-lookup"><span data-stu-id="2a429-166">Only include the SKUs which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions and not Azure plans:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a><span data-ttu-id="2a429-167">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2a429-167">REST response</span></span>

<span data-ttu-id="2a429-168">Ha ez sikeres, a válasz törzse [SKU](product-resources.md#sku) -erőforrások gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="2a429-168">If successful, the response body contains a collection of [SKU](product-resources.md#sku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2a429-169">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2a429-169">Response success and error codes</span></span>

<span data-ttu-id="2a429-170">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="2a429-170">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2a429-171">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="2a429-171">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2a429-172">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2a429-172">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="2a429-173">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="2a429-173">This method returns the following error codes:</span></span>

| <span data-ttu-id="2a429-174">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="2a429-174">HTTP Status Code</span></span>     | <span data-ttu-id="2a429-175">Hibakód</span><span class="sxs-lookup"><span data-stu-id="2a429-175">Error code</span></span>   | <span data-ttu-id="2a429-176">Leírás</span><span class="sxs-lookup"><span data-stu-id="2a429-176">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2a429-177">403</span><span class="sxs-lookup"><span data-stu-id="2a429-177">403</span></span>                  | <span data-ttu-id="2a429-178">400030</span><span class="sxs-lookup"><span data-stu-id="2a429-178">400030</span></span>       | <span data-ttu-id="2a429-179">A kért targetSegment való hozzáférés nem engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="2a429-179">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="2a429-180">404</span><span class="sxs-lookup"><span data-stu-id="2a429-180">404</span></span>                  | <span data-ttu-id="2a429-181">400013</span><span class="sxs-lookup"><span data-stu-id="2a429-181">400013</span></span>       | <span data-ttu-id="2a429-182">A fölérendelt termék nem található.</span><span class="sxs-lookup"><span data-stu-id="2a429-182">The parent product was not found.</span></span>                                                                         |

### <a name="response-example"></a><span data-ttu-id="2a429-183">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2a429-183">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51,e75c1060-852e-4b49-92b0-cd15167a0d51
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d,18b41adf-29b5-48eb-b14f-c9683a4e5b7d
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTVTXHNrdXM=?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 21:06:03 GMT
Content-Length: 50917

{
    "totalCount": 40,
    "items": [
        {
            "id": "0001",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND12s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND12s, US West 2, 1 Year",
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
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND12s",
                "cores": "12",
                "ram": "224",
                "skuDisplayName": "ND12",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0002",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND6s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND6s, US West 2, 1 Year",
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
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND6s",
                "cores": "6",
                "ram": "112",
                "skuDisplayName": "ND6",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
            "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
        [...]
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ5S/skus?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
