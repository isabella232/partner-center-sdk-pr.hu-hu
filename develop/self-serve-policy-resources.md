---
title: Önkiszolgáló szabályzat erőforrásai
description: A partnerek önkiszolgáló szabályzatokat állít be az ügyfelek számára.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e44581b805e076132984b67280699314e274ca94
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446717"
---
# <a name="selfservepolicy-resource"></a>SelfServePolicy erőforrás

A partnerek önkiszolgáló szabályzatokat állít be az ügyfelek számára.

## <a name="selfservepolicy"></a>SelfServePolicy

Egy kosárra ír le.

| Tulajdonság              | Típus             | Leírás                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sztring           | Önkiszolgáló szabályzatazonosító, amely az önkiszolgáló szabályzat sikeres létrehozásakor lesz megadva.     |
| SelfServeEntity       | SelfServeEntity  | Az önkiszolgáló entitás, amely hozzáférést kap.                                                     |
| Grantor               | Grantor          | A hozzáférést engedélyező megadó.                                                                    |
| Engedélyek           | Engedélytömb| [Engedélyerőforrások tömbje.](#permission)                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

Az engedélyeket kapott entitást jelöli.

| Tulajdonság             | Típus|Leírás|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | sztring                           | A hozzáférést kapott entitás, elfogadott értékek: Ügyfél.                                 |
| TenantID (Bérlőazonosító)             | sztring                           | A hozzáférést kapott entitás bérlőazonosítója.                                   |

## <a name="grantor"></a>Grantor

Az engedélyeket megadó engedélyezőt jelöli.

| Tulajdonság             | Típus|Leírás|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType (GrantorType)          | sztring                           | A hozzáférést engedélyező, elfogadott értékek: BillToPartner.                               |
| TenantID (Bérlőazonosító)             | sztring                           | A hozzáférést megadó entitás bérlőazonosítója.                                       |


## <a name="permission"></a>Engedély

Az önkiszolgáló szabályzatban egy engedélyt képvisel.

| Tulajdonság             | Típus|Leírás|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Erőforrás             | sztring                           | Az erőforrás-hozzáférés is biztosított: AzureReservedInstances.                          |
| Művelet               | sztring                           | A művelethez való hozzáférés a következő hez adható meg: Vásárlás                                           |
