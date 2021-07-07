---
title: Kosár frissítése
description: Hogyan frissítheti egy ügyfél megrendelését egy kosárban.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8954d4dad39f9b1a1b9a2f213e0231f01856fcd2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446683"
---
# <a name="update-a-cart"></a>Kosár frissítése

Hogyan frissítheti egy ügyfél megrendelését egy kosárban.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy meglévő kosár azonosítója.

## <a name="c"></a>C\#

Az ügyfél megrendelésének frissítéséhez szerezze be a kosárt a **Get()** metódussal úgy, hogy a **ById()** függvény használatával ad át az ügyfél- és kosárazonosítókat. Tegye meg a szükséges módosításokat a kosáron. Most hívja meg a **Put** metódust ügyfél- és kosárazonosítók használatával a **ById() metódussal.**

Végül hívja meg a **Put() vagy** **PutAsync()** metódust a rendelés létrehozásához.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfél-azonosító}/carts/{cart-id} HTTP/1.1              |

### <a name="uri-parameters"></a>URI-paraméterek

Az alábbi elérésiút-paraméterek használatával azonosíthatja az ügyfelet, és megadhatja a frissíteni kívánt kosárt.

| Név            | Típus     | Kötelező | Leírás                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ügyfél-azonosító** | sztring   | Igen      | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.             |
| **cart-id**     | sztring   | Igen      | Egy GUID formátumú kocsiazonosító, amely azonosítja a kosárat.                     |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kocsi [tulajdonságait ismerteti](cart-resources.md) a kérés törzsében.

| Tulajdonság              | Típus             | Kötelező        | Leírás                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | sztring           | No              | A kosár sikeres létrehozása után megadott bevásárlókocsi-azonosító.                                  |
| creationTimeStamp     | DateTime         | Nem              | A kosár létrehozási dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazva.        |
| lastModifiedTimeStamp | DateTime         | Nem              | A kosár legutóbbi frissítésének dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazva.    |
| expirationTimeStamp (lejárat ideje)   | DateTime         | Nem              | A kosár lejáratának dátuma, dátum-idő formátumban.  A kosár sikeres létrehozása után alkalmazva.            |
| lastModifiedUser      | sztring           | No              | Az a felhasználó, aki utoljára frissítette a kosárat. A kosár sikeres létrehozása után alkalmazva.                             |
| lineItems (sorsorok)             | Objektumok tömbje | Igen             | [CartLineItem-erőforrások tömbje.](cart-resources.md#cartlineitem)                                               |

Ez a táblázat a [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait ismerteti a kérés törzsében.

| Tulajdonság             | Típus                        | Kötelező     | Leírás                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | sztring                      | No           | A kosársorelem egyedi azonosítója. A kosár sikeres létrehozása után alkalmazva.                |
| catalogId (katalógusazonosító)            | sztring                      | Igen          | A katalóguselem azonosítója.                                                                       |
| friendlyName (rövid név)         | sztring                      | No           | Választható. A partner által meghatározott elem rövid neve, amely segít az egyértelműsségben.              |
| quantity             | int                         | Igen          | A licencek vagy példányok száma.     |
| currencyCode         | sztring                      | No           | A pénznemkód.                                                                                 |
| billingCycle (számlázási ciklus)         | Objektum                      | Igen          | Az aktuális időszakra beállított számlázási ciklus típusa.                                              |
| Résztvevők         | Objektumsring-párok listája | Nem           | A vásárlás résztvevőinek gyűjteménye.                                                      |
| provisioningContext  | Dictionary<string, string>  | Nem           | Az ajánlat építéshez használt környezet.                                                          |
| orderGroup           | sztring                      | No           | Egy csoport, amely jelzi, hogy mely elemek helyezhetők el együtt.                                            |
| error                | Objektum                      | Nem           | A kosár létrehozása után lesz alkalmazva hiba esetén.                                                 |

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

Ha ez a módszer sikeres, a válasz törzsében adja vissza a megadott [Cart](cart-resources.md) erőforrást.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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
