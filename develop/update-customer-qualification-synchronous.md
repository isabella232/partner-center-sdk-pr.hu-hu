---
title: Ügyfél végzettségének frissítése
description: Megtudhatja, hogyan frissítheti az ügyfél képzettségét szinkron szűréssel vagy átvilágítással, beleértve a profilhoz társított címeket is.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 7faab68d20c698f5b040a76f4776dbdf14180640
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768649"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a>Ügyfél minősítésének frissítése szinkron ellenőrzés útján

**A következőkre vonatkozik**

- Partnerközpont

Ismerje meg, hogyan frissítheti az ügyfeleket a partner Center API-kkal párhuzamosan. Ennek aszinkron módon történő végrehajtásával kapcsolatban lásd: [az ügyfél minősítésének frissítése aszinkron ellenőrzés útján](update-customer-qualification-asynchronous.md).

Egy partner frissítheti az ügyfél minősítését, hogy "Education" vagy "GovernmentCommunityCloud". Más értékek, "None" és "nonprofit" nem állíthatók be.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Ha frissíteni szeretné az ügyfél képzettségét az "oktatás" értékre, hívja meg a **[Update/DotNet/API/Microsoft. Store. partnercenter. minősítés. icustomerqualification. Update)** egy meglévő  [**ügyfélen**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: PartnerSDK. FeatureSamples **osztály**: CustomerQualificationOperations.cs

Az ügyfél minősítésének frissítése egy meglévő ügyfél **GovernmentCommunityCloud** minősítés nélkül.  Emellett a partnernek is meg kell adnia az ügyfél [**ValidationCode**](utility-resources.md#validationcode).

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/Qualification? kód = {VALIDATIONCODE} http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A minősítés frissítéséhez használja a következő lekérdezési paramétert.

| Név                   | Típus | Kötelező | Leírás                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél – bérlő – azonosító** | GUID | Igen      | Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti. |
| **validationCode**     | int  | Nem       | Csak a kormányzati közösségi felhőhöz szükséges.                                                                                                            |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

A [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enumerálás egész értékének értéke.

### <a name="request-example"></a>Példa kérésre

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus visszaadja a frissített [**minősítési**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) tulajdonságot a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a>Kapcsolódó cikkek

- [Egy ügyfél végzettségének lekérése](get-a-customer-s-qualification.md)
- [Egy partner ellenőrzési kódjainak lekérése](get-a-partner-s-validation-codes.md)
