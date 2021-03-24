---
title: A partner Center .NET SDK kibocsátási megjegyzései
description: A partner Center .NET SDK legújabb verziójára vonatkozó kibocsátási megjegyzések.
ms.date: 09/18/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2fe309500cc80e962c101ad97f0712bef7e11eb3
ms.sourcegitcommit: f7fce0b35ab1579e59136abc357b71cf768b81b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/23/2021
ms.locfileid: "104895533"
---
# <a name="net-sdk-release-notes"></a>A .NET SDK kibocsátási megjegyzései

A következő kibocsátási megjegyzések a [Microsoft partner Center .net SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)új verzióihoz érhetők el. [.Net SDK-minták](https://github.com/Microsoft/Partner-Center-DotNet-Samples) a githubon találhatók. A [partner Center .NET API-referenciát](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) a .NET API-böngészőben találja.

## <a name="version-1170"></a>1.17.0 verziója

A [Microsoft partner Center .net SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v 1.17.0 mostantól általánosan elérhető. A frissített [GitHub-minták](https://github.com/Microsoft/Partner-Center-DotNet-Samples) is elérhetők. Ebben a verzióban a következő változások szerepelnek:

* Frissítve – új műveleti típusok hozzáadva, amelyekből megtudhatja, mikor hagyta jóvá és szakítja meg a DAP-t
  * [DapAdminRelationshipApproved](auditing-resources.md)
  * [DapAdminRelationshipTerminated](auditing-resources.md)

* Napló frissítve – új erőforrás-és műveleti típusok hozzáadása az ügyfél-címtár szerepkör-forgatókönyv támogatásához
  * "[CustomerDirectoryRole](auditing-resources.md)" erőforrástípus
  * A "[AddUserMember](auditing-resources.md)" és a "[RemoveUserMember](auditing-resources.md)" típusú műveletek

* SDK-frissítések az ügyfelek számlájához – támogatás a következő API-k számára
  * /Customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus beolvasása
  * /Customers/{Customer-Tenant-ID}/Qualifications beolvasása 
  * POST/Customers/{customer_id}/Qualifications? Code = {validationCode}

* **Az új kereskedelmi szolgáltatás részeként bevezetett változások a következők: a M365/D365 új kereskedelmi tapasztalattal foglalkozó partnereknek szóló meghívások alapján jelenleg elérhető partnerek.** Az új kereskedelmi privát előzetes verzió részét nem képező partnerek nem láthatják a hatásokat, és visszamenőlegesen kompatibilisnek kell lenniük.
  * Katalógus változásai:
    * /Products/{Product-ID}/SKUs/{SKU-ID} beolvasása
  * Vásárlás és kezelés:
    * /Customers/{customerId}/subscriptions beolvasása
    * /Customers/{customerId}/subscriptions/{subscriptionId} beolvasása
    * /Customers/{customerId}/subscriptions/{subscriptionId} javítása
    * /Customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities beolvasása
    * /Customers/{customerId}/subscriptions/{subscriptionId}/transitions beolvasása
    * /Customers/{customerId}/subscriptions/{subscriptionId}/transitions közzététele


## <a name="version-1163"></a>1.16.3 verziója

A [Microsoft partner Center .net SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v 1.16.3 mostantól általánosan elérhető. A frissített [GitHub-minták](https://github.com/Microsoft/Partner-Center-DotNet-Samples) is elérhetők. Ebben a verzióban a következő változások szerepelnek:

* SelfServePolicies – új funkciók hozzáadva
  * [GetSelfServePolicies](get-a-self-serve-policy-by-id.md)
  * [GetListOfSelfServicePolicies](get-a-list-of-self-serve-policies.md)
  * [CreateSelfServePolicies](create-a-self-serve-policy.md)
  * [UpdateSelfServePolicies](update-a-self-serve-policy.md)
  * [DeleteSelfServePolicies](delete-a-self-serve-policy.md)

* Ügyfelek vállalati profil
  * [OrganizationRegistrationNumber](create-a-customer.md) hozzáadva

* CustomerBillingProfile.DefaultAddress
  * MiddleName hozzáadva

## <a name="version-1162"></a>1.16.2 verziója

A [Microsoft partner Center .net SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v 1.16.2 mostantól általánosan elérhető. A frissített [GitHub-minták](https://github.com/Microsoft/Partner-Center-DotNet-Samples) is elérhetők. Ebben a verzióban a következő változások szerepelnek:

* A támogatott műveleti típusok frissítése a naplózási rekordhoz. Az újonnan hozzáadott eszközök a következők:
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * DeleteTipCustomer
  * CreateRelatedReferral
  * UpdateRelatedReferral

* A szolgáltatási kérelem létrehozása már elavult
* A támogatási témakörök már elavultak


## <a name="version-1161"></a>1.16.1 verziója

A [Microsoft partner Center .net SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v 1.16.1 mostantól általánosan elérhető. A frissített [GitHub-minták](https://github.com/Microsoft/Partner-Center-DotNet-Samples) is elérhetők. Ebben a verzióban a következő változások szerepelnek:

Áttelepítettük a Microsoft partner Center SDK-t a .NET-keretrendszerről a .NET Standard 2,0 platformra. Így az SDK kompatibilis lesz a meglévő alkalmazásokkal a .NET-keretrendszer 4.6.1-es és újabb verzióinak használatával. Az SDK a .NET Core 2,0-es vagy újabb verzióját fogja támogatni. Győződjön meg arról, hogy a [.net-implementáció támogatja](/dotnet/standard/net-standard) a meglévő alkalmazásokhoz való portolás előtt.   


## <a name="version-1153"></a>1.15.3 verziója
A [Microsoft partner Center .net SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v 1.15.3 mostantól általánosan elérhető. A frissített REST API-k és a [GitHub-minták](https://github.com/Microsoft/Partner-Center-DotNet-Samples) is elérhetők. Ebben a verzióban a következő változások szerepelnek:

* Partneri szerződés
  * Lehetővé tette a közvetett szolgáltatók számára a [közvetett viszonteladók Microsoft partneri szerződéssel kapcsolatos állapotának ellenőrzését](verify-indirect-reseller-mpa-status.md).
* Termékek
  * A következő két csatoló helytelenül lett a Microsoft. Store. PartnerCenter. Products névtér alá helyezve. Most a Microsoft. Store. PartnerCenter. customers. Products névtér alatt találhatók.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
