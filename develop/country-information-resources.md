---
title: Országinformációs források
description: Ismerje meg a Partnerközpont API-k használatát az országokkal kapcsolatos információforrásokkal és egy adott országhoz vagy régióhoz kapcsolódó leíró metaadatokkal.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 35b570b27466699d8d85819f7603794888f8dd943038ee28a0a734b7ef9aa0d1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991820"
---
# <a name="country-information-resources-available-from-partner-center-apis"></a>A különböző API-kból Partnerközpont országokkal kapcsolatos információforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az alábbi források egy ország/régió leíró metaadatai.

## <a name="countryinformation"></a>CountryInformation (Országinformáció)

| Tulajdonság                      | Típus               | Description                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData (Bővítményadatok)                 | sztring             | A bővítmény adatai.                                                                                |
| Iso2Code                      | sztring             | Iso-2 kód.                                                                                     |
| Iso3Code                      | sztring             | Iso-3-kód.                                                                                     |
| DefaultCulture (Alapértelmezett culture)                | sztring             | Az alapértelmezett kulturális környezet.                                                                               |
| IsStateRequired               | boolean            | Azt jelzi, hogy szükség van-e egy államra/tartományra.                                             |
| SupportedStatesList (TámogatottstatesList)           | sztringek tömbje   | Ha szükség van egy államra/tartományra, az adott ország/régió teljes listáját adja vissza.                    |
| SupportedLanguagesList        | sztringek tömbje   | A támogatott nyelvek listája.                                                                     |
| SupportedCulturesList         | sztringek tömbje   | A támogatott kulturális világok listája.                                                                      |
| IsPostalCodeRequired          | boolean            | Azt jelzi, hogy szükség van-e irányítószámra vagy irányítószámra.                                    |
| PostalCodeRegex               | sztring             | Az irányítószámot meghatározó reguláris kifejezés.                                          |
| IsCityRequired                | boolean            | Azt jelzi, hogy szükség van-e egy városra.                                                       |
| IsVatIdSupported              | boolean            | Azt jelzi, hogy szükség van-e áfaazonosítóra.                                                     |
| TaxIdFormat                   | sztring             | Az adóazonosító formátuma.                                                                                 |
| TaxIdSample (TaxIdSample)                   | sztring             | Az adóazonosító-minta.                                                                                 |
| ÁfaazonosítóRegex                    | sztring             | Az adóazonosító reguláris kifejezés.                                                                     |
| PhoneNumberRegex              | sztring             | A telefonszám reguláris kifejezése.                                                               |
| IsRegistrationNumberSupported | boolean            | Azt jelzi, hogy a regisztrációs szám támogatott-e.                                       |
| IsTaxIdSupported              | boolean            | Azt jelzi, hogy az adóazonosító támogatott-e. Ez eltér az IsVatIdSupported-től. |
| ResellerAgreementRegion       | sztring             | A viszonteladói szerződés régiója.                                                                     |
| GeographicRegion (Földrajzi régió régiója)              | sztring             | A földrajzi régió.                                                                             |
| CountryCallingCodesList       | sztringek tömbje   | Az ország/régió által támogatott hívókódok.                                                 |
| Attribútumok                    | ResourceAttributes (Erőforrás-attribútumok) | A CountryInformation erőforrásnak megfelelő metaadat-attribútumok.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Egy ország/régió címformázási szabályait ismerteti.

| Tulajdonság                | Típus               | Description                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | sztring             | Iso-2 kód.                                                                                     |
| DefaultCulture (Alapértelmezett culture)          | sztring             | Az alapértelmezett kulturális környezet.                                                                               |
| IsStateRequired         | boolean            | Azt jelzi, hogy szükség van-e egy államra/tartományra.                                             |
| SupportedStatesList (TámogatottstatesList)     | sztringek tömbje   | Ha szükség van egy államra/tartományra, az adott ország/régió teljes listáját adja vissza.                    |
| SupportedLanguagesList  | sztringek tömbje   | A támogatott nyelvek listája.                                                                     |
| SupportedCulturesList   | sztringek tömbje   | A támogatott kulturális világok listája.                                                                      |
| IsPostalCodeRequired    | boolean            | Azt jelzi, hogy szükség van-e irányítószámra vagy irányítószámra.                                    |
| PostalCodeRegex         | sztring             | Az irányítószámot meghatározó reguláris kifejezés.                                          |
| IsCityRequired          | boolean            | Azt jelzi, hogy szükség van-e városra.                                                       |
| IsVatIdSupported        | boolean            | Azt jelzi, hogy szükség van-e áfaazonosítóra.                                                     |
| TaxIdFormat (TaxIdFormat)             | sztring             | Az adóazonosító formátuma.                                                                                 |
| TaxIdSample             | sztring             | Az adóazonosító-minta.                                                                                 |
| ÁfaazonosítóRegex              | sztring             | Az adóazonosító reguláris kifejezés.                                                                     |
| PhoneNumberRegex        | sztring             | A telefonszám reguláris kifejezése.                                                               |
| IsTaxIdSupported        | boolean            | Azt jelzi, hogy az adóazonosító támogatott-e. Ez a tulajdonság eltér az IsVatIdSupported tulajdonságtól. |
| IsTaxIdOptional         | boolean            | Azt jelzi, hogy az adóazonosító nem kötelező-e.                                                     |
| CountryCallingCodesList | sztringek tömbje   | Az ország/régió által támogatott hívókódok.                                                 |
| Attribútumok              | ResourceAttributes (Erőforrás-attribútumok) | A CountryInformation erőforrásnak megfelelő metaadat-attribútumok.                          |
