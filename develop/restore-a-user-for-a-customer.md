---
title: Törölt felhasználó visszaállítása egy ügyfélnél
description: Törölt felhasználó visszaállítása ügyfél-azonosító és felhasználói azonosító alapján.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9fd86a268c804a2fdd5efd67a8982afc043c95a6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768407"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>Törölt felhasználó visszaállítása egy ügyfélnél

**A következőkre vonatkozik**

- Partnerközpont

Törölt **felhasználó** visszaállítása ügyfél-azonosító és felhasználói azonosító alapján.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- A felhasználói azonosító. Ha nem rendelkezik a felhasználói AZONOSÍTÓval, tekintse [meg az ügyfél törölt felhasználóinak megtekintése](view-a-deleted-user.md)című témakört.

## <a name="when-can-you-restore-a-deleted-user-account"></a>Mikor állíthatja vissza a törölt felhasználói fiókot?

Felhasználói fiók törlésekor a felhasználói állapot "inaktív" értékre van állítva. Így harminc napig marad, amely után a felhasználói fiók és a hozzá tartozó adatok törlődnek, és helyreállíthatatlanul történnek. A törölt felhasználói fiókokat csak ezen a harminc napos időszakban lehet visszaállítani. Ha törölve lett, és "inaktív" jelöléssel jelölte meg, a felhasználói fiók már nem lesz visszaküldve a felhasználói gyűjtemény tagjaként (például az [ügyfél összes felhasználói fiókjának lekérése lista](get-a-list-of-all-user-accounts-for-a-customer.md)használatával).

## <a name="c"></a>C\#

Egy felhasználó visszaállításához hozza létre a [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) osztály új példányát, és állítsa be a [**User. State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) tulajdonság értékét a [**UserState. Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate)értékre.

A törölt felhasználókat úgy állíthatja vissza, hogy a felhasználó állapotát aktívra állítja. A felhasználói erőforrásban nem kell újratöltenie a fennmaradó mezőket. Ezeket az értékeket a rendszer automatikusan visszaállítja a törölt, inaktív felhasználói erőforrásból. Ezután használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához, valamint a Users [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust a felhasználó azonosításához.

Végül hívja meg a [**patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) metódust, és adja át a **CustomerUser** -példányt a felhasználó visszaállítására vonatkozó kérés elküldéséhez.

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

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: CustomerUserRestore.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus    | Kérés URI-ja                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **JAVÍTÁS** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az ügyfél-azonosító és a felhasználói azonosító megadásához használja a következő lekérdezési paramétereket.

| Név                   | Típus     | Kötelező | Leírás                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **ügyfél – bérlő – azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó az eredményeket egy adott ügyfélre szűrje. |
| **felhasználói azonosító**            | **guid** | Y        | Az érték egy olyan GUID formátumú **felhasználói azonosító** , amely egyetlen felhasználói fiókhoz tartozik.                                         |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.

| Név       | Típus   | Kötelező | Leírás                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| Állam      | sztring | Y        | A felhasználói állapot. A törölt felhasználók visszaállításához a karakterláncnak "aktív" értéknek kell lennie. |
| Attribútumok | object | N        | A "objektumtípus": "CustomerUser" kifejezést tartalmazza.                                 |

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

Ha a művelet sikeres, a válasz a visszaállított felhasználói adatokat adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

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
