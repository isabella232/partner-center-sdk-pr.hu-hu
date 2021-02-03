---
title: Átalakítási erőforrások
description: Útmutató a partneri központ API-átalakítási erőforrásainak használatához a próbaverziós előfizetés fizetős előfizetésre való átalakításának elősegítése érdekében.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d3ade5a5af76e7c637962b6bfe076ac806f337bf
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768587"
---
# <a name="conversion-resources-to-convert-trial-subscriptions-to-paid"></a>Konverziós erőforrások a próbaverziós előfizetések kifizetésre való átalakításához

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A konverziós erőforrások támogatják a próbaverziós előfizetés fizetős előfizetésre való átalakítását.

## <a name="conversion"></a>Átalakítás

A próbaverziós előfizetés fizetős előfizetésre való átalakításához használt információkat tartalmazza.

| Tulajdonság | Típus | Leírás |
| -------- | ---- | ----------- |
| offerId | sztring | Az eredeti, próbaverziós ajánlat ajánlatának azonosítója. |
| targetOfferId | sztring | A célként megadott ajánlat azonosítója. |
| Rendeléskód | sztring | A sorrend azonosítója. |
| quantity | int | A licencek száma. Az alapértelmezett érték a próbaverziós előfizetésben található licencek száma. |
| billingCycle | sztring | Azt jelzi, hogy a partner milyen gyakran számítja fel az előfizetést. Lehetséges értékek: **havonta** (partner számlázása havonta), **évente** (a partnert évente számlázzák), vagy **egyik sem** (a partnert nem számlázzák. Próbaverziós előfizetésekhez használatos). |

## <a name="conversionerror"></a>ConversionError

Az átalakítás során előforduló hibát jelöli.

| Tulajdonság | Típus | Leírás |
| -------- | ---- | ----------- |
| code | sztring | A problémához tartozó hibakód. Lehetséges értékek: **egyéb** (általános hiba), **ConversionsNotFound** (nem található konverzió a próbaverziós előfizetéshez a verzióra).
| leírás | sztring | A problémát leíró rövid szöveg. |

## <a name="conversionresult"></a>ConversionResult

Az előfizetés konverziójának eredményét jelöli.

| Tulajdonság       | Típus                                | Leírás                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | sztring                              | Az előfizetés azonosítója.                                           |
| offerId        | sztring                              | Az eredeti ajánlat azonosítója.                                         |
| targetOfferId  | sztring                              | A célként megadott ajánlat azonosítója.                             |
| error          | [ConversionError](#conversionerror) | Hiba történt az átalakítás megkísérlése során, ha van ilyen. |