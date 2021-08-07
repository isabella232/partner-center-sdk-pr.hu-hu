---
title: Az összes javaslat elemzési adatainak lekérése
description: A hivatkozások elemzési információinak lekérte.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: 8fded9cc9d540fa1f7f3fcb38620c26b85c1c6032ef0176e9bd043943a425f65
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992721"
---
# <a name="get-all-referrals-analytics-information"></a>Az összes javaslat elemzési adatainak lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az ügyfelekre vonatkozó összes hivatkozáselemzési információ lekérte.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja |
|---------|-------------|
| **Kap** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

| Paraméter | Típus | Description |
|-----------|------|-------------|
| filter (szűrő) | sztring | A szűrési feltételnek megfelelő adatokat ad vissza.</br> **Példa**</br>  `.../referrals?filter=field eq 'value'` |
| groupby | sztring | A feltételeket és a dátumokat is támogatja. Rövid áramköri logika a gyűjtők számának korlátozására.</br> **Példa**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | sztring | Az *aggregációszint* paraméterhez egy *csoportosítási paraméterre van szükség.* Az *aggregationLevel* paraméter a csoportosításban található összes *dátummezőre vonatkozik.*</br> **Példa**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | sztring | Az oldalkorlát 10000. 10000-esnél kisebb értéket vesz fel.</br> **Példa**</br> `.../referrals?top=100`</br> |
| Ugrál | sztring | A kihagyni kívánt sorok száma.</br> **Példa**</br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha ez sikeres, a válasz törzse hivatkozási erőforrások [gyűjteményét](partner-center-analytics-resources.md#referrals-resource) tartalmazza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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
