---
title: A rendelkezésre állás beolvasása azonosító alapján
description: A megadott termék és SKU rendelkezésre állásának beolvasása a rendelkezésre állási azonosító használatával.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 824303d40e1dcb0405246c8e29562c4527d147fd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767715"
---
# <a name="get-the-availability-by-id"></a>A rendelkezésre állás beolvasása azonosító alapján

**A következőkre vonatkozik**

- Partnerközpont

A megadott termék és SKU rendelkezésre állásának beolvasása a rendelkezésre állási azonosító használatával.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- A termék azonosítója.

- SKU-AZONOSÍTÓ.

- Egy rendelkezésre állási azonosító.

## <a name="c"></a>C\#

Egy adott [rendelkezésre állás](product-resources.md#availability)részleteinek beszerzéséhez először a [SKU BEszerzése azonosítóval](get-a-sku-by-id.md) című cikkben ismertetett lépéseket követve szerezheti be egy adott [SKU](product-resources.md#sku) műveleteinek felületét. Az eredményül kapott felületen válassza a beszerzések tulajdonságot, hogy beszerezze **az elérhető** műveletekkel rendelkező felületet. Ezután adja át a rendelkezésre állási azonosítót a **ById ()** metódusnak, hogy lekérje az adott rendelkezésre állásra vonatkozó műveleteket, majd hívja a **Get ()** vagy a **GetAsync ()** függvényt a rendelkezésre állási adatok lekéréséhez.

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Egy adott [rendelkezésre állás](product-resources.md#availability)részleteinek beszerzéséhez először a [SKU BEszerzése azonosítóval](get-a-sku-by-id.md) című cikkben ismertetett lépéseket követve szerezheti be egy adott [SKU](product-resources.md#sku) műveleteinek felületét. Az eredményül kapott felületről válassza a **getAvailabilities** függvényt, és szerezzen be egy felületet a rendelkezésre álláshoz elérhető műveletekkel. Ezután adja át a rendelkezésre állási azonosítót a **byId ()** függvénynek, hogy lekérje az adott rendelkezésre álláshoz tartozó műveleteket, majd a **Get ()** függvény meghívásával kérje le a rendelkezésre állási adatokat.

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Egy adott [rendelkezésre állás](product-resources.md#availability)részleteinek beszerzéséhez hajtsa végre a [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) , és adja meg a **AvailabilityId**, a **országhívószám**, a **Termékkód** és a **SkuId** paramétereket a rendelkezésre állási adatok lekéréséhez.

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities/{Availability-ID}? ország = {országkód} http/1.1         |

### <a name="uri-parameter"></a>URI-paraméter

A következő elérési út és lekérdezési paraméterek használatával a rendelkezésre állási AZONOSÍTÓval kaphat egy adott rendelkezésre állást.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| termék azonosítója             | sztring   | Igen      | Egy GUID formátumú karakterlánc, amely azonosítja a terméket.            |
| SKU-azonosító                 | sztring   | Igen      | Egy GUID formátumú karakterlánc, amely azonosítja az SKU-t.                |
| rendelkezésre állás – azonosító        | sztring   | Igen      | Egy GUID formátumú karakterlánc, amely azonosítja a rendelkezésre állást.       |
| országkód           | sztring   | Igen      | Ország/régió azonosítója.                                            |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse [rendelkezésre állási](product-resources.md#availability) erőforrást tartalmaz.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód     | Hibakód   | Leírás                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | A termék nem található.                                                                                    |
| 404                  | 400018       | Az SKU nem található.                                                                                        |
| 404                  | 400019       | A rendelkezésre állás nem található.                                                                                   |

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
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
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
