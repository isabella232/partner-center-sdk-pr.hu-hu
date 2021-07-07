---
title: Hasznos erőforrások
description: A Partnerközpont REST API számos erőforrást tartalmaz, amelyek az SDK-ban használt általános célú adatmodelleket írják le.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 095cf36d47b147eb6df28d8747889e218c270659
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529664"
---
# <a name="utility-resources"></a>Hasznos erőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A Partnerközpont REST API számos erőforrást tartalmaz, amelyek az SDK-ban használt általános célú adatmodelleket írják le.

## <a name="address"></a>Cím

Az ügyfél- vagy partnerprofilok által használt cím. A különböző országokban/régiókban támogatott formátumokkal és tulajdonságokkal kapcsolatos további információkért lásd: Címformázási szabályok lekérte [piac szerint.](get-market-specific-validation-data.md)

| Tulajdonság     | Típus   | Hossz (min, max) | Leírás                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | sztring | (1, 200)          | A cím első sorát.                                                                   |
| AddressLine2 | sztring | (0, 200)          | A cím második sorában. Ez a tulajdonság nem kötelező.                                       |
| City         | sztring | n.a.               | A város.                                                                                        |
| Állapot        | sztring | (0, 2)            | Az állapot.                                                                                       |
| Irányítószám   | sztring | n.a.               | Az irányítószám vagy irányítószám.                                                                     |
| Ország      | sztring | (2, 2)            | Az ország/régió ISO országkódformátumban.                                                   |
| Region       | sztring | n.a.               | A régió.                                                                                      |
| FirstName    | sztring | (1, 50)           | Az ügyfél vállalatának/szervezetének kapcsolattartója.                              |
| MiddleName (Középső név)   | sztring | (1, 50)           | Az ügyfél vállalatának/szervezetének kapcsolattartója középső neve. Ez a tulajdonság nem kötelező.  |
| LastName     | sztring | (1, 50)           | Az ügyfél vállalatának/szervezetének kapcsolattartója vezetékneve.                               |
| PhoneNumber  | sztring | n.a.               | Az ügyfél vállalatának/szervezetének kapcsolattartója telefonszáma. Ez a tulajdonság nem kötelező.|
|PhoneNumber|sztring|n.a.|Az ügyfél vállalatának/szervezetének kapcsolattartója telefonszáma. Az ügyfélprofilban ez a tulajdonság kötelező az ügyfél vállalata/szervezete számára, amely a következő országokban található: Uzbekistan(AZ), Uzbekistan(AZ), Amelyet(BY), Fog(HU), Torgyzstan (KZ), Kyrgyzstan(KG), Torgyzstan (KG), Oroszország(RU), Tajikistan(TJ), Uzbekistan(UZ), EgyVecs (UA)), India, Brazília, Dél-Afrikai Köztársaság, Egyesült Arab Emírségek, Egyesült Arab Emírségek, Észak-Karolina, Észak-Karolina, Dél-Afrikai Köztársaság és Dél-Korea. Ellenkező esetben ez nem kötelező.|


## <a name="contact"></a>Kapcsolattartó

Egy adott személy kapcsolattartási adatait ismerteti.

| Tulajdonság    | Típus   | Leírás                  |
|-------------|--------|------------------------------|
| FirstName   | sztring | A kapcsolattartó vezetékneve.    |
| LastName    | sztring | A kapcsolattartó vezetékneve.     |
| E-mail       | sztring | A kapcsolattartó e-mail-címe. |
| PhoneNumber | sztring | A kapcsolattartó telefonszáma.  |

## <a name="fieldfilter"></a>MezőSzűrő

A keresési eredményekre alkalmazható szűrőt ismerteti.

| Tulajdonság | Típus   | Leírás                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operátor | sztring | A szűrő operátora: "equals", \_ "not equals", \_ "greater than", "greater \_ than or \_ \_ equals", \_ "less than", "less than \_ or \_ \_ equals", "substring", "and", "or", "starts \_ with", "not \_ starts \_ with". |

