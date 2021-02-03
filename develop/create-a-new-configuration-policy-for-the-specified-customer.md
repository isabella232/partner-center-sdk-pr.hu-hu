---
title: Új ügyfél-konfigurációs házirend létrehozása
description: Ismerje meg, hogyan hozhat létre új konfigurációs házirendet a partner Center API-kkal egy adott ügyfélhez. A cikk előfeltételeket, lépéseket és példákat tartalmaz.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 21a0bfde7f931371ff09d6c27de0281a4ed3b3cb
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768639"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a>Új konfigurációs szabályzat létrehozása a megadott ügyfélnél

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja

Új konfigurációs házirend létrehozása a megadott ügyfélhez.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Új konfigurációs házirend létrehozása a megadott ügyfélhez:

1. A következő kódrészletben látható módon hozza létre az új [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) objektumot. Ezután hívja meg a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérje le a felületet a műveletekre a megadott ügyfélen.

2. Kérje le a [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) tulajdonságot, és szerezzen be egy felületet a konfigurációs házirend-gyűjtési műveletekhez.

3. A konfigurációs szabályzat létrehozásához hívja meg a [**create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metódust.

### <a name="c-example"></a>C \# példa

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var configurationPolicyToCreate = new ConfigurationPolicy
{
    Name = "Test Config Policy",
    Description = "This configuration policy is created by the SDK samples",
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.SkipEula }
};

var createdConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Create(configurationPolicyToCreate);
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: CreateConfigurationPolicy.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                              |
|----------|------------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies http/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

A kérelem létrehozásakor használja a következő elérésiút-paramétereket.

| Név        | Típus   | Kötelező | Leírás                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ügyfél-azonosító | sztring | Igen      | Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

A kérelem törzsének tartalmaznia kell egy olyan objektumot, amely tartalmazza a konfigurációs házirend adatait az alábbi táblázatban leírtak szerint:

| Név           | Típus             | Kötelező | Leírás                      |
|----------------|------------------|----------|----------------------------------|
| name           | sztring           | Igen      | A szabályzat rövid neve. |
| category       | sztring           | Igen      | A szabályzat kategóriája.             |
| leírás    | sztring           | No       | A szabályzat leírása.          |
| policySettings | sztringek tömbje | Igen      | A házirend-beállítások.             |

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com//v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 212
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"]
}
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse tartalmazza az új szabályzathoz tartozó [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) -erőforrást.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 404
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4beda413-74fc-4839-b74f-f580c353ab45
MS-RequestId: 0dfadf74-aa66-49ed-9a67-b3b78d9297cc
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:36 GMT

{
    "id": "40cdb858-edcc-44d7-9083-d6a36d43bd3f",
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
    "createdDate": "2017-07-25T18:07:36",
    "lastModifiedDate": "2017-07-25T18:07:36",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
