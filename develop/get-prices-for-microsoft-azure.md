---
title: Díjak lekérése a Microsoft Azure-tól
description: Azure Rate-kártya beszerzése valós idejű díjszabással az Azure-ajánlathoz. Az Azure díjszabása meglehetősen dinamikus, és gyakran változnak.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0716f0428b13604105b435a2ce8287a8b4609fea
ms.sourcegitcommit: 64c498d3571f2287305968890578bc7396779621
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/19/2020
ms.locfileid: "97768691"
---
# <a name="get-prices-for-microsoft-azure"></a>Díjak lekérése a Microsoft Azure-tól

**A következőkre vonatkozik**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Azure [Rate-kártya](azure-rate-card-resources.md) beszerzése valós idejű díjszabással az Azure-ajánlathoz. Az Azure díjszabása meglehetősen dinamikus, és gyakran változnak.

Ha nyomon szeretné követni a használatot, és segít megjósolni a havi számlát és az egyes ügyfelek számláit, kombinálhatja ezt az Azure Rate Card-lekérdezést úgy, hogy lekérje az [ügyfél által az Azure-hoz tartozó kihasználtsági rekordok beszerzésére](get-a-customer-s-utilization-record-for-azure.md)irányuló kéréssel Microsoft Azure árát.

Az árak a piac és a pénznem alapján eltérnek, és ez az API figyelembe veszi a helyet. Alapértelmezés szerint az API a partner-profil beállításait a partner Centerben és a böngésző nyelvén használja, és ezek a beállítások testreszabhatók. A hely ismertsége különösen akkor fontos, ha egyetlen, központosított irodában több piacon kezel értékesítéseket. További információ: URI- [Paraméterek](#uri-parameters).

## <a name="c"></a>C\#

Az Azure Rate kártya beszerzéséhez hívja meg a [**IAzureRateCard. Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) metódust egy olyan [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) -erőforrás visszaadásához, amely tartalmazza az Azure-árakat.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: GetAzureRateCard.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Az Azure Rate kártya beszerzéséhez hívja meg a **IAzureRateCard. Get** függvényt, amely visszaküldi az Azure-árakat tartalmazó kártya adatait.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Az Azure-kártya beszerzéséhez hajtsa végre a [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) parancsot az Azure-árakat tartalmazó kártya adatainak visszaküldéséhez.

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                        |
|---------|--------------------------------------------------------------------|
| **GET** | *{baseURL}*/v1/ratecards/Azure? pénznem = {pénznem} &régió = {régió} |

### <a name="uri-parameters"></a>URI-paraméterek

| Név     | Típus   | Kötelező | Leírás                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | sztring | No       | Nem kötelező három betűs ISO-kódot megadni ahhoz a pénznemhez, amelyben az erőforrás-díjszabást megadja (például `EUR` ). A mező alapértelmezett értéke: `USD`. |
| régió   | sztring | No       | Opcionális kétbetűs ISO ország-vagy régiókód, amely azt jelzi, hogy az ajánlat melyik piacon vásárolható meg (például `FR` ). A mező alapértelmezett értéke: `US`.        |

A kérelemben megadhatja a választható X-locale [fejlécet](headers.md#rest-request-headers) is. Ha nem tartalmazza az X-locale fejlécet, a rendszer az alapértelmezett értéket ("en-US") használja.

- Ha a kérelemben megadja a pénznem és a régió paramétereit, a rendszer az X területi beállítás értékét használja a válasz nyelvének meghatározására.

- Ha nem ad meg régió-és pénznem-paramétereket a kérelemben, a rendszer az X-locale értéket használja a válasz régiójának, pénznemének és nyelvének meghatározására.

### <a name="request-header"></a>Kérelem fejléce

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-válasz

Ha a kérelem sikeres, egy [Azure Rate Card](azure-rate-card-resources.md) -erőforrást ad vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 1545508
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57b25659-fc00-4215-87e7-2b09bac6845d
MS-RequestId: 870118d0-adbb-41a3-82d2-a3d45ade3c73
MS-CV: CYBB8PXMsEukJBIn.0
MS-ServerId: 201021413
Date: Wed, 01 Feb 2017 00:13:45 GMT

{
    "locale": "en",
    "currency": "USD",
    "isTaxIncluded": false,
    "meters": [{
            "id": "4b836326-7e19-46e6-8bce-1b19bb6cd91e",
            "name": "Unlimited Data - 1 Gbps",
            "rates": {
                "0": 7395.0
            },
            "tags": [],
            "category": "Networking",
            "subcategory": "ExpressRoute",
            "region": "Zone 2",
            "unit": "Connections",
            "includedQuantity": 0.0,
            "effectiveDate": "2015-09-01T00:00:00Z"
        }, {
            "id": "1e8f6d9f-8b40-4c97-80cc-cff87a290a93",
            "name": "Compute Hours",
            "rates": {
                "0": 3.9729
            },
            "tags": [],
            "category": "Cloud Services",
            "subcategory": "Standard_L16 Cloud Services",
            "region": "AU East",
            "unit": "1 Hour",
            "includedQuantity": 0.0,
            "effectiveDate": "2016-09-01T00:00:00Z"
        }, {
            "id": "7a2639ce-ae47-4413-9837-6b4f4b78be3d",
            "name": "Compute Hours",
            "rates": {
                "0": 0.1122
            },
            "tags": [],
            "category": "Virtual Machines",
            "subcategory": "Standard_D1_v2 VM (Windows)",
            "region": "BR South",
            "unit": "Hours",
            "includedQuantity": 0.0,
            "effectiveDate": "2017-01-01T00:00:00Z"
        }
    ],
    "offerTerms": [{
            "name": "Overage discount",
            "discount": 0.15,
            "excludedMeterIds": ["53cc0061-0fe2-4249-bf62-e1008c811f5c", "c82dbd27-c978-43a7-ad41-525a90d8962b"],
            "effectiveDate": "2014-01-01T00:00:00"
        }
    ],
    "attributes": {
        "objectType": "AzureRateCard"
    }
}
```
