---
title: Konfigurációs szabályzat frissítése a megadott ügyfélnél
description: A megadott ügyfél konfigurációs házirendjének frissítése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 42c57a92020723415b4621e9f9d7c5c3278bfb77
ms.sourcegitcommit: 970031473b2e8cd3d08c6c097949c057a51df3ef
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505339"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a>Konfigurációs szabályzat frissítése a megadott ügyfélnél

**A következőkre vonatkozik**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja

A megadott ügyfél konfigurációs házirendjének frissítése.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- A házirend-azonosító.

## <a name="c"></a>C\#

Ha frissíteni szeretne egy meglévő konfigurációs házirendet a megadott ügyfél számára, egy új [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) objektumot hoz létre, ahogy az a következő kódrészletben látható. Az új objektum értékei a meglévő objektum megfelelő értékeit cserélik le. Ezután hívja meg a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérje le a felületet a műveletekre a megadott ügyfélen. Ezután hívja meg a [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) metódust a házirend-azonosítóval, hogy lekérje az adott szabályzathoz tartozó konfigurációs házirend műveleteihez szükséges felületet. Végül hívja meg a [**patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) vagy a [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) metódust a konfigurációs szabályzat frissítéséhez.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: UpdateConfigurationPolicy.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A kérelem létrehozásakor használja a következő elérésiút-paramétereket.

| Név        | Típus   | Kötelező | Leírás                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| ügyfél-azonosító | sztring | Igen      | Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.         |
| házirend-azonosító   | sztring | Igen      | Egy GUID-formázott karakterlánc, amely a frissítendő szabályzatot azonosítja. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

A kérés törzsének tartalmaznia kell egy objektumot, amely megadja a szabályzat adatait.

| Név            | Típus             | Kötelező | Frissíthető | Leírás                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| id              | sztring           | Igen      | Nem        | A házirendet azonosító GUID formátumú karakterlánc.                                                                                                    |
| name            | sztring           | Igen      | Igen       | A szabályzat rövid neve.                                                                                                                         |
| category        | sztring           | Igen      | Nem        | A szabályzat kategóriája.                                                                                                                                     |
| leírás     | sztring           | Nem       | Igen       | A szabályzat leírása.                                                                                                                                  |
| devicesAssigned | szám           | Nem       | Nem        | Az eszközök száma.                                                                                                                                   |
| policySettings  | sztringek tömbje | Igen      | Igen       | A házirend-beállítások: "None", " \_ OEM- \_ előtelepítések eltávolítása", "Oobe \_ felhasználó \_ nem \_ helyi \_ rendszergazda", "expressz beállítások kihagyása \_ \_ ", "az \_ OEM- \_ regisztráció \_ kihagyása", "kihagyott EULA". |

### <a name="request-example"></a>Példa kérésre

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse tartalmazza az új szabályzathoz tartozó [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) -erőforrást.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
