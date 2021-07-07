---
title: Annak megerősítése, hogy az ügyfél elfogadta a Microsoft Ügyfélszerződést
description: Megtudhatja, hogyan erősítheti meg az ügyfelek számára a Microsoft Ügyfélszerződés API Partnerközpont használatával.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 002508109191ede53cd06f25efc38286647fd67c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974012"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a>Az ügyfél általi elfogadás megerősítése Microsoft Ügyfélszerződés API Partnerközpont használatával

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Partnerközpont jelenleg csak a Microsoft nyilvános felhőben támogatja a Microsoft Ügyfélszerződés ügyfél általi elfogadásának megerősítését.

Ez a cikk azt ismerteti, hogyan lehet megerősíteni vagy újra megerősíteni az ügyfél általi Microsoft Ügyfélszerződés.

## <a name="prerequisites"></a>Előfeltételek

- Ha az Partnerközpont .NET SDK-t használja, 1.14-es vagy újabb verzió szükséges.

- Az Partnerközpont [ismertetett hitelesítő adatok.](./partner-center-authentication.md) *Ez a forgatókönyv csak az alkalmazás- és felhasználóhitelesítést támogatja.*

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Az a **dátum (dateAgreed**), amikor az ügyfél elfogadta a Microsoft Ügyfélszerződés.

- Információ az ügyfélszervezettől származó felhasználóról, amely elfogadta a Microsoft Ügyfélszerződés. Ide tartoznak az alábbiak:
  - Utónév
  - Vezetéknév
  - E-mail-cím
  - Telefon száma (nem kötelező)
- Ha egy ügyfélnél az alábbi értékek változnak, a Partnerközpont lehetővé teszi egy másik szerződés létrejöttét az ügyfél számára: Vezetéknév vezetéknév e-mail-címe Telefon szám. Ellenkező esetben a partnerek a következő hibakódot kapják meg egy duplikált ügyfél létrehozása miatt


```
{
"code": 600061,
"message": "A partner confirmed agreement already exists for the customer.",
"description": "A partner confirmed agreement already exists for the customer.",
"errorName": "PartnerConfirmedAgreementAlreadyExists",
"isRetryable": false,
"parameters": {},
"errorMessageExtended": "InternalErrorCode=600061"
}
 ```

## <a name="net"></a>.NET

A következő feltételek ügyfél általi elfogadásának megerősítése vagy Microsoft Ügyfélszerződés:

1. A szerződés metaadatainak lekérése a Microsoft Ügyfélszerződés. Be kell szereznie a **sablonazonosítót** a Microsoft Ügyfélszerződés. További információkért lásd a [szerződés metaadatainak lekért Microsoft Ügyfélszerződés.](get-customer-agreement-metadata.md)

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Hozzon létre egy új **Szerződés** objektumot, amely a megerősítés részleteit tartalmazza.

3. Használja az **IAgreggatePartner.Customers** gyűjteményt, és hívja meg a **ById** metódust a megadott **ügyfél-bérlő-azonosítóval.**

4. Használja a **Agreements tulajdonságot,** majd hívja meg a **Create** vagy **a CreateAsync metódust.**

   ```csharp
   // string selectedCustomerId;

   var agreementToCreate = new Agreement
   {
       DateAgreed = DateTime.UtcNow,
       TemplateId = microsoftCustomerAgreementDetails.TemplateId,
       PrimaryContact = new Contact
       {
           FirstName = "Tania",
           LastName = "Carr",
           Email = "someone@example.com",
           PhoneNumber = "1234567890"
       }
   };

   Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
   ```

A teljes minta a [CreateCustomerAgreement osztályban](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) található a konzol [tesztalkalmazás-projektből.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="rest-request"></a>REST-kérés

A következő feltételek ügyfél általi elfogadásának megerősítése vagy Microsoft Ügyfélszerződés:

1. A szerződés metaadatainak lekérése a Microsoft Ügyfélszerződés. Be kell szereznie a **sablonazonosítót** a Microsoft Ügyfélszerződés. További információkért lásd a [szerződés metaadatainak lekért Microsoft Ügyfélszerződés.](get-customer-agreement-metadata.md)

2. Hozzon létre egy új [ **Szerződés** erőforrást](agreement-resources.md) annak megerősítéséhez, hogy az ügyfél elfogadta a Microsoft Ügyfélszerződés. Használja a [következő REST-kérési szintaxist:](#request-syntax).

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus | Kérés URI-ja                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

A következő lekérdezési paraméterrel adhatja meg azt az ügyfelet, akiről megerősítést ad.

| Név               | Típus | Kötelező | Leírás                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| ügyfél-bérlő-azonosító | GUID | Igen | Az érték egy GUID-formátumú **ügyfél-bérlő-azonosító,** amely egy olyan azonosító, amellyel megadhatja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a REST-kérelem törzsében szükséges tulajdonságokat ismerteti.

| Név      | Típus   | Leírás                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| Megállapodás | object | A partner által a feltételek ügyfél általi elfogadásának megerősítéséhez megadott Microsoft Ügyfélszerződés. |

#### <a name="agreement"></a>Megállapodás

Ez a táblázat a szerződéserőforrás létrehozásához minimálisan szükséges [ **mezőket** ismerteti.](agreement-resources.md)

| Tulajdonság       | Típus   | Leírás                              |
|----------------|--------|------------------------------------------|
| primaryContact (elsődleges tranzakció) | [Kapcsolatfelvétel](./utility-resources.md#contact) | A felhasználóval kapcsolatos információk az ügyfélszervezettől, amely elfogadta a Microsoft Ügyfélszerződés, beleértve a  **következőket: firstName,** **lastName,** **e-mail,** és **phoneNumber** (nem kötelező) |
| dateAgreed (dátum dátuma)     | sztring UTC dátum-idő formátumban |Az a dátum, amikor az ügyfél elfogadta a szerződést. |
| templateId (sablonazonosító)     | sztring | Az ügyfél által elfogadott szerződéstípus egyedi azonosítója. A sablon  sablonazonosítóját úgy szerezheti be Microsoft Ügyfélszerződés hogy lekérte a szerződés metaadatait a Microsoft Ügyfélszerződés. A részletekért tekintse meg a szerződés [metaadatainak le Microsoft Ügyfélszerződés](./get-customer-agreement-metadata.md) kapcsolatos információkat. |
| típus           | sztring | Az ügyfél által elfogadott szerződéstípus. Ha az ügyfél elfogadta a Microsoft Ügyfélszerződés, használja a "MicrosoftCustomerAgreement" Microsoft Ügyfélszerződés. |

#### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus egy [ **szerződéserőforrást ad** vissza.](./agreement-resources.md)

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.

Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

#### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
