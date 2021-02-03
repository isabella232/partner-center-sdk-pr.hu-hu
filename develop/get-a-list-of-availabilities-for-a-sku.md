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
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a>Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ország alapján)

**A következőkre vonatkozik:**

- Partnerközpont

Ez a cikk azt ismerteti, hogyan kérhető le egy adott országban egy adott termékre és SKU-ra vonatkozó elérhetőségek gyűjteménye.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- A termék azonosítója.

- SKU-azonosító.

- Egy ország.

## <a name="c"></a>C\#

Az [SKU](product-resources.md#sku)-beli [elérhetőségek](product-resources.md#availability) listájának lekérése:

1. Az adott SKU műveleteihez tartozó csatoló beszerzéséhez kövesse az [SKU beolvasása azonosító alapján](get-a-sku-by-id.md) című témakör lépéseit.

2. Az SKU felületén válassza ki az **elérhetőségek** tulajdonságot, hogy egy illesztőfelületet kapjon az elérhetőségi műveletekhez.

3. Választható Használja a **ByTargetSegment ()** metódust az elérhetőségek a célként megadott szegmens alapján történő szűréséhez.

4. A **Get ()** vagy a **GetAsync ()** hívásával kérheti le az ehhez az SKU-hoz tartozó elérhetőségek gyűjteményét.

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

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities? ország = {országkód} &targetSegment = {Target-szegmens} http/1.1     |

### <a name="uri-parameters"></a>URI-paraméterek

Használja az alábbi elérési utat és a lekérdezési paramétereket az SKU-ban található elérhetőségek listájának lekéréséhez.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| termék azonosítója             | sztring   | Igen      | A terméket azonosító karakterlánc.                           |
| SKU-azonosító                 | sztring   | Igen      | Egy karakterlánc, amely azonosítja az SKU-t.                               |
| országkód           | sztring   | Igen      | Ország/régió azonosítója.                                            |
| cél szegmens         | sztring   | No       | A szűréshez használt cél szegmenst azonosító karakterlánc. |
| reservationScope | sztring   | No | Ha egy Azure-beli foglalási SKU-hoz tartozó elérhetőségek listáját kérdezi le, akkor a AzurePlan-ra `reservationScope=AzurePlan` vonatkozó elérhetőségek listájának lekéréséhez válassza a következőt:. Zárja be ezt a paramétert, hogy lekérje a Microsoft Azure (MS-AZR-0145P) előfizetésekre vonatkozó elérhetőségek listáját.  |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-examples"></a>Példák kérése

#### <a name="availabilities-for-sku-by-country"></a>SKU-beli elérhetőségek országonként

Ezt a példát követve lekérheti az adott SKU-ra vonatkozó elérhetőségek listáját ország szerint:

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a>VIRTUÁLIS gépek foglalásának elérhetősége (Azure-csomag)

Ezt a példát követve megtekintheti az ország szerint az Azure-beli virtuálisgép-foglalási SKU-ket. Ez a példa az Azure-csomagokra vonatkozó SKU-ra vonatkozik:

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure (MS-AZR-0145P) előfizetések virtuális gépekre vonatkozó foglalásai

Ez a példa a Microsoft Azure (MS-AZR-0145P) előfizetésekre alkalmazható Azure-beli virtuálisgép-foglalások országbeli elérhetőségi listájának beszerzésére szolgál.

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse [**rendelkezésre állási**](product-resources.md#availability) erőforrások gyűjteményét tartalmazza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. Teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód     | Hibakód   | Leírás                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | A kért **targetSegment** való hozzáférés nem engedélyezett.                                                     |

### <a name="response-example"></a>Példa válaszra

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
