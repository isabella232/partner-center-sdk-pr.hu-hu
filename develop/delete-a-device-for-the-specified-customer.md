---
title: Eszköz törlése a megadott ügyfélnél
description: Megadott ügyfélhez tartozó eszköz törlése.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1e05ceb8615d6f84c1df101c542342f9a6eb04b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973077"
---
# <a name="delete-a-device-for-the-specified-customer"></a>Eszköz törlése a megadott ügyfélnél

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz

Ez a cikk egy adott ügyfélhez tartozó eszköz törlését ismerteti.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Az eszköz kötegazonosítója.

- Az eszköz azonosítója.

## <a name="c"></a>C\#

Eszköz törlése a megadott ügyfél számára:

1. Hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóval az ügyfélen folytatott műveletek interfészének lekérése érdekében.

2. Hívja meg [**a DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) metódust az eszköz kötegazonosítójának használatával, hogy lekért egy interfészt a megadott köteg műveleteihez.

3. Hívja meg [**a Devices.ById metódust,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) hogy lekért egy interfészt a művelethez a megadott eszközön.

4. Az eszköz [**kötegből**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) való törléséhez hívja meg a Delete vagy [**a DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) metódust.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** DeleteDevice.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus     | Kérés URI-ja                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/deviceBatches/{devicebatch-id}/devices/{eszközazonosító} HTTP/1.1  |

#### <a name="uri-parameters"></a>URI-paraméterek

A kérelem létrehozásakor használja az alábbi elérésiút-paramétereket.

| Név           | Típus   | Kötelező | Leírás                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| ügyfél-azonosító    | sztring | Igen      | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.              |
| devicebatch-id | sztring | Igen      | Az eszközt tartalmazó köteg eszközkötet-azonosítója. |
| eszközazonosító      | sztring | Igen      | Az eszköz azonosítója.                                             |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices/7b11cd8b-dd1e-4840-8c4a-84215e4de782 HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha a válasz sikeres, a **204 Nincs** tartalom állapotkódot adja vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
