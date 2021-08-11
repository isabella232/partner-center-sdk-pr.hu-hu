---
title: Önkiszolgáló szabályzat erőforrásai
description: A partner önkiszolgáló szabályzatokat állít be az ügyfél számára.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ffca78481572e201d3ef9f488e7d594a9c1176249b4415a347b488f4b9b81c51
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996767"
---
# <a name="selfservepolicy-resource"></a>SelfServePolicy erőforrás

A partner önkiszolgáló szabályzatokat állít be az ügyfél számára.

## <a name="selfservepolicy"></a>SelfServePolicy

Egy kosarat ír le.

| Tulajdonság              | Típus             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sztring           | Önkiszolgáló szabályzatazonosító, amely az önkiszolgáló szabályzat sikeres létrehozása után lesz megadva.     |
| SelfServeEntity       | SelfServeEntity  | Az önkiszolgáló entitás, amely hozzáféréssel rendelkezik.                                                     |
| Grantor               | Grantor          | A hozzáférést megadó megadó.                                                                    |
| Engedélyek           | Engedélytömb| [Engedélyerőforrások tömbje.](#permission)                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

Az engedélyeket kapott entitást jelöli.

| Tulajdonság             | Típus|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | sztring                           | A hozzáférést kapott entitás, elfogadott értékek: Ügyfél.                                 |
| TenantID (Bérlőazonosító)             | sztring                           | A hozzáférést kapott entitás bérlőazonosítója.                                   |

## <a name="grantor"></a>Grantor

Az engedélyeket megadó engedélyezőt jelöli.

| Tulajdonság             | Típus|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType (GrantorType)          | sztring                           | A hozzáférést engedélyező, elfogadott értékek: BillToPartner.                               |
| TenantID (Bérlőazonosító)             | sztring                           | A hozzáférést megadó entitás bérlőazonosítója.                                       |


## <a name="permission"></a>Engedély

Egy önkiszolgáló szabályzat engedélyét jelöli.

| Tulajdonság             | Típus|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Erőforrás             | sztring                           | Az erőforrás-hozzáférés is biztosított: AzureReservedInstances.                          |
| Művelet               | sztring                           | A művelet hozzáférése a következő hez: Vásárlás                                           |
