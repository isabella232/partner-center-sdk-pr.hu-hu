---
title: Az összes előfizetés elemzési adatainak lekérése
description: Az összes előfizetés-elemzési információ lekért adatai.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 5c93f36491851be11c700388201443f2e951122e4129786abc3e064091605b8d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992602"
---
# <a name="get-all-subscription-analytics-information"></a>Az összes előfizetés elemzési adatainak lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Ez a cikk azt ismerteti, hogyan lehet lekért összes előfizetési elemzési információt lekért ügyfelek számára.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus | Kérés URI-ja |
|--------|-------------|
| **Kap** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

A következő táblázat a választható paramétereket és azok leírását sorolja fel:

| Paraméter | Típus |  Description |
|-----------|------|--------------|
| top | int | A kérelemben visszaadni kívánt adatsorok száma. Ha az érték nincs megadva, a maximális érték és az alapértelmezett érték `10000` . Ha a lekérdezés több sort tartalmaz, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldal lekérésére használható. |
| Ugrál | int | A lekérdezésben kihagyni kívánt sorok száma. Ezzel a paraméterrel nagy adatkészletek között lapokat laposszunk. A például lekéri az első 10000 adatsort, és lekéri a következő `top=10000` `skip=0` `top=10000` `skip=10000` 10000 adatsort. |
| filter (szűrő) | sztring | Egy vagy több utasítás, amely szűri a válasz sorait. Minden filter utasítás tartalmaz egy mezőnevet a válasz törzséből, valamint egy értéket, amely a , vagy bizonyos mezőkhöz, az operátorhoz **`eq`** **`ne`** van **`contains`** társítva. Az utasítások kombinálhatók a vagy **`and`** a **`or`** használatával. A sztringértékeket a szűrőparaméterben idézőjelek közé **kell tenni.** A következő szakaszban felsoroljuk a szűrhető mezőket, valamint az ezekhez a mezőkhöz támogatott operátorokat. |
| aggregationLevel | sztring | Megadja az összesített adatok lekérésének időtartományát. A következő sztringek egyike lehet: **day,** **week**, vagy **month.** Ha az érték nincs megadva, az alapértelmezett érték **a dateRange.** Ez a paraméter csak akkor érvényes, ha a groupBy paraméter részeként egy **dátummezőt ad** át. |
| groupBy | sztring | Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítőt. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse előfizetési erőforrások [**gyűjteményét**](partner-center-analytics-resources.md#subscription-resource) tartalmazza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a>Lásd még

- [Partnerközpont-elemzések – forrásanyagok](partner-center-analytics-resources.md)
