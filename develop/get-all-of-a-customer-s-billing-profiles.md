---
title: Egy ügyfél számlázási profiljának lekérése
description: Lekérte egy ügyfél számlázási profilját. Az Partnerközpont irányítópulton ezt a műveletet az ügyfél kiválasztásával hajthatja végre.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d22be53a5be4efcda76a568578468615495febb6
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760589"
---
# <a name="get-a-customers-billing-profile"></a>Egy ügyfél számlázási profiljának lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Lekérte egy ügyfél számlázási profilját.

A Partnerközpont a művelet végrehajtásához először ki kell [választania egy ügyfelet.](get-a-customer-by-name.md) Ezután a bal oldali oldalsávon az ügyfél neve alatt válassza a **Fiók lehetőséget.** A számlázási profil a Számlázási adatok fejléc alatt **található.**

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Az ügyfél számlázási profiljának lehívásához használja [**az IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) Ezután hívja meg [**a Profiles (Profilok)**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) tulajdonságot, majd a [**Billing (Számlázás)**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) tulajdonságot. Végül hívja meg a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync)

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** PartnerSDK.FeatureSamples **osztály:** GetCustomerBillingProfile.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A számlázási profil lekérdezhető a következő lekérdezési paraméterrel.

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a>REST-válasz

Ha ez a módszer sikeres, a válasz törzsében [profilerőforrások](profile-resources.md) gyűjteményét adja vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 1206
Content-Type: application/json
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
Date: Mon, 23 Nov 2015 18:13:43 GMT

{
    "id": "<billing-profile-id>",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "CompanyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "firstName": "FirstName",
        "lastName": "LastName",
        "phoneNumber": "4255555555"
    },
    "links": {
        "self": {
            "uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "<etag>",
        "objectType": "CustomerBillingProfile"
    }
}
```
