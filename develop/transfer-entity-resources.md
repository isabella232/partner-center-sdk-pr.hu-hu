---
title: TransferEntity-erőforrások
description: A partner akkor hoz létre átadást, ha az ügyfél azt szeretné, hogy a partnerrel való előfizetése egy másik partnerre legyen átadva.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3103c0e9f8e6850336d663a5a38274ce7391e30edd433d08f44071de31b5fc5e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990205"
---
# <a name="transferentity-resources"></a>TransferEntity-erőforrások

A partner akkor hoz létre átadást, ha az ügyfél azt szeretné, hogy a partnerrel való előfizetése egy másik partnerre legyen átadva.

## <a name="transferentity"></a>TransferEntity (Átviteli átvitel)

Egy transferEntity átvitelt ír le.

| Tulajdonság              | Típus             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sztring           | A transferEntity sikeres létrehozásakor megadott transferEntity azonosító.                               |
| createdTime (létrehozás ideje)           | DateTime         | A transferEntity létrejöttének dátuma dátum-idő formátumban. Alkalmazva a transferEntity sikeres létrehozásakor.      |
| lastModifiedTime      | DateTime         | A transferEntity utolsó frissítésének dátuma dátum-idő formátumban. Alkalmazva a transferEntity sikeres létrehozásakor. |
| lastModifiedUser      | sztring           | Az a felhasználó, aki utoljára frissítette a transferEntity adatokat. Alkalmazva a transferEntity sikeres létrehozásakor.                          |
| customerName (ügyfél neve)          | sztring           | Választható. Annak az ügyfélnek a neve, akinek az előfizetései átadása folyamatban van.                                              |
| customerTenantId (customerTenantId)      | sztring           | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet. Alkalmazva a transferEntity sikeres létrehozásakor.         |
| partnertenantid       | sztring           | Egy GUID formátumú partnerazonosító, amely azonosítja a partnert.                                                                   |
| sourcePartnerName (forráspartner neve)     | sztring           | Választható. Az átadást kezdeményező partnerszervezet neve.                                           |
| sourcePartnerTenantId (forráspartner-partnerazonosító) | sztring           | Egy GUID formátumú partnerazonosító, amely azonosítja az átadást kezdeményező partnert.                                           |
| targetPartnerName     | sztring           | Választható. Annak a partnernek a neve, amely számára az átvitelt megcélozni kell.                                         |
| targetPartnerTenantId | sztring           | Egy GUID formátumú partnerazonosító, amely azonosítja azt a partnert, akinek az átadást megcéloznia kell.                                  |
| lineItems (sorsorok)             | Objektumok tömbje | [TransferLineItem-erőforrások tömbje.](#transferlineitem)                                                   |
| status                | sztring           | A transferEntity állapota. Lehetséges értékek: "Aktív" (törölhető/elküldve) és "Befejezve" (már befejeződött). Alkalmazva a transferEntity sikeres létrehozásakor.|

## <a name="transferlineitem"></a>TransferLineItem (Átviteli vonal)

Egy transferEntity elem egy elemét jelöli.

| Tulajdonság             | Típus                             | Description                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| id                   | sztring                           | Egy átvitelisor-elem egyedi azonosítója. Alkalmazva a transferEntity sikeres létrehozásakor.   |
| subscriptionId       | sztring                           | Az előfizetés azonosítója.                                                                            |
| quantity             | int                              | A licencek vagy példányok száma.                                                                    |
| billingCycle (számlázási ciklus)         | Objektum                           | Az aktuális időszakra beállított számlázási ciklus típusa.                                                   |
| friendlyName (rövid név)         | sztring                           | Választható. A partner által meghatározott elem rövid neve a egyértelműsséghez.                   |
| partnerIdOnRecord    | sztring                           | PartnerAzonosító a rekordban (MPNID) a vásárláskor, amely akkor történik, amikor a rendszer elfogadja az átadást.                 |
| offerId (ajánlatazonosító)              | sztring                           | Az ajánlat azonosítója.    |
| addonItems (bővítmények)           | **TransferLineItem objektumok** listája | A bővítmények transferEntity sorelemek gyűjteménye, amelyek át lesznek adva az átvitt alapelő előfizetéssel együtt. Alkalmazva a transferEntity sikeres létrehozásakor.|
| transferError (transferError)        | sztring                           | A transferEntity után lesz alkalmazva hiba esetén.                |
| status               | sztring           | A sortem állapota a transferEntity oszlopban.|

## <a name="transfersubmitresult"></a>TransferSubmitResult

Az átadás elfogadásának eredményét jelöli.

| Tulajdonság          | Típus                                                  | Description                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| rendelések            | Az Order [objektumok](order-resources.md#order) listája.    | A rendelések gyűjteménye.          |
| transferErrors (továbbítók)    | [TransferError-objektumok](#transfererror) listája.      | Átviteli hibák gyűjteménye. |

## <a name="transfererror"></a>TransferError (Továbbító)

Egy olyan hibát jelez, amely akkor fordul elő, ha az átvitel elfogadott.

| Tulajdonság          | Típus   | Description                                     |
|-------------------|--------|-------------------------------------------------|
| transferGroupId (átvitelicsoport-azonosító)   | sztring | A rendelési csoport azonosítója a hibával együtt. |
| code              | int    | A hibakód.                                 |
| leírás       | sztring | A hiba leírása.                   |
| lineItems (sorsorok)         | **TransferLineItem-objektumok** listája | TransferEntity sorelemek gyűjteménye, amelyek az átviteli hiba részét képezi.|

## <a name="transfererrorcode"></a>TransferErrorCode

Egy [Enum/dotnet/api/system.enum) értékekkel, amelyek a megrendelési hiba típusát jelzik.

| Érték | Pozíció | Description |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | A partneri jogkivonat hiányzik a kérelem kontextusában. |
| InvalidInput (Érvénytelen átviteli sebesség) | 800002 | Érvénytelen kérelembemenet. |
| ServiceException (ServiceException) | 800003 | Váratlan szolgáltatáshiba. |
| InvalidOfferId (ÉrvénytelenofferId) | 800004 | Érvénytelen ajánlatazonosító. |
| CreateOrderError (Rendelésererror létrehozása) | 800005 | A rendelés létrehozása nem sikerült. |
| MpnIdNotFound | 800015 | Az MPN-azonosító nem található. |
| NotValidIndirectResellerMpnId | 800016 | Az MPN-azonosító nem érvényes közvetett viszonteladó. |
| TransferIdNotFound | 900100   | Az átadási kérelem nem található.   |
| TransferNotAllowedIfStatusIsInProgress | 900101 | Az átadási kérelem már folyamatban van.|
| TransferNotAllowedIfStatusIsCompleted | 900102 | Az átadási kérelem már befejeződött.|
| TransferCreateOrderError | 900103 | Az átadási rendelés nem sikerült.|
| TransferProcessedByAnotherRequest | 900104 | Az átvitelt egy másik kérés feldolgozja.|