---
title: A Microsoft Ügyfélszerződés ügyfél általi elfogadási megerősítésének lekérése
description: Ez a cikk azt ismerteti, hogyan lehet megerősíteni a Microsoft ügyfél-szerződés elfogadását.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 55f63311e7bb1857fdc6c4b3d68446674542ba98
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768167"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>A Microsoft Ügyfélszerződés ügyfél általi elfogadási megerősítésének lekérése

**A következőkre vonatkozik:**

- Partnerközpont

A partner Center jelenleg csak a *Microsoft nyilvános felhőben* támogatja a **szerződési** erőforrást. Ez az erőforrás nem vonatkozik a következőkre:

- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ez a cikk azt ismerteti, hogyan kérhető le a Microsoft ügyfél-szerződés elfogadásának megerősítése (i).

## <a name="prerequisites"></a>Előfeltételek

- Ha a partner Center .NET SDK-t használja, a 1,14-es vagy újabb verzió szükséges.

- A [partner Center-hitelesítésben](./partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="net"></a>.NET

A korábban megadott ügyfél-elfogadás megerősítése (i) beolvasása:

- Használja a **IAggregatePartner. Customs** gyűjteményt, és hívja meg a **ById** metódust a megadott ügyfél-azonosítóval.

- A **ByAgreementType** metódus meghívásával olvassa be a **szerződések** tulajdonságot, és szűrje az eredményeket a Microsoft ügyfél-szerződésre.

- A **Get** vagy a **GetAsync** metódus hívása.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Teljes minta a [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) osztályban található a [konzol tesztelése alkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektben.

## <a name="rest-request"></a>REST-kérelem

A korábban megadott ügyfél-elfogadás megerősítésének beolvasása:

1. Hozzon létre egy REST-kérelmet a [szerződések](./agreement-resources.md) gyűjtésének lekéréséhez az ügyfél számára.

2. A **agreementType** lekérdezési paraméterrel az eredményeket csak a Microsoft ügyfél-szerződésre szűkítheti.

### <a name="request-syntax"></a>Kérelem szintaxisa

Használja a következő kérelem szintaxisát:

| Metódus | Kérés URI-ja                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements? agreementType = {egyezmény-típus} http/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

A kérelemhez a következő URI-paramétereket használhatja:

| Név             | Típus | Kötelező | Leírás                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| ügyfél – bérlő – azonosító | GUID | Igen | Az érték egy GUID formátumú **CustomerTenantId** , amely lehetővé teszi az ügyfél megadását. |
| szerződés típusa | sztring | No | Ez a paraméter az összes szerződési metaadatot visszaadja. Ezzel a paraméterrel a lekérdezési választ adott szerződési típusra szűkítheti. A támogatott értékek a következők: <br/><br/> **MicrosoftCloudAgreement** , amely csak a *MicrosoftCloudAgreement* típusú megállapodás-metaadatokat tartalmazza.<br/><br/> **MicrosoftCustomerAgreement** , amely csak a *MicrosoftCustomerAgreement* típusú megállapodás-metaadatokat tartalmazza.<br/><br/> **\*** Ez az összes szerződési metaadatot visszaadja. (Ne használja **\*** , kivéve, ha a kód nem rendelkezik a váratlan szerződések típusának kezeléséhez szükséges logikával.)<br/><br/> **Megjegyzés:** Ha nincs megadva az URI paraméter, a lekérdezés alapértelmezés szerint **MicrosoftCloudAgreement** a visszafelé kompatibilitás érdekében. A Microsoft bármikor bevezethet szerződési metaadatokat új szerződési típusokkal.  |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus a válasz törzsében a **Szerződés** erőforrásainak gyűjteményét adja vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.

A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
