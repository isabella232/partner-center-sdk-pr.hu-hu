---
title: Jogosultsági erőforrások
description: A jogosultsággal kapcsolatos erőforrásokat ismerteti.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 428ac6f8b4d67894092119a6246279045a04dac0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768075"
---
# <a name="entitlement-resources"></a>Jogosultsági erőforrások

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

## <a name="entitlement"></a>Jogosultság

Ez az erőforrás azokat a termékeket jelöli, amelyekre az ügyfélnek a katalógusban lévő elemekhez való partneri vásárlás miatt jogot kell használnia.

| Tulajdonság | Típus | Leírás |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | A jogosultságot eredményező rendelési hivatkozás. |
| productId | sztring | A termék azonosítója. |
| skuID | sztring | Az SKU azonosítója. |
| quantity | int | A jogosultságok mennyisége (kizárja a nem teljesített/átvitt jogosultságokat). |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | A jogosultsági mennyiség részleteinek listája (az elemek száma és az egyes mennyiségek állapota). |
| entitlementType | sztring | A jogosultság típusa. (Frissítve a karakterláncra a [EntitlementType](#entitlementtype) -ben az SDK 1,8-ben.) |
| entitledArtifacts | IEnumerable<[összetevő](#artifact)> | A jogosultsághoz társított összetevők listája. |
| IncludedEntitlements | IEnumerable<[jogosultság](#artifact)> | A jogosultságok listája, amelyek implicit módon szerepelnek a katalógusból származó Termékkód/SkuId vásárlásának eredményeképpen. |
| ExpiryDate | karakterlánc UTC dátum-idő formátumban  | A jogosultság lejárati dátuma (ha van ilyen). |

## <a name="referenceorder"></a>ReferenceOrder

Jogosultság megrendelési hivatkozása.

| Tulajdonság | Típus | Leírás |
|----------|------|-------------|
| id | sztring | A hivatkozott sorrend azonosítója. |
| lineItemId | sztring | A hivatkozott megrendelési sor elemeinek azonosítója |
| alternateId | sztring | A hivatkozott rendeléssor-tétel alternatív azonosítója |

## <a name="quantitydetail"></a>QuantityDetail

A jogosultsági mennyiség részleteit jelöli.

| Tulajdonság | Típus | Leírás |
|----------|------|-------------|
| quantity | int | Az elemek száma. |
| status | sztring | A mennyiség állapota. |

## <a name="entitlementtype"></a>EntitlementType

> [!IMPORTANT]
> Az SDK v 1.9-es verziójában elavult

Egy olyan [enumerálás](/dotnet/api/system.enum) , amelynek értékei a jogosultság típusát jelölik.

| Érték | Leírás |
|-------|-------------|
| Szoftverek | A szoftverhez kapcsolódó jogosultsági típust jelöli. |
| VirtualMachineReservedInstance | Azure Reserved Virtual Machine Instanceshoz kapcsolódó jogosultsági típust jelöl. |

## <a name="artifact"></a>Összetevő

A jogosultsághoz társított összetevő.

| Tulajdonság | Típus | Leírás |
|----------|------|-------------|
| artifactType | sztring | Az összetevő típusa. (Frissítve a [ArtifactType](#artifacttype) -ből származó karakterláncra az SDK-ban 1.8-as verzióban) |
| dynamicAttributes | Szótár &lt; karakterlánca, objektum&gt; | Artifacttype-specifikus értékeket tartalmazó dinamikus attribútumok. Ha például a artifactType = "reservedinstance", ez a tulajdonság a "reservationType" = "virtualmachines" vagy "reservationType" = "sqldatabases" karaktert fogja tartalmazni, amely a virtuális gép fenntartott példányát vagy az Azure SQL fenntartott példányt jelöli. (Az SDK 2.0-s verziójában érhető el) |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> Az SDK v 1.9-es verziójában elavult

Olyan [enumerálás](/dotnet/api/system.enum) , amelynek értékei a jogosultsági összetevők típusát jelölik.

| Érték                          | Leírás                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Azt jelzi, hogy a Azure Reserved Virtual Machine Instances lekérésével milyen összetevő-támogatás van. |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Az Azure-beli fenntartott példány jogosultságával társított összetevő. Ez örökli az [összetevő osztályát](#artifact) .

| Tulajdonság   | Típus                           | Leírás                                        |
|------------|--------------------------------|----------------------------------------------------|
| hivatkozás       | [Hivatkozás](./utility-resources.md#link) | A hivatkozás, amely az összes kapcsolódó összetevő részleteit beolvassa.   |
| resourceID | sztring                         | Az Azure-beli foglalási rendelés vagy erőforrás azonosítója. |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Az Azure Reserved instance összetevő-hivatkozás hívásakor visszaadott entitást jelöli.

|   Tulajdonság   |           Típus           |                          Leírás                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     típus     |          sztring          |                     Az összetevő típusa.                     |
| foglalások | IEnumerable<Reservation> | Az Azure-erőforrás vagy a foglalási sorrend azonosítóját jelzi. |

## <a name="reservation"></a>Foglalás

Egyéni foglalást jelöl.

| Tulajdonság          | Típus                           | Leírás                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | sztring                         | A foglalás azonosítója.                                         |
| scopeType         | sztring                         | A virtuális gép foglalásához társított hatókör típusa. |
| displayName       | sztring                         | A foglalás megjelenítendő neve.                               |
| appliedScopes     | IEnumerable                    | A foglaláshoz tartozó alkalmazott hatókörök listája. (Csak akkor érhető el, ha a scopeType nincs megosztva.) |
| quantity          | int                            | A foglalásban lévő virtuális gépek száma.                 |
| expiryDateTime    | karakterlánc UTC dátum-idő formátumban | A foglalás lejárati dátuma.                                |
| effectiveDateTime | karakterlánc UTC dátum-idő formátumban | A foglalás érvényességi dátuma.                             |
| provisioningState | sztring                         | A foglalás kiépítési állapota.                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> Az SDK v 1.9-es verziójában elavult

Az Azure-beli fenntartott virtuálisgép-példányra vonatkozó jogosultsághoz tartozó összetevő. Ez örökli az [összetevő osztályát](#artifact) .

| Tulajdonság   | Típus                              | Leírás                                        |
|------------|-----------------------------------|----------------------------------------------------|
| hivatkozás       | [Hivatkozás](utility-resources.md#link) | A hivatkozás, amely az összes kapcsolódó összetevő részleteit beolvassa.   |
| resourceID | sztring                            | Az Azure-beli foglalási rendelés vagy erőforrás azonosítója. |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> Az SDK v 1.9-es verziójában elavult

Az Azure-beli fenntartott virtuálisgép-példányok hivatkozásának hívásakor visszaadott entitást jelöli.

| Tulajdonság                    | Típus                                                                 | Leírás           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| típus                        | [ArtifactType](#artifacttype)                                        | Az összetevő típusa. |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Az Azure-erőforrás vagy a foglalási sorrend azonosítóját jelzi. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> Az SDK v 1.9-es verziójában elavult

A virtuális gépek egyéni foglalását jelöli.

|     Tulajdonság      |              Típus              |                                                Leírás                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             sztring             |                                         A foglalás azonosítója.                                         |
|     scopeType     |             sztring             |                     A virtuális gép foglalásához társított hatókör típusa.                     |
|    displayName    |             sztring             |                                    A foglalás megjelenítendő neve.                                    |
|   appliedScopes   |      IEnumerable<string>       | A foglaláshoz tartozó alkalmazott hatókörök listája. (Csak akkor érhető el, ha a scopeType nincs megosztva.) |
|     quantity      |              int               |                             A foglalásban lévő virtuális gépek száma.                             |
|  expiryDateTime   | karakterlánc UTC dátum-idő formátumban |                                    A foglalás lejárati dátuma.                                     |
| effectiveDateTime | karakterlánc UTC dátum-idő formátumban |                                   A foglalás érvényességi dátuma.                                   |
| provisioningState |             sztring             |                                 A foglalás kiépítési állapota.                                 |
