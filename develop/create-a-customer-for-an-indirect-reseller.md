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
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="cd718-103">Ügyfél létrehozása közvetett viszonteladó számára a Partnerközpont API-k használatával</span><span class="sxs-lookup"><span data-stu-id="cd718-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="cd718-104">Egy közvetett szolgáltató létrehozhat egy ügyfelet egy közvetett viszonteladó számára.</span><span class="sxs-lookup"><span data-stu-id="cd718-104">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd718-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="cd718-105">Prerequisites</span></span>

- <span data-ttu-id="cd718-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="cd718-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cd718-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="cd718-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="cd718-108">A közvetett viszonteladó bérlőazonosítója.</span><span class="sxs-lookup"><span data-stu-id="cd718-108">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="cd718-109">A közvetett viszonteladónak partnerkapcsolatban kell lennie a közvetett szolgáltatóval.</span><span class="sxs-lookup"><span data-stu-id="cd718-109">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="cd718-110">C\#</span><span class="sxs-lookup"><span data-stu-id="cd718-110">C\#</span></span>

<span data-ttu-id="cd718-111">Új ügyfél hozzáadása egy közvetett viszonteladóhoz:</span><span class="sxs-lookup"><span data-stu-id="cd718-111">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="cd718-112">Példányosuljon egy új [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) objektum, majd példányosuljon és töltse fel a [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) és a [**CompanyProfile adatokat.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)</span><span class="sxs-lookup"><span data-stu-id="cd718-112">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="cd718-113">Mindenképpen rendelje hozzá a közvetett viszonteladó azonosítóját az [**AssociatedPartnerID tulajdonsághoz.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid)</span><span class="sxs-lookup"><span data-stu-id="cd718-113">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="cd718-114">Az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) tulajdonság használatával lekért felület az ügyfélgyűjtési műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="cd718-114">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="cd718-115">Az ügyfél [**létrehozásához**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) hívja meg a [**Create vagy a CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="cd718-115">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="cd718-116">C \# példa</span><span class="sxs-lookup"><span data-stu-id="cd718-116">C\# example</span></span>

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

<span data-ttu-id="cd718-117">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="cd718-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="cd718-118">**Project**: Partnerközpont SDK **Osztály:** CreateCustomerforIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="cd718-118">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="cd718-119">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="cd718-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cd718-120">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="cd718-120">Request syntax</span></span>

| <span data-ttu-id="cd718-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="cd718-121">Method</span></span>   | <span data-ttu-id="cd718-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="cd718-122">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="cd718-123">**Post**</span><span class="sxs-lookup"><span data-stu-id="cd718-123">**POST**</span></span> | <span data-ttu-id="cd718-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cd718-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cd718-125">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="cd718-125">Request headers</span></span>

<span data-ttu-id="cd718-126">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="cd718-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cd718-127">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="cd718-127">Request body</span></span>

<span data-ttu-id="cd718-128">Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="cd718-128">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="cd718-129">Név</span><span class="sxs-lookup"><span data-stu-id="cd718-129">Name</span></span>                                          | <span data-ttu-id="cd718-130">Típus</span><span class="sxs-lookup"><span data-stu-id="cd718-130">Type</span></span>   | <span data-ttu-id="cd718-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="cd718-131">Required</span></span> | <span data-ttu-id="cd718-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="cd718-132">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="cd718-133">BillingProfile (Számlázási profil)</span><span class="sxs-lookup"><span data-stu-id="cd718-133">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="cd718-134">object</span><span class="sxs-lookup"><span data-stu-id="cd718-134">object</span></span> | <span data-ttu-id="cd718-135">Igen</span><span class="sxs-lookup"><span data-stu-id="cd718-135">Yes</span></span>      | <span data-ttu-id="cd718-136">Az ügyfél számlázási profiljának adatai.</span><span class="sxs-lookup"><span data-stu-id="cd718-136">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="cd718-137">Vállalatiprofil</span><span class="sxs-lookup"><span data-stu-id="cd718-137">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="cd718-138">object</span><span class="sxs-lookup"><span data-stu-id="cd718-138">object</span></span> | <span data-ttu-id="cd718-139">Igen</span><span class="sxs-lookup"><span data-stu-id="cd718-139">Yes</span></span>      | <span data-ttu-id="cd718-140">Az ügyfél céges profilinformációi.</span><span class="sxs-lookup"><span data-stu-id="cd718-140">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="cd718-141">AssociatedPartnerId (Társított partnerazonosító)</span><span class="sxs-lookup"><span data-stu-id="cd718-141">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="cd718-142">sztring</span><span class="sxs-lookup"><span data-stu-id="cd718-142">string</span></span> | <span data-ttu-id="cd718-143">Igen</span><span class="sxs-lookup"><span data-stu-id="cd718-143">Yes</span></span>      | <span data-ttu-id="cd718-144">A közvetett viszonteladó azonosítója.</span><span class="sxs-lookup"><span data-stu-id="cd718-144">The indirect reseller ID.</span></span> <span data-ttu-id="cd718-145">Az itt megadott azonosítóval jelzett közvetett viszonteladónak partnerkapcsolatban kell lennie a közvetett szolgáltatóval, különben a kérelem meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="cd718-145">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="cd718-146">Azt is vegye figyelembe, hogy ha az AssociatedPartnerId érték nincs megadva, az ügyfél a közvetett szolgáltató közvetlen ügyfeleként jön létre, nem pedig közvetett viszonteladóként.</span><span class="sxs-lookup"><span data-stu-id="cd718-146">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="cd718-147">Tartomány</span><span class="sxs-lookup"><span data-stu-id="cd718-147">Domain</span></span>| <span data-ttu-id="cd718-148">Sztring</span><span class="sxs-lookup"><span data-stu-id="cd718-148">String</span></span>| <span data-ttu-id="cd718-149">Igen</span><span class="sxs-lookup"><span data-stu-id="cd718-149">Yes</span></span>|<span data-ttu-id="cd718-150">Az ügyfél tartományneve, például contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="cd718-150">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="cd718-151">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="cd718-151">organizationRegistrationNumber</span></span>|    <span data-ttu-id="cd718-152">sztring</span><span class="sxs-lookup"><span data-stu-id="cd718-152">string</span></span>|<span data-ttu-id="cd718-153">Igen</span><span class="sxs-lookup"><span data-stu-id="cd718-153">Yes</span></span>|     <span data-ttu-id="cd718-154">Az ügyfél szervezeti regisztrációs száma (más néven INN-szám bizonyos országokban).</span><span class="sxs-lookup"><span data-stu-id="cd718-154">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="cd718-155">Csak a következő országokban található ügyfél vállalatához/szervezetéhez szükséges: Egyesült Államok(AM), Uzbekistan(AZ), Uzbekistan(BY), Amelyet (HU), Mirgyzstan(KZ), Kirgyzstan(KG), Torgyzsán (KG), Toajikistan(TJ), Uzbekistan(UZ), Uzbekistan(UA), India, Brazília, Dél-Afrika, Észak-Afrika, Egyesült Arab Emírségek, Szaúd-Arábia, Szignában, Vietnamban, Észak-Karolinában, Szignában, Dél-Afrikai Köztársaságban és Szignában.</span><span class="sxs-lookup"><span data-stu-id="cd718-155">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), India, Brazil, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan, and Venezuela.</span></span> <span data-ttu-id="cd718-156">Az ügyfél más országokban található vállalata/szervezete esetén ez egy nem kötelező mező.</span><span class="sxs-lookup"><span data-stu-id="cd718-156">For customer’s company/organization located in other countries this is an optional field.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="cd718-157">Számlázási profil</span><span class="sxs-lookup"><span data-stu-id="cd718-157">Billing profile</span></span>

