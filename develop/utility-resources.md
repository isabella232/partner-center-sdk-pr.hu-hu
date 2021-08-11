---
title: Hasznos erőforrások
description: A Partnerközpont REST API számos erőforrást tartalmaz, amelyek az SDK-ban használt általános célú adatmodelleket írják le.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: de97feed13a4d0bae9743939a03f8cb8470f5f960bec0507cd9c5adfad287120
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115998042"
---
# <a name="utility-resources"></a>Hasznos erőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A Partnerközpont REST API számos erőforrást tartalmaz, amelyek az SDK-ban használt általános célú adatmodelleket írják le.

## <a name="address"></a>Cím

Az ügyfél- vagy partnerprofilok által használt cím. További információ a különböző országokban/régiókban támogatott formátumokról és tulajdonságokról: Címformázási szabályok lekérte [piac szerint.](get-market-specific-validation-data.md)

| Tulajdonság     | Típus   | Hossz (perc, maximum) | Description                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | sztring | (1, 200)          | A cím első sorában.                                                                   |
| AddressLine2 | sztring | (0, 200)          | A cím második sorában. Ez a tulajdonság nem kötelező.                                       |
| City         | sztring | n.a.               | A város.                                                                                        |
| Állapot        | sztring | (0, 2)            | Az állapot.                                                                                       |
| Irányítószám   | sztring | n.a.               | Az irányítószám vagy irányítószám.                                                                     |
| Ország      | sztring | (2, 2)            | Az ország/régió ISO országkódformátumban.                                                   |
| Régió       | sztring | n.a.               | A régió.                                                                                      |
| FirstName    | sztring | (1, 50)           | Az ügyfél vállalatának/szervezetének kapcsolattartója neve.                              |
| MiddleName (Középső név)   | sztring | (1, 50)           | Az ügyfél vállalatának/szervezetének kapcsolattartója középső neve. Ez a tulajdonság nem kötelező.  |
| LastName     | sztring | (1, 50)           | Az ügyfél vállalatának/szervezetének kapcsolattartója vezetékneve.                               |
| PhoneNumber  | sztring | n.a.               | Az ügyfél vállalatának/szervezetének kapcsolattartója telefonszáma. Ez a tulajdonság nem kötelező.|
|PhoneNumber|sztring|n.a.|Az ügyfél vállalatának/szervezetének kapcsolattartója telefonszáma. Az ügyfélprofilban ez a tulajdonság kötelező az ügyfél vállalata/szervezete számára, amely a következő országokban található: Uzbekistan(AZ), Uzbekistan(AZ), To(BY), Amelyet (HU), Mirgyzstan (KZ), Kyrgyzstan(KG), Kyrgyzstan (KG), Torgyzsán (MD), Oroszország(RU), Tj), Uzbekistan(UZ), Uzbekistan(UA)), India, Brazília, Dél-Afrika, Észak-Afrika, Egyesült Arab Emírségek, Szaúd-Arábia, Szignában, Vietnamban, Észak-Karolinában, Szignában, Dél-Afrikai Köztársaságban és Szignában. Ellenkező esetben ez nem kötelező.|


## <a name="contact"></a>Kapcsolattartó

Egy adott személy kapcsolattartási adatait ismerteti.

| Tulajdonság    | Típus   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | sztring | A kapcsolattartó vezetékneve.    |
| LastName    | sztring | A kapcsolattartó vezetékneve.     |
| E-mail       | sztring | A kapcsolattartó e-mail-címe. |
| PhoneNumber | sztring | A kapcsolattartó telefonszáma.  |

## <a name="fieldfilter"></a>FieldFilter (Szűrő)

A keresési eredményekre alkalmazható szűrőt ismerteti.

| Tulajdonság | Típus   | Description                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operátor | sztring | A szűrő operátora: "equals", \_ "not equals", "greater \_ than", "greater \_ than or \_ \_ equals", "less \_ than", "less \_ than or \_ \_ equals", "substring", "and", "or", "starts \_ with", "not \_ starts \_ with". |

