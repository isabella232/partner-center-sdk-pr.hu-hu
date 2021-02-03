---
title: Az összes keresés elemzési adatainak lekérése
description: Az összes keresési elemzési információ beolvasása.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 967f8d0ed2d276e0f68a047204b64d83dc69da95
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767712"
---
# <a name="get-all-search-analytics-information"></a>Az összes keresés elemzési adatainak lekérése

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Az összes keresési elemzési információ beszerzése az ügyfelek számára.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja |
|---------|-------------|
| **GET** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Search http/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

|    Paraméter     |  Típus  |                                                                                                                   Leírás                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      filter (szűrő)      | sztring |                                                                     A szűrési feltételnek megfelelő adatok visszaadása. </br> **Példa**</br> `.../search?filter=field eq 'value'`                                                                     |
|     groupby      | sztring |                                         A a kifejezéseket és a dátumokat is támogatja. Rövidzárlat-logika a gyűjtők számának korlátozásához. </br> **Példa**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | sztring | A *aggregationLevel* paraméterhez *groupby* szükséges. A *aggregationLevel* paraméter a *groupby* lévő összes Date mezőre vonatkozik. </br> **Példa**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       top        | sztring |                                                                     Az oldal korlátja 10000. 10000-nál kisebb értéket vesz fel.  </br> **Példa**</br>  `.../search?top=100`                                                                     |
|       kihagyása       | sztring |                                                                                  A kihagyni kívánt sorok száma. </br> **Példa**</br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

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

Ha ez sikeres, a válasz törzse [keresési](partner-center-analytics-resources.md#search-resource) erőforrások gyűjteményét tartalmazza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

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
