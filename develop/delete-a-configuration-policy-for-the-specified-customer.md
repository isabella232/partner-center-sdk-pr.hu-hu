---
title: Konfigurációs szabályzat törlése a megadott ügyfélnél
description: Adott ügyfél és szabályzatazonosító konfigurációs szabályzatának törlése.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2d6a7d392bd6af6850eb7716528e6745943bb7bb
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973026"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a>Konfigurációs szabályzat törlése a megadott ügyfélnél

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz

Adott ügyfél és szabályzatazonosító konfigurációs szabályzatának törlése.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- A szabályzat azonosítója.

## <a name="c"></a>C\#

Adott ügyfél konfigurációs szabályzatának törlése:

1. Hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával, hogy lekérje a műveletek interfészét a megadott ügyfélen.

2. Hívja meg [**a ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) metódust a szabályzat azonosítójával, hogy lekérje a megadott szabályzat konfigurációs házirend-műveleteinek felületét.

3. A konfigurációs [**szabályzat törléséhez**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) hívja meg a [**Delete vagy a DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) metódust.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** DeleteConfigurationPolicy.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus     | Kérés URI-ja                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| **Töröl** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/policies/{policy-id} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

A kérelem létrehozásakor használja a következő elérésiút-paramétereket.

| Név        | Típus   | Kötelező | Leírás                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| ügyfél-azonosító | sztring | Igen      | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.         |
| policy-id   | sztring | Igen      | Egy GUID-formátumú sztring, amely azonosítja a törölni kívánt szabályzatot. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha a válasz sikeres, a 204 No Content (Nincs tartalom) állapotkódot adja vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
