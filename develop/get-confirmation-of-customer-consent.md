---
title: A Microsoft Cloud szerződés ügyfél általi elfogadási megerősítésének lekérése
description: Ez a cikk azt ismerteti, hogyan lehet megerősíteni a Microsoft Cloud szerződés ügyfél általi elfogadását.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: d91f70cbd8bc9b8622b8d41ab9e601e2aee2cfab
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768447"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a>A Microsoft Cloud szerződés ügyfél általi elfogadási megerősítésének lekérése

**A következőkre vonatkozik**

- Partnerközpont

> [!NOTE]
> A partner Center jelenleg csak a Microsoft nyilvános felhőben támogatja a **szerződési** erőforrást. Nem alkalmazható a következőre:
>
> - A 21Vianet által üzemeltetett partneri központ
> - A Microsoft Cloud Germany Partnerközpontja
> - A Microsoft Cloud for US Government Partnerközpontja

## <a name="prerequisites"></a>Előfeltételek

- Ha a partner Center .NET SDK-t használja, a 1,9-es vagy újabb verzió szükséges.

- Ha a partner Center Java SDK-t használja, a 1,8-es vagy újabb verzió szükséges.

- A [partner Center-hitelesítésben](./partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="net-version-14-or-newer"></a>.NET (1,4-es vagy újabb verzió)

A korábban megadott ügyfél-elfogadás megerősítése (i) beolvasása:

- Használja a **IAggregatePartner. Customs** gyűjteményt, és hívja meg a **ById** metódust a megadott ügyfél-azonosítóval.

- A **ByAgreementType** metódus meghívásával olvassa be a **szerződések** tulajdonságot, és szűrje Microsoft Cloud szerződés eredményét.

- A **Get** vagy a **GetAsync** metódus hívása.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Teljes minta a [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) osztályban található a [konzol tesztelése alkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektben.

## <a name="net-version-19---113"></a>.NET (1,9-1,13-es verzió)

A korábban megadott ügyfél-elfogadás megerősítésének lekérése:

Használja a **IAggregatePartner. Customs** gyűjteményt, és hívja meg a **ById** metódust a megadott ügyfél-azonosítóval. Ezután szerezze be a **szerződések** tulajdonságot, majd a **Get** vagy a **GetAsync** metódus meghívásával.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

A korábban megadott ügyfél-elfogadás megerősítésének lekérése:

Használja a **IAggregatePartner. getCustomers** függvényt, és hívja meg a **byId** függvényt a megadott ügyfél-azonosítóval. Ezután szerezze be a **getAgreements** függvényt, majd a **Get** függvény meghívásával.

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

Teljes minta a [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) osztályban található a [konzol tesztelése alkalmazás](https://github.com/Microsoft/Partner-Center-Java-Samples) projektben.

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

A korábban megadott ügyfél-elfogadás megerősítésének lekérése:

Használja a [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) parancsot.

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a>REST-kérelem

A korábban megadott ügyfél-elfogadás megerősítésének lekéréséhez tekintse meg az alábbi utasításokat.

Hozzon létre egy új **szerződési** erőforrást a megfelelő minősítési információkkal.

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus | Kérés URI-ja                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements http/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

A következő lekérdezési paraméterrel adhatja meg a megerősítő ügyfelet.

| Név             | Típus | Kötelező | Leírás                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| CustomerTenantId | GUID | Y        | Az érték egy GUID formátumú **CustomerTenantId** , amely lehetővé teszi az ügyfél megadását. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

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

Ha ez sikeres, ez a metódus a válasz törzsében a **Szerződés** erőforrásainak gyűjteményét adja vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

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
