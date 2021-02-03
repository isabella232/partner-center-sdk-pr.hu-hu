---
title: Önkiszolgáló házirend-erőforrások
description: Egy partner állít be önkiszolgáló házirendeket az ügyfél számára.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04daf6aaeb69153c4139941188f53dbab8979969
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767843"
---
# <a name="selfservepolicy-resource"></a>SelfServePolicy erőforrás

**A következőkre vonatkozik:**

- Partnerközpont

Egy partner állít be önkiszolgáló házirendeket az ügyfél számára.

## <a name="selfservepolicy"></a>SelfServePolicy

Útmutató a kosárhoz.

| Tulajdonság              | Típus             | Leírás                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sztring           | Önkiszolgáló házirend-azonosító, amelyet az önkiszolgáló házirend sikeres létrehozásakor kell megadni.     |
| SelfServeEntity       | SelfServeEntity  | Az önállóan kiszolgált entitás hozzáférést kap.                                                     |
| Megadó fél               | Megadó fél          | A hozzáférést biztosító biztosító.                                                                    |
| Engedélyek           | Engedély tömbje| [Engedélyezési](#permission) erőforrások tömbje.                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

Az engedélyt képviselő entitást jelöli.

| Tulajdonság             | Típus|Leírás|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | sztring                           | Az entitás hozzáférést kap, elfogadott értékek: ügyfél.                                 |
| TenantID             | sztring                           | A hozzáférést engedélyező entitás bérlői azonosítója.                                   |

## <a name="grantor"></a>Megadó fél

Az engedélyeket megadó megadót jelöli.

| Tulajdonság             | Típus|Leírás|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType          | sztring                           | A hozzáférést megadó engedélyező, elfogadott értékek: BillToPartner.                               |
| TenantID             | sztring                           | A hozzáférést biztosító entitás bérlői azonosítója.                                       |


## <a name="permission"></a>Engedély

Az önkiszolgáló házirendben lévő engedélyt jelöli.

| Tulajdonság             | Típus|Leírás|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Erőforrás             | sztring                           | Az erőforrás-hozzáférés is meg van adva: AzureReservedInstances.                          |
| Művelet               | sztring                           | A rendszer a következő műveletekhez biztosít hozzáférést: vásárlás                                           |
