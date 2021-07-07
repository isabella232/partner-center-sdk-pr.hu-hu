---
title: Egy termék termékváltozatait tartalmazó lista lekérése (ország alapján)
description: Termék termék termékgyűjteményét országonként is lekérte és szűrheti a Partnerközpont API-k használatával.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 27a2391a22a9439461fb53764b87c1cafa68b875
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873887"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a><span data-ttu-id="d705d-103">Egy termék termékváltozatait tartalmazó lista lekérése (ország alapján)</span><span class="sxs-lookup"><span data-stu-id="d705d-103">Get a list of SKUs for a product (by country)</span></span>

<span data-ttu-id="d705d-104">Egy adott termékhez egy adott országban elérhető terméktermékgyűjteményt az API-k használatával Partnerközpont le.</span><span class="sxs-lookup"><span data-stu-id="d705d-104">You can get a collection of SKUs available in a country for a specific product using Partner Center APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d705d-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d705d-105">Prerequisites</span></span>

- <span data-ttu-id="d705d-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d705d-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d705d-107">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="d705d-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d705d-108">Egy termékazonosító.</span><span class="sxs-lookup"><span data-stu-id="d705d-108">A product identifier.</span></span>

## <a name="c"></a><span data-ttu-id="d705d-109">C\#</span><span class="sxs-lookup"><span data-stu-id="d705d-109">C\#</span></span>

