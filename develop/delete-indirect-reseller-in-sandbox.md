---
title: Közvetett viszonteladó törlése a sandboxban
description: Információkat nyújt a tesztbox közvetett viszonteladóinak törlésével és a teljes tesztelés API-okkal való engedélyezésével kapcsolatban.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba1fd002ac62aba4e414d263b33ecc8153054602
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973009"
---
# <a name="delete-indirect-reseller-in-sandbox"></a>Közvetett viszonteladó törlése a sandboxban

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Németországhoz

Ez a dokumentum bemutatja, hogyan törölhet közvetett tesztkészlet-szolgáltatókat, és hogyan engedélyezheti a teljes tesztelést API-k használatával.

> [!Important]
> Ez a dokumentum azokat a funkciókat ismerteti, amelyek csak a sandbox környezetben engedélyezettek a közvetett modellélmények esetében.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.

## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller"></a>Sandbox Indirect Provider – Delete Sandbox Indirect Reseller 

Ez a funkció csak a Sandboxban érhető el, és lehetővé teszi a Sandbox indirect Resellers (Közvetett viszonteladók) létrehozására a Sandbox Indirect Providers (Közvetett viszonteladók) szolgáltatást.

1. A sandbox indirect reseller törlésének előfeltételei
    1. Az előfizetések felfüggesztése a Sandbox Indirect Reseller minden egyes ügyfele esetében
    2. Közvetett viszonteladó összes ügyfele törlése
2. A közvetett sandbox-viszonteladók engedélyezett maximális száma közvetett sandbox-szolgáltatónként. A közvetett sandbox (közvetett) viszonteladó törlése után a kvóta alaphelyzetbe áll.

## <a name="delete-sandbox-indirect-reseller-through-api"></a>Delete Sandbox Indirect Reseller through API

### <a name="rest-request"></a>REST-kérés

#### <a name="request-syntax"></a>Kérésszintaxis

| Metódus | Kérés URI-ja                                                                             |
|------------|-------------------------------------------------------------------------------------|
| **Töröl** | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId} |

#### <a name="request-headers"></a>Kérésfejlécek

- Ez az API idempotent (nem fog más eredményt eredményezni, ha többször is meghívja)
- Szükség van egy kérésazonosítóra és egy korrelációs azonosítóra
- További információ: [REST Partnerközpont fejlécek](headers.md)

### <a name="request-example"></a>Példa kérésre

Töröl https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}

```http
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

####  <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Feb 2021 00:43:02 GMT
```

#### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint egyéb hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

Ez a metódus a következő sikeres állapotot és hibakódokat adja vissza:

| HTTP-állapotkód                     | Hibakód     | Leírás                                      |
|--------------------------------------|----------------|--------------------------------------------------|
| 401                                  | 6002           | Jogosulatlan jogkivonat vagy nem tippszolgáltatói fiók |
| 403                                  | 6003           | A Delete Sandbox IR nem engedélyezett                 |
| 403                                  | 6004           | A sandbox IR-művelet létrehozása nem engedélyezett          |
| 409                                  | 1003           | Ütközés a bérlő létrehozása során                   |
