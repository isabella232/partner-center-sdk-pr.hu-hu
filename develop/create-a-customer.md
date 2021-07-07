---
title: Ügyfél létrehozása
description: Megtudhatja, Felhőszolgáltató (CSP)-partnerek hogyan használhatnak Partnerközpont API-kat új ügyfelek létrehozásához. A cikk ismerteti az előfeltételeket, és hogy mi történik még.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 6232ca77d057f2f5168b73d81ec551669d540246
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973723"
---
# <a name="create-a-customer-using-partner-center-apis"></a><span data-ttu-id="ec26d-104">Ügyfél létrehozása Partnerközpont API-k használatával</span><span class="sxs-lookup"><span data-stu-id="ec26d-104">Create a customer using Partner Center APIs</span></span>

<span data-ttu-id="ec26d-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ec26d-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ec26d-106">Ez a cikk bemutatja, hogyan hozhat létre új ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="ec26d-106">This article explains how to create a new customer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec26d-107">Ha Ön közvetett szolgáltató, és egy közvetett viszonteladóhoz szeretne ügyfelet létrehozni, tekintse meg az Ügyfél létrehozása közvetett [viszonteladóhoz(](create-a-customer-for-an-indirect-reseller.md))</span><span class="sxs-lookup"><span data-stu-id="ec26d-107">If you are an indirect provider and you want to create a customer for an indirect reseller, please see [Create a customer for an indirect reseller](create-a-customer-for-an-indirect-reseller.md).</span></span>

<span data-ttu-id="ec26d-108">Felhőszolgáltatói (CSP-) partnerként az ügyfél létrehozásakor az ügyfél nevében is ki lehet rendelni a rendeléseket.</span><span class="sxs-lookup"><span data-stu-id="ec26d-108">As a cloud solution provider (CSP) partner, when you create a customer you can place orders on behalf of the customer.</span></span> <span data-ttu-id="ec26d-109">Amikor létrehoz egy ügyfelet, a következőt is létrehozza:</span><span class="sxs-lookup"><span data-stu-id="ec26d-109">When you create a customer, you also create:</span></span>

- <span data-ttu-id="ec26d-110">Egy Azure Active Directory (AD) bérlőobjektuma.</span><span class="sxs-lookup"><span data-stu-id="ec26d-110">An Azure Active Directory (AD) tenant object for the customer.</span></span>

- <span data-ttu-id="ec26d-111">A viszonteladó és az ügyfél közötti kapcsolat, delegált rendszergazdai jogosultságokkal.</span><span class="sxs-lookup"><span data-stu-id="ec26d-111">A relationship between the reseller and customer, used for delegated admin privileges.</span></span>

- <span data-ttu-id="ec26d-112">Egy felhasználónév és egy jelszó, amely rendszergazdaként jelentkezik be az ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="ec26d-112">A user name and password to sign in as an admin for the customer.</span></span>

<span data-ttu-id="ec26d-113">Miután az ügyfél létrejött, mentse az ügyfél-azonosítót és az Azure AD adatait, hogy a Partnerközpont SDK használva (például fiókkezelés).</span><span class="sxs-lookup"><span data-stu-id="ec26d-113">Once the customer is created, be sure to save the customer ID and Azure AD details for future use with the Partner Center SDK (for example, account management).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec26d-114">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="ec26d-114">Prerequisites</span></span>

- <span data-ttu-id="ec26d-115">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ec26d-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ec26d-116">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="ec26d-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec26d-117">Ügyfélbérlő létrehozásához érvényes fizikai címet kell adnia a létrehozási folyamat során.</span><span class="sxs-lookup"><span data-stu-id="ec26d-117">To create a customer tenant you must provide a valid physical address during the creation process.</span></span> <span data-ttu-id="ec26d-118">A címeket a Cím ellenőrzése forgatókönyv lépéseit [követve ellenőrizheti.](validate-an-address.md)</span><span class="sxs-lookup"><span data-stu-id="ec26d-118">An address can be validated by following the steps outlined in the [Validate an address](validate-an-address.md) scenario.</span></span> <span data-ttu-id="ec26d-119">Ha érvénytelen címmel hoz létre ügyfelet a sandbox környezetben, nem tudja törölni az adott ügyfélbérlőt.</span><span class="sxs-lookup"><span data-stu-id="ec26d-119">If you create a customer using an invalid address in the sandbox environment, you will not be able to delete that customer tenant.</span></span>

## <a name="c"></a><span data-ttu-id="ec26d-120">C\#</span><span class="sxs-lookup"><span data-stu-id="ec26d-120">C\#</span></span>

