---
title: Erőforrások frissítése
description: A felhasználó forrás-előfizetésről cél-előfizetésre való frissítéséhez használt erőforrásokat ismerteti.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1ea7499a21312378f4fad3d47eaa9e10993ee3ce7ddb1498f161fac16e09b8a5
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992472"
---
# <a name="upgrade-resources"></a>Erőforrások frissítése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A felhasználó forrás-előfizetésről cél-előfizetésre való frissítéséhez használt erőforrásokat ismerteti.

## <a name="upgrade"></a>Frissítés

Az egyes frissítési erőforrások viselkedését ismerteti.

| Tulajdonság      | Típus                   | Description                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Ajánlat                  | A cél-előfizetés ajánlata.                                                        |
| UpgradeType (Frissítés típusa)   | sztring                 | A frissítés típusa: "nincs", "csak \_ frissítés" vagy "frissítés \_ \_ \_ licencátvitelsel".         |
| IsEligible (IsEligible)    | boolean                | Megállapítja, hogy a frissítés elvégezhető-e.                                                  |
| Mennyiség      | egész szám                | A megvásárolandó új ajánlat mennyisége. Alapértelmezés szerint a forrás-előfizetés mennyisége. |
| UpgradeErrors (Frissítési segédek) | UpgradeErrors tömb | Ok, amiért a frissítés nem hajtható végre, ha van ilyen.                                      |
| Attribútumok    | ResourceAttributes (Erőforrás-attribútumok)     | A frissítésnek megfelelő metaadat-attribútumok.                                        |

## <a name="upgradeerror"></a>UpgradeError

Leírja, hogy miért nem hajtható végre frissítés.

| Tulajdonság          | Típus               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code              | sztring             | A problémához kapcsolódó hibakód: "other", "delegated \_ admin \_ \_ permissions disabled", \_ "subscription status \_ not \_ active", "conflicting \_ service \_ types", "concurrency \_ conflicts", "user \_ context add \_ \_ \_ ons present", "subscription add ons present", "subscription does not have any upgrade \_ \_ \_ \_ \_ \_ \_ paths", "subscription \_ target offer not \_ \_ \_ found", or "subscription \_ not \_ provisioned". |
| Description       | sztring             | A hibát leíró rövid szöveg.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails (További részletek) | sztring             | A hibával kapcsolatos további részletek.                                                                                                                                                                                                                                                                                                                                                         |
| Attribútumok        | ResourceAttributes (Erőforrás-attribútumok) | A hibának megfelelő metaadat-attribútumok.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>UpgradeResult (Frissítés eredményének frissítése)

Az előfizetés-frissítési folyamat eredményét ismerteti.

| Tulajdonság             | Típus                        | Description                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId (Forrás-előíróazonosító) | sztring                      | A forrás-előfizetés azonosítója.                                           |
| TargetSubscriptionID (TargetSubscriptionID) | sztring                      | A cél-előfizetés azonosítója.                                           |
| UpgradeType (Frissítés típusa)          | sztring                      | A frissítés típusa: "nincs", "csak \_ frissítés" vagy "frissítés \_ \_ \_ licencátvitelsel". |
| UpgradeErrors (Frissítési segédek)        | UpgradeErrors tömb      | A frissítés végrehajtása során észlelt hibák, ha vannak.           |
| LicenseErrors (Licenccel rendelkezők)        | UserLicenseErrrors tömb | Felhasználói licencek áttelepítése során észlelt hibák, ha vannak.          |
| Attribútumok           | ResourceAttributes (Erőforrás-attribútumok)          | A licencnek megfelelő metaadat-attribútumok.                                |

## <a name="userlicenseerror"></a>UserLicenseError (FelhasználólicenseError)

A sikertelen felhasználói licencátvitelből eredő hibákat ismerteti.

| Tulajdonság     | Típus                   | Description                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId (Felhasználóiobjektum-azonosító) | sztring                 | A felhasználói objektum egyedi azonosítása.                                 |
| Name         | sztring                 | A felhasználó neve.                                                     |
| E-mail        | sztring                 | A felhasználó e-mail-címe.                                                    |
| Hibák       | ServiceFaults tömb | A felhasználói licencek átvitelekor történt kivételek listája. |
| Attribútumok   | ResourceAttributes (Erőforrás-attribútumok)     | A licencnek megfelelő metaadat-attribútumok.                     |

