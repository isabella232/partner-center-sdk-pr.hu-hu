---
title: Ügyfélrendelés létrehozása közvetett viszonteladó számára
description: Megtudhatja, hogyan hozhat létre rendelést egy közvetett viszonteladó ügyfele számára a Partnerközpont API-k használatával. A cikk előfeltételeket, lépéseket és példákat tartalmaz.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba46b151e423df27f1378ac8441a23702e47746911b4e05e370bbf0aa7b53233
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991548"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>Megrendelés létrehozása közvetett viszonteladó ügyfelének

Rendelés létrehozása egy közvetett viszonteladó ügyfele számára.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- A megvásárolni kívánt tétel ajánlatazonosítója.

- A közvetett viszonteladó bérlőazonosítója.

## <a name="c"></a>C\#

Megrendelés létrehozása egy közvetett viszonteladó ügyfele számára:

1. Szerezze be a bejelentkezett partnerrel kapcsolatban áll közvetett viszonteladók gyűjteményét.

2. Lekért egy helyi változót a gyűjteménynek arra az elemére, amely megegyezik a közvetett viszonteladó azonosítójával. Ez a lépés segít elérni a viszonteladó [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) tulajdonságát a rendelés létrehozásakor.

3. Példányositsa az [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) objektumot, és állítsa a [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) tulajdonságot az ügyfélazonosítóra az ügyfél rögzítéséhez.

4. Hozza létre az [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objektumok listáját, és rendelje hozzá a listát a rendelés [**LineItems (Soritemek) tulajdonságához.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) Minden rendeléssorelem egy adott ajánlat vásárlási adatait tartalmazza. A [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) tulajdonságot minden sorelemben töltse fel a közvetett viszonteladó MPN-azonosítójával. Legalább egy megrendeléssor-elemnek kell lennie.

5. Szerezzen be egy interfészt a műveletek megrendelésére az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódus ügyfél-azonosítóval való hívásával az ügyfél azonosításához, majd a felület az Orders tulajdonságból [**való lekérésével.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)

6. A rendelés [**létrehozásához**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) hívja meg a Create vagy [**a CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) metódust.

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

**Minta:** [Konzoltesztelő](console-test-app.md)**alkalmazás Project:** Partnerközpont SDK Samples **Class**: PlaceOrderForCustomer.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Az ügyfél azonosításához használja a következő elérésiút-paramétert.

| Név        | Típus   | Kötelező | Leírás                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ügyfélazonosító | sztring | Yes      | Egy GUID formátumú sztring, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

#### <a name="order"></a>Sorrend

Ez a táblázat a kérelem törzsében található **Order (Rendelés)** tulajdonságokat ismerteti.

| Név | Típus | Kötelező | Leírás |
| ---- | ---- | -------- | ----------- |
| id | sztring | No | A rendelés sikeres létrehozása után megadott rendelésazonosító. |
| referenceCustomerId | sztring | Yes | Az ügyfél azonosítója. |
| billingCycle | sztring | No | A rendelés számlázásának gyakorisága a partner számára. Az alapértelmezett érték a Havi, és a rendelés &quot; sikeres létrehozása után lesz &quot; alkalmazva. A támogatott értékek a [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype)típusban található tagnevek. Megjegyzés: Az éves számlázási funkció még nem általánosan elérhető. Az éves számlázás támogatása hamarosan meg fog rövidni. |
| lineItems (sorsorok) | objektumok tömbje | Yes | [**OrderLineItem-erőforrások tömbje.**](#orderlineitem) |
| creationDate (Létrehozás dátuma) | sztring | No | A rendelés létrehozási dátuma, dátum-idő formátumban. A rendelés sikeres létrehozása után alkalmazva. |
| Attribútumok | object | No | Tartalmazza az "ObjectType": "Order" típust. |

#### <a name="orderlineitem"></a>OrderLineItem (Megrendelési vonal)

Ez a táblázat a kérelem törzsében található **OrderLineItem** tulajdonságokat ismerteti.

| Név | Típus | Kötelező | Leírás |
| ---- | ---- | -------- | ----------- |
| lineItemNumber (sor száma) | int | Yes | A gyűjtemény minden soreleme egyedi sorszámot kap, amely 0-tól count-1-ig számol. |
| offerId (ajánlatazonosító) | sztring | Yes | Az ajánlat azonosítója. |
| subscriptionId | sztring | No | Az előfizetés azonosítója. |
| parentSubscriptionId (parentSubscriptionId) | sztring | No | Választható. A szülő-előfizetés azonosítója egy bővítményajánlatban. Csak a PATCH-re vonatkozik. |
| friendlyName (rövid név) | sztring | No | Választható. A partner által meghatározott előfizetés rövid neve, amely segít egyértelműsedni. |
| quantity | int | Yes | A licencalapú előfizetések licenceinek száma. |
| partnerIdOnRecord | sztring | No | Ha egy közvetett szolgáltató egy közvetett viszonteladó nevében ad ki rendelést, akkor ezt a mezőt csak a közvetett viszonteladó MPN-azonosítójával **töltse** fel (soha ne a közvetett szolgáltató azonosítójával). Ez biztosítja az ösztönzők megfelelő elszámolását. **Ha nem adja meg a viszonteladó MPN-azonosítóját, a rendelés nem fog meghiúsulni. A viszonteladót azonban nem rögzíti a rendszer, ezért előfordulhat, hogy az ösztönzők számításai nem tartalmazzák az értékesítést.** |
| Attribútumok | object | No | Az "ObjectType":"OrderLineItem" adatokat tartalmazza. |

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

Ha a művelet sikeres, a válasz törzse tartalmazza a kitöltve [order erőforrást.](order-resources.md)

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

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
