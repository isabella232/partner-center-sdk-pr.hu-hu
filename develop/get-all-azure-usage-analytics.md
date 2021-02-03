---
title: Az összes Azure-beli használatelemzési adat lekérése
description: Az összes Azure-használati elemzési információ beszerzése.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c281dcdeb93771a69a388ad64e1127b24156c809
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768168"
---
# <a name="get-all-azure-usage-analytics-information"></a>Az összes Azure-beli használatelemzési adat lekérése

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Az Azure használati elemzési információinak beszerzése az ügyfelek számára.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja |
|---------|-------------|
| **GET** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Usage/Azure http/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

|Paraméter        |Típus                        |Leírás               |
|:----------------|:---------------------------|:-------------------------|
|top              | sztring                     | A kérelemben visszaadni kívánt adatsorok száma. A maximális érték és az alapértelmezett érték, ha nincs megadva, 10000. Ha több sor van a lekérdezésben, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldalának lekérésére használható.                        |
|kihagyása             | int                        | A lekérdezésben kihagyni kívánt sorok száma. Használja ezt a paramétert a nagy adathalmazokon keresztüli lapra. Például `top=10000 and skip=0` lekéri az első 10000 sornyi adatsort, `top=10000 and skip=10000` lekérdezi a következő 10000 sort, és így tovább.                       |
|filter (szűrő)           | sztring                     | A kérelem *Filter* paraméterében egy vagy több olyan utasítás található, amely a válasz sorait szűri. Minden utasítás tartalmaz egy mezőt és egy értéket, amely társítva van az `eq` vagy `ne` operátorhoz, és a utasítások kombinálhatók a vagy a használatával `and` `or` . A következő karakterláncok megadására van lehetőség:<br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>**Példa**<br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> **Példa**<br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|aggregationLevel | sztring                    | Meghatározza azt az időtartományt, amely esetében az összesített adatokat le kell olvasni. A következő karakterláncok egyike lehet: `day` , `week` , vagy `month` . Ha nincs megadva, az alapértelmezett érték `day` .<br/><br/>                                              A paraméter nem támogatott a (z `aggregationLevel` `groupby` ) nélkül. A `aggregationLevel` paraméter a összes dátum mezőjére vonatkozik `groupby` .                                                      |
|OrderBy          |sztring                     | Az egyes telepítésekhez tartozó eredmény adatértékeit megrendelő utasítás. A szintaxis a következő: `...&orderby=field [order],field [order],...`. A `field` paraméter a következő karakterláncok egyike lehet:<br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> A *Order* paraméter nem kötelező, és az `asc` `desc` egyes mezőknél növekvő vagy csökkenő sorrendet adhat meg. A mező alapértelmezett értéke: `asc`.<br/><br/>**Példa**<br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|groupby          |sztring                    | Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítést. A következő mezőket adhatja meg:<br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>A visszaadott adatsorok tartalmazzák a paraméterben megadott mezőket `groupby`  és a *mennyiséget*.<br/><br/>A `groupby` paraméter használható a `aggregationLevel` paraméterrel.<br/><br/>**Példa**<br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse az [Azure használati](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) erőforrásainak gyűjteményét tartalmazza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20
}
```

## <a name="see-also"></a>Lásd még

- [Partnerközpont-elemzések – forrásanyagok](partner-center-analytics-resources.md)