<span data-ttu-id="ec26d-121">Ügyfél hozzáadása:</span><span class="sxs-lookup"><span data-stu-id="ec26d-121">To add a customer:</span></span>

1. <span data-ttu-id="ec26d-122">Új Customer objektum [**példányos**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) létrehozása.</span><span class="sxs-lookup"><span data-stu-id="ec26d-122">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object.</span></span> <span data-ttu-id="ec26d-123">Mindenképpen töltse ki a [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) és [**a CompanyProfile adatokat.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)</span><span class="sxs-lookup"><span data-stu-id="ec26d-123">Be sure to fill in the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span>

2. <span data-ttu-id="ec26d-124">Adja hozzá az új ügyfelet az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményhez a [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) vagy [**CreateAsync hívásával.**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)</span><span class="sxs-lookup"><span data-stu-id="ec26d-124">Add the new customer to your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection by calling [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span></span>

### <a name="c-example"></a><span data-ttu-id="ec26d-125">C \# példa</span><span class="sxs-lookup"><span data-stu-id="ec26d-125">C\# example</span></span>

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

<span data-ttu-id="ec26d-126">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ec26d-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ec26d-127">**Project**: Partnerközpont SDK **Osztály:** CreateCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="ec26d-127">**Project**: Partner Center SDK Samples **Class**: CreateCustomer.cs</span></span>

## <a name="java"></a><span data-ttu-id="ec26d-128">Java</span><span class="sxs-lookup"><span data-stu-id="ec26d-128">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="ec26d-129">Új ügyfél létrehozása:</span><span class="sxs-lookup"><span data-stu-id="ec26d-129">To create a new customer:</span></span>

1. <span data-ttu-id="ec26d-130">Hozzon létre egy új példányt a **CustomerBillingProfile** és **a CustomerCompanyProfile objektumból.**</span><span class="sxs-lookup"><span data-stu-id="ec26d-130">Create a new instance of the **CustomerBillingProfile** and the **CustomerCompanyProfile** objects.</span></span> <span data-ttu-id="ec26d-131">Mindenképpen töltse ki a kötelező mezőket.</span><span class="sxs-lookup"><span data-stu-id="ec26d-131">Be sure to populate the required fields.</span></span>

2. <span data-ttu-id="ec26d-132">Hozza létre az ügyfelet az **IAggregatePartner.getCustomers().create függvény hívásával.**</span><span class="sxs-lookup"><span data-stu-id="ec26d-132">Create the customer by calling the **IAggregatePartner.getCustomers().create** function.</span></span>

### <a name="java-example"></a><span data-ttu-id="ec26d-133">Java-példa</span><span class="sxs-lookup"><span data-stu-id="ec26d-133">Java example</span></span>

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

## <a name="powershell"></a><span data-ttu-id="ec26d-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec26d-134">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="ec26d-135">Ügyfél létrehozásához hajtsa végre a [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) parancsot.</span><span class="sxs-lookup"><span data-stu-id="ec26d-135">To create a customer, execute the [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) command.</span></span>

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a><span data-ttu-id="ec26d-136">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="ec26d-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ec26d-137">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="ec26d-137">Request syntax</span></span>

| <span data-ttu-id="ec26d-138">Metódus</span><span class="sxs-lookup"><span data-stu-id="ec26d-138">Method</span></span>   | <span data-ttu-id="ec26d-139">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="ec26d-139">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="ec26d-140">**Post**</span><span class="sxs-lookup"><span data-stu-id="ec26d-140">**POST**</span></span> | <span data-ttu-id="ec26d-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ec26d-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ec26d-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="ec26d-142">Request headers</span></span>

- <span data-ttu-id="ec26d-143">Ez az API idempotent (nem fog más eredményt eredményezni, ha többször is meghívja).</span><span class="sxs-lookup"><span data-stu-id="ec26d-143">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>

- <span data-ttu-id="ec26d-144">Szükség van egy kérésazonosítóra és egy korrelációs azonosítóra.</span><span class="sxs-lookup"><span data-stu-id="ec26d-144">A request ID and correlation ID are required.</span></span>

- <span data-ttu-id="ec26d-145">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ec26d-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ec26d-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="ec26d-146">Request body</span></span>

<span data-ttu-id="ec26d-147">Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="ec26d-147">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="ec26d-148">Név</span><span class="sxs-lookup"><span data-stu-id="ec26d-148">Name</span></span>                              | <span data-ttu-id="ec26d-149">Típus</span><span class="sxs-lookup"><span data-stu-id="ec26d-149">Type</span></span>   | <span data-ttu-id="ec26d-150">Leírás</span><span class="sxs-lookup"><span data-stu-id="ec26d-150">Description</span></span>                                 |
|-----------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="ec26d-151">BillingProfile (Számlázási profil)</span><span class="sxs-lookup"><span data-stu-id="ec26d-151">BillingProfile</span></span>](#billing-profile) | <span data-ttu-id="ec26d-152">object</span><span class="sxs-lookup"><span data-stu-id="ec26d-152">object</span></span> | <span data-ttu-id="ec26d-153">Az ügyfél számlázási profiljának adatai.</span><span class="sxs-lookup"><span data-stu-id="ec26d-153">The customer's billing profile information.</span></span> |
| [<span data-ttu-id="ec26d-154">Vállalatiprofil</span><span class="sxs-lookup"><span data-stu-id="ec26d-154">CompanyProfile</span></span>](#company-profile) | <span data-ttu-id="ec26d-155">object</span><span class="sxs-lookup"><span data-stu-id="ec26d-155">object</span></span> | <span data-ttu-id="ec26d-156">Az ügyfél céges profilinformációi.</span><span class="sxs-lookup"><span data-stu-id="ec26d-156">The customer's company profile information.</span></span> |

#### <a name="billing-profile"></a><span data-ttu-id="ec26d-157">Számlázási profil</span><span class="sxs-lookup"><span data-stu-id="ec26d-157">Billing profile</span></span>

<span data-ttu-id="ec26d-158">Ez a táblázat az új ügyfél létrehozásához szükséges Minimálisan szükséges mezőket ismerteti a [CustomerBillingProfile](customer-resources.md#customerbillingprofile) erőforrásból.</span><span class="sxs-lookup"><span data-stu-id="ec26d-158">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="ec26d-159">Név</span><span class="sxs-lookup"><span data-stu-id="ec26d-159">Name</span></span>             | <span data-ttu-id="ec26d-160">Típus</span><span class="sxs-lookup"><span data-stu-id="ec26d-160">Type</span></span>                                     | <span data-ttu-id="ec26d-161">Leírás</span><span class="sxs-lookup"><span data-stu-id="ec26d-161">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ec26d-162">e-mail</span><span class="sxs-lookup"><span data-stu-id="ec26d-162">email</span></span>            | <span data-ttu-id="ec26d-163">sztring</span><span class="sxs-lookup"><span data-stu-id="ec26d-163">string</span></span>                                   | <span data-ttu-id="ec26d-164">Az ügyfél e-mail-címe.</span><span class="sxs-lookup"><span data-stu-id="ec26d-164">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="ec26d-165">Kultúra</span><span class="sxs-lookup"><span data-stu-id="ec26d-165">culture</span></span>          | <span data-ttu-id="ec26d-166">sztring</span><span class="sxs-lookup"><span data-stu-id="ec26d-166">string</span></span>                                   | <span data-ttu-id="ec26d-167">A kommunikáció és a pénznem előnyben részesített kultúrája, például "en-US".</span><span class="sxs-lookup"><span data-stu-id="ec26d-167">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="ec26d-168">Lásd [Partnerközpont támogatott nyelvek és területi stb.](partner-center-supported-languages-and-locales.md)</span><span class="sxs-lookup"><span data-stu-id="ec26d-168">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="ec26d-169">language</span><span class="sxs-lookup"><span data-stu-id="ec26d-169">language</span></span>         | <span data-ttu-id="ec26d-170">sztring</span><span class="sxs-lookup"><span data-stu-id="ec26d-170">string</span></span>                                   | <span data-ttu-id="ec26d-171">Az alapértelmezett nyelv.</span><span class="sxs-lookup"><span data-stu-id="ec26d-171">The default language.</span></span> <span data-ttu-id="ec26d-172">Két karakteres nyelvkód (például `en` vagy `fr` ) támogatott.</span><span class="sxs-lookup"><span data-stu-id="ec26d-172">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="ec26d-173">vállalat \_ neve</span><span class="sxs-lookup"><span data-stu-id="ec26d-173">company\_name</span></span>    | <span data-ttu-id="ec26d-174">sztring</span><span class="sxs-lookup"><span data-stu-id="ec26d-174">string</span></span>                                   | <span data-ttu-id="ec26d-175">A regisztrált vállalat/szervezet neve.</span><span class="sxs-lookup"><span data-stu-id="ec26d-175">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="ec26d-176">alapértelmezett \_ cím</span><span class="sxs-lookup"><span data-stu-id="ec26d-176">default\_address</span></span> | [<span data-ttu-id="ec26d-177">Cím</span><span class="sxs-lookup"><span data-stu-id="ec26d-177">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="ec26d-178">Az ügyfél vállalatának/szervezetének regisztrált címe.</span><span class="sxs-lookup"><span data-stu-id="ec26d-178">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="ec26d-179">A [hosszkorlátozásokkal](utility-resources.md#address) kapcsolatos információkért tekintse meg a Cím erőforrást.</span><span class="sxs-lookup"><span data-stu-id="ec26d-179">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="ec26d-180">Vállalati profil</span><span class="sxs-lookup"><span data-stu-id="ec26d-180">Company profile</span></span>

<span data-ttu-id="ec26d-181">Ez a táblázat az új ügyfél létrehozásához szükséges Minimálisan szükséges mezőket ismerteti a [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) erőforrásból.</span><span class="sxs-lookup"><span data-stu-id="ec26d-181">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="ec26d-182">Név</span><span class="sxs-lookup"><span data-stu-id="ec26d-182">Name</span></span>   | <span data-ttu-id="ec26d-183">Típus</span><span class="sxs-lookup"><span data-stu-id="ec26d-183">Type</span></span>   | <span data-ttu-id="ec26d-184">Leírás</span><span class="sxs-lookup"><span data-stu-id="ec26d-184">Description</span></span>                                                  |
|--------|--------|--------------------------------------------------------------|
| <span data-ttu-id="ec26d-185">domain</span><span class="sxs-lookup"><span data-stu-id="ec26d-185">domain</span></span> | <span data-ttu-id="ec26d-186">sztring</span><span class="sxs-lookup"><span data-stu-id="ec26d-186">string</span></span> | <span data-ttu-id="ec26d-187">Az ügyfél tartományneve, például contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="ec26d-187">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
|<span data-ttu-id="ec26d-188">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="ec26d-188">organizationRegistrationNumber</span></span>|<span data-ttu-id="ec26d-189">Sztring</span><span class="sxs-lookup"><span data-stu-id="ec26d-189">String</span></span>|<span data-ttu-id="ec26d-190">Az ügyfél szervezeti regisztrációs száma (más néven INN-szám bizonyos országokban).</span><span class="sxs-lookup"><span data-stu-id="ec26d-190">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="ec26d-191">Csak a következő országokban található ügyfél vállalatához/szervezetéhez szükséges: Egyesült Államok(AM), Uzbekistan(AZ), Amelyet(BY), Amelyet (HU), Torgyzstan(KZ), Kyrgyzstan(KG), Torgyzstan(KG), Torgikistan(TJ), Uzbekistan(UZ), Uzbekistan(UZ), Brazília(BR), India, Dél-Afrika, Dél-Afrikai Köztársaság, Egyesült Arab Emírségek, Szaúd-Arábia, Észak-Korea, Vietnam, Észak-Korea, Szignában, Dél-Koreában és Észak-Koreában.</span><span class="sxs-lookup"><span data-stu-id="ec26d-191">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), Brazil(BR), India, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan, and Venezuela.</span></span> <span data-ttu-id="ec26d-192">Az ügyfél más országokban található vállalata/szervezete esetén ez egy nem kötelező mező.</span><span class="sxs-lookup"><span data-stu-id="ec26d-192">For customer’s company/organization located in other countries, this is an optional field.</span></span>|

### <a name="request-example"></a><span data-ttu-id="ec26d-193">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ec26d-193">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="ec26d-194">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="ec26d-194">REST response</span></span>

<span data-ttu-id="ec26d-195">Ha ez a művelet sikeres, ez az API egy [Ügyfél](customer-resources.md#customer) erőforrást ad vissza az új ügyfélnek.</span><span class="sxs-lookup"><span data-stu-id="ec26d-195">If successful, this API returns a [Customer](customer-resources.md#customer) resource for the new customer.</span></span> <span data-ttu-id="ec26d-196">Mentse az ügyfél-azonosítót és az Azure AD adatait a Partnerközpont SDK.</span><span class="sxs-lookup"><span data-stu-id="ec26d-196">Save the customer ID and Azure AD details for future use with the Partner Center SDK.</span></span> <span data-ttu-id="ec26d-197">Szüksége lesz rájuk például a fiókkezeléshez.</span><span class="sxs-lookup"><span data-stu-id="ec26d-197">You will need them for use with account management, for example.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ec26d-198">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="ec26d-198">Response success and error codes</span></span>

<span data-ttu-id="ec26d-199">A válaszokhoz egy HTTP-állapotkód is szükséges, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="ec26d-199">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ec26d-200">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="ec26d-200">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ec26d-201">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ec26d-201">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ec26d-202">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ec26d-202">Response example</span></span>

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
