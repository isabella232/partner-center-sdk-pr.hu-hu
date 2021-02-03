---
title: Felhasználói szerepkörök beállítása egy ügyfélnél
description: Egy ügyfél-fiókban több címtár-szerepkör található. A szerepkörökhöz felhasználói fiókokat is hozzárendelhet.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f42120e40e54ff8bd6242634d97268091abf8e1c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768268"
---
# <a name="set-user-roles-for-a-customer"></a>Felhasználói szerepkörök beállítása egy ügyfélnél

**A következőkre vonatkozik**

- Partnerközpont

Egy ügyfél-fiókban több címtár-szerepkör található. A szerepkörökhöz felhasználói fiókokat is hozzárendelhet.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Ha egy címtárbeli szerepkört szeretne hozzárendelni egy ügyfél-felhasználóhoz, hozzon létre egy új [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) a megfelelő felhasználói adatokkal. Ezután hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a megadott ügyfél-azonosítóval az ügyfél azonosításához. Innen válassza a [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) metódust a címtár SZEREPKÖR-azonosítóval a szerepkör megadásához. Ezután nyissa meg a **UserMembers** gyűjteményt, és a [**create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) metódussal adja hozzá az új felhasználói tagot az adott szerepkörhöz rendelt felhasználói tagok gyűjteményéhez.

``` csharp
// UserMember createdUser;
// IAggregatePartner partnerOperations;
// Customer selectedCustomer;
// IDirectoryRole selectedRole;

// Create the new user member.
UserMember userMemberToAdd = new UserMember()
{
    UserPrincipalName = createdUser.UserPrincipalName,
    DisplayName = createdUser.DisplayName,
    Id = createdUser.Id
};

// Add the new user member to the role.
var userMemberAdded = partnerOperations.Customers.ById(selectedCustomer.Id).DirectoryRoles.ById(selectedRole.Id).UserMembers.Create(userMemberToAdd);
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: AddUserMemberToDirectoryRole.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{role-ID}/usermembers http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A megfelelő ügyfél és szerepkör azonosításához használja a következő URI-paramétereket. Annak a felhasználónak a azonosításához, akihez a szerepkört hozzá szeretné rendelni, adja meg az azonosítási adatokat a kérelem törzsében.

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél – bérlő – azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti. |
| **szerepkör-azonosító**            | **guid** | Y        | Az érték egy GUID formátumú **szerepkör-azonosító** , amely azonosítja a felhasználóhoz hozzárendelni kívánt szerepkört.                                                              |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.

| Név                  | Típus       | Kötelező | Leírás                            |
|-----------------------|------------|----------|----------------------------------------|
| **ID**                | **karakterlánc** | Y        | A szerepkörhöz hozzáadandó felhasználó azonosítója. |
| **Megjelenítendő név**       | **karakterlánc** | Y        | A felhasználó felhasználóbarát megjelenítendő neve. |
| **UserPrincipalName** | **karakterlánc** | Y        | A felhasználói tag neve.        |
| **Attribútumok**        | **objektum** | Y        | A "objektumtípus": "UserMember" kifejezést tartalmazza     |

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/directoryroles/f023fd81-a637-4b56-95fd-791ac0226033/usermembers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 180
Expect: 100-continue

{
    "Id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "DisplayName": "Daniel Tsai",
    "UserPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "Attributes": {
        "ObjectType": "UserMember"
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ez a metódus visszaadja azt a felhasználói fiókot, amelyhez a szerepkör-azonosító csatolva lett, ha a felhasználó sikeresen hozzárendelte a szerepkört.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 201 Created
Content-Length: 231
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CV: aia94+gnrEeQqkGr.0
MS-ServerId: 101112202
Date: Tue, 20 Dec 2016 23:36:55 GMT

{
    "displayName": "Daniel Tsai",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "roleId": "f023fd81-a637-4b56-95fd-791ac0226033",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "attributes": {
        "objectType": "UserMember"
    }
}
```
