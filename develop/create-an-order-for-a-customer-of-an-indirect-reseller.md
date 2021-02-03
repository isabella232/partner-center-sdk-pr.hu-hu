---
title: Vevői rendelés létrehozása közvetett viszonteladóhoz
description: Ismerje meg, hogy a partner Center API-k segítségével hogyan hozhat létre rendelést egy közvetett viszonteladó ügyfelének. A cikk az előfeltételeket, a lépéseket és a Exmaples tartalmazza.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f72ecec8d82e6b8a1bc53c277206cafd7d8a4e03
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768636"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>Megrendelés létrehozása közvetett viszonteladó ügyfelének

**A következőkre vonatkozik:**

- Partnerközpont

Megrendelést hozhat létre egy közvetett viszonteladó ügyfelének.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- A megvásárolni kívánt tétel ajánlatának azonosítója.

- A közvetett viszonteladó bérlői azonosítója.

## <a name="c"></a>C\#

Egy közvetett viszonteladó ügyfelének rendelésének létrehozása:

1. Szerezze be azon közvetett viszonteladók gyűjteményét, akik kapcsolatban vannak a bejelentkezett partnerrel.

2. Szerezzen be egy helyi változót a gyűjtemény azon eleméhez, amely megfelel a közvetett viszonteladói AZONOSÍTÓnak. Ez a lépés segít a viszonteladó [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) tulajdonságának elérésében a rendelés létrehozásakor.

3. Hozzon létre egy [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) objektumot, és állítsa az [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) tulajdonságot az ügyfél-azonosítóra, hogy rögzítse az ügyfelet.

4. Hozza létre a [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) -objektumok listáját, és rendelje hozzá a listát a rendelés [**listaelemek**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) tulajdonságához. Az egyes rendelési sorok egy adott ajánlat vásárlási információit tartalmazzák. Ügyeljen arra, hogy az egyes sorokban található [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) tulajdonságot a közvetett viszonteladó MPN-azonosítójával feltöltse. Legalább egy Order line-elemmel kell rendelkeznie.

5. Szerezzen be egy felületet a megrendelési műveletekhez úgy, hogy meghívja a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához, majd lekéri a felületet a [**megrendelések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) tulajdonságból.

6. Hívja meg a [**create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) metódust a rendelés létrehozásához.

### <a name="c-example"></a>C \# példa

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Minta**: [Console test app](console-test-app.md)**Project**: a partner Center SDK Samples **osztálya**: PlaceOrderForCustomer.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders http/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Az ügyfél azonosításához használja a következő Path paramétert.

| Név        | Típus   | Kötelező | Leírás                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ügyfél-azonosító | sztring | Igen      | Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

#### <a name="order"></a>Sorrend

Ez a tábla a kérelem törzsének **Order (rendelés** ) tulajdonságait ismerteti.

| Név | Típus | Kötelező | Leírás |
| ---- | ---- | -------- | ----------- |
| id | sztring | No | A megrendelés sikeres létrehozásakor megadott rendelési azonosító. |
| referenceCustomerId | sztring | Igen | Az ügyfél-azonosító. |
| billingCycle | sztring | No | Az a gyakoriság, amellyel a partnert számlázzák a rendelésért. Az alapértelmezett érték &quot; havonta történik &quot; , és a rendszer a megrendelés sikeres létrehozása után alkalmazza. A támogatott értékek a [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype)található tagok nevei. Megjegyzés: az éves számlázási funkció még nem általánosan elérhető. Az éves számlázási támogatás hamarosan elérhető lesz. |
| Listaelemek | objektumok tömbje | Igen | [**OrderLineItem**](#orderlineitem) -erőforrások tömbje. |
| creationDate | sztring | No | A rendelés létrehozásának dátuma dátum-idő formátumban. A megrendelés sikeres létrehozása után alkalmazható. |
| attribútumok | object | Nem | A "objektumtípus": "Order" kifejezést tartalmazza. |

#### <a name="orderlineitem"></a>OrderLineItem

Ez a táblázat a kérelem törzsének **OrderLineItem** tulajdonságait ismerteti.

| Név | Típus | Kötelező | Leírás |
| ---- | ---- | -------- | ----------- |
| lineItemNumber | int | Igen | A gyűjtemény minden egyes sora egy egyedi sorszámot kap, amely a 0 és Count-1 közötti számlálást eredményezi. |
| offerId | sztring | Igen | Az ajánlat azonosítója. |
| subscriptionId | sztring | No | Az előfizetés azonosítója. |
| parentSubscriptionId | sztring | No | Választható. A szülő-előfizetés azonosítója egy kiegészítő ajánlatban. Csak a JAVÍTÁSra vonatkozik. |
| friendlyName | sztring | No | Választható. A partner által az előfizetéshez megadott rövid név, amely segít a egyértelműsítse. |
| quantity | int | Igen | A licenc alapú előfizetéshez tartozó licencek száma. |
| partnerIdOnRecord | sztring | No | Ha egy közvetett szolgáltató egy megrendelést helyez el egy közvetett viszonteladó nevében, töltse ki ezt a mezőt a **közvetett viszonteladóhoz** tartozó MPN-azonosítóval (soha nem a közvetett szolgáltató azonosítója). Ez biztosítja az ösztönzők megfelelő könyvelését. **Nem sikerült megadni a viszonteladói MPN-azonosítót, mert a rendelés sikertelen lesz. Azonban a viszonteladó nem kerül rögzítésre, és a következményi ösztönző számítások nem tartalmazzák az értékesítést.** |
| attribútumok | object | Nem | A "objektumtípus": "OrderLineItem" kifejezést tartalmazza. |

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
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

Ha a művelet sikeres, a válasz törzse tartalmazza a feltöltött [megrendelés](order-resources.md) erőforrását.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```
