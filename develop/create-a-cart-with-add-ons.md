---
title: Kosár létrehozása bővítményekkel
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat arra, hogy hozzáadja az ügyfélrendeléseket bővítmények segítségével egy kosárban. A cikk a bővítményeket is hozzátenő kosár létrehozásához szükséges előfeltételeket és lépéseket osztja meg.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: ed4b8be5171493f83aefef08253c748a7bfd90dc5f2b1e325e5ceba78e36bdc2
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991803"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a>Kosár létrehozása az ügyfélrendeléshez szükséges bővítményekkel

A bővítményeket kosárban vásárolhatja meg. A jelenleg értékesíthető ajánlatokkal kapcsolatos további információkért lásd a partneri ajánlatokat a [Felhőszolgáltató programjában.](/partner-center/csp-offers)

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

A kosár lehetővé teszi egy alapajánlat és a hozzá tartozó bővítmények megvásárlását. A kosár létrehozásához kövesse az alábbi lépéseket:

1. Cart-objektum [**példányosodása.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart)

2. Hozzon létre egy listát a [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objektumokról, amelyek az alapajánlat(okat) képviselik, és rendelje hozzá a listát a kosár [**LineItems (Soritemek) tulajdonságához.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems)

3. Az alapajánlatok kocsisorelemei alatt töltse fel az **AddOnItems** (Bővítmények) listáját más **CartLineItem** objektumokkal, amelyek mindegyike egy-egy bővítményt képvisel, és amely az adott alapajánlathoz lesz megvásárolva.

4. Szerezzen be egy interfészt a kosárműveletek számára az [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) használatával, hogy az ügyfél azonosítójával hívja meg az [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosításához, majd lehívja a felületet a **Cart** tulajdonságból.

5. Végül hívja meg a [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) vagy [**CreateAsync metódust**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) a kosár létrehozásához.

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

Kövesse az alábbi lépéseket egy olyan kosár létrehozásához, amely lehetővé teszi bővítmény(nek) vásárlását a meglévő alap előfizetés(ekkel) szemben:

1. Hozzon  létre egy új **CartLineItem** kosarat, amely tartalmazza az előfizetés azonosítóját a **ProvisioningContext** tulajdonságban a "ParentSubscriptionId" kulccsal.

2. Hívja meg a **Create** vagy **CreateAsync metódust.**

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

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfél-azonosító}/carts HTTP/1.1                        |

#### <a name="uri-parameter"></a>URI-paraméter

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
| lineItems (sorsorok)             | Objektumok tömbje | Yes             | [CartLineItem-erőforrások tömbje.](cart-resources.md#cartlineitem)                                             |

Ez a táblázat a [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait ismerteti a kérés törzsében.

| Tulajdonság             | Típus                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sztring                           | A kosársorelem egyedi azonosítója. A kosár sikeres létrehozása után alkalmazva.                                                                   |
| catalogId (katalógusazonosító)            | sztring                           | A katalóguselem azonosítója.                                                                                                                          |
| friendlyName (rövid név)         | sztring                           | Választható. A partner által meghatározott elem rövid neve a egyértelműsséghez.                                                                 |
| quantity             | int                              | A licencek vagy példányok száma.                                                                                                                  |
| currencyCode         | sztring                           | A pénznemkód.                                                                                                                                    |
| billingCycle         | Objektum                           | Az aktuális időszakhoz beállított számlázási ciklus típusa.                                                                                                 |
| Résztvevők         | Objektums sztringpárok listája      | A vásárláskor rekordban (MPN-azonosító) vásárolt PartnerId gyűjtemény.                                                                                          |
| provisioningContext  | Szótár<sztring, sztring>       | Az ajánlat építéshez használt környezet.                                                                                                             |
| orderGroup           | sztring                           | Egy csoport, amely jelzi, hogy mely elemek helyezhetők együtt.                                                                                               |
| addonItems (bővítmények)           | **CartLineItem-objektumok** listája | A kosársorelemek gyűjteménye bővítményekhez, amelyek a szülőkocsisor tételének megvásárlásából származó alap előfizetéshez lesznek megvásárolva. |
| error                | Objektum                           | A kosár létrehozása után alkalmazza, ha hiba történik.                                                                                                    |

### <a name="request-example-new-base-subscription"></a>Példa kérése (új alap előfizetés)

Az alábbi REST-példa bemutatja, hogyan hozhat létre egy új alap-előfizetéshez bővítményelemeket is a kosárban.

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

#### <a name="request-example-existing-base-subscription"></a>Példa kérése (meglévő alap előfizetés)

Az alábbi REST-példa bemutatja, hogyan fűzhet bővítményeket egy meglévő alap előfizetéshez.

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

Ha a művelet sikeres, ez a metódus visszaadja a válasz törzsében a megadott [Cart](cart-resources.md) erőforrást.

#### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

#### <a name="response-example-new-base-subscription"></a>Példaválasz (új alap előfizetés)

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

#### <a name="response-example-existing-base-subscription"></a>Példaválasz (meglévő alap előfizetés)

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
