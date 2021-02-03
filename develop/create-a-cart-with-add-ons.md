---
title: Kosár létrehozása bővítményekkel
description: Megtudhatja, hogyan veheti fel a partner Center API-kat a bővítmények egy kosárba való felvételéhez. Cikk megosztja az előfeltételeket és lépéseket a kosár bővítményekkel való létrehozásához.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 81c41405a2f56eb4d1d3447d14b93e05d550cc70
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768628"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a>Kosár létrehozása az ügyfelek megrendeléséhez bővítményekkel

**A következőkre vonatkozik:**

- Partnerközpont

A bővítményeket a kosáron keresztül is megvásárolhatja. További információ az értékesítésre jelenleg elérhető termékekről: [partneri ajánlatok a Cloud Solution Provider programban](/partner-center/csp-offers).

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

A kosár lehetővé teszi egy alapszintű ajánlat és a hozzájuk tartozó bővítmények megvásárlását. A kosár létrehozásához kövesse az alábbi lépéseket:

1. Egy [**cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) -objektum példányának létrehozása.

2. Hozzon létre egy listát az alapajánlat (oka) t képviselő [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) -objektumokról, és rendelje hozzá a listát a kosár [**listaelemek**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) tulajdonságához.

3. Az egyes alapajánlatok sorában töltse fel a **AddOnItems** listáját más **CartLineItem** objektumokkal, amelyek mindegyike az adott alapajánlathoz megvásárolt bővítményt képviseli.

4. Szerezzen be egy felületet a cart-műveletekhez a [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) használatával, hogy meghívja a [**ICustomerCollection. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, hogy azonosítsa az ügyfelet, majd beolvassa a felületet a **cart** tulajdonságból.

5. Végül hívja meg a [**create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) metódust a kosár létrehozásához.

### <a name="c-example"></a>C \# példa

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

Kövesse az alábbi lépéseket egy olyan kosár létrehozásához, amely lehetővé teszi bővítmény (ek) megvásárlását meglévő alapszintű előfizetések esetén:

1. Hozzon **létre egy új** **CartLineItem** , amely tartalmazza az előfizetés azonosítóját a **ProvisioningContext** tulajdonságban az "ParentSubscriptionId" kulccsal.

2. Hívja meg a **create** vagy a **CreateAsync** metódust.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts http/1.1                        |

#### <a name="uri-parameter"></a>URI-paraméter

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
| Listaelemek             | Objektumok tömbje | Igen             | [CartLineItem](cart-resources.md#cartlineitem) -erőforrások tömbje.                                             |

Ez a táblázat a kérelem törzsének [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait ismerteti.

| Tulajdonság             | Típus                             | Leírás                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sztring                           | Egy cart-sor egyedi azonosítója. A kosár sikeres létrehozása után alkalmazható.                                                                   |
| catalogId            | sztring                           | A katalógus-elemek azonosítója.                                                                                                                          |
| friendlyName         | sztring                           | Választható. A partner által a egyértelműsítse segítségére meghatározott rövid név.                                                                 |
| quantity             | int                              | A licencek vagy példányok száma.                                                                                                                  |
| currencyCode         | sztring                           | A Pénznemkód.                                                                                                                                    |
| billingCycle         | Objektum                           | Az aktuális időszakban beállított számlázási ciklus típusa.                                                                                                 |
| résztvevők         | Az Object string párok listája      | A PartnerId on Record (MPNID) gyűjteménye a vásárláson.                                                                                          |
| provisioningContext  | Szótár<karakterlánc, karakterlánc>       | Az ajánlat üzembe helyezéséhez használt környezet.                                                                                                             |
| orderGroup           | sztring                           | Egy csoport, amely jelzi, hogy mely elemek helyezhetők el egymásba.                                                                                               |
| addonItems           | **CartLineItem** -objektumok listája | Azon bővítmények gyűjteménye, amelyek az alapelőfizetés azon előfizetéséhez lesznek megvásárolva, amely a fölérendelt cikk megvásárlását eredményezi. |
| error                | Objektum                           | A kosár létrehozásakor a rendszer hiba esetén alkalmazza.                                                                                                    |

### <a name="request-example-new-base-subscription"></a>Példa kérésre (új alapszintű előfizetés)

A következő REST-példa azt szemlélteti, hogyan hozható létre egy új alapelőfizetés kiegészítő elemeit tartalmazó kosár.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a>Példa kérésre (meglévő alap előfizetés)

A következő REST-példa azt szemlélteti, hogyan lehet bővítményeket hozzáfűzni egy meglévő alap előfizetéshez.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus a válasz törzsében lévő feltöltött [kosár](cart-resources.md) -erőforrást adja vissza.

#### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

#### <a name="response-example-new-base-subscription"></a>Válasz példa (új alapszintű előfizetés)

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a>Válasz példa (meglévő alap előfizetés)

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
