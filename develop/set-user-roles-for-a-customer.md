---
title: Felhasználói szerepkörök beállítása egy ügyfélnél
description: Az ügyfélfiókon belül címtárszerepkör-készlet található. Ezekhez a szerepkörökhöz felhasználói fiókokat rendelhet.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 945b5180ce2fe9067a940942a6e3c61dc243978fcb9d02eb218dce69ec487402
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989032"
---
# <a name="set-user-roles-for-a-customer"></a>Felhasználói szerepkörök beállítása egy ügyfélnél

Az ügyfélfiókon belül címtárszerepkör-készlet található. Ezekhez a szerepkörökhöz felhasználói fiókokat rendelhet.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Ha címtárszerepkört szeretne hozzárendelni egy ügyfélfelhasználóhoz, hozzon létre egy új [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) adatokat a megfelelő felhasználói adatokkal. Ezután hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a megadott ügyfél-azonosítóval az ügyfél azonosításához. A szerepkör megadásához használja a [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) metódust a címtár-szerepkör azonosítójával. Ezután hozzáférés a **UserMembers** gyűjteményhez, és a [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) metódussal adja hozzá az új felhasználói tagot a szerepkörhöz rendelt felhasználói tagok gyűjteményéhez.

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

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** AddUserMemberToDirectoryRole.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{szerepkör-azonosító}/usermembers HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az alábbi URI-paraméterekkel azonosíthatja a megfelelő ügyfelet és szerepkört. Annak a felhasználónak az azonosításához, akihez a szerepkört hozzárendeli, a kérelem törzsében meg kell határoznia az azonosító adatokat.

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlőazonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit. |
| **szerepkör-azonosító**            | **guid** | Y        | Az érték egy GUID formátumú **szerepkör-azonosító,** amely azonosítja a felhasználóhoz hozzárendelni kívánt szerepkört.                                                              |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.

| Név                  | Típus       | Kötelező | Leírás                            |
|-----------------------|------------|----------|----------------------------------------|
| **Id**                | **sztring** | Y        | A szerepkörhöz hozzáadnia kell a felhasználó azonosítója. |
| **Megjelenítendő név**       | **sztring** | Y        | A felhasználó rövid megjelenített neve. |
| **UserPrincipalName (Felhasználónév)** | **sztring** | Y        | A rendszerbiztonsági tag neve.        |
| **Attribútumok**        | **Objektum** | Y        | Tartalmazza az "ObjectType":"UserMember" adatokat     |

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

Ez a metódus visszaadja a szerepkör-azonosítóval csatolt felhasználói fiókot, amikor a felhasználóhoz sikeresen hozzá lett rendelve a szerepkör.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
