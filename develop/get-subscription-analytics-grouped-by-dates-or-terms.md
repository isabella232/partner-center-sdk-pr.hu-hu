---
title: Előfizetési elemzések beolvasása dátumok vagy kifejezések szerint csoportosítva
description: Előfizetés-elemzési információk beszerzése dátumok vagy kifejezések szerint csoportosítva.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4a9946027fa89f5a93fff5eede86e36a6be5b721
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767908"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>Előfizetési elemzések beolvasása dátumok vagy kifejezések szerint csoportosítva

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Az előfizetések elemzési információinak beszerzése az ügyfelek számára dátumok vagy kifejezések szerint csoportosítva.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus | Kérés URI-ja |
|--------|-------------|
| **GET** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? groupby = {groupby_queries} |

### <a name="uri-parameters"></a>URI-paraméterek

Használja a következő szükséges elérésiút-paramétereket a szervezet azonosításához és az eredmények csoportosításához.

| Név | Típus | Kötelező | Leírás |
|------|------|----------|-------------|
| groupby_queries | karakterláncok és dateTime párok | Igen | Az eredmény szűrésére szolgáló feltételek és dátumok. |

### <a name="groupby-syntax"></a>GroupBy szintaxisa

A Group By paraméternek vesszővel tagolt, mező típusú értékből kell állnia.

A kódolás nélküli példa a következőképpen néz ki:

```http
?groupby=termField1,dateField1,termField2
```

A következő táblázat a Group By által támogatott mezők listáját tartalmazza.

| Mező | Típus | Leírás |
|-------|------|-------------|
| customerTenantId | sztring | Egy GUID-formázott karakterlánc, amely azonosítja az ügyfél bérlőjét. |
| Customername ( | sztring | Az ügyfél neve. |
| customerMarket | sztring | Az az ország/régió, amelyben az ügyfél üzleti tevékenységet végez. |
| id | sztring | Egy GUID-formázott karakterlánc, amely azonosítja az előfizetést. |
| status | sztring | Az előfizetés állapota. A támogatott értékek a következők: "ACTIVE", "FELFÜGGESZTett" vagy "kiépített". |
| productName | sztring | A termék neve. |
| Ügynökparamétert | sztring | Az előfizetés típusa. Megjegyzés: Ez a mező megkülönbözteti a kis-és nagybetűket. A támogatott értékek a következők: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| autoRenewEnabled | Logikai | Egy érték, amely azt jelzi, hogy az előfizetés automatikusan megújul-e. |
| partnerId  | sztring | Az MPN-azonosító. Közvetlen viszonteladó esetén ez a paraméter lesz a partner MPN-azonosítója. Közvetett viszonteladó esetén ez a paraméter a közvetett viszonteladó MPN-azonosítója lesz. |
| friendlyName | sztring | Az előfizetés neve. |
| partnerName | sztring | Annak a partnernek a neve, akivel az előfizetést megvásárolták |
| providerName | sztring | Ha az előfizetési tranzakció a közvetett viszonteladóhoz kapcsolódik, a szolgáltató neve az a közvetett szolgáltató, aki megvásárolta az előfizetést.
| creationDate | karakterlánc UTC-dátum időformátuma | Az előfizetés létrehozásának dátuma. |
| effectiveStartDate | karakterlánc UTC-dátum időformátuma | Az előfizetés megkezdésének dátuma. |
| commitmentEndDate | karakterlánc UTC-dátum időformátuma | Az előfizetés befejezésének dátuma. |
| currentStateEndDate | karakterlánc UTC-dátum időformátuma | Az előfizetés aktuális állapotának változási dátuma. |
| trialToPaidConversionDate | karakterlánc UTC-dátum időformátuma | Az előfizetés próbaverzióról fizetettre való konvertálása dátuma. Az alapértelmezett érték null. |
| trialStartDate | karakterlánc UTC-dátum időformátuma | Az előfizetés Próbaidőszakának elindításának dátuma. Az alapértelmezett érték null. |
| lastUsageDate | karakterlánc UTC-dátum időformátuma | Az előfizetés legutóbbi használatának dátuma. Az alapértelmezett érték null. |
| deprovisionedDate | karakterlánc UTC-dátum időformátuma | Az előfizetés megszüntetésének dátuma. Az alapértelmezett érték null. |
| lastRenewalDate | karakterlánc UTC-dátum időformátuma | Az előfizetés utolsó megújításának dátuma. Az alapértelmezett érték null. |

### <a name="filter-fields"></a>Mezők szűrése

A következő táblázat az opcionális szűrési mezőket és azok leírásait tartalmazza:

| Mező | Típus |  Leírás |
|-------|------|--------------|
| top | int | A kérelemben visszaadni kívánt adatsorok száma. Ha az érték nincs megadva, a maximális érték és az alapértelmezett érték 10000. Ha több sor van a lekérdezésben, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldalának lekérésére használható. |
| kihagyása | int | A lekérdezésben kihagyni kívánt sorok száma. Használja ezt a paramétert a nagy adathalmazokon keresztüli lapra. Például a Top = 10000 és a skip = 0 lekérdezi az első 10000 adatsort, a Top = 10000 és a skip = 10000 lekéri a következő 10000 sort. |
| filter (szűrő) | sztring | Egy vagy több olyan utasítás, amely a válasz sorait szűri. Minden szűrő-utasítás tartalmaz egy mezőnevet a válasz törzsében, valamint egy olyan értéket, amely a **`eq`** , a **`ne`** vagy bizonyos mezőkhöz társítva van **`contains`** . Az utasítások kombinálhatók a vagy a használatával **`and`** **`or`** . A karakterlánc-értékeket szimpla idézőjelek között kell megadni a Filter paraméterben. Tekintse meg a következő szakaszt a szűrhető mezők és a mezők által támogatott operátorok listájához. |
| aggregationLevel | sztring | Meghatározza azt az időtartományt, amely esetében az összesített adatokat le kell olvasni. A következő karakterláncok egyike lehet: **nap**, **hét** vagy **hónap**. Ha az érték nincs megadva, az alapértelmezett érték a **dateRange**. **Megjegyzés**: Ez a paraméter csak akkor érvényes, ha a groupBy paraméter részeként egy Date mezőt ad át. |
| groupBy | sztring | Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítést. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

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

Ha ez sikeres, a válasz törzse az [előfizetési](partner-center-analytics-resources.md#subscription-resource) erőforrások gyűjteményét tartalmazza a megadott feltételek és dátumok szerint csoportosítva.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

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
