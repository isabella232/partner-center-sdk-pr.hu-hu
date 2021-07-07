---
title: Leltár ellenőrzése
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat a katalóguselemek adott készletének leltározási halmazának ellenőrzésére. Ezzel azonosíthatja az ügyfél termékeit vagy termékkódját.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b982dbd7e5e10d454ef87a1e750546ea50eb8438
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974080"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a><span data-ttu-id="9b2cb-104">Katalóguselemek leltárának ellenőrzése a Partnerközpont API-k használatával</span><span class="sxs-lookup"><span data-stu-id="9b2cb-104">Check the inventory of catalog items using Partner Center APIs</span></span>

<span data-ttu-id="9b2cb-105">Katalóguselemek adott készletének leltározása.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-105">How to check the inventory for a specific set of catalog items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b2cb-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="9b2cb-106">Prerequisites</span></span>

- <span data-ttu-id="9b2cb-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9b2cb-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9b2cb-108">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9b2cb-109">Egy vagy több termékkulcs.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-109">One or more product IDs.</span></span> <span data-ttu-id="9b2cb-110">A termékváltozat-okat is meg lehet adni.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-110">Optionally, SKU IDs can also be specified.</span></span>

- <span data-ttu-id="9b2cb-111">Minden további környezet, amely a megadott termék/termékváltozat-azonosító(k) által hivatkozott termékváltozat(ek) leltárának ellenőrzéséhez szükséges.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-111">Any additional context needed for verifying the inventory of the SKU(s) referenced by the provided product/SKU ID(s).</span></span> <span data-ttu-id="9b2cb-112">Ezek a követelmények terméktípusonként/termékváltozatonként változhatnak, és a [termékváltozat](product-resources.md#sku) **InventoryVariables** tulajdonsága alapján határozhatók meg.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-112">These requirements may vary by type of product/SKU and can be determined from the [SKU's](product-resources.md#sku) **InventoryVariables** property.</span></span>

## <a name="c"></a><span data-ttu-id="9b2cb-113">C\#</span><span class="sxs-lookup"><span data-stu-id="9b2cb-113">C\#</span></span>

<span data-ttu-id="9b2cb-114">A leltár ellenőrzéshez készítsen [egy InventoryCheckRequest](product-resources.md#inventorycheckrequest) objektumot egy [InventoryItem](product-resources.md#inventoryitem) objektummal az egyes ellenőrizni kívánt elemekhez.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-114">To check the inventory, build an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) object using an [InventoryItem](product-resources.md#inventoryitem) object for each item to be checked.</span></span> <span data-ttu-id="9b2cb-115">Ezután használjon **egy IAggregatePartner.Extensions** hozzáférési kiszolgálót, és hatókörként adja meg a **Product** (Termék) lehetőséget, majd válassza ki az országot a **ByCountry() metódussal.**</span><span class="sxs-lookup"><span data-stu-id="9b2cb-115">Then, use an **IAggregatePartner.Extensions** accessor, scope it down to **Product** and then select the country using the **ByCountry()** method.</span></span> <span data-ttu-id="9b2cb-116">Végül hívja meg a **CheckInventory()** metódust az **InventoryCheckRequest objektummal.**</span><span class="sxs-lookup"><span data-stu-id="9b2cb-116">Finally, call the **CheckInventory()** method with your **InventoryCheckRequest** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="9b2cb-117">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="9b2cb-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9b2cb-118">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="9b2cb-118">Request syntax</span></span>

| <span data-ttu-id="9b2cb-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="9b2cb-119">Method</span></span>   | <span data-ttu-id="9b2cb-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="9b2cb-120">Request URI</span></span>                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9b2cb-121">**Post**</span><span class="sxs-lookup"><span data-stu-id="9b2cb-121">**POST**</span></span> | <span data-ttu-id="9b2cb-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9b2cb-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="9b2cb-123">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="9b2cb-123">URI parameter</span></span>

<span data-ttu-id="9b2cb-124">A leltár ellenőrzéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-124">Use the following query parameter to check the inventory.</span></span>

| <span data-ttu-id="9b2cb-125">Név</span><span class="sxs-lookup"><span data-stu-id="9b2cb-125">Name</span></span>                   | <span data-ttu-id="9b2cb-126">Típus</span><span class="sxs-lookup"><span data-stu-id="9b2cb-126">Type</span></span>     | <span data-ttu-id="9b2cb-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="9b2cb-127">Required</span></span> | <span data-ttu-id="9b2cb-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="9b2cb-128">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="9b2cb-129">országkód</span><span class="sxs-lookup"><span data-stu-id="9b2cb-129">country-code</span></span>           | <span data-ttu-id="9b2cb-130">sztring</span><span class="sxs-lookup"><span data-stu-id="9b2cb-130">string</span></span>   | <span data-ttu-id="9b2cb-131">Igen</span><span class="sxs-lookup"><span data-stu-id="9b2cb-131">Yes</span></span>      | <span data-ttu-id="9b2cb-132">Egy ország-/régióazonosító.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-132">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="9b2cb-133">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="9b2cb-133">Request headers</span></span>

<span data-ttu-id="9b2cb-134">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9b2cb-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9b2cb-135">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="9b2cb-135">Request body</span></span>

<span data-ttu-id="9b2cb-136">A leltárkérés részletei, amely egy vagy több [InventoryItem](product-resources.md#inventoryitem) erőforrást tartalmazó [InventoryCheckRequest](product-resources.md#inventorycheckrequest) erőforrásból áll.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-136">The inventory request details, consisting of an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) resource containing one or more [InventoryItem](product-resources.md#inventoryitem) resources.</span></span>

### <a name="request-example"></a><span data-ttu-id="9b2cb-137">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="9b2cb-137">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9b2cb-138">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="9b2cb-138">REST response</span></span>

<span data-ttu-id="9b2cb-139">Ha ez sikeres, a válasz törzse tartalmazza a korlátozás részleteivel feltölthető [InventoryItem-objektumok](product-resources.md#inventoryitem) gyűjteményét, ha van ilyen.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-139">If successful, the response body contains a collection of [InventoryItem](product-resources.md#inventoryitem) objects populated with the restriction details, if any apply.</span></span>

>[!NOTE]
><span data-ttu-id="9b2cb-140">Ha egy bemeneti InventoryItem olyan elemet képvisel, amely nem található a katalógusban, akkor az nem fog szerepelni a kimeneti gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-140">If an input InventoryItem represents an item that could not be found in the catalog, it will not be included in the output collection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9b2cb-141">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="9b2cb-141">Response success and error codes</span></span>

<span data-ttu-id="9b2cb-142">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9b2cb-143">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="9b2cb-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9b2cb-144">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9b2cb-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9b2cb-145">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="9b2cb-145">Response example</span></span>

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
