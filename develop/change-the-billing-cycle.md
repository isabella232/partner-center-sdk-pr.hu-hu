---
title: A számlázási ciklus módosítása
description: Megtudhatja, hogyan frissítheti az ügyfél-előfizetést havi vagy éves számlázásra az Partnerközpont API-k használatával. Ezt az irányítópulton Partnerközpont is.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: c45d599ace7895c03bc163cddde7cbb057ff60a06c58af39a2baacb3d557e72e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992160"
---
# <a name="change-a-customer-subscription-billing-cycle"></a>Ügyfél-előfizetés számlázási ciklusának módosítása

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Frissíti a [rendelést](order-resources.md) haviról éves vagy évesről havi számlázásra.

A Partnerközpont ezt a műveletet az ügyfél előfizetési adatait tartalmazó oldalra navigálva hajthatja végre. Itt fog látni egy lehetőséget, amely meghatározza az előfizetés aktuális számlázási ciklusát, és lehetővé teszi a váltást és a küldést.

**Ez a cikk nem** terjed ki a cikkre:

- Próbaverziók számlázási ciklusának módosítása
- Az Azure-előfizetések nem éves (havi, hat éves) időszakra vonatkozó számlázási ciklusainak & módosítása
- Inaktív előfizetések számlázási ciklusainak módosítása
- A Microsoft licencalapú előfizetések online szolgáltatások számlázási ciklusainak módosítása

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy rendelésazonosító.

## <a name="c"></a>C\#

A számlázási ciklus gyakoriságának változásához frissítse az [**Order.BillingCycle tulajdonságot.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle)

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

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus    | Kérés URI-ja                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **Javítás** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{rendelésazonosító} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja az előfizetés mennyiségének változásához szükséges lekérdezési paramétert.

| Név                   | Típus | Kötelező | Leírás                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | GUID |    Y     | Egy GUID formátumú **ügyfél-bérlőazonosító,** amely azonosítja az ügyfelet |
| **order-id (rendelésazonosító)**           | GUID |    Y     | A rendelés azonosítója                                                 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Az alábbi táblázatok a kérelem törzsében lévő tulajdonságokat ismertetik.

### <a name="order"></a>Sorrend

| Tulajdonság           | Típus             | Kötelező | Leírás                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | sztring           |    N     | A rendelés sikeres létrehozása után megadott rendelésazonosító |
|ReferenceCustomerId (ReferenciacustomerId) | sztring           |    Y     | Az ügyfél azonosítója                                                    |
| BillingCycle       | sztring           |    Y     | Azt jelzi, hogy milyen gyakorisággal számlázták a partnert a rendelésért. A támogatott értékek a [BillingCycleType](product-resources.md#billingcycletype)típusban található tagnevek. |
| Sorsorok          | objektumok tömbje |    Y     | [OrderLineItem-erőforrások tömbje](#orderlineitem)                      |
| CreationDate (Létrehozás dátuma)       | dátum/idő         |    N     | A rendelés létrehozási dátuma dátum és idő formátumban                        |
| Attribútumok         | Objektum           |    N     | Tartalmazza az "ObjectType": "OrderLineItem" adatokat                                     |

### <a name="orderlineitem"></a>OrderLineItem (Megrendelési vonal)

| Tulajdonság             | Típus   | Kötelező | Leírás                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber (Sortem száma)       | szám |    Y     | A sortétel száma, 0-val kezdve                                              |
| OfferId (Ajánlatazonosító)              | sztring |    Y     | Az ajánlat azonosítója                                                                |
| SubscriptionId       | sztring |    Y     | Az előfizetés azonosítója                                                         |
| FriendlyName (Rövid név)         | sztring |    N     | A partner által meghatározott előfizetés rövid neve, amely segít egyértelműsen |
| Mennyiség             | szám |    Y     | Licencek vagy példányok száma                                                |
| PartnerIdOnRecord    | sztring |    N     | A rekordpartner MPN-azonosítója                                                |
| Attribútumok           | Objektum |    N     | Tartalmazza az "ObjectType": "OrderLineItem" adatokat                                             |

### <a name="request-example"></a>Példa kérésre

Frissítés éves számlázásra

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

Ha a művelet sikeres, ez a metódus a válasz törzsében adja vissza a frissített előfizetési sorrendet.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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