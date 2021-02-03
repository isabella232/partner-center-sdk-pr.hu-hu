---
title: Ügyfél létrehozása egy közvetett viszonteladónál
description: Megtudhatja, hogyan használhatja a közvetett szolgáltató a partner Center API-kat, hogy ügyfelet hozzon létre egy közvetett viszonteladó számára.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e2386f1963a5bb3ea4269bcbf4327c75987f3b91
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768642"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a>Ügyfél létrehozása közvetett viszonteladók számára a partner Center API-k használatával

**A következőkre vonatkozik:**

- Partnerközpont

A közvetett szolgáltató létrehozhat egy ügyfelet közvetett viszonteladónak.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- A közvetett viszonteladó bérlői azonosítója.

- A közvetett viszonteladónak partneri kapcsolattal kell rendelkeznie a közvetett szolgáltatóval.

## <a name="c"></a>C\#

Új ügyfél hozzáadása közvetett viszonteladóhoz:

1. Új [**ügyfél**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) -objektum létrehozása, majd a [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) és a [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)példányának létrehozása és feltöltése. Ügyeljen arra, hogy a közvetett viszonteladó AZONOSÍTÓját a [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) tulajdonsághoz rendelje.

2. A [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) tulajdonsággal szerezzen be egy felületet az ügyfél-gyűjtési műveletekhez.

