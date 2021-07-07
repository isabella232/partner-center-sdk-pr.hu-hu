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
# <a name="get-a-list-of-skus-for-a-product-by-country"></a>Egy termék termékváltozatait tartalmazó lista lekérése (ország alapján)

Egy adott termékhez egy adott országban elérhető terméktermékgyűjteményt az API-k használatával Partnerközpont le.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.

- Egy termékazonosító.

## <a name="c"></a>C\#

Egy termék termék termékterméklistáinak lekért listája:

1. Szerezze be egy adott termék műveleteinek interfészét a Termék lekért azonosítója [alapján lépéseit követve.](get-a-product-by-id.md)

2. A felületről válassza ki a Skus tulajdonságot a **SKUS-hoz** elérhető műveletekkel való interfész beszerzéséhez.

3. Hívja meg **a Get() vagy** **a GetAsync()** metódust a termékhez elérhető termékkódok gyűjteményének lekéréséhez.

4. (Nem kötelező) Válassza ki a foglalási hatókört a **ByReservationScope() metódussal.**

5. (Nem kötelező) A **ByTargetSegment()** metódussal szűrheti a SKUs-okat célszegmens szerint a **Get()** vagy **a GetAsync() hívása előtt.**

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

Egy termék termék termékterméklistáinak lekért listája:

1. Szerezze be egy adott termék műveleteinek interfészét a Termék lekért azonosítója [alapján lépéseit követve.](get-a-product-by-id.md)

2. A felületen válassza ki a **getSkus** függvényt, hogy be tudja szerezni a rendelkezésre álló műveleteket a SKUs-hez.

3. Hívja meg a **get()** függvényt a termékhez elérhető termékkódok gyűjteményének lekéréséhez.

4. (Nem kötelező) A **byTargetSegment()** függvény használatával szűrheti a SKUs-okat célszegmens szerint a **get()** függvény hívása előtt.

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

Egy termék termék termékterméklistáinak lekért listája:

1. Hajtsa végre [**a Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) parancsot.

2. (Nem kötelező) Adja meg **a Szegmens** paramétert a SKUs célszegmens alapján való szűréséhez.

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{termékazonosító}/termékkód?country={országkód}&targetSegment={target-segment} HTTP/1.1  |

#### <a name="uri-parameters"></a>URI-paraméterek

Az alábbi elérési út és lekérdezési paraméterek használatával lekérdezheti egy terméktermékének listáját.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| termékazonosító             | sztring   | Igen      | A terméket azonosító sztring.                           |
| országkód           | sztring   | Igen      | Egy ország-/régióazonosító.                                            |
| célszegmens         | sztring   | No       | A szűréshez használt célszegmenst azonosító sztring. |
| reservationScope | sztring   | No | Egy Azure-foglalási termék terméktermék terméktermék-listájának lekérdezésekor adja meg a értéket az AzurePlanra vonatkozó termékkel kapcsolatos `reservationScope=AzurePlan` termékkódok listájának lekérdezőjéhez. Zárja ki ezt a paramétert, hogy lekérte a Microsoft Azure (MS-AZR-0145P) előfizetések terméktermék-listáját.  |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-examples"></a>Példák kérésre

Egy adott termék terméktermék termékterméklistáinak lekért listája:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

Lekért egy Azure-foglalási termék terméktermék terméktermékének listáját. Csak az Azure-csomagokra vonatkozó SKUS-okat foglalja bele, Microsoft Azure (MS-AZR-0145P) előfizetések esetében nem:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

Lekért egy Azure-foglalási termék terméktermék terméktermékének listáját. Csak a Microsoft Azure (MS-AZR-0145P) előfizetésre érvényes SKUS-okat foglalja bele, az Azure-csomagokba nem:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse [SKU-erőforrások gyűjteményét](product-resources.md#sku) tartalmazza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód     | Hibakód   | Leírás                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | A kért targetSegment szolgáltatáshoz való hozzáférés nem engedélyezett.                                                     |
| 404                  | 400013       | A szülőtermék nem található.                                                                         |

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
