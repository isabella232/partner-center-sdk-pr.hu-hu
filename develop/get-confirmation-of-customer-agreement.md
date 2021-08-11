---
title: A Microsoft Ügyfélszerződés ügyfél általi elfogadási megerősítésének lekérése
description: Ez a cikk azt ismerteti, hogyan lehet megerősítést kapni az ügyfél általi Microsoft Ügyfélszerződés.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f5e71f2660c6db638193deec02e9ba4f25a35be6aabdc1c4219f63b1f3295908
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993503"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>A Microsoft Ügyfélszerződés ügyfél általi elfogadási megerősítésének lekérése

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A **Szerződés** erőforrást jelenleg csak a Microsoft Partnerközpont támogatja.

Ez a cikk bemutatja, hogyan kérhető(k) le a jóváhagyás(ak) arról, hogy az ügyfél elfogadta-e Microsoft Ügyfélszerződés.

## <a name="prerequisites"></a>Előfeltételek

- Ha az Partnerközpont .NET SDK-t használja, 1.14-es vagy újabb verzió szükséges.

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](./partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="net"></a>.NET

A korábban megadott ügyfél-elfogadás megerősítésének(i) lekérése:

- Használja az **IAggregatePartner.Customers gyűjteményt,** és hívja meg a **ById** metódust a megadott ügyfélazonosítóval.

- A **ByAgreementType** metódus hívásával Microsoft Ügyfélszerződés be az **Agreements** tulajdonságot, és szűrje az eredményeket.

- Hívja meg **a Get** vagy **a GetAsync metódust.**

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

A teljes minta a [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) osztályban található a konzol tesztalkalmazás [projektjében.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="rest-request"></a>REST-kérés

A korábban megadott ügyfél-elfogadás megerősítésének lekérése:

1. Hozzon létre egy REST-kérést az ügyfél [szerződésgyűjteményének](./agreement-resources.md) lekéréséhez.

2. Az **agreementType lekérdezési** paraméterrel az eredményeket csak a lekérdezési Microsoft Ügyfélszerződés.

### <a name="request-syntax"></a>Kérésszintaxis

Használja a következő kérésszintaxist:

| Metódus | Kérés URI-ja                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

A kérelemhez a következő URI-paramétereket használhatja:

| Név             | Típus | Kötelező | Leírás                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| ügyfél-bérlő-azonosító | GUID | Yes | Az érték egy **CUSTOMERTenantId** formátumú GUID, amely lehetővé teszi egy ügyfél megadását. |
| szerződéstípus | sztring | No | Ez a paraméter az összes szerződési metaadatot visszaadja. Ezzel a paraméterrel adott szerződéstípusra lehet hatókört használni a lekérdezési válaszra. A támogatott értékek a következőek: <br/><br/> **MicrosoftCloudAgreement,** amely csak *MicrosoftCloudAgreement* típusú szerződési metaadatokat tartalmaz.<br/><br/> **MicrosoftCustomerAgreement,** amely csak *MicrosoftCustomerAgreement* típusú szerződési metaadatokat tartalmaz.<br/><br/> **\**_ az összes szerződési metaadatot visszaadja. (Ne használja a _* \* _ hacsak a kód nem rendelkezik a váratlan szerződéstípusok *kezeléshez szükséges logikával.) <br/> <br/> _* Megjegyzés:** Ha az URI paraméter nincs megadva, a lekérdezés alapértelmezés szerint **a MicrosoftCloudAgreement** értéket használja a visszamenőleges kompatibilitás érdekében. A Microsoft bármikor bevezetheti a szerződés metaadatait az új szerződéstípusokkal.  |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha a művelet sikeres, ez a metódus **szerződéserőforrások** gyűjteményét adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat.

Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
