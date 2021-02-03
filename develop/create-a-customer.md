---
title: Ügyfél létrehozása
description: Megtudhatja, hogyan használhatja a Cloud Solution Provider (CSP) partner a partner Center API-kat új ügyfél létrehozásához. A cikk leírja az előfeltételeket, és hogy mi történik.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 3bc8081c682bdf522bcb0ca218f16cafab7b3a99
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/08/2020
ms.locfileid: "97768659"
---
# <a name="create-a-customer-using-partner-center-apis"></a>Ügyfél létrehozása a partner Center API-kkal

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud for US Government Partnerközpontja

Ez a cikk azt ismerteti, hogyan lehet új ügyfelet létrehozni.

> [!IMPORTANT]
> Ha Ön közvetett szolgáltató, és szeretné létrehozni az ügyfelet egy közvetett viszonteladóhoz, tekintse meg az [ügyfél létrehozása közvetett viszonteladóhoz](create-a-customer-for-an-indirect-reseller.md)című témakört.

Felhőalapú megoldás-szolgáltatói (CSP) partnerként, amikor létrehoz egy ügyfelet, a rendeléseket az ügyfél nevében helyezheti el. Amikor létrehoz egy ügyfelet, a következőket is létrehozhatja:

- Az ügyfél Azure Active Directory (AD) bérlői objektuma.

- A viszonteladó és az ügyfél közötti kapcsolat, amelyet delegált rendszergazdai jogosultságokkal használtak.

- Egy Felhasználónév és egy jelszó, amely az ügyfél rendszergazdájaként való bejelentkezéshez szükséges.

Az ügyfél létrehozása után mindenképp mentse az ügyfél-azonosítót és az Azure AD-adatokat a partner Center SDK-val való jövőbeli használatra (például Fiókkezelés).

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

> [!IMPORTANT]
> Az ügyfél-bérlő létrehozásához érvényes fizikai címeket kell megadnia a létrehozási folyamat során. A címek a [címek ellenőrzése](validate-an-address.md) forgatókönyvben ismertetett lépéseket követve ellenőrizhetők. Ha a sandbox-környezet érvénytelen címe alapján hoz létre egy ügyfelet, nem fogja tudni törölni az ügyfél bérlőjét.

## <a name="c"></a>C\#

Ügyfél hozzáadása:

1. Új [**ügyfél**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) -objektum példányának létrehozása. Ügyeljen arra, hogy kitöltse a [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) és a [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).

2. Adja hozzá az új ügyfelet a [**IAggregatePartner. Customs**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményhez a [**create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)hívásával.

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

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: CreateCustomer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Új ügyfél létrehozása:

1. Hozzon létre egy új példányt a **CustomerBillingProfile** és a **CustomerCompanyProfile** objektumokhoz. Ügyeljen arra, hogy feltöltse a szükséges mezőket.

2. Hozza létre az ügyfelet a **IAggregatePartner. getCustomers (). Create** függvény meghívásával.

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

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                       |
|----------|-------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers http/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

- Ez az API idempotens (ez nem eredményez eltérő eredményt, ha többször hívja meg).

- A kérelem AZONOSÍTÓjának és korrelációs AZONOSÍTÓjának megadása kötelező.

- További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.

| Név                              | Típus   | Leírás                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile](#billing-profile) | object | Az ügyfél számlázási profiljának adatai. |
| [CompanyProfile](#company-profile) | object | Az ügyfél vállalati profiljának adatai. |

#### <a name="billing-profile"></a>Számlázási profil

Ez a táblázat az új ügyfelek létrehozásához szükséges [CustomerBillingProfile](customer-resources.md#customerbillingprofile) -erőforrás minimálisan szükséges mezőit ismerteti.

| Név             | Típus                                     | Leírás                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-mail            | sztring                                   | Az ügyfél e-mail-címe.                                                                                                                                                                                   |
| kulturális környezet          | sztring                                   | Az előnyben részesített kulturális környezet a kommunikációhoz és a pénznemhez, mint például az "en-US". Lásd: a [partneri központ által támogatott nyelvek és területi beállítások](partner-center-supported-languages-and-locales.md) a támogatott kulturális környezetekhez. |
| language         | sztring                                   | Az alapértelmezett nyelv. Két karakterből álló nyelvi kód (például `en` vagy `fr` ) támogatott.                                                                                                                                |
| cég \_ neve    | sztring                                   | A regisztrált vállalat/szervezet neve.                                                                                                                                                                       |
| alapértelmezett \_ címe | [Cím](utility-resources.md#address) | Az ügyfél vállalatának/szervezetének regisztrált címe. A hosszra vonatkozó korlátozásokkal kapcsolatos információkért tekintse meg a [címe](utility-resources.md#address) erőforrását.                                             |

#### <a name="company-profile"></a>Vállalati profil

Ez a táblázat az új ügyfelek létrehozásához szükséges [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) -erőforrás minimálisan szükséges mezőit ismerteti.

| Név   | Típus   | Leírás                                                  |
|--------|--------|--------------------------------------------------------------|
| domain | sztring | Az ügyfél tartományának neve, például contoso.onmicrosoft.com. |
|organizationRegistrationNumber|Sztring|Az ügyfél szervezetének regisztrációs száma (más néven az INN száma bizonyos országokban). Csak a következő országokban található ügyfél vállalata/szervezete számára szükséges. Örményország (AM), Azerbajdzsán (AZ), Fehéroroszország (BY), Magyarország (HU), Kazahsztán (KZ), Kirgizisztán (KG), Moldova (MD), Oroszország (RU), Tádzsikisztán (TJ), Üzbegisztán (UZ), Ukrajna (UA). Az ügyfél más országokban található vállalata/szervezete számára nem adható meg.|


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

Ha a művelet sikeres, az API az új ügyfélhez tartozó [ügyfél](customer-resources.md#customer) -erőforrást adja vissza. Mentse az ügyfél-azonosítót és az Azure AD-adatokat későbbi használatra a partner Center SDK-val. Szüksége lesz rájuk a fiókok felügyeletéhez, például:.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

A válaszok olyan HTTP-állapotkódot mutatnak be, amely sikeres vagy sikertelen, valamint további hibakeresési információkat jelez. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

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
