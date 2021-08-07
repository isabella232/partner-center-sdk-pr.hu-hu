---
title: Jogosultsági erőforrások
description: A jogosultságokkal kapcsolatos erőforrásokat ismerteti.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9582bb0d886078062ae14d0461accb8e0179bed2e33e9a264cc1da8b06383706
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989151"
---
# <a name="entitlement-resources"></a>Jogosultsági erőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

## <a name="entitlement"></a>Jogosultság

Ez az erőforrás azokat a termékeket jelöli, amelyekhez az ügyfélnek jogában áll használni a katalógus elemeinek partnervásárlása miatt.

| Tulajdonság | Típus | Description |
|----------|------|-------------|
| referenceOrder (hivatkozás rendelése) | [ReferenceOrder (Referenciarendelés)](#referenceorder) | A jogosultságot eredményező rendeléshivatkozás. |
| productId | sztring | A termék azonosítója. |
| skuID | sztring | A termékváltozat azonosítója. |
| quantity | int | A jogosultságok mennyisége (nem tartalmazza a Nem teljesült/Át nem adott jogosultságokat). |
| quantityDetails (részletek mennyisége) | IEnumerable<[QuantityDetail](#quantitydetail)> | A jogosultságok mennyiségének részletei (az elemek száma és az egyes mennyiségek állapota). |
| entitlementType (jogosultságtípus) | sztring | A jogosultság típusa. (Az SDK 1.8-ban az [EntitlementType](#entitlementtype) sztringre frissült.) |
| entitledArtifacts | IEnumerable<[Artifact](#artifact)> | A jogosultsághoz társított összetevők listája. |
| IncludedEntitlements (Benne foglalt) | IEnumerable<[Entitlement](#artifact)> | A jogosultságok listája, amelyek implicit módon szerepelnek a katalógusban vásárolt Termékazonosító /Termékazonosító alapján. |
| ExpiryDate (Lejárat dátuma) | sztring UTC dátum-idő formátumban  | A jogosultság lejárati dátuma (ha van). |

## <a name="referenceorder"></a>ReferenceOrder (Referenciarendelés)

Jogosultság rendelési hivatkozása.

| Tulajdonság | Típus | Description |
|----------|------|-------------|
| id | sztring | A hivatkozott rendelés azonosítója. |
| lineItemId (sortemazonosító) | sztring | A hivatkozott rendelési sorelem azonosítója. |
| alternateId (alternatívazonosító) | sztring | A hivatkozott rendelési sorelem alternatív azonosítója. |

## <a name="quantitydetail"></a>QuantityDetail (Mennyiségrészlet)

Egy jogosultsági mennyiség részleteit jelöli.

| Tulajdonság | Típus | Description |
|----------|------|-------------|
| quantity | int | Az elemek száma. |
| status | sztring | A mennyiség állapota. |

## <a name="entitlementtype"></a>EntitlementType (Jogosultságtípus)

> [!IMPORTANT]
> Az SDK 1.9-es verziójában elavult

Enum [a](/dotnet/api/system.enum) jogosultság típusát jelző értékekkel.

| Érték | Leírás |
|-------|-------------|
| Szoftverek | A szoftverhez kapcsolódó jogosultságtípust jelzi. |
| VirtualMachineReservedInstance | A következővel kapcsolatos jogosultságtípust Azure Reserved Virtual Machine Instances. |

## <a name="artifact"></a>Összetevő

A jogosultsághoz társított összetevő.

| Tulajdonság | Típus | Description |
|----------|------|-------------|
| artifactType (összetevőtípus) | sztring | Az összetevő típusa. (Frissítve az [ArtifactType sztringre](#artifacttype) az SDK 1.8-as verziójában) |
| dynamicAttributes (dinamikus attribútumok) | &lt;Szótárszavak, objektum&gt; | Összetevőtípus-specifikus értékeket tartalmazó dinamikus attribútumok. Ha például artifactType = "reservedinstance", ez a tulajdonság tartalmazza a "reservationType" = "virtualmachines" vagy a "reservationType" = "sqldatabases" értékeket, amelyek a fenntartott virtuális gép vagy az Azure SQL fenntartott példány jelölését tartalmazzák. (Az SDK 1.9-es verziójától kezdődően érhető el) |

## <a name="artifacttype"></a>ArtifactType (Összetevő típusa)

> [!IMPORTANT]
> Az SDK 1.9-es verziójában elavult

Egy [Enum,](/dotnet/api/system.enum) amely a jogosultság-összetevő típusát jelző értékeket tartalmaz.

| Érték                          | Leírás                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Azt jelzi, hogy az összetevő segíti a Azure Reserved Virtual Machine Instances. |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Az Azure-beli fenntartott példány jogosultságával társított összetevő. Az Artifact osztályból [örököl.](#artifact)

| Tulajdonság   | Típus                           | Description                                        |
|------------|--------------------------------|----------------------------------------------------|
| hivatkozás       | [Link](./utility-resources.md#link) | Az összes társított összetevő részleteinek lekért hivatkozása.   |
| resourceID (erőforrás-azonosító) | sztring                         | Az Azure-foglalási rendelés vagy erőforrás azonosítója. |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Az Azure Reserved Instance összetevő hivatkozásának meghívásakor visszaadott entitást jelöli.

|   Tulajdonság   |           Típus           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     típus     |          sztring          |                     Az összetevő típusa.                     |
| Foglalás | `IEnumerable<Reservation>` | Az Azure-erőforrás vagy foglalásrendelés azonosítóját jelzi. |

## <a name="reservation"></a>Foglalás

Egy egyéni foglalást képvisel.

| Tulajdonság          | Típus                           | Description                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | sztring                         | A foglalás azonosítója.                                         |
| scopeType (hatókörtípus)         | sztring                         | A virtuálisgép-foglaláshoz társított hatókörtípus. |
| displayName       | sztring                         | A foglalás megjelenített neve.                               |
| appliedScopes (hatókörök alkalmazása)     | IEnumerable (Számbavehető)                    | A foglaláshoz társított alkalmazott hatókörök listája. (Csak akkor érhető el, ha a scopeType nincs megosztva.) |
| quantity          | int                            | A foglalásban lévő virtuális gépek száma.                 |
| expiryDateTime (lejárat dátuma és ideje)    | sztring UTC dátum-idő formátumban | A foglalás lejárati dátuma.                                |
| effectiveDateTime | sztring UTC dátum-idő formátumban | A foglalás hatálybalott dátuma.                             |
| provisioningState | sztring                         | A foglalás kiépítési állapota.                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> Az SDK 1.9-es verziójában elavult

Az Azure-beli fenntartott virtuálisgép-példány jogosultságával társított összetevő. Az Artifact osztályból [örököl.](#artifact)

| Tulajdonság   | Típus                              | Description                                        |
|------------|-----------------------------------|----------------------------------------------------|
| hivatkozás       | [Link](utility-resources.md#link) | Az összes társított összetevő részleteinek lekért hivatkozása.   |
| resourceID (erőforrás-azonosító) | sztring                            | Az Azure-foglalási rendelés vagy erőforrás azonosítója. |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> Az SDK 1.9-es verziójában elavult

Az Azure Reserved Virtual Machine Instance összetevő hivatkozásának meghívásakor visszaadott entitást jelöli.

| Tulajdonság                    | Típus                                                                 | Description           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| típus                        | [ArtifactType (Összetevő típusa)](#artifacttype)                                        | Az összetevő típusa. |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Az Azure-erőforrás vagy foglalásrendelés azonosítóját jelzi. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> Az SDK 1.9-es verziójában elavult

Egy egyéni virtuálisgép-foglalást képvisel.

|     Tulajdonság      |              Típus              |                                                Description                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             sztring             |                                         A foglalás azonosítója.                                         |
|     scopeType (hatókörtípus)     |             sztring             |                     A virtuálisgép-foglaláshoz társított hatókörtípus.                     |
|    displayName    |             sztring             |                                    A foglalás megjelenített neve.                                    |
|   appliedScopes (hatókörök alkalmazása)   |      `IEnumerable<string>`       | A foglaláshoz társított alkalmazott hatókörök listája. (Csak akkor érhető el, ha a scopeType nincs megosztva.) |
|     quantity      |              int               |                             A foglalásban lévő virtuális gépek száma.                             |
|  expiryDateTime (lejárat dátuma és ideje)   | sztring UTC dátum-idő formátumban |                                    A foglalás lejárati dátuma.                                     |
| effectiveDateTime | sztring UTC dátum-idő formátumban |                                   A foglalás hatálybalott dátuma.                                   |
| provisioningState |             sztring             |                                 A foglalás kiépítési állapota.                                 |
