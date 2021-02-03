---
title: Eszköz központi telepítési erőforrásai
description: A partner Center-eszköz telepítésével kapcsolatos erőforrások.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a464cdad3979c305df16a3bdc9133ce70a7ac688
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767731"
---
# <a name="device-deployment-resources"></a>Eszköz központi telepítési erőforrásai

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja

A következő erőforrások az eszköz telepítésével kapcsolatosak.

## <a name="configurationpolicy"></a>ConfigurationPolicy

A **ConfigurationPolicy** információt nyújt a konfigurációs házirendről.

| Tulajdonság             | Típus                                                           | Leírás                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | sztring                                       | Egy GUID-formázott karakterlánc, amely azonosítja a szabályzatot.                                  |
| name                 | sztring                                       | A szabályzat rövid neve.                                                    |
| category             | sztring                                       | A kategória.                                                                        |
| leírás          | sztring                                       | A szabályzat leírása.                                                              |
| devicesAssignedCount | szám                                       | Az ehhez a Szabályzathoz rendelt eszközök száma.                                       |
| policySettings       | sztringek tömbje                             | A házirend-beállítások: "None", "az \_ OEM- \_ előtelepítések eltávolítása", "Oobe- \_ felhasználó \_ nem \_ helyi \_ rendszergazda", "expressz beállítások kihagyása" \_ \_ , "az OEM-regisztráció kihagyása", "kihagyott \_ \_ \_ EULA".    |
| createdDate          | karakterlánc UTC dátum-idő formátumban               | A szabályzat létrehozásának dátuma és időpontja.                                            |
| lastModifiedDate     | karakterlánc UTC dátum-idő formátumban               | A szabályzat legutóbbi módosításának dátuma és időpontja.                                      |
| attribútumok           | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.                                            |

## <a name="device"></a>Eszköz

Az **eszköz** információt nyújt az eszközről.

| Tulajdonság            | Típus                                                           | Leírás                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | sztring                                                         | Egy GUID-formázott karakterlánc, amely az eszközt azonosítja.                      |
| serialNumber        | sztring                                                         | Az eszközhöz egyedileg társított sorozatszám.                   |
| productKey          | sztring                                                         | Az eszközhöz egyedi módon társított termékkulcs.                     |
| hardwareHash        | sztring                                                         | Az eszközhöz egyedileg társított hardver-kivonat.                   |
| modelName           | sztring                                                         | Az eszközhöz társított modell neve.                               |
| oemManufacturerName | sztring                                                         | Az eszközhöz társított OEM-gyártó neve.             |
| policies            | objektumok tömbje                                               | Az eszközhöz hozzárendelt szabályzatok listája.                             |
| uploadedDate        | karakterlánc UTC dátum-idő formátumban                                 | Az eszköz adatainak feltöltésének dátuma és időpontja.                      |
| allowedOperations   | sztringek tömbje                                               | Az eszközön a GET, a PATCH és a DELETE lehetőséggel engedélyezett HTTP-metódusok listája. |
| attribútumok          | [ResourceAttributes](utility-resources.md#resourceattributes)  | A metaadatok attribútumai.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

A **BatchUploadDetails** ismerteti az eszközök batch-feltöltésének állapotát az eszközök listáján található egyes eszközökön.

| Tulajdonság        | Típus     | Leírás                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | sztring   | Egy GUID-formázott karakterlánc, amely a feltöltött eszközök kötegéhez van társítva. |
| status          | sztring   | A Batch-feltöltés állapota: "Unknown", "üzenetsor-kezelés", "feldolgozás", "befejezett", "befejezett \_ with \_ errors". |
| startedTime     | karakterlánc UTC dátum-idő formátumban | A kötegelt feltöltési folyamat elindításának dátuma és időpontja.   |
| completedTime   | karakterlánc UTC dátum-idő formátumban  | A kötegelt feltöltési folyamat befejezésének dátuma és időpontja.   |
| devicesStatus   | [DeviceUploadDetails](#deviceuploaddetails) -erőforrások tömbje | Objektumok tömbje, amely meghatározza az egyes eszközökre vonatkozó adatok feltöltésének állapotát. |
| attribútumok      | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

A **DeviceUploadDetails** leírja az eszközre vonatkozó adatok feltöltésének állapotát.

| Tulajdonság         | Típus                    | Leírás                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | sztring                  | Egy GUID-formázott karakterlánc, amely az eszközhöz van társítva. |
| serialNumber     | sztring                  | Az eszközhöz egyedileg társított sorozatszám. |
| productKey       | sztring                  | Az eszközhöz egyedi módon társított termékkulcs. |
| status           | sztring                  | Az eszköz adatai feltöltésének állapota: "folyamatban", "befejezett", "hibákkal fejeződött be \_ " \_ . |
| errorCode        | sztring                  | A HTTP-állapot hibakódja visszaadott, ha az eszköz feltöltése sikertelen. |
| errorDescription | sztring                  | A HTTP-hiba leírása, ha az eszköz feltöltése sikertelen. |
| attribútumok       | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.   |

## <a name="devicebatch"></a>DeviceBatch

A **DeviceBatch** az eszközök gyűjteményét jelöli.

| Tulajdonság     | Típus                                                           | Leírás                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | sztring                                                         | Egy GUID-formázott karakterlánc, amely az eszközök kötegéhez van társítva. |
| createdBy    | sztring                                                         | Annak a bérlőnek a neve, amely létrehozta a gyűjteményt.                   |
| creationDate | karakterlánc UTC dátum-idő formátumban                                 | A gyűjtemény létrehozásának dátuma és időpontja.                    |
| Eszközök száma  | szám                                                         | A gyűjteményben lévő eszközök száma.                              |
| devicesLink  | [Hivatkozás](utility-resources.md#link)                              | A kötegben található eszközökre mutató hivatkozás.                        |
| attribútumok   | [ResourceAttributes](utility-resources.md#resourceattributes)  | A metaadatok attribútumai.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

A **DeviceBatchCreationRequest** biztosítja az eszköz kötegének létrehozásához és az eszközökhöz való feltöltéséhez szükséges információkat.

| Tulajdonság     | Típus                                                           | Leírás                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| Kötegazonosító      | sztring                                                         | Egy GUID-formázott karakterlánc, amely az eszközök kötegéhez van társítva. |
| eszközök      | [eszköz](#device) objektumainak tömbje                             | Minden objektum egy eszközt határoz meg. Az eszközök azonosítására szolgáló mezők alábbi kombinációit fogadja el: hardwareHash + termék, hardwareHash + serialNumber, hardwareHash + termék + serialNumber, csak hardwareHash, csak termék, serialNumber + oemManufacturerName + modelName. |
| attribútumok   | [ResourceAttributes](utility-resources.md#resourceattributes)  | A metaadatok attribútumai.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

A **DevicePolicyUpdateRequest** biztosítja a szabályzattal rendelkező eszközök listájának frissítéséhez szükséges információkat.

| Tulajdonság     | Típus                                                           | Leírás                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| eszközök      | [eszköz](#device) objektumainak tömbje                             | Minden objektum egy eszközt határoz meg. A következő tulajdonságokkal kell rendelkeznie: azonosító, szabályzatok. |
| attribútumok   | [ResourceAttributes](utility-resources.md#resourceattributes)  | A metaadatok attribútumai.                                              |
