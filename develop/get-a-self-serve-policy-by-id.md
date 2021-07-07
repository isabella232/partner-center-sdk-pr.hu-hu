---
title: Önkiszolgáló szabályzat lekért azonosítója
description: Lekérte a megadott önkiszolgáló szabályzatot az azonosítójával.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 074d7ba65c7aab91687a67f50e871cee913fc2bb
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873836"
---
# <a name="get-a-self-serve-policy-by-id"></a>Önkiszolgáló szabályzat lekért azonosítója

Lekérte a megadott önkiszolgáló szabályzatot az azonosítójával.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.
- Egy önkiszolgáló szabályzatazonosító.

## <a name="examples"></a>Példák


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST-kérés

**Kérés szintaxisa**

| Metódus  | Kérés URI-ja                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1 |

**URI-paraméter**

A megadott termék lekért értékével az alábbi elérésiút-paramétereket használhatja.

| Név                       | Típus         | Kötelező | Leírás                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| **SelfServePolicy-id**     | **sztring**   | Igen      | Az önkiszolgáló szabályzatot azonosító sztring.                 |

**Kérelemfejlécek**

- További információ: [Fejlécek.](headers.md)

**Kérelem törzse**

Nincsenek.

**Példa kérésre**

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse tartalmaz egy [SelfServePolicy erőforrást.](self-serve-policy-resources.md#selfservepolicy)

**Sikeres válasz és hibakódok**

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód     | Hibakód   | Leírás                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | Az önkiszolgáló szabályzat nem található.                                                     |

**Példa válaszra**

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

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