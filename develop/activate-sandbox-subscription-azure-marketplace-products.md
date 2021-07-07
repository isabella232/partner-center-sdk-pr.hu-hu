---
title: Sandbox-előfizetés aktiválása kereskedelmi piactéri termékekhez
description: Megtudhatja, hogyan használhatja a C/# és a Partnerközpont REST API-kat a kereskedelmi piactéri termékekre vonatkozó sandbox-előfizetések aktiválásához.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b32c3e87462f58218771fc5da7da56ed177489cb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025700"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a>Sandbox-előfizetés aktiválása kereskedelmi piactéri SaaS-termékekhez a számlázás engedélyezéséhez

Előfizetés aktiválása kereskedelmi piactéri szolgáltatott szoftver (SaaS) termékekhez integrációs sandbox-fiókokból a számlázás engedélyezéséhez.

> [!NOTE]
> A kereskedelmi piactéri SaaS-termékek előfizetését csak integrációs sandbox-fiókokból lehet aktiválni. Ha éles üzemre vonatkozó előfizetéssel rendelkezik, a telepítési folyamat befejezéséhez meg kell látogatnia a közzétevő webhelyét. Az előfizetés számlázása csak a beállítás befejezése után kezdődik meg.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.

- Integrációs sandbox partnerfiók egy olyan ügyféllel, aki aktív előfizetéssel rendelkezik a kereskedelmi piactéri SaaS-termékekhez.

- A .NET SDK Partnerközpont t használó partnereknek az SDK 1.14.0-s vagy újabb verzióját kell használniuk a funkció eléréséhez.

## <a name="c"></a>C\#

A kereskedelmi piactéri SaaS-termékek előfizetésének aktiválásához kövesse az alábbi lépéseket:

1. Tegye elérhetővé az előfizetési műveletek felületét. Azonosítania kell az ügyfelet, és meg kell adnia a próba-előfizetés előfizetés-azonosítóját.

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. Aktiválja az előfizetést az **Aktiválás művelettel.**

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus     | Kérés URI-ja                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/activate HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y | Az érték egy GUID-formátumú ügyfél bérlőazonosítója **(ügyfél-bérlő-azonosító),** amely lehetővé teszi az ügyfél megadását. |
| **subscription-id** | **guid** | Y | Az érték egy GUID-formátumú előfizetés-azonosító **(előfizetés-azonosító),** amely lehetővé teszi egy előfizetés megadását. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a>REST-válasz

Ez a metódus visszaadja **az előfizetés-azonosító és az** állapot **tulajdonságait.**

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
