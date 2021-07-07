---
title: Felfüggesztett előfizetés újraaktiválása
description: Újraaktivál egy olyan előfizetést, amelyet korábban felfüggesztettek fizetés nélkül. Az Partnerközpont irányítópulton ez a művelet az ügyfél kiválasztásával hajtható végre.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c2b6e3574119f9c645cc3f730047d2a23484ad8a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547710"
---
# <a name="reactivate-a-suspended-subscription"></a>Felfüggesztett előfizetés újraaktiválása

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Újraaktivál egy [olyan előfizetést,](subscription-resources.md) amelyet korábban felfüggesztettek fizetés nélkül.

Az Partnerközpont irányítópulton ez a művelet úgy hajtható végre, hogy először [kiválaszt egy ügyfelet.](get-a-customer-by-name.md) Ezután válassza ki az átnevezni kívánt előfizetést. A befejezéshez kattintson az **Aktív gombra,** majd válassza a Küldés **lehetőséget.**

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

## <a name="c"></a>C\#

Az ügyfél előfizetésének újraaktiválához [](get-a-subscription-by-id.md)először szerezze be az előfizetést, majd módosítsa az előfizetés [**Status (Állapot) tulajdonságát.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) Az **állapotkódokkal** kapcsolatos információkért lásd: [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus). A módosítás után használja az [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) Ezután hívja meg [**a Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) Végül hívja meg a [**Patch() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)

``` csharp
// IPartner partnerOperations;
// var selectedCustomer as Customer;
// var selectedSubscription as Subscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Active
   });

```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** FeatureSamplesApplication. **Osztály:** UpdateSubscription

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus    | Kérés URI-ja                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **Javítás** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja az előfizetés újraaktiválához szükséges lekérdezési paramétert.

| Név                    | Típus     | Kötelező | Leírás                               |
|-------------------------|----------|----------|-------------------------------------------|
| **ügyfél-bérlő-azonosító**  | **guid** | Y        | Az ügyfélnek megfelelő GUID.     |
| **id-for-subscription** | **guid** | Y        | Az előfizetéshez tartozó GUID. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

A kérelem **törzsében** teljes előfizetési erőforrásra van szükség. Győződjön meg **arról, hogy** az Állapot tulajdonság frissítve lett.

### <a name="request-example"></a>Példa kérésre

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus a válasz törzsében adja vissza az előfizetés [frissített](subscription-resources.md) erőforrás-tulajdonságait.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```
