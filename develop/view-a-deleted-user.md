---
title: Egy ügyfél törölt felhasználóinak megtekintése
description: Lekéri az ügyfél által a törölt CustomerUser-erőforrások listáját az ügyfél azonosítója alapján. Igény szerint beállíthatja az oldalméret méretét. Meg kell adnia egy szűrőt.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b1a9b85e3eba7ae7ec1dab8e951134d03371604
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768231"
---
# <a name="view-deleted-users-for-a-customer"></a>Egy ügyfél törölt felhasználóinak megtekintése

**A következőkre vonatkozik**

- Partnerközpont

Lekéri az ügyfél által a törölt CustomerUser-erőforrások listáját az ügyfél azonosítója alapján. Igény szerint beállíthatja az oldalméret méretét. Meg kell adnia egy szűrőt.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="what-happens-when-you-delete-a-user-account"></a>Mi történik, amikor töröl egy felhasználói fiókot?

Felhasználói fiók törlésekor a felhasználói állapot "inaktív" értékre van állítva. Így harminc napig marad, amely után a felhasználói fiók és a hozzá tartozó adatok törlődnek, és helyreállíthatatlanul történnek. Ha a harminc napos ablakban szeretné visszaállítani a törölt felhasználói fiókot, tekintse meg a [törölt felhasználó visszaállítása az ügyfélre](restore-a-user-for-a-customer.md)című témakört. Ha törölve lett, és "inaktív" jelöléssel jelölte meg, a felhasználói fiókot a rendszer már nem adja vissza a felhasználói gyűjtemény tagjaként (például az [ügyfél összes felhasználói fiókjának lekérése lista](get-a-list-of-all-user-accounts-for-a-customer.md)használatával). A még nem törölt felhasználók listájának lekéréséhez le kell kérdezni az inaktív felhasználói fiókokat.

## <a name="c"></a>C\#

A törölt felhasználók listájának lekéréséhez hozzon létre egy lekérdezést, amely azokat az ügyfelek felhasználóinak szűri, akiknek az állapota inaktív. Először hozza létre a szűrőt egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumnak a paraméterekkel való létrehozásával, ahogy az a következő kódrészletben látható. Ezután hozza létre a lekérdezést a [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) metódus használatával. Ha nem szeretné, hogy a lapozható eredmények legyenek, használja helyette a [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódust. Ezután használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához. Végül hívja meg a [**lekérdezési**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) módszert a kérelem elküldéséhez.

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: GetCustomerInactiveUsers.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users? méret = {size} &szűrő = {Filter} http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A kérelem létrehozásakor használja az alábbi elérési utat és a lekérdezési paramétereket.

| Név        | Típus   | Kötelező | Leírás                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ügyfél-azonosító | guid   | Igen      | Az érték egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.                                                                                                            |
| size        | int    | Nem       | Az egyszerre megjelenítendő eredmények száma. Ezt a paramétert nem kötelező megadni.                                                                                                     |
| filter (szűrő)      | filter (szűrő) | Igen      | A felhasználói keresést szűrő lekérdezés. A törölt felhasználók beolvasásához a következő karakterláncot kell tartalmaznia és kódolnia: {"Field": "UserState", "value": "inaktív", "operátor": "Equals"}. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus [CustomerUser](user-resources.md#customeruser) -erőforrások gyűjteményét adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
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
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
