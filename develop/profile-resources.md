---
title: Profil erőforrásai
description: Leírja a felhőalapú megoldás-szolgáltató profiljainak viselkedését.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e0561278995f4f9747320866b51de57efea8f712
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768316"
---
# <a name="profile-resources"></a>Profil erőforrásai

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Leírja a felhőalapú megoldás-szolgáltató profiljainak viselkedését.

## <a name="billingprofile"></a>BillingProfile

A partner számlázási profilját ismerteti.

| Tulajdonság            | Típus                                                           | Leírás                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| companyName         | sztring                                                         | A számlázási vállalat neve.                                   |
| address             | [Cím](utility-resources.md#address)                       | A vállalat vagy szervezet számlázási cím címe. |
| primaryContact      | [Kapcsolatfelvétel](utility-resources.md#contact)                       | A vállalat vagy szervezet elsődleges kapcsolattartója.        |
| purchaseOrderNumber | sztring                                                         | A vállalat vagy szervezet beszerzési rendelésének száma.        |
| taxIs               | sztring                                                         | A vállalat vagy szervezet adóazonosító azonosítója.                       |
| billingCurrency     | sztring                                                         | A vállalat vagy szervezet által használt pénznem.           |
| előfájltípus         | sztring                                                         | A partner profiljának típusa                                   |
| linkek               | [ResourceLinks](utility-resources.md#resourcelinks)           | A profilnak megfelelő erőforrás-hivatkozások.            |
| attribútumok          | [ResourceAttributes](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok.       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

A partner jogi üzleti profilját ismerteti.

| Tulajdonság               | Típus                                                           | Leírás                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName            | sztring                                                         | A jogi cég neve.                                                                                                                                              |
| address                | [Cím](utility-resources.md#address)                       | A vállalat vagy szervezet címe.                                                                                                                          |
| primaryContact         | [Kapcsolatfelvétel](utility-resources.md#contact)                       | A vállalat vagy szervezet elsődleges kapcsolattartója.                                                                                                                 |
| companyApproverAddress | [Cím](utility-resources.md#address)                       | A vállalat jóváhagyójának címe.                                                                                                                                        |
| companyApproverEmail   | sztring                                                         | A vállalati jóváhagyó e-mail-címe.                                                                                                                                          |
| vettingStatus          | sztring                                                         | A bevett állapot. Ez az érték a [**VettingStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus)található egyik tag nevének karakterláncos ábrázolása.           |
| vettingSubStatus       | sztring                                                         | A bevett alállapot. Ez az érték a [**VettingSubStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus)található egyik tag nevének karakterláncos ábrázolása. |
| előfájltípus            | sztring                                                         | A partner profiljának típusa                                                                                                                                            |
| linkek                  | [ResourceLinks](utility-resources.md#resourcelinks)           | A profilnak megfelelő erőforrás-hivatkozások.                                                                                                                     |
| attribútumok             | [ResourceAttributes](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok.                                                                                                                |

## <a name="mpnprofile"></a>MpnProfile

A partner Microsoft Partner Network profilját ismerteti.

| Tulajdonság    | Típus                                                           | Leírás                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | sztring                                                         | A vállalat vagy szervezet neve.                     |
| mpnId       | sztring                                                         | A Microsoft Partner Network azonosítója.                     |
| előfájltípus | sztring                                                         | A partner profiljának típusa                             |
| linkek       | [ResourceLinks](utility-resources.md#resourcelinks)           | A profilnak megfelelő erőforrás-hivatkozások.      |
| attribútumok  | [ResourceAttributes](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok. |

## <a name="organizationprofile"></a>OrganizationProfile

A partner szervezeti profilját ismerteti.

| Tulajdonság       | Típus                                                           | Leírás                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | sztring                                                         | A szervezet azonosítója.                                                 |
| companyName    | sztring                                                         | A vállalat vagy szervezet neve.                               |
| defaultAddress | [Cím](utility-resources.md#address)                       | A vállalat vagy szervezet alapértelmezett címe.                    |
| tenantId       | sztring                                                         | A bérlő azonosítója.                                                 |
| domain         | sztring                                                         | A vállalat vagy a szervezet tartománya.                                  |
| e-mail          | sztring                                                         | Lekérdezi vagy beállítja a szülő-előfizetést.                                  |
| language       | sztring                                                         | A kommunikáció előnyben részesített nyelve.                              |
| kulturális környezet        | sztring                                                         | A kommunikáció és a pénznem előnyben részesített kulturális környezete, mint például az "en-us". |
| előfájltípus    | sztring                                                         | A partner profiljának típusa                                              |
| linkek          | [ResourceLinks](utility-resources.md#resourcelinks)           | A profilnak megfelelő erőforrás-hivatkozások.                       |
| attribútumok     | [ResourceAttributes](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok.                  |

## <a name="supportprofile"></a>SupportProfile

A partner támogatási profilját ismerteti.

| Tulajdonság    | Típus                                                           | Leírás                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| e-mail       | sztring                                                         | A profilhoz társított e-mail-cím.        |
| telefonon   | sztring                                                         | A profilhoz tartozó telefonszám.         |
| Honlap     | sztring                                                         | A támogatási webhely.                                  |
| előfájltípus | sztring                                                         | A partner profiljának típusa                             |
| linkek       | [ResourceLinks](utility-resources.md#resourcelinks)           | A profilnak megfelelő erőforrás-hivatkozások.      |
| attribútumok  | [ResourceAttributes](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok. |

