---
title: Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ország alapján)
description: A megadott termékhez és termékváltozathoz való rendelkezésre állások gyűjteményének lekérte az ügyfél országa szerint.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b29c005e74ad8a4da547a888b78e4599e74ebd02
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874533"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a><span data-ttu-id="bcc1b-103">Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ország alapján)</span><span class="sxs-lookup"><span data-stu-id="bcc1b-103">Get a list of availabilities for a SKU (by country)</span></span>

<span data-ttu-id="bcc1b-104">Ez a cikk azt ismerteti, hogyan lehet rendelkezésre állási gyűjteményt lekért egy adott országban egy adott termékhez és termékváltozathoz.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-104">This article describes how to get a collection of availabilities in a particular country for a specified product and SKU.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcc1b-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="bcc1b-105">Prerequisites</span></span>

- <span data-ttu-id="bcc1b-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="bcc1b-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bcc1b-107">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="bcc1b-108">Egy termékazonosító.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-108">A product identifier.</span></span>

- <span data-ttu-id="bcc1b-109">Egy termékváltozat-azonosító.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-109">A SKU identifier.</span></span>

- <span data-ttu-id="bcc1b-110">Egy ország.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-110">A country.</span></span>

## <a name="c"></a><span data-ttu-id="bcc1b-111">C\#</span><span class="sxs-lookup"><span data-stu-id="bcc1b-111">C\#</span></span>

