---
title: Előfizetés-elemzés beszerzése keresési lekérdezés alapján
description: A keresési lekérdezés által szűrt előfizetés-elemzési információk beolvasása.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1046ea3c7e813eedae4890eebf6356337c80ede
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767911"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>Előfizetés keresési lekérdezés szerint szűrt elemzési adatainak lekérése

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Az előfizetés elemzési információinak beszerzése az ügyfelek számára keresési lekérdezés alapján szűrve.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus | Kérés URI-ja |
|--------|-------------|
| **GET** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? Filter = {filter_string} |

### <a name="uri-parameters"></a>URI-paraméterek

A következő szükséges elérésiút-paraméter használatával azonosíthatja a szervezetét, és szűrheti a keresést.

| Név | Típus | Kötelező | Leírás |
|------|------|----------|-------------|
| filter_string | sztring | Igen | Az előfizetés-elemzésre alkalmazni kívánt szűrő. Az ebben a paraméterben használandó szintaxis, mezők és operátorok szűrése szintaxis és szűrés mezők szakaszban talál. |

### <a name="filter-syntax"></a>Szűrési szintaxis

A Filter paraméternek mező, érték és operátor kombinációk sorozatának kell lennie. Több kombináció is egyesíthető a **`and`** vagy **`or`** operátorok használatával.

A kódolás nélküli példa a következőképpen néz ki:

- Karakterlánc `?filter=Field operator 'Value'`
- Logikai `?filter=Field operator Value`
- Tartalmaz `?filter=contains(field,'value')`

### <a name="filter-fields"></a>Mezők szűrése

A kérelem Filter paraméterében egy vagy több olyan utasítás található, amely a válasz sorait szűri. Minden utasítás tartalmaz egy mezőt és egy értéket, amely társítva van a **`eq`** vagy **`ne`** operátorokhoz. Egyes mezők a,, **`contains`** , **`gt`** **`lt`** **`ge`** és **`le`** operátorokat is támogatják. Az utasítások kombinálhatók a **`and`** vagy **`or`** operátorok használatával.

A következő példák a szűrési karakterláncokra mutatnak:

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

A következő táblázat a Filter paraméter támogatott mezőinek és támogatási operátorának listáját tartalmazza. A karakterlánc-értékeket szimpla idézőjelek között kell megadni.

| Paraméter | Támogatott operátorok | Leírás |
|-----------|---------------------|-------------|
| autoRenewEnabled | `eq`, `ne` | Egy érték, amely azt jelzi, hogy az előfizetés automatikusan megújul-e. |
| commitmentEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Az előfizetés befejezésének dátuma. |
| creationDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Az előfizetés létrehozásának dátuma. |
| currentStateEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Az előfizetés aktuális állapotának változási dátuma. |
| customerMarket | `eq`, `ne` | Az az ország/régió, amelyben az ügyfél üzleti tevékenységet végez. |
| Customername ( | `contains` | Az ügyfél neve. |
| customerTenantId | `eq`, `ne` | Egy GUID-formázott karakterlánc, amely azonosítja az ügyfél bérlőjét. |
| deprovisionedDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Az előfizetés megszüntetésének dátuma. Az alapértelmezett érték null. |
| effectiveStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Az előfizetés megkezdésének dátuma. |
| friendlyName | `contains` | Az előfizetés neve. |
| id | `eq`, `ne` | Egy GUID-formázott karakterlánc, amely azonosítja az előfizetést. |
| lastRenewalDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Az előfizetés utolsó megújításának dátuma. Az alapértelmezett érték null. |
| lastUsageDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Az előfizetés legutóbbi használatának dátuma. Az alapértelmezett érték null. |
| partnerId | `eq`, `ne` | Az MPN-azonosító. Közvetlen viszonteladó esetén ez az érték lesz a partner MPN-azonosítója. Közvetett viszonteladó esetén ez az érték lesz a közvetett viszonteladó MPN-azonosítója. |
| partnerName | sztring | Annak a partnernek a neve, akivel az előfizetést megvásárolták |
| productName | `contains`, `eq`, `ne` | A termék neve. |
| providerName | sztring | Ha az előfizetési tranzakció a közvetett viszonteladóhoz kapcsolódik, a szolgáltató neve az a közvetett szolgáltató, aki megvásárolta az előfizetést.|
| status | `eq`, `ne` | Az előfizetés állapota. A támogatott értékek a következők: "ACTIVE", "FELFÜGGESZTett" vagy "kiépített". |
| Ügynökparamétert | `eq`, `ne` | Az előfizetés típusa. **Megjegyzés**: Ez a mező megkülönbözteti a kis-és nagybetűket. A támogatott értékek a következők: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| trialStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Az előfizetés Próbaidőszakának elindításának dátuma. Az alapértelmezett érték null. |
| trialToPaidConversionDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Az előfizetés próbaverzióról fizetettre való konvertálása dátuma. Az alapértelmezett érték null. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse olyan [előfizetési](partner-center-analytics-resources.md#subscription-resource) erőforrások gyűjteményét tartalmazza, amelyek megfelelnek a szűrési feltételeknek.

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
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="see-also"></a>Lásd még

- [Partnerközpont-elemzések – forrásanyagok](partner-center-analytics-resources.md)
