---
title: Erőforrások profillal való létrehozása
description: A Felhőszolgáltató profilok viselkedését ismerteti.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 945cfa141d1e6bde1709da882a177daaa32fba1f
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547784"
---
# <a name="profile-resources"></a>Erőforrások profillal való létrehozása

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A Felhőszolgáltató profilok viselkedését ismerteti.

## <a name="billingprofile"></a>BillingProfile (Számlázási profil)

Egy partner számlázási profilját ismerteti.

| Tulajdonság            | Típus                                                           | Leírás                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| companyName (vállalat neve)         | sztring                                                         | A számlázási vállalat neve.                                   |
| address             | [Cím](utility-resources.md#address)                       | A vállalat vagy szervezet számlázási címe. |
| primaryContact (elsődleges tranzakció)      | [Kapcsolatfelvétel](utility-resources.md#contact)                       | A vállalat vagy szervezet elsődleges kapcsolattartója.        |
| purchaseOrderNumber | sztring                                                         | A vállalat vagy szervezet rendelési száma.        |
| taxId (adóazonosító)               | sztring                                                         | A vállalat vagy szervezet adóazonosítója.                       |
| billingCurrency     | sztring                                                         | A vállalat vagy szervezet által használt pénznem.           |
| profileType (profiltípus)         | sztring                                                         | A partnerprofil típusa.                                   |
| Linkek               | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | A profilnak megfelelő erőforrás-hivatkozások.            |
| Attribútumok          | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok.       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

Ismerteti a partner jogi üzleti profilját.

| Tulajdonság               | Típus                                                           | Leírás                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName (vállalat neve)            | sztring                                                         | A jogi vállalat neve.                                                                                                                                              |
| address                | [Cím](utility-resources.md#address)                       | A vállalat vagy szervezet címe.                                                                                                                          |
| primaryContact (elsődleges tranzakció)         | [Kapcsolatfelvétel](utility-resources.md#contact)                       | A vállalat vagy szervezet elsődleges kapcsolattartója.                                                                                                                 |
| companyApproverAddress | [Cím](utility-resources.md#address)                       | A cég jóváhagyó címe.                                                                                                                                        |
| companyApproverEmail   | sztring                                                         | A cég jóváhagyó e-mail-címe.                                                                                                                                          |
| átvizsgálásÁllapot          | sztring                                                         | A átvizsgálás állapota. Ez az érték a [**VettingStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus)fájlban található tagnevek egyikének sztringes ábrázolása.           |
| átvizsgálásSubStatus       | sztring                                                         | A átvizsgálás alállapota. Ez az érték a [**VettingSubStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus)fájlban található tagnevek egyikének sztringes ábrázolása. |
| profileType (profiltípus)            | sztring                                                         | A partnerprofil típusa.                                                                                                                                            |
| Linkek                  | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | A profilnak megfelelő erőforrás-hivatkozások.                                                                                                                     |
| Attribútumok             | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok.                                                                                                                |

## <a name="mpnprofile"></a>MpnProfile

Ismerteti a partner Microsoft Partner Network profilját.

| Tulajdonság    | Típus                                                           | Leírás                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | sztring                                                         | A vállalat vagy szervezet neve.                     |
| mpnId       | sztring                                                         | Az Microsoft Partner Network (MPN) azonosítója.                     |
| profileType (profiltípus) | sztring                                                         | A partnerprofil típusa.                             |
| Linkek       | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | A profilnak megfelelő erőforrás-hivatkozások.      |
| Attribútumok  | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok. |

## <a name="organizationprofile"></a>OrganizationProfile (Szervezeti profilok)

Egy partner szervezeti profilját ismerteti.

| Tulajdonság       | Típus                                                           | Leírás                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | sztring                                                         | A szervezet azonosítója.                                                 |
| companyName (vállalat neve)    | sztring                                                         | A vállalat vagy szervezet neve.                               |
| defaultAddress (alapértelmezett cím) | [Cím](utility-resources.md#address)                       | A vállalat vagy szervezet alapértelmezett címe.                    |
| tenantId (bérlőazonosító)       | sztring                                                         | A bérlő azonosítója.                                                 |
| domain         | sztring                                                         | A vállalat vagy szervezet tartománya.                                  |
| e-mail          | sztring                                                         | Lekérte vagy beállítja a szülő-előfizetést.                                  |
| language       | sztring                                                         | A kommunikáció előnyben részesített nyelve.                              |
| Kultúra        | sztring                                                         | A kommunikáció és a pénznem előnyben részesített kultúrája, például "en-us". |
| profileType (profiltípus)    | sztring                                                         | A partnerprofil típusa.                                              |
| Linkek          | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | A profilnak megfelelő erőforrás-hivatkozások.                       |
| Attribútumok     | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok.                  |

## <a name="supportprofile"></a>Támogatásiprofil

Egy partner támogatási profilját ismerteti.

| Tulajdonság    | Típus                                                           | Leírás                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| e-mail       | sztring                                                         | A profilhoz társított e-mail-cím.        |
| Telefon   | sztring                                                         | A profilhoz társított telefonszám.         |
| Honlap     | sztring                                                         | A támogatási webhely.                                  |
| profileType (profiltípus) | sztring                                                         | A partnerprofil típusa.                             |
| Linkek       | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | A profilnak megfelelő erőforrás-hivatkozások.      |
| Attribútumok  | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok. |

