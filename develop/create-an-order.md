---
title: Ügyfél rendelésének létrehozása
description: Megtudhatja, hogyan hozhat létre rendelést egy ügyfél számára a partner Center API-k használatával. A cikk előfeltételeket, lépéseket és példákat tartalmaz.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ce176909a1f9c350f1c16615171de57a7beb888d
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768624"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a>Megrendelés létrehozása egy ügyfél számára a partner Center API-k használatával

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud for US Government Partnerközpontja

Az Azure-beli **fenntartott VM-példányok termékeinek rendelése** *csak* a következőkre vonatkozik:

- Partnerközpont

További információ a jelenleg elérhető értékesítésről: [partneri ajánlatok a Cloud Solution Provider programban](/partner-center/csp-offers).

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Egy ajánlat azonosítója.

## <a name="c"></a>C\#

Megrendelés létrehozása az ügyfél számára:

1. Hozzon létre egy [**Order**](order-resources.md) objektumot, és állítsa a **ReferenceCustomerID** tulajdonságot az ügyfél-azonosítóra az ügyfél rögzítéséhez.

2. Hozza létre a [**OrderLineItem**](order-resources.md#orderlineitem) -objektumok listáját, és rendelje hozzá a listát a rendelés **listaelemek** tulajdonságához. Az egyes rendelési sorok egy adott ajánlat vásárlási információit tartalmazzák. Legalább egy Order line-elemmel kell rendelkeznie.

3. Szerezzen be egy illesztőfelületet a rendelési műveletekhez. Először hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához. Ezután kérje le a felületet az [**orders (megrendelések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) ) tulajdonságból.

4. Hívja meg a [**create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) metódust, és adja meg a [**sorrend**](order-resources.md) objektumot.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: CreateOrder.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders http/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Az ügyfél azonosításához használja a következő Path paramétert.

| Név        | Típus   | Kötelező | Leírás                                                |
|-------------|--------|----------|------------------------------------------------------------|
| ügyfél-azonosító | sztring | Igen      | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

#### <a name="order"></a>Sorrend

Ez a tábla a kérelem törzsének [Order (rendelés](order-resources.md) ) tulajdonságait ismerteti.

| Tulajdonság             | Típus                        | Kötelező                        | Leírás                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| id                   | sztring                      | No                              | A megrendelés sikeres létrehozásakor megadott rendelési azonosító.   |
| referenceCustomerId  | sztring                      | No                              | Az ügyfél-azonosító. |
| billingCycle         | sztring                      | No                              | Azt jelzi, hogy milyen gyakorisággal történik a partner számlázása ebben a sorrendben. A támogatott értékek a [BillingCycleType](product-resources.md#billingcycletype)található tagok nevei. Az alapértelmezett érték a "havonta" vagy az "egykori" a megrendelés létrehozásakor. Ez a mező a megrendelés sikeres létrehozásakor lesz alkalmazva. |
| Listaelemek            | [OrderLineItem](order-resources.md#orderlineitem) -erőforrások tömbje | Igen      | Az ügyfél által megvásárolt ajánlatok részletezett listája, beleértve a mennyiséget is.        |
| currencyCode         | sztring                      | No                              | Csak olvasható. A megrendelés elhelyezésekor használt pénznem. A megrendelés sikeres létrehozása után alkalmazható.           |
| creationDate         | dátum/idő                    | Nem                              | Csak olvasható. A rendelés létrehozásának dátuma dátum-idő formátumban. A megrendelés sikeres létrehozása után alkalmazható.                                   |
| status               | sztring                      | No                              | Csak olvasható. A megrendelés állapota.  A támogatott értékek a [OrderStatus](order-resources.md#orderstatus)található tagok nevei.        |
| linkek                | [OrderLinks](utility-resources.md#resourcelinks)              | Nem                              | A rendelésnek megfelelő erőforrás-hivatkozások. |
| attribútumok           | [ResourceAttributes](utility-resources.md#resourceattributes) | Nem                              | A sorrendnek megfelelő metaadat-attribútumok. |

#### <a name="orderlineitem"></a>OrderLineItem

Ez a táblázat a kérelem törzsének [OrderLineItem](order-resources.md#orderlineitem) tulajdonságait ismerteti.

>[!NOTE]
>A partnerIdOnRecord csak akkor adható meg, ha egy közvetett szolgáltató egy közvetett viszonteladó nevében rendezi a rendelést. A rendszer a közvetett viszonteladó Microsoft Partner Network-AZONOSÍTÓját tárolja (soha nem a közvetett szolgáltató AZONOSÍTÓját).

| Név                 | Típus   | Kötelező | Leírás                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int    | Igen      | A gyűjtemény minden egyes sora egy egyedi sorszámot kap, amely a 0 és Count-1 közötti számlálást eredményezi.                                                                                                                                                 |
| offerId              | sztring | Igen      | Az ajánlat azonosítója.                                                                                                                                                                                                                      |
| subscriptionId       | sztring | No       | Az előfizetés azonosítója.                                                                                                                                                                                                               |
| parentSubscriptionId | sztring | No       | Választható. A szülő-előfizetés azonosítója egy kiegészítő ajánlatban. Csak a JAVÍTÁSra vonatkozik.                                                                                                                                                     |
| friendlyName         | sztring | No       | Választható. A partner által az előfizetéshez megadott rövid név, amely segít a egyértelműsítse.                                                                                                                                              |
| quantity             | int    | Igen      | A licenc alapú előfizetéshez tartozó licencek száma.                                                                                                                                                                                   |
| partnerIdOnRecord    | sztring | No       | Ha egy közvetett szolgáltató egy megrendelést helyez el egy közvetett viszonteladó nevében, töltse ki ezt a mezőt a **közvetett viszonteladóhoz** tartozó MPN-azonosítóval (soha nem a közvetett szolgáltató azonosítója). Ez biztosítja az ösztönzők megfelelő könyvelését. |
| provisioningContext  | Szótár<karakterlánc, karakterlánc>                | Nem       |  A katalógus egyes elemeinek kiépítési feladataihoz szükséges információk. Az SKU provisioningVariables tulajdonsága azt jelzi, hogy mely tulajdonságok szükségesek a katalógus adott elemeihez.                  |
| linkek                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | Nem       |  Csak olvasható. A rendelési sorhoz tartozó erőforrás-hivatkozások.  |
| attribútumok           | [ResourceAttributes](utility-resources.md#resourceattributes) | Nem       | A OrderLineItem megfelelő metaadat-attribútumok. |
| renewsTo             | Objektumok tömbje                          | Nem    |[RenewsTo](order-resources.md#renewsto) -erőforrások tömbje.                                                                            |

##### <a name="renewsto"></a>RenewsTo

Ez a táblázat a kérelem törzsének [RenewsTo](order-resources.md#renewsto) tulajdonságait ismerteti.

| Tulajdonság              | Típus             | Kötelező        | Leírás |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | sztring           | No              | A megújítási időszak érvényességének ISO 8601-es ábrázolása. A jelenleg támogatott értékek a következők: **P1M** (1 hónap) és **P1Y** (1 év). |

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a metódus egy [Order](order-resources.md) erőforrást ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
