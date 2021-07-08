---
title: Egy termék lekérése azonosító alapján
description: Lekérte a megadott termékerőforrást egy termékazonosítóval.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 769a4307dc3cebdc7ebbdcf51d9f2b67a9f4b7c2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874023"
---
# <a name="get-a-product-by-id"></a>Egy termék lekérése azonosító alapján

Lekérte a megadott termékerőforrást egy termékazonosítóval.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy termékazonosító.

## <a name="c"></a>C\#

Egy adott termék azonosító alapján való megkereséhez használja az **IAggregatePartner.Products** gyűjteményt, válassza ki az országot a **ByCountry()** metódussal, majd hívja meg a **ById() metódust.** Végül hívja meg a **Get() vagy** **a GetAsync()** metódust a termék visszaküldésére.

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

Ha azonosító alapján keres egy adott terméket, használja az **IAggregatePartner.getProducts** függvényt, válassza ki az országot a **byCountry()** függvény használatával, majd hívja meg a **byId()** függvényt. Végül hívja meg a **get()** függvényt a termék visszaküldésére.

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

Ha azonosító alapján keres egy adott terméket, hajtsa végre a [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) parancsot, és adja meg a **ProductId paramétert.** A **CountryCode** paraméter beállítások, ha nincs megadva, akkor a viszonteladóhoz társított ország lesz használva.

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{termékazonosító}?country={country} HTTP/1.1  |

### <a name="uri-parameter"></a>URI-paraméter

A megadott termék lekért értékével az alábbi elérésiút-paramétereket használhatja.

| Név                   | Típus     | Kötelező | Leírás                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| termékazonosító             | sztring   | Igen      | A terméket azonosító sztring.                           |
| ország                | sztring   | Igen      | Egy ország-/régióazonosító.                                            |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse tartalmaz egy [Product erőforrást.](product-resources.md#product)

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód     | Hibakód   | Leírás                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 400013       | A termék nem található.                                                     |

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "DZH318Z0BQ3Q",
    "title": "Virtual Machines DSv2 Series",
    "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "VirtualMachines",
            "displayName": "VirtualMachines"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3Q?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
