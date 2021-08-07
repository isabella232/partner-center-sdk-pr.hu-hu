---
title: Ügyfél létrehozása
description: Megtudhatja, Felhőszolgáltató (CSP-) partnerek hogyan használhatnak Partnerközpont API-kat egy új ügyfél létrehozásához. A cikk ismerteti az előfeltételeket, és hogy mi történik még.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 49df47441276c7e79074e1bf7f8d50cd72054b42acd93938de088046b68b6d98
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991769"
---
# <a name="create-a-customer-using-partner-center-apis"></a>Ügyfél létrehozása Partnerközpont API-k használatával

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont a Microsoft Cloud for US Government

Ez a cikk bemutatja, hogyan hozhat létre új ügyfelet.

> [!IMPORTANT]
> Ha Ön közvetett szolgáltató, és egy közvetett viszonteladóhoz szeretne ügyfelet létrehozni, tekintse meg az Ügyfél létrehozása közvetett [viszonteladó számára.](create-a-customer-for-an-indirect-reseller.md)

Felhőszolgáltatói (CSP-) partnerként az ügyfél létrehozásakor az ügyfél nevében is lekényhet rendeléseket. Amikor létrehoz egy ügyfelet, a következőt is létrehozza:

- Egy Azure Active Directory (AD) bérlőobjektum az ügyfél számára.

- A viszonteladó és az ügyfél közötti kapcsolat, delegált rendszergazdai jogosultságokkal.

- Egy felhasználónév és egy jelszó, amely rendszergazdaként jelentkezik be az ügyfélhez.

Az ügyfél létrehozása után mindenképpen mentse az ügyfél-azonosítót és az Azure AD adatait, hogy a Partnerközpont SDK használva (például fiókkezelés).

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

> [!IMPORTANT]
> Ügyfélbérlő létrehozásához érvényes fizikai címet kell adnia a létrehozási folyamat során. A címek ellenőrzéséhez kövesse a Cím ellenőrzése [forgatókönyvben leírt](validate-an-address.md) lépéseket. Ha érvénytelen címmel hoz létre ügyfelet a sandbox környezetben, nem tudja törölni az ügyfélbérlőt.

## <a name="c"></a>C\#

Ügyfél hozzáadása:

1. Új Customer objektum [**példányának**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) létrehozása. Mindenképpen töltse ki a [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) és [**a CompanyProfile adatokat.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)

2. Adja hozzá az új ügyfelet az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményhez a [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) vagy [**CreateAsync hívásával.**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)

### <a name="c-example"></a>C \# példa

```csharp
// IAggregatePartner partnerOperations;

var partnerOperations = this.Context.UserPartnerOperations;

var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "SampleApplication{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix),
        //// OrganizationRegistrationNumber = "123456" // Please add if in specific country that requires
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "someone@example.com",
        Language = "En",
        CompanyName = "Some Company" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Tania",
            MiddleName = "MiddleName",
            LastName = "Carr",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = ""
        }
    }
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** Partnerközpont SDK Samples **Osztály:** CreateCustomer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Új ügyfél létrehozása:

1. Hozzon létre egy új példányt a **CustomerBillingProfile** és **a CustomerCompanyProfile objektumból.** Mindenképpen töltse ki a kötelező mezőket.

2. Hozza létre az ügyfelet az **IAggregatePartner.getCustomers().create függvény hívásával.**

### <a name="java-example"></a>Java-példa

```java
// IAggregatePartner partnerOperations;

Address address = new Address();

address.setFirstName( "Gena" );
address.setLastName( "Soto" );
address.setAddressLine1( "One Microsoft Way" );
address.setCity( "Redmond" );
address.setState( "WA" );
address.setCountry( "US" );
address.setPostalCode( "98052" );
address.setPhoneNumber( "4255550101" );

CustomerBillingProfile billingProfile = new CustomerBillingProfile();

billingProfile.setCulture( "en-US" );
billingProfile.setEmail( "gena@wingtiptoys.com" );
billingProfile.setLanguage( "en" );
billingProfile.setCompanyName( "Wingtip Toys" + new Random().nextInt() );
billingProfile.setDefaultAddress( address );

CustomerCompanyProfile companyProfile = new CustomerCompanyProfile();

companyProfile.setDomain( "WingtipToys" + Math.abs( new Random().nextInt() ) + ".onmicrosoft.com" );

Customer customerToCreate = new Customer();

customerToCreate.setBillingProfile( billingProfile );
customerToCreate.setCompanyProfile( companyProfile );

Customer newCustomer = partnerOperations.getCustomers().create( customerToCreate );
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Ügyfél létrehozásához hajtsa végre a [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) parancsot.

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                       |
|----------|-------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

