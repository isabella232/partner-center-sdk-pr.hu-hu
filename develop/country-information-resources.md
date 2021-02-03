---
title: Ország információs erőforrásai
description: Ismerje meg, hogyan használhatja a partner Center API-kat az országbeli információs erőforrásokkal és egy adott országgal vagy régióval kapcsolatos leíró metaadatokkal.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba0974cf736ff86038f8abf9c77d6a648984d1df
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768633"
---
# <a name="country-information-resources-available-from-partner-center-apis"></a>A partner Center API-k által elérhető országspecifikus információforrások

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Az alábbi erőforrások leíró metaadatokat biztosítanak egy adott országhoz vagy régióhoz.

## <a name="countryinformation"></a>CountryInformation

| Tulajdonság                      | Típus               | Leírás                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | sztring             | A bővítmények adatkészlete.                                                                                |
| Iso2Code                      | sztring             | Egy ISO-2 kód.                                                                                     |
| Iso3Code                      | sztring             | Egy ISO-3 kód.                                                                                     |
| DefaultCulture                | sztring             | Az alapértelmezett kulturális környezet.                                                                               |
| IsStateRequired               | boolean            | Azt jelzi, hogy szükség van-e egy államra/tartományra.                                             |
| SupportedStatesList           | sztringek tömbje   | Ha egy állam/megye szükséges, az adott ország/régió teljes listáját adja vissza.                    |
| SupportedLanguagesList        | sztringek tömbje   | A támogatott nyelvek listája.                                                                     |
| SupportedCulturesList         | sztringek tömbje   | A támogatott kulturális környezetek listája.                                                                      |
| IsPostalCodeRequired          | boolean            | Azt jelzi, hogy szükség van-e IRÁNYÍTÓSZÁMra vagy irányítószámra.                                    |
| PostalCodeRegex               | sztring             | Az IRÁNYÍTÓSZÁMot definiáló reguláris kifejezés.                                          |
| IsCityRequired                | boolean            | Azt jelzi, hogy szükség van-e városra.                                                       |
| IsVatIdSupported              | boolean            | Azt jelzi, hogy szükség van-e egy ÁFA-AZONOSÍTÓra.                                                     |
| TaxIdFormat                   | sztring             | Az adó-azonosító formátuma.                                                                                 |
| TaxIdSample                   | sztring             | Az adóazonosító minta.                                                                                 |
| VatIdRegex                    | sztring             | Az adó-azonosító reguláris kifejezése.                                                                     |
| PhoneNumberRegex              | sztring             | A telefonszám reguláris kifejezése.                                                               |
| IsRegistrationNumberSupported | boolean            | Azt jelzi, hogy a regisztrációs szám támogatott-e vagy sem.                                       |
| IsTaxIdSupported              | boolean            | Azt jelzi, hogy a rendszer támogatja-e az adó AZONOSÍTÓját. Ez különbözik a IsVatIdSupported. |
| ResellerAgreementRegion       | sztring             | A viszonteladói szerződés régiója.                                                                     |
| GeographicRegion              | sztring             | A földrajzi régió.                                                                             |
| CountryCallingCodesList       | sztringek tömbje   | Az országban/régióban támogatott hívási kódok.                                                 |
| Attribútumok                    | ResourceAttributes | A CountryInformation-erőforrásnak megfelelő metaadat-attribútumok.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Leírja egy ország/régió címeinek formázási szabályait.

| Tulajdonság                | Típus               | Leírás                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | sztring             | Egy ISO-2 kód.                                                                                     |
| DefaultCulture          | sztring             | Az alapértelmezett kulturális környezet.                                                                               |
| IsStateRequired         | boolean            | Azt jelzi, hogy szükség van-e egy államra/tartományra.                                             |
| SupportedStatesList     | sztringek tömbje   | Ha egy állam/megye szükséges, az adott ország/régió teljes listáját adja vissza.                    |
| SupportedLanguagesList  | sztringek tömbje   | A támogatott nyelvek listája.                                                                     |
| SupportedCulturesList   | sztringek tömbje   | A támogatott kulturális környezetek listája.                                                                      |
| IsPostalCodeRequired    | boolean            | Azt jelzi, hogy szükség van-e IRÁNYÍTÓSZÁMra vagy irányítószámra.                                    |
| PostalCodeRegex         | sztring             | Az IRÁNYÍTÓSZÁMot definiáló reguláris kifejezés.                                          |
| IsCityRequired          | boolean            | Azt jelzi, hogy szükség van-e városra.                                                       |
| IsVatIdSupported        | boolean            | Azt jelzi, hogy szükség van-e egy ÁFA-AZONOSÍTÓra.                                                     |
| TaxIdFormat             | sztring             | Az adó-azonosító formátuma.                                                                                 |
| TaxIdSample             | sztring             | Az adóazonosító minta.                                                                                 |
| VatIdRegex              | sztring             | Az adó-azonosító reguláris kifejezése.                                                                     |
| PhoneNumberRegex        | sztring             | A telefonszám reguláris kifejezése.                                                               |
| IsTaxIdSupported        | boolean            | Azt jelzi, hogy a rendszer támogatja-e az adó AZONOSÍTÓját. Ez a tulajdonság eltér a IsVatIdSupported. |
| IsTaxIdOptional         | boolean            | Azt jelzi, hogy nem kötelező-e az adó azonosítója.                                                     |
| CountryCallingCodesList | sztringek tömbje   | Az országban/régióban támogatott hívási kódok.                                                 |
| Attribútumok              | ResourceAttributes | A CountryInformation-erőforrásnak megfelelő metaadat-attribútumok.                          |
