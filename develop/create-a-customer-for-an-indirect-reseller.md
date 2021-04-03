---
title: Ügyfél létrehozása egy közvetett viszonteladónál
description: Megtudhatja, hogyan használhatja a közvetett szolgáltató a partner Center API-kat, hogy ügyfelet hozzon létre egy közvetett viszonteladó számára.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 13cd1b051abb536d397dcd4000228f67fe3206b8
ms.sourcegitcommit: 204e518e794b6b076a17488ee9ca1aaaa4beaaec
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/01/2021
ms.locfileid: "106103946"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="e1cbd-103">Ügyfél létrehozása közvetett viszonteladók számára a partner Center API-k használatával</span><span class="sxs-lookup"><span data-stu-id="e1cbd-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="e1cbd-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="e1cbd-104">**Applies to:**</span></span>

- <span data-ttu-id="e1cbd-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="e1cbd-105">Partner Center</span></span>

<span data-ttu-id="e1cbd-106">A közvetett szolgáltató létrehozhat egy ügyfelet közvetett viszonteladónak.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-106">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1cbd-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="e1cbd-107">Prerequisites</span></span>

- <span data-ttu-id="e1cbd-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e1cbd-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e1cbd-110">A közvetett viszonteladó bérlői azonosítója.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-110">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="e1cbd-111">A közvetett viszonteladónak partneri kapcsolattal kell rendelkeznie a közvetett szolgáltatóval.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-111">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="e1cbd-112">C\#</span><span class="sxs-lookup"><span data-stu-id="e1cbd-112">C\#</span></span>

<span data-ttu-id="e1cbd-113">Új ügyfél hozzáadása közvetett viszonteladóhoz:</span><span class="sxs-lookup"><span data-stu-id="e1cbd-113">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="e1cbd-114">Új [**ügyfél**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) -objektum létrehozása, majd a [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) és a [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)példányának létrehozása és feltöltése.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-114">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="e1cbd-115">Ügyeljen arra, hogy a közvetett viszonteladó AZONOSÍTÓját a [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) tulajdonsághoz rendelje.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-115">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="e1cbd-116">A [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) tulajdonsággal szerezzen be egy felületet az ügyfél-gyűjtési műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-116">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="e1cbd-117">A [**create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metódus meghívásával hozza létre az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-117">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="e1cbd-118">C \# példa</span><span class="sxs-lookup"><span data-stu-id="e1cbd-118">C\# example</span></span>

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

<span data-ttu-id="e1cbd-119">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e1cbd-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e1cbd-120">**Projekt**: partner Center SDK Samples **osztály**: CreateCustomerforIndirectReseller. cs</span><span class="sxs-lookup"><span data-stu-id="e1cbd-120">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e1cbd-121">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="e1cbd-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e1cbd-122">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="e1cbd-122">Request syntax</span></span>

| <span data-ttu-id="e1cbd-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="e1cbd-123">Method</span></span>   | <span data-ttu-id="e1cbd-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="e1cbd-124">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="e1cbd-125">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="e1cbd-125">**POST**</span></span> | <span data-ttu-id="e1cbd-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers http/1.1</span><span class="sxs-lookup"><span data-stu-id="e1cbd-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e1cbd-127">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="e1cbd-127">Request headers</span></span>

<span data-ttu-id="e1cbd-128">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e1cbd-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e1cbd-129">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="e1cbd-129">Request body</span></span>

