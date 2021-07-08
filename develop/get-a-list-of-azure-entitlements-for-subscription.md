---
title: Egy előfizetés Azure-jogosultsági listájának lekérése
description: Az AzureEntitlement erőforrással lekért Azure-jogosultságú erőforrások gyűjteményét, amelyek egy előfizetéshez tartoznak.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 280da155122ed9efd99838d7819fb34f8f7ec52c
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874363"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a>Egy előfizetés Azure-jogosultsági listájának lekérése

Az [Azure-jogosultsági](subscription-resources.md#azureentitlement) erőforrás **(AzureEntitlement**) használatával egy előfizetéshez tartozó erőforrások gyűjteményét kaphatja meg.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/azureentitlements HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Az alábbi táblázat felsorolja az előfizetés összes Azure-jogosultságának lekérdezhető lekérdezési paramétereit.

| Név                   | Típus     | Kötelező | Leírás                           |
|------------------------|----------|----------|---------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az ügyfélnek megfelelő GUID. |
| **subscription-id**       | **guid** | Y        | Az előfizetéshez tartozó GUID.    |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus [**azureentitlement-erőforrások**](subscription-resources.md#azureentitlement) gyűjteményét adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 04 Oct 2019 05:50:45 GMT

{
"totalCount":1,
"items":[
  {
    "id":"899ae6f1-8a74-4d5e-b6c6-e6b5019bbff8",
    "friendlyName":"Microsoft Azure",
    "status":"active",
    "subscriptionId":"3f15978e-005c-b763-bb78-2a8fab289c58"
   }],
    "attributes":{"objectType":"Collection"}
  }
```
