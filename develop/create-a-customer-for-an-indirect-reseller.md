---
title: Ügyfél létrehozása egy közvetett viszonteladónál
description: Megtudhatja, hogyan használhatja a közvetett szolgáltató a partner Center API-kat, hogy ügyfelet hozzon létre egy közvetett viszonteladó számára.
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 0de40d08e9fc2b9cf87b7c3c41214fdd34ad26f3
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274580"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="5af4c-103">Ügyfél létrehozása közvetett viszonteladók számára a partner Center API-k használatával</span><span class="sxs-lookup"><span data-stu-id="5af4c-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="5af4c-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="5af4c-104">**Applies to:**</span></span>

- <span data-ttu-id="5af4c-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="5af4c-105">Partner Center</span></span>

<span data-ttu-id="5af4c-106">A közvetett szolgáltató létrehozhat egy ügyfelet közvetett viszonteladónak.</span><span class="sxs-lookup"><span data-stu-id="5af4c-106">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5af4c-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5af4c-107">Prerequisites</span></span>

- <span data-ttu-id="5af4c-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="5af4c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5af4c-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="5af4c-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5af4c-110">A közvetett viszonteladó bérlői azonosítója.</span><span class="sxs-lookup"><span data-stu-id="5af4c-110">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="5af4c-111">A közvetett viszonteladónak partneri kapcsolattal kell rendelkeznie a közvetett szolgáltatóval.</span><span class="sxs-lookup"><span data-stu-id="5af4c-111">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="5af4c-112">C\#</span><span class="sxs-lookup"><span data-stu-id="5af4c-112">C\#</span></span>

