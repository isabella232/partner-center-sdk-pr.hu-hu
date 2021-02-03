---
title: Leltár keresése
description: Megtudhatja, hogyan használhatja a partner Center API-kat egy adott katalógusbeli elem leltárának vizsgálatára. Ezt megteheti az ügyfél termékeinek vagy SKU-k azonosítására.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6921760abc0b95aff820467e84b3e8e9435731cd
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768599"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a><span data-ttu-id="19429-104">Katalógus-elemek leltárának megtekintése a partner Center API-k használatával</span><span class="sxs-lookup"><span data-stu-id="19429-104">Check the inventory of catalog items using Partner Center APIs</span></span>

<span data-ttu-id="19429-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="19429-105">**Applies to:**</span></span>

- <span data-ttu-id="19429-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="19429-106">Partner Center</span></span>

<span data-ttu-id="19429-107">A leltár beállítása a katalógus egyes elemeihez.</span><span class="sxs-lookup"><span data-stu-id="19429-107">How to check the inventory for a specific set of catalog items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19429-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="19429-108">Prerequisites</span></span>

- <span data-ttu-id="19429-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="19429-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="19429-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="19429-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="19429-111">Egy vagy több termékazonosító.</span><span class="sxs-lookup"><span data-stu-id="19429-111">One or more product IDs.</span></span> <span data-ttu-id="19429-112">Szükség esetén SKU-azonosító is megadható.</span><span class="sxs-lookup"><span data-stu-id="19429-112">Optionally, SKU IDs can also be specified.</span></span>

