---
title: Erőforrások váltása
description: Az új kereskedelmi előfizetések átváltása során használt erőforrásokat ismerteti.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 44867be3823414ab43957e789c0cd29aef44d956
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457309"
---
# <a name="transition-resources"></a>Erőforrások váltása

**A következőre vonatkozik:**

- Partnerközpont

**Megfelelő szerepkörök**

- Globális rendszergazda
- Rendszergazdai ügynök

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesző partnerek számára érhetők el.

Az egyik új kereskedelmi előfizetésről a másikra való áttéréshez használt erőforrásokat ismerteti.

## <a name="transitioneliblity"></a>TransitionEliblity (TransitionEliblity)

Az egyes előfizetés-váltási erőforrások viselkedését ismerteti.

| Tulajdonság          | Típus                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| CatalogItemId (Katalógusazonosító) | sztring                  | A katalóguselem-azonosító, amely a elemet ellenőrzi. |
| Cím  | sztring                  | A termékváltozat címe. |
| Description | sztring                  | A termékváltozat leírása. |
| Mennyiség | egész szám                 | A megvásárolandó új ajánlat mennyisége. |
| Képességek | TransitionEligibilityDetail listája | Az áttűnés jogosultsági részleteinek listája. | 

## <a name="transitioneligibilitydetail"></a>TransitionEligibilityDetail (TransitionEligibilityDetail)

Az egyéni átmenet jogosultsági adatait tartalmazó erőforrás viselkedését ismerteti.

| Tulajdonság          | Típus                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| IsEligible (IsEligible) | boolean | A jogosultságot adja vissza, amely érvényes vagy sem. |
| TransitionType (Átmeneti típus) | TransitionType (Átmeneti típus) | Az átváltás típusa. Ez lehet transition_with_license_transfer vagy transition_only. |
| Hibák | TransitionErrors (TransitionErrors) lista | A hibának megfelelő metaadat-attribútumok. |

## <a name="transition"></a>Átmenet

Az egyes előfizetés-váltási erőforrások viselkedését ismerteti.

| Tulajdonság          | Típus                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| FromCatalogItemId | sztring                  | A Katalógusból elemazonosító. |
| ToCatalogItemId (ToCatalogItemId)   | sztring                  | A Katalóguselem azonosítója. |
| ToSubscriptionId (Előíróazonosító)  | sztring                  | A To subscription id (Az előfizetéshez) azonosító. Ez csak akkor lesz kitöltve, ha az előfizetés megváltozik. Erre jelenleg csak az örökölt frissítésnek van szüksége, de a modern részleges átállás is szükséges. |
| Mennyiség          | egész szám                 | A célkatalógus-elemre áttért mennyiség. |
| TransitionType (Átmeneti típus)    | sztring              | Az átváltás típusa. Lehetséges értékek – transition_only, transition_with_license_transfer.   |
| Események            | TransitionEvents listája | Az átváltás eseményei. |

## <a name="transitionevent"></a>TransitionEvent (Áttűnés)Vent

Ismerteti, hogy miért nem hajtható végre frissítés.

| Tulajdonság          | Típus               | Leírás                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|------------------------------------------------------------------------------|
| Név | sztring | Az átváltási esemény neve. Lehetséges értékek Átalakítás vagy LicenseReassignment. |
| Állapot | sztring  | Az átváltási esemény állapota. Lehetséges Bejövő forgalom, Befejezve vagy Sikertelen értékek.  |
| Időbélyeg | DateTime | Az esemény UTC-időbélyege. |
| Hibák | TransitionErrors (TransitionErrors) lista | A hibának megfelelő metaadat-attribútumok. |

## <a name="transitionerror"></a>TransitionError (TransitionError)

Az előfizetés-átadás jogosultságára vonatkozó hibát jelez. Okot ad arra, hogy miért nem hajtható végre az átváltás.

| Tulajdonság          | Típus               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|--------------------------------------------------------------|
| Code | TransitionErrorCode (TransitionErrorCode) | A problémához társított hibakód. |
| Description | sztring  | A hibát leíró rövid szöveg. |

