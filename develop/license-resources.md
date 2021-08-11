---
title: Licencerőforrások
description: A licencekkel kapcsolatos erőforrásokat ismerteti.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e6d91110dcec8a873e77cb02bdb77f6335e27989201ea68eebf904c5159964c5
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996580"
---
# <a name="license-resources"></a>Licencerőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A licencekkel kapcsolatos erőforrásokat ismerteti.

## <a name="license"></a>Licenc

Felhasználói licencet ír le.

>[!NOTE]
>Nem támogatott a 21Vianet Partnerközpont által üzemeltetett virtuális hálózatokon.

| Tulajdonság     | Típus                                                           | Description                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans (servicePlans) | ServicePlan-erőforrások tömbje                                 | A licencnek megfelelő szolgáltatás csomagok gyűjteménye |
| productSKU (termékváltozat)   | ProductSku (Termékváltozat)                                                     | A licencnek megfelelő termékváltozat.        |
| Attribútumok   | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A licencnek megfelelő metaadat-attribútumok.          |

## <a name="licenseupdate"></a>LicenseUpdate (Licencupdate)

A licencek felhasználóhoz való hozzárendelésének vagy eltávolításának információit biztosítja.

| Tulajdonság         | Típus                                                           | Description                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign (licencek hozzárendelése) | objektumok tömbje                                               | [LicenseAssignment objektumok tömbje.](#licenseassignment) |
| licensesToRemove | sztringek tömbje                                               | Az eltávolítható licencek termékváltozat-azonosítói.    |
| licenseWarnings  | objektumok tömbje                                               | [LicenseWarning objektumok tömbje.](#licensewarning)       |
| Attribútumok       | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                  |

## <a name="licenseassignment"></a>LicenseAssignment (Licenc hozzárendelése)

A licencfrissítési művelethez szükséges információkat biztosít.

| Tulajdonság      | Típus             | Description                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans (kizártsíkok) | sztringek tömbje | A szolgáltatás csomagazonosítóit ki kell zárni a rendelkezésre állásból a felhasználó számára. |
| skuId (termékváltozatazonosító)         | sztring           | A licenc termékváltozat-azonosítója.                                |

## <a name="licensewarning"></a>LicenseWarning

A licencfrissítési művelet során történt figyelmeztetési információkat tartalmazza.

| Tulajdonság     | Típus             | Description                                         |
|--------------|------------------|-----------------------------------------------------|
| code         | sztring           | A figyelmeztető kód.                                   |
| message      | sztring           | A figyelmeztető üzenet.                                |
| servicePlans (servicePlans) | sztringek tömbje | A figyelmeztetéshez társított szolgáltatásterv-nevek. |

## <a name="productsku"></a>ProductSku (Termékváltozat)

A termékadatokat ismerteti.

| Tulajdonság       | Típus             | Description                                         |
|----------------|------------------|-----------------------------------------------------|
| id             | sztring           | A termékazonosító.                             |
| name           | sztring           | Az egyszerű felhasználó azonosítója.                      |
| skuPartNumber  | sztring           | A termék termékváltozatának részszáma. Az E3 Office 365 például ez az `EnterprisePack` érték. Ez a tulajdonság használható azonosító helyére, ha az azonosító nem érhető el.                |
| targetType (céltípus)     | sztring           | A termék céltípusa. Ez a tulajdonság határozza meg, hogy a termék egy vagy egy `User` esetén `Tenant` alkalmazható-e.                                                                    |
| licenseGroupId (licenccsoport-azonosító) | sztring           | Csoportazonosítóval azonosítja a productSku licencet kezelő szolgáltatót vagy szolgáltatást. A jobb kezelhetőség érdekében a termékek licenccsoportok szerint vannak elkülönítve.<br/><br/>                                                                                     `group1`– Minden olyan termék, amelynek licencét a Azure Active Directory (AAD) tudja kezelni.<br/><br/>                                            `group2`– Minecraft terméklicencek használata.                                         |

## <a name="serviceplan"></a>ServicePlan

Egy termékváltozaton belül üzembe helyezhető szolgáltatást azonosít. Egy termék számos szolgáltatási csomagból lehet.

| Tulajdonság         | Típus   | Description                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | sztring | A szolgáltatás csomagazonosítója.                                                                                      |
| displayName      | sztring | A szolgáltatás csomag honosított megjelenítendő neve.                                                                  |
| serviceName (szolgáltatásnév)      | sztring | A szolgáltatás neve.                                                                                                 |
| capabilityStatus (kapacitásállapot) | sztring | A szolgáltatás csomag állapota.                                                                      |
| targetType (céltípus)       | sztring | A szolgáltatás csomag céltípusa. Ez a tulajdonság azonosítja, hogy a termék egy felhasználóra vagy bérlőre vonatkozik-e. |

## <a name="subscribedsku"></a>SubscribedSku

Egy bérlő által birtokolt, előfizetett terméket ír le.

| Tulajdonság         | Típus                                                           | Description                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits (elérhető egység)   | egész szám                                                        | A hozzárendelhető egységek száma. Ezt az értéket az összes egység – felhasznált egységek alapján számítjuk ki. |
| activeUnits (aktív egység)      | egész szám                                                        | A hozzárendeléshez aktív egységek száma.                                                        |
| consumedUnits    | egész szám                                                        | A felhasznált egységek száma.                                                                     |
| suspendedUnits   | egész szám                                                        | A felfüggesztett egységek száma.                                                                    |
| totalUnits (összes egység)       | egész szám                                                        | Az egységek teljes száma. Ezt az értéket a rendszer az aktív és figyelmeztető egységek összegeként számítja ki.         |
| warningUnits     | egész szám                                                        | A figyelmeztető egységek száma.                                                                      |
| productSku (termékváltozat)       | ProductSku (Termékváltozat)                                                     | A termékváltozat.                                                                                  |
| servicePlans (servicePlans)     | ServicePlan-erőforrások tömbje                                 | Egy termék szolgáltatási csomaggyűjteménye.                                                     |
| capabilityStatus (kapacitásállapot) | sztring                                                         | Egy termék termékváltozatának állapota.                                                                      |
| Attribútumok       | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | Az erőforrásnak megfelelő metaadat-attribútumok.                                            |
