---
title: Erőforrások profillal való létrehozása
description: A Felhőszolgáltató profilok viselkedését ismerteti.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8d4c091e186b7a3ad13aee7202b3d992af95db8db50acd40a5ade496d7087359
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997311"
---
# <a name="profile-resources"></a>Erőforrások profillal való létrehozása

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A Felhőszolgáltató profilok viselkedését ismerteti.

## <a name="billingprofile"></a>BillingProfile (Számlázási profil)

Egy partner számlázási profilját ismerteti.

| Tulajdonság            | Típus                                                           | Description                                                 |
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

| Tulajdonság               | Típus                                                           | Description                                                                                                                                                          |
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

| Tulajdonság    | Típus                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | sztring                                                         | A vállalat vagy szervezet neve.                     |
| mpnId       | sztring                                                         | Az Microsoft Partner Network (MPN) azonosítója.                     |
| profileType (profiltípus) | sztring                                                         | A partnerprofil típusa.                             |
| Linkek       | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | A profilnak megfelelő erőforrás-hivatkozások.      |
| Attribútumok  | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok. |

## <a name="organizationprofile"></a>OrganizationProfile (Szervezeti profilok)

Egy partner szervezeti profilját ismerteti.

| Tulajdonság       | Típus                                                           | Description                                                            |
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

Ismerteti a partner támogatási profilját.

| Tulajdonság    | Típus                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| e-mail       | sztring                                                         | A profilhoz társított e-mail-cím.        |
| Telefon   | sztring                                                         | A profilhoz társított telefonszám.         |
| Honlap     | sztring                                                         | A támogatási webhely.                                  |
| profileType (profiltípus) | sztring                                                         | A partnerprofil típusa.                             |
| Linkek       | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | A profilnak megfelelő erőforrás-hivatkozások.      |
| Attribútumok  | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok. |

