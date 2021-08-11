---
title: Ügyfél végzettségének frissítése
description: Aszinkron módon frissíti az ügyfél minősítéseit, beleértve a profilhoz társított címet is.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 6d46d6a170e4ebcd441e678c482469c4041b2435bf7ee946dc91db554ec4932a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997957"
---
# <a name="update-a-customers-qualifications-asynchronously"></a>Ügyfél minősítésének aszinkron frissítése

Aszinkron módon frissíti az ügyfél minősítéseit.

A partner aszinkron módon frissítheti az ügyfelek minősítését Úgy, hogy "Education" vagy "GovernmentCocloud" legyen. Más értékek( "Nincs" és "Nonprofit" nem beállíthatók.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Az ügyfél "Education" minősítésének létrehozásához először hozzon létre egy objektumot, amely a minősítési típust képviseli. Ezután hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítóval. Ezután a [**Minősítés tulajdonság**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) használatával lekér egy [**ICustomerQualification felületet.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) Végül hívja meg a `CreateQualifications()` vagy a parancsot a `CreateQualificationsAsync()` minősítési típus objektummal bemeneti paraméterként.

``` csharp
var qualificationToCreate = "education";    // can also be "StateOwnedEntity" or "GovernmentCommunityCloud". See GCC example below.
var qualificationType = { Qualification = qualificationToCreate };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

**Minta:** [Konzol mintaalkalmazás.](https://github.com/microsoft/Partner-Center-DotNet-Samples) **Project:** SdkSamples **osztály:** CreateCustomerQualification.cs

Ahhoz, hogy az ügyfél minősítés nélkül frissítve legyen a **GovernmentCocloud** minősítése egy meglévő ügyfélen, a partnernek tartalmaznia kell az ügyfél [**ValidationCode (Érvényesítési**](utility-resources.md#validationcode)kódja) kódját is. Először hozzon létre egy objektumot, amely a minősítési típust képviseli. Ezután hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítóval. Ezután a [**Minősítés tulajdonság**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) használatával lekér egy [**ICustomerQualification felületet.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) Végül hívja meg a vagy a parancsot `CreateQualifications()` `CreateQualificationsAsync()` a minősítési típus objektummal és az érvényesítési kóddal bemeneti paraméterként.

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

**Minta:** [Konzol mintaalkalmazás.](https://github.com/microsoft/Partner-Center-DotNet-Samples) **Project:** SdkSamples **osztály:** CreateCustomerQualificationWithGCC.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A minősítés frissítéséhez használja a következő lekérdezési paramétert.

| Név                   | Típus | Kötelező | Leírás                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | GUID | Yes      | Az érték egy GUID formátumú **ügyfél-bérlőazonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit. |
| **validationCode**     | int  | No       | Csak a Government Community Cloud.                                                                                                            |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében található minősítési objektumot ismerteti.

Tulajdonság | Típus | Kötelező | Leírás
-------- | ---- | -------- | -----------
Minősítés | sztring | Yes | A [**CustomerQualification enum sztringértéke.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

{
    "Qualification": "Education"
}

```

## <a name="rest-response"></a>REST-válasz

Ha sikeres, ez a metódus egy minősítési objektumot ad vissza a válasz törzsében. Az alábbi példa egy **Olyan ügyfél POST-hívását** mutatja be (korábbi minősítése **Nincs),** aki rendelkezik Oktatási **minősítéssel.**

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 201 CREATED
Content-Length: 29
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualification": "Education",
    "vettingStatus": "InReview",
    "vettingCreateDate": "2020-12-04T20:54:24Z" // UTC
}
```

## <a name="related-articles"></a>Kapcsolódó cikkek

- [Ügyfél minősítésének lekértsége](./get-customer-qualification-asynchronous.md)
- [Egy partner ellenőrzési kódjainak lekérése](get-a-partner-s-validation-codes.md)
