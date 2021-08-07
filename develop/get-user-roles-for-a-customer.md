---
title: Egy ügyfél felhasználói szerepköreinek lekérése
description: Lekért lista a felhasználói fiókhoz csatolt összes szerepkörről/engedélyről. A változatok közé tartozik az ügyfél összes felhasználói fiókra vonatkozó összes engedélyének és egy adott szerepkört használó felhasználók listájának lekért listája.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b139ee69ae5148896b1a438b061907e022175f318956667cebb91ead15b863f6
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989338"
---
# <a name="get-user-roles-for-a-customer"></a>Egy ügyfél felhasználói szerepköreinek lekérése

Lekért lista a felhasználói fiókhoz csatolt összes szerepkörről/engedélyről. A változatok közé tartozik az ügyfél összes felhasználói fiókra vonatkozó összes engedélyének és egy adott szerepkört használó felhasználók listájának lekért listája.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Egy adott ügyfél összes címtárszerepkörének lekérése először a megadott ügyfél-azonosítót kell lekérni. Ezután használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById() metódust.** Ezután hívja meg **a DirectoryRoles** tulajdonságot, majd a **Get() vagy** **a GetAsync() metódust.**

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** GetCustomerDirectoryRoles.cs

Egy adott szerepkört használó ügyfélfelhasználók listájának lekérése először a megadott ügyfél-azonosítót és a címtárszerepkör-azonosítót kell lekérni. Ezután használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById() metódust.** Ezután hívja meg a **DirectoryRoles** tulajdonságot, majd a **ById()** metódust, majd a **UserMembers** tulajdonságot, majd a **Get() vagy** **a GetAsync() metódust.**

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: PartnerSDK.FeatureSamples **osztály:** GetCustomerDirectoryRoleUserMembers.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{felhasználói azonosító}/directoryroles HTTP/1.1 |
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1                 |
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{szerepkör-azonosító}/usermembers    |

### <a name="uri-parameter"></a>URI-paraméter

A következő lekérdezési paraméterrel azonosíthatja a megfelelő ügyfelet.

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.                                                      |
| **felhasználói azonosító**            | **guid** | N        | Az érték egy GUID formátumú felhasználói **azonosító,** amely egyetlen felhasználói fiókhoz tartozik.                                                                                                                            |
| **szerepkör-azonosító**            | **guid** | N        | Az érték egy GUID formátumú **szerepkör-azonosító,** amely egy szerepkörtípushoz tartozik. Ezeket az azonosítókat úgy kaphatja meg, hogy lekérdezi egy ügyfél összes címtár-szerepkörét az összes felhasználói fiókra. (A második forgatókönyv, fent). |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a>REST-válasz

Sikeres művelet esetén ez a metódus az adott felhasználói fiókhoz társított szerepkörök listáját adja vissza.

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
      "totalCount": 2,
      "items": [
        {
          "name": "Helpdesk Administrator",
          "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
          "attributes": { "objectType": "DirectoryRole" }
        },
        {
          "name": "User Account Administrator",
          "id": "fe930be7-5e62-47db-91af-98c3a49a38b1",
          "attributes": { "objectType": "DirectoryRole" }
        }
      ],
      "attributes": { "objectType": "Collection" }
}
```