## <a name="fileinfo"></a>FileInfo (Fájlbefo)

A fájlba feltöltött külső Partnerközpont.

| Tulajdonság                 | Típus   | Leírás                                   |
|--------------------------|--------|-----------------------------------------------|
| Megjegyzés                  | sztring | A fájlfeltöltéshez társított megjegyzés.    |
| FileExtension (Fájlextension)            | sztring | A fájlkiterjesztés.                           |
| FileNameWithoutExtension (FájlnévWithoutExtension) | sztring | A fájl neve, a bővítmény nem tartalmazza. |
| Fájlméretet                 | hosszú   | A fájl mérete.                         |
| Id                       | sztring | A fájlfeltöltés egyedi azonosítója.            |

## <a name="link"></a>Hivatkozás

Egy URI-hivatkozást és a kapcsolódó információkat tartalmazza.

| Tulajdonság | Típus                   | Leírás                        |
|----------|------------------------|------------------------------------|
| URI      | sztring                 | Az URI.                           |
| Metódus   | sztring                 | Az URI által képviselt metódus. |
| Fejlécek  | KeyValuePairs tömbje | A hivatkozás fejlécei.          |

## <a name="passwordprofile"></a>PasswordProfile (Jelszóprofil)

Egy adott jelszót és azt írja le, hogy a jelszót módosítani kell-e.

>[!NOTE]
>Nem támogatott a 21Vianet Partnerközpont által üzemeltetett virtuális hálózatokon.

| Tulajdonság            | Típus                          | Leírás                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Jelszó            | [SecureString](#securestring) | A jelszó.                                                          |
| ForceChangePassword | boolean                       | Meghatározza, hogy a jelszót a következő bejelentkezéskor kell-e meg kell-e változtatni. |

## <a name="resourcelinks"></a>ResourceLinks (Erőforrás-hivatkozás)

Egy erőforrásra mutató hivatkozások listáját tartalmazza.

| Tulajdonság   | Típus                                      | Leírás                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self       | [Link](#link)                             | Az ön URI.                                      |
| Következő       | [Link](#link)                             | Az elemek következő oldala.                            |
| Előző   | [Link](#link)                             | Az elemek előző oldala.                        |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](#resourceattributes) | A felhasználónak megfelelő metaadat-attribútumok. |

## <a name="resourceattributes"></a>ResourceAttributes (Erőforrás-attribútumok)

Attribútum-metaadatokat tartalmaz egy erőforráshoz.

| Tulajdonság   | Típus   | Leírás                                 |
|------------|--------|---------------------------------------------|
| Etag       | sztring | Az etag, más néven az objektum verziója. |
| ObjectType | sztring | Az alaperőforrás objektumtípusa.    |

## <a name="securestring"></a>SecureString

Biztonságos adatokat, például jelszót tárol.

| Tulajdonság | Típus | Leírás                       |
|----------|------|-----------------------------------|
| Hossz   | int  | A biztonságos sztring hossza. |

## <a name="validationcode"></a>Érvényesítési kód

Egy partner ellenőrzőkódját Government Community Cloud jelöli.

| Tulajdonság         | Típus         | Leírás                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| Partnerazonosító        | GUID         | Partnerazonosító                                                       |
| OrganizationName | sztring       | Az ellenőrzési folyamat során megadott szervezetnév             |
| ValidationId (Érvényesítésiazonosító)     | int          | Egy egyedi azonosító az ellenőrzéshez                                       |
| MaxCreates (Maximálislétrehozás)       | nullázható int | Ezzel az érvényesítési kóddal legfeljebb ügyfeleket lehet létrehozni    |
| FennmaradóLétrehozás | nullázható int | A fennmaradó ügyfél az érvényesítési azonosító alatt hoz létre egy újat                      |
| Etag             | sztring       | Az erőforrás adott verziója. Változások az erőforrás módosulása esetén. |
