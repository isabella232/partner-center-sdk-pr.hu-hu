---
title: Előfizetés regisztrációs állapotának lekérése
description: Lekéri egy olyan előfizetés állapotát, amely regisztrálva van a Azure Reserved VM Instancessal való használatra.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e06cf8a450d6c281f7f83a68c899d1e5b29e9855
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768440"
---
# <a name="get-subscription-registration-status"></a>Előfizetés regisztrációs állapotának lekérése

**A következőkre vonatkozik**

- Partnerközpont

Az előfizetés regisztrációs állapotának beszerzése olyan ügyfél-előfizetéshez, amely engedélyezve van a Azure Reserved VM Instances megvásárlására.

Ha egy Azure-beli fenntartott VM-példányt szeretne megvásárolni a partner Center API-val, rendelkeznie kell legalább egy meglévő CSP Azure-előfizetéssel. Az [előfizetés regisztrálása](register-a-subscription.md) lehetővé teszi a meglévő CSP Azure-előfizetés regisztrálását, amely lehetővé teszi a Azure Reserved VM instances megvásárlását. Ez a módszer lehetővé teszi az adott regisztráció állapotának beolvasását.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

## <a name="c"></a>C\#

Az előfizetés regisztrációs állapotának lekéréséhez először a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust használja az ügyfél-azonosítóval az ügyfél azonosításához. Ezután szerezzen be egy illesztőfelületet az előfizetési műveletekhez úgy, hogy meghívja az előfizetés [**. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódust az előfizetés-azonosítóval az előfizetés azonosításához. Ezután a RegistrationStatus tulajdonsággal szerezzen be egy felületet az aktuális előfizetés regisztrációs állapotára vonatkozó műveletekhez, és hívja meg a **Get** vagy a **GetAsync** metódust a **SubscriptionRegistrationStatus** objektum lekéréséhez.

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus    | Kérés URI-ja                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **GET**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrationstatus http/1.1 |

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
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
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

Ha ez sikeres, a válasz törzse [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) -erőforrást tartalmaz.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```
