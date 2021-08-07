---
title: Indirect Reseller létrehozása tesztkörnyezetben
description: Információkat nyújt a tesztbox közvetett szolgáltatói számára a végpontok közötti tesztelés API-k használatával való engedélyezéséről.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 970b7ba49f6bb4b842f0f7d96e689856b0362c03949e14c9cf5a0e205573277b
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991446"
---
# <a name="create-indirect-reseller-in-sandbox"></a>Indirect Reseller létrehozása tesztkörnyezetben

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Németországhoz

Ez a dokumentum bemutatja, hogyan hozhat létre közvetett tesztkészlet-szolgáltatókat, és hogyan engedélyezheti a végpontok közötti tesztelést API-k használatával.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.

## <a name="csp-indirect-provider"></a>CSP – Közvetett szolgáltató

| Éles képességek             | A sandbox képességei                            |
|-------------------------------------|-------------------------------------------------|
| Értékesítés a közvetett viszonteladón keresztül a végfelhasználónak | Támogatott |
| Az összes értékesítés, számlázás, kiépítés és felügyelet/támogatás tulajdonában van | Támogatott |
| Partnerkapcsolat kérése a viszonteladóktól | Támogatott |
| Ügyfelek megtekintése viszonteladó szerint | Támogatott |
| Új ügyfelek hozzáadása viszonteladók szerint | Támogatott |
| Ügyfelek meghívása | Az ügyfélkapcsolati kérés nem támogatott a sandboxban |
| A sandbox indirect provider (Sandbox Indirect Provider) kiválaszthatja a Sandbox IR (MPN ID) (Sandbox IR ( MPN-azonosító) lehetőséget a POR-ként a tranzakció elhelyezésekor | Támogatott |
| Éles környezetben nem támogatott | A sandbox indirect provider (Közvetett sandbox-szolgáltató) közvetett viszonteladót hozhat létre |
| A sandbox MPN-azonosítót meg kell adni, a termék MPN-azonosítója nem fog működni | Éles környezetben nem támogatott |
| Éles környezetben nem támogatott | A közvetett sandbox-szolgáltató törölheti a közvetett viszonteladót |

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller"></a>Közvetett sandbox szolgáltató – Közvetett viszonteladó létrehozása a sandboxban

Ez a funkció csak a Sandboxban érhető el, és lehetővé teszi, hogy közvetett viszonteladókat hozzon létre a Sandbox indirect Providers (Közvetett viszonteladók) számára.

1. A közvetett viszonteladók által engedélyezett öt közvetett viszonteladóra vonatkozó korlát a közvetett sandbox szolgáltatónként
2. A közvetett sandbox-szolgáltatók közvetett viszonteladókkal `associatedPartnerId` hozhatnak létre ügyfeleket
3. Adja meg [egy adott régió MPN-azonosítóját](/partner-center/mpn-create-a-partner-center-account) egy közvetett viszonteladó létrehozása során. Több közvetett viszonteladó is létre lehet hozva ugyanazokkal a sandbox MPN-azonosítóval.
4. Közvetett sandbox-szolgáltatónként csak 75 ügyfél engedélyezett

## <a name="sandbox-indirect-resellers--view-customers"></a>Sandbox Indirect Resellers ( Közvetett viszonteladók – Ügyfelek megtekintése)

1. A Sandbox Indirect Resellers (A közvetett sandbox-viszonteladók) megtekinthetik a sandbox-ügyfelek listáját közvetett sandbox-szolgáltatók szerint.
2. A közvetett sandbox-viszonteladók delegált rendszergazdai engedélyekkel kezelhetik az ügyfélfiókot.

## <a name="create-sandbox-indirect-reseller-through-api"></a>Sandbox Indirect Reseller létrehozása API-n keresztül

### <a name="rest-request"></a>REST-kérés

#### <a name="request-syntax"></a>Kérésszintaxis

| **Metódus** | **Kérés URI-ja**                                                        |
|------------|------------------------------------------------------------------------|
| **Post**   | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller |

#### <a name="request-headers"></a>Kérésfejlécek

- Ez az API idempotent (nem ad vissza más eredményt, ha többször is meghívja).
- Szükség van egy kérésazonosítóra és egy korrelációs azonosítóra.
- További információ: [REST Partnerközpont fejlécek.](headers.md)

#### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.

| Tulajdonság             | Típus           | Description                                      |
|----------------------|----------------|--------------------------------------------------|
| mpnId                | sztring         | Az integrációs integrációs csomag MPN-azonosítója egy adott régióban         |
| Bérlő               | &lt;Szótárszavak, sztringek&gt; | A létrehozni szükséges fiókot definiáló alapvető információk gyűjteménye |
| legalBusinessProfile | &lt;Szótárszavak, sztringek&gt; | A jogi személynek (például kapcsolattartónak, címnek és névnek) megfelelő adatok gyűjteménye |
| organizationProfileLanguage | &lt;Szótárszavak, sztringek&gt; | A szervezet nyelvazonosítója |

Ez a táblázat a bérlői attribútumban szükséges **tulajdonságokat ismerteti.**

| Tulajdonság           | Típus           | Description                         |
|--------------------|----------------|-------------------------------------|
| domainPrefix (tartomány előtagja)       | Sztring; Egyedi | A bérlőfiók tartománya       |
| name               | sztring         | A bérlő rövid neve         |
| displayName        | sztring         | A fiók megjelenítendő neve        |
| adminUserName      | sztring         | A bejelentkezéshez használt fiók felhasználóneve |
| adminfirstname     | sztring         | A rendszergazdai felhasználó vezetékneve       |
| adminlastname (rendszergazdailastname)      | sztring         | A rendszergazdai felhasználó vezetékneve        |
| adminAle fiókemail | sztring         | e-mail a rendszergazdai felhasználónak            |
| ország            | sztring         | A fiók országa              |
| Kultúra            | sztring         | A fiók nyelvi beállítása     |

Ez a táblázat a **legalBusinessProfile** attribútumban szükséges tulajdonságokat ismerteti.

| Tulajdonság       | Típus                             | Description                          |
|----------------|----------------------------------|--------------------------------------|
| companyName (vállalat neve)    | sztring                           | Jogi személy vállalatneve        |
| address        | &lt;Szótárszavak, sztringek&gt; | A jogi személy helyének címe |
| primaryContact (elsődleges tranzakció) | &lt;Szótárszavak, sztringek&gt; | A vállalat kapcsolattartási adatai       |
| Kultúra        | sztring                           | A vállalat által előnyben részesített nyelv    |

### <a name="request-example"></a>Példa kérésre

```http
{
    "mpnId": "6363276",
    "tenant": {
        "domainPrefix": "TipIRIntTest705",
        "name": "TipIRIntTest705",
        "displayName": "TipIRIntTest705",
        "adminUserName": "admin",
        "adminFirstName": "TipIRIntTest705",
        "adminLastName": "TipIRIntTest705",
        "adminAlternateEmail": "TipIRIntTest705@test.com",
        "country": "US",
        "culture": "en-us"
    },
    "legalBusinessProfile": {
        "companyName": "TipIRIntTest705",
        "address": {
            "country": "FR",
            "city": "Issy-les-Moulineaux",
            "state": "",
            "addressLine1": "39-41 quai du Président Roosevelt",
            "addressLine2": "",
            "postalCode": "92130"
        },
        "primaryContact": {
            "firstName": "Sandbox",
            "lastName": "Scenario",
            "email": "Sandbox.Scenario@test.com",
            "phoneNumber": "1234567890"
        },
        "culture": "en-US"
    },
    "organizationProfileLanguage": "en"
}
```

### <a name="rest-response"></a>REST-válasz

Ha ez a módszer sikeres, a válasz törzsében adja vissza a sandbox ir-erőforrást.

```http
{

    "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
    "mpnId": "6363276",
    "tenant": {
        "id": "6f94b119-793c-44c7-862b-c327c9057eab",
        "adminUserAccount": "admin@TipIRIntTest705.onmicrosoft.com",
        "password": "\*\*\*\*\*\*”
    },
    "agreementSignature": {
        "id": "30ac23e7-e200-42cf-a5bc-dd9148cdc632",
        "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
        "agreementId": "1e18c5b2-e42a-4b84-82c8-d0155aa94c6e",
        "agreementType": "ValueAddedReseller",
        "dateSigned": "2021-02-23T18:10:14.8461137Z",
        "signedByFirstName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserPrincipalName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserObjectId": "e6e0c29d-acda-4ef2-b370-d37a4e06fb98",
        "signedByUserTenantId": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "attributes": {
            "objectType": "AgreementSignatureResponse"
        }
    },
    "partnerRelationship": {
        "id": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "name": "PLAMUATT2NetNew",
        "relationshipType": "is\_indirect\_reseller\_of",
        "state": "Active",
        "mpnId": "6363276",
        "attributes": {
            "objectType": "PartnerRelationshipResponse"
        }
    }
}
```
