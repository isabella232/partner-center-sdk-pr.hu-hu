---
title: Erőforrások átalakítása
description: Megtudhatja, hogyan Partnerközpont API-konverziós erőforrások használatával a próba-előfizetések fizetős előfizetésre konvertálásához.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9e7f8985fa15f4959f3cb5a729e492bbb9f3f624a5812f5b87fc119f841dc87e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991871"
---
# <a name="conversion-resources-to-convert-trial-subscriptions-to-paid"></a>Erőforrások átváltása a próba-előfizetések fizetősre konvertálásához

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A konverziós erőforrások támogatják a próba-előfizetések fizetős előfizetésre való átalakítását.

## <a name="conversion"></a>Átalakítás

A próbaverziós előfizetés fizetős előfizetésre való konvertálásához használt adatokat tartalmazza.

| Tulajdonság | Típus | Description |
| -------- | ---- | ----------- |
| offerId (ajánlatazonosító) | sztring | Az eredeti próbaajánlat ajánlatazonosítója. |
| targetOfferId | sztring | A célajánlat ajánlatazonosítója. |
| orderId (rendelésazonosító) | sztring | A rendelés azonosítója. |
| quantity | int | A licencek száma. Az alapértelmezett érték a próbaverziós előfizetésben elérhető licencek száma. |
| billingCycle | sztring | Azt jelzi, hogy milyen gyakran kell fizetni a partnernek az előfizetésért. Lehetséges értékek: **Havi** (a partner számlázása havonta **történik),** Éves (a partner számlázása évente történik) vagy **Nincs** (a partner számlázása nem történik meg). Próbaverziós előfizetések esetén). |

## <a name="conversionerror"></a>ConversionError (Konverziós tényező)

Az átalakítás során bekövetkezett hibát jelöli.

| Tulajdonság | Típus | Description |
| -------- | ---- | ----------- |
| code | sztring | A problémához társított hibakód. Lehetséges értékek: **Egyéb** (általános hiba), **ConversionsNotFound** (nem található átalakítás a próba-előfizetéshez, amelybe konvertálni kell).
| leírás | sztring | A problémát leíró rövid szöveg. |

## <a name="conversionresult"></a>ConversionResult (Konverziós eredmény)

Az előfizetés átalakításának eredményét jelöli.

| Tulajdonság       | Típus                                | Description                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | sztring                              | Az előfizetés azonosítója.                                           |
| offerId (ajánlatazonosító)        | sztring                              | Az eredeti ajánlatazonosító.                                         |
| targetOfferId  | sztring                              | A célajánlat ajánlatazonosítója.                             |
| error          | [ConversionError (Konverziós tényező)](#conversionerror) | Az átalakítás megkísérlése során észlelt hiba, ha van ilyen. |