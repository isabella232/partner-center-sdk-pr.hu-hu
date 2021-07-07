---
title: A rendelkezésre állás lekért azonosítója
description: Lekérte a megadott termék és termékváltozat rendelkezésre állását egy rendelkezésre állási azonosítóval.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c31bc12d8d484cc8042f36aa865145600d9e6738
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760198"
---
# <a name="get-the-availability-by-id"></a>A rendelkezésre állás lekért azonosítója

Lekérte a megadott termék és termékváltozat rendelkezésre állását egy rendelkezésre állási azonosítóval.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

- Egy termékazonosító.

- Egy termékváltozat-azonosító.

- Egy rendelkezésre állási azonosító.

## <a name="c"></a>C\#

Egy adott rendelkezésre [](product-resources.md#availability)állás részleteinek lekért [](get-a-sku-by-id.md) lépéseit a Termékváltozat lekért azonosítója alapján lépéseit követve szerezze be az adott [termékváltozat](product-resources.md#sku) műveleteihez szükséges felületet. Az eredményül kapott felületen válassza az **Availabilities (Rendelkezésre** állások) tulajdonságot a rendelkezésre álláshoz elérhető műveletekkel való interfész beszerzéséhez. Ezt követően adja át a rendelkezésre állási azonosítót a **ById()** metódusnak az adott rendelkezésre álláshoz szükséges műveletek lekérése érdekében, majd hívja meg a **Get()** vagy **a GetAsync()** metódust a rendelkezésre állási adatok lekérése érdekében.

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

Egy adott rendelkezésre [](product-resources.md#availability)állás részleteinek lekért [](get-a-sku-by-id.md) lépéseit a Termékváltozat lekért azonosítója alapján lépéseit követve szerezze be az adott [termékváltozat](product-resources.md#sku) műveleteihez szükséges felületet. Az eredményül kapott felületen válassza a **getAvailabilities** függvényt a rendelkezésre álláshoz elérhető műveletekkel való felület beszerzéséhez. Ezután adja át a rendelkezésre állási azonosítót a **byId()** függvénynek az adott rendelkezésre álláshoz szükséges műveletek lekérése érdekében, majd hívja meg a get() függvényt a rendelkezésre állási adatok **lekérése** érdekében.

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

Egy adott rendelkezésre [](product-resources.md#availability)állás részleteinek lekérése érdekében hajtsa végre a [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) paramétert, és adja meg az **AvailabilityId,** **CountryCode,** **ProductId** és **SkuId** paramétereket a rendelkezésre állási adatok lekérése érdekében.

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{termékazonosító}/termékváltozatok/{sku-id}/availabilities/{availability-id}?country={országkód} HTTP/1.1         |

### <a name="uri-parameter"></a>URI-paraméter

Az alábbi elérési út és lekérdezési paraméterek használatával lekérdezheti az adott rendelkezésre állást egy rendelkezésre állási azonosító használatával.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| termékazonosító             | sztring   | Igen      | Egy GUID formátumú sztring, amely azonosítja a terméket.            |
| sku-id                 | sztring   | Igen      | Egy GUID formátumú sztring, amely azonosítja a termékváltozatot.                |
| rendelkezésre állási azonosító        | sztring   | Igen      | Egy GUID formátumú sztring, amely a rendelkezésre állást azonosítja.       |
| országkód           | sztring   | Igen      | Egy ország-/régióazonosító.                                            |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha ez sikeres, a válasz törzse tartalmaz egy [rendelkezésre állási erőforrást.](product-resources.md#availability)

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód     | Hibakód   | Leírás                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | A termék nem található.                                                                                    |
| 404                  | 400018       | A termékváltozat nem található.                                                                                        |
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
