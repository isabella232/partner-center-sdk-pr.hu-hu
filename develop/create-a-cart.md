---
title: Kosár létrehozása
description: Ismerje meg, hogy a partner Center API-k Hogyan vehetik igénybe az ügyfelek rendelését egy kosárban. A témakör a kosár létrehozásával és az előfeltételekkel kapcsolatos információkat tartalmaz.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a1c559b415a7d42af4e904e09795f92aed7f125f
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768627"
---
# <a name="create-a-cart-with-a-customer-order"></a>Kosár létrehozása az ügyfél megrendelésével

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Megrendelést adhat egy kosárban lévő ügyfélhez. További információ az értékesítésre jelenleg elérhető termékekről: [partneri ajánlatok a Cloud Solution Provider programban](/partner-center/csp-offers).

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Megrendelés létrehozása az ügyfél számára:

1. Egy cart-objektum példányának létrehozása.

2. Hozza létre a **CartLineItem** -objektumok listáját, és rendelje hozzá a listát a kosár listaelemek tulajdonságához. Minden egyes cart-sor egy termék vásárlási információit tartalmazza. Legalább egy cart-sorral kell rendelkeznie.

3. Szerezzen be egy felületet a cart-műveletekhez úgy, hogy meghívja a **IAggregatePartner. customers. ById** metódust az ügyfél-azonosítóval, hogy azonosítsa az ügyfelet, majd beolvassa a felületet a **cart** tulajdonságból.

4. A kosár létrehozásához hívja meg a **create** vagy a **CreateAsync** metódust.

### <a name="c-example"></a>C \# példa

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

var cart = new Cart()
{
    LineItems = new List<CartLineItem>()
    {
        new CartLineItem()
        {
      /* Microsoft Azure Subscription */
            Id = 0,
            CatalogItemId = "MS-AZR-0145P",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1Y"
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 1,
            CatalogItemId = "DZH318Z0BQ36:004G:DZH318Z08C0S",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P1Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 2,
            CatalogItemId = "DZH318Z0BQ36:004J:DZH318Z08B8X",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P3Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Perpetual Software */
            Id = 3,
            CatalogItemId = "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime
        },
        new CartLineItem()
        {
      /* SaaS */
            Id = 4,
            CatalogItemId = "DZH318Z0BXWC:0002:DZH318Z0BMRV",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1M"
        },
        new CartLineItem()
        {
      /* SaaS Free Trial */
            Id = 5,
            CatalogItemId = "DZH318Z0C0WF:0001:DZH318Z0BP69",
            Quantity = 10,
            BillingCycle = BillingCycleType.None,
            TermDuration = "P1M",
            RenewsTo = new RenewsTo
            {
                TermDuration = "P1Y"
            }
        }
    }
};

cart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Megrendelés létrehozása az ügyfél számára:

1. Egy cart-objektum példányának létrehozása.

2. Hozzon létre egy listát a **CartLineItem** objektumokról, és rendelje hozzá a listát a kosár sorához. Minden egyes cart-sor egy termék vásárlási információit tartalmazza. Legalább egy cart-sorral kell rendelkeznie.

3. Szerezzen be egy felületet a cart-műveletekhez úgy, hogy meghívja a **IAggregatePartner. getCustomers (). byId** függvényt az ügyfél-azonosítóval, hogy azonosítsa az ügyfelet, majd beolvassa a felületet a **getCart** függvényből.

4. Hívja meg a **create** függvényt a kosár létrehozásához.

## <a name="java-example"></a>Java-példa

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;
// String catalogItemId;

CartLineItem lineItem = new CartLineItem();

lineItem.setBillingCycle(BillingCycleType.OneTime);
lineItem.setCatalogItemId(catalogItemId);
lineItem.setFriendlyName("Sample RI Purchase");
lineItem.setQuantity(1);

Map<String, String> provisioningContext = new HashMap<String,String>();

provisioningContext.put("duration", "3Years");
provisioningContext.put("scope", "shared");
provisioningContext.put("subscriptionId", subscriptionId);

lineItem.setProvisioningContext(provisioningContext);

List<CartLineItem> lineItemList = new ArrayList<CartLineItem>();
lineItemList.add(lineItem);

Cart cart = new Cart();
cart.setLineItems(lineItemList);

Cart cartCreated = partnerOperations.getCustomers().byId(customerId).getCarts().create(cart);
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Megrendelés létrehozása az ügyfél számára:

1. Egy cart-objektum példányának létrehozása.

2. Hozzon létre egy listát a **CartLineItem** objektumokról, és rendelje hozzá a listát a kosár sorához. Minden egyes cart-sor egy termék vásárlási információit tartalmazza. Legalább egy cart-sorral kell rendelkeznie.

3. Futtassa a [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) parancsot a kosár létrehozásához.

