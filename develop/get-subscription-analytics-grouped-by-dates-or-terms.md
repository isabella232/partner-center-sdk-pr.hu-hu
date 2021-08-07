---
title: Előfizetés-elemzések lekért dátumai vagy feltételei szerint csoportosítva
description: Előfizetés-elemzési információk lekért dátumok vagy kifejezések szerint csoportosítva.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 66336d3e5573598eb4810853ad2704bc8d2c76680292a4f5b4a3da9bb50936b8
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989678"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>Előfizetés-elemzések lekért dátumai vagy feltételei szerint csoportosítva

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Hogyan lehet lekért előfizetési elemzési adatokat az ügyfelekről dátumok vagy kifejezések szerint csoportosítva.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus | Kérés URI-ja |
|--------|-------------|
| **Kap** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries} |

### <a name="uri-parameters"></a>URI-paraméterek

Használja a következő kötelező elérésiút-paramétereket a szervezet azonosításához és az eredmények csoportosításához.

| Név | Típus | Kötelező | Leírás |
|------|------|----------|-------------|
| groupby_queries | sztringpárok és dateTime | Yes | Az eredmény szűréséhez megadott kifejezések és dátumok. |

### <a name="groupby-syntax"></a>GroupBy-szintaxis

A csoportosítási paraméternek vesszővel elválasztott mezőértékek sorozataként kell össze lennie.

Egy nem kódolatlan példa a következő:

```http
?groupby=termField1,dateField1,termField2
```

Az alábbi táblázat a csoportosítási csoportok támogatott mezőinek listáját tartalmazza.

| Mező | Típus | Description |
|-------|------|-------------|
| customerTenantId (customerTenantId) | sztring | Egy GUID-formátumú sztring, amely azonosítja az ügyfélbérlőt. |
| customerName (ügyfél neve) | sztring | Az ügyfél neve. |
| customerMarket | sztring | Az az ország/régió, ahol az ügyfél üzleti tevékenységhez tartozik. |
| id | sztring | Egy GUID-formátumú sztring, amely azonosítja az előfizetést. |
| status | sztring | Az előfizetés állapota. A támogatott értékek: "ACTIVE", "SUSPENDED" vagy "DEPROVISIONED". |
| Productname | sztring | A termék neve. |
| subscriptionType (előfizetés típusa) | sztring | Az előfizetés típusa. Megjegyzés: Ez a mező megkülönbözteti a kis- és nagybetűket. Támogatott értékek: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| autoRenewEnabled | Logikai | Egy érték, amely jelzi, hogy az előfizetés automatikusan megújul-e. |
| partnerazonosító  | sztring | Az MPN-azonosító. Közvetlen viszonteladó esetén ez a paraméter a partner MPN-azonosítója lesz. Közvetett viszonteladó esetén ez a paraméter a közvetett viszonteladó MPN-azonosítója lesz. |
| friendlyName (rövid név) | sztring | Az előfizetés neve. |
| partnerName | sztring | Annak a partnernek a neve, aki számára az előfizetést megvásárolták |
| providerName (szolgáltató neve) | sztring | Ha az előfizetési tranzakció a közvetett viszonteladóra történik, a szolgáltató neve az a közvetett szolgáltató, aki megvásárolta az előfizetést.
| creationDate (Létrehozás dátuma) | sztring UTC dátum-idő formátumban | Az előfizetés létrehozási dátuma. |
| effectiveStartDate | sztring UTC dátum-idő formátumban | Az előfizetés kezdési dátuma. |
| commitmentEndDate | sztring UTC dátum-idő formátumban | Az előfizetés végének dátuma. |
| currentStateEndDate | sztring UTC dátum-idő formátumban | Az előfizetés aktuális állapotának változásának dátuma. |
| trialToPaidConversionDate | sztring UTC dátum-idő formátumban | Az a dátum, amikor az előfizetés próbaverzióról fizetősre vált. Az alapértelmezett érték a null. |
| trialStartDate | sztring UTC dátum-idő formátumban | Az előfizetés próbaidőszakának elindulásának dátuma. Az alapértelmezett érték a null. |
| lastUsageDate (lastUsageDate) | sztring UTC dátum-idő formátumban | Az előfizetés utolsó használt dátuma. Az alapértelmezett érték a null. |
| megszüntetésDate | sztring UTC dátum-idő formátumban | Az előfizetés megszüntetésének dátuma. Az alapértelmezett érték a null. |
| lastRenewalDate (lastRenewalDate) | sztring UTC dátum-idő formátumban | Az előfizetés utolsó megújításának dátuma. Az alapértelmezett érték a null. |

### <a name="filter-fields"></a>Mezők szűrése

A következő táblázat a nem kötelező szűrőmezőket és azok leírását tartalmazza:

| Mező | Típus |  Description |
|-------|------|--------------|
| top | int | A kérelemben visszaadni kívánt adatsorok száma. Ha az érték nincs megadva, a maximális érték és az alapértelmezett érték 10000. Ha a lekérdezés több sort tartalmaz, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldal lekérésére használható. |
| Ugrál | int | A lekérdezésben kihagyni kívánt sorok száma. Ezzel a paraméterrel nagy adatkészletek között lapokat laposszunk. Például a top=10000 és a skip=0 lekéri az első 10000 adatsort, a top=10000 és a skip=10000 pedig a következő 10000 adatsort. |
| filter (szűrő) | sztring | Egy vagy több utasítás, amely szűri a válasz sorait. Minden filter utasítás tartalmaz egy mezőnevet a válasz törzséből, valamint egy értéket, amely a , vagy bizonyos mezőkhöz, az operátorhoz **`eq`** **`ne`** van **`contains`** társítva. Az utasítások kombinálhatók a vagy **`and`** a **`or`** használatával. A sztringértékeket a szűrőparaméterben idézőjelek közé kell tenni. A következő szakaszban felsoroljuk a szűrhető mezőket, valamint az ezekhez a mezőkhöz támogatott operátorokat. |
| aggregationLevel | sztring | Megadja az összesített adatok lekérésének időtartományát. A következő sztringek egyike lehet: **day,** **week**, vagy **month.** Ha az érték nincs megadva, az alapértelmezett érték **a dateRange.** **Megjegyzés:** Ez a paraméter csak akkor érvényes, ha egy dátummezőt ad át a groupBy paraméter részeként. |
| groupBy | sztring | Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítőt. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a [](partner-center-analytics-resources.md#subscription-resource) válasz törzse a megadott feltételek és dátumok szerint csoportosított előfizetési erőforrások gyűjteményét tartalmazza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a>Lásd még

[Partnerközpont-elemzések – forrásanyagok](partner-center-analytics-resources.md)
