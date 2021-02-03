---
title: Erőforrások frissítése
description: Azokat az erőforrásokat ismerteti, amelyekkel a felhasználó a forrás-előfizetésből a cél előfizetésre frissíthető.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bdbef383370761a01eb462f90284ad826a38ddaa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767868"
---
# <a name="upgrade-resources"></a>Erőforrások frissítése

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Azokat az erőforrásokat ismerteti, amelyekkel a felhasználó a forrás-előfizetésből a cél előfizetésre frissíthető.

## <a name="upgrade"></a>Frissítés

Leírja egy adott frissítési erőforrás viselkedését.

| Tulajdonság      | Típus                   | Leírás                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Ajánlat                  | A célként megadott előfizetés ajánlata.                                                        |
| UpgradeType   | sztring                 | A frissítés típusa: "None", "csak frissítés \_ " vagy "verziófrissítés \_ a licenccel" \_ \_ .         |
| IsEligible    | boolean                | Meghatározza, hogy a frissítés végrehajtható-e.                                                  |
| Mennyiség      | egész szám                | A megvásárolni kívánt új ajánlat számszerűsítése. Az alapértelmezett érték a forrás-előfizetés mennyisége. |
| UpgradeErrors | UpgradeErrors tömbje | A frissítés nem hajtható végre, ha van ilyen.                                      |
| Attribútumok    | ResourceAttributes     | A frissítéshez tartozó metaadat-attribútumok.                                        |

## <a name="upgradeerror"></a>UpgradeError

Leírja, hogy miért nem hajtható végre a frissítés.

| Tulajdonság          | Típus               | Leírás                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code              | sztring             | A problémához társított hibakód: "egyéb", "delegált \_ rendszergazdai \_ engedélyek \_ Letiltva", "az előfizetés \_ állapota \_ nem \_ aktív", "ütköző \_ szolgáltatások típusai", \_ "párhuzamossági \_ ütközések", "felhasználói \_ környezet \_ szükséges", "előfizetés hozzáadása a \_ \_ \_ jelen", "az előfizetés nem \_ \_ \_ rendelkezik \_ \_ frissítési \_ útvonalakkal", "az előfizetés \_ céljának \_ ajánlata \_ nem található" \_ vagy "előfizetés \_ nincs \_ kiépítve". |
| Description       | sztring             | A hibát leíró rövid szöveg.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | sztring             | A hibával kapcsolatos további részletek.                                                                                                                                                                                                                                                                                                                                                         |
| Attribútumok        | ResourceAttributes | A hibának megfelelő metaadat-attribútumok.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>UpgradeResult

Az előfizetés frissítési folyamatának eredményét írja le.

| Tulajdonság             | Típus                        | Leírás                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | sztring                      | A forrás-előfizetés azonosítója.                                           |
| TargetSubscriptionID | sztring                      | A célként megadott előfizetés azonosítója.                                           |
| UpgradeType          | sztring                      | A frissítés típusa: "None", "csak frissítés \_ " vagy "verziófrissítés \_ a licenccel" \_ \_ . |
| UpgradeErrors        | UpgradeErrors tömbje      | Hibák történtek a frissítés elvégzésére tett kísérlet során, ha van ilyen.           |
| LicenseErrors        | UserLicenseErrrors tömbje | Hiba történt a felhasználói licencek migrálása közben, ha van ilyen.          |
| Attribútumok           | ResourceAttributes          | A licenchez tartozó metaadat-attribútumok.                                |

## <a name="userlicenseerror"></a>UserLicenseError

A sikertelen felhasználói licencek átvitele miatti hibákat ismerteti.

| Tulajdonság     | Típus                   | Leírás                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | sztring                 | A felhasználói objektum egyedi azonosítása.                                 |
| Name         | sztring                 | A felhasználó neve.                                                     |
| E-mail        | sztring                 | A felhasználó e-mail-címe.                                                    |
| Hibák       | ServiceFaults tömbje | A felhasználói licencek átvitelére tett kísérlet során fellépő kivételek listája. |
| Attribútumok   | ResourceAttributes     | A licenchez tartozó metaadat-attribútumok.                     |

