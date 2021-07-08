---
title: Egy ügyfél szabályzati listájának lekérése
description: A megadott ügyfél konfigurációs házirendek gyűjteményének lekérése.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: bf6ace0d2425e28d80c4f2310878c2d2a9e2a876
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874584"
---
# <a name="get-a-list-of-a-customers-policies"></a>Egy ügyfél szabályzati listájának lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz

Ez a cikk azt ismerteti, hogyan lehet lekérni a megadott ügyfél konfigurációs szabályzatának gyűjteményét.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Az ügyfél összes szabályzatának listáját a következővel lehet lekérte:

1. Hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával, hogy lekérje a műveletek interfészét a megadott ügyfélen.

2. A [**ConfigurationPolicies tulajdonság lekérésével**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) lekéri a konfigurációs szabályzatgyűjtemény műveleteinek felületét.
3. A [**szabályzatgyűjtemény lekéréséhez**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) hívja meg a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) metódust.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

var configPolicies = partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Get();
```

Példaként tekintse meg a következőket:

- Minta: [Konzoltesztalkalmazás](console-test-app.md)
- Project: **Partnerközpont SDK minták**
- Osztály: **GetAllConfigurationPolicies.cs**

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                              |
|---------|------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/policies HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

A kérelem létrehozásakor használja a következő elérésiút-paramétert:

| Név        | Típus   | Kötelező | Leírás                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ügyfél-azonosító | sztring | Igen      | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
Content-Length:0
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse [tartalmazza a ConfigurationPolicy erőforrások gyűjteményét.](device-deployment-resources.md#configurationpolicy)

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a REST Partnerközpont [hibakódokat.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 1221
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d5ff2573-3ef8-4553-aac4-4b73d97dce1b
MS-RequestId: 6eb7383d-eeb5-44d7-8570-e0ed12c0547a
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:49 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "8c7d25aa-2dbb-409c-a1f0-f55bd9108fa9",
            "name": "Windows 10 Enterprise E3",
            "category": "o_o_b_e",
            "description": "P462017 description",
            "devicesAssigned": 0,
            "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
            "createdDate": "2017-04-27T11:30:34.1944704-07:00",
            "lastModifiedDate": "2017-04-27T11:30:34.1944704-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }, {
            "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
            "name": "Test policy",
            "category": "o_o_b_e",
            "description": "Test policy creation from API 1",
            "devicesAssigned": 0,
            "policySettings": ["skip_express_settings"],
            "createdDate": "2017-07-25T11:03:03.8457088-07:00",
            "lastModifiedDate": "2017-07-25T11:04:00.8150016-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }, {
            "id": "a96b5fd9-0f3a-419a-b55c-a8aecd6b1f00",
            "name": "Windows 10 Enterprise E5",
            "category": "o_o_b_e",
            "description": "test policy creation from API",
            "devicesAssigned": 0,
            "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
            "createdDate": "2017-07-25T11:07:36.1501184-07:00",
            "lastModifiedDate": "2017-07-25T11:07:36.1501184-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
