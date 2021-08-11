---
title: Egy ügyfél felhasználói jelszavának alaphelyzetbe állítása
description: A jelszó alaphelyzetbe állítása hasonlít az ügyfél meglévő felhasználói fiókjának egyéb részleteinek frissítéséhez.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 7ba8dadccf8159a9c55b2a4bb53f881f0ac732ce6c14dc7d5feb3a0c668c8a19
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996954"
---
# <a name="reset-user-password-for-a-customer"></a>Egy ügyfél felhasználói jelszavának alaphelyzetbe állítása

A jelszó alaphelyzetbe állítása hasonlít az ügyfél meglévő felhasználói fiókjának egyéb részleteinek frissítéséhez.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Egy adott ügyfélfelhasználó jelszavának visszaállításához először a megadott ügyfél-azonosítót és a megcélzott felhasználót kell lekérni. Ezután hozzon létre egy új **CustomerUser** objektumot, amely tartalmazza a meglévő ügyfél adatait, de egy új **PasswordProfile objektummal.** Ezután használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById() metódust.** Ezután hívja meg **a Users** tulajdonságot, a **ById()** metódust, majd a **Patch metódust.**

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// CustomerUser specifiedUser;

var selectedCustomer = partnerOperations.Customers.ById(selectedCustomerId).Get();
var userToUpdate = new CustomerUser()
   {
      PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "newPassword" },
      DisplayName = "Roger Federer",
      FirstName = "Roger",
      LastName = "Federer",
      UsageLocation = "US",
      UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
   };

// update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: PartnerSDK.FeatureSamples **osztály:** CustomerUserUpdate.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus    | Kérés URI-ja                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| **Javítás** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A következő lekérdezési paraméterrel azonosíthatja a megfelelő ügyfelet.

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit. |
| **felhasználói azonosító**            | **guid** | Y        | Az érték egy GUID formátumú felhasználói **azonosító,** amely egyetlen felhasználói fiókhoz tartozik.                                                                       |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

### <a name="request-example"></a>Példa kérésre

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
     "passwordProfile":{
        password: "Renew456*",
        forceChangePassword: true
      },

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a>REST-válasz

Ha ez a módszer sikeres, a felhasználói adatokat és a frissített jelszóadatokat adja vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "AX",
  "id": "95794928-9abe-4548-8b43-50ffc20b9404",
  "userPrincipalName": "aaaa4@abcdefgh1234.ccsctp.net",
  "firstName": "aaaa4",
  "lastName": "aaaa4",
  "displayName": "aaaa4",
  "passwordProfile": {
    "forceChangePassword": false,
    "password": "Renew456*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/95794928-9abe-4548-8b43-50ffc20b9404",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```
