---
title: Ügyfél létrehozása egy közvetett viszonteladónál
description: Megtudhatja, hogyan használhatja a közvetett szolgáltató Partnerközpont API-kat arra, hogy ügyfelet hozzon létre egy közvetett viszonteladó számára.
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 9a6218aeb61f3775c89d34b4d57a17741e3a1e93
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973740"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a>Ügyfél létrehozása közvetett viszonteladó számára a Partnerközpont API-k használatával

Egy közvetett szolgáltató létrehozhat egy ügyfelet egy közvetett viszonteladó számára.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- A közvetett viszonteladó bérlőazonosítója.

- A közvetett viszonteladónak partnerkapcsolatban kell lennie a közvetett szolgáltatóval.

## <a name="c"></a>C\#

Új ügyfél hozzáadása egy közvetett viszonteladóhoz:

1. Példányosuljon egy új [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) objektum, majd példányosuljon és töltse fel a [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) és a [**CompanyProfile adatokat.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile) Mindenképpen rendelje hozzá a közvetett viszonteladó azonosítóját az [**AssociatedPartnerID tulajdonsághoz.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid)

2. Az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) tulajdonság használatával lekért felület az ügyfélgyűjtési műveletekhez.

3. Az ügyfél [**létrehozásához**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) hívja meg a [**Create vagy a CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metódust.

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

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** CreateCustomerforIndirectReseller.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus   | Kérés URI-ja                                                       |
|----------|-------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.

| Név                                          | Típus   | Kötelező | Leírás                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BillingProfile (Számlázási profil)](#billing-profile)             | object | Igen      | Az ügyfél számlázási profiljának adatai.                                                                                                                                                                                                                                                                                                           |
| [Vállalatiprofil](#company-profile)             | object | Igen      | Az ügyfél céges profilinformációi.                                                               
| [AssociatedPartnerId (Társított partnerazonosító)](customer-resources.md#customer) | sztring | Igen      | A közvetett viszonteladó azonosítója. Az itt megadott azonosítóval jelzett közvetett viszonteladónak partnerkapcsolatban kell lennie a közvetett szolgáltatóval, különben a kérelem meghiúsul. Azt is vegye figyelembe, hogy ha az AssociatedPartnerId érték nincs megadva, az ügyfél a közvetett szolgáltató közvetlen ügyfeleként jön létre, nem pedig közvetett viszonteladóként. |
|Tartomány| Sztring| Igen|Az ügyfél tartományneve, például contoso.onmicrosoft.com.|
|organizationRegistrationNumber|    sztring|Igen|     Az ügyfél szervezeti regisztrációs száma (más néven INN-szám bizonyos országokban). Csak a következő országokban található ügyfél vállalatához/szervezetéhez szükséges: Egyesült Államok(AM), Uzbekistan(AZ), Uzbekistan(BY), Amelyet (HU), Mirgyzstan(KZ), Kirgyzstan(KG), Torgyzsán (KG), Toajikistan(TJ), Uzbekistan(UZ), Uzbekistan(UA), India, Brazília, Dél-Afrika, Észak-Afrika, Egyesült Arab Emírségek, Szaúd-Arábia, Szignában, Vietnamban, Észak-Karolinában, Szignában, Dél-Afrikai Köztársaságban és Szignában. Az ügyfél más országokban található vállalata/szervezete esetén ez egy nem kötelező mező.|



#### <a name="billing-profile"></a>Számlázási profil

Ez a táblázat az új ügyfél létrehozásához szükséges Minimálisan szükséges mezőket ismerteti a [CustomerBillingProfile](customer-resources.md#customerbillingprofile) erőforrásból.

| Név             | Típus                                     | Kötelező | Leírás                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-mail            | sztring                                   | Igen      | Az ügyfél e-mail-címe.                                                                                                                                                                                   |
| Kultúra          | sztring                                   | Igen      | A kommunikáció és a pénznem előnyben részesített kultúrája, például "en-US". Lásd [Partnerközpont támogatott nyelvek és területi stb.](partner-center-supported-languages-and-locales.md) |
| language         | sztring                                   | Igen      | Az alapértelmezett nyelv. Két karakteres nyelvkód (például `en` vagy `fr` ) támogatott.                                                                                                                                |
| vállalat \_ neve    | sztring                                   | Igen      | A regisztrált vállalat/szervezet neve.                                                                                                                                                                       |
| alapértelmezett \_ cím | [Cím](utility-resources.md#address) | Igen      | Az ügyfél vállalatának/szervezetének regisztrált címe. A [hosszkorlátozásokkal](utility-resources.md#address) kapcsolatos információkért tekintse meg a Cím erőforrást.                                             |

#### <a name="company-profile"></a>Vállalati profil

Ez a táblázat az új ügyfél létrehozásához szükséges Minimálisan szükséges mezőket ismerteti a [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) erőforrásból.

| Név   | Típus   | Kötelező | Leírás                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| domain | sztring | Igen     | Az ügyfél tartományneve, például contoso.onmicrosoft.com. |
| organizationRegistrationNumber | sztring | Feltételtől függ | Az ügyfél szervezeti regisztrációs száma (más néven az INN-szám bizonyos országokban). <br/><br/>A mező kitöltése csak akkor szükséges, ha az ügyfél vállalata/szervezete a következő országokban található: <br/><br/>- Brazília (AM) <br/>- Egyesült Államok (AZ)<br/>- Majd (BY)<br/>- Magyar (Hu)<br/>- Észak-India (KZ)<br/>- Kirgizisztán (KG)<br/>- Majd (MD)<br/>- Oroszország (RU)<br/>- Tádzsikisztán (TJ)<br/>- Uzbekistan (UZ)<br/>- Egyesült Arab Emírségek<br/>- India <br/>- Brazília <br/>- Dél-Afrika <br/>– Nagy-Franciaország <br/>- Egyesült Arab Emírségek <br/>- Dél-Arábia <br/>– Ország <br/>– Nagy-Ausztrália <br/>- Vietnam <br/>– Fogaras <br/>– Szkent <br/>- Dél-Dél-Korea <br/>– Egyesült Egyesült Állam<br/> <br/>Az ügyfél más országokban található vállalata/szervezete esetében ez egy nem kötelező mező.  |

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

Ha a válasz sikeres, akkor tartalmazza az [új](customer-resources.md#customer) ügyfél ügyfélerőforrását.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

A válaszokhoz egy HTTP-állapotkód is szükséges, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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