<span data-ttu-id="bcc1b-112">Egy termékváltozat [rendelkezésre állási](product-resources.md#availability) listájának [lekért listája:](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="bcc1b-112">To get the list of [availabilities](product-resources.md#availability) for a [SKU](product-resources.md#sku):</span></span>

1. <span data-ttu-id="bcc1b-113">Az adott termékváltozat műveleteihez szükséges felület lekért felületének lekért lépéseit az [SKU](get-a-sku-by-id.md) azonosító alapján való lekért lépéseit követve.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-113">Follow the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific SKU's operations.</span></span>

2. <span data-ttu-id="bcc1b-114">A termékváltozat felületén válassza az **Availabilities (Rendelkezésre** állások) tulajdonságot, hogy lekérte a rendelkezésre állási műveletekhez szükséges interfészt.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-114">From the SKU interface, select the **Availabilities** property to get an interface with the operations for availabilities.</span></span>

3. <span data-ttu-id="bcc1b-115">(Nem kötelező) A **ByTargetSegment()** metódussal szűrheti a rendelkezésre állásokat célszegmens szerint.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-115">(Optional) Use the **ByTargetSegment()** method to filter the availabilities by target segment.</span></span>

4. <span data-ttu-id="bcc1b-116">A termékváltozat rendelkezésre állási gyűjteményének lekéréséhez hívja meg a **Get()** vagy a **GetAsync()** metódust.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-116">Call **Get()** or **GetAsync()** to retrieve a collection of the availabilities for this SKU.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="bcc1b-117">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="bcc1b-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bcc1b-118">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="bcc1b-118">Request syntax</span></span>

| <span data-ttu-id="bcc1b-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="bcc1b-119">Method</span></span>  | <span data-ttu-id="bcc1b-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="bcc1b-120">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bcc1b-121">**Kap**</span><span class="sxs-lookup"><span data-stu-id="bcc1b-121">**GET**</span></span> | <span data-ttu-id="bcc1b-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{termékazonosító}/termékváltozatok/{sku-id}/availabilities?country={országkód}&targetSegment={target-segment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="bcc1b-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="bcc1b-123">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="bcc1b-123">URI parameters</span></span>

<span data-ttu-id="bcc1b-124">Az alábbi elérési út és lekérdezési paraméterek használatával lekérdezheti a termékváltozatok rendelkezésre állási listáját.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-124">Use the following path and query parameters to get a list of availabilities for a SKU.</span></span>

| <span data-ttu-id="bcc1b-125">Név</span><span class="sxs-lookup"><span data-stu-id="bcc1b-125">Name</span></span>                   | <span data-ttu-id="bcc1b-126">Típus</span><span class="sxs-lookup"><span data-stu-id="bcc1b-126">Type</span></span>     | <span data-ttu-id="bcc1b-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="bcc1b-127">Required</span></span> | <span data-ttu-id="bcc1b-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="bcc1b-128">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="bcc1b-129">termékazonosító</span><span class="sxs-lookup"><span data-stu-id="bcc1b-129">product-id</span></span>             | <span data-ttu-id="bcc1b-130">sztring</span><span class="sxs-lookup"><span data-stu-id="bcc1b-130">string</span></span>   | <span data-ttu-id="bcc1b-131">Igen</span><span class="sxs-lookup"><span data-stu-id="bcc1b-131">Yes</span></span>      | <span data-ttu-id="bcc1b-132">A terméket azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-132">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="bcc1b-133">sku-id</span><span class="sxs-lookup"><span data-stu-id="bcc1b-133">sku-id</span></span>                 | <span data-ttu-id="bcc1b-134">sztring</span><span class="sxs-lookup"><span data-stu-id="bcc1b-134">string</span></span>   | <span data-ttu-id="bcc1b-135">Igen</span><span class="sxs-lookup"><span data-stu-id="bcc1b-135">Yes</span></span>      | <span data-ttu-id="bcc1b-136">A termékváltozatot azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-136">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="bcc1b-137">országkód</span><span class="sxs-lookup"><span data-stu-id="bcc1b-137">country-code</span></span>           | <span data-ttu-id="bcc1b-138">sztring</span><span class="sxs-lookup"><span data-stu-id="bcc1b-138">string</span></span>   | <span data-ttu-id="bcc1b-139">Igen</span><span class="sxs-lookup"><span data-stu-id="bcc1b-139">Yes</span></span>      | <span data-ttu-id="bcc1b-140">Egy ország-/régióazonosító.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-140">A country/region ID.</span></span>                                            |
| <span data-ttu-id="bcc1b-141">célszegmens</span><span class="sxs-lookup"><span data-stu-id="bcc1b-141">target-segment</span></span>         | <span data-ttu-id="bcc1b-142">sztring</span><span class="sxs-lookup"><span data-stu-id="bcc1b-142">string</span></span>   | <span data-ttu-id="bcc1b-143">No</span><span class="sxs-lookup"><span data-stu-id="bcc1b-143">No</span></span>       | <span data-ttu-id="bcc1b-144">A szűréshez használt célszegmenst azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-144">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="bcc1b-145">reservationScope</span><span class="sxs-lookup"><span data-stu-id="bcc1b-145">reservationScope</span></span> | <span data-ttu-id="bcc1b-146">sztring</span><span class="sxs-lookup"><span data-stu-id="bcc1b-146">string</span></span>   | <span data-ttu-id="bcc1b-147">No</span><span class="sxs-lookup"><span data-stu-id="bcc1b-147">No</span></span> | <span data-ttu-id="bcc1b-148">Az Azure-foglalási termékváltozatok rendelkezésre állási listájának lekérdezésekor adja meg a értéket az AzurePlanra vonatkozó rendelkezésre `reservationScope=AzurePlan` állások listájának lekérdezőjéhez.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-148">When querying for a list of availabilities for an Azure Reservation SKU, specify `reservationScope=AzurePlan` to get a list of availabilities that are applicable to AzurePlan.</span></span> <span data-ttu-id="bcc1b-149">Zárja ki ezt a paramétert a Microsoft Azure (MS-AZR-0145P) előfizetések esetében elérhető rendelkezésre állások listájának lekértéhez.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-149">Exclude this parameter to get a list of availabilities that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="bcc1b-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="bcc1b-150">Request headers</span></span>

<span data-ttu-id="bcc1b-151">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="bcc1b-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bcc1b-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="bcc1b-152">Request body</span></span>

<span data-ttu-id="bcc1b-153">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-153">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="bcc1b-154">Példák kérésre</span><span class="sxs-lookup"><span data-stu-id="bcc1b-154">Request examples</span></span>

#### <a name="availabilities-for-sku-by-country"></a><span data-ttu-id="bcc1b-155">Termékváltozatok rendelkezésre állása országonként</span><span class="sxs-lookup"><span data-stu-id="bcc1b-155">Availabilities for SKU by country</span></span>

<span data-ttu-id="bcc1b-156">Kövesse ezt a példát egy adott termékváltozat rendelkezésre állási listájának országonkénti lekért listájához:</span><span class="sxs-lookup"><span data-stu-id="bcc1b-156">Follow this example to get a list of availabilities for a given SKU by country:</span></span>

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a><span data-ttu-id="bcc1b-157">Virtuálisgép-foglalások rendelkezésre állása (Azure-csomag)</span><span class="sxs-lookup"><span data-stu-id="bcc1b-157">Availabilities for VM reservations (Azure plan)</span></span>

<span data-ttu-id="bcc1b-158">Kövesse ezt a példát az Azure-beli virtuális gépek foglalási termékkódok országonkénti rendelkezésre állási listájának lekért listájához.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-158">Follow this example to get a list of availabilities by country for Azure VM reservation SKUs.</span></span> <span data-ttu-id="bcc1b-159">Ez a példa az Azure-csomagokra vonatkozó SKUS-okat példázhatja:</span><span class="sxs-lookup"><span data-stu-id="bcc1b-159">This example is for SKUs that apply to Azure plans:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="bcc1b-160">Virtuálisgép-foglalások rendelkezésre állása Microsoft Azure (MS-AZR-0145P) előfizetések esetében</span><span class="sxs-lookup"><span data-stu-id="bcc1b-160">Availabilities for VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="bcc1b-161">Ebben a példában az egyes országok szerinti elérhetőségek listáját azon Azure-beli virtuális gépek foglalásainál adhatja meg, amelyek Microsoft Azure (MS-AZR-0145P) előfizetésre vonatkoznak.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-161">Follow this example to get a list of availabilities by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="bcc1b-162">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="bcc1b-162">REST response</span></span>

<span data-ttu-id="bcc1b-163">Ha ez sikeres, a válasz törzse rendelkezésre állási [**erőforrások gyűjteményét**](product-resources.md#availability) tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-163">If successful, the response body contains a collection of [**Availability**](product-resources.md#availability) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bcc1b-164">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="bcc1b-164">Response success and error codes</span></span>

<span data-ttu-id="bcc1b-165">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-165">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bcc1b-166">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-166">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bcc1b-167">A teljes listát lásd: Partnerközpont [hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="bcc1b-167">For a full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="bcc1b-168">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="bcc1b-168">This method returns the following error codes:</span></span>

| <span data-ttu-id="bcc1b-169">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="bcc1b-169">HTTP Status Code</span></span>     | <span data-ttu-id="bcc1b-170">Hibakód</span><span class="sxs-lookup"><span data-stu-id="bcc1b-170">Error code</span></span>   | <span data-ttu-id="bcc1b-171">Leírás</span><span class="sxs-lookup"><span data-stu-id="bcc1b-171">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bcc1b-172">403</span><span class="sxs-lookup"><span data-stu-id="bcc1b-172">403</span></span>                  | <span data-ttu-id="bcc1b-173">400030</span><span class="sxs-lookup"><span data-stu-id="bcc1b-173">400030</span></span>       | <span data-ttu-id="bcc1b-174">A kért **targetSegment szolgáltatáshoz való hozzáférés** nem engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="bcc1b-174">Access to the requested **targetSegment** is not allowed.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="bcc1b-175">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="bcc1b-175">Response example</span></span>

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
