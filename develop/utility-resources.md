---
title: Hasznos erőforrások
description: A partner Center REST API számos olyan erőforrást tartalmaz, amelyek az SDK-ban használt általános célú adatmodelleket írják le.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 115b0508f956c4b60e4db53193ef2585fa0c9a34
ms.sourcegitcommit: 204e518e794b6b076a17488ee9ca1aaaa4beaaec
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/01/2021
ms.locfileid: "106103980"
---
# <a name="utility-resources"></a>Hasznos erőforrások

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A partner Center REST API számos olyan erőforrást tartalmaz, amelyek az SDK-ban használt általános célú adatmodelleket írják le.

## <a name="address"></a>Cím

Az ügyfél-vagy partneri profilokhoz használandó címe. A különböző országokban/régiókban támogatott formátumokkal és tulajdonságokkal kapcsolatos további információkért lásd: a [címek formázási szabályainak beolvasása a piacon](get-market-specific-validation-data.md).

| Tulajdonság     | Típus   | Hossz (min., max.) | Leírás                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | sztring | (1, 200)          | A címe első sora.                                                                   |
| AddressLine2 | sztring | (0, 200)          | A címe második sora. Ez a tulajdonság nem kötelező.                                       |
| City         | sztring | n.a.               | A város.                                                                                        |
| Állapot        | sztring | (0, 2)            | Az állapot.                                                                                       |
| Irányítószám   | sztring | n.a.               | A ZIP-kód vagy postai irányítószám.                                                                     |
| Ország      | sztring | (2, 2)            | Az ország/régió ISO-országkód szerinti formátuma.                                                   |
| Region       | sztring | n.a.               | A régió.                                                                                      |
| FirstName    | sztring | (1, 50)           | Egy partner vezetékneve az ügyfél vállalatánál vagy szervezetében.                              |
| MiddleName   | sztring | (1, 50)           | Az ügyfél cége/szervezete kapcsolattartójának középső neve. Ez a tulajdonság nem kötelező.  |
| LastName     | sztring | (1, 50)           | Egy partner vezetékneve az ügyfél vállalatánál vagy szervezetében.                               |
| PhoneNumber  | sztring | n.a.               | Egy partner telefonszáma az ügyfél vállalata/szervezete számára. Ez a tulajdonság nem kötelező.|
|PhoneNumber|sztring|n.a.|Egy partner telefonszáma az ügyfél vállalata/szervezete számára. Az ügyfél profiljában ez a tulajdonság a következő országokban található ügyfél vállalata/szervezete számára kötelező: Örményország (AM), Azerbajdzsán (AZ), Fehéroroszország (BY), Magyarország (HU), Kazahsztán (KZ), Kirgizisztán (KG), Moldova (MD), Oroszország (RU), Tádzsikisztán (TJ), Üzbegisztán (), Ukrajna (UA)), India, Brazília, Dél-Afrika, Lengyelország, Egyesült Arab Emírségek, Szaúd-Arábia, Törökország, Thaiföld, Vietnam, Mianmar, Irak, Dél-Szudán és Venezuela. Ellenkező esetben ez nem kötelező.|


## <a name="contact"></a>Kapcsolattartó

Egy adott személy kapcsolattartási adatait ismerteti.

| Tulajdonság    | Típus   | Leírás                  |
|-------------|--------|------------------------------|
| FirstName   | sztring | A partner vezetékneve.    |
| LastName    | sztring | A partner vezetékneve.     |
| E-mail       | sztring | A partner e-mail-címe. |
| PhoneNumber | sztring | A partner telefonszáma.  |

## <a name="fieldfilter"></a>FieldFilter

A keresési eredményekre alkalmazható szűrőt ismerteti.