- <span data-ttu-id="19429-113">A megadott termék/SKU-azonosító (k) által hivatkozott SKU (ok) leltárának ellenőrzéséhez szükséges további környezet.</span><span class="sxs-lookup"><span data-stu-id="19429-113">Any additional context needed for verifying the inventory of the SKU(s) referenced by the provided product/SKU ID(s).</span></span> <span data-ttu-id="19429-114">Ezek a követelmények a termék/SKU típusától függően eltérőek lehetnek, és az [SKU](product-resources.md#sku) **InventoryVariables** tulajdonsága alapján határozhatók meg.</span><span class="sxs-lookup"><span data-stu-id="19429-114">These requirements may vary by type of product/SKU and can be determined from the [SKU's](product-resources.md#sku) **InventoryVariables** property.</span></span>

## <a name="c"></a><span data-ttu-id="19429-115">C\#</span><span class="sxs-lookup"><span data-stu-id="19429-115">C\#</span></span>

<span data-ttu-id="19429-116">A leltár ellenőrzéséhez hozzon létre egy [InventoryCheckRequest](product-resources.md#inventorycheckrequest) objektumot egy [InventoryItem](product-resources.md#inventoryitem) objektum használatával az egyes ellenőrizendő elemek esetében.</span><span class="sxs-lookup"><span data-stu-id="19429-116">To check the inventory, build an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) object using an [InventoryItem](product-resources.md#inventoryitem) object for each item to be checked.</span></span> <span data-ttu-id="19429-117">Ezután használjon egy **IAggregatePartner. Extensions** -hozzáférést a **termékhez** , majd válassza ki az országot a **ByCountry ()** metódus használatával.</span><span class="sxs-lookup"><span data-stu-id="19429-117">Then, use an **IAggregatePartner.Extensions** accessor, scope it down to **Product** and then select the country using the **ByCountry()** method.</span></span> <span data-ttu-id="19429-118">Végül hívja meg a **CheckInventory ()** metódust a **InventoryCheckRequest** objektummal.</span><span class="sxs-lookup"><span data-stu-id="19429-118">Finally, call the **CheckInventory()** method with your **InventoryCheckRequest** object.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string subscriptionId;
string countryCode;
string productId;

// Build the inventory check request details object.
var inventoryCheckRequest = new InventoryCheckRequest()
{
    TargetItems = new InventoryItem[]{ new InventoryItem { ProductId = productId } },
    InventoryContext = new Dictionary<string, string>()
    {
      { "customerId", customerId },
      { "azureSubscriptionId", subscriptionId }
      { "armRegionName", armRegionName }
    }
};

// Get the inventory results.
var inventoryResults = partnerOperations.Extensions.Product.ByCountry(countryCode).CheckInventory(inventoryCheckRequest);
```

## <a name="rest-request"></a><span data-ttu-id="19429-119">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="19429-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="19429-120">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="19429-120">Request syntax</span></span>

| <span data-ttu-id="19429-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="19429-121">Method</span></span>   | <span data-ttu-id="19429-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="19429-122">Request URI</span></span>                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="19429-123">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="19429-123">**POST**</span></span> | <span data-ttu-id="19429-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Extensions/Product/checkInventory? ország = {országkód} http/1.1</span><span class="sxs-lookup"><span data-stu-id="19429-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="19429-125">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="19429-125">URI parameter</span></span>

<span data-ttu-id="19429-126">Használja a következő lekérdezési paramétert a leltár vizsgálatához.</span><span class="sxs-lookup"><span data-stu-id="19429-126">Use the following query parameter to check the inventory.</span></span>

| <span data-ttu-id="19429-127">Név</span><span class="sxs-lookup"><span data-stu-id="19429-127">Name</span></span>                   | <span data-ttu-id="19429-128">Típus</span><span class="sxs-lookup"><span data-stu-id="19429-128">Type</span></span>     | <span data-ttu-id="19429-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="19429-129">Required</span></span> | <span data-ttu-id="19429-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="19429-130">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="19429-131">országkód</span><span class="sxs-lookup"><span data-stu-id="19429-131">country-code</span></span>           | <span data-ttu-id="19429-132">sztring</span><span class="sxs-lookup"><span data-stu-id="19429-132">string</span></span>   | <span data-ttu-id="19429-133">Igen</span><span class="sxs-lookup"><span data-stu-id="19429-133">Yes</span></span>      | <span data-ttu-id="19429-134">Ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="19429-134">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="19429-135">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="19429-135">Request headers</span></span>

<span data-ttu-id="19429-136">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="19429-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="19429-137">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="19429-137">Request body</span></span>

<span data-ttu-id="19429-138">A leltári kérelem részletei, amely egy vagy több [InventoryItem](product-resources.md#inventoryitem) -erőforrást tartalmazó [InventoryCheckRequest](product-resources.md#inventorycheckrequest) -erőforrást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="19429-138">The inventory request details, consisting of an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) resource containing one or more [InventoryItem](product-resources.md#inventoryitem) resources.</span></span>

### <a name="request-example"></a><span data-ttu-id="19429-139">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="19429-139">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/extensions/product/checkinventory?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json

{"TargetItems":[{"ProductId":"DZH318Z0BQ3P"}],"InventoryContext":{"customerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d","azureSubscriptionId":"3A231FBE-37FE-4410-93FD-730D3D5D4C75","armRegionName":"Europe"}}
```

## <a name="rest-response"></a><span data-ttu-id="19429-140">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="19429-140">REST response</span></span>

<span data-ttu-id="19429-141">Ha ez sikeres, a válasz törzse [InventoryItem](product-resources.md#inventoryitem) -objektumok gyűjteményét tartalmazza, amely a korlátozás részleteivel van feltöltve, ha van ilyen alkalmazás.</span><span class="sxs-lookup"><span data-stu-id="19429-141">If successful, the response body contains a collection of [InventoryItem](product-resources.md#inventoryitem) objects populated with the restriction details, if any apply.</span></span>

>[!NOTE]
><span data-ttu-id="19429-142">Ha egy bemeneti InventoryItem olyan elemet jelöl, amely nem található a katalógusban, nem fog szerepelni a kimeneti gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="19429-142">If an input InventoryItem represents an item that could not be found in the catalog, it will not be included in the output collection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="19429-143">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="19429-143">Response success and error codes</span></span>

<span data-ttu-id="19429-144">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="19429-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="19429-145">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="19429-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="19429-146">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="19429-146">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="19429-147">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="19429-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1021
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
X-Locale: en-US
[
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0039",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0038",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "000S",
        "isRestricted": false,
        "restrictions": []
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0011",
        "isRestricted": false,
        "restrictions": []
    }
]
```
