---
title: Ügyfél végzettségének frissítése
description: Megtudhatja, hogyan frissítheti az ügyfelek minősítését szinkron szűréssel vagy átvizsgálással, beleértve a profilhoz társított címet is.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 5047743afdef02033d9494e3d8c16c9ab96b3fe9
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446649"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a>Ügyfél minősítésének frissítése szinkron ellenőrzéssel

Megtudhatja, hogyan frissítheti az ügyfelek minősítését szinkron módon az Partnerközpont API-kon keresztül. Ennek aszinkron módon történő érvényre hozásról lásd: Ügyfél minősítésének frissítése [aszinkron ellenőrzéssel.](update-customer-qualification-asynchronous.md)

A partnerek frissíthetik az ügyfelek "Education" vagy "GovernmentCocloud" minősítését. Más értékek( "Nincs" és "Nonprofit" nem beállíthatók.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Ha frissítenie kell egy ügyfél "Education" minősítését, hívja meg **az [Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** hívást egy meglévő [**ügyfélen.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer)

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** PartnerSDK.FeatureSamples **osztály:** CustomerQualificationOperations.cs

Ahhoz, hogy az ügyfél minősítés nélkül frissítve legyen a **GovernmentCocloud** minősítése egy meglévő ügyfélen, a partnernek tartalmaznia kell az ügyfél [**ValidationCode (Érvényesítési**](utility-resources.md#validationcode)kódja) kódját.

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A minősítés frissítéséhez használja a következő lekérdezési paramétert.

| Név                   | Típus | Kötelező | Leírás                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | GUID | Igen      | Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit. |
| **validationCode**     | int  | Nem       | Csak a Government Community Cloud.                                                                                                            |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

A [**CustomerQualification enum**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) egész értéke.

### <a name="request-example"></a>Példa kérésre

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus visszaadja a [**frissített Minősítés tulajdonságot**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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

- [Egy ügyfél végzettségének lekérése](./get-customer-qualification-synchronous.md)
- [Egy partner ellenőrzési kódjainak lekérése](get-a-partner-s-validation-codes.md)
