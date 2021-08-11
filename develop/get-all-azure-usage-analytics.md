---
title: Az összes Azure-beli használatelemzési adat lekérése
description: Az Azure használatelemzési információinak le szolgáltatása.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1d671c07185f92a36055af12d9de2e39adeab129bfcb2497da66d35807db270e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994081"
---
# <a name="get-all-azure-usage-analytics-information"></a>Az összes Azure-beli használatelemzési adat lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az Azure használatelemzési információinak lekért használata az ügyfelek számára.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja |
|---------|-------------|
| **Kap** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

|Paraméter        |Típus                        |Description               |
|:----------------|:---------------------------|:-------------------------|
|top              | sztring                     | A kérelemben visszaadni kívánt adatsorok száma. Ha nincs megadva, a maximális érték és az alapértelmezett érték 10000. Ha a lekérdezés több sort tartalmaz, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldal lekérésére használható.                        |
|Ugrál             | int                        | A lekérdezésben kihagyni kívánt sorok száma. Ezzel a paraméterrel nagy adatkészletek között lapokat laposszunk. A például lekéri az első 10000 adatsort, lekéri a következő `top=10000 and skip=0` `top=10000 and skip=10000` 10000 adatsort és így tovább.                       |
|filter (szűrő)           | sztring                     | A *kérés* szűrőparamétere egy vagy több olyan utasításokat tartalmaz, amelyek szűrik a válasz sorait. Minden utasítás tartalmaz egy mezőt és egy értéket, amely az vagy operátorhoz van társítva, és az utasítások kombinálhatók `eq` `ne` a vagy a `and` `or` használatával. A következő sztringeket adhatja meg:<br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>**Példa**<br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> **Példa**<br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|aggregationLevel | sztring                    | Megadja az összesített adatok lekérésének időtartományát. A következő sztringek egyike lehet: `day` , `week` vagy `month` . Ha nincs meghatározva, az alapértelmezett érték `day` a .<br/><br/>                                              A `aggregationLevel` paraméter nem támogatott a `groupby` nélkül. A `aggregationLevel` paraméter a összes, a-ban található dátummezőre vonatkozik. `groupby`                                                      |
|orderby          |sztring                     | Egy utasítás, amely minden telepítéshez megrendeli az eredményadatértékeket. A szintaxis a következő: `...&orderby=field [order],field [order],...`. A `field` paraméter a következő sztringek egyike lehet:<br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> A *rendelési* paraméter megadása nem kötelező, és a értéke vagy lehet, ha növekvő vagy csökkenő sorrendet ad meg az `asc` egyes `desc` mezőkhöz. A mező alapértelmezett értéke: `asc`.<br/><br/>**Példa**<br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|groupby          |sztring                    | Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítőt. A következő mezőket adhatja meg:<br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>A visszaadott adatsorok tartalmazzák a paraméterben és a `groupby` Quantity mezőben megadott *mezőket.*<br/><br/>A `groupby` paraméter a paraméterrel együtt `aggregationLevel` használható.<br/><br/>**Példa**<br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha a művelet sikeres, a válasz törzse azure-beli [használati erőforrások gyűjteményét](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) tartalmazza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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
