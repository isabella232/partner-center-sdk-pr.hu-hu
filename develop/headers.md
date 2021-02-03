---
title: Partnerközpont – REST-fejlécek
description: Ismerje meg a partner Center REST API által támogatott HTTP REST-kérelmek fejléceit és a REST-válaszok fejléceit.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9f506c8c610c2584912c24453288d0f3578b84e3
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768511"
---
# <a name="partner-center-rest-and-response-headers-supported-by-the-partner-center-rest-api"></a>A partner Center által támogatott REST-és válasz-fejlécek REST API 

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A partner Center REST API a következő HTTP-kéréseket és válasz-fejléceket támogatja. Nem minden API-hívás fogadja el az összes fejlécet.

## <a name="rest-request-headers"></a>REST-kérelmek fejlécei

A partner Center REST API a következő HTTP-kérések fejléceit támogatja.

| Fejléc                       | Leírás                                                                                                                                                                                                                                                                            | Érték típusa |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Authorization (Engedélyezés):               | Kötelező. Az engedélyezési jogkivonat az űrlap tulajdonosi &lt; jogkivonatában &gt; .                                                                                                                                                                                                                    | sztring     |
| Fogadja el                      | Megadja a kérelem és a válasz típusát: "Application/JSON".                                                                                                                                                                                                                           | sztring     |
| MS-kérelemazonosító:                | A hívás egyedi azonosítója, amely az azonosító-hatékonyság biztosítására szolgál. Ha időtúllépés van, az újrapróbálkozási hívásnak ugyanazt az értéket kell tartalmaznia. A válasz fogadása (sikeres vagy üzleti hiba) esetén az értéket vissza kell állítani a következő híváshoz.                                            | GUID       |
| MS-CorrelationId:            | A hívás egyedi azonosítója, hasznos a naplókhoz és a hálózati nyomkövetésekhez a hibák elhárítása érdekében. Az értéket minden hívásnál alaphelyzetbe kell állítani. Az összes műveletnek tartalmaznia kell ezt a fejlécet. További információ: a korrelációs azonosító adatai a [tesztben és a hibakeresésben](test-and-debug.md). | GUID       |
| MS-szerződés – verzió:         | Kötelező. Meghatározza a kért API verzióját; általános API-Version: v1, kivéve, ha másként van megadva a [forgatókönyvek](scenarios.md) szakaszban.                                                                                                                                  | sztring     |
| If-Match:                    | A Egyidejűség-vezérléshez használatos. Néhány API-híváshoz a If-Match fejlécen keresztül kell átadni a ETag. A ETag általában az erőforráson van, ezért a GET-Ting a legújabbat igényli. További információkért tekintse meg a ETag információit a [tesztben és a hibakeresésben](test-and-debug.md).                | sztring     |
| MS-PartnerCenter – alkalmazás | Választható. A partner Center REST APIt használó alkalmazás nevét adja meg.                                                                                                                                                                                             | sztring     |
| X területi beállítás:                    | Választható. Meghatározza azt a nyelvet, amelyben a rendszer a díjszabást adja vissza. Az alapértelmezett érték az "en-US". A támogatott értékek listáját lásd: a [partneri központ által támogatott nyelvek és területi beállítások](partner-center-supported-languages-and-locales.md).                                                                                                                                                                                                  | sztring     |

## <a name="rest-response-headers"></a>REST-válaszok fejlécei

A következő HTTP-válasz fejléceket lehet visszaadni a partner Center REST API.

| Fejléc            | Leírás                                                                                                                                                                                                                                 | Érték típusa |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Fogadja el           | Megadja a kérelem és a válasz típusát: "Application/JSON".                                                                                                                                                                                | sztring     |
| MS-kérelemazonosító:     | A hívás egyedi azonosítója, amely az azonosító-hatékonyság biztosítására szolgál. Ha időtúllépés van, az újrapróbálkozási hívásnak ugyanazt az értéket kell tartalmaznia. A válasz fogadása (sikeres vagy üzleti hiba) esetén az értéket vissza kell állítani a következő híváshoz. | GUID       |
| MS-CorrelationId: | A hívás egyedi azonosítója. Ez az érték hasznos lehet a naplók és hálózati Nyomkövetések hibaelhárításához a hiba megtalálásához. Az értéket minden hívásnál alaphelyzetbe kell állítani. Az összes műveletnek tartalmaznia kell ezt a fejlécet.                                                       | GUID       |
