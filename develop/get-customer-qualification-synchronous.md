---
title: Egy ügyfél végzettségének lekérése
description: Megtudhatja, hogyan használhatja a szinkron érvényesítést az ügyfél a partner Center API-n keresztüli minősítésének beszerzéséhez. A partnerek ezt az oktatási ügyfelek ellenőrzésére használhatják.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e39ace3b598736abed6ab22021a8b93d473486a3
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711885"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a>Az ügyfél minősítésének beszerzése szinkron ellenőrzés útján

**A következőkre vonatkozik**

- Partnerközpont

Megtudhatja, hogyan lehet a partner Center API-kon keresztül szinkronban megszerezni az ügyfél képzettségét. Ha szeretné megtudni, hogyan teheti meg ezt aszinkron módon, tekintse meg az [ügyfél minősítésének beszerzése aszinkron ellenőrzésen keresztül](get-customer-qualification-asynchronous.md)című témakört.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Az ügyfél minősítésének beszerzéséhez hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval. Ezután használja a [**minősítés**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) tulajdonságot egy [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) felület lekéréséhez. Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) az ügyfél minősítésének lekéréséhez.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Qualification http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja a szükséges lekérdezési paramétereket az összes minősítés beszerzéséhez.

| Név               | Típus   | Kötelező | Leírás                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| **ügyfél – bérlő – azonosító** | sztring | Yes      | Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus egy minősítési értéket ad vissza a válasz törzsében.  Alább látható egy példa arra, **hogy az ügyfél az** **oktatási** végzettséggel rendelkezik.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a>Kapcsolódó cikkek

- [Ügyfél végzettségének frissítése](./update-customer-qualification-synchronous.md)