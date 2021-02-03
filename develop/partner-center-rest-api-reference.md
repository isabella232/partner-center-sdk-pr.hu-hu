---
title: Partnerközpont – REST API-referencia
description: Ismerje meg, hogy a CSP-partnerek hogyan használhatják a partner Center REST API-kat a CRM-és számlázási szoftverek Microsoft-rendszerekkel való integrálásához, hogy jobban kezeljék az ügyfelek fiókjait
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 3f83b2b73c3480f76646cae4fcbbcbacd31d4b3f
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768503"
---
# <a name="partner-center-rest-api-reference-to-rest-urls-rest-headers-rest-resources-and-rest-events"></a>A partner Center REST API a REST URL-címekre, a REST-fejlécekre, a REST-erőforrásokra és a REST-eseményekre

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

## <a name="partner-center-rest-api"></a>Partner Center REST API

A partner Center REST API segíti a Cloud Solution Provider (CSP) partnerei számára a meglévő CRM-vagy számlázási szoftverek integrálását a felhasználói fiókokat kezelő Microsoft-rendszerekkel, a megrendelések megrendelésével, az előfizetések kezelésével és a támogatási kérelmek kezelésével.

További információ arról, hogy mit tehet az API, beleértve a mintakódt is, a [forgatókönyvek](scenarios.md) témakörben, beleértve a háttér áttekintését.

A kódolás megkezdése előtt olvassa el az [első lépések](get-started.md) témakört. Ez a cikk a tesztelési és üzemi fiókok beállításával, a hitelesítés működésének beszerzésével és a mintakód megkeresésével kapcsolatos információkat tartalmaz.

## <a name="topics"></a>Témakörök

| Témakör | Leírás |
| ----- | ----------- |
| [Partnerközpont – REST URL-címek](partner-center-rest-urls.md) | Meghatározza a partner központ különböző verzióihoz REST API végpontokat. |
| [Partnerközpont – REST-fejlécek](headers.md) | Meghatározza a REST API által használt kérelem és válasz fejléceit. |
| [Partnerközpont – REST-erőforrások](partner-center-rest-resources.md) | Azokat a JSON-szerkezeteket határozza meg, amelyek a REST API használatához szükséges objektumokat jelölik. |
| [Partnerközpont – REST-események](partner-center-webhook-events.md) | Meghatározza a partner Center webhookok által támogatott REST-erőforrás-módosítási eseményeket. |
| [Partnerközpont – támogatott nyelvek és területi beállítások](partner-center-supported-languages-and-locales.md) | Felsorolja a partner Center API-k által támogatott területi beállításokat, nyelveket és ország/régió kódokat. |
| [Partnerközpont – webhookok](partner-center-webhooks.md) | Események fogadása, visszahívás hitelesítése és a partner Center webhook API-k használata egy esemény regisztrációjának létrehozásához, megtekintéséhez és frissítéséhez. |