---
title: Partnerközpont .NET SDK kibocsátási megjegyzései
description: Az Partnerközpont .NET SDK legújabb verziójának kibocsátási megjegyzései.
ms.date: 07/07/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6fc6182638cb2cc5457bdfada37b928c88e1ca786e401f7eb8d5309a0abd9310
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991222"
---
# <a name="net-sdk-release-notes"></a>A .NET SDK kibocsátási megjegyzései

Az alábbi kibocsátási megjegyzések a Microsoft Partnerközpont .NET SDK új [verzióihoz érhetők el.](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter) A [.NET SDK-mintákat a](https://github.com/Microsoft/Partner-Center-DotNet-Samples) GitHub. A [.NET API Partnerközpont .NET API-referenciát a](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) .NET API-böngészőben találja.

## <a name="version-201"></a>2.0.1-es verzió

[A Microsoft Partnerközpont .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) 2.0.1-es verziója mostantól általánosan elérhető. A [GitHub minták is](https://github.com/Microsoft/Partner-Center-DotNet-Samples) elérhetők. Ebben a verzióban a következő módosítások szerepelnek:

> [!NOTE]
> Az új kereskedelmi élmények ("NCE") részeként bevezetett módosítások némelyike, amelyek jelenleg csak az M365/D365 új kereskedelmi élmény technikai előzetes kiadásának partnereinek szóló meghívón alapulnak. Azok a partnerek, akik nem részei az Új kereskedelmi privát előzetes verziónak, nem láthatják a hatásokat, és visszamenőlegesen kompatibilisnek kell lenniük.

### <a name="common"></a>Közös
* A hitelesítési kódtárra való hivatkozás módosítása – A hivatkozás Azure Active Directory Authentication Library[(ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)és a Microsoft Authentication Library ([MSAL)](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)között

  A következő módosításokat kell eszközlni annak érdekében, hogy az MSAL megfelelően fut az alkalmazáson vagy a .NET-mintán:

  * Hozzáadás `https://login.microsoftonline.com/common/oauth2/nativeclient` RedirectUrl-ként mobil- és asztali alkalmazásokhoz
  * Adja **hozzá a Tartományt** az alkalmazáskonfigurációs fájl UserAuthentication szakaszához. 

    A tartomány az Azure Active Directory tartomány vagy bérlő azonosítója, ahol az Azure AD-alkalmazást létrehozták

* [Hibakódok](error-codes.md) – Új hibakód hozzáadva 
  * 408: Kérés időtúllépése
  * 504: Átjáró időtúllépése 

### <a name="manage-billing"></a>Számlázás kezelése

* [Számlasorelemek](get-invoiceline-items.md) – új attribútumok hozzáadva a következő API-khoz:
  * `GET /invoices/{invoice-id}/lineitems?provider={provider}&invoicelineitemtype=billinglineitems`
  * `GET /invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems`

  Új attribútumok: 
  * productQualifiers
  * subscriptionStartDate (Előfizetés kezdődátum)
  * subscriptionEndDate
  * referenceId (referenciaazonosító)
  * creditReasonCode (csak az NCE-re vonatkozik)
  * promotionId (előléptetésazonosító) 


* [Napi névleges használat Sorelemek](get-invoice-billed-consumption-lineitems.md) – új attribútumok hozzáadva a következő API-hoz: 
  * `GET /invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems`
  
  Új attribútumok: 
  * hasPartnerEarnedCredit (csak az NCE-re vonatkozik)
  * creditType (csak az NCE-hez alkalmazható)
  * rateOfCredit (csak az NCE-hez alkalmazható)


### <a name="manage-orders"></a>Megrendelések kezelése

* [Előfizetési erőforrások](subscription-resources.md) – Új tulajdonság hozzáadva. 
  * CancellationAllowedUntilDate – (csak az NCE-hez alkalmazható)

* Erőforrások váltása (csak az NCE-hez alkalmazható) – Új tulajdonság hozzáadva 
  * FromSubscriptionId (Előíróazonosító)

### <a name="manage-customer-accounts"></a>Ügyfélfiókok kezelése

* [Cím ellenőrzése](validate-an-address.md) – A válasz logikairól új API-modellre változik:
  * `POST /validations/address`
  
  Új válaszmodell: 
  * AddressValidationResponse

* Az ügyfél minősítési szinkron API-ja elavult.  


## <a name="version-1170"></a>1.17.0-s verzió

[A Microsoft Partnerközpont .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) 1.17.0-s verziója mostantól általánosan elérhető. A [GitHub minták is](https://github.com/Microsoft/Partner-Center-DotNet-Samples) elérhetők. Ebben a verzióban a következő módosítások szerepelnek:

* Napló frissítve – Új művelettípusok hozzáadva annak tudatában, hogy az ügyfél mikor hagyta jóvá és szüntette meg a DAP-t
  * [DapAdminRelationshipApproved](auditing-resources.md)
  * [DapAdminRelationshipTerminated (DapAdminRelationshipTerminated)](auditing-resources.md)

* Napló frissítve – Új erőforrás- és művelettípusok hozzáadva az ügyfél címtárszerepkör-forgatókönyvének támogatásához
  * Erőforrástípus: "[CustomerDirectoryRole](auditing-resources.md)"
  * Művelettípusok: "[AddUserMember](auditing-resources.md)" és "[RemoveUserMember](auditing-resources.md)"

* Sdk-frissítések az ügyfélfiókhoz – A következő API-k támogatása
  * GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus
  * GET /customers/{customer-tenant-id}/qualifications 
  * POST /customers/{customer_id}/qualifications?code={validationCode}

* **Az új kereskedelem részeként bevezetett változások, amelyek jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesz partnerek meghívása alapján érhetők el.** Azok a partnerek, akik nem részei az Új kereskedelmi privát előzetes verziónak, nem láthatják a hatásokat, és visszamenőlegesen kompatibilisnek kell lenniük.
  * Katalógusváltozások:
    * GET /products/{termékazonosító}/skus/{sku-id}
  * Vásárlás és kezelés:
    * GET /customers/{customerId}/subscriptions
    * GET /customers/{customerId}/subscriptions/{subscriptionId}
    * PATCH /customers/{customerId}/subscriptions/{subscriptionId}
    * GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities
    * GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions
    * POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions


## <a name="version-1163"></a>1.16.3-as verzió

[A Microsoft Partnerközpont .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) 1.16.3-as verziója mostantól általánosan elérhető. A [GitHub minták is](https://github.com/Microsoft/Partner-Center-DotNet-Samples) elérhetők. Ebben a verzióban a következő módosítások szerepelnek:

* SelfServePolicies – új funkciók hozzáadva
  * [GetSelfServePolicies](get-a-self-serve-policy-by-id.md)
  * [GetListOfSelfServicePolicies](get-a-list-of-self-serve-policies.md)
  * [CreateSelfServePolicies](create-a-self-serve-policy.md)
  * [UpdateSelfServePolicies](update-a-self-serve-policy.md)
  * [DeleteSelfServePolicies](delete-a-self-serve-policy.md)

* Ügyfelek vállalati profilja
  * [OrganizationRegistrationNumber hozzáadva](create-a-customer.md)

* CustomerBillingProfile.DefaultAddress
  * MiddleName hozzáadva

## <a name="version-1162"></a>1.16.2-es verzió

[A Microsoft Partnerközpont .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) 1.16.2-es verziója mostantól általánosan elérhető. A [GitHub minták is](https://github.com/Microsoft/Partner-Center-DotNet-Samples) elérhetők. Ebben a verzióban a következő módosítások szerepelnek:

* Frissítse a naplórekord támogatott művelettípusát. Az újonnan hozzáadottak a következőek:
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship (Partnerreláció eltávolítása)
  * DeleteTipCustomer
  * CreateRelatedReferral (RelatedReferral létrehozása)
  * UpdateRelatedReferral

* A szolgáltatáskérés létrehozása elavult
* A támogatási témakörök elavultak


## <a name="version-1161"></a>1.16.1-es verzió

[A Microsoft Partnerközpont .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) 1.16.1-es verziója mostantól általánosan elérhető. A [GitHub minták is](https://github.com/Microsoft/Partner-Center-DotNet-Samples) elérhetők. Ebben a verzióban a következő módosítások szerepelnek:

A meglévő Microsoft-Partnerközpont SDK a .NET-keretrendszer .NET Standard 2.0 platformra. Így az SDK kompatibilis lesz a meglévő alkalmazásokkal a .NET-keretrendszer 4.6.1-es és korábbi verziók használatával. Az SDK támogatni fogja a .NET Core 2.0-s és magasabb verzióját. A [meglévő alkalmazásokba való](/dotnet/standard/net-standard) portolás előtt ellenőrizze a .NET-megvalósítás támogatását.   


## <a name="version-1153"></a>1.15.3-as verzió
[A Microsoft Partnerközpont .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) 1.15.3-as verziója mostantól általánosan elérhető. Frissített REST API-k [és GitHub minták](https://github.com/Microsoft/Partner-Center-DotNet-Samples) is elérhetők. Ebben a verzióban a következő módosítások szerepelnek:

* Partnerszerződés
  * A közvetett szolgáltatók már képesek ellenőrizni [Microsoft Partnerszerződés közvetett](verify-indirect-reseller-mpa-status.md)viszonteladók állapotát.
* Termékek
  * Az alábbi két felület helytelenül került a Microsoft.Store.PartnerCenter.Products névtérbe. Ezek most a Microsoft.Store.PartnerCenter.Customers.Products névtér alatt találhatók.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
