---
title: Partnerközpont – REST-fejlécek
description: Ismerje meg a HTTP REST-kérésfejléceket és a REST-válaszfejléceket, amelyek a Partnerközpont REST API.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3f09ab5808a9751f02e451da2027f6b35877390b
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548464"
---
# <a name="partner-center-rest-and-response-headers-supported-by-the-partner-center-rest-api"></a>Partnerközpont által támogatott REST- és válaszfejlécek Partnerközpont REST API 

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A következő HTTP-kérés- és válaszfejléceket támogatja a Partnerközpont REST API. Nem minden API-hívás fogad el minden fejlécet.

## <a name="rest-request-headers"></a>REST-kérelemfejlécek

A következő HTTP-kérésfejléceket támogatja a Partnerközpont REST API.

| Fejléc                       | Leírás                                                                                                                                                                                                                                                                            | Érték típusa |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Authorization (Engedélyezés):               | Kötelező. Az engedélyezési jogkivonat a következő formában: Bearer &lt; &gt; token.                                                                                                                                                                                                                    | sztring     |
| Elfogadja:                      | Megadja az "application/json" kérés- és választípust.                                                                                                                                                                                                                           | sztring     |
| MS-RequestId:                | A hívás egyedi azonosítója, amely az azonosító-azonosítót biztosítja. Időtúllépés esetén az újrapróbálkozási hívásnak ugyanazt az értéket kell tartalmaznia. A válasz (sikeres vagy sikertelen) fogadása esetén az értéket vissza kell állítani a következő híváshoz.                                            | GUID       |
| MS-CorrelationId:            | A hívás egyedi azonosítója, amely hasznos a naplókban és a hálózati nyomkövetésben a hibák elhárításához. Az értéket minden híváshoz alaphelyzetbe kell állítani. Minden műveletnek tartalmaznia kell ezt a fejlécet. További információkért tekintse meg a Korrelációs azonosítóra vonatkozó információkat [a Tesztelés és hibakeresés oldalon.](test-and-debug.md) | GUID       |
| MS-Contract-Version:         | Kötelező. Megadja a kért API verzióját; általában api-version: v1, hacsak másként nincs megadva a [Forgatókönyvek szakaszban.](scenarios.md)                                                                                                                                  | sztring     |
| If-Match (Ha egyezés):                    | Egyidejűség-vezérlésre használatos. Egyes API-hívásokhoz át kell adni az ETaget az If-Match fejlécen keresztül. Az ETag általában az erőforráson van, ezért a GET-ting a legújabbat igényli. További információ: ETag-információk: [Tesztelés és hibakeresés.](test-and-debug.md)                | sztring     |
| MS-PartnerCenter-Application | Választható. Az alkalmazást használó alkalmazás nevét adja Partnerközpont REST API.                                                                                                                                                                                             | sztring     |
| X területi:                    | Választható. Megadja a díjszabások visszaadási nyelvét. Az alapértelmezett érték az "en-US". A támogatott értékek listáját a támogatott nyelvek és [területi Partnerközpont tartalmazza.](partner-center-supported-languages-and-locales.md)                                                                                                                                                                                                  | sztring     |

## <a name="rest-response-headers"></a>REST-válaszfejlécek

A következő HTTP-válaszfejléceket a kiszolgáló Partnerközpont REST API.

| Fejléc            | Leírás                                                                                                                                                                                                                                 | Érték típusa |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Elfogadja:           | Megadja az "application/json" kérés- és választípust.                                                                                                                                                                                | sztring     |
| MS-RequestId:     | A hívás egyedi azonosítója, amely az azonosító-azonosítót biztosítja. Időtúllépés esetén az újrapróbálkozási hívásnak ugyanazt az értéket kell tartalmaznia. A válasz (sikeres vagy sikertelen) fogadása esetén az értéket vissza kell állítani a következő híváshoz. | GUID       |
| MS-CorrelationId: | A hívás egyedi azonosítója. Ez az érték a naplók és hálózati nyomkövetések hibaelhárításához hasznos, hogy megtalálja a hibát. Az értéket minden híváshoz alaphelyzetbe kell állítani. Minden műveletnek tartalmaznia kell ezt a fejlécet.                                                       | GUID       |
