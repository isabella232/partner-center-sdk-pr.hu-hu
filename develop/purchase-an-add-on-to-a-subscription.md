---
title: Bővítmény vásárlása egy előfizetéshez
description: Bővítmény vásárlása meglévő előfizetéshez.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 975a2516bccdc6274bfec5d6a3286a649fc4f808
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768312"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>Bővítmény vásárlása egy előfizetéshez

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud for US Government Partnerközpontja

Bővítmény vásárlása meglévő előfizetéshez.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító. Ezt a meglévő előfizetést kell megvásárolnia.

- A megvásárolni kívánt bővítményt azonosító ajánlat azonosítója.

## <a name="purchasing-an-add-on-through-code"></a>Kiegészítő csomag megvásárlása kód használatával

Ha hozzáad egy bővítményt egy előfizetéshez, az eredeti előfizetési rendelést a bővítmény sorrendjével frissíti. A következő példában a Vevőkód az ügyfél-azonosító, a subscriptionId az előfizetés azonosítója, a addOnOfferId pedig a bővítmény ajánlatának azonosítója.

A lépések a következők:

1.  Adapter beszerzése az előfizetés műveleteihez.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Használja ezt a felületet egy előfizetési objektum létrehozásához. Így megkapja a szülő-előfizetés részleteit, beleértve a megrendelés azonosítóját is.

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Új [**megrendelési**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) objektum létrehozása Ez a megrendelési példány az előfizetés megvásárlásához használt eredeti megrendelés frissítésére szolgál. Vegyen fel egy egysoros tételt a bővítményt jelölő sorrendbe.
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

4.  Frissítse az előfizetés eredeti sorrendjét a bővítmény új sorrendjével.
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

Egy bővítmény megvásárlásához először az [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust kell beszereznie az ügyfél-azonosítóval, és az [**előfizetések. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódussal kell megadnia azt az előfizetést, amely a kiegészítő ajánlattal rendelkezik. Ezzel a [**csatolóval**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) kérheti le az előfizetés részleteit a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get)utasítás meghívásával. Miért van szüksége az előfizetés részleteire? Mivel szüksége van az előfizetési rendeléshez tartozó Order ID azonosítóra. Ez a bővítmény frissítésének sorrendje.

Ezután hozza létre az új [**megrendelési**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) objektumot, és töltse fel egyetlen [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) -példánnyal, amely tartalmazza a bővítmény azonosítására szolgáló adatokat, ahogy az a következő kódrészletben látható. Ezzel az új objektummal frissítheti az előfizetési sorrendet a bővítmény használatával. Végül hívja meg a [**patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) metódust az előfizetési sorrend frissítéséhez, miután először azonosítja az ügyfelet a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) és a Orders [**. ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).

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

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: AddSubscriptionAddOn.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus    | Kérés URI-ja                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **JAVÍTÁS** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

A következő paraméterek használatával azonosíthatja az ügyfelet és a sorrendet.

| Név                   | Típus     | Kötelező | Leírás                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **ügyfél – bérlő – azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlő-azonosító** , amely azonosítja az ügyfelet. |
| **megrendelés azonosítója**           | **guid** | Y        | A sorrend azonosítója.                                                              |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

A következő táblázatok a kérés törzsének tulajdonságait ismertetik.

## <a name="order"></a>Sorrend

| Név                | Típus             | Kötelező | Leírás                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | sztring           | N        | A megrendelés azonosítója.                                        |
| ReferenceCustomerId | sztring           | Y        | Az ügyfél-azonosító.                                     |
| Listaelemek           | objektumok tömbje | Y        | [OrderLineItem](#orderlineitem) objektumok tömbje. |
| CreationDate        | sztring           | N        | A rendelés létrehozásának dátuma dátum-idő formátumban. |
| Attribútumok          | object           | N        | A "objektumtípus": "Order" kifejezést tartalmazza.                      |

## <a name="orderlineitem"></a>OrderLineItem

| Név                 | Típus   | Kötelező | Leírás                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber       | szám | Y        | A sor elemének száma, a 0-tól kezdődően.                       |
| OfferId              | sztring | Y        | A bővítmény ajánlatának azonosítója.                                  |
| SubscriptionId       | sztring | N        | A megvásárolt bővítmény-előfizetés azonosítója.                 |
| ParentSubscriptionId | sztring | Y        | Annak a szülő-előfizetésnek az azonosítója, amelyhez a kiegészítő ajánlat tartozik. |
| FriendlyName         | sztring | N        | A sorhoz tartozó rövid név                        |
| Mennyiség             | szám | Y        | A licencek száma.                                      |
| PartnerIdOnRecord    | sztring | N        | A rekord partnerének MPN-azonosítója.                         |
| Attribútumok           | object | N        | A "objektumtípus": "OrderLineItem" kifejezést tartalmazza.                      |

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

Ha ez sikeres, a metódus visszaadja a frissített előfizetés sorrendjét a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).

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
