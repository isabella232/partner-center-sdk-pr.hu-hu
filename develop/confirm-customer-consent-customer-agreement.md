---
title: Annak megerősítése, hogy az ügyfél elfogadta a Microsoft Ügyfélszerződést
description: Megtudhatja, hogyan erősítheti meg a Microsoft-ügyfél szerződését a partner Center API-k használatával.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 62a6cebd5d6d093377dd5940dcff6204b7095c70
ms.sourcegitcommit: ebb36208d6e2dea705f62b7d60d471f10c55132e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/09/2021
ms.locfileid: "100006071"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a>A Microsoft Customer-szerződés ügyfél általi elfogadásának megerősítése a partner Center API-k használatával

**A következőkre vonatkozik:**

- Partnerközpont

A partner Center jelenleg csak a Microsoft *nyilvános felhőben* támogatja a Microsoft-ügyfél szerződésének megerősítő jóváhagyását. Ez a funkció jelenleg nem érvényes a következőkre:

- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ez a cikk azt ismerteti, hogyan lehet megerősíteni vagy újból megerősíteni a Microsoft ügyfél-szerződését.

## <a name="prerequisites"></a>Előfeltételek

- Ha a partner Center .NET SDK-t használja, a 1,14-es vagy újabb verzió szükséges.

- A [partner Center-hitelesítésben](./partner-center-authentication.md)leírt hitelesítő adatok. *Ez a forgatókönyv csak az App + felhasználói hitelesítést támogatja.*

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- A dátum (**dateAgreed**), amikor az ügyfél elfogadta a Microsoft ügyfél-szerződést.

- A Microsoft ügyfél-szerződését elfogadó ügyfélről szóló információ. Ide tartoznak az alábbiak:
  - Utónév
  - Vezetéknév
  - E-mail-cím
  - Telefonszám (nem kötelező)
- Ha az ügyfélen a következő értékek változnak, a partneri központ lehetővé teszi, hogy egy másik szerződést hozzon létre az adott ügyfél számára: Utónév vezetékneve e-mail-cím telefonszáma, máskülönben a partnerek a következő hibakódot kapják meg az ismétlődő ügyfél létrehozása miatt


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

A Microsoft ügyfél-szerződés elfogadásának megerősítése vagy újbóli megerősítése:

1. Kérje le a Microsoft Customer szerződéshez tartozó szerződési metaadatokat. Be kell szereznie a Microsoft Customer szerződés **templateId** . További részletekért lásd: [a szerződés metaadatainak beszerzése a Microsoft ügyfél-szerződéshez](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Hozzon létre egy új **Szerződés** objektumot, amely tartalmazza a megerősítés részleteit.

3. Használja a **IAgreggatePartner. Customs** gyűjteményt, és hívja meg a **ById** metódust a megadott **ügyfél-bérlő-azonosítóval**.

4. Használja a **szerződések** tulajdonságot, amelyet a **create** vagy a **CreateAsync** hívása követ.

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

Teljes minta a [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) osztályban található a [konzol tesztelése alkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektben.

## <a name="rest-request"></a>REST-kérelem

A Microsoft ügyfél-szerződés elfogadásának megerősítése vagy újbóli megerősítése:

1. Kérje le a Microsoft Customer szerződéshez tartozó szerződési metaadatokat. Be kell szereznie a Microsoft Customer szerződés **templateId** . További részletekért lásd: [a szerződés metaadatainak beszerzése a Microsoft ügyfél-szerződéshez](get-customer-agreement-metadata.md).

2. Hozzon létre egy új [ **szerződési** erőforrást](agreement-resources.md) annak megerősítéséhez, hogy az ügyfél elfogadta a Microsoft ügyfél-szerződést. Használja az alábbi [Rest-kérelem szintaxisát](#request-syntax).

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus | Kérés URI-ja                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements http/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

A következő lekérdezési paraméterrel adhatja meg a megerősítő ügyfelet.

| Név               | Típus | Kötelező | Leírás                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| ügyfél – bérlő – azonosító | GUID | Igen | Az érték egy GUID-formátumú **ügyfél-bérlői azonosító**, amely egy ügyfél megadását lehetővé tevő azonosító. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a REST-kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.

| Név      | Típus   | Description                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| Megállapodás | object | A partner által biztosított részletek a Microsoft ügyfél-szerződésének megerősítő elfogadásának megerősítéséhez. |

#### <a name="agreement"></a>Megállapodás

Ez a táblázat a [ **szerződési** erőforrások](agreement-resources.md)létrehozásához szükséges minimális mezőket ismerteti.

| Tulajdonság       | Típus   | Description                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Kapcsolatfelvétel](./utility-resources.md#contact) | Információk a Microsoft ügyfél-szerződést elfogadó, a  **firstName**, a **lastName**, az **e-mail** és a **telefonszám** (nem kötelező) felhasználóról |
| dateAgreed     | karakterlánc UTC-dátum időformátuma |Az a dátum, amikor az ügyfél elfogadta a szerződést. |
| templateId     | sztring | Az ügyfél által elfogadott szerződés típusának egyedi azonosítója. A Microsoft ügyfél-szerződéshez tartozó **templateId** beszerezheti a Microsoft-szerződés metaadatainak beolvasásával. További részletekért lásd: a [Szerződés metaadatainak beszerzése a Microsoft Customer szerződéshez](./get-customer-agreement-metadata.md) . |
| típus           | sztring | Az ügyfél által elfogadott szerződés típusa. Ha az ügyfél elfogadta a Microsoft Customer szerződést, használja a "MicrosoftCustomerAgreement" lehetőséget. |

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

Ha ez sikeres, ez a metódus egy [ **Szerződés** -erőforrást](./agreement-resources.md)ad vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.

A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

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
