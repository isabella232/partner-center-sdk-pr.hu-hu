---
title: Licencerőforrások
description: A licencekkel kapcsolatos erőforrásokat ismerteti.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 27d44f89ac89f365e77e073c425ca45ab3638c68
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548396"
---
# <a name="license-resources"></a>Licencerőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A licencekkel kapcsolatos erőforrásokat ismerteti.

## <a name="license"></a>Licenc

Felhasználói licencet ír le.

>[!NOTE]
>Nem támogatott a 21Vianet Partnerközpont által üzemeltetett virtuális hálózatokon.

| Tulajdonság     | Típus                                                           | Leírás                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans (szolgáltatássíkok) | ServicePlan-erőforrások tömbje                                 | A licencnek megfelelő szolgáltatás csomagok gyűjteménye |
| productSKU (termékváltozat)   | ProductSku (Termékváltozat)                                                     | A licencnek megfelelő termékváltozat.        |
| Attribútumok   | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A licencnek megfelelő metaadat-attribútumok.          |

## <a name="licenseupdate"></a>LicenseUpdate (Licencupdate)

A licencek felhasználókhoz való hozzárendelésének vagy eltávolításának információit biztosítja.

| Tulajdonság         | Típus                                                           | Leírás                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | objektumok tömbje                                               | [LicenseAssignment objektumok tömbje.](#licenseassignment) |
| licensesToRemove | sztringek tömbje                                               | Az eltávolítható licencek termékváltozat-azonosítói.    |
| licenseWarnings  | objektumok tömbje                                               | [LicenseWarning objektumok tömbje.](#licensewarning)       |
| Attribútumok       | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                  |

## <a name="licenseassignment"></a>LicenseAssignment (Licenc hozzárendelése)

A licencfrissítési művelethez szükséges információkat biztosítja.

| Tulajdonság      | Típus             | Leírás                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans (kizártsíkok) | sztringek tömbje | A szolgáltatásterv-azonosítókat ki kell zárni a rendelkezésre állásból a felhasználó számára. |
| skuId (termékváltozatazonosító)         | sztring           | A licenc termékváltozat-azonosítója.                                |

## <a name="licensewarning"></a>LicenseWarning

A licencfrissítési művelet során történt figyelmeztetési információkat tartalmazza.

| Tulajdonság     | Típus             | Leírás                                         |
|--------------|------------------|-----------------------------------------------------|
| code         | sztring           | A figyelmeztető kód.                                   |
| message      | sztring           | A figyelmeztető üzenet.                                |
| servicePlans (szolgáltatássíkok) | sztringek tömbje | A figyelmeztetéshez társított szolgáltatásterv-nevek. |

## <a name="productsku"></a>ProductSku (Termékváltozat)

Ismerteti a termékadatokat.

| Tulajdonság       | Típus             | Leírás                                         |
|----------------|------------------|-----------------------------------------------------|
| id             | sztring           | A termékazonosító.                             |
| name           | sztring           | Az egyszerű felhasználó azonosítója.                      |
| skuPartNumber  | sztring           | A termék termékváltozatának részszáma. Az E3 Office 365 például ez az érték `EnterprisePack` . Ez a tulajdonság használható az azonosító helyén, ha az azonosító nem érhető el.                |
| targetType (céltípus)     | sztring           | A termék céltípusa. Ez a tulajdonság azonosítja, hogy a termék alkalmazható-e egy vagy `User` egy `Tenant` termékre.                                                                    |
| licenseGroupId (licenccsoport-azonosító) | sztring           | Csoportazonosítón keresztül azonosítja a productSku licencet kezelő szolgáltatót vagy szolgáltatást. A jobb kezelhetőség érdekében a termékek licenccsoportok szerint vannak elkülönítve.<br/><br/>                                                                                     `group1`– Minden olyan termék, amelynek licencét a Azure Active Directory (AAD) tudja kezelni.<br/><br/>                                            `group2`– Minecraft terméklicencek használata.                                         |

## <a name="serviceplan"></a>ServicePlan

Egy termékváltozaton belül üzembe helyezhető szolgáltatást azonosít. Egy termék számos szolgáltatási csomagból lehet.

| Tulajdonság         | Típus   | Leírás                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | sztring | A szolgáltatás csomagazonosítója.                                                                                      |
| displayName      | sztring | A szolgáltatásterv honosított megjelenítendő neve.                                                                  |
| serviceName (szolgáltatásnév)      | sztring | A szolgáltatás neve.                                                                                                 |
| capabilityStatus (kapacitásállapot) | sztring | A szolgáltatás csomagállapota.                                                                      |
| targetType (céltípus)       | sztring | A szolgáltatás csomag céltípusa. Ez a tulajdonság azonosítja, hogy a termék alkalmazható-e a "Felhasználó" vagy a "Bérlő" tulajdonságra. |

## <a name="subscribedsku"></a>SubscribedSku

Egy bérlő által birtokolt, előfizetett terméket ír le.

| Tulajdonság         | Típus                                                           | Leírás                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits (elérhető egység)   | egész szám                                                        | A hozzárendelésre elérhető egységek száma. Ezt az értéket az összes egység – felhasznált egységek alapján számítjuk ki. |
| activeUnits      | egész szám                                                        | A hozzárendeléshez aktív egységek száma.                                                        |
| consumedUnits    | egész szám                                                        | A felhasznált egységek száma.                                                                     |
| suspendedUnits   | egész szám                                                        | A felfüggesztett egységek száma.                                                                    |
| totalUnits (összes egység)       | egész szám                                                        | Az egységek teljes száma. Ezt az értéket az aktív és a figyelmeztető egységek összegeként számítjuk ki.         |
| warningUnits     | egész szám                                                        | A figyelmeztető egységek száma.                                                                      |
| productSku (termékváltozat)       | ProductSku (Termékváltozat)                                                     | A termékváltozat.                                                                                  |
| servicePlans (szolgáltatássíkok)     | ServicePlan-erőforrások tömbje                                 | Egy termék szolgáltatás-csomaggyűjteménye.                                                     |
| capabilityStatus (kapacitásállapot) | sztring                                                         | Egy termék termékváltozatának állapota.                                                                      |
| Attribútumok       | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | Az erőforrásnak megfelelő metaadat-attribútumok.                                            |
