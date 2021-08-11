---
title: Az ügyfelek listájának lekérése keresési mező alapján szűrve
description: Lekért egy szűrőnek megfelelő ügyfélerőforrás-gyűjteményt. Igény szerint meg is állíthatja az oldalméretet. Szűrhet vállalatnév, tartomány, közvetett viszonteladó vagy közvetett felhőszolgáltató (CSP) alapján.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 4e77edd3e7d94711ad18796c0afb4db30c50abf0bc9636335b413a5d41dff9c8
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993095"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a>Az ügyfelek listájának lekérése keresési mező alapján szűrve

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Lekért egy [szűrőnek](customer-resources.md#customer) megfelelő ügyfélerőforrás-gyűjteményt. Igény szerint meg is állíthatja az oldalméretet. Szűrhet vállalatnév, tartomány, közvetett viszonteladó vagy közvetett felhőszolgáltató (CSP) alapján.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.

- Felhasználó által felépített szűrő.

## <a name="c"></a>C\#

A szűrőnek megfelelő ügyfelek gyűjteményének lekért létrehozásához először hozzon létre egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumot. A [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)mezőt tartalmazó sztringet kell átadnia, és a szűrőművelet típusát [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation)értékkel kell jeleznie. Ez az egyetlen mezőszűrő művelet, amelyet az ügyfelek végpontja támogat. A szűréshez meg kell adnia a sztringet is.

Ezután példányosított [**egy iQuery-objektumot**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) a lekérdezésnek való átadáshoz a [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódus hívásával és a szűrő átadásával. A BuildSimplyQuery csak egy a [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) osztály által támogatott lekérdezéstípusok közül.

Végül a szűrő végrehajtásához és az eredmény lekért eredményéhez először használja az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) metódust, hogy lekért egy felületet a partner ügyfélműveleteihez. Ezután hívja meg a [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) vagy [**a QueryAsync metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)

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

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK Samples **Class**: FilterCustomers.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

Használja az alábbi lekérdezési paramétereket.

| Név   | Típus   | Kötelező | Leírás                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| size   | int    | No       | Az egyszerre megjelenítendő eredmények száma. Ezt a paramétert nem kötelező megadni. |
| filter (szűrő) | filter (szűrő) | Yes      | Az ügyfelekre alkalmazandó szűrő. Ennek kódolt sztringnek kell lennie.              |

### <a name="filter-syntax"></a>Szűrőszintaxis

A szűrőparamétert vesszővel tagolt kulcs-érték párok sorozataként kell összerakni. Minden kulcsot és értéket külön kell idézni, és kettősponttal kell elválasztani egymástól. A teljes szűrőt kódolni kell.

Egy nem kódolatlan példa a következő:

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

Az alábbi táblázat a szükséges kulcs-érték párokat ismerteti:

| Kulcs      | Érték                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| Mező    | A szűrni való mező. Az érvényes értékek a [**CustomerSearchField mezőben találhatók.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) |
| Érték    | A szűrési érték. A rendszer figyelmen kívül hagyja az érték kis- és nagyját.                                                                |
| Operátor | Az alkalmazandó operátor. Ebben az ügyfélforgatókönyvben az egyetlen támogatott érték a \_ "kezdete".                            |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha ez a módszer sikeres, a válasz törzsében egyező [Ügyfél-erőforrások](customer-resources.md#customer) gyűjteményét adja vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
