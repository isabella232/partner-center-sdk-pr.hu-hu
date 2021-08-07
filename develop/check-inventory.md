---
title: Leltár ellenőrzése
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat a katalóguselemek adott készletének leltározási halmazának ellenőrzésére. Ezzel azonosíthatja az ügyfél termékeit vagy termékkódját.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: de931c7dd89f94b6be8fdaf0ad79c8faee268267c35a2c0f8e38d36b97842f3f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992109"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a>Katalóguselemek leltárának ellenőrzése a Partnerközpont API-k használatával

Katalóguselemek adott készletének leltározása.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy vagy több termékkulcs. Igény szerint termékváltozat-is meg lehet adni a termékváltozat-értékeket.

- Bármely további környezet, amely a megadott termék/termékváltozat-azonosítók által hivatkozott termékváltozat(ak) leltárának ellenőrzéséhez szükséges. Ezek a követelmények terméktípus/termékváltozat szerint változhatnak, és a [termékváltozat](product-resources.md#sku) **InventoryVariables** tulajdonsága alapján határozhatók meg.

## <a name="c"></a>C\#

A leltár ellenőrzéshez állítson össze [egy InventoryCheckRequest](product-resources.md#inventorycheckrequest) objektumot egy [InventoryItem](product-resources.md#inventoryitem) objektummal minden egyes ellenőrizni kívánt elemhez. Ezután használjon **egy IAggregatePartner.Extensions** hozzáférési elérést, hatókörként a **Termék** mezőre, majd válassza ki az országot a **ByCountry() metódussal.** Végül hívja meg a **CheckInventory() metódust** az **InventoryCheckRequest objektummal.**

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

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1                        |

### <a name="uri-parameter"></a>URI-paraméter

A leltár ellenőrzéséhez használja a következő lekérdezési paramétert.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| országkód           | sztring   | Yes      | Egy ország-/régióazonosító.                                            |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

A leltárkérés részletei, amely egy egy vagy több [InventoryItem](product-resources.md#inventoryitem) erőforrást tartalmazó [InventoryCheckRequest](product-resources.md#inventorycheckrequest) erőforrásból áll.

### <a name="request-example"></a>Példa kérésre

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

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse tartalmazza a korlátozás részleteivel kitöltve az [InventoryItem](product-resources.md#inventoryitem) objektumok gyűjteményét, ha van ilyen.

>[!NOTE]
>Ha egy bemeneti InventoryItem olyan elemet képvisel, amely nem található a katalógusban, akkor az nem fog szerepelni a kimeneti gyűjteményben.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a [hibakódok Partnerközpont tekintse meg.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

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
