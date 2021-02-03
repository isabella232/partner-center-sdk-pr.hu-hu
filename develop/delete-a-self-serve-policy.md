---
title: Önkiszolgáló szabályzat törlése
description: Önkiszolgáló házirend törlése.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3450145d6daf2ffca5e2886245e592406cb0886d
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/08/2020
ms.locfileid: "97768656"
---
# <a name="delete-a-selfservepolicy"></a>SelfServePolicy törlése

**A következőkre vonatkozik:**

- Partnerközpont

Ez a témakör az önkiszolgáló szabályzatok frissítését ismerteti.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja az Application + felhasználói hitelesítő adatokkal történő hitelesítést.

## <a name="c"></a>C\#

Önkiszolgáló házirend törlése:

1. Hívja meg a [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metódust az entitás-azonosítóval, és kérje le a házirendek műveleteire szolgáló felületet.

2. Az önkiszolgáló házirend törléséhez hívja meg a [**delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) vagy a [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) metódust.

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

Példaként tekintse meg a következőket:

- Minta: [konzol tesztelési alkalmazás](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Osztály: **DeleteSelfServePolicies.cs**

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                   |
|---------|-------------------------------------------------------------------------------|
| **TÖRLÉSE** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{ID} http/1.1 |

**URI-paraméter**

A megadott termék beolvasásához használja a következő elérésiút-paramétereket.

| Név                       | Típus         | Kötelező | Leírás                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| **SelfServePolicy-azonosító**     | **karakterlánc**   | Igen      | Az önkiszolgáló házirendet azonosító karakterlánc.                 |

### <a name="request-headers"></a>Kérésfejlécek

- A kérelem AZONOSÍTÓjának és korrelációs AZONOSÍTÓjának megadása kötelező.
- További információért lásd a [partneri központ Rest-fejléceit](headers.md) .

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
DELETE https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 789
Connection: Keep-Alive

```

## <a name="rest-response"></a>REST-válasz

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
