---
title: Az összes közvetett viszonteladó elemzési adatainak lekérése
description: Az összes közvetett viszonteladói elemzési információ beszerzése.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 9f9c030278ba8fef9090f7be89064ac6054129ef
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768171"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Az összes közvetett viszonteladó elemzési adatainak lekérése

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A közvetett viszonteladók elemzési információinak beszerzése az ügyfelek számára.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja |
|---------|-------------|
| **GET** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/indirectresellers http/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

| Paraméter                             | Típus     | Leírás                              |
|:--------------------------------------|:---------|:-----------------------------------------|
| partnerTenantId                       | sztring   | Annak a partnernek a bérlői azonosítója, amelyhez közvetett viszonteladói adatmennyiséget kíván beolvasni. |
| id                                    | sztring   | Közvetett viszonteladó azonosítója                                                                 |
| name                                  | sztring   | Annak a partnernek a neve, amelyhez közvetett viszonteladói adatmennyiséget kíván beolvasni.      |
| piac                                | sztring   | Annak a partnernek a piaca, amelyhez közvetett viszonteladói adatmennyiséget kíván beolvasni.    |
| firstSubscriptionCreationDate         | karakterlánc UTC-dátum időformátuma  | Az első előfizetés létrehozásának dátuma, amely alapján a közvetett viszonteladói adatok lekérését kéri.  |
| latestSubscriptionCreationDate        | karakterlánc UTC-dátum időformátuma  | A legújabb előfizetés létrehozásának dátuma.                 |
| firstSubscriptionEndDate              | karakterlánc UTC-dátum időformátuma  | Az előfizetés első befejezése után.                        |
| latestSubscriptionEndDate             | karakterlánc UTC-dátum időformátuma  | Az előfizetés befejezésének utolsó dátuma.                  |
| firstSubscriptionSuspendedDate        | karakterlánc UTC dátum idő szerint         | Az előfizetés felfüggesztésének első időpontja.                    |
| latestSubscriptionSuspendedDate       | karakterlánc UTC-dátum időformátuma  | Az előfizetés felfüggesztésének utolsó dátuma.              |
| firstSubscriptionDeprovisionedDate    | karakterlánc UTC-dátum időformátuma  | Az előfizetés első kiépítésekor.                |
| latestSubscriptionDeprovisionedDate   | karakterlánc UTC-dátum időformátuma  | Az előfizetés megszűnésének utolsó dátuma.          |
| subscriptionCount                     | double   | Az összes hozzáadott értékhez tartozó előfizetés száma                                     |
| licenseCount                          | double   | Az összes hozzáadott értékhez tartozó licencek száma.                                         |
| indirectResellerCount                 | double   | Közvetett viszonteladók száma                                                             |
|  top                                  | sztring   | A kérelemben visszaadni kívánt adatsorok száma. A maximális érték és az alapértelmezett érték, ha nincs megadva, 10000. Ha több sor van a lekérdezésben, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldalának lekérésére használható.  |
| kihagyása                                  | int      | A lekérdezésben kihagyni kívánt sorok száma. Használja ezt a paramétert a nagy adathalmazokon keresztüli lapra. Például **`top=10000 and skip=0`** lekéri az első 10000 sornyi adatsort, **`top=10000 and skip=10000`** lekérdezi a következő 10000 sort, és így tovább.              |
| filter (szűrő)                                | sztring   | A kérelem *Filter* paraméterében egy vagy több olyan utasítás található, amely a válasz sorait szűri. Minden utasítás tartalmaz egy mezőt és egy értéket, amely társítva van az **`eq`** vagy **`ne`** operátorhoz, és a utasítások kombinálhatók a vagy a használatával **`and`** **`or`** . A következő mezőket adhatja meg:<br/><br/>     *partnerTenantId*<br/> *id*<br/> *Név*<br/>                *piac*<br/> *firstSubscriptionCreationDate*<br/> *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>         **Példa**<br/>              `.../indirectresellers?filter=market eq 'US'`<br/><br/>            **Példa**<br/>                `.../indirectresellers?filter=market eq 'US' or (firstSubscriptionCreationDate le cast('2018-01-01',Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast('2018-04-01',Edm.DateTimeOffset))` |              
| aggregationLevel                     | sztring    | Meghatározza azt az időtartományt, amely esetében az összesített adatokat le kell olvasni. A következő karakterláncok egyike lehet: &quot; nap &quot; , &quot; hét &quot; vagy &quot; hónap &quot; . Ha nincs megadva, az alapértelmezett érték a &quot; nap &quot; .<br/><br/>                                 `aggregationLevel` nem támogatott `aggregationLevel` . `aggregationLevel` a következőben szereplő összes **datefields** vonatkozik: `aggregationLevel`                         |
| OrderBy                              | sztring    | Az egyes telepítésekhez tartozó eredmény adatértékeit megrendelő utasítás. A szintaxis a következő: `...&orderby=field[order],field [order],...`. A Field paraméter a következő karakterláncok egyike lehet:<br/><br/>                &quot;partnerTenantId&quot;<br/>                &quot;id&quot;<br/>                &quot;név&quot;<br/>                &quot;piac&quot;<br/>                &quot;firstSubscriptionCreationDate&quot;<br/>               &quot;latestSubscriptionCreationDate&quot;<br/>                &quot;firstSubscriptionEndDate&quot;<br/>               &quot;latestSubscriptionEndDate&quot;<br/>                &quot;firstSubscriptionSuspendedDate&quot;<br/>                &quot;latestSubscriptionSuspendedDate&quot;<br/>               &quot;firstSubscriptionDeprovisionedDate&quot;<br/>                &quot;latestSubscriptionDeprovisionedDate&quot;<br/>                &quot;subscriptionCount&quot;<br/>                &quot;licenseCount&quot;<br/><br/>   A *Order* paraméter nem kötelező, és az is lehet, `asc` `desc` hogy az egyes mezőkhöz növekvő vagy csökkenő sorrendet kell megadni. A mező alapértelmezett értéke: `asc`.<br/><br/>    **Példa**<br/>                `...&orderby=market,subscriptionCount`                                       |                   
| groupby                              | sztring    | Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítést. A következő mezőket adhatja meg:<br/><br/>         *partnerTenantId*<br/>    *id*<br/>               *Név*<br/>                *piac*<br/>                *firstSubscriptionCreationDate*<br/>                *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>                 A visszaadott adatsorok tartalmazzák a `groupby` záradékban megadott mezőket és a következő mezőket:<br/><br/>            *indirectResellerCount*<br/>                *licenseCount*<br/>                *subscriptionCount*<br/><br/>            A `groupby` paraméter használható a `aggregationLevel` paraméterrel.<br/><br/>            **Példa**</br>               `...&groupby=ageGroup,market&aggregationLevel=week`                         |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse [közvetett viszonteladói](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics) erőforrások gyűjteményét tartalmazza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
{
    "partnerTenantId": "AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE",
    "id": "1111111",
    "name": "RESELLER NAME",
    "market": "US",
    "firstSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "latestSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "firstSubscriptionEndDate": "2018-11-07T00:00:00",
    "latestSubscriptionEndDate": "2018-11-07T00:00:00",
    "firstSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "latestSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "firstSubscriptionDeprovisionedDate": "0001-01-01T00:00:00",
    "latestSubscriptionDeprovisionedEndDate": "0001-01-01T00:00:00",
    "subscriptionCount": 10,
    "licenseCount": 20
}
```

## <a name="see-also"></a>Lásd még

- [Partnerközpont-elemzések – forrásanyagok](partner-center-analytics-resources.md)
