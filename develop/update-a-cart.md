---
title: Kosár frissítése
description: Hogyan frissítheti egy ügyfél megrendelését egy kosárban.
ms.date: 09/06/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 48fec2d9fb72d1a58fe79969e48ccd39a32c5ccc
ms.sourcegitcommit: 5f27733d7c984c29f71c8b9c8ba5f89753eeabc4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/07/2021
ms.locfileid: "123557286"
---
# <a name="update-a-cart"></a>Kosár frissítése

Hogyan frissítheti egy ügyfél megrendelését egy kosárban.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Egy meglévő kosár azonosítója.

## <a name="c"></a>C\#

Egy ügyfél megrendelésének frissítéséhez a **Get()** metódussal szerezze be a kosárat az ügyfél és a kosárazonosítók **ById()** függvény használatával való átadásával. Készítse el a szükséges módosításokat a kosáron. Most hívja meg a **Put** metódust ügyfél- és kosárazonosítók használatával a **ById() metódussal.**

Végül hívja meg a **Put() vagy** **PutAsync()** metódust a rendelés létrehozásához.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

Az igazolás befejezéséhez és a további viszonteladókhoz való be includehoz tekintse meg az alábbi mintát.

### <a name="api-sample---check-out-cart"></a>API-minta – Bevásárlókocsi

``` csharp
{
    "orders": [
        {
            "id": "f76c6b7f449d",
            "alternateId": "f76c6b7f449d",
            "referenceCustomerId": "f81d98dd-c2f4-499e-a194-5619e260344e",
            "billingCycle": "monthly",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
                    "subscriptionId": "ebc0beef-7ffb-4044-c074-16f324432139",
                    "termDuration": "P1M",
                    "transactionType": "New",
                    "friendlyName": "AI Builder Capacity add-on",
                    "quantity": 1,
                    "links": {
                        "product": {
                            "uri": "/products/CFQ7TTC0LH0Z?country=US",
                            "method": "GET",
                            "headers": []
                        },
                        "sku": {
                            "uri": "/products/CFQ7TTC0LH0Z/skus/0001?country=US",
                            "method": "GET",
                            "headers": []
                        },
                        "availability": {
                            "uri": "/products/CFQ7TTC0LH0Z/skus/0001/availabilities/CFQ7TTC0K18P?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                },
                {
                    "lineItemNumber": 1,
                    "offerId": "CFQ7TTC0LFLS:0002:CFQ7TTC0KDLJ",
                    "subscriptionId": "261bac40-7d88-4327-dfa3-dacd09222d62",
                    "termDuration": "P1Y",
                    "transactionType": "New",
                    "friendlyName": "Azure Active Directory Premium P1",
                    "quantity": 2,
                    "partnerIdOnRecord": "517285",
                    "additionalPartnerIdsOnRecord": 
                        "5357564",
                        "5357563"
                    ],
                 
   "links": {
                        "product": {
                            "uri": "/products/CFQ7TTC0LFLS?country=US",
                            "method": "GET",
                            "headers": []
                        },
                        "sku": {
                            "uri": "/products/CFQ7TTC0LFLS/skus/0002?country=US",
                            "method": "GET",
                            "headers": []
                        },
                        "availability": {
                            "uri": "/products/CFQ7TTC0LFLS/skus/0002/availabilities/CFQ7TTC0KDLJ?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2021-08-18T07:52:23.1921872Z",
            "status": "pending",
            "transactionType": "UserPurchase",
            "links": {
                "self": {
                    "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/f76c6b7f449d",
                    "method": "GET",
                    "headers": []
                },
                "provisioningStatus": {
                    "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/f76c6b7f449d/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "patchOperation": {
                    "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/f76c6b7f449d",
                    "method": "PATCH",
                    "headers": []
                }
            },
            "client": {},
            "attributes": {
                "objectType": "Order"
            }
        }
    ],
    "attributes": {
        "objectType": "CartCheckoutResult"
    }
}

```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/carts/{kocsiazonosító} HTTP/1.1              |

### <a name="uri-parameters"></a>URI-paraméterek

Az alábbi elérésiút-paraméterekkel azonosíthatja az ügyfelet, és megadhatja a frissíteni kívánt kosárt.

| Név            | Típus     | Kötelező | Leírás                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ügyfél-azonosító** | sztring   | Yes      | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.             |
| **kocsiazonosító**     | sztring   | Yes      | Egy GUID formátumú kocsiazonosító, amely azonosítja a kosárat.                     |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kocsi [tulajdonságait ismerteti](cart-resources.md) a kérés törzsében.

| Tulajdonság              | Típus             | Kötelező        | Leírás                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | sztring           | No              | A kosár sikeres létrehozása után megadott kocsiazonosító.                                  |
| creationTimeStamp     | DateTime         | No              | A kosár létrehozási dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazva.        |
| lastModifiedTimeStamp | DateTime         | No              | A kosár legutóbbi frissítésének dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazva.    |
| expirationTimeStamp (lejárati idő)   | DateTime         | No              | A kosár lejáratának dátuma, dátum-idő formátumban.  A kosár sikeres létrehozása után alkalmazva.            |
| lastModifiedUser      | sztring           | No              | Az a felhasználó, aki utoljára frissítette a kosárat. A kosár sikeres létrehozása után alkalmazva.                             |
| lineItems (sorsorok)             | Objektumok tömbje | Yes             | [CartLineItem-erőforrások tömbje.](cart-resources.md#cartlineitem)                                               |

Ez a táblázat ismerteti a [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait a kérelem törzsében.

| Tulajdonság             | Típus                        | Kötelező     | Leírás                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | sztring                      | No           | Egy kocsisorelem egyedi azonosítója. A kosár sikeres létrehozása után alkalmazva.                |
| catalogId (katalógusazonosító)            | sztring                      | Yes          | A katalóguselem azonosítója.                                                                       |
| friendlyName (rövid név)         | sztring                      | No           | Választható. A partner által definiált elem rövid neve, amely segít egyértelműsedni.              |
| quantity             | int                         | Yes          | A licencek vagy példányok száma.     |
| currencyCode         | sztring                      | No           | A pénznemkód.                                                                                 |
| billingCycle         | Objektum                      | Yes          | Az aktuális időszakhoz beállított számlázási ciklus típusa.                                              |
| Résztvevők         | Objektums sztringpárok listája | No           | A vásárlás résztvevőinek gyűjteménye.                                                      |
| provisioningContext  | Szótár<sztring, sztring>  | No           | Az ajánlat építéshez használt környezet.                                                          |
| orderGroup           | sztring                      | No           | Egy csoport, amely jelzi, hogy mely elemek helyezhetők együtt.                                            |
| error                | Objektum                      | No           | A kosár hiba esetén a kosár létrehozása után lesz alkalmazva.                                                 |
| AdditionalPartnerIdsOnRecord (További partnerazonosítókOnRecord) | Sztring | No | Ha egy közvetett szolgáltató egy közvetett viszonteladó nevében ad ki rendelést, akkor ezt a mezőt csak a további közvetett viszonteladó MPN-azonosítójával **töltse** ki (soha ne a közvetett szolgáltató azonosítójával). Az ösztönzők nem alkalmazhatók ezekre a további viszonteladókra. Csak legfeljebb 5 közvetett viszonteladót lehet megadni. Ez csak az EU-/EFTA-országokon belül tranzakciós partnerekre vonatkozik.  |

### <a name="request-example"></a>Példa kérésre

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
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
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus visszaadja a válasz törzsében a megadott [Cart](cart-resources.md) erőforrást.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```
