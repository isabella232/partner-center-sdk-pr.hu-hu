---
title: Egy ügyfél törölt felhasználóinak megtekintése
description: Lekérte az ügyfél törölt CustomerUser erőforrásainak listáját ügyfélazonosító alapján. Igény szerint meg is állíthatja az oldalméretet. Meg kell adnunk egy szűrőt.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2f7e94d5e360075378e1895e586690597baaf66237f0b93bb526baee0c5d84ae
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989814"
---
# <a name="view-deleted-users-for-a-customer"></a>Egy ügyfél törölt felhasználóinak megtekintése

Lekérte az ügyfél törölt CustomerUser erőforrásainak listáját ügyfélazonosító alapján. Igény szerint meg is állíthatja az oldalméretet. Meg kell adnunk egy szűrőt.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

## <a name="what-happens-when-you-delete-a-user-account"></a>Mi történik, ha töröl egy felhasználói fiókot?

Felhasználói fiók törlésekor a felhasználói állapot "inaktív" lesz. Ez 30 napig így marad, ezt követően a rendszer kiüríti a felhasználói fiókot és a hozzá tartozó adatokat, és nem állítható vissza. Ha egy törölt felhasználói fiókot szeretne visszaállítani a 30 napos időkereten belül, tekintse meg a Törölt felhasználó visszaállítása egy [ügyfélre vonatkozó útmutatót.](restore-a-user-for-a-customer.md) A törlést és az "inaktívként" megjelölt felhasználói fiókot a rendszer már nem a felhasználói gyűjtemény tagjaként visszaadja (például egy ügyfél összes felhasználói fiókjának lekért [listáját használva).](get-a-list-of-all-user-accounts-for-a-customer.md) A törölt, még nem véglegesen törölt felhasználók listájának lekérdezéséhez le kellkérdeznie az inaktívra beállított felhasználói fiókokat.

## <a name="c"></a>C\#

A törölt felhasználók listájának lekéréséhez állítson össze egy olyan lekérdezést, amely az inaktív állapotú ügyfelekre szűr. Először hozza létre a szűrőt egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektum példányosulatával a paraméterekkel az alábbi kódrészletben látható módon. Ezután hozza létre a lekérdezést a [**BuildIndexedQuery metódussal.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) Ha nem szeretne lapozott eredményeket, használhatja helyette a [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódust. Ezután használja az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával az ügyfél azonosításához. Végül hívja meg [**a Query metódust**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) a kérés elküldéhez.

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

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** GetCustomerInactiveUsers.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/users?size={size}&filter={filter} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A kérelem létrehozásakor használja a következő elérési utat és lekérdezési paramétereket.

| Név        | Típus   | Kötelező | Leírás                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ügyfél-azonosító | guid   | Yes      | Az érték egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.                                                                                                            |
| size        | int    | No       | Az egyszerre megjelenítendő eredmények száma. Ezt a paramétert nem kötelező megadni.                                                                                                     |
| filter (szűrő)      | filter (szűrő) | Yes      | A felhasználókeresést szűrő lekérdezés. A törölt felhasználók lekéréséhez bele kell foglalnia és kódolnia kell a következő sztringet: {"Field":"UserState","Value":"Inactive","Operator":"equals"}. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha a művelet sikeres, ez a metódus [CustomerUser-erőforrások](user-resources.md#customeruser) gyűjteményét adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