3. A [**create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metódus meghívásával hozza létre az ügyfelet.

### <a name="c-example"></a>C \# példa

``` csharp
// IAggregatePartner partnerOperations;
// var indirectResellerId;
var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "WingtipToys{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "Gena@wingtiptoys.com",
        Language = "En",
        CompanyName = "Wingtip Toys" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Gena",
            LastName = "Soto",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = "4255550101"
        }
    },
    AssociatedPartnerId = indirectResellerId
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: CreateCustomerforIndirectReseller.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                       |
|----------|-------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers http/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.

| Név                                          | Típus   | Kötelező | Leírás                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BillingProfile](#billing-profile)             | object | Igen      | Az ügyfél számlázási profiljának adatai.                                                                                                                                                                                                                                                                                                           |
| [CompanyProfile](#company-profile)             | object | Igen      | Az ügyfél vállalati profiljának adatai.                                                               
| [AssociatedPartnerId](customer-resources.md#customer) | sztring | Igen      | A közvetett viszonteladó azonosítója. Az itt megadott azonosító által jelzett közvetett viszonteladónak partneri kapcsolattal kell rendelkeznie a közvetett szolgáltatóval, vagy a kérés sikertelen lesz. Azt is vegye figyelembe, hogy ha a AssociatedPartnerId érték nincs megadva, az ügyfél a közvetett szolgáltató közvetlen ügyfeleként jön létre a közvetett viszonteladó helyett. |
|Tartomány| Sztring| Igen|Az ügyfél tartományának neve, például contoso.onmicrosoft.com.|
|organizationRegistrationNumber|    sztring|Igen|     Az ügyfél szervezetének regisztrációs száma (más néven az INN száma bizonyos országokban). Csak a következő országokban található ügyfél vállalata/szervezete számára szükséges. Örményország (AM), Azerbajdzsán (AZ), Fehéroroszország (BY), Magyarország (HU), Kazahsztán (KZ), Kirgizisztán (KG), Moldova (MD), Oroszország (RU), Tádzsikisztán (TJ), Üzbegisztán (UZ), Ukrajna (UA). Az ügyfél más országokban található vállalata/szervezete számára nem adható meg.|



#### <a name="billing-profile"></a>Számlázási profil

Ez a táblázat az új ügyfelek létrehozásához szükséges [CustomerBillingProfile](customer-resources.md#customerbillingprofile) -erőforrás minimálisan szükséges mezőit ismerteti.

| Név             | Típus                                     | Kötelező | Leírás                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-mail            | sztring                                   | Igen      | Az ügyfél e-mail-címe.                                                                                                                                                                                   |
| kulturális környezet          | sztring                                   | Igen      | Az előnyben részesített kulturális környezet a kommunikációhoz és a pénznemhez, mint például az "en-US". Lásd: a [partneri központ által támogatott nyelvek és területi beállítások](partner-center-supported-languages-and-locales.md) a támogatott kulturális környezetekhez. |
| language         | sztring                                   | Igen      | Az alapértelmezett nyelv. Két karakterből álló nyelvi kód (például `en` vagy `fr` ) támogatott.                                                                                                                                |
| cég \_ neve    | sztring                                   | Igen      | A regisztrált vállalat/szervezet neve.                                                                                                                                                                       |
| alapértelmezett \_ címe | [Cím](utility-resources.md#address) | Igen      | Az ügyfél vállalatának/szervezetének regisztrált címe. A hosszra vonatkozó korlátozásokkal kapcsolatos információkért tekintse meg a [címe](utility-resources.md#address) erőforrását.                                             |

#### <a name="company-profile"></a>Vállalati profil

Ez a táblázat az új ügyfelek létrehozásához szükséges [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) -erőforrás minimálisan szükséges mezőit ismerteti.

| Név   | Típus   | Kötelező | Leírás                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| domain | sztring | Igen     | Az ügyfél tartományának neve, például contoso.onmicrosoft.com. |
| organizationRegistrationNumber | sztring | Feltételtől függ | Az ügyfél szervezetének regisztrációs száma (más néven az egyes országokban található INN-szám). <br/><br/>A mező kitöltése csak akkor szükséges, ha az ügyfél vállalata/szervezete a következő országokban található: <br/><br/>-Örményország (AM) <br/>-Azerbajdzsán (AZ)<br/>– Fehéroroszország (BY)<br/>– Magyarország (HU)<br/>-Kazahsztán (KZ)<br/>-Kirgizisztán (KG)<br/>-Moldova (MD)<br/>– Oroszország (RU)<br/>– Tádzsikisztán (TJ)<br/>-Üzbegisztán (UZ)<br/>– Ukrajna (UA)<br/><br/>Erre a mezőre nincs szükség, ha az ügyfél vállalata/szervezete más országokban található, az itt láthatónál tovább.  |

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 823
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": null,
    "CommerceId": null,
    "CompanyProfile": {
        "TenantId": null,
        "Domain": "WingtipToys678152504.onmicrosoft.com",
        "CompanyName": null,
        "Attributes": {
            "ObjectType": "CustomerCompanyProfile"
        }
    },
    "BillingProfile": {
        "Id": null,
        "FirstName": null,
        "LastName": null,
        "Email": "Gena@wingtiptoys.com",
        "Culture": "EN-US",
        "Language": "En",
        "CompanyName": "Wingtip Toys678152504",
        "DefaultAddress": {
            "Country": "US",
            "Region": null,
            "City": "Redmond",
            "State": "WA",
            "AddressLine1": "One Microsoft Way",
            "AddressLine2": null,
            "PostalCode": "98052",
            "FirstName": "Gena",
            "LastName": "Soto",
            "PhoneNumber": "4255550101"
        },
        "Attributes": {
            "ObjectType": "CustomerBillingProfile"
        }
    },
    "RelationshipToPartner": "none",
    "AllowDelegatedAccess": null,
    "UserCredentials": null,
    "CustomDomains": null,
    "AssociatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "Attributes": {
        "ObjectType": "Customer"
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz az új ügyfélhez tartozó [ügyfél](customer-resources.md#customer) -erőforrást tartalmaz.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

A válaszok olyan HTTP-állapotkódot mutatnak be, amely sikeres vagy sikertelen, valamint további hibakeresési információkat jelez. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 201 Created
Content-Length: 1085
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CV: Yy/YaA0gYEmfQyR/.0
MS-ServerId: 030020525
Date: Tue, 06 Jun 2017 23:11:40 GMT

{
    "id": "626099fe-17af-4756-9fd0-6a73b7127859",
    "commerceId": "626099fe-17af-4756-9fd0-6a73b7127859",
    "companyProfile": {
        "tenantId": "626099fe-17af-4756-9fd0-6a73b7127859",
        "domain": "WingtipToys678152504.onmicrosoft.com",
        "companyName": "Wingtip Toys678152504",
        "links": {
            "self": {
                "uri": "/customers/626099fe-17af-4756-9fd0-6a73b7127859/profiles/company",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "7079246e-7b62-56ef-7cbd-a819514b54b5",
        "email": "Gena@wingtiptoys.com",
        "culture": "en-US",
        "language": "En",
        "companyName": "Wingtip Toys678152504",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Gena",
            "lastName": "Soto",
            "phoneNumber": "4255550101"
        },
        "attributes": {
            "etag": "-8799889149591823008",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "reseller",
    "allowDelegatedAccess": true,
    "userCredentials": {
        "userName": "admin",
        "password": "0Krha*Io"
    },
    "associatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "attributes": {
        "objectType": "Customer"
    }
}
```