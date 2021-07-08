---
title: Erőforrások ajánlata
description: Egy, a viszonteladói katalógusban felsorolt terméket ismertet, amely az ügyfeleknek kínálhat.
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 704e5580f2cdf84fc82b627e3b2ca165b81a3af5
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548107"
---
# <a name="offer-resources"></a>Erőforrások ajánlata

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Egy, a viszonteladói katalógusban felsorolt terméket ismertet, amely az ügyfeleknek kínálhat.

## <a name="offer"></a>Ajánlat

| Tulajdonság                    | Típus                      | Leírás                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | sztring                    | Az ajánlat azonosítója.                                                                                           |
| name                        | sztring                    | Az ajánlat neve.                                                                                                 |
| leírás                 | sztring                    | Az ajánlat leírása.                                                                                     |
| minimumQuantity (minimálisquantitás)             | int                       | Az elérhető minimális mennyiség.                                                                                 |
| maximumQuantity (Maximálisquantitás)             | int                       | Az elérhető maximális mennyiség.                                                                                 |
| rang                        | int                       | Az ajánlat rangsorolása vagy prioritása az ugyanabban a termékvonalon a többi kategóriához képest. Ezt a tulajdonságot csak akkor kell beállítani, ha egy adott terméksorhoz több ajánlat is van.  |
| Uri                         | sztring                    | Az ajánlat URI-ját.                                                                                                  |
| területi beállítás                      | sztring                    | Az a területi beállítás, amelyre az ajánlat vonatkozik.                                                                          |
| ország                     | sztring                    | Az az ország/régió, ahol az ajánlat érvényes.                                                                    |
| category                    | [OfferCategory (Ajánlatkategória)](#offercategory)           | Az ajánlat kategóriája.                                                                   |
| limitUnitOfMeasure          | sztring                    | A vásárlási korlátozás típusát jelző érték. A lehetséges értékek a következők:<br/> "Nincs" – A megvásárolt ajánlat alapján nincs korlátozva az előfizetések száma.<br/> "Egyidejű" – Az ügyfélbérlőben egy adott időpontban létező előfizetések száma, beleértve az aktív vagy lemondott előfizetéseket is. Ez az érték főleg kisvállalati ajánlatokra vonatkozik, ahol a licencszám kevesebb, mint 300. A nem kiépített előfizetések nem számítanak.<br/> "LifeTime" (Élettartam) – Az ügyfélbérlő teljes élettartama alatt létező előfizetések száma. Ez az érték a próbaverziókra a leginkább alkalmazható. A nem kiépített előfizetések nem számítanak.      |
| korlát                       | int                       | Az ajánlathoz megvásárolható előfizetések száma a limitUnitOfMeasure alapján.                |
| prerequisiteOffers          | sztring                    | Az előfeltételként szükséges ajánlatok.                                                                                        |
| isAddOn (IsAddOn)                     | boolean                   | Egy érték, amely azt jelzi, hogy ez a példány bővítmény-e.                                                           |
| hasAddOns (hasAddOns)                   | boolean                   | Egy érték, amely jelzi, hogy az ajánlat rendelkezik-e bővítményekkel.                                                           |
| isAvailableForPurchase      | boolean                   | Egy érték, amely jelzi, hogy ez a példány megvásárolható-e.                                             |
| számlázás                     | sztring                    | Megadja a tételvásárlás számlázási típusát: "nincs", "használat" vagy "licenc".                           |
| supportedBillingCycles      | sztringek tömbje          | Az ajánlat által támogatott számlázási ciklusokat jelzi. A támogatott értékek a [BillingCycleType](product-resources.md#billingcycletype) típusban található tagnevek   |
| isAutoRenewable             | boolean                   | Egy érték, amely jelzi, hogy az ajánlat automatikusan megújul-e.                                                      |
| upgradeTargetOffers         | sztringek tömbje          | Azon ajánlatok listája, amelyekre ez az ajánlat frissíthető.                                                          |
| conversionTargetOffers      | sztringek tömbje          | Azon ajánlatok listája, amelyekre az ajánlat konvertálható.                                                         |
| resleleQualifications      | sztringek tömbje          | Az ügyfél által az adott ügyfél számára az ajánlat megvásárlásához szükséges minősítések.     |
| resellerQualifications      | sztringek tömbje          | A partner által az ajánlat ügyfél számára való megvásárlásához szükséges minősítések.                       |
| salesGroupId (értékesítési csoportazonosító)                | sztring                    | Egy sztring, amely az ajánlatokat külön rendelésekbe csoportosítja.                                                             |
| isTrial (isTrial)                     | boolean                   | Egy érték, amely jelzi, hogy ez próbaverziós ajánlat-e.                                                               |
| product                     | [OfferProduct (Ajánlattermék)](#offerproduct)           | Lekérte az ajánlat termékét.                                                                           |
| unitType (egységtípus)                    | sztring                    | Az egység típusa.                                                                                      |
| Linkek                       | [OfferLinks (Ajánlatkapcsolatok)](#offerlinks)               | Az ajánlat "További információ" hivatkozása.                                                                    |
| Attribútumok                  | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | Az ajánlatnak megfelelő metaadat-attribútumok.                         |

## <a name="offercategory"></a>OfferCategory (Ajánlatkategória)

Egy ajánlat kategorizálását ismerteti. Ez magában foglalja az ajánlatkategória rangsorolását vagy prioritását az ugyanabban a termékvonalon található többi termékhez képest.

| Tulajdonság   | Típus                                                           | Leírás                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | sztring                                                         | A kategóriaazonosító.                                                                                                                                                   |
| name       | sztring                                                         | A kategória neve.                                                                                                                                                         |
| rang       | int                                                            | A kategória rangsorolása vagy prioritása az ugyanazon ajánlat többi kategóriájához képest. Ezt a tulajdonságot csak akkor kell beállítani, ha egy adott ajánlathoz egynél több ajánlatkategória tartozik. |
| területi beállítás     | sztring                                                         | Az a területi beállítás, amelyre az ajánlat vonatkozik.                                                                                                                        |
| ország    | sztring                                                         | Az az ország/régió, ahol az ajánlat érvényes.                                                                                                                   |
| Linkek      | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | Az OfferCategory erőforrás-hivatkozásai.                                                                                                                     |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | Az OfferCategory attribútumainak megfelelő metaadat-attribútumok.                                                                                                                |

## <a name="offerlinks"></a>OfferLinks (Ajánlatkapcsolatok)

Hivatkozásokat tartalmaz az ajánlattal kapcsolatos további információkért.

| Tulajdonság  | Típus | Leírás                 |
|-----------|------|-----------------------------|
| learnMore | Hivatkozás | A "További információ" hivatkozás.      |
| Önálló      | Hivatkozás | Az ön-URI                |
| Következő      | Hivatkozás | Az elemek következő oldala.     |
| Előző  | Hivatkozás | Az elemek előző oldala. |

## <a name="offerproduct"></a>OfferProduct (Ajánlattermék)

Olyan termék vagy szolgáltatás, amely több ajánlattal is társítva lehet, különböző funkciókkal és különböző ügyfél-igényekkel.

| Tulajdonság | Típus   | Leírás              |
|----------|--------|--------------------------|
| Id       | sztring | A kategóriaazonosító. |
| Name     | sztring | A kategória neve.       |
| Unit (Egység)     | sztring | A termékegység.        |
