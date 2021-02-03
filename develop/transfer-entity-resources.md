---
title: TransferEntity-erőforrások
description: Egy partner akkor hoz létre átvitelt, ha az ügyfél az előfizetését a partnerrel egy másik partnernek kívánja átvinni.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96c43d255fcd31e6dc4de50baa0e19f5d8855685
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768020"
---
# <a name="transferentity-resources"></a>TransferEntity-erőforrások

**A következőkre vonatkozik:**

- Partnerközpont

Egy partner akkor hoz létre átvitelt, ha az ügyfél az előfizetését a partnerrel egy másik partnernek kívánja átvinni.

## <a name="transferentity"></a>TransferEntity

Leírja a transferEntity.

| Tulajdonság              | Típus             | Leírás                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sztring           | A transferEntity sikeres létrehozásakor megadott transferEntity-azonosító.                               |
| createdTime           | DateTime         | A transferEntity létrehozásának dátuma dátum és idő formátumban. A transferEntity sikeres létrehozása után alkalmazható.      |
| lastModifiedTime      | DateTime         | A transferEntity utolsó frissítésének dátuma, dátum-idő formátumban. A transferEntity sikeres létrehozása után alkalmazható. |
| lastModifiedUser      | sztring           | Az a felhasználó, aki utoljára frissítette a transferEntity. A transferEntity sikeres létrehozásakor lett alkalmazva.                          |
| Customername (          | sztring           | Választható. Annak az ügyfélnek a neve, amelynek előfizetéseit át kell vinni.                                              |
| customerTenantId      | sztring           | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet. A transferEntity sikeres létrehozása után alkalmazható.         |
| partnertenantid       | sztring           | Egy GUID formátumú partner-azonosító, amely azonosítja a partnert.                                                                   |
| sourcePartnerName     | sztring           | Választható. A partner azon szervezetének neve, aki kezdeményezi az átvitelt.                                           |
| sourcePartnerTenantId | sztring           | Egy GUID formátumú partner-azonosító, amely azonosítja az átvitelt kezdeményező partnert.                                           |
| targetPartnerName     | sztring           | Választható. A partner azon szervezetének neve, amelyhez az átvitel irányul.                                         |
| targetPartnerTenantId | sztring           | Egy GUID formátumú partner-azonosító, amely azonosítja azt a partnert, akire az átvitel irányul.                                  |
| Listaelemek             | Objektumok tömbje | [TransferLineItem](#transferlineitem) -erőforrások tömbje.                                                   |
| status                | sztring           | A transferEntity állapota. A lehetséges értékek: "Active" (törölhető/elküldhető) és "befejezett" (már befejeződött). A transferEntity sikeres létrehozása után alkalmazható.|

## <a name="transferlineitem"></a>TransferLineItem

Egy transferEntity található egyik elemnek felel meg.

| Tulajdonság             | Típus                             | Leírás                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| id                   | sztring                           | Egy adatátviteli sorhoz tartozó egyedi azonosító. A transferEntity sikeres létrehozása után alkalmazható.   |
| subscriptionId       | sztring                           | Az előfizetés azonosítója.                                                                            |
| quantity             | int                              | A licencek vagy példányok száma.                                                                    |
| billingCycle         | Objektum                           | Az aktuális időszakban beállított számlázási ciklus típusa.                                                   |
| friendlyName         | sztring                           | Választható. A partner által a egyértelműsítse segítségére meghatározott rövid név.                   |
| partnerIdOnRecord    | sztring                           | A PartnerId on Record (MPNID) azon a vásárláson, amely az átvitel elfogadásakor történik.                 |
| offerId              | sztring                           | Az ajánlat azonosítója.    |
| addonItems           | **TransferLineItem** -objektumok listája | Olyan transferEntity-elemek gyűjteménye, amelyek az átvitt alap előfizetéssel együtt lesznek átadva. A transferEntity sikeres létrehozása után alkalmazható.|
| transferError        | sztring                           | A transferEntity elfogadását követően alkalmazva hiba esetén.                |
| status               | sztring           | A lineitem állapota a transferEntity.|

## <a name="transfersubmitresult"></a>TransferSubmitResult

Egy átvitel eredményét jelöli.

| Tulajdonság          | Típus                                                  | Leírás                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| rendelések            | [Megrendelési](order-resources.md#order) objektumok listája.    | A megrendelések gyűjteménye.          |
| transferErrors    | [TransferError](#transfererror) -objektumok listája.      | Az adatátviteli hibák gyűjteménye. |

## <a name="transfererror"></a>TransferError

Olyan hibát jelöl, amely akkor fordul elő, amikor elfogadják az átvitelt.

| Tulajdonság          | Típus   | Leírás                                     |
|-------------------|--------|-------------------------------------------------|
| transferGroupId   | sztring | A megrendelési csoport azonosítója a hibával. |
| code              | int    | A hibakód.                                 |
| leírás       | sztring | A hiba leírása.                   |
| Listaelemek         | **TransferLineItem** -objektumok listája | Az átviteli hiba részét képező transferEntity-sorok gyűjteménye.|

## <a name="transfererrorcode"></a>TransferErrorCode

Egy [Enum/DotNet/API/System. Enum) olyan értékekkel, amelyek sorrendi hibát jeleznek.

| Érték | Pozíció | Leírás |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | Hiányzó partneri jogkivonat a kérelem környezetében. |
| InvalidInput | 800002 | Érvénytelen kérés-bevitel. |
| ServiceException | 800003 | Váratlan szolgáltatási hiba történt. |
| InvalidOfferId | 800004 | Az ajánlat azonosítója érvénytelen. |
| CreateOrderError | 800005 | A létrehozási sorrend nem sikerült. |
| MpnIdNotFound | 800015 | Az MPN-azonosító nem található. |
| NotValidIndirectResellerMpnId | 800016 | Az MPN-azonosító nem érvényes közvetett viszonteladó. |
| TransferIdNotFound | 900100   | Az átviteli kérelem nem található.   |
| TransferNotAllowedIfStatusIsInProgress | 900101 | Az átviteli kérelem már folyamatban van.|
| TransferNotAllowedIfStatusIsCompleted | 900102 | Az átviteli kérelem már befejeződött.|
| TransferCreateOrderError | 900103 | Az átviteli sorrend nem sikerült.|
| TransferProcessedByAnotherRequest | 900104 | Az átvitelt egy másik kérelem dolgozza fel.|