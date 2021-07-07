---
title: Felhasználói fiók törlése egy ügyfélnél
description: Egy ügyfél meglévő felhasználói fiókjának törlése.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c45646da43b8926f911942374de5da07f318c526
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973060"
---
# <a name="delete-a-user-account-for-a-customer"></a>Felhasználói fiók törlése egy ügyfélnél

Ez a cikk egy ügyfél meglévő felhasználói fiókjának törlését ismerteti.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy felhasználói azonosító. Ha nem tudja a felhasználói azonosítót, tekintse meg az ügyfél összes felhasználói fiókjának [listáját.](get-a-list-of-all-user-accounts-for-a-customer.md)

## <a name="deleting-a-user-account"></a>Felhasználói fiók törlése

Felhasználói fiók törlésekor a felhasználói állapot  30 napig inaktívra lesz állítva. 30 nap után a rendszer kiüríti a felhasználói fiókot és a hozzá tartozó adatokat, és nem állítható vissza.

Az ügyfelek [törölt felhasználói](restore-a-user-for-a-customer.md) fiókjai visszaállíthatóak, ha az inaktív fiók a 30 napos időkereten belül van. Ha azonban visszaállít egy törölt és inaktívként megjelölt fiókot, a rendszer nem ad vissza fiókot a felhasználógyűjtemény tagjaként (például amikor lekért egy listát az ügyfél összes felhasználói [fiókjáról).](get-a-list-of-all-user-accounts-for-a-customer.md)

## <a name="c"></a>C\#

Meglévő ügyfél-felhasználói fiók törlése:

1. Az [**ügyfél azonosításához használja az IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával.

2. A felhasználó azonosításához hívja meg a [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust.

3. Hívja meg [**a Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) metódust a felhasználó törléséhez, és állítsa a felhasználói állapotot inaktívra.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** DeleteCustomerUser.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus     | Kérés URI-ja                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{felhasználói azonosító} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

A következő lekérdezési paraméterekkel azonosíthatja az ügyfelet és a felhasználót.

| Név                   | Típus     | Kötelező | Leírás                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| ügyfél-bérlő-azonosító     | GUID     | Y        | Az érték egy GUID-formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára az eredmények szűrését egy adott ügyfélre. |
| felhasználói azonosító                | GUID     | Y        | Az érték egy GUID formátumú felhasználói **azonosító,** amely egyetlen felhasználói fiókhoz tartozik.                                          |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Sikeres művelet esetén ez a metódus **egy 204 Nincs** tartalom állapotkódot ad vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
