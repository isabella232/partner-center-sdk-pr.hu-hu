---
title: Közvetett viszonteladó ügyfeleinek lekérése
description: Egy közvetett viszonteladó ügyfeleinek listájának lekért listája.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e05248b16b803529258de806c25b117f3104ad2a
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446326"
---
# <a name="get-customers-of-an-indirect-reseller"></a>Közvetett viszonteladó ügyfeleinek lekérése

Egy közvetett viszonteladó ügyfeleinek listájának lekért listája.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- A közvetett viszonteladó bérlőazonosítója.

## <a name="c"></a>C\#

Ha olyan ügyfelek gyűjteményét kell lekérte, akik kapcsolatban vannak a megadott közvetett viszonteladóval, először hozzon létre egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumot a szűrő létrehozásához. A [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumerálás tagját át kell adni egy sztringgé, és a szűrőművelet típusaként meg kell adni a [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) mezőt. Meg kell adnia annak a közvetett viszonteladónak a bérlőazonosítóját is, amely alapján szűrni tud.

Ezután példányosított egy [**iQuery-objektumot,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) amelyet átadhat a lekérdezésnek a [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódus hívásával és a szűrő átadásával. A BuildSimplyQuery csak egy a [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) osztály által támogatott lekérdezéstípusok közül.

A szűrő végrehajtásához és az eredmény lekért végrehajtásához először az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) használatával szerezze be a partner ügyfélműveletei interfészét. Ezután hívja meg a [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) vagy [**a QueryAsync metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)

Ha létre kell hoznia egy enumerátort a lapozó eredmények bejárása érdekében, szerezze be az ügyfélgyűjtemény enumerátor-előállító felületét az [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) tulajdonságból, majd hívja meg a [**Létrehozás**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create)függvényt az alábbi kódban látható módon, az ügyfélgyűjteményt tartalmazó változó átadásával.

``` csharp
IAggregatePartner partnerOperations;
string indirectResellerId;

// Create a filter.
var filter = new SimpleFieldFilter(
    CustomerSearchField.IndirectReseller.ToString(),
    FieldFilterOperation.StartsWith,
    indirectResellerId);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(filter);

// Get the collection of matching customers.
var customersPage = partnerOperations.Customers.Query(myQuery);

// Create a customer enumerator for traversing the customer pages.
var customersEnumerator = partnerOperations.Enumerators.Customers.Create(customersPage);
int pageNumber = 1;

while (customersEnumerator.HasValue)
{
    // Work with the current page.
     foreach (var c in customersEnumerator.Current.Items)
    {
        // Display customer tenant identifier and company name.
        Console.WriteLine(string.Format("{0} - {1}.",c.Id,c.CompanyProfile.CompanyName));
    }
    // Get the next page of customers.
    customersEnumerator.Next();
}
```

**Minta:** [Konzoltesztelő](console-test-app.md)**alkalmazás Project:** Partnerközpont SDK Samples **Osztály:** GetCustomersOfIndirectReseller.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A kérelem létrehozásához használja a következő lekérdezési paramétereket.

| Név   | Típus   | Kötelező | Leírás                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| size   | int    | Nem       | Az egyszerre megjelenítendő eredmények száma. Ezt a paramétert nem kötelező megadni.                                                                                                                                                                                                                |
| filter (szűrő) | filter (szűrő) | Igen      | A keresést szűrő lekérdezés. Egy adott közvetett viszonteladó ügyfeleinek lekéréséhez be kell szúrni a közvetett viszonteladó azonosítóját, és bele kell foglalnia és kódolnia kell a következő sztringet: {"Field":"IndirectReseller","Value":"{közvetett viszonteladó-azonosító}","Operátor":"kezdete"}. \_ |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example-encoded"></a>Példakérés (kódolt)

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a>Példa kérése (dekódolva)

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha a válasz törzse sikeres, a viszonteladó ügyfeleivel kapcsolatos információkat tartalmaz.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 2273
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: XI2/vIHmIEGVlGL9.0
MS-ServerId: 101112012
Date: Tue, 11 Apr 2017 23:31:28 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
            "companyProfile": {
                "tenantId": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                "domain": "FourthCoffee137.onmicrosoft.com",
                "companyName": "FourthCoffee137",
                "links": {
                    "self": {
                        "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
            "companyProfile": {
                "tenantId": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                "domain": "WingtipToys1254789149.onmicrosoft.com",
                "companyName": "Wingtip Toys1254789149",
                "links": {
                    "self": {
                        "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        },
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
