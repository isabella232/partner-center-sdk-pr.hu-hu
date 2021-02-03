---
title: Felhasználói erőforrások
description: Ügyfelet vagy viszonteladót képviselő ügyfelek erőforrásai.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: fbd72ab5710876ba303fd1e30e6e552ecf89c5cd
ms.sourcegitcommit: 741cfa8585901de207c2e5da5eeebe26db0b0ad1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/18/2020
ms.locfileid: "97768572"
---
# <a name="customer-resources"></a>Felhasználói erőforrások

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

## <a name="customer"></a>Ügyfél

Az **ügyfél** -erőforrás egy ügyfelet vagy viszonteladót jelöl. A legszélesebb körben az ügyfél-erőforrás olyan személy, alkalmazott vagy szervezet, aki üzleti tevékenységet kíván végezni a Microsofttal és a Microsoft viszonteladókkal. Az ügyfeleknek emellett a vállalati profillal és a számlázási profillal is rendelkeznek.

>[!NOTE]
>Az **ügyfél** -erőforráshoz a bérlői azonosítók száma percenként 500 kérelem.

| Tulajdonság              | Típus                                                             | Leírás                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | sztring                                                           | Az ügyfél-azonosító.                                                                                                                             |
| commerceId            | sztring                                                           | A kereskedelmi azonosító.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | További információ a vállalatról vagy szervezetről.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | További információ a számlázáshoz.                                                                                                     |
| relationshipToPartner | sztring                                                           | Meghatározza azt a licencelési programot, amelyet a partner használ ehhez az ügyfélhez: "None", "viszonteladó", "Advisor", "hírszolgáltatás" vagy "Microsoft \_ support". |
| allowDelegatedAccess  | boolean                                                          | Azt határozza meg, hogy a partner delegált rendszergazdai jogosultságokat kapott-e az ügyféltől. Ez a tulajdonság csak akkor érhető el, ha az ügyfél azonosító alapján, nem lista szerint van beolvasva.                                                         |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | A felhasználó hitelesítő adatai.                                                                                                                        |
| customDomains         | sztringek tömbje                                                 | Az ügyfél egyéni tartományának listája.                                                                                                        |
| associatedPartnerId   | sztring                                                           | Az ügyfél-fiókhoz társított közvetett viszonteladó. Ez az érték csak közvetett CSP-partnerek számára állítható be.                              |
| linkek                 | [ResourceLinks](utility-resources.md#resourcelinks)             | A profilban található erőforrás-hivatkozások.                                                                                             |
| attribútumok            | [ResourceAttributes](utility-resources.md#resourceattributes)   | A profilnak megfelelő metaadat-attribútumok.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

A **CustomerCompanyProfile** -erőforrás a vállalattal vagy szervezettel kapcsolatos további információk.

| Tulajdonság    | Típus                                                           | Leírás                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | sztring                                                         | Az ügyfél bérlői azonosítója az Azure AD-hez. Ezt nevezik MicrosoftID is. |
| domain      | sztring                                                         | Az ügyfél neve, például contoso.onmicrosoft.com.                             |
| companyName | sztring                                                         | A vállalat vagy szervezet neve.                                          |
| linkek       | [ResourceLinks](utility-resources.md#resourcelinks)           | A profilban található erőforrás-hivatkozások.                                  |
| attribútumok  | [ResourceAttributes](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok.                             |

| organizationRegistrationNumber | Karakterlánc | Az ügyfél szervezetének regisztrációs száma (más néven az INN száma bizonyos országokban). Csak a következő országokban található ügyfél vállalata/szervezete számára szükséges. Örményország (AM), Azerbajdzsán (AZ), Fehéroroszország (BY), Magyarország (HU), Kazahsztán (KZ), Kirgizisztán (KG), Moldova (MD), Oroszország (RU), Tádzsikisztán (TJ), Üzbegisztán (UZ), Ukrajna (UA). Az ügyfél más országokban található vállalata/szervezete számára nem adható meg. |


## <a name="customerbillingprofile"></a>CustomerBillingProfile

A **CustomerBillingProfile** -erőforrás az ügyfél számlázására szolgáló további információ.

| Tulajdonság       | Típus                                                           | Leírás                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | sztring                                                         | A profil azonosítója.                                                                                                                                |
| firstName      | sztring                                                         | Az ügyfél vállalatának számlázási kapcsolatának utóneve. Ez az a személy, aki a számlákat és egyéb számlázási kommunikációt irányítja. |
| lastName       | sztring                                                         | A számlázási kapcsolat vezetékneve.                                                                                                                  |
| e-mail          | sztring                                                         | A számlázási partner e-mail-címe                                                                                                                    |
| kulturális környezet        | sztring                                                         | Az előnyben részesített kulturális környezet a kommunikációhoz és a pénznemhez, mint például az "en-us".                                                                               |
| language       | sztring                                                         | Az előnyben részesített nyelv a kommunikációhoz.                                                                                                            |
| companyName    | sztring                                                         | A vállalat vagy szervezet neve.                                                                                                               |
| defaultAddress | [Cím](utility-resources.md#address)                       | Az a cím, amelyet a számlák küldenek, ahol a számlázási kapcsolat működik.                                                                                   |
| linkek          | [ResourceLinks](utility-resources.md#resourcelinks)           | A profilban található erőforrás-hivatkozások.                                                                                                       |
| attribútumok     | [ResourceAttributes](utility-resources.md#resourceattributes) | A profilnak megfelelő metaadat-attribútumok.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

A **CustomerRelationshipRequest** -erőforrás tartalmazza azt az URL-címet, amelyet az ügyfél a viszonteladói kapcsolat létrehozásához használ a partnerrel.

| Tulajdonság   | Típus                                                           | Leírás                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | sztring                                                         | Az ügyfél által a partnerrel létesített kapcsolat létesítéséhez használt URL-cím. |
| attribútumok | [ResourceAttributes](utility-resources.md#resourceattributes) | A kapcsolati kérelemhez tartozó metaadat-attribútumok.       |