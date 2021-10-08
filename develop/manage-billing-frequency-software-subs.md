---
title: Szoftver-előfizetések számlázási gyakoriságának kezelése
description: Frissítse egy előfizetési erőforrás számlázási gyakoriságát, amely megfelel az ügyfél és az előfizetés azonosítójának.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3cacfe94868afb0b4c1c93842b187d653dffe64f
ms.sourcegitcommit: 36e88224d0957b7ea6298789c75cdd18fc0f3685
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/07/2021
ms.locfileid: "129664937"
---
# <a name="update-billing-frequency-for-software-subscriptions"></a>A szoftver-előfizetések számlázási gyakoriságának frissítése

**A következőkre vonatkozik:** Partnerközpont

Frissítse egy szoftver előfizetési erőforrásának számlázási [gyakoriságát,](subscription-resources.md) amely megfelel az ügyfél és az előfizetés azonosítójának.

A Partnerközpont ezt a műveletet úgy hajtjuk végre, hogy először kiválasztunk [egy ügyfelet.](get-a-customer-by-name.md) Ezután válassza ki a frissíteni kívánt előfizetést. Végül kattintson a Manage scheduled changed (Ütemezetten módosítottak kezelése) elemre a beállítás kiválasztásához, majd válassza a **Save (Mentés) lehetőséget.**

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, a következő irányítópulton Partnerközpont [ki:](https://partner.microsoft.com/dashboard). Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

## <a name="c"></a>C\#

Az ügyfél szoftveres előfizetésének [](get-a-subscription-by-id.md)frissítéséhez először szerezze be az előfizetést, majd állítsa be az előfizetés [**billingCycle tulajdonságát.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.billingCycle) A módosítás után használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById() metódust.** Ezután hívja meg [**a Subscriptions tulajdonságot,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) majd a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) Végül hívja meg a **Patch() metódust.**

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

this.Context.ConsoleHelper.StartProgress("Updating subscription scheduled change");
selectedSubscription.ScheduledNextTermInstructions = new ScheduledNextTermInstructions
{
    Product = new ProductTerm
    {
        ProductId = changeToProductId,
        SkuId = changeToSkuId,
        AvailabilityId = changeToAvailabilityId,
        BillingCycle = changeToBillingCycle,
        TermDuration = changeToTermDuration,
    },
    Quantity = changeToQuantity,
};

var updatedSubscription = subscriptionOperations.Patch(selectedSubscription);
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** PartnerSDK.FeatureSample **osztály:** UpdateSubscription.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus    | Kérés URI-ja                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **JAVÍTÁS** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja az előfizetés felfüggesztéséhez szükséges lekérdezési paramétert.

| Név                    | Típus     | Kötelező | Leírás                               |
|-------------------------|----------|----------|-------------------------------------------|
| **ügyfél-bérlő-azonosító**  | **GUID** | Y        | Az ügyfélnek megfelelő GUID.     |
| **id-for-subscription** | **GUID** | Y        | Az előfizetéshez tartozó GUID. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

A kérelem törzsében egy teljes **kereskedelmi** piactéri előfizetési erőforrásra van szükség. Győződjön meg arról, hogy az **AutoRenewEnabled tulajdonság** frissült.

### <a name="request-example-for-a-software-subscription"></a>Szoftver-előfizetésre vonatkozó példa kérése

```http
{ 
    "id": "d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
    "offerId": "DG7GMGF0DVSV:000P:DG7GMGF0F3Q9", 
    "offerName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "friendlyName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "productType": { 
        "id": "Software", 
        "displayName": "Software" 
    }, 
    "quantity": 1, 
    "unitType": "Licenses", 
    "hasPurchasableAddons": false, 
    "creationDate": "2021-09-14T16:44:14.1210743Z", 
    "effectiveStartDate": "2021-09-14T16:44:03.4609789Z", 
    "commitmentEndDate": "2024-09-13T00:00:00Z", 
    "cancellationAllowedUntilDate": "2021-10-14T23:59:00Z", 
    "status": "active", 
    "autoRenewEnabled": true, 
    "scheduledNextTermInstructions": { 
      "product": { 
         "productId":  "DG7GMGF0DVSV", 
         "skuId":  "000P", 
         "availabilityId":  "DG7GMGF0F3Q9", 
         "billingCycle":  "Annual", 
         "termDuration":  "P3Y" 
        }, 
      "quantity":  1 
     },  // original value = null 
    "isTrial": false, 
    "billingType": "license", 
    "billingCycle": "triennial", 
    "termDuration": "P3Y", 
    "renewalTermDuration": "", 
    "isMicrosoftProduct": true, 
    "partnerId": "", 
    "attentionNeeded": false, 
    "actionTaken": false, 
    "contractType": "subscription", 
    "links": { 
        "product": { 
            "uri": "/products/DG7GMGF0DVSV?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "sku": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "availability": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P/availabilities/DG7GMGF0F3Q9?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "self": { 
            "uri": "/customers/1f53d7b3-cd04-43a3-a09f-e52f3eb3c205/subscriptions/d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
            "method": "GET", 
            "headers": [] 
        } 
    }, 
    "publisherName": "Microsoft", 
    "orderId": "123456789101", 
    "attributes": { 
        "objectType": "Subscription" 
    } 
} 
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus a válasz törzsében adja vissza az előfizetés [frissített](subscription-resources.md) erőforrás-tulajdonságait.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
{ 
    "id": "d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
    "offerId": "DG7GMGF0DVSV:000P:DG7GMGF0F3Q9", 
    "offerName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "friendlyName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "productType": { 
        "id": "Software", 
        "displayName": "Software" 
    }, 
    "quantity": 1, 
    "unitType": "Licenses", 
    "hasPurchasableAddons": false, 
    "creationDate": "2021-09-14T16:44:14.1210743Z", 
    "effectiveStartDate": "2021-09-14T16:44:03.4609789Z", 
    "commitmentEndDate": "2024-09-13T00:00:00Z", 
    "cancellationAllowedUntilDate": "2021-10-14T23:59:00Z", 
    "status": "active", 
    "autoRenewEnabled": true, 
    "scheduledNextTermInstructions": { 
      "product": { 
         "productId":  "DG7GMGF0DVSV", 
         "skuId":  "000P", 
         "availabilityId":  "DG7GMGF0F3Q9", 
         "billingCycle":  "Annual", 
         "termDuration":  "P3Y" 
        }, 
      "quantity":  1 
     },  // original value = null 

    "isTrial": false, 
    "billingType": "license", 
    "billingCycle": "triennial", 
    "termDuration": "P3Y", 
    "renewalTermDuration": "", 
    "isMicrosoftProduct": true, 
    "partnerId": "", 
    "attentionNeeded": false, 
    "actionTaken": false, 
    "contractType": "subscription", 
    "links": { 
        "product": { 
            "uri": "/products/DG7GMGF0DVSV?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "sku": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "availability": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P/availabilities/DG7GMGF0F3Q9?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "self": { 
            "uri": "/customers/1f53d7b3-cd04-43a3-a09f-e52f3eb3c205/subscriptions/d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
            "method": "GET", 
            "headers": [] 
        } 
    }, 
    "publisherName": "Microsoft", 
    "orderId": "123456789101", 
    "attributes": { 
        "objectType": "Subscription" 
    } 
} 
```
