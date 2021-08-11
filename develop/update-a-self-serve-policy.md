---
title: Önkiszolgáló szabályzat frissítése
description: Önkiszolgáló szabályzat frissítése.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8e1330de6655e7a4dbe2d7432ece208b4600f3659266e20199e729400a917771
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996631"
---
# <a name="update-a-selfservepolicy"></a>SelfServePolicy frissítése

Ez a cikk az önkiszolgáló szabályzatok frissítését ismerteti.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az Application+User hitelesítő adatokkal történő hitelesítést.

## <a name="c"></a>C\#

Önkiszolgáló szabályzat törlése:

1. Hívja meg az [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metódust az entitásazonosítóval, hogy lekérje a szabályzatok műveleteinek interfészét.

2. Az önkiszolgáló szabályzat frissítéséhez hívja meg a [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) vagy [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) metódust.

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus   | Kérés URI-ja                                                       |
|----------|-------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

- Szükség van egy kérelem- és korrelációs azonosítóra.
- További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.

| Név                              | Típus   | Description                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)| object | Az önkiszolgáló szabályzat adatai. |

#### <a name="selfservepolicy"></a>SelfServePolicy

Ez a táblázat az új önkiszolgáló szabályzat létrehozásához szükséges [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) erőforrás minimálisan szükséges mezőit ismerteti.

| Tulajdonság              | Típus             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sztring           | Önkiszolgáló szabályzatazonosító, amely az önkiszolgáló szabályzat sikeres létrehozása után lesz megadva.     |
| SelfServeEntity       | SelfServeEntity  | Az önkiszolgáló entitás, amely hozzáférést kap.                                                     |
| Grantor               | Grantor          | A hozzáférést megadó megadó.                                                                    |
| Engedélyek           | Engedélytömb| [Engedélyerőforrások tömbje.](self-serve-policy-resources.md#permission)                                                      |
| Etag                  | sztring           | Az Etag.                                                                                               |


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

Ha ez az API sikeres, egy [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) erőforrást ad vissza a frissített önkiszolgáló szabályzathoz.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód     | Hibakód   | Description                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | Az önkiszolgáló szabályzat nem található                                            |
| 404                  | 600040       | Az önkiszolgáló szabályzatazonosító helytelen                                  |


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
