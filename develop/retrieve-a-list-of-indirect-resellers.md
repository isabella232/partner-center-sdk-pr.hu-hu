---
title: Közvetett viszonteladók listájának lekérése
description: A bejelentkezett partner közvetett viszonteladói listájának lekérése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 901bf045d1de29744114bb58ed445f9eb17f70a4744786fd4617da9697e7c683
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996920"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>Közvetett viszonteladók listájának lekérése

A bejelentkezett partner közvetett viszonteladói listájának lekérése.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="c"></a>C\#

Azon közvetett viszonteladók listájának lekéréséhez, akikkel a bejelentkezett partner kapcsolatban áll, először szerezze be a [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) tulajdonságból a kapcsolatgyűjtési műveletek felületét. Ezután hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) vagy [**Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) metódust, és adja át a [**PartnerRelationshipType enumerálás**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) egyik tagját a kapcsolattípus azonosításához. Közvetett viszonteladók lekérése az IsIndirectCloudSolutionProviderOf használatával oldható meg.

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**Minta:** [Konzoltesztelő alkalmazás](console-test-app.md)**Project:** Partnerközpont SDK Samples **Osztály:** GetIndirectResellers.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship \_ type=IsIndirectCloudSolutionProviderOf HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A kapcsolattípus azonosításához használja a következő lekérdezési paramétert.

| Név               | Típus    | Kötelező  | Leírás                         |
|--------------------|---------|-----------|-------------------------------------|
| relationship_type  | sztring  | Yes       | Az érték a [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype)típusban található egyik tagnév sztringes ábrázolása.<br/><br/> Ha a partner szolgáltatóként van bejelentkezve, és le szeretné kapni azon közvetett viszonteladók listáját, akikkel kapcsolatot létrehoztak, használja az IsIndirectCloudSolutionProviderOf használhatja.<br/><br/> Ha a partner viszonteladóként van bejelentkezve, és le szeretné kapni azon közvetett szolgáltatók listáját, akikkel kapcsolatot létrehoztak, használja az IsIndirectResellerOf használhatja.    |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha a válasz törzse sikeres, a [partnerreláció](relationships-resources.md) erőforrásainak gyűjteményét tartalmazza a viszonteladók azonosításához.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a [hibakódok Partnerközpont tekintse meg.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 298
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CV: b21Ll1miM0yFMPQQ.0
MS-ServerId: 030020643
Date: Wed, 05 Apr 2017 21:08:44 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847383",
            "location": "US",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }, {
            "id": "b01b1487-b36e-4e6d-9b5e-0b58974c4b28",
            "name": "ReleCloud",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847433",
            "location": "BR",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```