---
title: A számlázási ciklus módosítása
description: Megtudhatja, hogyan frissítheti az ügyfél-előfizetést havi vagy éves számlázásra a partner Center API-k használatával. Ezt a partner Center irányítópultján is elvégezheti.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 8a2879db061ced799e29d84e71be5b1259b07689
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768600"
---
# <a name="change-a-customer-subscription-billing-cycle"></a>Ügyfél-előfizetés számlázási ciklusának módosítása

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Havonta és évenkénti számlázással, vagy éves és havi számlázással frissíti a [rendelést](order-resources.md) .

A partneri központ irányítópultján ez a művelet az ügyfél előfizetésének részleteit tartalmazó oldalra navigálva végezhető el. Ekkor megjelenik egy lehetőség, amely meghatározza az előfizetés aktuális számlázási ciklusát, amely lehetővé teszi a módosítást és a beküldést.

A cikk **Hatókörön kívüli** :

- A számlázási ciklus módosítása a próbaverziók esetében
- A számlázási ciklusok bármely nem éves időszakra vonatkozó ajánlatának módosítása (havi, 6 éves) & Azure-előfizetések
- Az inaktív előfizetések számlázási ciklusának módosítása
- Számlázási ciklusok módosítása a Microsoft online szolgáltatások licenc-alapú előfizetésekhez

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Egy megrendelés azonosítója.

## <a name="c"></a>C\#

A számlázási ciklus gyakoriságának módosításához frissítse a [**Order. BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) tulajdonságot.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus    | Kérés URI-ja                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **JAVÍTÁS** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja a szükséges lekérdezési paramétert az előfizetés mennyiségének módosításához.

| Név                   | Típus | Kötelező | Leírás                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| **ügyfél – bérlő – azonosító** | GUID |    Y     | Az ügyfelet azonosító, formázott **ügyfél-bérlői azonosító** |
| **megrendelés azonosítója**           | GUID |    Y     | A megrendelés azonosítója                                                 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

A következő táblázatok a kérés törzsének tulajdonságait ismertetik.

### <a name="order"></a>Sorrend

| Tulajdonság           | Típus             | Kötelező | Leírás                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | sztring           |    N     | A megrendelés sikeres létrehozásakor megadott rendelési azonosító |
|ReferenceCustomerId | sztring           |    Y     | Az ügyfél azonosítója                                                    |
| BillingCycle       | sztring           |    Y     | Azt jelzi, hogy milyen gyakorisággal történik a partner számlázása ebben a sorrendben. A támogatott értékek a [BillingCycleType](product-resources.md#billingcycletype)található tagok nevei. |
| Listaelemek          | objektumok tömbje |    Y     | [OrderLineItem](#orderlineitem) -erőforrások tömbje                      |
| CreationDate       | dátum/idő         |    N     | A rendelés létrehozásának dátuma dátum-idő formátumban                        |
| Attribútumok         | Objektum           |    N     | A "objektumtípus": "OrderLineItem" kifejezést tartalmazza                                     |

### <a name="orderlineitem"></a>OrderLineItem

| Tulajdonság             | Típus   | Kötelező | Leírás                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber       | szám |    Y     | A sor sorszáma, kezdő és 0                                              |
| OfferId              | sztring |    Y     | Az ajánlat azonosítója                                                                |
| SubscriptionId       | sztring |    Y     | Az előfizetés azonosítója                                                         |
| FriendlyName         | sztring |    N     | A partner által az előfizetéshez megadott rövid név, amely segít a egyértelműsítse |
| Mennyiség             | szám |    Y     | A licencek vagy példányok száma                                                |
| PartnerIdOnRecord    | sztring |    N     | A rekord partnerének MPN-azonosítója                                                |
| Attribútumok           | Objektum |    N     | A "objektumtípus": "OrderLineItem" kifejezést tartalmazza                                             |

### <a name="request-example"></a>Példa kérésre

Frissítés az éves számlázásra

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a metódus visszaadja a frissített előfizetés sorrendjét a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "Annual",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```