- Ez az API idempotent (nem ad vissza más eredményt, ha többször is meghívja).

- Szükség van egy kérésazonosítóra és egy korrelációs azonosítóra.

- További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.

| Név                              | Típus   | Description                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile (Számlázási profil)](#billing-profile) | object | Az ügyfél számlázási profiljának adatai. |
| [Vállalatiprofil](#company-profile) | object | Az ügyfél vállalati profilinformációi. |

#### <a name="billing-profile"></a>Számlázási profil

Ez a táblázat az új ügyfél létrehozásához szükséges minimálisan szükséges mezőket ismerteti a [CustomerBillingProfile](customer-resources.md#customerbillingprofile) erőforrásból.

| Név             | Típus                                     | Description                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-mail            | sztring                                   | Az ügyfél e-mail-címe.                                                                                                                                                                                   |
| Kultúra          | sztring                                   | A kommunikáció és a pénznem előnyben részesített kultúrája, például "en-US". A [támogatott Partnerközpont nyelvek és területi](partner-center-supported-languages-and-locales.md) területi stb. |
| language         | sztring                                   | Az alapértelmezett nyelv. Két karakteres nyelvkód (például `en` vagy `fr` ) támogatott.                                                                                                                                |
| vállalat \_ neve    | sztring                                   | A regisztrált vállalat/szervezet neve.                                                                                                                                                                       |
| alapértelmezett \_ cím | [Cím](utility-resources.md#address) | Az ügyfél vállalatának/szervezetének regisztrált címe. A [hosszkorlátokkal](utility-resources.md#address) kapcsolatos információkért tekintse meg a Cím erőforrást.                                             |

#### <a name="company-profile"></a>Vállalati profil

Ez a táblázat az új ügyfél létrehozásához szükséges minimálisan szükséges mezőket ismerteti a [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) erőforrásból.

| Név   | Típus   | Description                                                  |
|--------|--------|--------------------------------------------------------------|
| domain | sztring | Az ügyfél tartományneve, például contoso.onmicrosoft.com. |
|organizationRegistrationNumber|Sztring|Az ügyfél szervezeti regisztrációs száma (más néven INN-szám bizonyos országokban). Csak a következő országokban található ügyfél cégéhez/szervezetéhez szükséges: Egyesült Államok( Am), Uzbekistan(UZ), Amelyet(BY), Fogja (KZ), Kyrgyzstan(KG), Fog(MD), Oroszország(RU), Tajikistan(TJ), Uzbekistan(UZ), Valamint(UA), Brazília(BR), India, Dél-Afrika, Észak-Afrika, Egyesült Arab Emírségek, Délkelet-Korea, Észak-Karolina, Vietnam, Észak-Karolina, Észak-Afrika, Dél-Afrikai Köztársaság és Észak-Korea. Az ügyfél más országokban található vállalata/szervezete esetében ez egy nem kötelező mező.|

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "CompanyProfile": {
        "Domain": "xyz.ccsctp.net",
    },
    "BillingProfile": {
        "Culture": "EN-US",
        "Email": "test@outlook.com",
        "Language": "en",
        "CompanyName": "test company",
        "DefaultAddress": {
            "FirstName": "Test",
            "LastName": "Test",
            "AddressLine1": "One Microsoft Way",
            "City": "Redmond",
            "State": "WA",
            "PostalCode": "98052",
            "Country": "US",
        }
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha ez az API sikeres, egy [Ügyfél erőforrást](customer-resources.md#customer) ad vissza az új ügyfélnek. Mentse az ügyfél-azonosítót és az Azure AD adatait a Partnerközpont SDK. Szüksége lesz rájuk például a fiókkezeléshez.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

A válaszokhoz egy HTTP-állapotkód is szükséges, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CV: ObwhuhD2tUKJoM+Z.0
MS-ServerId: 202010223
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "dfd8cc0a-c592-468c-8461-869a38d24738",
    "commerceId": "0a4ce58a-6f96-4273-8035-d9c7d31b9ba4",
    "companyProfile": {
        "tenantId": "dfd8cc0a-c592-468c-8461-869a38d24738",
        "domain": "xyz.ccsctp.net",
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "d17c0275-da92-5c33-9032-782ef1d0b69b",
        "email": "test@outlook.com",
        "culture": "en-US",
        "language": "en",
        "companyName": "test company",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Test",
            "lastName": "Test",
            "phoneNumber": ""
        },
        "attributes": {
            "etag": "5920358838484612121",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "none",
    "userCredentials": {
        "userName": "admin",
        "password": "=;;n.=s9Z"
    },
    "attributes": {
        "objectType": "Customer"
    }
}
```
