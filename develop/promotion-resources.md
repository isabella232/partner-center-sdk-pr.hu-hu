---
title: Előléptetési erőforrások
description: Az új kereskedelmi előfizetések tranzakcióira alkalmazott promóciók erőforrásait ismerteti.
ms.date: 09/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 6a0b38576f5756a127fe6ba787f970db9ac59be3
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/24/2021
ms.locfileid: "128715993"
---
# <a name="promotions-resources"></a>Előléptetési források

**A következőre vonatkozik:**

- Partnerközpont

**Megfelelő szerepkörök**

- Globális rendszergazda
- Rendszergazdai ügynök

> [!Note] 
> Az új kereskedelmi változások jelenleg csak a Microsoft 365 és a Dynamics 365 új kereskedelmi felhasználói élményének technikai előzetesében lévő partnerek számára érhetők el.

Az új kereskedelmi előfizetések tranzakcióira alkalmazott promóciók erőforrásait ismerteti.

## <a name="promotion"></a>Előléptetés

Termékváltozat megvásárlásakor alkalmazott kedvezmény, ha a jogosultsági feltételek teljesülnek.

| Tulajdonság          | Típus                    | Leírás                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| id | sztring                  | Az előléptetés azonosítója. |
| name | sztring                  | Az előléptetés rövid neve. |
| leírás | sztring                  | Az előléptetés leírása. |
| startDate (kezdőDátum) | sztring | Az előléptetés alkalmazható kezdési dátuma. |
| endDate (záródátum) | sztring  | Az előléptetés alkalmazható időszakának záródátuma. |
| requiredProducts (kötelező termékek) | kötelező termékek listája | Termék, termékváltozat részletei és díjszabási szabályzatok, amelyekre az előléptetés vonatkozik. | 
| properties | tulajdonságok listája | Az előléptetés tulajdonságai, beleértve azt is, hogy az előléptetés automatikusan alkalmazható-e. | 

## <a name="requiredproducts"></a>RequiredProducts (Kötelező termékek)

Termék, termékváltozat részletei és díjszabási szabályzatok, amelyekre az előléptetés vonatkozik.

| Tulajdonság          | Típus                    | Leírás                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| productId| sztring | Annak a terméknek az azonosítója, amely számára az előléptetés elérhető. |
| skuId (termékváltozatazonosító) | sztring | Annak a termékváltozatnak az azonosítója, amely számára az előléptetés elérhető. |
| Kifejezés | Időszak | Az az időtartam és számlázási ciklus, amely alatt az előléptetés elérhető. |
| pricingPolicies| A pricingPolicies listája | Az előléptetési kedvezmény típusait és értékeit meghatározó szabályzatok listája. |

## <a name="term"></a>Időszak

Egy olyan időszak, amelyre az előléptetés megvásárolható.

| Tulajdonság          | Típus                    | Leírás                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| duration          | sztring                  | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek: P1M (egy hónap), P1Y (egy év) és P3Y (három év). 
| billingCycle (számlázási ciklus)      | sztring | Leírja, hogy milyen gyakran lesz alkalmazva az előléptetés a számlázásra. Az értékek lehetnek Havi, Éves, OneTime vagy Ismeretlen. | 

## <a name="pricingpolicies"></a>PricingPolicies

Ismertesse az előléptetési kedvezmény típusait és értékeit.

| Tulajdonság          | Típus               | Leírás                                                                  |          
|-------------------|--------------------|------------------------------------------------------------------------------|
| típus | sztring | Annak a leírására, hogy a kedvezmény százalékos vagy díjfizetési kedvezményeken alapul-e. |
| érték | sztring  | Az alkalmazott kedvezmény összegét határozza meg. |

## <a name="properties"></a>Tulajdonságok

Az előléptetés tulajdonságai.

| Tulajdonság          | Típus               | Leírás                                        |
|-------------------|--------------------|----------------------------------------------------|
| isAutoApplicable  | logikai  | Jelzi, hogy az előléptetést automatikusan alkalmazzák-e, vagy a partnernek kell-e átesni rajta. |


## <a name="promotioneligibilitiesrequestitem"></a>PromotionEligibilitiesRequestItem

A tranzakciót és az előléptetés jogosultságát jelképező tulajdonságok.

| Tulajdonság          | Típus               | Leírás                                        |
|-------------------|--------------------|----------------------------------------------------|
| id | int| Az előléptetések elemazonosítója. |
| catalogItemId (katalógusazonosító) | sztring | A katalóguselem-azonosító, amelyre az előléptetés alkalmazva lesz. Tartalmazza a termékazonosítót, a termékváltozat-azonosítót és a rendelkezésre állási azonosítót. |
| quantity | int | A licencek vagy példányok száma. |
| termDuration (kifejezés-lekértség) | sztring | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek: P1M (egy hónap), P1Y (egy év) és P3Y (három év). |
| billingCycle | sztring | Leírja, hogy milyen gyakran lesz alkalmazva az előléptetés a számlázásra. Az értékek lehetnek Havi, Éves, OneTime vagy Ismeretlen. | 
| promotionID (előléptetésazonosító) | sztring | Az előléptetés azonosítója. |

