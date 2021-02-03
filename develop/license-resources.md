---
title: Licenc-erőforrások
description: A licencekkel kapcsolatos erőforrásokat ismerteti.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 681f53ec73122a4861e6f1a2f96560336481a068
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768199"
---
# <a name="license-resources"></a>Licenc-erőforrások

**A következőkre vonatkozik**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A licencekkel kapcsolatos erőforrásokat ismerteti.

## <a name="license"></a>Licenc

A felhasználói licenc leírása.

>[!NOTE]
>Nem támogatott a 21Vianet által működtetett partner Centerben.

| Tulajdonság     | Típus                                                           | Leírás                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | ServicePlan-erőforrások tömbje                                 | A licencnek megfelelő szolgáltatási csomagok gyűjteménye |
| productSKU   | ProductSku                                                     | A licencnek megfelelő termék SKU-jának.        |
| attribútumok   | [ResourceAttributes](utility-resources.md#resourceattributes) | A licenchez tartozó metaadat-attribútumok.          |

## <a name="licenseupdate"></a>LicenseUpdate

A felhasználók licencének hozzárendeléséhez vagy eltávolításához használt információkat tartalmazza.

| Tulajdonság         | Típus                                                           | Leírás                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | objektumok tömbje                                               | [LicenseAssignment](#licenseassignment) objektumok tömbje. |
| licensesToRemove | sztringek tömbje                                               | Az eltávolítandó licencek termék SKU-azonosítói.    |
| licenseWarnings  | objektumok tömbje                                               | [LicenseWarning](#licensewarning) objektumok tömbje.       |
| attribútumok       | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.                                  |

## <a name="licenseassignment"></a>LicenseAssignment

A licenc-frissítési művelethez szükséges információkat tartalmazza.

| Tulajdonság      | Típus             | Leírás                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | sztringek tömbje | A felhasználó számára a rendelkezésre állásból kizárandó szolgáltatáscsomag-azonosítók. |
| skuId         | sztring           | A licenc termék SKU-azonosítója.                                |

## <a name="licensewarning"></a>LicenseWarning

A licenc-frissítési művelet során bekövetkezett figyelmeztetési információkat tartalmaz.

| Tulajdonság     | Típus             | Leírás                                         |
|--------------|------------------|-----------------------------------------------------|
| code         | sztring           | A figyelmeztetési kód.                                   |
| message      | sztring           | A figyelmeztető üzenet.                                |
| servicePlans | sztringek tömbje | A figyelmeztetéshez társított szolgáltatási csomag neve. |

## <a name="productsku"></a>ProductSku

A termék részleteit ismerteti.

| Tulajdonság       | Típus             | Leírás                                         |
|----------------|------------------|-----------------------------------------------------|
| id             | sztring           | A termék azonosítója.                             |
| name           | sztring           | Az egyszerű felhasználói azonosító.                      |
| skuPartNumber  | sztring           | A termékhez tartozó SKU-cikkszám neve. Például az Office 365 E3 csomag esetében ez az érték `EnterprisePack` . Ez a tulajdonság az azonosító helyett használható, ha az azonosító nem érhető el.                |
| targetType     | sztring           | A termék céljának típusa. Ez a tulajdonság határozza meg, hogy a termék alkalmazható-e a `User` vagy a értékre `Tenant` .                                                                    |
| licenseGroupId | sztring           | A productSku-licencet kezelő szolgáltató vagy szolgáltatás csoport-azonosítóján keresztül azonosítja. A termékek a jobb kezelhetőség érdekében a licencfeltételeket elkülönítve vannak.<br/><br/>                                                                                     `group1` – Az összes olyan termék, amelynek licenceit Azure Active Directory kezelheti (HRE).<br/><br/>                                            `group2` -Minecraft-termékek licencei.                                         |

## <a name="serviceplan"></a>ServicePlan

A termék SKU-ban található telepíthető szolgáltatás. Egy terméknek számos szolgáltatási csomagja lehet.

| Tulajdonság         | Típus   | Leírás                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | sztring | A szolgáltatási csomag azonosítója.                                                                                      |
| displayName      | sztring | A szolgáltatási csomag honosított megjelenítendő neve.                                                                  |
| serviceName      | sztring | A szolgáltatás neve.                                                                                                 |
| capabilityStatus | sztring | A szolgáltatáscsomag szolgáltatási tervének állapota.                                                                      |
| targetType       | sztring | A szolgáltatási csomag célként megadott típusa. Ez a tulajdonság határozza meg, hogy a termék alkalmazható-e "felhasználó" vagy "bérlő" esetén. |

## <a name="subscribedsku"></a>SubscribedSku

Egy bérlő által birtokolt előfizetett termék leírása.

| Tulajdonság         | Típus                                                           | Leírás                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | egész szám                                                        | A hozzárendeléshez rendelkezésre álló egységek száma. Ez az érték teljes egységként felhasznált egységként lesz kiszámítva. |
| activeUnits      | egész szám                                                        | A hozzárendeléshez aktív egységek száma.                                                        |
| consumedUnits    | egész szám                                                        | A felhasznált egységek száma.                                                                     |
| suspendedUnits   | egész szám                                                        | A felfüggesztett egységek száma.                                                                    |
| totalUnits       | egész szám                                                        | Az egységek teljes száma. Ezt az értéket az aktív és a figyelmeztetési egységek összegeként számítjuk ki.         |
| warningUnits     | egész szám                                                        | A figyelmeztetési egységek száma.                                                                      |
| productSku       | ProductSku                                                     | A termék SKU-jának.                                                                                  |
| servicePlans     | ServicePlan-erőforrások tömbje                                 | Egy termék szolgáltatási csomagjainak gyűjteménye.                                                     |
| capabilityStatus | sztring                                                         | Egy termék SKU-állapota.                                                                      |
| attribútumok       | [ResourceAttributes](utility-resources.md#resourceattributes) | Az erőforráshoz tartozó metaadat-attribútumok.                                            |
