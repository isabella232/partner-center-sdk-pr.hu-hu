---
title: Felhasználói erőforrások
description: Egy egyéni felhasználót Partnerközpont, a személyes és fiókinformációit, valamint a felhasználókon belüli Partnerközpont.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c91e3509d86c8817da30c8ad0d96a2b1b6eec7697e43b47d3dfb96055cac632
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989219"
---
# <a name="user-resources"></a>Felhasználói erőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Egy egyéni felhasználót Partnerközpont, a személyes és fiókinformációit, valamint a felhasználókon belüli Partnerközpont.

## <a name="user"></a>Felhasználó

Egy adott felhasználót ír le.

| Tulajdonság              | Típus                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | sztring                                                         | A felhasználói azonosító.                                                                                                                                                                                                       |
| userPrincipalName     | sztring                                                         | Az egyszerű felhasználó azonosítója.                                                                                                                                                                                             |
| firstName             | sztring                                                         | A felhasználó vezetékneve.                                                                                                                                                                                                |
| lastName              | sztring                                                         | A felhasználó vezetékneve.                                                                                                                                                                                                 |
| displayName           | sztring                                                         | A felhasználó megjelenített neve.                                                                                                                                                                                            |
| passwordProfile (jelszóprofil)       | [PasswordProfile (Jelszóprofil)](utility-resources.md#passwordprofile)       | A felhasználó jelszóprofilja.                                                                                                                                                                                               |
| phoneNumber (telefonszám)           | sztring                                                         | A felhasználó telefonszáma.                                                                                                                                                                                                   |
| lastDirectorySyncTime | sztring UTC dátum- és időformátumban                                 | Az utolsó alkalom, amikor a felhasználó adatai szinkronizálva Azure Active Directory és helyi Active Directory. A dátum-idő érték csak akkor jelenik meg, ha az Azure AD Csatlakozás engedélyezve van. Ellenkező esetben az érték null. |
| userDomainType (felhasználótartománytípus)        | sztring                                                         | A felhasználói tartomány típusa: "nincs", "felügyelt" vagy "összevont".                                                                                                                                                                   |
| állapot                 | sztring                                                         | A felhasználó állapota: "aktív", "inaktív" (törölt felhasználó esetében).                                                                                                                                                          |
| softDeletionTime      | sztring UTC dátum- és időformátumban                                 | Annak a 30 napos időszaknak a kezdete, amely után a törölt felhasználóhoz társított adatok véglegesen törölve lesznek, ezért nem állíthatók vissza.                                                                          |
| Linkek                 | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | Az erőforrás-hivatkozások.                                                                                                                                                                                                        |
| Attribútumok            | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                                                                                                                                                                                   |

## <a name="customeruser"></a>CustomerUser

Egy ügyfélfelhasználót ír le.

| Tulajdonság              | Típus                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | sztring                                                         | Az a hely, ahol a felhasználó használni kívánja a licencet.                                                                                                                                                                    |
| id                    | sztring                                                         | A felhasználói azonosító.                                                                                                                                                                                                       |
| userPrincipalName     | sztring                                                         | Az egyszerű felhasználó azonosítója.                                                                                                                                                                                             |
| firstName             | sztring                                                         | A felhasználó vezetékneve.                                                                                                                                                                                                |
| lastName              | sztring                                                         | A felhasználó vezetékneve.                                                                                                                                                                                                 |
| displayName           | sztring                                                         | A felhasználó megjelenített neve.                                                                                                                                                                                            |
| immutableId (nem módosíthatóid)           | sztring                                                         | A felhasználó nem módosítható azonosítója.                                                                                                                                                                                              |
| passwordProfile (jelszóprofil)       | [PasswordProfile (Jelszóprofil)](utility-resources.md#passwordprofile)       | A felhasználó jelszóprofilja.                                                                                                                                                                                               |
| phoneNumber (telefonszám)           | sztring                                                         | A felhasználó telefonszáma.                                                                                                                                                                                                   |
| lastDirectorySyncTime | sztring UTC dátum- és időformátumban                                 | Az utolsó alkalom, amikor a felhasználó adatai szinkronizálva Azure Active Directory és helyi Active Directory. A dátum-idő érték csak akkor jelenik meg, ha az Azure AD Csatlakozás engedélyezve van. Ellenkező esetben az érték null. |
| userDomainType (felhasználótartománytípus)        | sztring                                                         | A felhasználói tartomány típusa: "nincs", "felügyelt" vagy "összevont".                                                                                                                                                                   |
| állapot                 | sztring                                                         | A felhasználó állapota: "aktív", "inaktív" (törölt felhasználó esetében).                                                                                                                                                          |
| softDeletionTime      | sztring UTC dátum- és időformátumban                                 | Annak a 30 napos időszaknak a kezdete, amely után a törölt felhasználóhoz társított adatok véglegesen törölve lesznek, ezért nem állíthatók vissza.                                                                          |
| Linkek                 | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | Az erőforrás-hivatkozások.                                                                                                                                                                                                        |
| Attribútumok            | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                                                                                                                                                                                   |

## <a name="usercredentials"></a>UserCredentials (UserCredentials)

A felhasználó bejelentkezési hitelesítő adatait ismerteti.

| Tulajdonság | Típus                                               | Description                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName (Felhasználónév) | sztring                                             | A felhasználó neve.                |
| jelszó | [SecureString](utility-resources.md#securestring) | A felhasználó biztonságosan tárolt jelszava. |

## <a name="usermember"></a>UserMember

A felhasználó taginformációit ismerteti.

| Tulajdonság          | Típus                                                           | Description                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | sztring                                                         | A felhasználó megjelenített neve.   |
| userPrincipalName | sztring                                                         | Az egyszerű felhasználó neve.    |
| roleId (szerepkörazonosító)            | sztring                                                         | A felhasználó szerepkörének azonosítója. |
| id                | sztring                                                         | A tag azonosítója.      |
| Attribútumok        | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.           |

