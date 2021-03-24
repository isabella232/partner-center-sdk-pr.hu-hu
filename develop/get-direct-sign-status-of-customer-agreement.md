---
title: Ügyfél közvetlen aláírási állapotának beolvasása a Microsoft ügyfél-szerződéshez.
description: A DirectSignedCustomerAgreementStatus-erőforrás segítségével lekérheti a Microsoft ügyfél-szerződés közvetlen aláírásának (közvetlen elfogadásának) állapotát.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 267e3aa63a94c5045977ad566eb5061df3b59882
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030556"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Ügyfél közvetlen aláírása (közvetlen elfogadás) állapotának lekérése a Microsoft ügyfél-szerződésből

**A következőkre vonatkozik:**

- Partnerközpont

A **DirectSignedCustomerAgreementStatus** erőforrást jelenleg csak a Microsoft nyilvános felhőben támogatja a partner Center.

Ez az erőforrás *nem alkalmazható* a következőre:

- A 21Vianet által üzemeltetett Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ez a cikk azt ismerteti, hogyan kérheti le a Microsoft ügyfél-szerződés közvetlen elfogadásának állapotát.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Az ügyfél Microsoft-szerződéssel kapcsolatos közvetlen elfogadásának állapotának lekéréséhez hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval. Ezután használja a [**szerződések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) tulajdonságot egy [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) -felület lekéréséhez. Végül hívja `GetDirectSignedCustomerAgreementStatus()` meg vagy kérje `GetDirectSignedCustomerAgreementStatusAsync()` le az állapotot.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

**Példa**: [konzolos minta alkalmazás](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Projekt**: SdkSamples **osztály**: GetDirectSignedCustomerAgreementStatus. cs

## <a name="rest-request"></a>REST-kérelem

Az ügyfél Microsoft-szerződéssel kapcsolatos közvetlen elfogadásának állapotának lekéréséhez hozzon létre egy REST-kérelmet az ügyfél [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) beolvasásához.

### <a name="request-syntax"></a>Kérelem szintaxisa

Használja a következő kérelem szintaxisát:

| Metódus | Kérés URI-ja                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directSignedMicrosoftCustomerAgreementStatus http/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

A kérelemhez a következő URI-paramétereket használhatja:

| Név             | Típus | Kötelező | Leírás                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| ügyfél – bérlő – azonosító | GUID | Igen | Az érték egy GUID-formátumú **CustomerTenantId** , amely lehetővé teszi az ügyfél BÉRLŐi azonosítójának megadását. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

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

Ha ez sikeres, ez a metódus egy [ **DirectSignedCustomerAgreementStatus** -erőforrást](./customer-agreement-direct-sign-status-resource.md) ad vissza a válasz törzsében.

Az erőforrás rendelkezik egy **isSigned** tulajdonsággal, amely az ügyfél közvetlen aláírása (közvetlen elfogadás) állapotát jelzi.

- A **true** érték azt jelzi, hogy a szerződés aláírása (elfogadva) közvetlenül az ügyfél által történt.

- A **false** érték azt jelzi, hogy a szerződés *nem* lett aláírva (elfogadva) közvetlenül az ügyfél által.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.

A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