<span data-ttu-id="e1cbd-130">Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-130">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="e1cbd-131">Név</span><span class="sxs-lookup"><span data-stu-id="e1cbd-131">Name</span></span>                                          | <span data-ttu-id="e1cbd-132">Típus</span><span class="sxs-lookup"><span data-stu-id="e1cbd-132">Type</span></span>   | <span data-ttu-id="e1cbd-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e1cbd-133">Required</span></span> | <span data-ttu-id="e1cbd-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="e1cbd-134">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="e1cbd-135">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="e1cbd-135">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="e1cbd-136">object</span><span class="sxs-lookup"><span data-stu-id="e1cbd-136">object</span></span> | <span data-ttu-id="e1cbd-137">Yes</span><span class="sxs-lookup"><span data-stu-id="e1cbd-137">Yes</span></span>      | <span data-ttu-id="e1cbd-138">Az ügyfél számlázási profiljának adatai.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-138">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="e1cbd-139">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="e1cbd-139">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="e1cbd-140">object</span><span class="sxs-lookup"><span data-stu-id="e1cbd-140">object</span></span> | <span data-ttu-id="e1cbd-141">Yes</span><span class="sxs-lookup"><span data-stu-id="e1cbd-141">Yes</span></span>      | <span data-ttu-id="e1cbd-142">Az ügyfél vállalati profiljának adatai.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-142">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="e1cbd-143">AssociatedPartnerId</span><span class="sxs-lookup"><span data-stu-id="e1cbd-143">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="e1cbd-144">sztring</span><span class="sxs-lookup"><span data-stu-id="e1cbd-144">string</span></span> | <span data-ttu-id="e1cbd-145">Yes</span><span class="sxs-lookup"><span data-stu-id="e1cbd-145">Yes</span></span>      | <span data-ttu-id="e1cbd-146">A közvetett viszonteladó azonosítója.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-146">The indirect reseller ID.</span></span> <span data-ttu-id="e1cbd-147">Az itt megadott azonosító által jelzett közvetett viszonteladónak partneri kapcsolattal kell rendelkeznie a közvetett szolgáltatóval, vagy a kérés sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-147">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="e1cbd-148">Azt is vegye figyelembe, hogy ha a AssociatedPartnerId érték nincs megadva, az ügyfél a közvetett szolgáltató közvetlen ügyfeleként jön létre a közvetett viszonteladó helyett.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-148">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="e1cbd-149">Tartomány</span><span class="sxs-lookup"><span data-stu-id="e1cbd-149">Domain</span></span>| <span data-ttu-id="e1cbd-150">Sztring</span><span class="sxs-lookup"><span data-stu-id="e1cbd-150">String</span></span>| <span data-ttu-id="e1cbd-151">Yes</span><span class="sxs-lookup"><span data-stu-id="e1cbd-151">Yes</span></span>|<span data-ttu-id="e1cbd-152">Az ügyfél tartományának neve, például contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-152">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="e1cbd-153">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="e1cbd-153">organizationRegistrationNumber</span></span>|    <span data-ttu-id="e1cbd-154">sztring</span><span class="sxs-lookup"><span data-stu-id="e1cbd-154">string</span></span>|<span data-ttu-id="e1cbd-155">Yes</span><span class="sxs-lookup"><span data-stu-id="e1cbd-155">Yes</span></span>|     <span data-ttu-id="e1cbd-156">Az ügyfél szervezetének regisztrációs száma (más néven az INN száma bizonyos országokban).</span><span class="sxs-lookup"><span data-stu-id="e1cbd-156">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="e1cbd-157">Csak a következő országokban található ügyfél vállalata vagy szervezete számára szükséges: Örményország (AM), Azerbajdzsán (AZ), Fehéroroszország (BY), Magyarország (HU), Kazahsztán (KZ), Kirgizisztán (KG), Moldova (MD), Oroszország (RU), Tádzsikisztán (TJ), Üzbegisztán (UZ), Ukrajna (UA), India, Brazília, Dél-Afrika, Lengyelország, Egyesült Arab Emírségek, Szaúd-Arábia, Törökország, Thaiföld, Vietnam, Mianmar, Irak, Dél-Szudán és Venezuela.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-157">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), India, Brazil, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan and Venezuela.</span></span> <span data-ttu-id="e1cbd-158">Az ügyfél más országokban található vállalata/szervezete számára ez egy választható mező.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-158">For customer’s company/organization located in other countries this is an optional field.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="e1cbd-159">Számlázási profil</span><span class="sxs-lookup"><span data-stu-id="e1cbd-159">Billing profile</span></span>

