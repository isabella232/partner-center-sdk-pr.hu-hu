---
title: Az összes közvetett viszonteladó elemzési adatainak lekérése
description: A közvetett viszonteladók elemzési információinak lekért adatai.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 4252f5fcbbcb038f382408074c8fd6ede3fd1f58
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760742"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Az összes közvetett viszonteladó elemzési adatainak lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az összes közvetett viszonteladó elemzési információinak lekért információ az ügyfelek számára.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja |
|---------|-------------|
| **Kap** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/indirectresellers HTTP/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

| Paraméter                             | Típus     | Leírás                              |
|:--------------------------------------|:---------|:-----------------------------------------|
| partnerTenantId                       | sztring   | Annak a partnernek a bérlőazonosítója, amelyhez közvetett viszonteladói adatokat szeretne lekérni. |
| id                                    | sztring   | Közvetett viszonteladó azonosítója                                                                 |
| name                                  | sztring   | Annak a partnernek a neve, amelyhez közvetett viszonteladói adatokat szeretne lekérni.      |
| piac                                | sztring   | Annak a partnernek a piaca, amelyhez közvetett viszonteladói adatokat szeretne lekérni.    |
| firstSubscriptionCreationDate         | sztring UTC dátum- és időformátumban  | Annak az első előfizetésnek a létrehozási dátuma, amely alapján közvetett viszonteladói adatokat szeretne lekérni.  |
| latestSubscriptionCreationDate        | sztring UTC dátum- és időformátumban  | A legújabb előfizetés létrehozásának dátuma.                 |
| firstSubscriptionEndDate              | sztring UTC dátum- és időformátumban  | Az első alkalommal, amikor egy előfizetés véget ért.                        |
| latestSubscriptionEndDate             | sztring UTC dátum- és időformátumban  | Az előfizetések végének legkésőbbi dátuma.                  |
| firstSubscriptionSuspendedDate        | sztring UTC dátum és idő szerint         | Az előfizetések első felfüggesztésekor.                    |
| latestSubscriptionSuspendedDate       | sztring UTC dátum- és időformátumban  | Az előfizetések felfüggesztésének legkésőbbi dátuma.              |
| firstSubscriptionDeprovisionedDate    | sztring UTC dátum- és időformátumban  | Az első alkalommal, amikor egy előfizetést megszüntettek.                |
| latestSubscriptionDeprovisionedDate   | sztring UTC dátum- és időformátumban  | Bármely előfizetés megszüntetésének legkésőbbi dátuma.          |
| subscriptionCount (előfizetés száma)                     | double   | Előfizetések száma az összes hozzáadott értékkel hozzáadott viszonteladóhoz                                     |
| licenseCount (licencszám)                          | double   | Az összes hozzáadott értékkel rendelkező viszonteladó licencszáma.                                         |
| indirectResellerCount                 | double   | Közvetett viszonteladók száma                                                             |
|  top                                  | sztring   | A kérésben visszaadni kívánt adatsorok száma. Ha nincs megadva, a maximális érték és az alapértelmezett érték 10000. Ha a lekérdezés több sort tartalmaz, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldal lekérésére használható.  |
| Ugrál                                  | int      | A lekérdezésben kihagyni kívánt sorok száma. Ezzel a paraméterrel nagy adatkészletek között lapokat laposszunk. A például lekéri az első 10 000 adatsort, lekéri a következő **`top=10000 and skip=0`** **`top=10000 and skip=10000`** 10000 adatsort és így tovább.              |
| filter (szűrő)                                | sztring   | A *kérés* szűrőparamétere egy vagy több olyan utasításokat tartalmaz, amelyek szűrik a válasz sorait. Minden utasítás tartalmaz egy mezőt és egy értéket, amely az vagy operátorhoz van társítva, és az utasítások a vagy a használatával **`eq`** **`ne`** **`and`** **`or`** kombinálhatók. A következő mezőket adhatja meg:<br/><br/>     *partnerTenantId*<br/> *id*<br/> *Név*<br/>                *piac*<br/> *firstSubscriptionCreationDate*<br/> *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>         **Példa**<br/>              `.../indirectresellers?filter=market eq 'US'`<br/><br/>            **Példa**<br/>                `.../indirectresellers?filter=market eq 'US' or (firstSubscriptionCreationDate le cast('2018-01-01',Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast('2018-04-01',Edm.DateTimeOffset))` |              
| aggregationLevel (összesítési szint)                     | sztring    | Megadja az összesített adatok lekérésének időtartományát. A következő sztringek egyike lehet: &quot; &quot; day, &quot; week , vagy &quot; month &quot; &quot; . Ha nincs meghatározva, az alapértelmezett érték a &quot; day &quot; .<br/><br/>                                 `aggregationLevel` A nem támogatott a `aggregationLevel` nélkül. `aggregationLevel`A a `aggregationLevel`                         |
| orderby                              | sztring    | Az egyes telepítések eredményadatértékeit megrendelő utasítás. A szintaxis a következő: `...&orderby=field[order],field [order],...`. A mezőparaméter a következő sztringek egyike lehet:<br/><br/>                &quot;partnerTenantId&quot;<br/>                &quot;id&quot;<br/>                &quot;név&quot;<br/>                &quot;piac&quot;<br/>                &quot;firstSubscriptionCreationDate&quot;<br/>               &quot;latestSubscriptionCreationDate&quot;<br/>                &quot;firstSubscriptionEndDate&quot;<br/>               &quot;latestSubscriptionEndDate&quot;<br/>                &quot;firstSubscriptionSuspendedDate&quot;<br/>                &quot;latestSubscriptionSuspendedDate&quot;<br/>               &quot;firstSubscriptionDeprovisionedDate&quot;<br/>                &quot;latestSubscriptionDeprovisionedDate&quot;<br/>                &quot;subscriptionCount (előfizetés száma)&quot;<br/>                &quot;licenseCount (licencszám)&quot;<br/><br/>   A *rendelési* paraméter nem kötelező, és vagy lehet ; az egyes mezők növekvő vagy `asc` csökkenő `desc` sorrendjének megadásához. A mező alapértelmezett értéke: `asc`.<br/><br/>    **Példa**<br/>                `...&orderby=market,subscriptionCount`                                       |                   
| groupby (csoportosítás)                              | sztring    | Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítőt. A következő mezőket adhatja meg:<br/><br/>         *partnerTenantId*<br/>    *id*<br/>               *Név*<br/>                *piac*<br/>                *firstSubscriptionCreationDate*<br/>                *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>                 A visszaadott adatsorok tartalmazzák a záradékban megadott mezőket `groupby` és a következő mezőket:<br/><br/>            *indirectResellerCount*<br/>                *licenseCount (licencszám)*<br/>                *subscriptionCount (előfizetés száma)*<br/><br/>            A `groupby` paraméter a paraméterrel együtt `aggregationLevel` használható.<br/><br/>            **Példa**</br>               `...&groupby=ageGroup,market&aggregationLevel=week`                         |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha ez sikeres, a válasz törzse közvetett viszonteladói [erőforrások gyűjteményét](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics) tartalmazza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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
