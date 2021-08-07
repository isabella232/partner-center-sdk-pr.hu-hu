---
title: A megadott köteg és ügyfél eszközlistájának lekérése
description: Eszköz- és eszközadatok gyűjteményének lekérése a megadott eszközkötetben az ügyfél számára.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 77dcab4b26a74cec886e6b654c3abdcb97007ed8e14966873ce43fdcbc1d2809
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989406"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a>A megadott köteg és ügyfél eszközlistájának lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz

Ez a cikk azt ismerteti, hogyan lehet lekérni egy adott eszközkötetben található eszközgyűjteményt egy adott ügyfél számára. Minden eszközerőforrás az eszköz adatait tartalmazza.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy eszközkötet-azonosító.

## <a name="c"></a>C\#

Egy adott eszközkötetben található eszközök gyűjteményének lekérése a megadott ügyfél számára:

1. Hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával, hogy lekérje a műveletek interfészét a megadott ügyfélen.

2. A [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) metódus hívásával lekért egy interfészt az eszközkötet-gyűjtési műveletekhez a megadott köteghez.

3. Az [**Eszközök tulajdonság lekérésével**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) illesztőfelületet kap a köteg eszközgyűjteményi műveleteihez.

4. Az eszközök [**gyűjteményének**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) lekéréséhez hívja meg a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) metódust.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

Példaként tekintse meg a következőket:

- Minta: [Konzoltesztalkalmazás](console-test-app.md)
- Project: **Partnerközpont SDK minták**
- Osztály: **GetDevices.cs**

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/deviceBatches/{devicebatch-id}/devices HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

A kérelem létrehozásakor használja az alábbi elérésiút-paramétereket.

| Név           | Típus   | Kötelező | Leírás                                           |
|----------------|--------|----------|-------------------------------------------------------|
| ügyfél-azonosító    | sztring | Yes      | Egy GUID formátumú sztring, amely azonosítja az ügyfelet. |
| devicebatch-id | sztring | Yes      | Az eszközkötetet azonosító sztringazonosító. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse az eszközerőforrások [lapszámált gyűjteményét](device-deployment-resources.md#device) tartalmazza. A gyűjtemény 100 eszközt tartalmaz egy oldalon. A 100 eszköz következő oldalának lekéréséhez a válasz törzsében található continuationToken-nek a következő kérelemben kell szerepelnie az MS-ContinuationToken fejléceként.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a REST Partnerközpont [hibakódokat.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 1742
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 2,
    "items":
    [{
            "id": "7c141ea9-2816-4e15-a819-53f6856499ff",
            "serialNumber": "2R9-ZNP67",
            "productKey": "00329-00000-0003-AA6069",
            "modelName": "Precision WorkStation T7500",
            "oemManufacturerName":"Dell Inc.",
            "policies":[{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate":"2017-08-09T14:43:26.0092288-07:00",
            " attributes": {
                "objectType": "Device"
            }
        }, {
            "id": "e528a62f-5031-49f4-bea7-5fafe47388fd",
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "modelName": "HP Z420 Workstation",
            "oemManufacturerName": "Hewlett-Packard",
            "policies": [{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate": "2017-08-09T14:35:51.3126144-07:00",
            "attributes": {
                "objectType": "Device"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
