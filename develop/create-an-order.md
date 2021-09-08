---
title: Ügyfélrendelés létrehozása
description: Megtudhatja, hogyan hozhat létre rendelést Partnerközpont API-k használatával egy ügyfél számára. A cikk előfeltételeket, lépéseket és példákat tartalmaz.
ms.date: 09/06/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 232888ee798b4579246bbfd787e049f9f6e2e8a3
ms.sourcegitcommit: 5f27733d7c984c29f71c8b9c8ba5f89753eeabc4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/07/2021
ms.locfileid: "123557252"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a>Rendelés létrehozása egy ügyfél számára a Partnerközpont API-k használatával

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont a Microsoft Cloud for US Government

Az **Azure-beli fenntartott VM-példányok termékeire vonatkozó rendelés létrehozása** csak a *következőkre* vonatkozik:

- Partnerközpont

A jelenleg értékesíthető termékről a partneri ajánlatok a Felhőszolgáltató [érhetők el.](/partner-center/csp-offers)

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, a következő irányítópulton Partnerközpont [ki:](https://partner.microsoft.com/dashboard). Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy ajánlatazonosító.

## <a name="c"></a>C\#

Rendelés létrehozása egy ügyfél számára:

1. Példányositsa az [**Order**](order-resources.md) objektumot, és állítsa a **ReferenceCustomerID** tulajdonságot az ügyfélazonosítóra az ügyfél rögzítéséhez.

2. Hozzon létre egy [**listát az OrderLineItem**](order-resources.md#orderlineitem) objektumokból, és rendelje hozzá a listát a rendelés **LineItems tulajdonságához.** Minden rendeléssorelem egy adott ajánlat vásárlási adatait tartalmazza. Legalább egy megrendeléssor-elemnek kell lennie.

3. Szerezzen be egy interfészt a műveletek megrendelésére. Először hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához. Ezután olvassa be az interfészt az [**Orders tulajdonságból.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)

4. Hívja meg [**a Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) vagy [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) metódust, és adja át az [**Order objektumot.**](order-resources.md)

5. Az igazolás befejezéséhez és további viszonteladókhoz való igényléshez tekintse meg az alábbi kérés- és válaszmintákat:

### <a name="request-example"></a>Példa kérésre

``` csharp
{
    "PartnerOnRecordAttestationAccepted":true, 
    "lineItems": [
        {
            "offerId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
            "quantity": 1,
            "lineItemNumber": 0,
            "PartnerIdOnRecord": "873452",
            "AdditionalPartnerIdsOnRecord":["4847383","873452"]
        }
    ],
    "billingCycle": "monthly"
}
```

### <a name="response-example"></a>Példa válaszra

``` csharp
{
    "id": "5cf72f146967",
    "alternateId": "5cf72f146967",
    "referenceCustomerId": "f81d98dd-c2f4-499e-a194-5619e260344e",
    "billingCycle": "monthly",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
            "subscriptionId": "fcddfa52-1da8-4529-d347-50ea51e1e7be",
            "termDuration": "P1M",
            "transactionType": "New",
            "friendlyName": "AI Builder Capacity add-on",
            "quantity": 1,
            "partnerIdOnRecord": "873452",
            "additionalPartnerIdsOnRecord": [
                "4847383",
                "873452"
            ],
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
        }
    ],
    "creationDate": "2021-08-17T18:13:11.3122226Z",
    "status": "pending",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/5cf72f146967",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/5cf72f146967/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/5cf72f146967",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {},
    "attributes": {
        "objectType": "Order"
    }
}

```

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

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** Partnerközpont SDK **Osztály:** CreateOrder.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Az ügyfél azonosításához használja a következő path paramétert.

| Név        | Típus   | Kötelező | Leírás                                                |
|-------------|--------|----------|------------------------------------------------------------|
| ügyfél-azonosító | sztring | Yes      | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

#### <a name="order"></a>Sorrend

Ez a táblázat a kérelem törzsében található [Order (Rendelés)](order-resources.md) tulajdonságokat ismerteti.

| Tulajdonság             | Típus                        | Kötelező                        | Leírás                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| id                   | sztring                      | No                              | A rendelés sikeres létrehozása után megadott rendelésazonosító.   |
| referenceCustomerId  | sztring                      | No                              | Az ügyfél azonosítója. |
| billingCycle (számlázási ciklus)         | sztring                      | No                              | Azt jelzi, hogy milyen gyakorisággal számlázták a partnert a rendelésért. A támogatott értékek a [BillingCycleType](product-resources.md#billingcycletype)típusban található tagnevek. Az alapértelmezett érték a "Havi" vagy a "OneTime" a rendelés létrehozásakor. Ez a mező a rendelés sikeres létrehozásakor lesz alkalmazva. |
| lineItems (sorsorok)            | [OrderLineItem-erőforrások tömbje](order-resources.md#orderlineitem) | Yes      | Az ügyfél által megvásárolt ajánlatok elemi listája, beleértve a mennyiséget is.        |
| currencyCode         | sztring                      | No                              | Csak olvasható. A rendelés leadáskor használt pénznem. A rendelés sikeres létrehozásakor alkalmazva.           |
| creationDate (Létrehozás dátuma)         | dátum/idő                    | No                              | Csak olvasható. A rendelés létrehozási dátuma, dátum-idő formátumban. A rendelés sikeres létrehozásakor alkalmazva.                                   |
| status               | sztring                      | No                              | Csak olvasható. A rendelés állapota.  A támogatott értékek az [OrderStatus](order-resources.md#orderstatus)oszlopban található tagnevek.        |
| Linkek                | [OrderLinks (Megrendelési hivatkozás)](utility-resources.md#resourcelinks)              | No                              | Az Order (Rendelés) erőforrás-hivatkozások. |
| Attribútumok           | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | No                              | Az Order attribútumnak megfelelő metaadat-attribútumok. |
| PartnerOnRecordAttestationAccepted | Logikai | Yes | Megerősíti az igazolás befejezését |


#### <a name="orderlineitem"></a>OrderLineItem (Megrendelési vonal)

Ez a táblázat a kérelem törzsében található [OrderLineItem](order-resources.md#orderlineitem) tulajdonságokat ismerteti.

>[!NOTE]
>A partnerIdOnRecord csak akkor biztosított, ha egy közvetett szolgáltató egy közvetett viszonteladó nevében ad ki rendelést. Csak a közvetett viszonteladó Microsoft Partner Network (soha nem a közvetett szolgáltató azonosítója) tárolására használható.

| Név                 | Típus   | Kötelező | Leírás                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber (sor száma)       | int    | Yes      | A gyűjtemény minden soreleme egyedi sorszámot kap, amely 0-tól count-1-ig számol.                                                                                                                                                 |
| offerId (ajánlatazonosító)              | sztring | Yes      | Az ajánlat azonosítója.                                                                                                                                                                                                                      |
| subscriptionId       | sztring | No       | Az előfizetés azonosítója.                                                                                                                                                                                                               |
| parentSubscriptionId (parentSubscriptionId) | sztring | No       | Választható. A szülő-előfizetés azonosítója egy bővítményajánlatban. Csak a PATCH-re vonatkozik.                                                                                                                                                     |
| friendlyName (rövid név)         | sztring | No       | Választható. A partner által meghatározott előfizetés rövid neve, amely segít egyértelműsedni.                                                                                                                                              |
| quantity             | int    | Yes      | A licencalapú előfizetések licenceinek száma.                                                                                                                                                                                   |
| partnerIdOnRecord    | sztring | No       | Ha egy közvetett szolgáltató egy közvetett viszonteladó nevében ad ki rendelést, akkor ezt a mezőt csak a közvetett viszonteladó MPN-azonosítójával **töltse** fel (soha ne a közvetett szolgáltató azonosítójával). Ez biztosítja az ösztönzők megfelelő elszámolását. |
| provisioningContext  | Szótár<sztring, sztring>                | No       |  A katalógus egyes elemeinek kiépítéséhez szükséges információk. A termékváltozat provisioningVariables tulajdonsága jelzi, hogy mely tulajdonságok szükségesek a katalógus adott elemeihez.                  |
| Linkek                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | No       |  Csak olvasható. Az Order sorelemnek megfelelő erőforrás-hivatkozások.  |
| Attribútumok           | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | No       | Az OrderLineItem elemnek megfelelő metaadat-attribútumok. |
| renewsTo             | Objektumok tömbje                          | No    |A [RenewsTo erőforrások tömbje.](order-resources.md#renewsto)                                                                            |
| AttestationAccepted             | logikai                 | No   |  Az ajánlatra vagy termékváltozatra vonatkozó feltételeket jelzi. Csak olyan ajánlatok vagy termékváltozatok esetén szükséges, ahol a SkuAttestationProperties vagy az OfferAttestationProperties enforceAttestation true (Igaz) érték.          |
| AdditionalPartnerIdsOnRecord (További partnerazonosítókOnRecord) | Sztring | No | Ha egy közvetett szolgáltató egy közvetett viszonteladó nevében ad ki rendelést, akkor ezt a mezőt csak a további közvetett viszonteladó MPN-azonosítójával **töltse** ki (soha ne a közvetett szolgáltató azonosítójával). Az ösztönzők nem alkalmazhatók ezekre a további viszonteladókra. Csak legfeljebb 5 közvetett viszonteladót lehet megadni. Ez csak az EU-/EFTA-országokon belül tranzakciós partnerekre vonatkozik. |

##### <a name="renewsto"></a>RenewsTo

Ez a táblázat a [kérés törzsében található RenewsTo](order-resources.md#renewsto) tulajdonságokat ismerteti.

| Tulajdonság              | Típus             | Kötelező        | Leírás |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration (kifejezés-lekértség)          | sztring           | No              | A megújítási időszak időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek a **P1M (1** hónap) és **a P1Y (1** év). |

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

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [hibakódok.](error-codes.md)

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
