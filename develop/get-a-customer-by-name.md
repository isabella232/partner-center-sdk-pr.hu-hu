---
title: Az ügyfelek listájának lekérése keresési mező alapján szűrve
description: Egy szűrőnek megfelelő ügyfél-erőforrások gyűjteményét kéri le. Igény szerint beállíthatja az oldalméret méretét. A szűrést vállalat neve, tartomány, közvetett viszonteladó vagy közvetett felhőalapú megoldás-szolgáltató (CSP) alapján végezheti el.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: aad9524dbe2c9edbbd7c1d50da7a448f6872fcb9
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768124"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a>Az ügyfelek listájának lekérése keresési mező alapján szűrve

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Egy szűrőnek megfelelő [ügyfél](customer-resources.md#customer) -erőforrások gyűjteményét kéri le. Igény szerint beállíthatja az oldalméret méretét. A szűrést vállalat neve, tartomány, közvetett viszonteladó vagy közvetett felhőalapú megoldás-szolgáltató (CSP) alapján végezheti el.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Felhasználó által létrehozott szűrő.

## <a name="c"></a>C\#

Egy szűrőnek megfelelő ügyfelek gyűjteményének lekéréséhez először hozzon létre egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumot a szűrő létrehozásához. Meg kell adnia egy karakterláncot, amely tartalmazza a [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), és a szűrési művelet típusát adja meg [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation)néven. Ez az egyetlen, az ügyfelek végpontja által támogatott szűrési művelet. Emellett meg kell adnia a szűréshez használandó karakterláncot is.

Ezután hozza létre a [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) objektumot a lekérdezésnek való átadáshoz. ehhez hívja meg a [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódust, és adja át a szűrőt. A BuildSimplyQuery csak az [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) osztály által támogatott lekérdezések egyike.

Végül, a szűrő végrehajtásához és az eredmény beszerzéséhez először használja a [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) felületet a partner ügyfél-műveleteihez. Ezután hívja meg a [**lekérdezés**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) vagy a [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) metódust.

``` csharp
IAggregatePartner partnerOperations;

// Specify the partial string to filter by (to match Contoso).
string searchPrefix = "cont"

// Create a simple field filter.
var fieldFilter = new SimpleFieldFilter(
    CustomerSearchField.CompanyName.ToString(),
    FieldFilterOperation.StartsWith,
    searchPrefix);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(fieldFilter);

// Get the collection of matching customers.
var customers = partnerOperations.Customers.Query(myQuery);
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: FilterCustomers.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? méret = {size} &szűrő = {Filter} http/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

Használja a következő lekérdezési paramétereket.

| Név   | Típus   | Kötelező | Leírás                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| size   | int    | Nem       | Az egyszerre megjelenítendő eredmények száma. Ezt a paramétert nem kötelező megadni. |
| filter (szűrő) | filter (szűrő) | Igen      | Az ügyfelekre alkalmazandó szűrő. Ennek kódolású sztringnek kell lennie.              |

### <a name="filter-syntax"></a>Szűrési szintaxis

A Filter paramétert vesszővel elválasztott, kulcs-érték párokból álló sorozatként kell összeállítani. Minden kulcsot és értéket külön kell megadni, és kettősponttal kell elválasztani őket. A teljes szűrőt kódolni kell.

A kódolás nélküli példa a következőképpen néz ki:

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

A következő táblázat a szükséges kulcs-érték párokat ismerteti:

| Kulcs      | Érték                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| Mező    | A szűrni kívánt mező. Az érvényes értékek a [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)-ben találhatók. |
| Érték    | A szűréshez használandó érték. A rendszer figyelmen kívül hagyja az érték esetét.                                                                |
| Operátor | Az alkalmazni kívánt operátor. Ez az ügyfél-forgatókönyv egyetlen támogatott értéke a "kezdete \_ ".                            |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22CompanyName%22%2C%22Value%22%3A%22Cont%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5ce66de5-eea9-486f-a11c-c852aa3d1502
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus a válasz törzsében lévő [ügyfél](customer-resources.md#customer) -erőforrások egyező gyűjteményét adja vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 1839
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
MS-RequestId: dfeda56c-1af5-43fc-a9c0-346b9e85dc96
MS-CV: n0lMNyJtaUC802pO.0
MS-ServerId: 202010223
Date: Fri, 24 Feb 2017 22:08:20 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "c5757d70-06f3-4f23-8367-5a9e55019f94",
            "companyProfile": {
                "tenantId": "c5757d70-06f3-4f23-8367-5a9e55019f94",
                "domain": "contoso190.onmicrosoft.com",
                "companyName": "Contoso190",
                "links": {
                    "self": {
                        "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94/profiles/company",
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
                    "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
            "companyProfile": {
                "tenantId": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                "domain": "ContosoCorpCo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d/profiles/company",
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
                    "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
            "companyProfile": {
                "tenantId": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                "domain": "contosocorpdemo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b/profiles/company",
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
                    "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers?size=0&filter=%7B%22Field%22%3A%22Domain%22%2C%22Value%22%3A%22cont%22%2C%22Operator%22%3A%22starts_with%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