<span data-ttu-id="e1cbd-160">Ez a táblázat az új ügyfelek létrehozásához szükséges [CustomerBillingProfile](customer-resources.md#customerbillingprofile) -erőforrás minimálisan szükséges mezőit ismerteti.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-160">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="e1cbd-161">Név</span><span class="sxs-lookup"><span data-stu-id="e1cbd-161">Name</span></span>             | <span data-ttu-id="e1cbd-162">Típus</span><span class="sxs-lookup"><span data-stu-id="e1cbd-162">Type</span></span>                                     | <span data-ttu-id="e1cbd-163">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e1cbd-163">Required</span></span> | <span data-ttu-id="e1cbd-164">Leírás</span><span class="sxs-lookup"><span data-stu-id="e1cbd-164">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e1cbd-165">e-mail</span><span class="sxs-lookup"><span data-stu-id="e1cbd-165">email</span></span>            | <span data-ttu-id="e1cbd-166">sztring</span><span class="sxs-lookup"><span data-stu-id="e1cbd-166">string</span></span>                                   | <span data-ttu-id="e1cbd-167">Yes</span><span class="sxs-lookup"><span data-stu-id="e1cbd-167">Yes</span></span>      | <span data-ttu-id="e1cbd-168">Az ügyfél e-mail-címe.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-168">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="e1cbd-169">kulturális környezet</span><span class="sxs-lookup"><span data-stu-id="e1cbd-169">culture</span></span>          | <span data-ttu-id="e1cbd-170">sztring</span><span class="sxs-lookup"><span data-stu-id="e1cbd-170">string</span></span>                                   | <span data-ttu-id="e1cbd-171">Yes</span><span class="sxs-lookup"><span data-stu-id="e1cbd-171">Yes</span></span>      | <span data-ttu-id="e1cbd-172">Az előnyben részesített kulturális környezet a kommunikációhoz és a pénznemhez, mint például az "en-US".</span><span class="sxs-lookup"><span data-stu-id="e1cbd-172">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="e1cbd-173">Lásd: a [partneri központ által támogatott nyelvek és területi beállítások](partner-center-supported-languages-and-locales.md) a támogatott kulturális környezetekhez.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-173">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="e1cbd-174">language</span><span class="sxs-lookup"><span data-stu-id="e1cbd-174">language</span></span>         | <span data-ttu-id="e1cbd-175">sztring</span><span class="sxs-lookup"><span data-stu-id="e1cbd-175">string</span></span>                                   | <span data-ttu-id="e1cbd-176">Yes</span><span class="sxs-lookup"><span data-stu-id="e1cbd-176">Yes</span></span>      | <span data-ttu-id="e1cbd-177">Az alapértelmezett nyelv.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-177">The default language.</span></span> <span data-ttu-id="e1cbd-178">Két karakterből álló nyelvi kód (például `en` vagy `fr` ) támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-178">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="e1cbd-179">cég \_ neve</span><span class="sxs-lookup"><span data-stu-id="e1cbd-179">company\_name</span></span>    | <span data-ttu-id="e1cbd-180">sztring</span><span class="sxs-lookup"><span data-stu-id="e1cbd-180">string</span></span>                                   | <span data-ttu-id="e1cbd-181">Yes</span><span class="sxs-lookup"><span data-stu-id="e1cbd-181">Yes</span></span>      | <span data-ttu-id="e1cbd-182">A regisztrált vállalat/szervezet neve.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-182">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="e1cbd-183">alapértelmezett \_ címe</span><span class="sxs-lookup"><span data-stu-id="e1cbd-183">default\_address</span></span> | [<span data-ttu-id="e1cbd-184">Cím</span><span class="sxs-lookup"><span data-stu-id="e1cbd-184">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="e1cbd-185">Yes</span><span class="sxs-lookup"><span data-stu-id="e1cbd-185">Yes</span></span>      | <span data-ttu-id="e1cbd-186">Az ügyfél vállalatának/szervezetének regisztrált címe.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-186">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="e1cbd-187">A hosszra vonatkozó korlátozásokkal kapcsolatos információkért tekintse meg a [címe](utility-resources.md#address) erőforrását.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-187">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="e1cbd-188">Vállalati profil</span><span class="sxs-lookup"><span data-stu-id="e1cbd-188">Company profile</span></span>

<span data-ttu-id="e1cbd-189">Ez a táblázat az új ügyfelek létrehozásához szükséges [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) -erőforrás minimálisan szükséges mezőit ismerteti.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-189">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="e1cbd-190">Név</span><span class="sxs-lookup"><span data-stu-id="e1cbd-190">Name</span></span>   | <span data-ttu-id="e1cbd-191">Típus</span><span class="sxs-lookup"><span data-stu-id="e1cbd-191">Type</span></span>   | <span data-ttu-id="e1cbd-192">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e1cbd-192">Required</span></span> | <span data-ttu-id="e1cbd-193">Leírás</span><span class="sxs-lookup"><span data-stu-id="e1cbd-193">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="e1cbd-194">domain</span><span class="sxs-lookup"><span data-stu-id="e1cbd-194">domain</span></span> | <span data-ttu-id="e1cbd-195">sztring</span><span class="sxs-lookup"><span data-stu-id="e1cbd-195">string</span></span> | <span data-ttu-id="e1cbd-196">Yes</span><span class="sxs-lookup"><span data-stu-id="e1cbd-196">Yes</span></span>     | <span data-ttu-id="e1cbd-197">Az ügyfél tartományának neve, például contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-197">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="e1cbd-198">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="e1cbd-198">organizationRegistrationNumber</span></span> | <span data-ttu-id="e1cbd-199">sztring</span><span class="sxs-lookup"><span data-stu-id="e1cbd-199">string</span></span> | <span data-ttu-id="e1cbd-200">Feltételtől függ</span><span class="sxs-lookup"><span data-stu-id="e1cbd-200">Depends on condition</span></span> | <span data-ttu-id="e1cbd-201">Az ügyfél szervezetének regisztrációs száma (más néven az egyes országokban található INN-szám).</span><span class="sxs-lookup"><span data-stu-id="e1cbd-201">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="e1cbd-202">A mező kitöltése csak akkor szükséges, ha az ügyfél vállalata/szervezete a következő országokban található:</span><span class="sxs-lookup"><span data-stu-id="e1cbd-202">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="e1cbd-203">-Örményország (AM)</span><span class="sxs-lookup"><span data-stu-id="e1cbd-203">- Armenia (AM)</span></span> <br/><span data-ttu-id="e1cbd-204">-Azerbajdzsán (AZ)</span><span class="sxs-lookup"><span data-stu-id="e1cbd-204">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="e1cbd-205">– Fehéroroszország (BY)</span><span class="sxs-lookup"><span data-stu-id="e1cbd-205">- Belarus (BY)</span></span><br/><span data-ttu-id="e1cbd-206">– Magyarország (HU)</span><span class="sxs-lookup"><span data-stu-id="e1cbd-206">- Hungary (HU)</span></span><br/><span data-ttu-id="e1cbd-207">-Kazahsztán (KZ)</span><span class="sxs-lookup"><span data-stu-id="e1cbd-207">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="e1cbd-208">-Kirgizisztán (KG)</span><span class="sxs-lookup"><span data-stu-id="e1cbd-208">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="e1cbd-209">-Moldova (MD)</span><span class="sxs-lookup"><span data-stu-id="e1cbd-209">- Moldova (MD)</span></span><br/><span data-ttu-id="e1cbd-210">– Oroszország (RU)</span><span class="sxs-lookup"><span data-stu-id="e1cbd-210">- Russia (RU)</span></span><br/><span data-ttu-id="e1cbd-211">– Tádzsikisztán (TJ)</span><span class="sxs-lookup"><span data-stu-id="e1cbd-211">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="e1cbd-212">-Üzbegisztán (UZ)</span><span class="sxs-lookup"><span data-stu-id="e1cbd-212">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="e1cbd-213">– Ukrajna (UA)</span><span class="sxs-lookup"><span data-stu-id="e1cbd-213">- Ukraine (UA)</span></span><br/><br/><span data-ttu-id="e1cbd-214">Erre a mezőre nincs szükség, ha az ügyfél vállalata/szervezete más országokban található, az itt láthatónál tovább.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-214">This field is not required if the customer’s company/organization is located in other countries beyond those shown here.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="e1cbd-215">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="e1cbd-215">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="e1cbd-216">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="e1cbd-216">REST response</span></span>

<span data-ttu-id="e1cbd-217">Ha ez sikeres, a válasz az új ügyfélhez tartozó [ügyfél](customer-resources.md#customer) -erőforrást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-217">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e1cbd-218">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="e1cbd-218">Response success and error codes</span></span>

<span data-ttu-id="e1cbd-219">A válaszok olyan HTTP-állapotkódot mutatnak be, amely sikeres vagy sikertelen, valamint további hibakeresési információkat jelez.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-219">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e1cbd-220">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-220">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e1cbd-221">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="e1cbd-221">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e1cbd-222">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="e1cbd-222">Response example</span></span>

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