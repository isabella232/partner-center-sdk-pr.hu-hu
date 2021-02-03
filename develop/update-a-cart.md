---
title: Kosár frissítése
description: Ügyfél rendelésének frissítése egy kosárban.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7c0806ccc87281b9b34005f22cd8d6ad57fb5de5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767835"
---
# <a name="update-a-cart"></a>Kosár frissítése

**A következőkre vonatkozik**

- Partnerközpont

Ügyfél rendelésének frissítése egy kosárban.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Egy meglévő kosárhoz tartozó kosár-azonosító.

## <a name="c"></a>C\#

Egy ügyfél rendelésének frissítéséhez szerezze be a kosárt a **Get ()** metódussal, ha az ügyfél és a kosár azonosítóját a **ById ()** függvény használatával adja át. Végezze el a szükséges módosításokat a kosárban. Most hívja meg a **put** metódust az ügyfél és a kosár azonosítójának használatával a **ById ()** metódus használatával.

Végül hívja a **put ()** vagy a **PutAsync ()** metódust a rendelés létrehozásához.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts/{cart-ID} http/1.1              |

### <a name="uri-parameters"></a>URI-paraméterek

A következő elérésiút-paraméterek használatával azonosíthatja az ügyfelet, és megadhatja a frissítendő szekéret.

| Név            | Típus     | Kötelező | Leírás                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ügyfél-azonosító** | sztring   | Igen      | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.             |
| **kosár-azonosító**     | sztring   | Igen      | A szekér azonosítására szolgáló GUID formátumú kosár-azonosító.                     |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérés törzsében lévő [kosár](cart-resources.md) tulajdonságait ismerteti.

| Tulajdonság              | Típus             | Kötelező        | Leírás                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | sztring           | No              | A kosár sikeres létrehozásához megadott cart-azonosító.                                  |
| creationTimeStamp     | DateTime         | Nem              | A kosár létrehozásának dátuma dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazható.        |
| lastModifiedTimeStamp | DateTime         | Nem              | A kosár utolsó frissítésének dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazható.    |
| expirationTimeStamp   | DateTime         | Nem              | A kosár lejáratának dátuma dátum-idő formátumban.  A kosár sikeres létrehozása után alkalmazható.            |
| lastModifiedUser      | sztring           | No              | A kosár utolsó frissítését végző felhasználó. A kosár sikeres létrehozása után alkalmazható.                             |
| Listaelemek             | Objektumok tömbje | Igen             | [CartLineItem](cart-resources.md#cartlineitem) -erőforrások tömbje.                                               |

Ez a táblázat a kérelem törzsének [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait ismerteti.

| Tulajdonság             | Típus                        | Kötelező     | Leírás                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | sztring                      | No           | Egy cart-sor egyedi azonosítója. A kosár sikeres létrehozása után alkalmazható.                |
| catalogId            | sztring                      | Igen          | A katalógus-elemek azonosítója.                                                                       |
| friendlyName         | sztring                      | No           | Választható. A partner által a egyértelműsítse segítségére meghatározott rövid név.              |
| quantity             | int                         | Igen          | A licencek vagy példányok száma.     |
| currencyCode         | sztring                      | No           | A Pénznemkód.                                                                                 |
| billingCycle         | Objektum                      | Igen          | Az aktuális időszakban beállított számlázási ciklus típusa.                                              |
| résztvevők         | Az Object string párok listája | Nem           | A vásárlás résztvevőinek gyűjteménye.                                                      |
| provisioningContext  | Szótár<karakterlánc, karakterlánc>  | Nem           | Az ajánlat üzembe helyezéséhez használt környezet.                                                          |
| orderGroup           | sztring                      | No           | Egy csoport, amely jelzi, hogy mely elemek helyezhetők el egymásba.                                            |
| error                | Objektum                      | Nem           | A kosár létrehozásakor a rendszer hiba esetén alkalmazza.                                                 |

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
