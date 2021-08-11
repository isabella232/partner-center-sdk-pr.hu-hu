---
title: Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ország alapján)
description: A megadott termékhez és termékváltozathoz való rendelkezésre állások gyűjteményének lekérte az ügyfél országa szerint.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 2bc7ec0609fa03f91427df2944c39e4c0401d11b27370d812d96e4fd0eb1ee6a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993656"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a>Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ország alapján)

Ez a cikk azt ismerteti, hogyan lehet rendelkezésre állási gyűjteményt lekért egy adott országban egy adott termékhez és termékváltozathoz.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.

- Egy termékazonosító.

- Egy termékváltozat-azonosító.

- Egy ország.

## <a name="c"></a>C\#

Egy termékváltozat [rendelkezésre állási](product-resources.md#availability) listájának [lekért listája:](product-resources.md#sku)

1. Az adott termékváltozat műveleteinek interfészét [a Termékváltozat](get-a-sku-by-id.md) lekért azonosítója alapján lépéseit követve szerezze be.

2. A termékváltozat felületén válassza az **Availabilities (Rendelkezésre** állás) tulajdonságot, hogy lekérte a rendelkezésre állási műveletekhez szükséges interfészt.

3. (Nem kötelező) A **ByTargetSegment()** metódussal szűrheti a rendelkezésre állásokat célszegmens szerint.

4. A termékváltozat rendelkezésre állási gyűjteményének lekéréséhez hívja meg a **Get()** vagy a **GetAsync()** metódust.

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

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{termékazonosító}/termékváltozatok/{sku-id}/availabilities?country={országkód}&targetSegment={target-segment} HTTP/1.1     |

### <a name="uri-parameters"></a>URI-paraméterek

Az alábbi elérési út és lekérdezési paraméterek használatával lekérdezheti a termékváltozatok rendelkezésre állási listáját.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| termékazonosító             | sztring   | Yes      | A terméket azonosító sztring.                           |
| sku-id                 | sztring   | Yes      | A termékváltozatot azonosító sztring.                               |
| országkód           | sztring   | Yes      | Egy ország-/régióazonosító.                                            |
| célszegmens         | sztring   | No       | A szűréshez használt célszegmenst azonosító sztring. |
| reservationScope | sztring   | No | Az Azure-foglalási termékváltozatok rendelkezésre állási listájának lekérdezésekor adja meg a értéket az AzurePlanra vonatkozó rendelkezésre állások `reservationScope=AzurePlan` listájának lekérdezőjéhez. Zárja ki ezt a paramétert a Microsoft Azure (MS-AZR-0145P) előfizetések esetében alkalmazható rendelkezésre állások listájának lekértéhez.  |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-examples"></a>Példák kérésre

#### <a name="availabilities-for-sku-by-country"></a>Termékváltozatok rendelkezésre állása országonként

Kövesse ezt a példát egy adott termékváltozat rendelkezésre állási listájának országonkénti lekért listájához:

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a>Virtuálisgép-foglalások rendelkezésre állása (Azure-csomag)

Kövesse ezt a példát az Azure-beli virtuális gépek foglalási termékkódjaihoz országonkénti rendelkezésre állások listájának lekért listájához. Ez a példa az Azure-csomagokra vonatkozó SKUS-okat példázhatja:

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Virtuálisgép-foglalások rendelkezésre állása Microsoft Azure (MS-AZR-0145P) előfizetések esetében

Ebben a példában az egyes országok szerinti elérhetőségek listáját azon Azure-beli virtuális gépek foglalásainál adhatja meg, amelyek Microsoft Azure (MS-AZR-0145P) előfizetésre vonatkoznak.

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse rendelkezésre állási [**erőforrások gyűjteményét**](product-resources.md#availability) tartalmazza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [hibakódok.](error-codes.md)

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód     | Hibakód   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | A kért **targetSegment szolgáltatáshoz való hozzáférés** nem engedélyezett.                                                     |

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
