---
title: Önkiszolgáló szabályzat törlése
description: Önkiszolgáló szabályzat törlése.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 063cf98d4c78e82622e486427baeb1a5721715e5
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973094"
---
# <a name="delete-a-selfservepolicy"></a>SelfServePolicy törlése

Ez a cikk az önkiszolgáló szabályzatok frissítését ismerteti.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az Application+User hitelesítő adatokkal történő hitelesítést.

## <a name="c"></a>C\#

Önkiszolgáló szabályzat törlése:

1. Hívja meg az [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metódust az entitásazonosítóval, hogy lekérje a szabályzatok műveleteinek interfészét.

2. Az [**önkiszolgáló**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) szabályzat törléséhez hívja meg a Delete vagy [**a DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) metódust.

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

Példaként tekintse meg a következőket:

- Minta: [Konzoltesztalkalmazás](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Osztály: **DeleteSelfServePolicies.cs**

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Töröl** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1 |

**URI-paraméter**

Az alábbi elérésiút-paraméterek használatával szerezze be a megadott terméket.

| Név                       | Típus         | Kötelező | Leírás                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| **SelfServePolicy-id**     | **sztring**   | Igen      | Az önkiszolgáló szabályzatot azonosító sztring.                 |

### <a name="request-headers"></a>Kérésfejlécek

- Szükség van egy kérésazonosítóra és egy korrelációs azonosítóra.
- További információ: [REST Partnerközpont fejlécek.](headers.md)

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

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
