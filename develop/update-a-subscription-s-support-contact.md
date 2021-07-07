---
title: Egy előfizetés támogatási kapcsolattartójának frissítése
description: Hogyan frissítheti egy előfizetés támogatási kapcsolattartóját a partner egyik hozzáadott értékkel bővült viszonteladóira.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c89f91fc9e89384a7be1237c08d7a9a1cfe3164
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530361"
---
# <a name="update-a-subscriptions-support-contact"></a>Egy előfizetés támogatási kapcsolattartójának frissítése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Hogyan frissítheti egy előfizetés támogatási kapcsolattartóját a partner egyik hozzáadott értékkel bővült viszonteladóira.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

- Az új támogatási kapcsolattartóval kapcsolatos információk: bérlőazonosító, Microsoft Partner Network azonosító és név. A támogatási kapcsolattartónak a partner értékével hozzáadott viszonteladók egyikének kell lennie.

## <a name="c"></a>C\#

Az előfizetés támogatási kapcsolattartóját úgy frissítheti, hogy először példányosul, majd feltölti a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) objektumot az új értékekkel. Ezután használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához. Ezután szerezze be az előfizetési műveletek interfészét a [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódus az előfizetés azonosítójával való hívásával. Ezután a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) tulajdonság használatával szerezzen be egy felületet, amely támogatja a kapcsolattartási műveleteket. Végül hívja meg az [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) vagy [**az UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) metódust a kitöltve a SupportContact objektummal a támogatási kapcsolattartó frissítéséhez.

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Instantiate a SupportContact object and populate it with the new support contact information.
var supportContact = new SupportContact()
{
    Name = "Support contact's name",
    SupportTenantId = "Support contact's tenant ID",
    SupportMpnId = "Support contact's MPN ID"
};

// Update the support contact with a new object that has valid VAR values.
var updatedSupportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).SupportContact.Update(supportContact);
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** Partnerközpont SDK **Osztály:** UpdateSubscriptionSupportContact.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/supportcontact HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az ügyfél és az előfizetés azonosításához használja az alábbi elérésiút-paramétereket.

| Név            | Típus   | Kötelező | Leírás                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| ügyfél-azonosító     | sztring | Igen      | Egy GUID formátumú sztring, amely azonosítja az ügyfelet.           |
| subscription-id (előfizetés-azonosító) | sztring | Igen      | A próba-előfizetést azonosító GUID formátumú sztring. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

A kérés törzsében meg kell lennie egy [feltöltve a SupportContact](subscription-resources.md#supportcontact) erőforrásnak. A támogatási kapcsolattartónak egy meglévő viszonteladónak kell lennie, aki kapcsolatban áll a partnerrel.

### <a name="request-example"></a>Példa kérésre

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b72d732a-eed7-4a60-82d1-1b2e6cba0ed2
MS-CorrelationId: 84eff9e1-6a8c-42aa-8678-c00b0d3fb26f
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 320
Expect: 100-continue

{
    "SupportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "SupportMpnId": "4391507",
    "Name": "Trey Research",
    "Links": {
        "Self": {
            "Uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "Method": "Get",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "SupportContact"
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse tartalmazza a [SupportContact erőforrást.](subscription-resources.md#supportcontact)

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b0cd9bcc-742e-4c76-9e34-a96d3bdc7673
MS-RequestId: 7591ca22-d4e3-409d-bfa6-09806eaff4f3
MS-CV: W8Tzj6NGckKHcq+E.0
MS-ServerId: 030020344
Date: Wed, 21 Jun 2017 01:01:17 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
