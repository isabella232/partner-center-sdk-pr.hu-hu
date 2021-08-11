---
title: Eszköztelepítési erőforrások
description: Az eszközök üzembe Partnerközpont kapcsolódó erőforrások.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e8e2429fea88a89873955d9af9253492934e40e5be1a1b7600446485d13f5bd7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994846"
---
# <a name="device-deployment-resources"></a>Eszköztelepítési erőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz

A következő erőforrások kapcsolódnak az eszközök üzembe helyezéséhez.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**A ConfigurationPolicy** a konfigurációs szabályzatokkal kapcsolatos információkat biztosít.

| Tulajdonság             | Típus                                                           | Description                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | sztring                                       | Egy GUID-formátumú sztring, amely azonosítja a szabályzatot.                                  |
| name                 | sztring                                       | A szabályzat rövid neve.                                                    |
| category             | sztring                                       | A kategória.                                                                        |
| leírás          | sztring                                       | A szabályzat leírása.                                                              |
| devicesAssignedCount | szám                                       | A szabályzathoz rendelt eszközök száma.                                       |
| policySettings       | sztringek tömbje                             | A szabályzat beállításai: "none","remove \_ oem \_ preinstalls","oobe \_ user not local \_ \_ \_ admin","skip \_ express \_ settings","skip \_ oem \_ registration", "skip \_ eula".    |
| createdDate (Létrehozásidátum)          | sztring UTC dátum-idő formátumban               | A szabályzat létrehozási dátuma és időpontja.                                            |
| lastModifiedDate (utolsó módosítvaddátum)     | sztring UTC dátum-idő formátumban               | A szabályzat utolsó módosításának dátuma és időpontja.                                      |
| Attribútumok           | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                            |

## <a name="device"></a>Eszköz

**Az** eszköz információkat biztosít az eszközről.

| Tulajdonság            | Típus                                                           | Description                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | sztring                                                         | Egy GUID-formátumú sztring, amely azonosítja az eszközt.                      |
| serialNumber        | sztring                                                         | Az eszközhöz egyedileg társított sorozatszám.                   |
| Productkey          | sztring                                                         | Az eszközhöz egyedileg társított termékkulcs.                     |
| hardwareHash (hardverhash)        | sztring                                                         | Az eszközhöz egyedileg társított hardver-kivonat.                   |
| Modelname           | sztring                                                         | Az eszközhöz társított modellnév.                               |
| oemManufacturerName | sztring                                                         | Az eszközhöz társított OEM-gyártó neve.             |
| policies            | objektumok tömbje                                               | Az eszközhöz rendelt szabályzatok listája.                             |
| uploadedDate (feltöltésidátum)        | sztring UTC dátum-idő formátumban                                 | Az eszközadatok feltöltésének dátuma és időpontja.                      |
| allowedOperations (engedélyezett művelet)   | sztringek tömbje                                               | Az eszközszinkronizáláshoz engedélyezett HTTP-metódusok listája GET, PATCH, DELETE és ként. |
| Attribútumok          | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**A BatchUploadDetails** az eszközök listájában az egyes eszközökre vonatkozó adatok kötegelt feltöltésének állapotát ismerteti.

| Tulajdonság        | Típus     | Description                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | sztring   | Egy GUID formátumú sztring, amely a feltöltött eszközök kötegéhez van társítva. |
| status          | sztring   | A kötegelt feltöltés állapota: "unknown", "queued","processing","finished","finished \_ with \_ errors". |
| startedTime (elindított idő)     | sztring UTC dátum-idő formátumban | A kötegelt feltöltési folyamat elindulási dátuma és időpontja.   |
| completedTime (befejeződött idő)   | sztring UTC dátum-idő formátumban  | A kötegelt feltöltési folyamat befejezésének dátuma és időpontja.   |
| devicesStatus   | [DeviceUploadDetails erőforrások tömbje](#deviceuploaddetails) | Az egyes eszközinformációk feltöltési állapotának megadására használható objektumok tömbje. |
| Attribútumok      | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**A DeviceUploadDetails** az eszközzel kapcsolatos információk feltöltésének állapotát ismerteti.

| Tulajdonság         | Típus                    | Description                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | sztring                  | Egy GUID-formátumú sztring, amely az eszközhöz van társítva. |
| serialNumber     | sztring                  | Az eszközhöz egyedileg társított sorozatszám. |
| Productkey       | sztring                  | Az eszközhöz egyedileg társított termékkulcs. |
| status           | sztring                  | Az eszközinformációk feltöltésének állapota: "folyamatban", "finished", "finished \_ with \_ errors". |
| errorCode        | sztring                  | Ha az eszköz feltöltése sikertelen, a rendszer HTTP-állapot hibakódot ad vissza. |
| errorDescription (hibaleíró) | sztring                  | A HTTP-hiba leírása, ha az eszköz feltöltése sikertelen. |
| Attribútumok       | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.   |

## <a name="devicebatch"></a>DeviceBatch (Eszközbatch)

**A DeviceBatch** az eszközök gyűjteményét jelöli.

| Tulajdonság     | Típus                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | sztring                                                         | Egy GUID-formátumú sztring, amely az eszközök kötegéhez van társítva. |
| createdBy    | sztring                                                         | A gyűjteményt létrehozó bérlő neve.                   |
| creationDate (Létrehozás dátuma) | sztring UTC dátum-idő formátumban                                 | A gyűjtemény létrehozási ideje és adatai.                    |
| deviceCount  | szám                                                         | A gyűjteményben az eszközök száma.                              |
| devicesLink (eszközök hivatkozása)  | [Link](utility-resources.md#link)                              | A kötegben található eszközökre mutató hivatkozás.                        |
| Attribútumok   | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**A DeviceBatchCreationRequest** az eszközkötet létrehozásához szükséges információkat biztosítja, és feltölti az eszközökkel.

| Tulajdonság     | Típus                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId (kötegazonosító)      | sztring                                                         | Egy GUID-formátumú sztring, amely az eszközök kötegéhez van társítva. |
| eszközök      | [Eszközobjektumok tömbje](#device)                             | Minden objektum megad egy eszközt. Az eszköz azonosításához a következő mezőkombinációk lesznek elfogadva: hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, hardwareHash only, productKey only, serialNumber + oemManufacturerName + modelName. |
| Attribútumok   | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**A DevicePolicyUpdateRequest** az eszközök listájának szabályzatokkal való frissítéséhez szükséges információkat tartalmazza.

| Tulajdonság     | Típus                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| eszközök      | [Eszközobjektumok tömbje](#device)                             | Minden objektum megad egy eszközt. A következő tulajdonságok szükségesek: Azonosító, Szabályzatok. |
| Attribútumok   | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok.                                              |
