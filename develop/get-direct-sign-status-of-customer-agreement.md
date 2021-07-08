---
title: Lekérte az ügyfél közvetlen aláírási állapotát a Microsoft Ügyfélszerződés.
description: A DirectSignedCustomerAgreementStatus erőforrás használatával lekértheti az ügyfél közvetlen aláírásának (közvetlen elfogadásának) állapotát a Microsoft Ügyfélszerződés.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: a17775614b4eb328514b2b32b4cac1e513019cff
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549178"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Az ügyfél közvetlen aláírásának (közvetlen elfogadásának) állapotát Microsoft Ügyfélszerződés

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A **DirectSignedCustomerAgreementStatus** erőforrást jelenleg csak a Microsoft nyilvános Partnerközpont támogatja.

Ez a cikk azt ismerteti, hogyan lehet lekérni az ügyfél által a Microsoft Ügyfélszerződés.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Az ügyfél általi közvetlen ügyfél-elfogadás állapotának Microsoft Ügyfélszerződés hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóval. Ezután a [**Agreements tulajdonság**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) használatával lekér egy [**ICustomerAgreementCollection felületet.**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) Végül hívja meg a `GetDirectSignedCustomerAgreementStatus()` vagy `GetDirectSignedCustomerAgreementStatusAsync()` a et az állapot lekérése.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

**Minta:** [Konzol mintaalkalmazás.](https://github.com/microsoft/Partner-Center-DotNet-Samples) **Project:** SdkSamples **osztály:** GetDirectSignedCustomerAgreementStatus.cs

## <a name="rest-request"></a>REST-kérés

Az Microsoft Ügyfélszerződés ügyfél általi közvetlen elfogadás állapotának lekérésére hozzon létre egy REST-kérést, amely lekéri a [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) adatokat az ügyfél számára.

### <a name="request-syntax"></a>Kérés szintaxisa

Használja a következő kérésszintaxist:

| Metódus | Kérés URI-ja                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

A kérelemhez a következő URI-paramétereket használhatja:

| Név             | Típus | Kötelező | Leírás                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| ügyfél-bérlő-azonosító | GUID | Igen | Az érték egy GUID formátumú **CustomerTenantId,** amely lehetővé teszi az ügyfél bérlőazonosítójának megadását. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST-válasz

Ha sikeres, ez a metódus egy [ **DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) erőforrást ad vissza a válasz törzsében.

Az erőforrás rendelkezik **egy isSigned tulajdonságtal,** amely az ügyfél közvetlen aláírási (közvetlen elfogadási) állapotát jelzi.

- A true **(igaz) érték** azt jelzi, hogy a szerződést közvetlenül az ügyfél írta alá (fogadta el).

- A false **(hamis)** érték  azt jelzi, hogy a szerződést nem közvetlenül az ügyfél írta alá (fogadta el).

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.

Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
