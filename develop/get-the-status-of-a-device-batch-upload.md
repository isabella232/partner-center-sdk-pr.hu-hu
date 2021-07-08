---
title: Eszköz kötegelt feltöltési állapotának lekérése
description: Eszköz kötegelt feltöltési állapotának lekért állapota egy adott ügyfél számára.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd8726af41fe4399797f39a0790cf962fde64acc
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548481"
---
# <a name="get-the-status-of-a-device-batch-upload"></a>Eszköz kötegelt feltöltési állapotának lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz

Eszköz kötegelt feltöltési állapotának lekért állapota egy adott ügyfél számára.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- A Hely fejlécben az eszközkötet beküldtekor visszaadott kötegkövetési azonosítót. További információ: [Eszközök listájának feltöltése a megadott ügyfél számára.](upload-a-list-of-devices-for-the-specified-customer.md)

## <a name="c"></a>C\#

Az eszköz kötegelt feltöltési állapotának lekéréséhez először hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával, hogy lekérje a megadott ügyfél műveleteinek interfészét. Ezután hívja meg a [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) metódust a kötegkövetési azonosítóval a kötegelt feltöltési állapotműveletek interfészének lehívása érdekében. Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) vagy [**GetAsync metódust**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) az állapot lekéréshez.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** GetBatchUploadStatus.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfél-azonosító}/batchJobStatus/{batchtracking-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A kérelem létrehozásakor használja a következő elérésiút-paramétereket.

| Név             | Típus   | Kötelező | Leírás                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ügyfélazonosító      | sztring | Igen      | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.                                                                                                                          |
| batchtracking-id | sztring | Igen      | Egy GUID formátumú azonosító, amely az eszközkötet feltöltési állapotának lekérésére használatos. Ezt az azonosítót az eszközkötet sikeres beküldtekor a Hely fejlécben kell visszaadni. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz tartalmaz egy [BatchUploadDetails erőforrást.](device-deployment-resources.md#batchuploaddetails)

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 400
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "batchTrackingId": "0127ed8e-ff72-4983-a3d8-e8d8bd378932",
    "status": "finished",
    "startedTime": "2017-07-25T10:00:00",
    "completedTime": "2017-07-25T10:10:00",
    "devicesStatus": [{
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "status": "finished_with_errors",
            "errorCode": "808",
            "errorDescription": "ZtdDeviceAssignedToOtherTenant",
            "attributes": {
                "objectType": "DeviceUploadDetails"
            }
        }
    ],
    "attributes": {
        "objectType": "BatchUploadDetails"
    }
}
```