<span data-ttu-id="cd718-158">Ez a táblázat az új ügyfél létrehozásához szükséges Minimálisan szükséges mezőket ismerteti a [CustomerBillingProfile](customer-resources.md#customerbillingprofile) erőforrásból.</span><span class="sxs-lookup"><span data-stu-id="cd718-158">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="cd718-159">Név</span><span class="sxs-lookup"><span data-stu-id="cd718-159">Name</span></span>             | <span data-ttu-id="cd718-160">Típus</span><span class="sxs-lookup"><span data-stu-id="cd718-160">Type</span></span>                                     | <span data-ttu-id="cd718-161">Kötelező</span><span class="sxs-lookup"><span data-stu-id="cd718-161">Required</span></span> | <span data-ttu-id="cd718-162">Leírás</span><span class="sxs-lookup"><span data-stu-id="cd718-162">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cd718-163">e-mail</span><span class="sxs-lookup"><span data-stu-id="cd718-163">email</span></span>            | <span data-ttu-id="cd718-164">sztring</span><span class="sxs-lookup"><span data-stu-id="cd718-164">string</span></span>                                   | <span data-ttu-id="cd718-165">Igen</span><span class="sxs-lookup"><span data-stu-id="cd718-165">Yes</span></span>      | <span data-ttu-id="cd718-166">Az ügyfél e-mail-címe.</span><span class="sxs-lookup"><span data-stu-id="cd718-166">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="cd718-167">Kultúra</span><span class="sxs-lookup"><span data-stu-id="cd718-167">culture</span></span>          | <span data-ttu-id="cd718-168">sztring</span><span class="sxs-lookup"><span data-stu-id="cd718-168">string</span></span>                                   | <span data-ttu-id="cd718-169">Igen</span><span class="sxs-lookup"><span data-stu-id="cd718-169">Yes</span></span>      | <span data-ttu-id="cd718-170">A kommunikáció és a pénznem előnyben részesített kultúrája, például "en-US".</span><span class="sxs-lookup"><span data-stu-id="cd718-170">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="cd718-171">Lásd [Partnerközpont támogatott nyelvek és területi stb.](partner-center-supported-languages-and-locales.md)</span><span class="sxs-lookup"><span data-stu-id="cd718-171">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="cd718-172">language</span><span class="sxs-lookup"><span data-stu-id="cd718-172">language</span></span>         | <span data-ttu-id="cd718-173">sztring</span><span class="sxs-lookup"><span data-stu-id="cd718-173">string</span></span>                                   | <span data-ttu-id="cd718-174">Igen</span><span class="sxs-lookup"><span data-stu-id="cd718-174">Yes</span></span>      | <span data-ttu-id="cd718-175">Az alapértelmezett nyelv.</span><span class="sxs-lookup"><span data-stu-id="cd718-175">The default language.</span></span> <span data-ttu-id="cd718-176">Két karakteres nyelvkód (például `en` vagy `fr` ) támogatott.</span><span class="sxs-lookup"><span data-stu-id="cd718-176">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="cd718-177">vállalat \_ neve</span><span class="sxs-lookup"><span data-stu-id="cd718-177">company\_name</span></span>    | <span data-ttu-id="cd718-178">sztring</span><span class="sxs-lookup"><span data-stu-id="cd718-178">string</span></span>                                   | <span data-ttu-id="cd718-179">Igen</span><span class="sxs-lookup"><span data-stu-id="cd718-179">Yes</span></span>      | <span data-ttu-id="cd718-180">A regisztrált vállalat/szervezet neve.</span><span class="sxs-lookup"><span data-stu-id="cd718-180">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="cd718-181">alapértelmezett \_ cím</span><span class="sxs-lookup"><span data-stu-id="cd718-181">default\_address</span></span> | [<span data-ttu-id="cd718-182">Cím</span><span class="sxs-lookup"><span data-stu-id="cd718-182">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="cd718-183">Igen</span><span class="sxs-lookup"><span data-stu-id="cd718-183">Yes</span></span>      | <span data-ttu-id="cd718-184">Az ügyfél vállalatának/szervezetének regisztrált címe.</span><span class="sxs-lookup"><span data-stu-id="cd718-184">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="cd718-185">A [hosszkorlátozásokkal](utility-resources.md#address) kapcsolatos információkért tekintse meg a Cím erőforrást.</span><span class="sxs-lookup"><span data-stu-id="cd718-185">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="cd718-186">Vállalati profil</span><span class="sxs-lookup"><span data-stu-id="cd718-186">Company profile</span></span>

<span data-ttu-id="cd718-187">Ez a táblázat az új ügyfél létrehozásához szükséges Minimálisan szükséges mezőket ismerteti a [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) erőforrásból.</span><span class="sxs-lookup"><span data-stu-id="cd718-187">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="cd718-188">Név</span><span class="sxs-lookup"><span data-stu-id="cd718-188">Name</span></span>   | <span data-ttu-id="cd718-189">Típus</span><span class="sxs-lookup"><span data-stu-id="cd718-189">Type</span></span>   | <span data-ttu-id="cd718-190">Kötelező</span><span class="sxs-lookup"><span data-stu-id="cd718-190">Required</span></span> | <span data-ttu-id="cd718-191">Leírás</span><span class="sxs-lookup"><span data-stu-id="cd718-191">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="cd718-192">domain</span><span class="sxs-lookup"><span data-stu-id="cd718-192">domain</span></span> | <span data-ttu-id="cd718-193">sztring</span><span class="sxs-lookup"><span data-stu-id="cd718-193">string</span></span> | <span data-ttu-id="cd718-194">Igen</span><span class="sxs-lookup"><span data-stu-id="cd718-194">Yes</span></span>     | <span data-ttu-id="cd718-195">Az ügyfél tartományneve, például contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="cd718-195">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="cd718-196">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="cd718-196">organizationRegistrationNumber</span></span> | <span data-ttu-id="cd718-197">sztring</span><span class="sxs-lookup"><span data-stu-id="cd718-197">string</span></span> | <span data-ttu-id="cd718-198">Feltételtől függ</span><span class="sxs-lookup"><span data-stu-id="cd718-198">Depends on condition</span></span> | <span data-ttu-id="cd718-199">Az ügyfél szervezeti regisztrációs száma (más néven az INN-szám bizonyos országokban).</span><span class="sxs-lookup"><span data-stu-id="cd718-199">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="cd718-200">A mező kitöltése csak akkor szükséges, ha az ügyfél vállalata/szervezete a következő országokban található:</span><span class="sxs-lookup"><span data-stu-id="cd718-200">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="cd718-201">- Brazília (AM)</span><span class="sxs-lookup"><span data-stu-id="cd718-201">- Armenia (AM)</span></span> <br/><span data-ttu-id="cd718-202">- Egyesült Államok (AZ)</span><span class="sxs-lookup"><span data-stu-id="cd718-202">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="cd718-203">- Majd (BY)</span><span class="sxs-lookup"><span data-stu-id="cd718-203">- Belarus (BY)</span></span><br/><span data-ttu-id="cd718-204">- Magyar (Hu)</span><span class="sxs-lookup"><span data-stu-id="cd718-204">- Hungary (HU)</span></span><br/><span data-ttu-id="cd718-205">- Észak-India (KZ)</span><span class="sxs-lookup"><span data-stu-id="cd718-205">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="cd718-206">- Kirgizisztán (KG)</span><span class="sxs-lookup"><span data-stu-id="cd718-206">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="cd718-207">- Majd (MD)</span><span class="sxs-lookup"><span data-stu-id="cd718-207">- Moldova (MD)</span></span><br/><span data-ttu-id="cd718-208">- Oroszország (RU)</span><span class="sxs-lookup"><span data-stu-id="cd718-208">- Russia (RU)</span></span><br/><span data-ttu-id="cd718-209">- Tádzsikisztán (TJ)</span><span class="sxs-lookup"><span data-stu-id="cd718-209">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="cd718-210">- Uzbekistan (UZ)</span><span class="sxs-lookup"><span data-stu-id="cd718-210">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="cd718-211">- Egyesült Arab Emírségek</span><span class="sxs-lookup"><span data-stu-id="cd718-211">- Ukraine (UA)</span></span><br/><span data-ttu-id="cd718-212">- India</span><span class="sxs-lookup"><span data-stu-id="cd718-212">- India</span></span> <br/><span data-ttu-id="cd718-213">- Brazília</span><span class="sxs-lookup"><span data-stu-id="cd718-213">- Brazil</span></span> <br/><span data-ttu-id="cd718-214">- Dél-Afrika</span><span class="sxs-lookup"><span data-stu-id="cd718-214">- South Africa</span></span> <br/><span data-ttu-id="cd718-215">– Nagy-Franciaország</span><span class="sxs-lookup"><span data-stu-id="cd718-215">- Poland</span></span> <br/><span data-ttu-id="cd718-216">- Egyesült Arab Emírségek</span><span class="sxs-lookup"><span data-stu-id="cd718-216">- United Arab Emirates</span></span> <br/><span data-ttu-id="cd718-217">- Dél-Arábia</span><span class="sxs-lookup"><span data-stu-id="cd718-217">- Saudi Arabia</span></span> <br/><span data-ttu-id="cd718-218">– Ország</span><span class="sxs-lookup"><span data-stu-id="cd718-218">- Turkey</span></span> <br/><span data-ttu-id="cd718-219">– Nagy-Ausztrália</span><span class="sxs-lookup"><span data-stu-id="cd718-219">- Thailand</span></span> <br/><span data-ttu-id="cd718-220">- Vietnam</span><span class="sxs-lookup"><span data-stu-id="cd718-220">- Vietnam</span></span> <br/><span data-ttu-id="cd718-221">– Fogaras</span><span class="sxs-lookup"><span data-stu-id="cd718-221">- Myanmar</span></span> <br/><span data-ttu-id="cd718-222">– Szkent</span><span class="sxs-lookup"><span data-stu-id="cd718-222">- Iraq</span></span> <br/><span data-ttu-id="cd718-223">- Dél-Dél-Korea</span><span class="sxs-lookup"><span data-stu-id="cd718-223">- South Sudan</span></span> <br/><span data-ttu-id="cd718-224">– Egyesült Egyesült Állam</span><span class="sxs-lookup"><span data-stu-id="cd718-224">- Venezuela</span></span><br/> <br/><span data-ttu-id="cd718-225">Az ügyfél más országokban található vállalata/szervezete esetében ez egy nem kötelező mező.</span><span class="sxs-lookup"><span data-stu-id="cd718-225">For customer’s company/organization located in other countries, this is an optional field.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="cd718-226">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="cd718-226">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="cd718-227">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="cd718-227">REST response</span></span>

<span data-ttu-id="cd718-228">Ha a válasz sikeres, akkor tartalmazza az [új](customer-resources.md#customer) ügyfél ügyfélerőforrását.</span><span class="sxs-lookup"><span data-stu-id="cd718-228">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cd718-229">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="cd718-229">Response success and error codes</span></span>

<span data-ttu-id="cd718-230">A válaszokhoz egy HTTP-állapotkód is szükséges, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="cd718-230">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cd718-231">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="cd718-231">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cd718-232">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="cd718-232">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cd718-233">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="cd718-233">Response example</span></span>

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