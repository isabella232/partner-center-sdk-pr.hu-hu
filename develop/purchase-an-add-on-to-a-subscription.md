---
title: Bővítmény vásárlása egy előfizetéshez
description: Bővítmény vásárlása meglévő előfizetéshez.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d8b700a2ad41a37ca0ad745f3e7767449974b18a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547682"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>Bővítmény vásárlása egy előfizetéshez

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont a Microsoft Cloud for US Government

Bővítmény vásárlása meglévő előfizetéshez.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító. Ez az a meglévő előfizetés, amelyhez bővítményajánlatot szeretne vásárolni.

- Egy ajánlatazonosító, amely azonosítja a vásárolható bővítményajánlatot.

## <a name="purchasing-an-add-on-through-code"></a>Bővítmény vásárlása kóddal

Amikor bővítményt vásárol egy előfizetéshez, az eredeti előfizetési rendelést a bővítmény rendelésével frissíti. A következőben a customerId az ügyfél azonosítója, a subscriptionId az előfizetés azonosítója, az addOnOfferId pedig a bővítmény ajánlatazonosítója.

A lépések a következők:

1.  Felület lekérte az előfizetés műveleteihez.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Ezzel a felülettel példányosithat egy előfizetési objektumot. Ez lekérte a szülő-előfizetés adatait, beleértve a rendelés azonosítóját is.

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Új Order objektum [**példányosodása.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) Ezzel a rendelési példánysal frissítheti az előfizetés megvásárlásához használt eredeti rendelést. Adjon hozzá egy egysoros elemet a bővítményt képviselő sorrendhez.
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  Frissítse az előfizetés eredeti rendelését a bővítmény új rendelésével.
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

Bővítmény vásárlásához először szerezzen be egy felületet az előfizetési műveletekhez. Ehhez hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához, és a [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust a bővítményajánlattal kapcsolatos előfizetés azonosításához. Ezen a [**felületen**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) lekérhetőek az előfizetés részletei a [**Get hívása segítségével.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get) Az előfizetés részletei tartalmazzák az előfizetési rendelés rendelésazonosítóját, amely a bővítménysel frissíthető rendelés.

Ezután példányosítsa az új [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) objektumot, és töltse fel egyetlen [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) példáncával, amely tartalmazza a bővítmény azonosításához szükséges információkat, ahogyan az alábbi kódrészletben látható. Ezzel az új objektummal frissítheti az előfizetési rendelést a bővítmény használatával. Végül hívja meg a [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) metódust az előfizetési rendelés frissítéséhez, miután először azonosította az ügyfelet az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) azonosítóval, a rendelést pedig [**az Orders.ById azonosítóval.**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **osztály:** AddSubscriptionAddOn.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus    | Kérés URI-ja                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **Javítás** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{rendelésazonosító} HTTP/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

A következő paraméterekkel azonosíthatja az ügyfelet és a megrendelést.

| Név                   | Típus     | Kötelező | Leírás                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely azonosítja az ügyfelet. |
| **rendelésazonosító**           | **guid** | Y        | A rendelés azonosítója.                                                              |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Az alábbi táblázatok a kérelem törzsében lévő tulajdonságokat ismertetik.

## <a name="order"></a>Sorrend

| Név                | Típus             | Kötelező | Leírás                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | sztring           | N        | A rendelés azonosítója.                                        |
| ReferenceCustomerId (ReferenciacustomerId) | sztring           | Y        | Az ügyfél azonosítója.                                     |
| Sorsorok           | objektumok tömbje | Y        | [OrderLineItem objektumok tömbje.](#orderlineitem) |
| CreationDate (Létrehozás dátuma)        | sztring           | N        | A rendelés létrehozási dátuma, dátum-idő formátumban. |
| Attribútumok          | object           | N        | Tartalmazza az "ObjectType": "Order" típust.                      |

## <a name="orderlineitem"></a>OrderLineItem (Megrendelési vonal)

| Név                 | Típus   | Kötelező | Leírás                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber (Sor száma)       | szám | Y        | A sorelem száma, 0-val kezdve.                       |
| OfferId (Ajánlatazonosító)              | sztring | Y        | A bővítmény ajánlatazonosítója.                                  |
| SubscriptionId       | sztring | N        | A megvásárolt bővítmény-előfizetés azonosítója.                 |
| ParentSubscriptionId (Szülő-előíróazonosító) | sztring | Y        | Annak a szülő előfizetésnek az azonosítója, amely a bővítményajánlattal rendelkezik. |
| FriendlyName (Rövid név)         | sztring | N        | A sorelem rövid neve.                        |
| Mennyiség             | szám | Y        | A licencek száma.                                      |
| PartnerIdOnRecord    | sztring | N        | A rekordpartner MPN-azonosítója.                         |
| Attribútumok           | object | N        | Tartalmazza az "ObjectType": "OrderLineItem" adatokat.                      |

### <a name="request-example"></a>Példa kérésre

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
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
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

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [hibakódok.](error-codes.md)

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
    "billingCycle": "none",
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
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
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
