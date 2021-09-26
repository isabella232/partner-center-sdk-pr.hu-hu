---
title: Előléptetési jogosultság ellenőrzése
description: Ellenőrzi, hogy egy ügyféltranzakció jogosult-e egy adott előléptetésre.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: ad3346ddca0438c0011e2c6fd03c3ec00b1a1fe3
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/24/2021
ms.locfileid: "128715992"
---
# <a name="verify-promotion-eligibility"></a>Az előléptetésre való jogosultság ellenőrzése

**A következőre vonatkozik:**

- Partnerközpont

**Megfelelő szerepkörök**

- Globális rendszergazda
- Rendszergazdai ügynök

> [!Note] 
> Az új kereskedelmi változások jelenleg csak a Microsoft 365 és a Dynamics 365 új kereskedelmi felhasználói élményének technikai előzetesében lévő partnerek számára érhetők el.

A parters ellenőrizheti, hogy egy ügyféltranzakció jogosult-e egy adott előléptetésre. Ez a metódus *Igaz értéket* ad vissza, ha az ügyféltranzakció jogosult egy adott előléptetésre. A partnerek ellenőrizhetik a jogosultságot a tranzakció beküldése előtt, így meggyőződve arról, hogy az előléptetés alkalmazva lesz.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- A jogosultság magában foglalja a megvásárolt termékváltozatot, a kiértékelt előléptetési azonosítót, a mennyiséget, az időszak időtartamát és a tranzakció számlázási ciklusát.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **POST**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/promotionEligibilities HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az elérhető promóciók visszaadása érdekében használja az alábbi lekérdezési paramétereket.

| Név                    | Típus     | Kötelező | Leírás                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **Vevőkód**  | **sztring** | Y        | Az érték egy GUID-formátumú ügyfél-bérlő-azonosító, amely egy azonosító, amellyel megadhatja az ügyfelet.          |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

A törzs a PromotionEligibilitiesRequestItems gyűjteményt tartalmazza. Ez a táblázat egy [PromotionEligibilitiesRequestItem](promotion-resources.md#promotioneligibilitiesrequestitem)tulajdonságát ismerteti.

| Tulajdonság        | Típus             | Kötelező        | Leírás                                                                                               |
|-----------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| catalogItemId (katalógusazonosító)   | sztring           | Igen             | A katalóguselem azonosítója.                         |
| quantity        | int | Igen        | A licencek vagy példányok száma.                 |
| termDuration (kifejezés-lekértség)    | DateTime         | Igen             | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek: P1M (egy hónap), P1Y (egy év) és P3Y (három év).   |
| billingCycle (számlázási ciklus)    | sztring | Igen     | A számlázási ciklus típusát jelző érték.   |
| promotionId (előléptetésazonosító)     | sztring           | Igen             | Az előléptetési elem azonosítója.                       | 

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/46632f71-f052-4384-8f84-4cdb6c12c2a1/promotionEligibilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
            "quantity": 1,
            "termDuration": "P1Y",
            "billingCycle": "Monthly",
            "promotionId": " CFQ7TTC0HL8W:0001:CFQ7TTC0K59M"
        }
    ]
}

```

## <a name="rest-response"></a>REST-válasz

Ha ez a módszer sikeres, a jogosultsági eredmények gyűjteményét adja vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely sikeres vagy sikertelen állapotot jelez, valamint további hibakeresési információkat tartalmaz. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "totalCount": 1,
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
            "quantity": 1,
            "termDuration": "P1Y",
            "billingCycle": "Monthly",
            "eligibilities": [
                {
                    "promotionId": "CFQ9TTC0HH4R:0001:CFQ8HGC0K77G",
                    "isEligible": false,
                    "errors": [
                        {
                            "type": "SeatCount",
                            "minRequiredSeats": 25,
                            "maxRequiredSeats": 500
                        },
                        {
                            "type": "Term",
                            "eligibleTerms": [
                                {
                                    "duration": "P3Y",
                                    "billingCycle": "Monthly"
                                }
                            ]
                        },
                        {
                            "type": "FirstPurchase"
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "PromotionEligibilities"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

