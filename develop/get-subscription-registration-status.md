---
title: Előfizetés regisztrációs állapotának lekérése
description: Lekérte egy előfizetés állapotát, amely regisztrálva van a Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0e0a65abba94f1f05a98282fa67ff1d185ba4e082488d2d7887b4e9346c38967
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989661"
---
# <a name="get-subscription-registration-status"></a>Előfizetés regisztrációs állapotának lekérése

Hogyan lehet lekérte az előfizetés regisztrációs állapotát egy olyan ügyfél-előfizetéshez, amely számára engedélyezett a Azure Reserved VM Instances.

Ha azure-beli fenntartott virtuálisgép-példányt az Partnerközpont API-val vásárolni, legalább egy meglévő CSP Azure-előfizetéssel kell lennie. Az [Előfizetés regisztrálása](register-a-subscription.md) módszerrel regisztrálhatja meglévő CSP Azure-előfizetését, így megvásárolhatja a Azure Reserved VM Instances. Ezzel a módszerrel lekérhető a regisztráció állapota.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

## <a name="c"></a>C\#

Az előfizetés regisztrációs állapotának lehöz először használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához. Ezután szerezze be az előfizetési műveletek interfészét a [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódus az előfizetés azonosítójával való hívásával az előfizetés azonosításához. Ezután a RegistrationStatus tulajdonság használatával szerezzen be egy felületet az aktuális előfizetés regisztrációs állapotműveleteihez, és hívja meg a **Get** vagy **GetAsync** metódust a **SubscriptionRegistrationStatus** objektum lekéréséhez.

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus    | Kérés URI-ja                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **Kap**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/registrationstatus HTTP/1.1 |

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

Ha ez sikeres, a válasz törzse tartalmaz egy [SubscriptionRegistrationStatus erőforrást.](subscription-resources.md#subscriptionregistrationstatus)

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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
