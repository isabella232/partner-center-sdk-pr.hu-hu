---
title: Törölt felhasználó visszaállítása egy ügyfélnél
description: Törölt felhasználó visszaállítása ügyfél- és felhasználói azonosító alapján.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04cca2f7c99023ef277f0f265a755be3e4692fa5e786ce37939b6aebd32a3ba3
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996903"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>Törölt felhasználó visszaállítása egy ügyfélnél

Törölt felhasználó visszaállítása  ügyfél- és felhasználói azonosító alapján.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- A felhasználói azonosító. Ha nem tudja a felhasználói azonosítót, lásd: Törölt felhasználók [megtekintése egy ügyfélhez.](view-a-deleted-user.md)

## <a name="when-can-you-restore-a-deleted-user-account"></a>Mikor lehet visszaállítani egy törölt felhasználói fiókot?

A felhasználói állapot a felhasználói fiók törlésekor "inaktív" lesz. Ez 30 napig így marad, ezt követően a rendszer kiüríti a felhasználói fiókot és a hozzá tartozó adatokat, és nem állítható vissza. Törölt felhasználói fiókot csak ebben a 30 napos időszakban lehet visszaállítani. A törlést és az "inaktívként" megjelölt felhasználói fiókot a rendszer már nem a felhasználói gyűjtemény tagjaként visszaadja (például a Get a list of all user accounts for a customer (Ügyfél összes felhasználói fiókjának [lekért listája) használatával).](get-a-list-of-all-user-accounts-for-a-customer.md)

## <a name="c"></a>C\#

Felhasználó visszaállításához hozza létre a [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) osztály egy új példányát, és állítsa a [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) tulajdonság értékét [**UserState.Active értékre.**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate)

Egy törölt felhasználót úgy lehet visszaállítani, hogy a felhasználó állapotát aktívra állítani. A felhasználói erőforrás többi mezőjét nem kell újra kitöltenünk. Ezek az értékek automatikusan visszaállnak a törölt, inaktív felhasználói erőforrásból. Ezután használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához, és a [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust a felhasználó azonosításához.

Végül hívja meg a [**Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) metódust, és adja át a **CustomerUser** példányt, hogy elküldje a felhasználó visszaállítására vonatkozó kérést.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** CustomerUserRestore.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus    | Kérés URI-ja                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **Javítás** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{felhasználói azonosító} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A következő lekérdezési paraméterekkel adhatja meg az ügyfél-azonosítót és a felhasználói azonosítót.

| Név                   | Típus     | Kötelező | Leírás                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi, hogy a viszonteladó szűrje az eredményeket egy adott ügyfélre. |
| **felhasználóazonosító**            | **guid** | Y        | Az érték egy GUID formátumú felhasználói **azonosító,** amely egyetlen felhasználói fiókhoz tartozik.                                         |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.

| Név       | Típus   | Kötelező | Leírás                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| Állapot      | sztring | Y        | A felhasználói állapot. Törölt felhasználó visszaállításához ennek a sztringnek "aktívnak" kell lennie. |
| Attribútumok | object | N        | Tartalmazza az "ObjectType": "CustomerUser" adatokat.                                 |

### <a name="request-example"></a>Példa kérésre

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha sikeres, a válasz visszaadja a visszaállított felhasználói adatokat a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerUser"
    }
}
```
