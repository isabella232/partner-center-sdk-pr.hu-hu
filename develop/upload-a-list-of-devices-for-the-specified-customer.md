---
title: Eszközök listájának feltöltése a megadott ügyfél meglévő kötegére
description: Az eszközökre vonatkozó információk listájának feltöltése egy meglévő kötegbe a megadott ügyfél számára. Ez egy már létrehozott eszközkötethez társítja az eszközöket.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3fa9cff39113130c54cecfaef1f8ca28e0ac5adf
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530310"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a>Eszközök listájának feltöltése a megadott ügyfél meglévő kötegére

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz

Az eszközökre vonatkozó információk listájának feltöltése egy meglévő kötegbe a megadott ügyfél számára. Ez egy már létrehozott eszközkötethez társítja az eszközöket.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Az eszköz kötegazonosítója.

- Az egyes eszközökre vonatkozó információkat szolgáltató eszközerőforrások listája.

## <a name="c"></a>C\#

Az eszközök listájának meglévő eszközkötetre való feltöltéséhez először példányosítenie kell egy új [List/dotnet/api/system.collections.generic.list-1) típusú eszközt, és töltse fel a listát az eszközökkel. [](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) Az egyes eszközök azonosításához legalább a következő tulajdonságkombinációk szükségesek:

- [**HardwareHash (Hardverhash)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey (Termékkulcs).**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)

- [**HardwareHash (Hardverhash)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)( Sorozatszám).

- [**HardwareHash (Hardverhash)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey (Termékkulcs)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)( Sorozatszám).

- [**Csak HardverHash.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)

- [**Csak ProductKey.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)

- [**SerialNumber (Sorozatszám)**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName ( Modellnév).**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname)

Ezután hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóval a megadott ügyfél műveleteinek interfészének lekérése érdekében. Ezután hívja meg a [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) metódust az eszköz kötegazonosítójának használatával, hogy lekérte a megadott köteg műveleteinek interfészét. Végül hívja meg a [**Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) vagy [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) metódust az eszközök listájával, hogy hozzáadja az eszközöket az eszközkötemhez.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash1234",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    },

    new Device
    {
        HardwareHash = "DummyHash12345",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    }
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Create(devicesToBeUploaded);
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** CreateDevices.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus   | Kérés URI-ja                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/deviceBatches/{devicebatch-id}/devices HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A kérelem létrehozásakor használja a következő elérési utat és lekérdezési paramétereket.

| Név           | Típus   | Kötelező | Leírás                                           |
|----------------|--------|----------|-------------------------------------------------------|
| ügyfélazonosító    | sztring | Igen      | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet. |
| devicebatch-id | sztring | Igen      | Az eszközkötetet azonosító sztringazonosító. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

A kérelem törzsének eszközobjektumok [tömböt kell tartalmaznia.](device-deployment-resources.md#device) Az eszköz azonosítására a következő mezőkombinációk fogadhatóak el:

- hardwareHash + productKey.
- hardwareHash + serialNumber.
- hardwareHash + productKey + serialNumber.
- csak hardwareHash.
- Csak productKey.
- serialNumber + oemManufacturerName + modelName.

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches/Test/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 482
Expect: 100-continue

[{
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash1234",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }, {
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash12345",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }
]
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz tartalmaz egy **Location** fejlécet, amely rendelkezik egy URI-azonosítóval, amely az eszköz feltöltési állapotának lekérésére használható. Mentse ezt az URI-t a többi kapcsolódó REST API-val való használathoz.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/16c00110-e79a-433d-aa28-f69dd60df671
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CV: OBkGN9pSN0a5xvua.0
MS-ServerId: 101112012
Date: Thu, 28 Sep 2017 20:08:46 GMT
```
