---
title: Kosár létrehozása
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat egy ügyfél megrendelésének kosárba való felvételhez. A témakör információkat tartalmaz a kosár létrehozásáról és az előfeltételekről.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 1f5c0ae7693a8ac2a2919c385dc1b8837a9171ed8cc422bba79bb892f9fe837a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991837"
---
# <a name="create-a-cart-with-a-customer-order"></a>Kosár létrehozása ügyfélrendeléssel

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Egy ügyfél megrendelését kosárban is hozzáadhatja. A jelenleg értékesíthető ajánlatokkal kapcsolatos további információkért lásd a partneri ajánlatokat a [Felhőszolgáltató programjában.](/partner-center/csp-offers)

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Rendelés létrehozása egy ügyfél számára:

1. Cart-objektum példányosodása.

2. Hozza létre a **CartLineItem** objektumok listáját, és rendelje hozzá a listát a kosár LineItems (Soritemek) tulajdonságához. Minden kosársorelem egy termék vásárlási információit tartalmazza. Legalább egy kosársori elemet kell berakni.

3. A kosárműveleteket úgy szerezheti be, ha az ügyfél azonosítójával hívja meg az **IAggregatePartner.Customers.ById** metódust az ügyfél azonosításához, majd lehívja a felületet a **Cart** tulajdonságból.

4. A **kosár létrehozásához** hívja meg a **Create vagy a CreateAsync** metódust.

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

Rendelés létrehozása egy ügyfél számára:

1. Cart-objektum példányosodása.

2. Létrehozhatja a **CartLineItem** objektumok listáját, és hozzárendelheti a listát a kosár sorelemekhez. Minden kosársorelem egy termék vásárlási információit tartalmazza. Legalább egy kosársori elemet kell berakni.

3. A kosárműveleteket úgy szerezheti be, hogy az ügyfél azonosítójával hívja meg az **IAggregatePartner.getCustomers().byId** függvényt az ügyfél azonosításához, majd lehívja a felületet a **getCart függvényből.**

4. A **kosár létrehozásához** hívja meg a create függvényt.

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

Rendelés létrehozása egy ügyfél számára:

1. Cart-objektum példányosodása.

2. Létrehozhatja a **CartLineItem** objektumok listáját, és hozzárendelheti a listát a kosár sorelemekhez. Minden kosársorelem egy termék vásárlási információit tartalmazza. Legalább egy kosársori elemet kell berakni.

3. Hajtsa végre a [**New-PartnerCustomerCart parancsot**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) a kosár létrehozásához.

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

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfél-azonosító}/carts HTTP/1.1                        |

### <a name="uri-parameter"></a>URI-paraméter

Az ügyfél azonosításához használja a következő path paramétert.

| Név            | Típus     | Kötelező | Leírás                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ügyfél-azonosító** | sztring   | Yes      | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.             |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kocsi [tulajdonságait ismerteti](cart-resources.md) a kérés törzsében.

| Tulajdonság              | Típus             | Kötelező        | Leírás |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | sztring           | No              | A kosár sikeres létrehozása után megadott bevásárlókocsi-azonosító.                                  |
| creationTimeStamp     | DateTime         | No              | A kosár létrehozási dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazva.         |
| lastModifiedTimeStamp | DateTime         | No              | A kosár legutóbbi frissítésének dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazva.    |
| expirationTimeStamp (lejárat/időstamp)   | DateTime         | No              | A kosár lejáratának dátuma, dátum és idő formátumban.  A kosár sikeres létrehozása után alkalmazva.            |
| lastModifiedUser      | sztring           | No              | Az a felhasználó, aki utoljára frissítette a kosárat. A kosár sikeres létrehozása után alkalmazva.                             |
| lineItems (sorsorok)             | Objektumok tömbje | Yes             | [CartLineItem-erőforrások tömbje.](cart-resources.md#cartlineitem)                                     |

Ez a táblázat a [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait ismerteti a kérés törzsében.

|      Tulajdonság       |            Típus             | Kötelező |                                                                                         Leírás                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         id          |           sztring            |    No    |                                                     A kosársorelem egyedi azonosítója. A kosár sikeres létrehozása után alkalmazva.                                                     |
|      catalogId (katalógusazonosító)      |           sztring            |   Yes    |                                                                                A katalóguselem azonosítója.                                                                                 |
|    friendlyName (rövid név)     |           sztring            |    No    |                                                    Választható. A partner által meghatározott elem rövid neve a egyértelműsséghez.                                                    |
|      quantity       |             int             |   Yes    |                                                                            A licencek vagy példányok száma.                                                                             |
|    currencyCode     |           sztring            |    No    |                                                                                     A pénznemkód.                                                                                      |
|    billingCycle (számlázási ciklus)     |           Objektum            |   Yes    |                                                                    Az aktuális időszakra beállított számlázási ciklus típusa.                                                                    |
|    Résztvevők     | Objektumsring-párok listája |    No    |                                                                A vásárláskor rekordban (MPNID) vásárolt PartnerId gyűjtemény.                                                                 |
| provisioningContext | Dictionary<string, string>  |    No    | A katalógus egyes elemeinek kiépítéséhez szükséges információk. A termékváltozatok provisioningVariables tulajdonsága jelzi, hogy mely tulajdonságok szükségesek a katalógus adott elemeihez. |
|     orderGroup      |           sztring            |    No    |                                                                   Egy csoport, amely jelzi, hogy mely elemek helyezhetők együtt.                                                                   |
|        error        |           Objektum            |    No    |                                                                     A kocsi létrehozása után lesz alkalmazva, ha hiba történik.                                                                      |
|     renewsTo        | Objektumok tömbje            |    No    |                                                    A [RenewsTo erőforrások tömbje.](cart-resources.md#renewsto)                                                                            |
|     AttestationAccepted (AttestationAccepted)        | Logikai            |    No    |                                                   Az ajánlati vagy termékváltozat-feltételekre vonatkozó szerződést jelzi. Csak olyan ajánlatokhoz vagy termékváltozatokhoz szükséges, ahol a SkuAttestationProperties vagy az OfferAttestationProperties enforceAttestation true (Igaz) érték.                                                                             |

Ez a táblázat a [kérés törzsében található RenewsTo](cart-resources.md#renewsto) tulajdonságokat ismerteti.

| Tulajdonság              | Típus             | Kötelező        | Leírás |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration (kifejezés-lekértség)          | sztring           | No              | A megújítási időtartam ISO 8601-es ábrázolása. A jelenleg támogatott értékek a **P1M (1** hónap) és a **P1Y (1** év). |

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

Ha ez a módszer sikeres, a válasz törzsében adja vissza a megadott [cart](cart-resources.md) erőforrást.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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