| Tulajdonság | Típus   | Leírás                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operátor | sztring | A Filter operátor: "Equals", "nem \_ egyenlő", "nagyobb, mint \_ ", "nagyobb \_ \_ vagy egyenlő" \_ , "kisebb, \_ mint", "kisebb \_ \_ vagy \_ egyenlő", "alsztring", "és", "vagy", "a", "karakterrel kezdődik" \_ , "nem \_ kezdődik \_ ". |

## <a name="fileinfo"></a>FileInfo

A partner központba feltöltött külső fájlt jelöli.

| Tulajdonság                 | Típus   | Leírás                                   |
|--------------------------|--------|-----------------------------------------------|
| Megjegyzés                  | sztring | A fájl feltöltésével kapcsolatos megjegyzés.    |
| FileExtension            | sztring | A fájlkiterjesztés.                           |
| FileNameWithoutExtension | sztring | A fájl neve, amely nem tartalmazza a kiterjesztést. |
| FileSize                 | hosszú   | A fájl mérete.                         |
| Id                       | sztring | A fájlfeltöltés egyedi azonosítója.            |

## <a name="link"></a>Hivatkozás

URI-hivatkozást és kapcsolódó adatokat tartalmaz.

| Tulajdonság | Típus                   | Leírás                        |
|----------|------------------------|------------------------------------|
| URI      | sztring                 | Az URI.                           |
| Metódus   | sztring                 | Az URI által jelzett metódus. |
| Fejlécek  | KeyValuePairs tömbje | A hivatkozás fejlécei          |

## <a name="passwordprofile"></a>PasswordProfile

Egy adott jelszó leírása, és ha a jelszót módosítani kell.

>[!NOTE]
>Nem támogatott a 21Vianet által működtetett partner Centerben.

| Tulajdonság            | Típus                          | Leírás                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Jelszó            | [SecureString](#securestring) | A jelszó.                                                          |
| ForceChangePassword | boolean                       | Meghatározza, hogy a jelszót kényszerítve kell-e módosítani a következő bejelentkezéskor. |

## <a name="resourcelinks"></a>ResourceLinks

Egy erőforrás hivatkozásainak listáját tartalmazza.

| Tulajdonság   | Típus                                      | Leírás                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self       | [Hivatkozás](#link)                             | A saját URI-ja.                                      |
| Következő       | [Hivatkozás](#link)                             | Az elemek következő lapja.                            |
| Előző   | [Hivatkozás](#link)                             | Az elemek előző lapja.                        |
| Attribútumok | [ResourceAttributes](#resourceattributes) | A felhasználóhoz tartozó metaadat-attribútumok. |

## <a name="resourceattributes"></a>ResourceAttributes

Attribútum-metaadatokat tartalmaz egy erőforráshoz.

| Tulajdonság   | Típus   | Leírás                                 |
|------------|--------|---------------------------------------------|
| ETAG       | sztring | A ETAG, más néven az objektum verziója. |
| ObjectType | sztring | Az alap erőforrás objektumának típusa    |

## <a name="securestring"></a>SecureString

Biztonságos adatokat, például jelszavakat tárol.

| Tulajdonság | Típus | Leírás                       |
|----------|------|-----------------------------------|
| Hossz   | int  | A biztonságos sztring hossza. |

## <a name="validationcode"></a>ValidationCode

A partner kormányzati közösségi felhő-ellenőrzési kódját jelöli.

| Tulajdonság         | Típus         | Leírás                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | Partner azonosítója                                                       |
| OrganizationName | sztring       | Az érvényesítési folyamat során megadott szervezet neve             |
| ValidationId     | int          | Az érvényesítés egyedi azonosítója                                       |
| MaxCreates       | NULL értékű int | Az ezzel az érvényesítési kóddal létrehozott ügyfelek maximális száma    |
| RemainingCreates | NULL értékű int | Fennmaradó ügyfél létrehozva ebben az érvényesítési AZONOSÍTÓban                      |
| ETag             | sztring       | Az erőforrás adott verziója. Változások az erőforrás változásakor. |