## <a name="fileinfo"></a>FileInfo (Fájlinfo)

A fájlba feltöltött külső Partnerközpont.

| Tulajdonság                 | Típus   | Description                                   |
|--------------------------|--------|-----------------------------------------------|
| Megjegyzés                  | sztring | A fájlfeltöltéshez társított megjegyzés.    |
| FileExtension (Fájlextension)            | sztring | A fájlkiterjesztés.                           |
| FileNameWithoutExtension (FájlnévWithoutExtension) | sztring | A fájl neve, a bővítmény nem tartalmazza. |
| Fájlméretet                 | hosszú   | A fájl mérete.                         |
| Id                       | sztring | A fájlfeltöltés egyedi azonosítója.            |

## <a name="link"></a>Hivatkozás

Egy URI-hivatkozást és a kapcsolódó információkat tartalmazza.

| Tulajdonság | Típus                   | Description                        |
|----------|------------------------|------------------------------------|
| URI      | sztring                 | Az URI.                           |
| Metódus   | sztring                 | Az URI által képviselt metódus. |
| Fejlécek  | KeyValuePairs tömbje | A hivatkozás fejlécei.          |

## <a name="passwordprofile"></a>PasswordProfile (Jelszóprofil)

Egy adott jelszót és azt írja le, hogy a jelszót módosítani kell-e.

>[!NOTE]
>Nem támogatott a 21Vianet Partnerközpont által üzemeltetett virtuális hálózatokon.

| Tulajdonság            | Típus                          | Description                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Jelszó            | [SecureString](#securestring) | A jelszó.                                                          |
| ForceChangePassword | boolean                       | Meghatározza, hogy a jelszót a következő bejelentkezéskor kell-e meg kell-e változtatni. |

## <a name="resourcelinks"></a>ResourceLinks (Erőforrás-hivatkozás)

Egy erőforrásra mutató hivatkozások listáját tartalmazza.

| Tulajdonság   | Típus                                      | Description                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self       | [Link](#link)                             | Az ön URI.                                      |
| Következő       | [Link](#link)                             | Az elemek következő oldala.                            |
| Előző   | [Link](#link)                             | Az elemek előző oldala.                        |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](#resourceattributes) | A felhasználónak megfelelő metaadat-attribútumok. |

## <a name="resourceattributes"></a>ResourceAttributes (Erőforrás-attribútumok)

Attribútum-metaadatokat tartalmaz egy erőforráshoz.

| Tulajdonság   | Típus   | Description                                 |
|------------|--------|---------------------------------------------|
| Etag       | sztring | Az etag, más néven az objektum verziója. |
| ObjectType | sztring | Az alaperőforrás objektumtípusa.    |

## <a name="securestring"></a>SecureString

Biztonságos adatokat, például jelszót tárol.

| Tulajdonság | Típus | Description                       |
|----------|------|-----------------------------------|
| Hossz   | int  | A biztonságos sztring hossza. |

## <a name="validationcode"></a>Érvényesítési kód

Egy partner ellenőrzőkódját Government Community Cloud jelöli.

| Tulajdonság         | Típus         | Description                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| Partnerazonosító        | GUID         | Partnerazonosító                                                       |
| OrganizationName | sztring       | Az ellenőrzési folyamat során megadott szervezetnév             |
| ValidationId (Érvényesítésiazonosító)     | int          | Egy egyedi azonosító az ellenőrzéshez                                       |
| MaxCreates (Maximálislétrehozás)       | nullázható int | Ezzel az érvényesítési kóddal legfeljebb ügyfeleket lehet létrehozni    |
| FennmaradóLétrehozás | nullázható int | A fennmaradó ügyfél az érvényesítési azonosító alatt hoz létre egy újat                      |
| Etag             | sztring       | Az erőforrás adott verziója. Változások az erőforrás módosulása esetén. |
