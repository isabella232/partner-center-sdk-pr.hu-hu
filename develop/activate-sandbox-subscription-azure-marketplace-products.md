---
title: Sandbox-előfizetés aktiválása kereskedelmi piactéri termékekhez
description: Megtudhatja, hogyan használhatja a C/# és a Partnerközpont REST API-kat a kereskedelmi piactéri termékekhez való sandbox-előfizetés aktiválásához.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1ea581695e4328f02d08486c91b7b90a78e75a50985279d78cc54ef8b35fa715
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990494"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a>Sandbox-előfizetés aktiválása kereskedelmi piactéri SaaS-termékekhez a számlázás engedélyezéséhez

Előfizetés aktiválása kereskedelmi piactéri szolgáltatott szoftver (SaaS) termékekhez integrációs sandbox-fiókokból a számlázás engedélyezéséhez.

> [!NOTE]
> Előfizetést csak a kereskedelmi piactéri SaaS-termékekhez lehet aktiválni az integrációs sandbox-fiókokból. Ha éles üzemre vonatkozó előfizetéssel rendelkezik, a telepítési folyamat befejezéséhez meg kell jelennie a közzétevő webhelyén. Az előfizetés számlázása csak a telepítés befejezése után kezdődik meg.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Integrációs védőfali partnerfiók egy olyan ügyféllel, aki aktív előfizetéssel rendelkezik a kereskedelmi piactéri SaaS-termékekhez.

- A .NET SDK Partnerközpont t használó partnereknek az SDK 1.14.0-s vagy újabb verzióját kell használniuk a funkció eléréséhez.

## <a name="c"></a>C\#

A kereskedelmi piactéri SaaS-termékek előfizetésének aktiválásához kövesse az alábbi lépéseket:

1. Tegye elérhetővé az előfizetési műveletek felületét. Azonosítania kell az ügyfelet, és meg kell adnia a próba-előfizetés előfizetés-azonosítóját.

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. Aktiválja az előfizetést az Aktiválás **művelettel.**

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
| **ügyfél-bérlő-azonosító** | **guid** | Y | Az érték egy GUID-formátumú ügyfél bérlőazonosítója (**ügyfél-bérlő-azonosító),** amely lehetővé teszi az ügyfél megadását. |
| **subscription-id** | **guid** | Y | Az érték egy GUID formátumú előfizetés-azonosító (**subscription-id**), amely lehetővé teszi egy előfizetés megadását. |

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

Ez a metódus visszaadja **az előfizetés-azonosító és** az **állapot tulajdonságait.**

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
