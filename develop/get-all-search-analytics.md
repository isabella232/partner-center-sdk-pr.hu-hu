---
title: Az összes keresés elemzési adatainak lekérése
description: A keresési elemzésekre vonatkozó összes információ lekért információ.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e789a013b01fb63a38c72f4fe94864ecf21f7e4b
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760164"
---
# <a name="get-all-search-analytics-information"></a>Az összes keresés elemzési adatainak lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az összes keresési elemzési információ lekért információ az ügyfelek számára.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja |
|---------|-------------|
| **Kap** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

|    Paraméter     |  Típus  |                                                                                                                   Leírás                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      filter (szűrő)      | sztring |                                                                     A szűrési feltételnek megfelelő adatokat ad vissza. </br> **Példa**</br> `.../search?filter=field eq 'value'`                                                                     |
|     groupby (csoportosítás)      | sztring |                                         A feltételeket és a dátumokat is támogatja. Rövid áramköri logika a gyűjtők számának korlátozására. </br> **Példa**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel (összesítési szint) | sztring | Az *aggregációszint* paraméterhez csoportosítás *szükséges.* Az *aggregátumszint* paraméter a csoportosítási gyűjtőben található összes *dátummezőre vonatkozik.* </br> **Példa**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       top        | sztring |                                                                     Az oldalkorlát 10000. 10000-esnél kisebb értéket vesz fel.  </br> **Példa**</br>  `.../search?top=100`                                                                     |
|       Ugrál       | sztring |                                                                                  A kihagyni kívánt sorok száma. </br> **Példa**</br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse keresési erőforrások [gyűjteményét](partner-center-analytics-resources.md#search-resource) tartalmazza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```

## <a name="see-also"></a>Lásd még

- [Partnerközpont-elemzések – forrásanyagok](partner-center-analytics-resources.md)
