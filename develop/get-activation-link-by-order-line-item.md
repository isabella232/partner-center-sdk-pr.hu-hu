---
title: Aktiválási hivatkozás lekérése megrendelési sorelem alapján
description: Lekért egy előfizetés-aktiválási hivatkozást rendeléssorelem alapján.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: aa02a5a5b4a281b96e32ee6d239cc440cf8af4ec
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760776"
---
# <a name="get-activation-link-by-order-line-item"></a>Aktiválási hivatkozás lekérése megrendelési sorelem alapján

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Lekért egy kereskedelmi piactéri előfizetés aktiválási hivatkozását a rendelési sor tételszáma alapján.

Az Partnerközpont-irányítópulton ezt a műveletet úgy használhatja, hogy  kiválaszt egy adott előfizetést **az** Előfizetés alatt a főoldalon, vagy az  Előfizetések lapon az aktiválni kívánt előfizetés melletti Ugrás az **Publisher** webhelyre hivatkozást.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.

- Kész rendelés az aktiválni szükséges termékkel.

## <a name="c"></a>C\#

Egy sorelem aktiválási hivatkozásának lehívásához használja az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a kiválasztott ügyfél-azonosítóval. Ezután hívja meg [**az Orders tulajdonságot**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) és a [**ById() metódust**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) a megadott [**OrderId értékével.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id) Ezután hívja meg a [**LineItems metódust**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) **a ById() metódussal** és a sortételszám azonosítóját.  Végül hívja meg az **ActivationLinks() metódust.**

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus ügyfélerőforrások [gyűjteményét](customer-resources.md#customer) adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 809
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT
{
  "totalCount": 1,
  "items": [
    {
      "lineItemNumber": 0,
      "link": {
        "uri": "<link populated here>",
        "method": "GET",
        "headers": [

        ]
      }
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```
