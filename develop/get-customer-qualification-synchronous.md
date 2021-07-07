---
title: Egy ügyfél végzettségének lekérése
description: Megtudhatja, hogyan használhatja a szinkron érvényesítést az ügyfél minősítésének az API-n keresztüli Partnerközpont le. A partnerek ezzel ellenőrizhetik az oktatási ügyfeleket.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d215ddb105efe3acd1182c4ff4bb25b045b121f0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446343"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a>Ügyfél minősítésének lekértsége szinkron ellenőrzéssel

Megtudhatja, hogyan szerezhető be az ügyfél minősítése szinkron módon az Partnerközpont API-kon keresztül. Ennek aszinkron módon történő érvényre jutásról lásd: Ügyfél minősítésének lekértsége [aszinkron ellenőrzéssel.](get-customer-qualification-asynchronous.md)

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Az ügyfél minősítésének megszerzéséhez hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóval. Ezután a [**Minősítés tulajdonság**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) használatával lekér egy [**ICustomerQualification felületet.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) vagy [**a GetAsync metódust**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) az ügyfél minősítésének lekérésére.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja az összes minősítéshez szükséges lekérdezési paramétert.

| Név               | Típus   | Kötelező | Leírás                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | sztring | Igen      | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha sikeres, ez a metódus egy minősítési értéket ad vissza a válasz törzsében.  Az alábbi példa egy **GET** hívást mutat be egy oktatási jogosultsággal **rendelkező ügyfélhez.**

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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