---
title: Felhasználói erőforrások
description: Ismerteti az egyes partneri központ felhasználóit, a személyes és a fiókadatok adatait, valamint a partner centeren belüli engedélyeket.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c88b9b65dfb925712ff85fb42d34251cca6e0b5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767680"
---
# <a name="user-resources"></a>Felhasználói erőforrások

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ismerteti az egyes partneri központ felhasználóit, a személyes és a fiókadatok adatait, valamint a partner centeren belüli engedélyeket.

## <a name="user"></a>User

Egy egyéni felhasználót ír le.

| Tulajdonság              | Típus                                                           | Leírás                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | sztring                                                         | A felhasználói azonosító.                                                                                                                                                                                                       |
| userPrincipalName     | sztring                                                         | Az egyszerű felhasználói azonosító.                                                                                                                                                                                             |
| firstName             | sztring                                                         | A felhasználó vezetékneve.                                                                                                                                                                                                |
| lastName              | sztring                                                         | A felhasználó vezetékneve.                                                                                                                                                                                                 |
| displayName           | sztring                                                         | A felhasználó megjelenített neve.                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | A felhasználó jelszavas profilja.                                                                                                                                                                                               |
| Telefonszám           | sztring                                                         | A felhasználó telefonszáma.                                                                                                                                                                                                   |
| lastDirectorySyncTime | karakterlánc UTC-dátum időformátuma                                 | A Azure Active Directory és a helyszíni Active Directory között az utolsó alkalommal szinkronizálva lett a felhasználó adatai. A dátum/idő érték csak akkor jelenik meg, ha Azure AD Connect szinkronizálás engedélyezve van. Ellenkező esetben az érték null. |
| userDomainType        | sztring                                                         | A felhasználói tartomány típusa: "None", "felügyelt" vagy "összevont".                                                                                                                                                                   |
| állapot                 | sztring                                                         | A felhasználó állapota: "Active", "inaktív" (törölt felhasználó esetén).                                                                                                                                                          |
| softDeletionTime      | karakterlánc UTC-dátum időformátuma                                 | Azt a harminc napos időszak kezdetét jelöli, amely után a törölt felhasználóhoz tartozó adatok véglegesen törlődnek, és ezért nem állíthatók helyre.                                                                          |
| linkek                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Az erőforrás-hivatkozások.                                                                                                                                                                                                        |
| attribútumok            | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.                                                                                                                                                                                                   |

## <a name="customeruser"></a>CustomerUser

Az ügyfél felhasználóját ismerteti.

| Tulajdonság              | Típus                                                           | Leírás                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | sztring                                                         | Az a hely, ahol a felhasználó használni kívánja a licencet.                                                                                                                                                                    |
| id                    | sztring                                                         | A felhasználói azonosító.                                                                                                                                                                                                       |
| userPrincipalName     | sztring                                                         | Az egyszerű felhasználói azonosító.                                                                                                                                                                                             |
| firstName             | sztring                                                         | A felhasználó vezetékneve.                                                                                                                                                                                                |
| lastName              | sztring                                                         | A felhasználó vezetékneve.                                                                                                                                                                                                 |
| displayName           | sztring                                                         | A felhasználó megjelenített neve.                                                                                                                                                                                            |
| immutableId           | sztring                                                         | A felhasználó megváltoztathatatlan azonosítója.                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | A felhasználó jelszavas profilja.                                                                                                                                                                                               |
| Telefonszám           | sztring                                                         | A felhasználó telefonszáma.                                                                                                                                                                                                   |
| lastDirectorySyncTime | karakterlánc UTC-dátum időformátuma                                 | A Azure Active Directory és a helyszíni Active Directory között az utolsó alkalommal szinkronizálva lett a felhasználó adatai. A dátum/idő érték csak akkor jelenik meg, ha Azure AD Connect szinkronizálás engedélyezve van. Ellenkező esetben az érték null. |
| userDomainType        | sztring                                                         | A felhasználói tartomány típusa: "None", "felügyelt" vagy "összevont".                                                                                                                                                                   |
| állapot                 | sztring                                                         | A felhasználó állapota: "Active", "inaktív" (törölt felhasználó esetén).                                                                                                                                                          |
| softDeletionTime      | karakterlánc UTC-dátum időformátuma                                 | Azt a harminc napos időszak kezdetét jelöli, amely után a törölt felhasználóhoz tartozó adatok véglegesen törlődnek, és ezért nem állíthatók helyre.                                                                          |
| linkek                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Az erőforrás-hivatkozások.                                                                                                                                                                                                        |
| attribútumok            | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.                                                                                                                                                                                                   |

## <a name="usercredentials"></a>UserCredentials

A felhasználó bejelentkezési hitelesítő adatainak leírása.

| Tulajdonság | Típus                                               | Leírás                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName (Felhasználónév) | sztring                                             | A felhasználó neve.                |
| jelszó | [SecureString](utility-resources.md#securestring) | A felhasználó biztonságos tárolt jelszava. |

## <a name="usermember"></a>UserMember

A felhasználó tag adatait ismerteti.

| Tulajdonság          | Típus                                                           | Leírás                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | sztring                                                         | A felhasználó megjelenített neve.   |
| userPrincipalName | sztring                                                         | A felhasználói tag neve.    |
| Szerepkörazonosítónak            | sztring                                                         | A felhasználó szerepkörének azonosítója. |
| id                | sztring                                                         | A tag azonosítója.      |
| attribútumok        | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.           |

