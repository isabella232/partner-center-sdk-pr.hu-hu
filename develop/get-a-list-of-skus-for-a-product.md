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
# <a name="get-a-list-of-skus-for-a-product-by-country"></a>Egy termék termékváltozatait tartalmazó lista lekérése (ország alapján)

**A következőkre vonatkozik:**

- Partnerközpont

A partner Center API-k használatával egy adott termékhez tartozó SKU-k gyűjteményét is beszerezheti egy adott országban.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- A termék azonosítója.

## <a name="c"></a>C\#

A termékhez tartozó SKU-termékek listájának lekérése:

1. Szerezzen be egy felületet egy adott termék műveleteihez a [termék beolvasása azonosító alapján](get-a-product-by-id.md)című rész lépéseit követve.

2. A csatolón válassza a **SKUs** tulajdonságot, hogy beszerezze a csatolót az SKU-hoz elérhető műveletekkel.

3. Hívja meg a **Get ()** vagy a **GetAsync ()** metódust, hogy lekérje a termékhez rendelkezésre álló SKU-gyűjteményt.

4. Választható Válassza ki a foglalási hatókört a **ByReservationScope ()** metódus használatával.

5. Választható A **Get (** ) vagy a **GetAsync ()** hívása előtt a **ByTargetSegment ()** metódus használatával szűrheti a SKU-ket a célként megadott szegmens alapján.

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

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

A termékhez tartozó SKU-termékek listájának lekérése:

1. Szerezzen be egy felületet egy adott termék műveleteihez a [termék beolvasása azonosító alapján](get-a-product-by-id.md)című rész lépéseit követve.

2. A csatolón válassza a **getSkus** függvényt, és szerezzen be egy felületet az SKU-hoz elérhető műveletekkel.

3. A **Get ()** függvény meghívásával lekérheti a termékhez rendelkezésre álló SKU-gyűjteményt.

4. Választható A **Get ()** függvény hívása előtt a **byTargetSegment ()** függvénnyel szűrheti az SKU-ket a célként megadott szegmens alapján.

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

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

A termékhez tartozó SKU-termékek listájának lekérése:

1. Futtassa a [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) parancsot.

2. Választható A **szegmens** paraméter megadásával szűrheti az SKU-ket a célként megadott szegmens alapján.

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs? ország = {országkód} &targetSegment = {Target-szegmens} http/1.1  |

#### <a name="uri-parameters"></a>URI-paraméterek

A következő elérési út és lekérdezési paraméterek segítségével szerezzen be egy termék SKU-listáját.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| termék azonosítója             | sztring   | Igen      | A terméket azonosító karakterlánc.                           |
| országkód           | sztring   | Igen      | Ország/régió azonosítója.                                            |
| cél szegmens         | sztring   | No       | A szűréshez használt cél szegmenst azonosító karakterlánc. |
| reservationScope | sztring   | No | Ha egy Azure-beli foglalási termékhez tartozó SKU-ket szeretne lekérdezni, akkor a AzurePlan vonatkozó SKU-lista lekéréséhez válassza a következőt: `reservationScope=AzurePlan` . Zárja be ezt a paramétert egy olyan Azure-beli foglalási termék SKU-listájának lekéréséhez, amely Microsoft Azure (MS-AZR-0145P) előfizetésekre alkalmazható.  |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-examples"></a>Példák kérése

Egy adott termék SKU-listájának lekérése:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

Egy Azure-beli foglalási termék SKU-i listájának beolvasása. Csak az Azure-csomagokra érvényes SKU-ket és nem Microsoft Azure (MS-AZR-0145P) előfizetéseket tartalmazza:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

Egy Azure-beli foglalási termék SKU-i listájának beolvasása. Csak a Microsoft Azure (MS-AZR-0145P) előfizetésekre és nem Azure-csomagokra alkalmazandó SKU-ket foglalja bele:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse [SKU](product-resources.md#sku) -erőforrások gyűjteményét tartalmazza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód     | Hibakód   | Leírás                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | A kért targetSegment való hozzáférés nem engedélyezett.                                                     |
| 404                  | 400013       | A fölérendelt termék nem található.                                                                         |

### <a name="response-example"></a>Példa válaszra

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
