---
title: Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ország alapján)
description: A megadott termékhez és SKU-hoz tartozó elérhetőségek gyűjteményének beszerzése az ügyfél országa szerint.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b97a4ce85b5edd9de1301a577988f8c54096ebeb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767956"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a><span data-ttu-id="11915-103">Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ország alapján)</span><span class="sxs-lookup"><span data-stu-id="11915-103">Get a list of availabilities for a SKU (by country)</span></span>

<span data-ttu-id="11915-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="11915-104">**Applies to:**</span></span>

- <span data-ttu-id="11915-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="11915-105">Partner Center</span></span>

<span data-ttu-id="11915-106">Ez a cikk azt ismerteti, hogyan kérhető le egy adott országban egy adott termékre és SKU-ra vonatkozó elérhetőségek gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="11915-106">This article describes how to get a collection of availabilities in a particular country for a specified product and SKU.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11915-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="11915-107">Prerequisites</span></span>

- <span data-ttu-id="11915-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="11915-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="11915-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="11915-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="11915-110">A termék azonosítója.</span><span class="sxs-lookup"><span data-stu-id="11915-110">A product identifier.</span></span>

- <span data-ttu-id="11915-111">SKU-azonosító.</span><span class="sxs-lookup"><span data-stu-id="11915-111">A SKU identifier.</span></span>

- <span data-ttu-id="11915-112">Egy ország.</span><span class="sxs-lookup"><span data-stu-id="11915-112">A country.</span></span>

## <a name="c"></a><span data-ttu-id="11915-113">C\#</span><span class="sxs-lookup"><span data-stu-id="11915-113">C\#</span></span>