## <a name="promotioneligibilities"></a>PromotionEligibilities (Előléptetési képességek)

Termékek, termékkódok és előléptetési képességeik listája.

| Tulajdonság          | Típus               | Leírás                                        |
|-------------------|--------------------|----------------------------------------------------|
| id | int| Az előléptetések elemazonosítója. |
| catalogItemId (katalógusazonosító) | sztring | A katalóguselem-azonosító, amelyre az előléptetés vonatkozni fog. Tartalmazza a termékazonosítót, a termékváltozat-azonosítót és a rendelkezésre állási azonosítót. |
| quantity | int | A licencek vagy példányok száma. |
| termDuration (kifejezés-lekértség) | sztring | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek: P1M (egy hónap), P1Y (egy év) és P3Y (három év). |
| billingCycle | sztring | Leírja, hogy milyen gyakran lesz alkalmazva az előléptetés a számlázásra. Az értékek lehetnek Havi, Éves, OneTime vagy Ismeretlen. | 
| az eligibilities (képességek) | Előléptetési képességek listája | Az előléptetés jogosultsági eredményeinek listáját jelöli. |

## <a name="promotioneligibility"></a>ElőléptetésEligibility

Termékek, termékkódok és előléptetési képességeik listája.

| Tulajdonság          | Típus               | Leírás                                        |
|-------------------|--------------------|----------------------------------------------------|
| promotionId (előléptetésazonosító) | sztring | Az előléptetés azonosítója. |
| isEligible | logikai | Leírja, hogy az előléptetés jogosult-e az adott jogosultságkérési elemre. |
| Hibák | A PromotionEligibilityErrors listája | Hibák, amelyek azt írják le, hogy egy előléptetési képesség kéréseleme miért nem volt jogosult. | 

## <a name="promotioneligibilityerror"></a>PromotionEligibilityError

Ez a cikk azt ismerteti, hogy egy előléptetési jogosultsági kérelemelem miért nem volt jogosult. 

| Tulajdonság          | Típus               | Leírás                                        |
|-------------------|--------------------|----------------------------------------------------|
| típus | sztring | Az előléptetés jogosultsági hibatípusai közé tartozhat az InvalidCatalogItemId, az InvalidPromotion, a PrerequisiteProductOwnership, a RedemptionLimit, a SeatCount, az OfferPurchasedPreviously vagy a Term. |
| leírás | sztring | Leírja, hogy az előléptetés jogosult-e az adott jogosultságkérési elemre. |

## <a name="redemptionlimitpromotioneligibilityerror"></a>RedemptionLimitPromotionEligibilityError

A beváltási korlát túllépési okának részleteit tartalmazza.

| Tulajdonság          | Típus               | Leírás                                        |
|-------------------|--------------------|----------------------------------------------------|
| maxPromotionRedemptionCount | int | Az előléptetések megszerzésének maximális száma. |
| remainingPromotionRedemptionCount| int | A fennmaradó számú alkalommal szerezhető be előléptetés. |

## <a name="seatcountpromotioneligibilityerror"></a>SeatCountPromotionEligibilityError

A helyszámkorlát túllépése okának részleteit tartalmazza. Mindkét érték nullázható.

| Tulajdonság          | Típus               | Leírás                                        |
|-------------------|--------------------|----------------------------------------------------|
| minimumRequiredSeats | Int? | Az előléptetés által támogatott minimális licencek. |
| maximumRequiredSeats | Int? | Az előléptetés által támogatott maximális licencek. |

## <a name="termpromotioneligibilityerror"></a>TermPromotionEligibilityError

Részletes információkat tartalmaz arról, hogy miért nem fogadták el az előléptetési kifejezést.

| Tulajdonság          | Típus               | Leírás                                        |
|-------------------|--------------------|----------------------------------------------------|
| eligibleTerms (jogosult feltételek) | PromotionTerm (Előléptetési idő) | Az előléptetésre jogosult feltételek támogatottak lesznek. |

## <a name="promotionterm"></a>PromotionTerm (Előléptetési idő)

A helyszámkorlát túllépése okának részleteit tartalmazza.

| Tulajdonság          | Típus               | Leírás                                        |
|-------------------|--------------------|----------------------------------------------------|
| billingCycle | sztring | Leírja, hogy milyen gyakran lesz alkalmazva az előléptetés a számlázásra. Az értékek lehetnek Havi, Éves, OneTime vagy Ismeretlen. |
| duration | sztring | A megvásárolt időszak időtartama. |




