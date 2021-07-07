---
title: Eszköztelepítési erőforrások
description: Az eszközök üzembe Partnerközpont kapcsolódó erőforrások.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c85f0bd6a633ac18aa8e56e5a89bfc5c8f0398cc
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906502"
---
# <a name="device-deployment-resources"></a>Eszköztelepítési erőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz

A következő erőforrások kapcsolódnak az eszközök üzembe helyezéséhez.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**A ConfigurationPolicy** a konfigurációs szabályzatokkal kapcsolatos információkat biztosít.

| Tulajdonság             | Típus                                                           | Leírás                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | sztring                                       | Egy GUID-formátumú sztring, amely azonosítja a szabályzatot.                                  |
| name                 | sztring                                       | A szabályzat rövid neve.                                                    |
| category             | sztring                                       | A kategória.                                                                        |
| leírás          | sztring                                       | A szabályzat leírása.                                                              |
| devicesAssignedCount | szám                                       | A szabályzathoz rendelt eszközök száma.                                       |
| policySettings       | sztringek tömbje                             | A szabályzat beállításai: "none","remove \_ oem \_ preinstalls","oobe \_ user not local \_ \_ \_ admin","skip \_ express \_ settings","skip \_ oem \_ registration", "skip \_ eula".    |
| createdDate (Létrehozásidátum)          | sztring UTC dátum-idő formátumban               | A szabályzat létrehozási dátuma és időpontja.                                            |
| lastModifiedDate (lastModifiedDate)     | sztring UTC dátum-idő formátumban               | A szabályzat utolsó módosításának dátuma és időpontja.                                      |
| Attribútumok           | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                            |

## <a name="device"></a>Eszköz

**Az** eszköz információkat biztosít az eszközről.

| Tulajdonság            | Típus                                                           | Leírás                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | sztring                                                         | Egy GUID-formátumú sztring, amely azonosítja az eszközt.                      |
| serialNumber        | sztring                                                         | Az eszközhöz egyedileg társított sorozatszám.                   |
| Productkey          | sztring                                                         | Az eszközhöz egyedileg társított termékkulcs.                     |
| hardwareHash        | sztring                                                         | Az eszközhöz egyedileg társított hardver-kivonat.                   |
| Modelname           | sztring                                                         | Az eszközhöz társított modellnév.                               |
| oemManufacturerName | sztring                                                         | Az eszközhöz társított OEM-gyártó neve.             |
| policies            | objektumok tömbje                                               | Az eszközhöz rendelt szabályzatok listája.                             |
| uploadedDate (feltöltöttdátum)        | sztring UTC dátum-idő formátumban                                 | Az eszközadatok feltöltésének dátuma és időpontja.                      |
| allowedOperations (engedélyezett működés)   | sztringek tömbje                                               | Az eszközszinkronizáláshoz engedélyezett HTTP-metódusok listája GET, PATCH, DELETE ként. |
| Attribútumok          | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**A BatchUploadDetails** az eszközök listájában az egyes eszközökre vonatkozó adatok kötegelt feltöltésének állapotát ismerteti.

| Tulajdonság        | Típus     | Leírás                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | sztring   | Egy GUID formátumú sztring, amely a feltöltött eszközök kötegéhez van társítva. |
| status          | sztring   | A kötegelt feltöltés állapota: "unknown","queued","processing","finished","finished \_ with \_ errors". |
| startedTime (elindított idő)     | sztring UTC dátum-idő formátumban | A kötegelt feltöltési folyamat elindulási dátuma és időpontja.   |
| completedTime (kész idő)   | sztring UTC dátum-idő formátumban  | A kötegelt feltöltési folyamat befejezésének dátuma és időpontja.   |
| devicesStatus   | [DeviceUploadDetails erőforrások tömbje](#deviceuploaddetails) | Objektumok tömbje, amely meghatározza az egyes eszközinformációk feltöltésének állapotát. |
| Attribútumok      | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**A DeviceUploadDetails** az eszközzel kapcsolatos információk feltöltésének állapotát írja le.

| Tulajdonság         | Típus                    | Leírás                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | sztring                  | Az eszközhöz társított GUID formátumú sztring. |
| serialNumber     | sztring                  | Az eszközhöz egyedileg társított sorozatszám. |
| Productkey       | sztring                  | Az eszközhöz egyedileg társított termékkulcs. |
| status           | sztring                  | Az eszközinformációk feltöltésének állapota: "folyamatban", "kész", \_ "hibákkal \_ fejeződött be". |
| errorCode        | sztring                  | Ha az eszköz feltöltése sikertelen, a rendszer HTTP-állapot hibakódot ad vissza. |
| errorDescription (hibaleíró) | sztring                  | A HTTP-hiba leírása, ha az eszköz feltöltése sikertelen. |
| Attribútumok       | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.   |

## <a name="devicebatch"></a>DeviceBatch

**A DeviceBatch** eszközök gyűjteményét jelöli.

| Tulajdonság     | Típus                                                           | Leírás                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | sztring                                                         | Egy GUID formátumú sztring, amely az eszközök kötegéhez van társítva. |
| createdBy    | sztring                                                         | A gyűjteményt létrehozó bérlő neve.                   |
| creationDate (Létrehozás dátuma) | sztring UTC dátum-idő formátumban                                 | A gyűjtemény létrehozási ideje és adatai.                    |
| deviceCount (eszköz száma)  | szám                                                         | A gyűjteményben az eszközök száma.                              |
| devicesLink (eszközök hivatkozása)  | [Link](utility-resources.md#link)                              | A kötegben található eszközökre mutató hivatkozás.                        |
| Attribútumok   | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**A DeviceBatchCreationRequest** az eszközkötet létrehozásához szükséges információkat biztosítja, és feltölti az eszközökkel.

| Tulajdonság     | Típus                                                           | Leírás                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId (kötegazonosító)      | sztring                                                         | Egy GUID formátumú sztring, amely az eszközök kötegéhez van társítva. |
| eszközök      | [Eszközobjektumok tömbje](#device)                             | Minden objektum megad egy eszközt. Az eszköz azonosításához a következő mezőkombinációk lesznek elfogadva: hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, hardwareHash only, productKey only, serialNumber + oemManufacturerName + modelName. |
| Attribútumok   | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**A DevicePolicyUpdateRequest** az eszközök listájának szabályzatokkal való frissítéséhez szükséges információkat tartalmazza.

| Tulajdonság     | Típus                                                           | Leírás                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| eszközök      | [Eszközobjektumok tömbje](#device)                             | Minden objektum megad egy eszközt. A következő tulajdonságok szükségesek: Azonosító, Szabályzatok. |
| Attribútumok   | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok.                                              |
