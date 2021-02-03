---
title: Felhasználói fiók törlése egy ügyfélnél
description: Meglévő felhasználói fiók törlése egy ügyfélhez.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 77fc1a1c7264779ca549be8d52798e90c91138bb
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768128"
---
# <a name="delete-a-user-account-for-a-customer"></a>Felhasználói fiók törlése egy ügyfélnél

**A következőkre vonatkozik:**

- Partnerközpont

Ez a cikk azt ismerteti, hogyan törölheti az ügyfelek meglévő felhasználói fiókját.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Egy felhasználói azonosító. Ha nem rendelkezik a felhasználói AZONOSÍTÓval, tekintse [meg az ügyfélhez tartozó összes felhasználói fiók listájának beolvasása](get-a-list-of-all-user-accounts-for-a-customer.md)című témakört.

## <a name="deleting-a-user-account"></a>Felhasználói fiók törlése

Felhasználói fiók törlésekor a felhasználói állapot 30 napig **inaktívra** van állítva. Harminc nap elteltével a felhasználói fiók és a hozzá tartozó adatok törlődnek, és helyreállíthatatlanul történnek.

Ha az inaktív fiók a harminc napos időszakon belül van, [visszaállíthatja az ügyfél törölt felhasználói fiókját](restore-a-user-for-a-customer.md) . Ha azonban olyan fiókot állít vissza, amely törölve lett, és inaktívként jelölt meg, a fiók már nem lesz visszaküldve a felhasználói gyűjtemény tagjaként (például ha az [ügyfél összes felhasználói fiókjának listáját kapja](get-a-list-of-all-user-accounts-for-a-customer.md)).

## <a name="c"></a>C\#

Meglévő ügyfél-felhasználói fiók törlése:

1. Az ügyfél azonosításához használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval.

2. A felhasználó azonosításához hívja meg a Users [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust.

3. A [**törlési**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) metódus hívásával törölje a felhasználót, és állítsa inaktívra a felhasználói állapotot.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: DeleteCustomerUser.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus     | Kérés URI-ja                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Az ügyfél és a felhasználó azonosításához használja a következő lekérdezési paramétereket.

| Név                   | Típus     | Kötelező | Leírás                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| ügyfél – bérlő – azonosító     | GUID     | Y        | Az érték egy GUID-formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi a viszonteladónak az adott ügyfél eredményeinek szűrését. |
| felhasználói azonosító                | GUID     | Y        | Az érték egy GUID-formátumú **felhasználói azonosító** , amely egyetlen felhasználói fiókhoz tartozik.                                          |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a metódus egy **204** -as értéket ad vissza, amely nem a tartalom állapotkód.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
