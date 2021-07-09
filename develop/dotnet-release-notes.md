---
title: Partnerközpont .NET SDK kibocsátási megjegyzései
description: Az Partnerközpont .NET SDK legújabb verziójának kibocsátási megjegyzései.
ms.date: 07/07/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1532d48c00550f5eb437ed0164d6a1f7bb340dd
ms.sourcegitcommit: 53c94db33b09c30e762b842c4275b2b531dba932
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/09/2021
ms.locfileid: "113522634"
---
# <a name="net-sdk-release-notes"></a><span data-ttu-id="a9157-103">A .NET SDK kibocsátási megjegyzései</span><span class="sxs-lookup"><span data-stu-id="a9157-103">.NET SDK release notes</span></span>

<span data-ttu-id="a9157-104">Az alábbi kibocsátási megjegyzések a Microsoft Partnerközpont .NET SDK új [verzióihoz érhetők el.](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)</span><span class="sxs-lookup"><span data-stu-id="a9157-104">The following release notes are available for new versions of [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter).</span></span> <span data-ttu-id="a9157-105">A [.NET SDK-mintákat a GitHub.](https://github.com/Microsoft/Partner-Center-DotNet-Samples)</span><span class="sxs-lookup"><span data-stu-id="a9157-105">You can find [.NET SDK samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) on GitHub.</span></span> <span data-ttu-id="a9157-106">A [.NET API Partnerközpont .NET API-referencia a](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) .NET API-böngészőben található.</span><span class="sxs-lookup"><span data-stu-id="a9157-106">You can find the [Partner Center .NET API reference](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) in the .NET API Browser.</span></span>

## <a name="version-201"></a><span data-ttu-id="a9157-107">2.0.1-es verzió</span><span class="sxs-lookup"><span data-stu-id="a9157-107">Version 2.0.1</span></span>

<span data-ttu-id="a9157-108">[A Microsoft Partnerközpont .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 mostantól általánosan elérhető.</span><span class="sxs-lookup"><span data-stu-id="a9157-108">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 is now general availability.</span></span> <span data-ttu-id="a9157-109">Frissített [GitHub minták is](https://github.com/Microsoft/Partner-Center-DotNet-Samples) elérhetők.</span><span class="sxs-lookup"><span data-stu-id="a9157-109">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="a9157-110">Ebben a verzióban a következő módosítások szerepelnek:</span><span class="sxs-lookup"><span data-stu-id="a9157-110">The following changes are included in this version:</span></span>

> [!NOTE]
> <span data-ttu-id="a9157-111">Az új kereskedelmi élmények ("NCE") részeként bevezetett módosítások némelyike, amelyek jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesz partnerek meghívása alapján érhetők el.</span><span class="sxs-lookup"><span data-stu-id="a9157-111">Some of changes introduced as part of New Commerce Experiences (“NCE”) which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span> <span data-ttu-id="a9157-112">Azok a partnerek, akik nem részei az Új kereskedelmi privát előzetes verziónak, nem láthatják a hatásokat, és visszamenőlegesen kompatibilisnek kell lenniük.</span><span class="sxs-lookup"><span data-stu-id="a9157-112">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>

### <a name="common"></a><span data-ttu-id="a9157-113">Közös</span><span class="sxs-lookup"><span data-stu-id="a9157-113">Common</span></span>
* <span data-ttu-id="a9157-114">A hitelesítési kódtárra való hivatkozás módosítása – A hivatkozás Azure Active Directory Authentication Library[(ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)és a Microsoft Authentication Library ([MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)) között</span><span class="sxs-lookup"><span data-stu-id="a9157-114">Change on the reference to authentication library – The reference is changed from Azure Active Directory Authentication Library ([ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)) to Microsoft Authentication Library ([MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet))</span></span>

  <span data-ttu-id="a9157-115">A következő módosításokat kell eszközlni annak biztosításához, hogy az MSAL megfelelően fut az alkalmazáson vagy a .NET-mintán:</span><span class="sxs-lookup"><span data-stu-id="a9157-115">Following changes should be made to ensure MSAL runs correctly on your application or .NET sample:</span></span>

  * <span data-ttu-id="a9157-116">Hozzáadás `https://login.microsoftonline.com/common/oauth2/nativeclient` RedirectUrl-ként mobil- és asztali alkalmazásokhoz</span><span class="sxs-lookup"><span data-stu-id="a9157-116">Add `https://login.microsoftonline.com/common/oauth2/nativeclient` as RedirectUrl for Mobile and desktop applications</span></span>
  * <span data-ttu-id="a9157-117">Adja **hozzá a Tartományt** az alkalmazáskonfigurációs fájl UserAuthentication szakaszához.</span><span class="sxs-lookup"><span data-stu-id="a9157-117">Add **Domain** into UserAuthentication section in your application configuration file.</span></span> 

    <span data-ttu-id="a9157-118">A tartomány az a Azure Active Directory vagy bérlőazonosító, ahol az Azure AD-alkalmazást létrehozták</span><span class="sxs-lookup"><span data-stu-id="a9157-118">Domain is the Azure Active Directory domain or tenant ID where the Azure AD application was created</span></span>

* <span data-ttu-id="a9157-119">[Hibakódok](error-codes.md) – Új hibakód hozzáadva</span><span class="sxs-lookup"><span data-stu-id="a9157-119">[Error codes](error-codes.md) – New error code added</span></span> 
  * <span data-ttu-id="a9157-120">408: Kérés időtúllépése</span><span class="sxs-lookup"><span data-stu-id="a9157-120">408: Request timeout</span></span>
  * <span data-ttu-id="a9157-121">504: Átjáró időtúllépése</span><span class="sxs-lookup"><span data-stu-id="a9157-121">504: Gateway timeout</span></span> 

### <a name="manage-billing"></a><span data-ttu-id="a9157-122">Számlázás kezelése</span><span class="sxs-lookup"><span data-stu-id="a9157-122">Manage billing</span></span>

* <span data-ttu-id="a9157-123">[Számlasorelemek](get-invoiceline-items.md) – új attribútumok hozzáadva a következő API-khoz:</span><span class="sxs-lookup"><span data-stu-id="a9157-123">[Invoice line-items](get-invoiceline-items.md) - new attributes added to following APIs:</span></span>
  * `GET /invoices/{invoice-id}/lineitems?provider={provider}&invoicelineitemtype=billinglineitems`
  * `GET /invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems`

  <span data-ttu-id="a9157-124">Új attribútumok:</span><span class="sxs-lookup"><span data-stu-id="a9157-124">New attributes:</span></span> 
  * <span data-ttu-id="a9157-125">productQualifiers</span><span class="sxs-lookup"><span data-stu-id="a9157-125">productQualifiers</span></span>
  * <span data-ttu-id="a9157-126">subscriptionStartDate</span><span class="sxs-lookup"><span data-stu-id="a9157-126">subscriptionStartDate</span></span>
  * <span data-ttu-id="a9157-127">subscriptionEndDate</span><span class="sxs-lookup"><span data-stu-id="a9157-127">subscriptionEndDate</span></span>
  * <span data-ttu-id="a9157-128">referenceId (referenciaazonosító)</span><span class="sxs-lookup"><span data-stu-id="a9157-128">referenceId</span></span>
  * <span data-ttu-id="a9157-129">creditReasonCode (csak az NCE-re vonatkozik)</span><span class="sxs-lookup"><span data-stu-id="a9157-129">creditReasonCode  (Only applicable to NCE)</span></span>
  * <span data-ttu-id="a9157-130">promotionId (előléptetésazonosító)</span><span class="sxs-lookup"><span data-stu-id="a9157-130">promotionId</span></span> 


* <span data-ttu-id="a9157-131">[Napi minősítésű használat Sorelemek](get-invoice-billed-consumption-lineitems.md) – új attribútumok hozzáadva a következő API-hoz:</span><span class="sxs-lookup"><span data-stu-id="a9157-131">[Daily rated usage Line-items](get-invoice-billed-consumption-lineitems.md) – new attributes added to following API:</span></span> 
  * `GET /invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems`
  
  <span data-ttu-id="a9157-132">Új attribútumok:</span><span class="sxs-lookup"><span data-stu-id="a9157-132">New attributes:</span></span> 
  * <span data-ttu-id="a9157-133">hasPartnerEarnedCredit (csak az NCE-re vonatkozik)</span><span class="sxs-lookup"><span data-stu-id="a9157-133">hasPartnerEarnedCredit (Only applicable to NCE)</span></span>
  * <span data-ttu-id="a9157-134">creditType (csak az NCE-hez alkalmazható)</span><span class="sxs-lookup"><span data-stu-id="a9157-134">creditType (Only applicable to NCE)</span></span>
  * <span data-ttu-id="a9157-135">rateOfCredit (csak az NCE-hez alkalmazható)</span><span class="sxs-lookup"><span data-stu-id="a9157-135">rateOfCredit (Only applicable to NCE)</span></span>


### <a name="manage-orders"></a><span data-ttu-id="a9157-136">Megrendelések kezelése</span><span class="sxs-lookup"><span data-stu-id="a9157-136">Manage orders</span></span>

* <span data-ttu-id="a9157-137">[Előfizetési erőforrások](subscription-resources.md) – Új tulajdonság hozzáadva.</span><span class="sxs-lookup"><span data-stu-id="a9157-137">[Subscription Resources](subscription-resources.md) – New property added.</span></span> 
  * <span data-ttu-id="a9157-138">CancellationAllowedUntilDate – (csak az NCE-hez alkalmazható)</span><span class="sxs-lookup"><span data-stu-id="a9157-138">CancellationAllowedUntilDate  - (Only applicable to NCE)</span></span>

* <span data-ttu-id="a9157-139">Erőforrások váltása (csak az NCE-hez alkalmazható) – Új tulajdonság hozzáadva</span><span class="sxs-lookup"><span data-stu-id="a9157-139">Transition Resources (Only applicable to NCE) – New property added</span></span> 
  * <span data-ttu-id="a9157-140">FromSubscriptionId (Előíróazonosító)</span><span class="sxs-lookup"><span data-stu-id="a9157-140">FromSubscriptionId</span></span>

### <a name="manage-customer-accounts"></a><span data-ttu-id="a9157-141">Ügyfélfiókok kezelése</span><span class="sxs-lookup"><span data-stu-id="a9157-141">Manage customer accounts</span></span>

* <span data-ttu-id="a9157-142">[Cím ellenőrzése](validate-an-address.md) – A válasz logikairól új API-modellre módosul:</span><span class="sxs-lookup"><span data-stu-id="a9157-142">[Validate an address](validate-an-address.md) – Response is changed from a Boolean to a new model for API:</span></span>
  * `POST /validations/address`
  
  <span data-ttu-id="a9157-143">Új válaszmodell:</span><span class="sxs-lookup"><span data-stu-id="a9157-143">New response model:</span></span> 
  * <span data-ttu-id="a9157-144">AddressValidationResponse</span><span class="sxs-lookup"><span data-stu-id="a9157-144">AddressValidationResponse</span></span>

* <span data-ttu-id="a9157-145">Az ügyfél minősítési szinkron API-ja elavult.</span><span class="sxs-lookup"><span data-stu-id="a9157-145">Customer’s qualification synchronous API is deprecated.</span></span>  


## <a name="version-1170"></a><span data-ttu-id="a9157-146">1.17.0-s verzió</span><span class="sxs-lookup"><span data-stu-id="a9157-146">Version 1.17.0</span></span>

<span data-ttu-id="a9157-147">[A Microsoft Partnerközpont .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) 1.17.0-s verziója általánosan elérhető.</span><span class="sxs-lookup"><span data-stu-id="a9157-147">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 is now general availability.</span></span> <span data-ttu-id="a9157-148">Frissített [GitHub minták is](https://github.com/Microsoft/Partner-Center-DotNet-Samples) elérhetők.</span><span class="sxs-lookup"><span data-stu-id="a9157-148">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="a9157-149">Ebben a verzióban a következő módosítások szerepelnek:</span><span class="sxs-lookup"><span data-stu-id="a9157-149">The following changes are included in this version:</span></span>

* <span data-ttu-id="a9157-150">Napló frissítve – Új művelettípusok hozzáadva annak tudatában, hogy az ügyfél mikor hagyta jóvá és szüntette meg a DAP-t</span><span class="sxs-lookup"><span data-stu-id="a9157-150">Audit Updated - Added new operation types for knowing when the customer approved and terminated DAP</span></span>
  * [<span data-ttu-id="a9157-151">DapAdminRelationshipApproved</span><span class="sxs-lookup"><span data-stu-id="a9157-151">DapAdminRelationshipApproved</span></span>](auditing-resources.md)
  * [<span data-ttu-id="a9157-152">DapAdminRelationshipTerminated</span><span class="sxs-lookup"><span data-stu-id="a9157-152">DapAdminRelationshipTerminated</span></span>](auditing-resources.md)

* <span data-ttu-id="a9157-153">Napló frissítve – Új erőforrás- és művelettípusok hozzáadva az ügyfél címtárszerepkör-forgatókönyvének támogatásához</span><span class="sxs-lookup"><span data-stu-id="a9157-153">Audit Updated – Added new resource and operation types for supporting the customer directory role scenario</span></span>
  * <span data-ttu-id="a9157-154">Erőforrástípus:[CustomerDirectoryRole](auditing-resources.md)</span><span class="sxs-lookup"><span data-stu-id="a9157-154">Resource type "[CustomerDirectoryRole](auditing-resources.md)"</span></span>
  * <span data-ttu-id="a9157-155">Az["AddUserMember"](auditing-resources.md)és a "[RemoveUserMember" művelettípusok](auditing-resources.md)</span><span class="sxs-lookup"><span data-stu-id="a9157-155">Operation types "[AddUserMember](auditing-resources.md)" and "[RemoveUserMember](auditing-resources.md)"</span></span>

* <span data-ttu-id="a9157-156">SDK-frissítések az ügyfelek fiókjához – A következő API-k támogatása</span><span class="sxs-lookup"><span data-stu-id="a9157-156">SDK Updates to Customers Account - Support for following API's</span></span>
  * <span data-ttu-id="a9157-157">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="a9157-157">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span></span>
  * <span data-ttu-id="a9157-158">GET /customers/{customer-tenant-id}/qualifications</span><span class="sxs-lookup"><span data-stu-id="a9157-158">GET /customers/{customer-tenant-id}/qualifications</span></span> 
  * <span data-ttu-id="a9157-159">POST /customers/{customer_id}/qualifications?code={validationCode}</span><span class="sxs-lookup"><span data-stu-id="a9157-159">POST /customers/{customer_id}/qualifications?code={validationCode}</span></span>

* <span data-ttu-id="a9157-160">**Az új kereskedelem részeként bevezetett módosításokat, amelyek jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesző partnerek meghívása alapján érhetők el.**</span><span class="sxs-lookup"><span data-stu-id="a9157-160">**Following changes introduced as part of New Commerce which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.**</span></span> <span data-ttu-id="a9157-161">Azok a partnerek, akik nem részei az Új kereskedelmi privát előzetes verziónak, nem láthatják a hatásokat, és visszamenőlegesen kompatibilisnek kell lenniük.</span><span class="sxs-lookup"><span data-stu-id="a9157-161">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>
  * <span data-ttu-id="a9157-162">Katalógusváltozások:</span><span class="sxs-lookup"><span data-stu-id="a9157-162">Catalog Changes:</span></span>
    * <span data-ttu-id="a9157-163">GET /products/{termékazonosító}/skus/{sku-id}</span><span class="sxs-lookup"><span data-stu-id="a9157-163">GET /products/{product-id}/skus/{sku-id}</span></span>
  * <span data-ttu-id="a9157-164">Vásárlás és kezelés:</span><span class="sxs-lookup"><span data-stu-id="a9157-164">Purchase and Manage:</span></span>
    * <span data-ttu-id="a9157-165">GET /customers/{customerId}/subscriptions</span><span class="sxs-lookup"><span data-stu-id="a9157-165">GET /customers/{customerId}/subscriptions</span></span>
    * <span data-ttu-id="a9157-166">GET /customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="a9157-166">GET /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="a9157-167">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="a9157-167">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="a9157-168">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span><span class="sxs-lookup"><span data-stu-id="a9157-168">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span></span>
    * <span data-ttu-id="a9157-169">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="a9157-169">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>
    * <span data-ttu-id="a9157-170">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="a9157-170">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>


## <a name="version-1163"></a><span data-ttu-id="a9157-171">1.16.3-as verzió</span><span class="sxs-lookup"><span data-stu-id="a9157-171">Version 1.16.3</span></span>

<span data-ttu-id="a9157-172">[A Microsoft Partnerközpont .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) 1.16.3-as verziója általánosan elérhető.</span><span class="sxs-lookup"><span data-stu-id="a9157-172">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 is now general availability.</span></span> <span data-ttu-id="a9157-173">Frissített [GitHub minták is](https://github.com/Microsoft/Partner-Center-DotNet-Samples) elérhetők.</span><span class="sxs-lookup"><span data-stu-id="a9157-173">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="a9157-174">Ebben a verzióban a következő módosítások szerepelnek:</span><span class="sxs-lookup"><span data-stu-id="a9157-174">The following changes are included in this version:</span></span>

* <span data-ttu-id="a9157-175">SelfServePolicies – új funkciók hozzáadva</span><span class="sxs-lookup"><span data-stu-id="a9157-175">SelfServePolicies - new functionality added</span></span>
  * [<span data-ttu-id="a9157-176">GetSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="a9157-176">GetSelfServePolicies</span></span>](get-a-self-serve-policy-by-id.md)
  * [<span data-ttu-id="a9157-177">GetListOfSelfServicePolicies</span><span class="sxs-lookup"><span data-stu-id="a9157-177">GetListOfSelfServicePolicies</span></span>](get-a-list-of-self-serve-policies.md)
  * [<span data-ttu-id="a9157-178">CreateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="a9157-178">CreateSelfServePolicies</span></span>](create-a-self-serve-policy.md)
  * [<span data-ttu-id="a9157-179">UpdateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="a9157-179">UpdateSelfServePolicies</span></span>](update-a-self-serve-policy.md)
  * [<span data-ttu-id="a9157-180">DeleteSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="a9157-180">DeleteSelfServePolicies</span></span>](delete-a-self-serve-policy.md)

* <span data-ttu-id="a9157-181">Ügyfelek vállalati profilja</span><span class="sxs-lookup"><span data-stu-id="a9157-181">Customers Company Profile</span></span>
  * <span data-ttu-id="a9157-182">[OrganizationRegistrationNumber hozzáadva](create-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="a9157-182">Added [OrganizationRegistrationNumber](create-a-customer.md)</span></span>

* <span data-ttu-id="a9157-183">CustomerBillingProfile.DefaultAddress</span><span class="sxs-lookup"><span data-stu-id="a9157-183">CustomerBillingProfile.DefaultAddress</span></span>
  * <span data-ttu-id="a9157-184">MiddleName hozzáadva</span><span class="sxs-lookup"><span data-stu-id="a9157-184">Added MiddleName</span></span>

## <a name="version-1162"></a><span data-ttu-id="a9157-185">1.16.2-es verzió</span><span class="sxs-lookup"><span data-stu-id="a9157-185">Version 1.16.2</span></span>

<span data-ttu-id="a9157-186">[A Microsoft Partnerközpont .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 mostantól általánosan elérhető.</span><span class="sxs-lookup"><span data-stu-id="a9157-186">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 is now general availability.</span></span> <span data-ttu-id="a9157-187">Frissített [GitHub minták is](https://github.com/Microsoft/Partner-Center-DotNet-Samples) elérhetők.</span><span class="sxs-lookup"><span data-stu-id="a9157-187">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="a9157-188">Ebben a verzióban a következő módosítások szerepelnek:</span><span class="sxs-lookup"><span data-stu-id="a9157-188">The following changes are included in this version:</span></span>

* <span data-ttu-id="a9157-189">Frissítse a naplórekord támogatott művelettípusát.</span><span class="sxs-lookup"><span data-stu-id="a9157-189">Update supported operation types for Audit Record.</span></span> <span data-ttu-id="a9157-190">Az újonnan hozzáadottak a következőek:</span><span class="sxs-lookup"><span data-stu-id="a9157-190">The newly added ones are:</span></span>
  * <span data-ttu-id="a9157-191">CreateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="a9157-191">CreateSelfServePolicy</span></span>
  * <span data-ttu-id="a9157-192">UpdateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="a9157-192">UpdateSelfServePolicy</span></span>
  * <span data-ttu-id="a9157-193">DeleteSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="a9157-193">DeleteSelfServePolicy</span></span>
  * <span data-ttu-id="a9157-194">RemovePartnerRelationship (Partnerreláció eltávolítása)</span><span class="sxs-lookup"><span data-stu-id="a9157-194">RemovePartnerRelationship</span></span>
  * <span data-ttu-id="a9157-195">DeleteTipCustomer (TipCustomer törlése)</span><span class="sxs-lookup"><span data-stu-id="a9157-195">DeleteTipCustomer</span></span>
  * <span data-ttu-id="a9157-196">CreateRelatedReferral (RelatedReferral létrehozása)</span><span class="sxs-lookup"><span data-stu-id="a9157-196">CreateRelatedReferral</span></span>
  * <span data-ttu-id="a9157-197">UpdateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="a9157-197">UpdateRelatedReferral</span></span>

* <span data-ttu-id="a9157-198">A szolgáltatáskérés létrehozása elavult</span><span class="sxs-lookup"><span data-stu-id="a9157-198">Service request creation is now deprecated</span></span>
* <span data-ttu-id="a9157-199">A támogatási témakörök elavultak</span><span class="sxs-lookup"><span data-stu-id="a9157-199">Support topics are now deprecated</span></span>


## <a name="version-1161"></a><span data-ttu-id="a9157-200">1.16.1-es verzió</span><span class="sxs-lookup"><span data-stu-id="a9157-200">Version 1.16.1</span></span>

<span data-ttu-id="a9157-201">[A Microsoft Partnerközpont .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) 1.16.1-es verziója mostantól általánosan elérhető.</span><span class="sxs-lookup"><span data-stu-id="a9157-201">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v1.16.1 is now general availability.</span></span> <span data-ttu-id="a9157-202">A [GitHub minták is](https://github.com/Microsoft/Partner-Center-DotNet-Samples) elérhetők.</span><span class="sxs-lookup"><span data-stu-id="a9157-202">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="a9157-203">Ebben a verzióban a következő módosítások szerepelnek:</span><span class="sxs-lookup"><span data-stu-id="a9157-203">The following changes are included in this version:</span></span>

<span data-ttu-id="a9157-204">A meglévő Microsoft-Partnerközpont SDK a .NET-keretrendszer .NET Standard 2.0 platformra.</span><span class="sxs-lookup"><span data-stu-id="a9157-204">We have migrated the existing Microsoft Partner Center SDK from .NET Framework to .NET Standard 2.0 platform.</span></span> <span data-ttu-id="a9157-205">Így az SDK kompatibilis lesz a meglévő alkalmazásokkal a .NET-keretrendszer 4.6.1-es és korábbi verziók használatával.</span><span class="sxs-lookup"><span data-stu-id="a9157-205">This will make the SDK compatible with existing applications using .NET Framework 4.6.1 and above.</span></span> <span data-ttu-id="a9157-206">Az SDK támogatni fogja a .NET Core 2.0-s és magasabb verzióját.</span><span class="sxs-lookup"><span data-stu-id="a9157-206">The SDK will support .NET Core 2.0 and above.</span></span> <span data-ttu-id="a9157-207">A [meglévő alkalmazásokba való](/dotnet/standard/net-standard) portolás előtt ellenőrizze a .NET-megvalósítás támogatását.</span><span class="sxs-lookup"><span data-stu-id="a9157-207">Check [.NET implementation support](/dotnet/standard/net-standard) before porting it to existing applications.</span></span>   


## <a name="version-1153"></a><span data-ttu-id="a9157-208">1.15.3-as verzió</span><span class="sxs-lookup"><span data-stu-id="a9157-208">Version 1.15.3</span></span>
<span data-ttu-id="a9157-209">[A Microsoft Partnerközpont .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) 1.15.3-as verziója mostantól általánosan elérhető.</span><span class="sxs-lookup"><span data-stu-id="a9157-209">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v1.15.3 is now general availability.</span></span> <span data-ttu-id="a9157-210">Frissített REST API-k [és GitHub minták](https://github.com/Microsoft/Partner-Center-DotNet-Samples) is elérhetők.</span><span class="sxs-lookup"><span data-stu-id="a9157-210">Updated REST APIs and [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="a9157-211">Ebben a verzióban a következő módosítások szerepelnek:</span><span class="sxs-lookup"><span data-stu-id="a9157-211">The following changes are included in this version:</span></span>

* <span data-ttu-id="a9157-212">Partnerszerződés</span><span class="sxs-lookup"><span data-stu-id="a9157-212">Partner Agreement</span></span>
  * <span data-ttu-id="a9157-213">A közvetett szolgáltatók már képesek ellenőrizni [Microsoft Partnerszerződés közvetett](verify-indirect-reseller-mpa-status.md)viszonteladók állapotát.</span><span class="sxs-lookup"><span data-stu-id="a9157-213">Added the ability for indirect providers to [verify Microsoft Partner Agreement status of indirect resellers](verify-indirect-reseller-mpa-status.md).</span></span>
* <span data-ttu-id="a9157-214">Termékek</span><span class="sxs-lookup"><span data-stu-id="a9157-214">Products</span></span>
  * <span data-ttu-id="a9157-215">Az alábbi két felület helytelenül került a Microsoft.Store.PartnerCenter.Products névtérbe.</span><span class="sxs-lookup"><span data-stu-id="a9157-215">The following two interfaces were incorrectly placed under the Microsoft.Store.PartnerCenter.Products namespace.</span></span> <span data-ttu-id="a9157-216">Ezek most a Microsoft.Store.PartnerCenter.Customers.Products névtér alatt találhatók.</span><span class="sxs-lookup"><span data-stu-id="a9157-216">Now, they are located under the Microsoft.Store.PartnerCenter.Customers.Products namespace.</span></span>
    * <span data-ttu-id="a9157-217">ICustomerProductByReservationScope</span><span class="sxs-lookup"><span data-stu-id="a9157-217">ICustomerProductByReservationScope</span></span>
    * <span data-ttu-id="a9157-218">ICustomerSkuByReservationScope</span><span class="sxs-lookup"><span data-stu-id="a9157-218">ICustomerSkuByReservationScope</span></span>