<span data-ttu-id="11915-114">Az [SKU](product-resources.md#sku)-beli [elérhetőségek](product-resources.md#availability) listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="11915-114">To get the list of [availabilities](product-resources.md#availability) for a [SKU](product-resources.md#sku):</span></span>

1. <span data-ttu-id="11915-115">Az adott SKU műveleteihez tartozó csatoló beszerzéséhez kövesse az [SKU beolvasása azonosító alapján](get-a-sku-by-id.md) című témakör lépéseit.</span><span class="sxs-lookup"><span data-stu-id="11915-115">Follow the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific SKU's operations.</span></span>

2. <span data-ttu-id="11915-116">Az SKU felületén válassza ki az **elérhetőségek** tulajdonságot, hogy egy illesztőfelületet kapjon az elérhetőségi műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="11915-116">From the SKU interface, select the **Availabilities** property to get an interface with the operations for availabilities.</span></span>

3. <span data-ttu-id="11915-117">Választható Használja a **ByTargetSegment ()** metódust az elérhetőségek a célként megadott szegmens alapján történő szűréséhez.</span><span class="sxs-lookup"><span data-stu-id="11915-117">(Optional) Use the **ByTargetSegment()** method to filter the availabilities by target segment.</span></span>

4. <span data-ttu-id="11915-118">A **Get ()** vagy a **GetAsync ()** hívásával kérheti le az ehhez az SKU-hoz tartozó elérhetőségek gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="11915-118">Call **Get()** or **GetAsync()** to retrieve a collection of the availabilities for this SKU.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string targetSegment;
string productIdForAzureReservation;
string skuIdForAzureReservation;

// Get the availabilities.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.Get();

// Get the availabilities, filtered by target segment.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.BySegment(targetSegment).Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.ByReservationScope("AzurePlan").Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Azure plans only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.Get();

```

## <a name="rest-request"></a><span data-ttu-id="11915-119">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="11915-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="11915-120">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="11915-120">Request syntax</span></span>

| <span data-ttu-id="11915-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="11915-121">Method</span></span>  | <span data-ttu-id="11915-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="11915-122">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="11915-123">**GET**</span><span class="sxs-lookup"><span data-stu-id="11915-123">**GET**</span></span> | <span data-ttu-id="11915-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities? ország = {országkód} &targetSegment = {Target-szegmens} http/1.1</span><span class="sxs-lookup"><span data-stu-id="11915-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="11915-125">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="11915-125">URI parameters</span></span>

<span data-ttu-id="11915-126">Használja az alábbi elérési utat és a lekérdezési paramétereket az SKU-ban található elérhetőségek listájának lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="11915-126">Use the following path and query parameters to get a list of availabilities for a SKU.</span></span>

| <span data-ttu-id="11915-127">Név</span><span class="sxs-lookup"><span data-stu-id="11915-127">Name</span></span>                   | <span data-ttu-id="11915-128">Típus</span><span class="sxs-lookup"><span data-stu-id="11915-128">Type</span></span>     | <span data-ttu-id="11915-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="11915-129">Required</span></span> | <span data-ttu-id="11915-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="11915-130">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="11915-131">termék azonosítója</span><span class="sxs-lookup"><span data-stu-id="11915-131">product-id</span></span>             | <span data-ttu-id="11915-132">sztring</span><span class="sxs-lookup"><span data-stu-id="11915-132">string</span></span>   | <span data-ttu-id="11915-133">Igen</span><span class="sxs-lookup"><span data-stu-id="11915-133">Yes</span></span>      | <span data-ttu-id="11915-134">A terméket azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="11915-134">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="11915-135">SKU-azonosító</span><span class="sxs-lookup"><span data-stu-id="11915-135">sku-id</span></span>                 | <span data-ttu-id="11915-136">sztring</span><span class="sxs-lookup"><span data-stu-id="11915-136">string</span></span>   | <span data-ttu-id="11915-137">Igen</span><span class="sxs-lookup"><span data-stu-id="11915-137">Yes</span></span>      | <span data-ttu-id="11915-138">Egy karakterlánc, amely azonosítja az SKU-t.</span><span class="sxs-lookup"><span data-stu-id="11915-138">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="11915-139">országkód</span><span class="sxs-lookup"><span data-stu-id="11915-139">country-code</span></span>           | <span data-ttu-id="11915-140">sztring</span><span class="sxs-lookup"><span data-stu-id="11915-140">string</span></span>   | <span data-ttu-id="11915-141">Igen</span><span class="sxs-lookup"><span data-stu-id="11915-141">Yes</span></span>      | <span data-ttu-id="11915-142">Ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="11915-142">A country/region ID.</span></span>                                            |
| <span data-ttu-id="11915-143">cél szegmens</span><span class="sxs-lookup"><span data-stu-id="11915-143">target-segment</span></span>         | <span data-ttu-id="11915-144">sztring</span><span class="sxs-lookup"><span data-stu-id="11915-144">string</span></span>   | <span data-ttu-id="11915-145">No</span><span class="sxs-lookup"><span data-stu-id="11915-145">No</span></span>       | <span data-ttu-id="11915-146">A szűréshez használt cél szegmenst azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="11915-146">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="11915-147">reservationScope</span><span class="sxs-lookup"><span data-stu-id="11915-147">reservationScope</span></span> | <span data-ttu-id="11915-148">sztring</span><span class="sxs-lookup"><span data-stu-id="11915-148">string</span></span>   | <span data-ttu-id="11915-149">No</span><span class="sxs-lookup"><span data-stu-id="11915-149">No</span></span> | <span data-ttu-id="11915-150">Ha egy Azure-beli foglalási SKU-hoz tartozó elérhetőségek listáját kérdezi le, akkor a AzurePlan-ra `reservationScope=AzurePlan` vonatkozó elérhetőségek listájának lekéréséhez válassza a következőt:.</span><span class="sxs-lookup"><span data-stu-id="11915-150">When querying for a list of availabilities for an Azure Reservation SKU, specify `reservationScope=AzurePlan` to get a list of availabilities which are applicable to AzurePlan.</span></span> <span data-ttu-id="11915-151">Zárja be ezt a paramétert, hogy lekérje a Microsoft Azure (MS-AZR-0145P) előfizetésekre vonatkozó elérhetőségek listáját.</span><span class="sxs-lookup"><span data-stu-id="11915-151">Exclude this parameter to get a list of availabilities which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="11915-152">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="11915-152">Request headers</span></span>

<span data-ttu-id="11915-153">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="11915-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="11915-154">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="11915-154">Request body</span></span>

<span data-ttu-id="11915-155">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="11915-155">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="11915-156">Példák kérése</span><span class="sxs-lookup"><span data-stu-id="11915-156">Request examples</span></span>

#### <a name="availabilities-for-sku-by-country"></a><span data-ttu-id="11915-157">SKU-beli elérhetőségek országonként</span><span class="sxs-lookup"><span data-stu-id="11915-157">Availabilities for SKU by country</span></span>

<span data-ttu-id="11915-158">Ezt a példát követve lekérheti az adott SKU-ra vonatkozó elérhetőségek listáját ország szerint:</span><span class="sxs-lookup"><span data-stu-id="11915-158">Follow this example to get a list of availabilities for a given SKU by country:</span></span>

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a><span data-ttu-id="11915-159">VIRTUÁLIS gépek foglalásának elérhetősége (Azure-csomag)</span><span class="sxs-lookup"><span data-stu-id="11915-159">Availabilities for VM reservations (Azure plan)</span></span>

<span data-ttu-id="11915-160">Ezt a példát követve megtekintheti az ország szerint az Azure-beli virtuálisgép-foglalási SKU-ket.</span><span class="sxs-lookup"><span data-stu-id="11915-160">Follow this example to get a list of availabilities by country for Azure VM reservation SKUs.</span></span> <span data-ttu-id="11915-161">Ez a példa az Azure-csomagokra vonatkozó SKU-ra vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="11915-161">This example is for SKUs that apply to Azure plans:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="11915-162">Microsoft Azure (MS-AZR-0145P) előfizetések virtuális gépekre vonatkozó foglalásai</span><span class="sxs-lookup"><span data-stu-id="11915-162">Availabilities for VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="11915-163">Ez a példa a Microsoft Azure (MS-AZR-0145P) előfizetésekre alkalmazható Azure-beli virtuálisgép-foglalások országbeli elérhetőségi listájának beszerzésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="11915-163">Follow this example to get a list of availabilities by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="11915-164">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="11915-164">REST response</span></span>

<span data-ttu-id="11915-165">Ha ez sikeres, a válasz törzse [**rendelkezésre állási**](product-resources.md#availability) erőforrások gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="11915-165">If successful, the response body contains a collection of [**Availability**](product-resources.md#availability) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="11915-166">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="11915-166">Response success and error codes</span></span>

<span data-ttu-id="11915-167">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="11915-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="11915-168">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="11915-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="11915-169">Teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="11915-169">For a full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="11915-170">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="11915-170">This method returns the following error codes:</span></span>

| <span data-ttu-id="11915-171">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="11915-171">HTTP Status Code</span></span>     | <span data-ttu-id="11915-172">Hibakód</span><span class="sxs-lookup"><span data-stu-id="11915-172">Error code</span></span>   | <span data-ttu-id="11915-173">Leírás</span><span class="sxs-lookup"><span data-stu-id="11915-173">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="11915-174">403</span><span class="sxs-lookup"><span data-stu-id="11915-174">403</span></span>                  | <span data-ttu-id="11915-175">400030</span><span class="sxs-lookup"><span data-stu-id="11915-175">400030</span></span>       | <span data-ttu-id="11915-176">A kért **targetSegment** való hozzáférés nem engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="11915-176">Access to the requested **targetSegment** is not allowed.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="11915-177">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="11915-177">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02,70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllcw==?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:37 GMT
Content-Length: 808

{
    "totalCount": 1,
    "items": [
        {
            "id": "DZH318XZXVNF",
            "productId": "DZH318Z0BQ3Q",
            "skuId": "0001",
            "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXVNF",
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
                    "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318Z0HMKQ?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetSegment=commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