<span data-ttu-id="d705d-110">Egy termék termék termékterméklistáinak lekért listája:</span><span class="sxs-lookup"><span data-stu-id="d705d-110">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="d705d-111">Szerezze be egy adott termék műveleteinek interfészét a Termék lekért azonosítója [alapján lépéseit követve.](get-a-product-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="d705d-111">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="d705d-112">A felületről válassza ki a Skus tulajdonságot a **SKUS-hoz** elérhető műveletekkel való interfész beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="d705d-112">From the interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="d705d-113">Hívja meg **a Get() vagy** **a GetAsync()** metódust a termékhez elérhető termékkódok gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="d705d-113">Call the **Get()** or **GetAsync()** method to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="d705d-114">(Nem kötelező) Válassza ki a foglalási hatókört a **ByReservationScope() metódussal.**</span><span class="sxs-lookup"><span data-stu-id="d705d-114">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

5. <span data-ttu-id="d705d-115">(Nem kötelező) A **ByTargetSegment()** metódussal szűrheti a SKUs-okat célszegmens szerint a **Get()** vagy **a GetAsync() hívása előtt.**</span><span class="sxs-lookup"><span data-stu-id="d705d-115">(Optional) Use the **ByTargetSegment()** method to filter the SKUs by target segment before calling **Get()** or **GetAsync()**.</span></span>

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

## <a name="java"></a><span data-ttu-id="d705d-116">Java</span><span class="sxs-lookup"><span data-stu-id="d705d-116">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="d705d-117">Egy termék termék termékterméklistáinak lekért listája:</span><span class="sxs-lookup"><span data-stu-id="d705d-117">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="d705d-118">Szerezze be egy adott termék műveleteinek interfészét a Termék lekért azonosítója [alapján lépéseit követve.](get-a-product-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="d705d-118">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="d705d-119">A felületen válassza ki a **getSkus** függvényt, hogy be tudja szerezni a rendelkezésre álló műveleteket a SKUs-hez.</span><span class="sxs-lookup"><span data-stu-id="d705d-119">From the interface, select the **getSkus** function to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="d705d-120">Hívja meg a **get()** függvényt a termékhez elérhető termékkódok gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="d705d-120">Call the **get()** function to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="d705d-121">(Nem kötelező) A **byTargetSegment()** függvény használatával szűrheti a SKUs-okat célszegmens szerint a **get()** függvény hívása előtt.</span><span class="sxs-lookup"><span data-stu-id="d705d-121">(Optional) Use the **byTargetSegment()** function to filter the SKUs by target segment before calling the **get()** function.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="d705d-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d705d-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="d705d-123">Egy termék termék termékterméklistáinak lekért listája:</span><span class="sxs-lookup"><span data-stu-id="d705d-123">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="d705d-124">Hajtsa végre [**a Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) parancsot.</span><span class="sxs-lookup"><span data-stu-id="d705d-124">Execute the [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) command.</span></span>

2. <span data-ttu-id="d705d-125">(Nem kötelező) Adja meg **a Szegmens** paramétert a SKUs célszegmens alapján való szűréséhez.</span><span class="sxs-lookup"><span data-stu-id="d705d-125">(Optional) Specify the **Segment** parameter to filter the SKUs by target segment.</span></span>

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a><span data-ttu-id="d705d-126">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d705d-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d705d-127">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="d705d-127">Request syntax</span></span>

| <span data-ttu-id="d705d-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="d705d-128">Method</span></span>  | <span data-ttu-id="d705d-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d705d-129">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d705d-130">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d705d-130">**GET**</span></span> | <span data-ttu-id="d705d-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{termékazonosító}/termékkód?country={országkód}&targetSegment={target-segment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d705d-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="d705d-132">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="d705d-132">URI parameters</span></span>

<span data-ttu-id="d705d-133">Az alábbi elérési út és lekérdezési paraméterek használatával lekérdezheti egy terméktermékének listáját.</span><span class="sxs-lookup"><span data-stu-id="d705d-133">Use the following path and query parameters to get a list of SKUs for a product.</span></span>

| <span data-ttu-id="d705d-134">Név</span><span class="sxs-lookup"><span data-stu-id="d705d-134">Name</span></span>                   | <span data-ttu-id="d705d-135">Típus</span><span class="sxs-lookup"><span data-stu-id="d705d-135">Type</span></span>     | <span data-ttu-id="d705d-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d705d-136">Required</span></span> | <span data-ttu-id="d705d-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="d705d-137">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="d705d-138">termékazonosító</span><span class="sxs-lookup"><span data-stu-id="d705d-138">product-id</span></span>             | <span data-ttu-id="d705d-139">sztring</span><span class="sxs-lookup"><span data-stu-id="d705d-139">string</span></span>   | <span data-ttu-id="d705d-140">Igen</span><span class="sxs-lookup"><span data-stu-id="d705d-140">Yes</span></span>      | <span data-ttu-id="d705d-141">A terméket azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="d705d-141">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="d705d-142">országkód</span><span class="sxs-lookup"><span data-stu-id="d705d-142">country-code</span></span>           | <span data-ttu-id="d705d-143">sztring</span><span class="sxs-lookup"><span data-stu-id="d705d-143">string</span></span>   | <span data-ttu-id="d705d-144">Igen</span><span class="sxs-lookup"><span data-stu-id="d705d-144">Yes</span></span>      | <span data-ttu-id="d705d-145">Egy ország-/régióazonosító.</span><span class="sxs-lookup"><span data-stu-id="d705d-145">A country/region ID.</span></span>                                            |
| <span data-ttu-id="d705d-146">célszegmens</span><span class="sxs-lookup"><span data-stu-id="d705d-146">target-segment</span></span>         | <span data-ttu-id="d705d-147">sztring</span><span class="sxs-lookup"><span data-stu-id="d705d-147">string</span></span>   | <span data-ttu-id="d705d-148">No</span><span class="sxs-lookup"><span data-stu-id="d705d-148">No</span></span>       | <span data-ttu-id="d705d-149">A szűréshez használt célszegmenst azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="d705d-149">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="d705d-150">reservationScope</span><span class="sxs-lookup"><span data-stu-id="d705d-150">reservationScope</span></span> | <span data-ttu-id="d705d-151">sztring</span><span class="sxs-lookup"><span data-stu-id="d705d-151">string</span></span>   | <span data-ttu-id="d705d-152">No</span><span class="sxs-lookup"><span data-stu-id="d705d-152">No</span></span> | <span data-ttu-id="d705d-153">Egy Azure-foglalási termék terméktermék terméktermék-listájának lekérdezésekor adja meg a értéket az AzurePlanra vonatkozó termékkel kapcsolatos `reservationScope=AzurePlan` termékkódok listájának lekérdezőjéhez.</span><span class="sxs-lookup"><span data-stu-id="d705d-153">When querying for a list of SKUs for an Azure Reservation product, specify `reservationScope=AzurePlan` to get a list of SKUs that are applicable to AzurePlan.</span></span> <span data-ttu-id="d705d-154">Zárja ki ezt a paramétert, hogy lekérte a Microsoft Azure (MS-AZR-0145P) előfizetések terméktermék-listáját.</span><span class="sxs-lookup"><span data-stu-id="d705d-154">Exclude this parameter to get a list of SKUs for Azure Reservation products that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="d705d-155">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d705d-155">Request headers</span></span>

<span data-ttu-id="d705d-156">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d705d-156">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d705d-157">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d705d-157">Request body</span></span>

<span data-ttu-id="d705d-158">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d705d-158">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="d705d-159">Példák kérésre</span><span class="sxs-lookup"><span data-stu-id="d705d-159">Request examples</span></span>

<span data-ttu-id="d705d-160">Egy adott termék terméktermék termékterméklistáinak lekért listája:</span><span class="sxs-lookup"><span data-stu-id="d705d-160">Get a list of SKUs for a given product:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="d705d-161">Lekért egy Azure-foglalási termék terméktermék terméktermékének listáját.</span><span class="sxs-lookup"><span data-stu-id="d705d-161">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="d705d-162">Csak az Azure-csomagokra vonatkozó SKUS-okat foglalja bele, Microsoft Azure (MS-AZR-0145P) előfizetések esetében nem:</span><span class="sxs-lookup"><span data-stu-id="d705d-162">Only include the SKUs that are applicable to Azure plans and not Microsoft Azure (MS-AZR-0145P) subscriptions:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="d705d-163">Lekért egy Azure-foglalási termék terméktermék terméktermékének listáját.</span><span class="sxs-lookup"><span data-stu-id="d705d-163">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="d705d-164">Csak a Microsoft Azure (MS-AZR-0145P) előfizetésre érvényes SKUS-okat foglalja bele, az Azure-csomagokba nem:</span><span class="sxs-lookup"><span data-stu-id="d705d-164">Only include the SKUs that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions and not Azure plans:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a><span data-ttu-id="d705d-165">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d705d-165">REST response</span></span>

<span data-ttu-id="d705d-166">Ha a művelet sikeres, a válasz törzse [SKU-erőforrások gyűjteményét](product-resources.md#sku) tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="d705d-166">If successful, the response body contains a collection of [SKU](product-resources.md#sku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d705d-167">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d705d-167">Response success and error codes</span></span>

<span data-ttu-id="d705d-168">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d705d-168">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d705d-169">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d705d-169">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d705d-170">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d705d-170">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="d705d-171">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="d705d-171">This method returns the following error codes:</span></span>

| <span data-ttu-id="d705d-172">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="d705d-172">HTTP Status Code</span></span>     | <span data-ttu-id="d705d-173">Hibakód</span><span class="sxs-lookup"><span data-stu-id="d705d-173">Error code</span></span>   | <span data-ttu-id="d705d-174">Leírás</span><span class="sxs-lookup"><span data-stu-id="d705d-174">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d705d-175">403</span><span class="sxs-lookup"><span data-stu-id="d705d-175">403</span></span>                  | <span data-ttu-id="d705d-176">400030</span><span class="sxs-lookup"><span data-stu-id="d705d-176">400030</span></span>       | <span data-ttu-id="d705d-177">A kért targetSegment szolgáltatáshoz való hozzáférés nem engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="d705d-177">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="d705d-178">404</span><span class="sxs-lookup"><span data-stu-id="d705d-178">404</span></span>                  | <span data-ttu-id="d705d-179">400013</span><span class="sxs-lookup"><span data-stu-id="d705d-179">400013</span></span>       | <span data-ttu-id="d705d-180">A szülőtermék nem található.</span><span class="sxs-lookup"><span data-stu-id="d705d-180">The parent product was not found.</span></span>                                                                         |

### <a name="response-example"></a><span data-ttu-id="d705d-181">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d705d-181">Response example</span></span>

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
