---
title: Önkiszolgáló szabályzatok listájának beolvasása
description: Az ügyfél önkiszolgáló házirendjeit képviselő erőforrások gyűjteményének beszerzése.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ff3116b8757e28e03615930ebd19bc75f34e2efe
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/08/2020
ms.locfileid: "97768664"
---
# <a name="get-a-list-of-self-serve-policies"></a>Önkiszolgáló szabályzatok listájának beolvasása

**A következőkre vonatkozik:**

- Partnerközpont

Ez a cikk azt ismerteti, hogyan szerezhet be olyan erőforrás-gyűjteményt, amely az entitások önkiszolgáló házirendjeit jelképezi.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja az Application + felhasználói hitelesítő adatokkal történő hitelesítést.

## <a name="c"></a>C\#

Az összes önkiszolgáló házirend listájának lekérése:

1. Hívja meg a [**IAggregatePartner. SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) metódust az entitás-azonosítóval, és kérje le a szabályzatok műveleteihez szükséges felületet.

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// gets the self-serve policies
var SelfServePolicies = scopedPartnerOperations.SelfServePolicies.Get(customerIdAsEntity);
```

Példaként tekintse meg a következőket:

- Minta: [konzol tesztelési alkalmazás](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Osztály: **GetSelfServePolicies.cs**

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                   |
|---------|-------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy? entity_id = {ENTITY_ID} http/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

Használja az alábbi lekérdezési paramétert az ügyfelek listájának lekéréséhez.

| Név          | Típus       | Kötelező | Leírás                                        |
|---------------|------------|----------|----------------------------------------------------|
| **entity_id** | **karakterlánc** | Y        | A számára hozzáférést kérő entitás azonosítója. Ez lesz az ügyfél bérlői azonosítója. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [fejlécek](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy?entity_id=0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -erőforrások gyűjteményét adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 1,
    "items": [{
        "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
        "selfServeEntity": {
            "selfServeEntityType": "customer",
            "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
        },
        "grantor": {
            "grantorType": "billToPartner",
            "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
        },
        "permissions": [{
            "resource": "AzureReservedInstances",
            "action": "Purchase"
        }],
        "attributes": {
            "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
            "objectType": "SelfServePolicy"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
