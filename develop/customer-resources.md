---
title: Ügyfélerőforrások
description: Ügyfél-erőforrások, amelyek egy ügyfelet vagy viszonteladót képviselnek.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 7d76de33c9a0d28e9d3fb0b0821cbd37ad67e7af
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973145"
---
# <a name="customer-resources"></a>Ügyfélerőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

## <a name="customer"></a>Ügyfél

Az **Ügyfél** erőforrás egy ügyfelet vagy viszonteladót képvisel. Az ügyfélerőforrás általában bármely olyan személy, alkalmazott vagy szervezet lehet, aki a Microsoft és a Microsoft viszonteladói között szeretne üzleti vállalkozást. Az ügyfelek emellett vállalati profillal és számlázási profillal is.

>[!NOTE]
>Az **Ügyfél** erőforrás sebességkorlátja bérlőazonosítónként percenként 500 kérés.

| Tulajdonság              | Típus                                                             | Leírás                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | sztring                                                           | Az ügyfél azonosítója.                                                                                                                             |
| commerceId (kereskedelmiazonosító)            | sztring                                                           | A kereskedelmi azonosító.                                                                                                                             |
| companyProfile (vállalatiprofil)        | [CustomerCompanyProfile (Ügyfél cégesprofil)](#customercompanyprofile)                | További információk a vállalatról vagy szervezetről.                                                                                    |
| billingProfile (számlázási profil)        | [CustomerBillingProfile](#customerbillingprofile)                | A számlázáshoz használt további információk.                                                                                                     |
| relationshipToPartner (partnerkapcsolat) | sztring                                                           | Meghatározza a partner által az ügyfélhez használt licencprogramot: "none", "reseller", "advisor", "syndication" vagy "microsoft \_ support". |
| allowDelegatedAccess  | boolean                                                          | Jelzi, hogy a partner kapott-e delegált rendszergazdai jogosultságokat az ügyféltől. Ez a tulajdonság csak akkor érhető el, ha az ügyfél azonosító alapján van lekért, nem lista alapján.                                                         |
| userCredentials (userCredentials)       | [UserCredentials (Felhasználói adatok)](user-resources.md#usercredentials) | A felhasználói hitelesítő adatok.                                                                                                                        |
| customDomains (egyéni tartomány)         | sztringek tömbje                                                 | Egy ügyfél egyéni tartományának listája.                                                                                                        |
| associatedPartnerId (társított partnerazonosító)   | sztring                                                           | Az ügyfélfiókhoz társított közvetett viszonteladó. Ezt az értéket csak közvetett CSP-partnerek állíthatják be.                              |
| Linkek                 | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)             | A profilban található erőforrás-hivatkozások.                                                                                             |
| Attribútumok            | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)   | A profilnak megfelelő metaadat-attribútumok.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile (Ügyfél cégesprofil)

A **CustomerCompanyProfile** erőforrás további információkat tartalmaz a vállalatról vagy szervezetről.

| Tulajdonság    | Típus                                                           | Leírás                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId (bérlőazonosító)    | sztring                                                         | Az ügyfél Azure AD-bérlőazonosítója. Ezt MicrosoftID-nek is nevezik. |
| domain      | sztring                                                         | Az ügyfél neve, például contoso.onmicrosoft.com.                             |
| companyName (vállalat neve) | sztring                                                         | A vállalat vagy szervezet neve.                                          |
| Linkek       | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | A profilban található erőforrás-hivatkozások.                                  |
| Attribútumok  | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok.                             |
|organizationRegistrationNumber|Sztring|Az ügyfél szervezeti regisztrációs száma (más néven INN-szám bizonyos országokban). Csak a következő országokban található ügyfél cégéhez/szervezetéhez szükséges: Egyesült Államok( AM), Uzbekistan(AZ), Inc(BY), Fogja(HU), Torgyzstan (KZ), Kyrgyzstan(KG), Fog(MD), Oroszország(RU), Tajikistan(TJ), Uzbekistan(UZ), Ova(UA), India, Brazília, Dél-Afrikai Köztársaság, Egyesült Arab Emírségek, Egyesült Arab Emírségek, Észak-Karolina, Észak-Karolina, Dél-Afrikai Köztársaság és Dél-Korea. Az ügyfél más országokban található vállalata/szervezete esetében ezt nem szabad megadni.|


## <a name="customerbillingprofile"></a>CustomerBillingProfile

A **CustomerBillingProfile erőforrás** az ügyfél számlázására használt további információ.

| Tulajdonság       | Típus                                                           | Leírás                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | sztring                                                         | A profilazonosító.                                                                                                                                |
| firstName      | sztring                                                         | Az ügyfél vállalatának számlázási kapcsolattartója vezetékneve. Ez az a személy, akihez a számlák és egyéb számlázási kommunikációk lesznek irányítva. |
| lastName       | sztring                                                         | A számlázási kapcsolattartó vezetékneve.                                                                                                                  |
| e-mail          | sztring                                                         | A számlázási kapcsolattartó e-mail-címe                                                                                                                    |
| Kultúra        | sztring                                                         | A kommunikáció és a pénznem előnyben részesített kultúrája, például "en-us".                                                                               |
| language       | sztring                                                         | Az előnyben részesített kommunikációs nyelv.                                                                                                            |
| companyName (vállalat neve)    | sztring                                                         | A vállalat vagy szervezet neve.                                                                                                               |
| defaultAddress (alapértelmezett cím) | [Cím](utility-resources.md#address)                       | A számlázó cím, ahová a számlázási kapcsolattartó működik.                                                                                   |
| Linkek          | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | A profilban található erőforrás-hivatkozások.                                                                                                       |
| Attribútumok     | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

A **CustomerRelationshipRequest** erőforrás tartalmazza azt az URL-címet, amelyet az ügyfél a partnerrel való viszonteladói kapcsolat létesítéhez használ.

| Tulajdonság   | Típus                                                           | Leírás                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | sztring                                                         | Az ügyfél által a partnerrel való kapcsolat létesítéhez használt URL-cím. |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A kapcsolatkéréshez tartozó metaadat-attribútumok.       |