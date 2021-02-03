---
title: Előfizetés regisztrálása
description: Regisztráljon egy meglévő előfizetést, hogy engedélyezve legyen az Azure-foglalások rendezése.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9a96bb350f22430c9fd7a1759e336cc9f3ca1939
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768308"
---
# <a name="register-a-subscription"></a>Előfizetés regisztrálása

**A következőkre vonatkozik**

- Partnerközpont

Regisztráljon egy meglévő [előfizetést](subscription-resources.md) , hogy engedélyezve legyen az Azure-foglalások rendezése.

Azure-foglalás megvásárlásához legalább egy meglévő CSP Azure-előfizetéssel kell rendelkeznie. Ez a módszer lehetővé teszi a meglévő CSP Azure-előfizetés regisztrálását, amely lehetővé teszi az Azure-foglalások megvásárlását.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

## <a name="c"></a>C\#

Az ügyfél előfizetésének regisztrálásához kérje le az [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosítására. Ezután hívja meg az [**előfizetés. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódust az előfizetés-azonosítóval a regisztrálni kívánt előfizetés azonosításához.

Végül hívja meg a **regisztrációs. Register ()** metódust az előfizetés regisztrálásához és az előfizetés regisztrációs állapotának lekéréséhez használható URI beszerzéséhez. További információ: előfizetés- [regisztráció állapotának beolvasása](get-subscription-registration-status.md).

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus    | Kérés URI-ja                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **UTÁNI**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrations http/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

A következő elérésiút-paraméterek használatával azonosíthatja az ügyfelet és az előfizetést.

| Név                    | Típus       | Kötelező | Leírás                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| ügyfél-azonosító             | sztring     | Igen      | Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.         |
| előfizetés-azonosító         | sztring     | Igen      | Egy GUID formátumú karakterlánc, amely azonosítja az előfizetést.     |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

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

Ha ez sikeres, a válasz tartalmaz egy URI-t tartalmazó **Location** fejlécet, amely az előfizetés regisztrációs állapotának lekérésére használható. Mentse ezt az URI-t más kapcsolódó REST API-kkal való használatra. Az állapot beolvasására vonatkozó példát az [előfizetés regisztrációs állapotának beolvasása](get-subscription-registration-status.md)című témakörben talál.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

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
