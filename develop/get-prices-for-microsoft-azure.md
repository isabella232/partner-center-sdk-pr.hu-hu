---
title: Díjak lekérése a Microsoft Azure-tól
description: Azure-díjkártyák lekért valós idejű árai egy Azure-ajánlathoz. Az Azure díjszabása meglehetősen dinamikus, és gyakran változik.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4f66ab19ef3723fbaa27acff941cf48683a7c25c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548787"
---
# <a name="get-prices-for-microsoft-azure"></a>Díjak lekérése a Microsoft Azure-tól

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Azure-díjkártyák [lekért](azure-rate-card-resources.md) valós idejű árai egy Azure-ajánlathoz. Az Azure díjszabása meglehetősen dinamikus, és gyakran változik.

A használat nyomon követéséhez és a havi számla és az egyes ügyfelek számlái előrejelzéséhez kombinálhatja ezt az Azure Rate Card-lekérdezést az Microsoft Azure árainak lekéréséhez az ügyfél Azure-beli kihasználtsági rekordjainak lekérésére vonatkozó [kéréssel.](get-a-customer-s-utilization-record-for-azure.md)

Az árak piac és pénznem szerint különböznek, és ez az API figyelembe veszi a helyet. Alapértelmezés szerint az API a partnerprofil beállításait használja a Partnerközpont böngészőnyelven, és ezek a beállítások testre szabhatók. A helytudatosság különösen fontos, ha az értékesítéseket több piacon kezeli egyetlen központi irodából. További információ: [URI-paraméterek.](#uri-parameters)

## <a name="c"></a>C\#

Az Azure Rate Card beszerzéséhez hívja meg az [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) metódust az Azure-árakat tartalmazó [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) erőforrás visszaadása érdekében.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** Partnerközpont SDK **Osztály:** GetAzureRateCard.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Az Azure Rate Card beszerzéséhez hívja meg az **IAzureRateCard.get** függvényt az Azure-árakat tartalmazó díjszabási kártya részleteinek visszaadás érdekében.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Az Azure-kártya beszerzéséhez futtasa le a [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) parancsot az Azure-árakat tartalmazó díjszabási kártya részleteinek visszaadás érdekében.

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                        |
|---------|--------------------------------------------------------------------|
| **Kap** | *{baseURL}*/v1/ratecards/azure?currency={currency}&region={region} |

### <a name="uri-parameters"></a>URI-paraméterek

| Név     | Típus   | Kötelező | Leírás                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | sztring | No       | Nem kötelező hárombetűs ISO-kód az erőforrás-díjszabást megszabadtó pénznemhez `EUR` (például). A mező alapértelmezett értéke: `USD`. |
| régió   | sztring | No       | Választható kétbetűs ISO-ország-/régiókód, amely az ajánlat vásárlásának piacát jelzi `FR` (például). A mező alapértelmezett értéke: `US`.        |

A kérelembe be is [](headers.md#rest-request-headers) foglalhatja az opcionális X-Locale fejlécet. Ha nem tartalmazza az X-Locale fejlécet, a rendszer az alapértelmezett értéket ("en-US") használja.

- Ha a kérelemben pénznem- és régióparamétereket ad meg, az X-Locale értéke határozza meg a válasz nyelvét.

- Ha nem ad meg régió- és pénznemparamétereket a kérésben, az X-Locale értéke határozza meg a válasz régióját, pénznemét és nyelvét.

### <a name="request-header"></a>Kérelem fejléce

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha a kérés sikeres, egy [Azure Rate Card-erőforrást ad](azure-rate-card-resources.md) vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
