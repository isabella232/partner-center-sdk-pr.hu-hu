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
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a>Katalógus-elemek leltárának megtekintése a partner Center API-k használatával

**A következőkre vonatkozik:**

- Partnerközpont

A leltár beállítása a katalógus egyes elemeihez.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Egy vagy több termékazonosító. Szükség esetén SKU-azonosító is megadható.

- A megadott termék/SKU-azonosító (k) által hivatkozott SKU (ok) leltárának ellenőrzéséhez szükséges további környezet. Ezek a követelmények a termék/SKU típusától függően eltérőek lehetnek, és az [SKU](product-resources.md#sku) **InventoryVariables** tulajdonsága alapján határozhatók meg.

## <a name="c"></a>C\#

A leltár ellenőrzéséhez hozzon létre egy [InventoryCheckRequest](product-resources.md#inventorycheckrequest) objektumot egy [InventoryItem](product-resources.md#inventoryitem) objektum használatával az egyes ellenőrizendő elemek esetében. Ezután használjon egy **IAggregatePartner. Extensions** -hozzáférést a **termékhez** , majd válassza ki az országot a **ByCountry ()** metódus használatával. Végül hívja meg a **CheckInventory ()** metódust a **InventoryCheckRequest** objektummal.

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

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Extensions/Product/checkInventory? ország = {országkód} http/1.1                        |

### <a name="uri-parameter"></a>URI-paraméter

Használja a következő lekérdezési paramétert a leltár vizsgálatához.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| országkód           | sztring   | Igen      | Ország/régió azonosítója.                                            |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

A leltári kérelem részletei, amely egy vagy több [InventoryItem](product-resources.md#inventoryitem) -erőforrást tartalmazó [InventoryCheckRequest](product-resources.md#inventorycheckrequest) -erőforrást tartalmaz.

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

Ha ez sikeres, a válasz törzse [InventoryItem](product-resources.md#inventoryitem) -objektumok gyűjteményét tartalmazza, amely a korlátozás részleteivel van feltöltve, ha van ilyen alkalmazás.

>[!NOTE]
>Ha egy bemeneti InventoryItem olyan elemet jelöl, amely nem található a katalógusban, nem fog szerepelni a kimeneti gyűjteményben.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).

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
