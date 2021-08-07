---
title: A Microsoft Cloud szerződés ügyfél általi elfogadási megerősítésének lekérése
description: Ez a cikk azt ismerteti, hogyan lehet megerősítést kapni az ügyfelek általi Microsoft Cloud szerződés.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: eb1f9ec5a7e96984f9c458419268fb305cf13ffd44d92fd01823ad94c2fb1798
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990800"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a>A Microsoft Cloud szerződés ügyfél általi elfogadási megerősítésének lekérése

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A **Szerződés** erőforrást jelenleg csak a Microsoft Partnerközpont támogatja.

## <a name="prerequisites"></a>Előfeltételek

- Ha az Partnerközpont .NET SDK-t használja, 1.9-es vagy újabb verzió szükséges.

- Ha az Partnerközpont Java SDK-t használja, 1.8-as vagy újabb verzió szükséges.

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](./partner-center-authentication.md) Ez a forgatókönyv csak az alkalmazás- és felhasználóhitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="net-version-14-or-newer"></a>.NET (1.4-es vagy újabb verzió)

A korábban megadott ügyfél-elfogadás megerősítésének(i) lekérése:

- Használja az **IAggregatePartner.Customers gyűjteményt,** és hívja meg a **ById** metódust a megadott ügyfélazonosítóval.

- A **ByAgreementType** metódus hívásával lekérheti a **Agreements** Microsoft Cloud szerződés és szűrheti az eredményeket.

- Hívja meg **a Get** vagy **a GetAsync metódust.**

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

A teljes minta a [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) osztályban található a konzol tesztalkalmazás [projektjében.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="net-version-19---113"></a>.NET (1.9-es és 1.13-as verzió)

A korábban megadott ügyfél-elfogadás megerősítésének lekérése:

Használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById** metódust a megadott ügyfél azonosítóval. Ezután szerezze be a **Agreements** tulajdonságot, majd hívja meg a **Get** vagy **GetAsync metódusokat.**

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

A korábban megadott ügyfél-elfogadás megerősítésének lekérése:

Használja az **IAggregatePartner.getCustomers** függvényt, és hívja meg a **byId** függvényt a megadott ügyfél azonosítóval. Ezután szerezze be a **getAgreements** függvényt, majd hívja meg a **get** függvényt.

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

A teljes minta a [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) osztályban található a konzol tesztalkalmazás [projektjében.](https://github.com/Microsoft/Partner-Center-Java-Samples)

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

A korábban megadott ügyfél-elfogadás megerősítésének lekérése:

Használja a [**Get-PartnerCustomerAgreement parancsot.**](/powershell/module/partnercenter/get-partnercustomeragreement)

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a>REST-kérés

A korábban megadott ügyfél-elfogadás megerősítésének lekérését az alábbi utasításokban láthatja.

Hozzon létre egy új **Szerződés** erőforrást a megfelelő tanúsítványinformációk alapján.

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus | Kérés URI-ja                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

A következő lekérdezési paraméterrel adhatja meg a megerősíteni kívánt ügyfelet.

| Név             | Típus | Kötelező | Leírás                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| CustomerTenantId | GUID | Y        | Az érték egy **CUSTOMERTenantId** formátumú GUID, amely lehetővé teszi egy ügyfél megadását. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus **szerződéserőforrások** gyűjteményét adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```
