---
title: Ügyfél létrehozása
description: Megtudhatja, hogyan használhatja a Cloud Solution Provider (CSP) partner a partner Center API-kat új ügyfél létrehozásához. A cikk leírja az előfeltételeket, és hogy mi történik.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 73286e6068663187b973827df1b5b49d44b95532
ms.sourcegitcommit: 204e518e794b6b076a17488ee9ca1aaaa4beaaec
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/01/2021
ms.locfileid: "106103997"
---
# <a name="create-a-customer-using-partner-center-apis"></a><span data-ttu-id="f15fe-104">Ügyfél létrehozása a partner Center API-kkal</span><span class="sxs-lookup"><span data-stu-id="f15fe-104">Create a customer using Partner Center APIs</span></span>

<span data-ttu-id="f15fe-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="f15fe-105">**Applies to:**</span></span>

- <span data-ttu-id="f15fe-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f15fe-106">Partner Center</span></span>
- <span data-ttu-id="f15fe-107">A 21Vianet által üzemeltetett Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f15fe-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f15fe-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f15fe-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f15fe-109">Ez a cikk azt ismerteti, hogyan lehet új ügyfelet létrehozni.</span><span class="sxs-lookup"><span data-stu-id="f15fe-109">This article explains how to create a new customer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f15fe-110">Ha Ön közvetett szolgáltató, és szeretné létrehozni az ügyfelet egy közvetett viszonteladóhoz, tekintse meg az [ügyfél létrehozása közvetett viszonteladóhoz](create-a-customer-for-an-indirect-reseller.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="f15fe-110">If you are an indirect provider and you want to create a customer for an indirect reseller, please see [Create a customer for an indirect reseller](create-a-customer-for-an-indirect-reseller.md).</span></span>

<span data-ttu-id="f15fe-111">Felhőalapú megoldás-szolgáltatói (CSP) partnerként, amikor létrehoz egy ügyfelet, a rendeléseket az ügyfél nevében helyezheti el.</span><span class="sxs-lookup"><span data-stu-id="f15fe-111">As a cloud solution provider (CSP) partner, when you create a customer you can place orders on behalf of the customer.</span></span> <span data-ttu-id="f15fe-112">Amikor létrehoz egy ügyfelet, a következőket is létrehozhatja:</span><span class="sxs-lookup"><span data-stu-id="f15fe-112">When you create a customer, you also create:</span></span>

- <span data-ttu-id="f15fe-113">Az ügyfél Azure Active Directory (AD) bérlői objektuma.</span><span class="sxs-lookup"><span data-stu-id="f15fe-113">An Azure Active Directory (AD) tenant object for the customer.</span></span>

- <span data-ttu-id="f15fe-114">A viszonteladó és az ügyfél közötti kapcsolat, amelyet delegált rendszergazdai jogosultságokkal használtak.</span><span class="sxs-lookup"><span data-stu-id="f15fe-114">A relationship between the reseller and customer, used for delegated admin privileges.</span></span>

- <span data-ttu-id="f15fe-115">Egy Felhasználónév és egy jelszó, amely az ügyfél rendszergazdájaként való bejelentkezéshez szükséges.</span><span class="sxs-lookup"><span data-stu-id="f15fe-115">A user name and password to sign in as an admin for the customer.</span></span>

<span data-ttu-id="f15fe-116">Az ügyfél létrehozása után mindenképp mentse az ügyfél-azonosítót és az Azure AD-adatokat a partner Center SDK-val való jövőbeli használatra (például Fiókkezelés).</span><span class="sxs-lookup"><span data-stu-id="f15fe-116">Once the customer is created, be sure to save the customer ID and Azure AD details for future use with the Partner Center SDK (for example, account management).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f15fe-117">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f15fe-117">Prerequisites</span></span>

- <span data-ttu-id="f15fe-118">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="f15fe-118">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f15fe-119">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="f15fe-119">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f15fe-120">Az ügyfél-bérlő létrehozásához érvényes fizikai címeket kell megadnia a létrehozási folyamat során.</span><span class="sxs-lookup"><span data-stu-id="f15fe-120">To create a customer tenant you must provide a valid physical address during the creation process.</span></span> <span data-ttu-id="f15fe-121">A címek a [címek ellenőrzése](validate-an-address.md) forgatókönyvben ismertetett lépéseket követve ellenőrizhetők.</span><span class="sxs-lookup"><span data-stu-id="f15fe-121">An address can be validated by following the steps outlined in the [Validate an address](validate-an-address.md) scenario.</span></span> <span data-ttu-id="f15fe-122">Ha a sandbox-környezet érvénytelen címe alapján hoz létre egy ügyfelet, nem fogja tudni törölni az ügyfél bérlőjét.</span><span class="sxs-lookup"><span data-stu-id="f15fe-122">If you create a customer using an invalid address in the sandbox environment, you will not be able to delete that customer tenant.</span></span>

## <a name="c"></a><span data-ttu-id="f15fe-123">C\#</span><span class="sxs-lookup"><span data-stu-id="f15fe-123">C\#</span></span>

<span data-ttu-id="f15fe-124">Ügyfél hozzáadása:</span><span class="sxs-lookup"><span data-stu-id="f15fe-124">To add a customer:</span></span>

1. <span data-ttu-id="f15fe-125">Új [**ügyfél**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) -objektum példányának létrehozása.</span><span class="sxs-lookup"><span data-stu-id="f15fe-125">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object.</span></span> <span data-ttu-id="f15fe-126">Ügyeljen arra, hogy kitöltse a [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) és a [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span><span class="sxs-lookup"><span data-stu-id="f15fe-126">Be sure to fill in the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span>

2. <span data-ttu-id="f15fe-127">Adja hozzá az új ügyfelet a [**IAggregatePartner. Customs**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményhez a [**create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)hívásával.</span><span class="sxs-lookup"><span data-stu-id="f15fe-127">Add the new customer to your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection by calling [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span></span>

### <a name="c-example"></a><span data-ttu-id="f15fe-128">C \# példa</span><span class="sxs-lookup"><span data-stu-id="f15fe-128">C\# example</span></span>

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

<span data-ttu-id="f15fe-129">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f15fe-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f15fe-130">**Projekt**: partner Center SDK Samples **osztály**: CreateCustomer. cs</span><span class="sxs-lookup"><span data-stu-id="f15fe-130">**Project**: Partner Center SDK Samples **Class**: CreateCustomer.cs</span></span>

## <a name="java"></a><span data-ttu-id="f15fe-131">Java</span><span class="sxs-lookup"><span data-stu-id="f15fe-131">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="f15fe-132">Új ügyfél létrehozása:</span><span class="sxs-lookup"><span data-stu-id="f15fe-132">To create a new customer:</span></span>

1. <span data-ttu-id="f15fe-133">Hozzon létre egy új példányt a **CustomerBillingProfile** és a **CustomerCompanyProfile** objektumokhoz.</span><span class="sxs-lookup"><span data-stu-id="f15fe-133">Create a new instance of the **CustomerBillingProfile** and the **CustomerCompanyProfile** objects.</span></span> <span data-ttu-id="f15fe-134">Ügyeljen arra, hogy feltöltse a szükséges mezőket.</span><span class="sxs-lookup"><span data-stu-id="f15fe-134">Be sure to populate the required fields.</span></span>

2. <span data-ttu-id="f15fe-135">Hozza létre az ügyfelet a **IAggregatePartner. getCustomers (). Create** függvény meghívásával.</span><span class="sxs-lookup"><span data-stu-id="f15fe-135">Create the customer by calling the **IAggregatePartner.getCustomers().create** function.</span></span>

### <a name="java-example"></a><span data-ttu-id="f15fe-136">Java-példa</span><span class="sxs-lookup"><span data-stu-id="f15fe-136">Java example</span></span>

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

## <a name="powershell"></a><span data-ttu-id="f15fe-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f15fe-137">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="f15fe-138">Ügyfél létrehozásához hajtsa végre a [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) parancsot.</span><span class="sxs-lookup"><span data-stu-id="f15fe-138">To create a customer execute the [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) command.</span></span>

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a><span data-ttu-id="f15fe-139">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="f15fe-139">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f15fe-140">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f15fe-140">Request syntax</span></span>

| <span data-ttu-id="f15fe-141">Metódus</span><span class="sxs-lookup"><span data-stu-id="f15fe-141">Method</span></span>   | <span data-ttu-id="f15fe-142">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f15fe-142">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="f15fe-143">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="f15fe-143">**POST**</span></span> | <span data-ttu-id="f15fe-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers http/1.1</span><span class="sxs-lookup"><span data-stu-id="f15fe-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f15fe-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f15fe-145">Request headers</span></span>

- <span data-ttu-id="f15fe-146">Ez az API idempotens (ez nem eredményez eltérő eredményt, ha többször hívja meg).</span><span class="sxs-lookup"><span data-stu-id="f15fe-146">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>

- <span data-ttu-id="f15fe-147">A kérelem AZONOSÍTÓjának és korrelációs AZONOSÍTÓjának megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="f15fe-147">A request ID and correlation ID are required.</span></span>

- <span data-ttu-id="f15fe-148">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f15fe-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f15fe-149">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f15fe-149">Request body</span></span>

<span data-ttu-id="f15fe-150">Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="f15fe-150">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="f15fe-151">Név</span><span class="sxs-lookup"><span data-stu-id="f15fe-151">Name</span></span>                              | <span data-ttu-id="f15fe-152">Típus</span><span class="sxs-lookup"><span data-stu-id="f15fe-152">Type</span></span>   | <span data-ttu-id="f15fe-153">Leírás</span><span class="sxs-lookup"><span data-stu-id="f15fe-153">Description</span></span>                                 |
|-----------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="f15fe-154">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="f15fe-154">BillingProfile</span></span>](#billing-profile) | <span data-ttu-id="f15fe-155">object</span><span class="sxs-lookup"><span data-stu-id="f15fe-155">object</span></span> | <span data-ttu-id="f15fe-156">Az ügyfél számlázási profiljának adatai.</span><span class="sxs-lookup"><span data-stu-id="f15fe-156">The customer's billing profile information.</span></span> |
| [<span data-ttu-id="f15fe-157">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="f15fe-157">CompanyProfile</span></span>](#company-profile) | <span data-ttu-id="f15fe-158">object</span><span class="sxs-lookup"><span data-stu-id="f15fe-158">object</span></span> | <span data-ttu-id="f15fe-159">Az ügyfél vállalati profiljának adatai.</span><span class="sxs-lookup"><span data-stu-id="f15fe-159">The customer's company profile information.</span></span> |

#### <a name="billing-profile"></a><span data-ttu-id="f15fe-160">Számlázási profil</span><span class="sxs-lookup"><span data-stu-id="f15fe-160">Billing profile</span></span>

<span data-ttu-id="f15fe-161">Ez a táblázat az új ügyfelek létrehozásához szükséges [CustomerBillingProfile](customer-resources.md#customerbillingprofile) -erőforrás minimálisan szükséges mezőit ismerteti.</span><span class="sxs-lookup"><span data-stu-id="f15fe-161">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="f15fe-162">Név</span><span class="sxs-lookup"><span data-stu-id="f15fe-162">Name</span></span>             | <span data-ttu-id="f15fe-163">Típus</span><span class="sxs-lookup"><span data-stu-id="f15fe-163">Type</span></span>                                     | <span data-ttu-id="f15fe-164">Leírás</span><span class="sxs-lookup"><span data-stu-id="f15fe-164">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f15fe-165">e-mail</span><span class="sxs-lookup"><span data-stu-id="f15fe-165">email</span></span>            | <span data-ttu-id="f15fe-166">sztring</span><span class="sxs-lookup"><span data-stu-id="f15fe-166">string</span></span>                                   | <span data-ttu-id="f15fe-167">Az ügyfél e-mail-címe.</span><span class="sxs-lookup"><span data-stu-id="f15fe-167">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="f15fe-168">kulturális környezet</span><span class="sxs-lookup"><span data-stu-id="f15fe-168">culture</span></span>          | <span data-ttu-id="f15fe-169">sztring</span><span class="sxs-lookup"><span data-stu-id="f15fe-169">string</span></span>                                   | <span data-ttu-id="f15fe-170">Az előnyben részesített kulturális környezet a kommunikációhoz és a pénznemhez, mint például az "en-US".</span><span class="sxs-lookup"><span data-stu-id="f15fe-170">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="f15fe-171">Lásd: a [partneri központ által támogatott nyelvek és területi beállítások](partner-center-supported-languages-and-locales.md) a támogatott kulturális környezetekhez.</span><span class="sxs-lookup"><span data-stu-id="f15fe-171">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="f15fe-172">language</span><span class="sxs-lookup"><span data-stu-id="f15fe-172">language</span></span>         | <span data-ttu-id="f15fe-173">sztring</span><span class="sxs-lookup"><span data-stu-id="f15fe-173">string</span></span>                                   | <span data-ttu-id="f15fe-174">Az alapértelmezett nyelv.</span><span class="sxs-lookup"><span data-stu-id="f15fe-174">The default language.</span></span> <span data-ttu-id="f15fe-175">Két karakterből álló nyelvi kód (például `en` vagy `fr` ) támogatott.</span><span class="sxs-lookup"><span data-stu-id="f15fe-175">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="f15fe-176">cég \_ neve</span><span class="sxs-lookup"><span data-stu-id="f15fe-176">company\_name</span></span>    | <span data-ttu-id="f15fe-177">sztring</span><span class="sxs-lookup"><span data-stu-id="f15fe-177">string</span></span>                                   | <span data-ttu-id="f15fe-178">A regisztrált vállalat/szervezet neve.</span><span class="sxs-lookup"><span data-stu-id="f15fe-178">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="f15fe-179">alapértelmezett \_ címe</span><span class="sxs-lookup"><span data-stu-id="f15fe-179">default\_address</span></span> | [<span data-ttu-id="f15fe-180">Cím</span><span class="sxs-lookup"><span data-stu-id="f15fe-180">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="f15fe-181">Az ügyfél vállalatának/szervezetének regisztrált címe.</span><span class="sxs-lookup"><span data-stu-id="f15fe-181">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="f15fe-182">A hosszra vonatkozó korlátozásokkal kapcsolatos információkért tekintse meg a [címe](utility-resources.md#address) erőforrását.</span><span class="sxs-lookup"><span data-stu-id="f15fe-182">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="f15fe-183">Vállalati profil</span><span class="sxs-lookup"><span data-stu-id="f15fe-183">Company profile</span></span>

<span data-ttu-id="f15fe-184">Ez a táblázat az új ügyfelek létrehozásához szükséges [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) -erőforrás minimálisan szükséges mezőit ismerteti.</span><span class="sxs-lookup"><span data-stu-id="f15fe-184">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="f15fe-185">Név</span><span class="sxs-lookup"><span data-stu-id="f15fe-185">Name</span></span>   | <span data-ttu-id="f15fe-186">Típus</span><span class="sxs-lookup"><span data-stu-id="f15fe-186">Type</span></span>   | <span data-ttu-id="f15fe-187">Leírás</span><span class="sxs-lookup"><span data-stu-id="f15fe-187">Description</span></span>                                                  |
|--------|--------|--------------------------------------------------------------|
| <span data-ttu-id="f15fe-188">domain</span><span class="sxs-lookup"><span data-stu-id="f15fe-188">domain</span></span> | <span data-ttu-id="f15fe-189">sztring</span><span class="sxs-lookup"><span data-stu-id="f15fe-189">string</span></span> | <span data-ttu-id="f15fe-190">Az ügyfél tartományának neve, például contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f15fe-190">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
|<span data-ttu-id="f15fe-191">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="f15fe-191">organizationRegistrationNumber</span></span>|<span data-ttu-id="f15fe-192">Sztring</span><span class="sxs-lookup"><span data-stu-id="f15fe-192">String</span></span>|<span data-ttu-id="f15fe-193">Az ügyfél szervezetének regisztrációs száma (más néven az INN száma bizonyos országokban).</span><span class="sxs-lookup"><span data-stu-id="f15fe-193">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="f15fe-194">Csak a következő országokban található ügyfél vállalata vagy szervezete számára szükséges: Örményország (AM), Azerbajdzsán (AZ), Fehéroroszország (BY), Magyarország (HU), Kazahsztán (KZ), Kirgizisztán (KG), Moldova (MD), Oroszország (RU), Tádzsikisztán (TJ), Üzbegisztán (UZ), Ukrajna (UA), India, Brazília, Dél-Afrika, Lengyelország, Egyesült Arab Emírségek, Szaúd-Arábia, Törökország, Thaiföld, Vietnam, Mianmar, Irak, Dél-Szudán és Venezuela.</span><span class="sxs-lookup"><span data-stu-id="f15fe-194">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), India, Brazil, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan and Venezuela.</span></span> <span data-ttu-id="f15fe-195">Az ügyfél más országokban található vállalata/szervezete számára ez egy választható mező.</span><span class="sxs-lookup"><span data-stu-id="f15fe-195">For customer’s company/organization located in other countries this is an optional field.</span></span>|


### <a name="request-example"></a><span data-ttu-id="f15fe-196">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f15fe-196">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f15fe-197">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f15fe-197">REST response</span></span>

<span data-ttu-id="f15fe-198">Ha a művelet sikeres, az API az új ügyfélhez tartozó [ügyfél](customer-resources.md#customer) -erőforrást adja vissza.</span><span class="sxs-lookup"><span data-stu-id="f15fe-198">If successful, this API returns a [Customer](customer-resources.md#customer) resource for the new customer.</span></span> <span data-ttu-id="f15fe-199">Mentse az ügyfél-azonosítót és az Azure AD-adatokat későbbi használatra a partner Center SDK-val.</span><span class="sxs-lookup"><span data-stu-id="f15fe-199">Save the customer ID and Azure AD details for future use with the Partner Center SDK.</span></span> <span data-ttu-id="f15fe-200">Szüksége lesz rájuk a fiókok felügyeletéhez, például:.</span><span class="sxs-lookup"><span data-stu-id="f15fe-200">You will need them for use with account management, for example.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f15fe-201">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f15fe-201">Response success and error codes</span></span>

<span data-ttu-id="f15fe-202">A válaszok olyan HTTP-állapotkódot mutatnak be, amely sikeres vagy sikertelen, valamint további hibakeresési információkat jelez.</span><span class="sxs-lookup"><span data-stu-id="f15fe-202">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f15fe-203">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="f15fe-203">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f15fe-204">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="f15fe-204">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f15fe-205">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f15fe-205">Response example</span></span>

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
