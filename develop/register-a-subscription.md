---
title: Előfizetés regisztrálása
description: Regisztráljon egy meglévő előfizetést, hogy engedélyezve legyen az Azure Reservations megrendelése.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4ea2183ab0c2367c7772bdf40b5988c2b7eff7c539686760332bec4addda8bbe
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997192"
---
# <a name="register-a-subscription"></a>Előfizetés regisztrálása

Regisztráljon egy meglévő [előfizetést,](subscription-resources.md) hogy engedélyezve legyen az Azure Reservations megrendelése.

Azure-foglalás vásárlásához legalább egy meglévő CSP Azure-előfizetéssel kell lennie. Ezzel a módszerrel regisztrálhatja meglévő CSP Azure-előfizetését, így azure-foglalásokat is megvásárolhat.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

## <a name="c"></a>C\#

Az ügyfél előfizetésének regisztrálásához az ügyfél azonosítójával hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával, hogy azonosítsa az előfizetési műveleteket. Ezután hívja meg a [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódust az előfizetés azonosítójával a regisztráló előfizetés azonosításához.

Végül hívja meg a **Registration.Register()** metódust az előfizetés regisztrálásához és az előfizetés regisztrációs állapotának lekéréséhez használható URI lekéréséhez. További információ: [Előfizetés regisztrációs állapotának lekért állapota.](get-subscription-registration-status.md)

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus    | Kérés URI-ja                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **Post**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/registrations HTTP/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

Az ügyfél és az előfizetés azonosításához használja az alábbi elérésiút-paramétereket.

| Név                    | Típus       | Kötelező | Leírás                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| ügyfél-azonosító             | sztring     | Yes      | Egy GUID formátumú sztring, amely azonosítja az ügyfelet.         |
| subscription-id         | sztring     | Yes      | Egy GUID formátumú sztring, amely azonosítja az előfizetést.     |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-válasz

Ha a válasz sikeres, a válasz tartalmaz egy **Location** fejlécet egy URI-val, amely az előfizetés regisztrációs állapotának lekérésére használható. Mentse ezt az URI-t a többi kapcsolódó REST API-val való használathoz. Az állapot lekérésével kapcsolatos példáért lásd: [Előfizetés regisztrációs állapotának lekérése.](get-subscription-registration-status.md)

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
