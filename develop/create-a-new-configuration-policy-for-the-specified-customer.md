---
title: Új ügyfél-konfigurációs szabályzat létrehozása
description: Megtudhatja, hogyan hozhat létre Partnerközpont új konfigurációs szabályzatot egy adott ügyfél számára a Partnerközpont API-k használatával. A cikk előfeltételeket, lépéseket és példákat tartalmaz.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b3637b6d482934d894a5807734b541cc73dea3f265b5460ba807c7fad6834a82
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991616"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a>Új konfigurációs szabályzat létrehozása a megadott ügyfélnél

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz

Új konfigurációs szabályzat létrehozása a megadott ügyfél számára.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Új konfigurációs szabályzat létrehozása a megadott ügyfél számára:

1. Példányositsa az új [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) objektumot az alábbi kódrészletben látható módon. Ezután hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával, hogy lekérje a megadott ügyfél műveleteinek interfészét.

2. A [**ConfigurationPolicies tulajdonság lekérése**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) a konfigurációs házirend-gyűjtési műveletek felületének lekéréséhez.

3. A konfigurációs [**szabályzat létrehozásához**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) hívja meg a Create vagy [**a CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metódust.

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

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **osztály:** CreateConfigurationPolicy.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                              |
|----------|------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/policies HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

A kérelem létrehozásakor használja a következő elérésiút-paramétereket.

| Név        | Típus   | Kötelező | Leírás                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ügyfélazonosító | sztring | Yes      | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

A kérelem törzsének tartalmaznia kell egy objektumot, amely tartalmazza a konfigurációs szabályzat adatait az alábbi táblázatban leírtak szerint:

| Név           | Típus             | Kötelező | Leírás                      |
|----------------|------------------|----------|----------------------------------|
| name           | sztring           | Yes      | A szabályzat rövid neve. |
| category       | sztring           | Yes      | A szabályzat kategóriája.             |
| leírás    | sztring           | No       | A szabályzat leírása.          |
| policySettings | sztringek tömbje | Yes      | A szabályzat beállításai.             |

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

Ha ez sikeres, a válasz törzse tartalmazza az új szabályzat [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) erőforrását.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
