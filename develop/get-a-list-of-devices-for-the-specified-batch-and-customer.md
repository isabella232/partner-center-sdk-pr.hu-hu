---
title: A megadott köteg és ügyfél eszközlistájának lekérése
description: Eszközök és eszközök részleteinek beolvasása a megadott eszköz-kötegben az ügyfelek számára.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 36fe3b97612adfd26c1b498f31b90f743bf774cb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768240"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a>A megadott köteg és ügyfél eszközlistájának lekérése

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja

Ez a cikk azt ismerteti, hogyan kérhető le egy adott eszközhöz tartozó eszközök gyűjteménye egy adott ügyfél számára. Minden eszköz erőforrása az eszköz részletes adatait tartalmazza.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Egy eszköz batch-azonosítója.

## <a name="c"></a>C\#

Az eszközök gyűjteményének lekérése egy megadott eszköz-kötegben a megadott ügyfél számára:

1. Hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérje le a felületet a műveletekre a megadott ügyfélen.

2. Hívja meg a [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) metódust, hogy lekérje a megadott kötegre vonatkozó illesztőfelületet az eszköz batch-gyűjtési műveleteihez.

3. Kérje le az [**Devices (eszközök**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) ) tulajdonságot, és kérje meg, hogy csatolja a köteg eszköz-gyűjtemény műveleteit.

4. Az eszközök gyűjteményének lekéréséhez hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) metódust.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

Példaként tekintse meg a következőket:

- Minta: [konzol tesztelési alkalmazás](console-test-app.md)
- Projekt: **partner Center SDK-minták**
- Osztály: **GetDevices.cs**

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices http/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

A kérelem létrehozásakor használja a következő elérésiút-paramétereket.

| Név           | Típus   | Kötelező | Leírás                                           |
|----------------|--------|----------|-------------------------------------------------------|
| ügyfél-azonosító    | sztring | Igen      | Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet. |
| devicebatch-azonosító | sztring | Igen      | Az eszköz kötegét azonosító karakterlánc-azonosító. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincs

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

Ha ez sikeres, a válasz törzse az [eszköz](device-deployment-resources.md#device) erőforrásainak lapozható gyűjteményét tartalmazza. A gyűjtemény 100 eszközt tartalmaz egy oldalon. Az 100-es eszközök következő oldalának lekéréséhez a Continuationtoken argumentumot használja található MS-ContinuationToken-fejlécnek szerepelnie kell a következő kérelemben.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. Teljes listát a következő témakörben talál: [partner Center Rest](error-codes.md)-hibakódok.

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
