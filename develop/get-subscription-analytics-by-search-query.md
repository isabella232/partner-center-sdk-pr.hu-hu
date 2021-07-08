---
title: Előfizetés-elemzés lekérdező lekérdezéssel
description: Előfizetés-elemzési információk keresési lekérdezés alapján szűrve való lekérdezhetők.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8df777b9a88206f8b22579f0f445c54d80f7cd64
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548736"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>Előfizetés keresési lekérdezés szerint szűrt elemzési adatainak lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Előfizetés-elemzési információk lekérdezhetők az ügyfelekről keresési lekérdezés alapján szűrve.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus | Kérés URI-ja |
|--------|-------------|
| **Kap** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string} |

### <a name="uri-parameters"></a>URI-paraméterek

A szervezet azonosításához és a keresés szűréséhez használja a következő szükséges elérésiút-paramétert.

| Név | Típus | Kötelező | Leírás |
|------|------|----------|-------------|
| filter_string | sztring | Igen | Az előfizetés-elemzésre alkalmazandó szűrő. A paraméterben használható szintaxist, mezőket és operátorokat a Szűrőszintaxis és a Szűrőmezők szakaszban láthatja. |

### <a name="filter-syntax"></a>Szűrőszintaxis

A szűrőparaméternek mező-, érték- és operátorkombinációk sorozatának kell lennie. Több kombináció kombinálható a vagy **`and`** **`or`** operátorok használatával.

Egy nem kódolatlan példa a következő:

- Karakterlánc: `?filter=Field operator 'Value'`
- Logikai: `?filter=Field operator Value`
- Tartalmaz `?filter=contains(field,'value')`

### <a name="filter-fields"></a>Mezők szűrése

A kérés szűrőparamétere egy vagy több olyan utasításokat tartalmaz, amelyek szűrik a válasz sorait. Minden utasítás tartalmaz egy mezőt és egy értéket, amely a vagy az **`eq`** **`ne`** operátorhoz van társítva. Egyes mezők a **`contains`** , , , és **`gt`** **`lt`** **`ge`** **`le`** operátorokat is támogatják. Az utasítások vagy operátorok **`and`** használatával **`or`** kombinálhatók.

Az alábbiakban példákat talál a szűrősringek használatára:

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

Az alábbi táblázat a szűrőparaméter támogatott mezőit és támogató operátorait tartalmazza. A sztringértékeket idézőjelek közé kell tenni.

| Paraméter | Támogatott operátorok | Leírás |
|-----------|---------------------|-------------|
| autoRenewEnabled | `eq`, `ne` | Egy érték, amely jelzi, hogy az előfizetés automatikusan megújul-e. |
| commitmentEndDate (kötelezettségvállalási deddátum) | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Az előfizetés végének dátuma. |
| creationDate (Létrehozás dátuma) | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Az előfizetés létrehozási dátuma. |
| currentStateEndDate (aktuális állapot: Dátum) | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Az a dátum, amikor az előfizetés aktuális állapota megváltozik. |
| customerMarket | `eq`, `ne` | Az az ország/régió, ahol az ügyfél üzleti tevékenységhez tartozik. |
| customerName (ügyfél neve) | `contains` | Az ügyfél neve. |
| customerTenantId (customerTenantId) | `eq`, `ne` | Egy GUID-formátumú sztring, amely azonosítja az ügyfélbérlőt. |
| megszüntetésDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Az előfizetés megszüntetésének dátuma. Az alapértelmezett érték a null. |
| effectiveStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Az előfizetés kezdési dátuma. |
| friendlyName (rövid név) | `contains` | Az előfizetés neve. |
| id | `eq`, `ne` | Egy GUID-formátumú sztring, amely azonosítja az előfizetést. |
| lastRenewalDate (lastRenewalDate) | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Az előfizetés utolsó megújításának dátuma. Az alapértelmezett érték a null. |
| lastUsageDate (lastUsageDate) | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Az előfizetés utolsó felhasznált dátuma. Az alapértelmezett érték a null. |
| partnerazonosító | `eq`, `ne` | Az MPN-azonosító. Közvetlen viszonteladó esetén ez az érték a partner MPN-azonosítója lesz. Közvetett viszonteladó esetén ez az érték a közvetett viszonteladó MPN-azonosítója lesz. |
| partnerName | sztring | Annak a partnernek a neve, aki számára az előfizetést megvásárolták |
| Productname | `contains`, `eq`, `ne` | A termék neve. |
| providerName (szolgáltató neve) | sztring | Ha az előfizetési tranzakció a közvetett viszonteladóra történik, a szolgáltató neve az a közvetett szolgáltató, aki megvásárolta az előfizetést.|
| status | `eq`, `ne` | Az előfizetés állapota. A támogatott értékek: "ACTIVE", "SUSPENDED" vagy "DEPROVISIONED". |
| subscriptionType (előfizetés típusa) | `eq`, `ne` | Az előfizetés típusa. **Megjegyzés:** Ez a mező megkülönbözteti a kis- és nagybetűket. Támogatott értékek: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| trialStartDate (próbaindításidátum) | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Az előfizetés próbaidőszakának elindulásának dátuma. Az alapértelmezett érték a null. |
| trialToPaidConversionDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Az a dátum, amikor az előfizetés próbaverzióról fizetősre vált. Az alapértelmezett érték a null. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha ez sikeres, a válasz törzse a szűrési feltételeknek megfelelő [előfizetési](partner-center-analytics-resources.md#subscription-resource) erőforrások gyűjteményét tartalmazza.

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
