---
title: Egy ügyfél közvetett viszonteladóinak lekérése
description: Azon közvetett viszonteladók listájának lekérte, akik kapcsolatban vannak egy adott ügyféllel.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 8697c40c22d5c19979c066b8d3a1de733e211f71
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446241"
---
# <a name="get-indirect-resellers-of-a-customer"></a>Egy ügyfél közvetett viszonteladóinak lekérése

Azon közvetett viszonteladók listájának lekérte, akik kapcsolatban vannak egy adott ügyféllel.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Azon közvetett viszonteladók listájának lekéréséhez, akikkel a megadott ügyfél kapcsolatban áll, először szerezze be a [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) tulajdonságból az ügyfél azonosítóját az ügyfél azonosításához. Ezután hívja meg [**a Relationships.Get vagy**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) [**a Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) metódust a közvetett viszonteladók listájának lehívásához.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

**Minta:** [Konzoltesztelő](console-test-app.md)**alkalmazás Project:** Partnerközpont SDK Samples **Class:** GetIndirectResellersOfCustomer.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/kapcsolatok HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az ügyfél azonosításához használja a következő elérésiút-paramétert.

| Név        | Típus   | Kötelező | Leírás                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ügyfélazonosító | sztring | Igen      | Egy GUID formátumú sztring, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha a válasz törzse sikeres, a [partnerreláció](relationships-resources.md) erőforrásainak gyűjteményét tartalmazza a viszonteladók azonosításához.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 264
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CV: plJP3ufU0UqXMeuh.0
MS-ServerId: 020021921
Date: Fri, 07 Apr 2017 23:42:11 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "mpnId": "4847383",
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
