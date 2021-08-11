---
title: Egy ügyfél vállalati profiljának lekérése
description: Lekérte egy ügyfél céges profilját.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: fb8c21c8307480bb0573e189ac95cc05756f9080f6156ff860d8193f134c4aa6
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992976"
---
# <a name="get-a-customers-company-profile"></a>Egy ügyfél vállalati profiljának lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Lekérte egy ügyfél céges profilját.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Az ügyfél céges profiljának lehíváshoz hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához. Ezután szerezze be az ügyfél [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) felületét a [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) (Profilok) tulajdonságból, hogy hozzáférjen a Cég tulajdonsághoz. Ezután szerezze be az [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) felületet az [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) tulajdonságból, és hívja meg a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) [**GetAsync() metódusokat.**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync)

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

**Minta:** [Töltse le a Partnerközpont SDK.](https://go.microsoft.com/fwlink/p/?LinkId=746681) **Project:** PartnerSdk.FeatureSamples **osztály:** GetCustomerCompanyProfile.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Az ügyfél céges profiljának lehíváshoz hívja meg az **IAggregatePartner.getCustomers().byId** függvényt az ügyfél azonosítóval az ügyfél azonosításához. Ezután szerezze be az ügyfél **ICustomerProfileCollection** felületét a [**getProfiles**] függvényből, hogy hozzáférjen a Cég tulajdonsághoz. Ezután szerezze be az **ICustomerReadonlyProfile** felületet az **ICustomerProfileCollection.getCompany függvényből,** és hívja meg a **get** függvényt.

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                             |
|---------|-------------------------------------------------------------------------|
| **Kap** | *{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A következő lekérdezési paraméterrel lekérdezheti a vállalati profilt.

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlőazonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus a válasz törzsében ad vissza információt.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 488
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CV: /e74N8OrkE29ycwZ.0
MS-ServerId: 101112202
Date: Wed, 04 Jan 2017 19:48:51 GMT

{
    "tenantId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "domain": "dtdemocspcustomer005.onmicrosoft.com",
    "companyName": "DT Demo CSP Customer 005",
    "address": {
        "country": "US",
        "region": "WA",
        "city": "Redmond ",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "phoneNumber": "4155551212"
    },
    "email": "daniel@hotmail.com.tw",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerCompanyProfile"
    }
}
```