<span data-ttu-id="5af4c-113">Új ügyfél hozzáadása közvetett viszonteladóhoz:</span><span class="sxs-lookup"><span data-stu-id="5af4c-113">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="5af4c-114">Új [**ügyfél**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) -objektum létrehozása, majd a [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) és a [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)példányának létrehozása és feltöltése.</span><span class="sxs-lookup"><span data-stu-id="5af4c-114">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="5af4c-115">Ügyeljen arra, hogy a közvetett viszonteladó AZONOSÍTÓját a [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) tulajdonsághoz rendelje.</span><span class="sxs-lookup"><span data-stu-id="5af4c-115">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="5af4c-116">A [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) tulajdonsággal szerezzen be egy felületet az ügyfél-gyűjtési műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="5af4c-116">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="5af4c-117">A [**create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metódus meghívásával hozza létre az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="5af4c-117">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="5af4c-118">C \# példa</span><span class="sxs-lookup"><span data-stu-id="5af4c-118">C\# example</span></span>

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

<span data-ttu-id="5af4c-119">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5af4c-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5af4c-120">**Projekt**: partner Center SDK Samples **osztály**: CreateCustomerforIndirectReseller. cs</span><span class="sxs-lookup"><span data-stu-id="5af4c-120">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5af4c-121">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="5af4c-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5af4c-122">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5af4c-122">Request syntax</span></span>

| <span data-ttu-id="5af4c-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="5af4c-123">Method</span></span>   | <span data-ttu-id="5af4c-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5af4c-124">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="5af4c-125">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="5af4c-125">**POST**</span></span> | <span data-ttu-id="5af4c-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers http/1.1</span><span class="sxs-lookup"><span data-stu-id="5af4c-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5af4c-127">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5af4c-127">Request headers</span></span>

<span data-ttu-id="5af4c-128">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5af4c-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5af4c-129">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="5af4c-129">Request body</span></span>

<span data-ttu-id="5af4c-130">Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="5af4c-130">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="5af4c-131">Név</span><span class="sxs-lookup"><span data-stu-id="5af4c-131">Name</span></span>                                          | <span data-ttu-id="5af4c-132">Típus</span><span class="sxs-lookup"><span data-stu-id="5af4c-132">Type</span></span>   | <span data-ttu-id="5af4c-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5af4c-133">Required</span></span> | <span data-ttu-id="5af4c-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="5af4c-134">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="5af4c-135">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="5af4c-135">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="5af4c-136">object</span><span class="sxs-lookup"><span data-stu-id="5af4c-136">object</span></span> | <span data-ttu-id="5af4c-137">Igen</span><span class="sxs-lookup"><span data-stu-id="5af4c-137">Yes</span></span>      | <span data-ttu-id="5af4c-138">Az ügyfél számlázási profiljának adatai.</span><span class="sxs-lookup"><span data-stu-id="5af4c-138">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="5af4c-139">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="5af4c-139">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="5af4c-140">object</span><span class="sxs-lookup"><span data-stu-id="5af4c-140">object</span></span> | <span data-ttu-id="5af4c-141">Igen</span><span class="sxs-lookup"><span data-stu-id="5af4c-141">Yes</span></span>      | <span data-ttu-id="5af4c-142">Az ügyfél vállalati profiljának adatai.</span><span class="sxs-lookup"><span data-stu-id="5af4c-142">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="5af4c-143">AssociatedPartnerId</span><span class="sxs-lookup"><span data-stu-id="5af4c-143">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="5af4c-144">sztring</span><span class="sxs-lookup"><span data-stu-id="5af4c-144">string</span></span> | <span data-ttu-id="5af4c-145">Igen</span><span class="sxs-lookup"><span data-stu-id="5af4c-145">Yes</span></span>      | <span data-ttu-id="5af4c-146">A közvetett viszonteladó azonosítója.</span><span class="sxs-lookup"><span data-stu-id="5af4c-146">The indirect reseller ID.</span></span> <span data-ttu-id="5af4c-147">Az itt megadott azonosító által jelzett közvetett viszonteladónak partneri kapcsolattal kell rendelkeznie a közvetett szolgáltatóval, vagy a kérés sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="5af4c-147">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="5af4c-148">Azt is vegye figyelembe, hogy ha a AssociatedPartnerId érték nincs megadva, az ügyfél a közvetett szolgáltató közvetlen ügyfeleként jön létre a közvetett viszonteladó helyett.</span><span class="sxs-lookup"><span data-stu-id="5af4c-148">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="5af4c-149">Tartomány</span><span class="sxs-lookup"><span data-stu-id="5af4c-149">Domain</span></span>| <span data-ttu-id="5af4c-150">Sztring</span><span class="sxs-lookup"><span data-stu-id="5af4c-150">String</span></span>| <span data-ttu-id="5af4c-151">Igen</span><span class="sxs-lookup"><span data-stu-id="5af4c-151">Yes</span></span>|<span data-ttu-id="5af4c-152">Az ügyfél tartományának neve, például contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="5af4c-152">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="5af4c-153">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="5af4c-153">organizationRegistrationNumber</span></span>|    <span data-ttu-id="5af4c-154">sztring</span><span class="sxs-lookup"><span data-stu-id="5af4c-154">string</span></span>|<span data-ttu-id="5af4c-155">Igen</span><span class="sxs-lookup"><span data-stu-id="5af4c-155">Yes</span></span>|     <span data-ttu-id="5af4c-156">Az ügyfél szervezetének regisztrációs száma (más néven az INN száma bizonyos országokban).</span><span class="sxs-lookup"><span data-stu-id="5af4c-156">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="5af4c-157">Csak a következő országokban található ügyfél vállalata vagy szervezete számára szükséges: Örményország (AM), Azerbajdzsán (AZ), Fehéroroszország (BY), Magyarország (HU), Kazahsztán (KZ), Kirgizisztán (KG), Moldova (MD), Oroszország (RU), Tádzsikisztán (TJ), Üzbegisztán (UZ), Ukrajna (UA), India, Brazília, Dél-Afrika, Lengyelország, Egyesült Arab Emírségek, Szaúd-Arábia, Törökország, Thaiföld, Vietnam, Mianmar, Irak, Dél-Szudán és Venezuela.</span><span class="sxs-lookup"><span data-stu-id="5af4c-157">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), India, Brazil, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan and Venezuela.</span></span> <span data-ttu-id="5af4c-158">Az ügyfél más országokban található vállalata/szervezete számára ez egy választható mező.</span><span class="sxs-lookup"><span data-stu-id="5af4c-158">For customer’s company/organization located in other countries this is an optional field.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="5af4c-159">Számlázási profil</span><span class="sxs-lookup"><span data-stu-id="5af4c-159">Billing profile</span></span>

<span data-ttu-id="5af4c-160">Ez a táblázat az új ügyfelek létrehozásához szükséges [CustomerBillingProfile](customer-resources.md#customerbillingprofile) -erőforrás minimálisan szükséges mezőit ismerteti.</span><span class="sxs-lookup"><span data-stu-id="5af4c-160">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="5af4c-161">Név</span><span class="sxs-lookup"><span data-stu-id="5af4c-161">Name</span></span>             | <span data-ttu-id="5af4c-162">Típus</span><span class="sxs-lookup"><span data-stu-id="5af4c-162">Type</span></span>                                     | <span data-ttu-id="5af4c-163">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5af4c-163">Required</span></span> | <span data-ttu-id="5af4c-164">Leírás</span><span class="sxs-lookup"><span data-stu-id="5af4c-164">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5af4c-165">e-mail</span><span class="sxs-lookup"><span data-stu-id="5af4c-165">email</span></span>            | <span data-ttu-id="5af4c-166">sztring</span><span class="sxs-lookup"><span data-stu-id="5af4c-166">string</span></span>                                   | <span data-ttu-id="5af4c-167">Igen</span><span class="sxs-lookup"><span data-stu-id="5af4c-167">Yes</span></span>      | <span data-ttu-id="5af4c-168">Az ügyfél e-mail-címe.</span><span class="sxs-lookup"><span data-stu-id="5af4c-168">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="5af4c-169">kulturális környezet</span><span class="sxs-lookup"><span data-stu-id="5af4c-169">culture</span></span>          | <span data-ttu-id="5af4c-170">sztring</span><span class="sxs-lookup"><span data-stu-id="5af4c-170">string</span></span>                                   | <span data-ttu-id="5af4c-171">Igen</span><span class="sxs-lookup"><span data-stu-id="5af4c-171">Yes</span></span>      | <span data-ttu-id="5af4c-172">Az előnyben részesített kulturális környezet a kommunikációhoz és a pénznemhez, mint például az "en-US".</span><span class="sxs-lookup"><span data-stu-id="5af4c-172">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="5af4c-173">Lásd: a [partneri központ által támogatott nyelvek és területi beállítások](partner-center-supported-languages-and-locales.md) a támogatott kulturális környezetekhez.</span><span class="sxs-lookup"><span data-stu-id="5af4c-173">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="5af4c-174">language</span><span class="sxs-lookup"><span data-stu-id="5af4c-174">language</span></span>         | <span data-ttu-id="5af4c-175">sztring</span><span class="sxs-lookup"><span data-stu-id="5af4c-175">string</span></span>                                   | <span data-ttu-id="5af4c-176">Igen</span><span class="sxs-lookup"><span data-stu-id="5af4c-176">Yes</span></span>      | <span data-ttu-id="5af4c-177">Az alapértelmezett nyelv.</span><span class="sxs-lookup"><span data-stu-id="5af4c-177">The default language.</span></span> <span data-ttu-id="5af4c-178">Két karakterből álló nyelvi kód (például `en` vagy `fr` ) támogatott.</span><span class="sxs-lookup"><span data-stu-id="5af4c-178">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="5af4c-179">cég \_ neve</span><span class="sxs-lookup"><span data-stu-id="5af4c-179">company\_name</span></span>    | <span data-ttu-id="5af4c-180">sztring</span><span class="sxs-lookup"><span data-stu-id="5af4c-180">string</span></span>                                   | <span data-ttu-id="5af4c-181">Igen</span><span class="sxs-lookup"><span data-stu-id="5af4c-181">Yes</span></span>      | <span data-ttu-id="5af4c-182">A regisztrált vállalat/szervezet neve.</span><span class="sxs-lookup"><span data-stu-id="5af4c-182">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="5af4c-183">alapértelmezett \_ címe</span><span class="sxs-lookup"><span data-stu-id="5af4c-183">default\_address</span></span> | [<span data-ttu-id="5af4c-184">Cím</span><span class="sxs-lookup"><span data-stu-id="5af4c-184">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="5af4c-185">Igen</span><span class="sxs-lookup"><span data-stu-id="5af4c-185">Yes</span></span>      | <span data-ttu-id="5af4c-186">Az ügyfél vállalatának/szervezetének regisztrált címe.</span><span class="sxs-lookup"><span data-stu-id="5af4c-186">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="5af4c-187">A hosszra vonatkozó korlátozásokkal kapcsolatos információkért tekintse meg a [címe](utility-resources.md#address) erőforrását.</span><span class="sxs-lookup"><span data-stu-id="5af4c-187">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="5af4c-188">Vállalati profil</span><span class="sxs-lookup"><span data-stu-id="5af4c-188">Company profile</span></span>

<span data-ttu-id="5af4c-189">Ez a táblázat az új ügyfelek létrehozásához szükséges [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) -erőforrás minimálisan szükséges mezőit ismerteti.</span><span class="sxs-lookup"><span data-stu-id="5af4c-189">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="5af4c-190">Név</span><span class="sxs-lookup"><span data-stu-id="5af4c-190">Name</span></span>   | <span data-ttu-id="5af4c-191">Típus</span><span class="sxs-lookup"><span data-stu-id="5af4c-191">Type</span></span>   | <span data-ttu-id="5af4c-192">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5af4c-192">Required</span></span> | <span data-ttu-id="5af4c-193">Leírás</span><span class="sxs-lookup"><span data-stu-id="5af4c-193">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="5af4c-194">domain</span><span class="sxs-lookup"><span data-stu-id="5af4c-194">domain</span></span> | <span data-ttu-id="5af4c-195">sztring</span><span class="sxs-lookup"><span data-stu-id="5af4c-195">string</span></span> | <span data-ttu-id="5af4c-196">Igen</span><span class="sxs-lookup"><span data-stu-id="5af4c-196">Yes</span></span>     | <span data-ttu-id="5af4c-197">Az ügyfél tartományának neve, például contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="5af4c-197">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="5af4c-198">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="5af4c-198">organizationRegistrationNumber</span></span> | <span data-ttu-id="5af4c-199">sztring</span><span class="sxs-lookup"><span data-stu-id="5af4c-199">string</span></span> | <span data-ttu-id="5af4c-200">Feltételtől függ</span><span class="sxs-lookup"><span data-stu-id="5af4c-200">Depends on condition</span></span> | <span data-ttu-id="5af4c-201">Az ügyfél szervezetének regisztrációs száma (más néven az egyes országokban található INN-szám).</span><span class="sxs-lookup"><span data-stu-id="5af4c-201">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="5af4c-202">A mező kitöltése csak akkor szükséges, ha az ügyfél vállalata/szervezete a következő országokban található:</span><span class="sxs-lookup"><span data-stu-id="5af4c-202">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="5af4c-203">-Örményország (AM)</span><span class="sxs-lookup"><span data-stu-id="5af4c-203">- Armenia (AM)</span></span> <br/><span data-ttu-id="5af4c-204">-Azerbajdzsán (AZ)</span><span class="sxs-lookup"><span data-stu-id="5af4c-204">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="5af4c-205">– Fehéroroszország (BY)</span><span class="sxs-lookup"><span data-stu-id="5af4c-205">- Belarus (BY)</span></span><br/><span data-ttu-id="5af4c-206">– Magyarország (HU)</span><span class="sxs-lookup"><span data-stu-id="5af4c-206">- Hungary (HU)</span></span><br/><span data-ttu-id="5af4c-207">-Kazahsztán (KZ)</span><span class="sxs-lookup"><span data-stu-id="5af4c-207">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="5af4c-208">-Kirgizisztán (KG)</span><span class="sxs-lookup"><span data-stu-id="5af4c-208">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="5af4c-209">-Moldova (MD)</span><span class="sxs-lookup"><span data-stu-id="5af4c-209">- Moldova (MD)</span></span><br/><span data-ttu-id="5af4c-210">– Oroszország (RU)</span><span class="sxs-lookup"><span data-stu-id="5af4c-210">- Russia (RU)</span></span><br/><span data-ttu-id="5af4c-211">– Tádzsikisztán (TJ)</span><span class="sxs-lookup"><span data-stu-id="5af4c-211">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="5af4c-212">-Üzbegisztán (UZ)</span><span class="sxs-lookup"><span data-stu-id="5af4c-212">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="5af4c-213">– Ukrajna (UA)</span><span class="sxs-lookup"><span data-stu-id="5af4c-213">- Ukraine (UA)</span></span><br/><span data-ttu-id="5af4c-214">– India</span><span class="sxs-lookup"><span data-stu-id="5af4c-214">- India</span></span> <br/><span data-ttu-id="5af4c-215">– Brazília</span><span class="sxs-lookup"><span data-stu-id="5af4c-215">- Brazil</span></span> <br/><span data-ttu-id="5af4c-216">– Dél-Afrika</span><span class="sxs-lookup"><span data-stu-id="5af4c-216">- South Africa</span></span> <br/><span data-ttu-id="5af4c-217">-Lengyelország</span><span class="sxs-lookup"><span data-stu-id="5af4c-217">- Poland</span></span> <br/><span data-ttu-id="5af4c-218">– Egyesült Arab Emírségek</span><span class="sxs-lookup"><span data-stu-id="5af4c-218">- United Arab Emirates</span></span> <br/><span data-ttu-id="5af4c-219">– Szaúd-Arábia</span><span class="sxs-lookup"><span data-stu-id="5af4c-219">- Saudi Arabia</span></span> <br/><span data-ttu-id="5af4c-220">– Törökország</span><span class="sxs-lookup"><span data-stu-id="5af4c-220">- Turkey</span></span> <br/><span data-ttu-id="5af4c-221">– Thaiföld</span><span class="sxs-lookup"><span data-stu-id="5af4c-221">- Thailand</span></span> <br/><span data-ttu-id="5af4c-222">– Vietnam</span><span class="sxs-lookup"><span data-stu-id="5af4c-222">- Vietnam</span></span> <br/><span data-ttu-id="5af4c-223">-Mianmar</span><span class="sxs-lookup"><span data-stu-id="5af4c-223">- Myanmar</span></span> <br/><span data-ttu-id="5af4c-224">– Irak</span><span class="sxs-lookup"><span data-stu-id="5af4c-224">- Iraq</span></span> <br/><span data-ttu-id="5af4c-225">– Dél-Szudán</span><span class="sxs-lookup"><span data-stu-id="5af4c-225">- South Sudan</span></span> <br/><span data-ttu-id="5af4c-226">– Venezuela</span><span class="sxs-lookup"><span data-stu-id="5af4c-226">- Venezuela</span></span><br/> <br/><span data-ttu-id="5af4c-227">Az ügyfél más országokban található vállalata/szervezete számára ez egy választható mező.</span><span class="sxs-lookup"><span data-stu-id="5af4c-227">For customer’s company/organization located in other countries this is an optional field.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="5af4c-228">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5af4c-228">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="5af4c-229">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5af4c-229">REST response</span></span>

<span data-ttu-id="5af4c-230">Ha ez sikeres, a válasz az új ügyfélhez tartozó [ügyfél](customer-resources.md#customer) -erőforrást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="5af4c-230">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5af4c-231">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5af4c-231">Response success and error codes</span></span>

<span data-ttu-id="5af4c-232">A válaszok olyan HTTP-állapotkódot mutatnak be, amely sikeres vagy sikertelen, valamint további hibakeresési információkat jelez.</span><span class="sxs-lookup"><span data-stu-id="5af4c-232">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5af4c-233">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="5af4c-233">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5af4c-234">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="5af4c-234">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5af4c-235">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5af4c-235">Response example</span></span>

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