---
title: Önkiszolgáló házirend frissítése
description: Önkiszolgáló házirend frissítése.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4d53ab8e5b8ef5b7be83360a3f43ec7791b2e3b4
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/08/2020
ms.locfileid: "97768668"
---
# <a name="update-a-selfservepolicy"></a>SelfServePolicy frissítése

**A következőkre vonatkozik:**

- Partnerközpont

Ez a témakör az önkiszolgáló szabályzatok frissítését ismerteti.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja az Application + felhasználói hitelesítő adatokkal történő hitelesítést.

## <a name="c"></a>C\#

Önkiszolgáló házirend törlése:

1. Hívja meg a [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metódust az entitás-azonosítóval, és kérje le a házirendek műveleteire szolgáló felületet.

2. A saját kiszolgálási szabályzat frissítéséhez hívja meg a [**put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) vagy a [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) metódust.

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                       |
|----------|-------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy http/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

- A kérelem azonosítójának és korrelációs azonosítójának megadása kötelező.
- További információért lásd a [partneri központ Rest-fejléceit](headers.md) .

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.

| Név                              | Típus   | Leírás                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)| object | Az önkiszolgáló házirend adatai. |

#### <a name="selfservepolicy"></a>SelfServePolicy

Ez a táblázat ismerteti az új önkiszolgáló házirend létrehozásához szükséges [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -erőforrás minimálisan szükséges mezőit.

| Tulajdonság              | Típus             | Leírás                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sztring           | Önkiszolgáló házirend-azonosító, amelyet az önkiszolgáló házirend sikeres létrehozásakor kell megadni.     |
| SelfServeEntity       | SelfServeEntity  | Az önkiszolgáló entitás, amely hozzáférést kap.                                                     |
| Megadó fél               | Megadó fél          | A hozzáférést biztosító biztosító.                                                                    |
| Engedélyek           | Engedély tömbje| [Engedélyezési](self-serve-policy-resources.md#permission) erőforrások tömbje.                                                      |
| ETAG                  | sztring           | A ETAG.                                                                                               |


### <a name="request-example"></a>Példa kérésre

```http
PUT https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive

{
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
}
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez az API egy [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -erőforrást ad vissza a frissített önkiszolgáló házirendhez.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód     | Hibakód   | Leírás                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | Az önkiszolgáló házirend nem található                                            |
| 404                  | 600040       | Az önkiszolgáló házirend-azonosító helytelen                                  |


### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 Ok
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
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
        "etag": "\"1ec98034-a249-46f4-b9dd-9cd464fb5e47\"",
        "objectType": "SelfServePolicy"
    }
}
```