```powershell
# $customerId
# $subscriptionId
# $catalogItemId

$lineItem = New-Object -TypeName Microsoft.Store.PartnerCenter.PowerShell.Models.Carts.PSCartLineItem

$lineItem.BillingCycle = 'OneTime'
$lineItem.CatalogItemId = $catalogItemId
$lineItem.FriendlyName = 'Sample RI Purchase'
$lineItem.ProvisioningContext.Add('duration', '1Year')
$lineItem.ProvisioningContext.Add('scope', 'shared')
$lineItem.ProvisioningContext.Add('subscriptionId', $subsciptionId)
$lineItem.Quantity = 10

New-PartnerCustomerCart -CustomerId $customerId -LineItems $lineItem
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts http/1.1                        |

### <a name="uri-parameter"></a>URI-paraméter

Az ügyfél azonosításához használja a következő Path paramétert.

| Név            | Típus     | Kötelező | Leírás                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ügyfél-azonosító** | sztring   | Igen      | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.             |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérés törzsében lévő [kosár](cart-resources.md) tulajdonságait ismerteti.

| Tulajdonság              | Típus             | Kötelező        | Leírás |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | sztring           | No              | A kosár sikeres létrehozásához megadott cart-azonosító.                                  |
| creationTimeStamp     | DateTime         | Nem              | A kosár létrehozásának dátuma dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazható.         |
| lastModifiedTimeStamp | DateTime         | Nem              | A kosár utolsó frissítésének dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazható.    |
| expirationTimeStamp   | DateTime         | Nem              | A kosár lejáratának dátuma dátum-idő formátumban.  A kosár sikeres létrehozása után alkalmazható.            |
| lastModifiedUser      | sztring           | No              | A kosár utolsó frissítését végző felhasználó. A kosár sikeres létrehozása után alkalmazható.                             |
| Listaelemek             | Objektumok tömbje | Igen             | [CartLineItem](cart-resources.md#cartlineitem) -erőforrások tömbje.                                     |

Ez a táblázat a kérelem törzsének [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait ismerteti.

|      Tulajdonság       |            Típus             | Kötelező |                                                                                         Leírás                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         id          |           sztring            |    No    |                                                     Egy cart-sor egyedi azonosítója. A kosár sikeres létrehozása után alkalmazható.                                                     |
|      catalogId      |           sztring            |   Igen    |                                                                                A katalógus-elemek azonosítója.                                                                                 |
|    friendlyName     |           sztring            |    No    |                                                    Választható. A partner által a egyértelműsítse segítségére meghatározott rövid név.                                                    |
|      quantity       |             int             |   Igen    |                                                                            A licencek vagy példányok száma.                                                                             |
|    currencyCode     |           sztring            |    No    |                                                                                     A Pénznemkód.                                                                                      |
|    billingCycle     |           Objektum            |   Igen    |                                                                    Az aktuális időszakban beállított számlázási ciklus típusa.                                                                    |
|    résztvevők     | Az Object string párok listája |    Nem    |                                                                A PartnerId on Record (MPNID) gyűjteménye a vásárláson.                                                                 |
| provisioningContext | Szótár<karakterlánc, karakterlánc>  |    Nem    | A katalógus egyes elemeinek kiépítési feladataihoz szükséges információk. Az SKU provisioningVariables tulajdonsága azt jelzi, hogy mely tulajdonságok szükségesek a katalógus adott elemeihez. |
|     orderGroup      |           sztring            |    No    |                                                                   Egy csoport, amely jelzi, hogy mely elemek helyezhetők el egymásba.                                                                   |
|        error        |           Objektum            |    Nem    |                                                                     A kosár létrehozásakor a rendszer hiba esetén alkalmazza.                                                                      |
|     renewsTo        | Objektumok tömbje            |    Nem    |                                                    [RenewsTo](cart-resources.md#renewsto) -erőforrások tömbje.                                                                            |

Ez a táblázat a kérelem törzsének [RenewsTo](cart-resources.md#renewsto) tulajdonságait ismerteti.

| Tulajdonság              | Típus             | Kötelező        | Leírás |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | sztring           | No              | A megújítási időszak érvényességének ISO 8601-es ábrázolása. A jelenleg támogatott értékek a következők: **P1M** (1 hónap) és **P1Y** (1 év). |

### <a name="request-example"></a>Példa kérésre

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
  "lineItems": [
    {
    /* Microsoft Azure Subscription */
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1Y"
    },
    {
    /* Azure Reserved Instance */
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      }
    },
    {
    /* Azure Reserved Instance */
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "single"
      }
    },
    {
    /* Perpetual Software */
      "id": 3,
      "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSFM",
      "quantity": 1,
      "billingCycle": "one_time"
    },
    {
    /* SaaS */
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1M"
    },
  {
    /* SaaS Free Trial */
       "id": 5,
       "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
       "quantity": 10,
       "billingCycle": "none",
       "termDuration": "P1M",
       "renewsTo": {
         "termDuration": "P1Y"
       }
    }
  ]
}
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus a válasz törzsében lévő feltöltött [kosár](cart-resources.md) -erőforrást adja vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
  "id": "3655b1a0-b1c9-4268-9824-577fdbc4d0be",
  "creationTimestamp": "2019-01-16T00:45:41.6062996Z",
  "lastModifiedTimestamp": "2019-01-16T00:45:41.6062996Z",
  "expirationTimestamp": "2019-01-16T01:00:54.4188497Z",
  "lastModifiedUser": "1824b7fc-2fac-4478-b177-66823c40ab75",
  "status": "Active",
  "lineItems": [
    {
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1Y",
      "orderGroup": "OMS-0"
    },
    {
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 3,
      "catalogItemId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "orderGroup": "0"
    },
    {
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1M",
      "orderGroup": "1"
    },
  {
      "id": 5,
      "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
      "quantity": 10,
      "currencyCode": "USD",
      "billingCycle": "none",
      "termDuration": "P1M",
      "renewsTo": {
  "termDuration": "P1Y"
      },
    "orderGroup": "2"
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/28045616-f6b9-462f-9701-0d89b5e65c44/carts/3655b1a0-b1c9-4268-9824-577fdbc4d0be",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Cart"
  }
}
```
