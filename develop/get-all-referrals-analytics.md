---
title: Az összes javaslat elemzési adatainak lekérése
description: Az összes átirányítási elemzés információjának beolvasása.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: b470c59cecf8b214e6d90a244e928e5d15ebd3e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767928"
---
# <a name="get-all-referrals-analytics-information"></a>Az összes javaslat elemzési adatainak lekérése

**A következőkre vonatkozik**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Az összes átirányítási elemzés információinak beszerzése az ügyfelek számára.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja |
|---------|-------------|
| **GET** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Referrals http/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

| Paraméter | Típus | Leírás |
|-----------|------|-------------|
| filter (szűrő) | sztring | A szűrési feltételnek megfelelő adatok visszaadása.</br> **Példa**</br>  `.../referrals?filter=field eq 'value'` |
| groupby | sztring | A a kifejezéseket és a dátumokat is támogatja. Rövidzárlat-logika a gyűjtők számának korlátozásához.</br> **Példa**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | sztring | A *aggregationLevel* paraméterhez *groupby* szükséges. A *aggregationLevel* paraméter a *groupby* lévő összes Date mezőre vonatkozik.</br> **Példa**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | sztring | Az oldal korlátja 10000. 10000-nál kisebb értéket vesz fel.</br> **Példa**</br> `.../referrals?top=100`</br> |
| kihagyása | sztring | A kihagyni kívánt sorok száma.</br> **Példa**</br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse az [átirányítási](partner-center-analytics-resources.md#referrals-resource) erőforrások gyűjteményét tartalmazza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```

## <a name="see-also"></a>Lásd még

- [Partnerközpont-elemzések – forrásanyagok](partner-center-analytics-resources.md)
