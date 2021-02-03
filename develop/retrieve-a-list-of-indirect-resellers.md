---
title: Közvetett viszonteladók listájának lekérése
description: A bejelentkezett partner közvetett viszonteladói listájának beolvasása.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e53237b97fa26d3a987f0ee7de491084b596af4a
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768399"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>Közvetett viszonteladók listájának lekérése

**A következőkre vonatkozik**

- Partnerközpont

A bejelentkezett partner közvetett viszonteladói listájának beolvasása.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="c"></a>C\#

Azon közvetett viszonteladók listájának lekéréséhez, akikkel a bejelentkezett partnernek van kapcsolata, először szerezzen be egy felületet a kapcsolat gyűjtési műveleteihez a [**partnerOperations. kapcsolatok**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) tulajdonságból. Ezután hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) vagy a [**Get \_ aszinkron**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) metódust, amely a [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) enumerálás egy tagját továbbítja a kapcsolat típusának azonosításához. A közvetett viszonteladók beolvasásához a IsIndirectCloudSolutionProviderOf-t kell használnia.

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**Minta**: [Console test app](console-test-app.md)**Project**: a partner Center SDK Samples **osztálya**: GetIndirectResellers.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Relationships? kapcsolat \_ típusa = IsIndirectCloudSolutionProviderOf http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A kapcsolat típusának azonosításához használja a következő lekérdezési paramétert.

| Név               | Típus    | Kötelező  | Leírás                         |
|--------------------|---------|-----------|-------------------------------------|
| relationship_type  | sztring  | Igen       | Az érték a [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype)található egyik tag nevének karakterláncos ábrázolása.<br/><br/> Ha a partner be van jelentkezve szolgáltatóként, és szeretné lekérni azon közvetett viszonteladók listáját, akikkel kapcsolatot létesítettek, használja a IsIndirectCloudSolutionProviderOf.<br/><br/> Ha a partnert viszonteladóként jelentkezett be, és szeretné lekérni azon közvetett szolgáltatók listáját, akikkel kapcsolatot létesítettek, használja a IsIndirectResellerOf-t.    |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

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

Ha ez sikeres, a válasz törzse [PartnerRelationship](relationships-resources.md) -erőforrások gyűjteményét tartalmazza a viszonteladók azonosításához.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).

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