---
title: Az önkiszolgáló szabályzatok listájának lekért listája
description: Az ügyfél önkiszolgáló szabályzatát képviselő erőforrások gyűjteményének lekért gyűjtése.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ce217e34090d589c07a49cd51abef3f5cfc010631088890324a63bdef1480f65
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995526"
---
# <a name="get-a-list-of-self-serve-policies"></a>Az önkiszolgáló szabályzatok listájának lekért listája

Lekérte az entitás önkiszolgáló szabályzatának megfelelő erőforrások gyűjteményét.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az Application+User hitelesítő adatokkal történő hitelesítést.

## <a name="c"></a>C\#

Az összes önkiszolgáló szabályzat listájának lekért listája:

1. Hívja meg az [**IAggregatePartner.SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) metódust az entitásazonosítóval, hogy lekérje a szabályzatok műveleteinek interfészét.

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// gets the self-serve policies
var SelfServePolicies = scopedPartnerOperations.SelfServePolicies.Get(customerIdAsEntity);
```

Példaként tekintse meg a következőket:

- Minta: [Konzoltesztalkalmazás](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Osztály: **GetSelfServePolicies.cs**

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy?entity_id={entity_id} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

Az alábbi lekérdezési paraméterrel lekérdezheti az ügyfelek listáját.

| Név          | Típus       | Kötelező | Leírás                                        |
|---------------|------------|----------|----------------------------------------------------|
| **entity_id** | **sztring** | Y        | A hozzáférést kérő entitásazonosító. Ez lesz az ügyfél bérlőazonosítója. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [Fejlécek.](headers.md)

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

Ha ez a metódus sikeres, a válasz törzsében [visszaadja a SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) erőforrások gyűjteményét.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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
