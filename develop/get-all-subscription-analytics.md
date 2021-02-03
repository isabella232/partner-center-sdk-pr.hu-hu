---
title: Az összes előfizetés elemzési adatainak lekérése
description: Az előfizetés-elemzési információk beszerzése.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: f32fb99ad52939ae8e9de26276588d3022f18fbc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767711"
---
# <a name="get-all-subscription-analytics-information"></a>Az összes előfizetés elemzési adatainak lekérése

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ez a cikk azt ismerteti, hogyan kérhető le az összes előfizetés-elemzési információ az ügyfelek számára.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus | Kérés URI-ja |
|--------|-------------|
| **GET** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions http/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Az alábbi táblázat a választható paramétereket és azok leírásait tartalmazza:

| Paraméter | Típus |  Leírás |
|-----------|------|--------------|
| top | int | A kérelemben visszaadni kívánt adatsorok száma. Ha az érték nincs megadva, a maximális érték és az alapértelmezett érték `10000` . Ha több sor van a lekérdezésben, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldalának lekérésére használható. |
| kihagyása | int | A lekérdezésben kihagyni kívánt sorok száma. Használja ezt a paramétert a nagy adathalmazokon keresztüli lapra. Például, `top=10000` és `skip=0` lekérdezi az első 10000 sort, `top=10000` és `skip=10000` lekéri a következő 10000 sort. |
| filter (szűrő) | sztring | Egy vagy több olyan utasítás, amely a válasz sorait szűri. Minden szűrő-utasítás tartalmaz egy mezőnevet a válasz törzsében, valamint egy olyan értéket, amely a **`eq`** , a **`ne`** vagy bizonyos mezőkhöz társítva van **`contains`** . Az utasítások kombinálhatók a vagy a használatával **`and`** **`or`** . A karakterlánc-értékeket szimpla idézőjelek között kell megadni a **Filter** paraméterben. Tekintse meg a következő szakaszt a szűrhető mezők és a mezők által támogatott operátorok listájához. |
| aggregationLevel | sztring | Meghatározza azt az időtartományt, amely esetében az összesített adatokat le kell olvasni. A következő karakterláncok egyike lehet: **nap**, **hét** vagy **hónap**. Ha az érték nincs megadva, az alapértelmezett érték a **dateRange**. Ez a paraméter csak akkor érvényes, ha a **groupBy** paraméter részeként egy Date mezőt ad át. |
| groupBy | sztring | Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítést. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

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

Ha ez sikeres, a válasz törzse az [**előfizetési**](partner-center-analytics-resources.md#subscription-resource) erőforrások gyűjteményét tartalmazza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

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
