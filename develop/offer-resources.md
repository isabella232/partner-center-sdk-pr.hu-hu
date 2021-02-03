---
title: Ajánlatok erőforrásai
description: A viszonteladói katalógusban szereplő, az ügyfelek számára elérhetővé tenni kívánt termék leírása.
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 45af02705d2a03c7586ba6bf3a5537c3e4eec3c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767775"
---
# <a name="offer-resources"></a>Ajánlatok erőforrásai

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A viszonteladói katalógusban szereplő, az ügyfelek számára elérhetővé tenni kívánt termék leírása.

## <a name="offer"></a>Ajánlat

| Tulajdonság                    | Típus                      | Leírás                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | sztring                    | Az ajánlat azonosítója.                                                                                           |
| name                        | sztring                    | Az ajánlat neve.                                                                                                 |
| leírás                 | sztring                    | Az ajánlat leírása.                                                                                     |
| minimumQuantity             | int                       | A rendelkezésre álló minimális mennyiség.                                                                                 |
| maximumQuantity             | int                       | A rendelkezésre álló maximális mennyiség.                                                                                 |
| rang                        | int                       | Az ajánlat rangsorolása vagy prioritása más kategóriákhoz képest ugyanabban a termékcsaládban. Ezt a tulajdonságot csak akkor kell beállítani, ha egy adott termékcsaládhoz több ajánlat is van.  |
| URI                         | sztring                    | Az ajánlat URI-ja.                                                                                                  |
| területi beállítás                      | sztring                    | Az a területi beállítás, amelyben az ajánlat érvényes.                                                                          |
| ország                     | sztring                    | Az az ország/régió, ahol az ajánlat érvényes.                                                                    |
| category                    | [OfferCategory](#offercategory)           | Az ajánlat kategóriája.                                                                   |
| limitUnitOfMeasure          | sztring                    | A vásárlás korlátozásának típusát jelző érték. A lehetséges értékek a következők:<br/> "Nincs" – az előfizetések számának korlátozása a megvásárolt ajánlat alapján.<br/> "Párhuzamos" – az ügyfél bérlője számára egy adott időpontban létezhető előfizetések száma, beleértve az aktív vagy a megszakított előfizetéseket is. Ez az érték főként olyan kisméretű üzleti ajánlatokra vonatkozik, ahol a licencek száma kevesebb, mint 300. A de-provisionioned előfizetések nem számítanak.<br/> "Élettartam" – az ügyfél bérlője számára elérhető előfizetések száma. Ez az érték a legtöbb esetben alkalmazható a próbaverzióra. A de-provisionioned előfizetések nem számítanak.      |
| korlát                       | int                       | Az ajánlat által a limitUnitOfMeasure alapján megvásárolható előfizetések mennyisége.                |
| prerequisiteOffers          | sztring                    | Az előfeltételt jelentő ajánlatok.                                                                                        |
| isAddOn                     | boolean                   | Egy érték, amely azt jelzi, hogy ez a példány addon-e.                                                           |
| hasAddOns                   | boolean                   | Egy érték, amely azt jelzi, hogy az ajánlat rendelkezik-e kiegészítéssel.                                                           |
| isAvailableForPurchase      | boolean                   | Egy érték, amely azt jelzi, hogy a példány megvásárolható-e.                                             |
| számlázás                     | sztring                    | Megadja a tétel megvásárlásának számlázási típusát: "None", "használati" vagy "licenc".                           |
| supportedBillingCycles      | sztringek tömbje          | Az ajánlat által támogatott számlázási ciklusokat jelzi. A támogatott értékek a [BillingCycleType](product-resources.md#billingcycletype) található tagok nevei   |
| isAutoRenewable             | boolean                   | Egy érték, amely azt jelzi, hogy az ajánlat automatikusan megújítható-e.                                                      |
| upgradeTargetOffers         | sztringek tömbje          | Azon ajánlatok listája, amelyekre ez az ajánlat frissíthető.                                                          |
| conversionTargetOffers      | sztringek tömbje          | Azon ajánlatok listája, amelyeket az ajánlat átalakíthat.                                                         |
| reselleeQualifications      | sztringek tömbje          | Az ügyfél által megkövetelt minősítések ahhoz, hogy egy partner megvásárolja az ajánlatot az adott ügyfél számára.     |
| resellerQualifications      | sztringek tömbje          | A partner által az ajánlat megvásárlásához szükséges minősítések az ügyfelek számára.                       |
| salesGroupId                | sztring                    | Az ajánlatok különálló megrendelésekre való csoportosítására szolgáló sztring.                                                             |
| Isztriai                     | boolean                   | Egy érték, amely azt jelzi, hogy ez egy próbaverziós ajánlat.                                                               |
| product                     | [OfferProduct](#offerproduct)           | Az ajánlat termékének beolvasása.                                                                           |
| unitType                    | sztring                    | Az egység típusa                                                                                      |
| linkek                       | [OfferLinks](#offerlinks)               | Az ajánlat "További információ" hivatkozása.                                                                    |
| attribútumok                  | [ResourceAttributes](utility-resources.md#resourceattributes) | Az ajánlathoz tartozó metaadat-attribútumok.                         |

## <a name="offercategory"></a>OfferCategory

Az ajánlat kategorizálását ismerteti. Ebbe beletartozik az ajánlat kategóriájának rangsorolása vagy prioritása, mint az azonos termékcsalád többi részén.

| Tulajdonság   | Típus                                                           | Leírás                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | sztring                                                         | A kategória azonosítója.                                                                                                                                                   |
| name       | sztring                                                         | A kategória neve.                                                                                                                                                         |
| rang       | int                                                            | A kategória rangsorolása vagy prioritása más kategóriákhoz képest ugyanabban az ajánlatban. Ezt a tulajdonságot csak akkor kell beállítani, ha egy adott ajánlathoz több ajánlati kategória is tartozik. |
| területi beállítás     | sztring                                                         | Az a területi beállítás, amelyben az ajánlat érvényes.                                                                                                                        |
| ország    | sztring                                                         | Az az ország/régió, ahol az ajánlat érvényes.                                                                                                                   |
| linkek      | [ResourceLinks](utility-resources.md#resourcelinks)           | A OfferCategory megfelelő erőforrás-hivatkozások.                                                                                                                     |
| attribútumok | [ResourceAttributes](utility-resources.md#resourceattributes) | A OfferCategory megfelelő metaadat-attribútumok.                                                                                                                |

## <a name="offerlinks"></a>OfferLinks

Hivatkozásokat tartalmaz az ajánlatra vonatkozó további információk megismeréséhez.

| Tulajdonság  | Típus | Leírás                 |
|-----------|------|-----------------------------|
| learnMore | Hivatkozás | A "További információ" hivatkozás.      |
| önálló      | Hivatkozás | Saját URI                |
| következő      | Hivatkozás | Az elemek következő lapja.     |
| korábbi  | Hivatkozás | Az elemek előző lapja. |

## <a name="offerproduct"></a>OfferProduct

Olyan termék vagy szolgáltatás, amelynek több ajánlata is van társítva, amelyek mindegyike különböző funkciókkal rendelkezik, és különböző felhasználói igényeket céloz meg.

| Tulajdonság | Típus   | Leírás              |
|----------|--------|--------------------------|
| Id       | sztring | A kategória azonosítója. |
| Name     | sztring | A kategória neve.       |
| Unit (Egység)     | sztring | A termék egysége.        |
