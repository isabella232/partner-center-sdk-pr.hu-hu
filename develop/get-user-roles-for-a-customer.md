---
title: Egy ügyfél felhasználói szerepköreinek lekérése
description: A felhasználói fiókhoz csatolt összes szerepkör/engedély listájának beolvasása. A variációk közé tartozik az ügyfél összes felhasználói fiókja összes engedélyének lekérése, valamint az adott szerepkörrel rendelkező felhasználók listájának beolvasása.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dad5c035c08905c3d39052de07ebb912452a16b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767812"
---
# <a name="get-user-roles-for-a-customer"></a>Egy ügyfél felhasználói szerepköreinek lekérése

**A következőkre vonatkozik**

- Partnerközpont

A felhasználói fiókhoz csatolt összes szerepkör/engedély listájának beolvasása. A variációk közé tartozik az ügyfél összes felhasználói fiókja összes engedélyének lekérése, valamint az adott szerepkörrel rendelkező felhasználók listájának beolvasása.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Egy adott ügyfél összes címtár-szerepkörének lekéréséhez először kérje le a megadott ügyfél-azonosítót. Ezután használja a **IAggregatePartner. Customers** gyűjteményt, és hívja meg a **ById ()** metódust. Ezután hívja meg a **DirectoryRoles** tulajdonságot, majd a **Get ()** vagy a **GetAsync ()** metódust.

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: GetCustomerDirectoryRoles.cs

Az adott szerepkörrel rendelkező ügyfél-felhasználók listájának lekéréséhez először kérje le a megadott ügyfél-azonosítót és a címtár szerepkör-AZONOSÍTÓját. Ezután használja a **IAggregatePartner. Customers** gyűjteményt, és hívja meg a **ById ()** metódust. Ezután hívja meg a **DirectoryRoles** tulajdonságot, majd a **ById ()** metódust, majd a **UserMembers** tulajdonságot, amelyet a **Get ()** vagy a **GetAsync ()** metódus követ.

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: PartnerSDK. FeatureSamples **osztály**: GetCustomerDirectoryRoleUserMembers.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID}/directoryroles http/1.1 |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles http/1.1                 |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{role-ID}/usermembers    |

### <a name="uri-parameter"></a>URI-paraméter

A megfelelő ügyfél azonosításához használja a következő lekérdezési paramétert.

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél – bérlő – azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.                                                      |
| **felhasználói azonosító**            | **guid** | N        | Az érték egy olyan GUID formátumú **felhasználói azonosító** , amely egyetlen felhasználói fiókhoz tartozik.                                                                                                                            |
| **szerepkör-azonosító**            | **guid** | N        | Az érték egy szerepkör-típushoz tartozó GUID formátumú **szerepkör-azonosító** . Ezeket az azonosítókat úgy érheti el, ha lekérdezi az összes címtárbeli szerepkört az összes felhasználói fiókban. (A fenti második forgatókönyv). |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

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

Ha a művelet sikeres, ez a metódus az adott felhasználói fiókhoz társított szerepkörök listáját adja vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

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
