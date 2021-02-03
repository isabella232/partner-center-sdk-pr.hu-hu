---
title: Licencek hozzárendelése egy felhasználóhoz
description: Megtudhatja, hogyan rendelhet hozzá licenceket egy ügyfél-felhasználóhoz a partner Center API-kon keresztül, például C \# vagy REST API-k használatával.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6eb0b953b9157e48074415bb3207e2946cfb2ab4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768547"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a><span data-ttu-id="afa5e-103">Licencek kiosztása egy felhasználónak a partner Center API-kon keresztül</span><span class="sxs-lookup"><span data-stu-id="afa5e-103">Assign licenses to a user via Partner Center APIs</span></span>

<span data-ttu-id="afa5e-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="afa5e-104">**Applies to:**</span></span>

- <span data-ttu-id="afa5e-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="afa5e-105">Partner Center</span></span>

<span data-ttu-id="afa5e-106">Licencek kiosztása az ügyfél felhasználói számára.</span><span class="sxs-lookup"><span data-stu-id="afa5e-106">How to assign licenses to a customer user.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afa5e-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="afa5e-107">Prerequisites</span></span>

- <span data-ttu-id="afa5e-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="afa5e-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="afa5e-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="afa5e-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="afa5e-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="afa5e-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="afa5e-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="afa5e-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="afa5e-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="afa5e-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="afa5e-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="afa5e-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="afa5e-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="afa5e-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="afa5e-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="afa5e-116">Felhasználói azonosító.</span><span class="sxs-lookup"><span data-stu-id="afa5e-116">A customer user identifier.</span></span> <span data-ttu-id="afa5e-117">Ez az azonosító azonosítja azt a felhasználót, akihez a licencet hozzá kell rendelni.</span><span class="sxs-lookup"><span data-stu-id="afa5e-117">This ID identifies the user to whom to assign the license.</span></span>

- <span data-ttu-id="afa5e-118">A licenchez tartozó terméket azonosító termék SKU-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="afa5e-118">A product SKU identifier that identifies the product for the license.</span></span>

## <a name="assigning-licenses-through-code"></a><span data-ttu-id="afa5e-119">Licencek kiosztása kód használatával</span><span class="sxs-lookup"><span data-stu-id="afa5e-119">Assigning licenses through code</span></span>

<span data-ttu-id="afa5e-120">Amikor licenceket rendel egy felhasználóhoz, ki kell választania az ügyfél előfizetett SKU-gyűjteményéből.</span><span class="sxs-lookup"><span data-stu-id="afa5e-120">When you assign licenses to a user, you must choose from the customer's collection of subscribed SKUs.</span></span> <span data-ttu-id="afa5e-121">Ezután, miután azonosította a hozzárendelni kívánt termékeket, minden termékhez be kell szereznie a termék SKU-AZONOSÍTÓját a hozzárendelések elvégzéséhez.</span><span class="sxs-lookup"><span data-stu-id="afa5e-121">Then, having identified the products that you want to assign, you must obtain the product SKU ID for each product in order to make the assignments.</span></span> <span data-ttu-id="afa5e-122">Minden [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) -példány tartalmaz egy [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) -tulajdonságot, amelyből hivatkozhat a [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) objektumra, és lekérheti az [**azonosítót**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span><span class="sxs-lookup"><span data-stu-id="afa5e-122">Each [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) instance contains a [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) property from which you can reference the [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) object and get the [**ID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span></span>

<span data-ttu-id="afa5e-123">A licenc-hozzárendelési kérelemnek egyetlen licencszerződésből származó licenceket kell tartalmaznia.</span><span class="sxs-lookup"><span data-stu-id="afa5e-123">A license assignment request must contain licenses from a single license group.</span></span> <span data-ttu-id="afa5e-124">Nem rendelhet hozzá például licenceket a [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) és a **Group2** alkalmazáshoz ugyanabban a kérésben.</span><span class="sxs-lookup"><span data-stu-id="afa5e-124">For example, you cannot assign licenses from [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) and **Group2** in the same request.</span></span> <span data-ttu-id="afa5e-125">Egy adott kérelemben egynél több csoport licencének hozzárendelésére tett kísérlet a megfelelő hibával meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="afa5e-125">An attempt to assign licenses from more than one group in a single request will fail with an appropriate error.</span></span> <span data-ttu-id="afa5e-126">Ha szeretné megtudni, hogy milyen licencek érhetők el a licencszerződésben, tekintse meg az [elérhető licencek listájának beszerzése a licencszerződés alapján](get-a-list-of-available-licenses-by-license-group.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="afa5e-126">To find out what licenses are available by license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

<span data-ttu-id="afa5e-127">A licencek kód használatával történő hozzárendelésének lépései a következők:</span><span class="sxs-lookup"><span data-stu-id="afa5e-127">Here are the steps to assign licenses through code:</span></span>

1. <span data-ttu-id="afa5e-128">[**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) objektum példányának létrehozása.</span><span class="sxs-lookup"><span data-stu-id="afa5e-128">Instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object.</span></span> <span data-ttu-id="afa5e-129">Ezzel az objektummal adhatja meg a Hozzárendelendő termékhez tartozó SKU-t és szolgáltatási terveket.</span><span class="sxs-lookup"><span data-stu-id="afa5e-129">You use this object to specify the product SKU and service plans to assign.</span></span>

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. <span data-ttu-id="afa5e-130">Töltse fel az objektum tulajdonságait az alább látható módon.</span><span class="sxs-lookup"><span data-stu-id="afa5e-130">Populate the object properties as shown below.</span></span> <span data-ttu-id="afa5e-131">Ez a kód feltételezi, hogy már rendelkezik a termék SKU-azonosítójával, és az összes elérhető szolgáltatáscsomag hozzá lesz rendelve (azaz a None nem lesz kizárva).</span><span class="sxs-lookup"><span data-stu-id="afa5e-131">This code assumes that you already have the product SKU ID, and that all of the available service plans will be assigned (that is, none will be excluded).</span></span>

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. <span data-ttu-id="afa5e-132">Ha nem rendelkezik a termék SKU-azonosítójával, le kell kérnie az előfizetett SKU-gyűjteményt, és be kell szereznie a termék SKU-AZONOSÍTÓját az egyik közül.</span><span class="sxs-lookup"><span data-stu-id="afa5e-132">If you don't have the product SKU ID, you need to retrieve the collection of subscribed SKUs and get the product SKU ID from one of them.</span></span> <span data-ttu-id="afa5e-133">Íme egy példa, ha ismeri a termék SKU-nevét.</span><span class="sxs-lookup"><span data-stu-id="afa5e-133">Here is an example if you know the product SKU name.</span></span>

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. <span data-ttu-id="afa5e-134">Ezután hozza létre a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)típusú új listát, és adja hozzá a License objektumot.</span><span class="sxs-lookup"><span data-stu-id="afa5e-134">Next, instantiate a new list of type [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment), and add the license object.</span></span> <span data-ttu-id="afa5e-135">Több licencet is hozzárendelhet úgy, hogy mindegyiket egyenként hozzáadja a listához.</span><span class="sxs-lookup"><span data-stu-id="afa5e-135">You can assign more than one license by adding each individually to the list.</span></span> <span data-ttu-id="afa5e-136">A listában szereplő licenceknek ugyanabból a csoportból kell származnia.</span><span class="sxs-lookup"><span data-stu-id="afa5e-136">The licenses included in this list must be from the same license group.</span></span>

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. <span data-ttu-id="afa5e-137">Hozzon létre egy [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) -példányt, és rendelje hozzá a licenc-hozzárendelések listáját a [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) tulajdonsághoz.</span><span class="sxs-lookup"><span data-stu-id="afa5e-137">Create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. <span data-ttu-id="afa5e-138">A licencek hozzárendeléséhez hívja meg a [**create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) metódust, és adja át a licenc frissítése objektumot a lent látható módon.</span><span class="sxs-lookup"><span data-stu-id="afa5e-138">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object as shown below to assign the licenses.</span></span>

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a><span data-ttu-id="afa5e-139">C\#</span><span class="sxs-lookup"><span data-stu-id="afa5e-139">C\#</span></span>

<span data-ttu-id="afa5e-140">Ahhoz, hogy licencet rendeljen egy ügyfél-felhasználóhoz, először hozza létre a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) objektumot, és töltse fel a [**SkuID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) és a [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="afa5e-140">To assign a license to a customer user, first instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object, and populate the [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) and [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) properties.</span></span> <span data-ttu-id="afa5e-141">Ezzel az objektummal adhatja meg a kizárni kívánt termék SKU-jának kiosztását és a szolgáltatási terveket.</span><span class="sxs-lookup"><span data-stu-id="afa5e-141">You use this object to specify the product SKU to assign and service plans to exclude.</span></span> <span data-ttu-id="afa5e-142">Ezután hozza létre a **LicenseAssignment** típusú új listát, és adja hozzá a licenc objektumot a listához.</span><span class="sxs-lookup"><span data-stu-id="afa5e-142">Next, instantiate a new list of type **LicenseAssignment**, and add the license object to the list.</span></span> <span data-ttu-id="afa5e-143">Ezután hozzon létre egy [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) -példányt, és rendelje hozzá a licenc-hozzárendelések listáját a [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) tulajdonsághoz.</span><span class="sxs-lookup"><span data-stu-id="afa5e-143">Then create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

<span data-ttu-id="afa5e-144">Ezután használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához, valamint a Users [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) METÓDUSt a felhasználói azonosítóval a felhasználó azonosításához.</span><span class="sxs-lookup"><span data-stu-id="afa5e-144">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="afa5e-145">Ezután szerezzen be egy felületet az ügyfél felhasználói licencek frissítési műveleteihez a [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="afa5e-145">Then get an interface to customer user license update operations from the [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) property.</span></span>

<span data-ttu-id="afa5e-146">Végül hívja meg a [**create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) metódust, és adja át a licenc frissítése objektumot a licenc hozzárendeléséhez.</span><span class="sxs-lookup"><span data-stu-id="afa5e-146">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object to assign the license.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerUserId;
// string selectedCustomerId;
// string selectedProductSkuId;

// Instantiate and populate a LicenseAssignment object.
LicenseAssignment license = new LicenseAssignment();
license.SkuId = selectedProductSkuId;
license.ExcludedPlans = null;

// Instantiate a list of licenses to assign and add the license to it.
List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
licenseList.Add(license);

// Instantiate a LicenseUpdate object and add the list of licenses to assign.
LicenseUpdate updateLicense = new LicenseUpdate();
updateLicense.LicensesToAssign = licenseList;

// Update the user licenses.
var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
```

<span data-ttu-id="afa5e-147">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="afa5e-147">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="afa5e-148">**Projekt**: partner Center SDK Samples **osztály**: CustomerUserAssignLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="afa5e-148">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="afa5e-149">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="afa5e-149">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="afa5e-150">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="afa5e-150">Request syntax</span></span>

| <span data-ttu-id="afa5e-151">Metódus</span><span class="sxs-lookup"><span data-stu-id="afa5e-151">Method</span></span>   | <span data-ttu-id="afa5e-152">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="afa5e-152">Request URI</span></span>                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="afa5e-153">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="afa5e-153">**POST**</span></span> | <span data-ttu-id="afa5e-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenseupdates http/1.1</span><span class="sxs-lookup"><span data-stu-id="afa5e-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="afa5e-155">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="afa5e-155">URI parameters</span></span>

<span data-ttu-id="afa5e-156">Az ügyfél és a felhasználó azonosításához használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="afa5e-156">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="afa5e-157">Név</span><span class="sxs-lookup"><span data-stu-id="afa5e-157">Name</span></span>        | <span data-ttu-id="afa5e-158">Típus</span><span class="sxs-lookup"><span data-stu-id="afa5e-158">Type</span></span>   | <span data-ttu-id="afa5e-159">Kötelező</span><span class="sxs-lookup"><span data-stu-id="afa5e-159">Required</span></span> | <span data-ttu-id="afa5e-160">Leírás</span><span class="sxs-lookup"><span data-stu-id="afa5e-160">Description</span></span>                                       |
|-------------|--------|----------|---------------------------------------------------|
| <span data-ttu-id="afa5e-161">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="afa5e-161">customer-id</span></span> | <span data-ttu-id="afa5e-162">sztring</span><span class="sxs-lookup"><span data-stu-id="afa5e-162">string</span></span> | <span data-ttu-id="afa5e-163">Igen</span><span class="sxs-lookup"><span data-stu-id="afa5e-163">Yes</span></span>      | <span data-ttu-id="afa5e-164">Egy GUID formátumú azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="afa5e-164">A GUID formatted ID that identifies the customer.</span></span> |
| <span data-ttu-id="afa5e-165">felhasználói azonosító</span><span class="sxs-lookup"><span data-stu-id="afa5e-165">user-id</span></span>     | <span data-ttu-id="afa5e-166">sztring</span><span class="sxs-lookup"><span data-stu-id="afa5e-166">string</span></span> | <span data-ttu-id="afa5e-167">Igen</span><span class="sxs-lookup"><span data-stu-id="afa5e-167">Yes</span></span>      | <span data-ttu-id="afa5e-168">A felhasználó azonosítására szolgáló GUID formátumú azonosító.</span><span class="sxs-lookup"><span data-stu-id="afa5e-168">A GUID formatted ID that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="afa5e-169">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="afa5e-169">Request headers</span></span>

<span data-ttu-id="afa5e-170">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="afa5e-170">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="afa5e-171">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="afa5e-171">Request body</span></span>

<span data-ttu-id="afa5e-172">Adjon meg egy [LicenseUpdate](license-resources.md#licenseupdate) -erőforrást a kérelem törzsében, amely meghatározza a hozzárendelni kívánt licenceket.</span><span class="sxs-lookup"><span data-stu-id="afa5e-172">Include a [LicenseUpdate](license-resources.md#licenseupdate) resource in the request body that specifies the licenses to assign.</span></span>

### <a name="request-example"></a><span data-ttu-id="afa5e-173">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="afa5e-173">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/554526aa-cf5e-46fa-95df-98dbc55d8a1e/licenseupdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 183
Expect: 100-continue

{
    "LicensesToAssign": [{
            "ExcludedPlans": null,
            "SkuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "LicensesToRemove": null,
    "LicenseWarnings": null,
    "Attributes": {
        "ObjectType": "LicenseUpdate"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="afa5e-174">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="afa5e-174">REST response</span></span>

<span data-ttu-id="afa5e-175">Ha a művelet sikeres, a rendszer a 201-as HTTP-válasz állapotkódot adja vissza, és a válasz törzse tartalmaz egy [LicenseUpdate](license-resources.md#licenseupdate) -erőforrást a licencelési adatokkal.</span><span class="sxs-lookup"><span data-stu-id="afa5e-175">If successful, an HTTP response status code 201 is returned and the response body contains a [LicenseUpdate](license-resources.md#licenseupdate) resource with the license information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="afa5e-176">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="afa5e-176">Response success and error codes</span></span>

<span data-ttu-id="afa5e-177">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="afa5e-177">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="afa5e-178">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="afa5e-178">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="afa5e-179">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="afa5e-179">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="afa5e-180">Válasz példa (sikeres)</span><span class="sxs-lookup"><span data-stu-id="afa5e-180">Response example (success)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 139
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CV: 5AnzcZQrvUqCq3kd.0
MS-ServerId: 030020525
Date: Thu, 20 Apr 2017 21:50:39 GMT

{
    "licensesToAssign": [{
            "skuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "licenseWarnings": [],
    "attributes": {
        "objectType": "LicenseUpdate"
    }
}
```

### <a name="response-example-license-isnt-available"></a><span data-ttu-id="afa5e-181">Válasz példa (a licenc nem érhető el)</span><span class="sxs-lookup"><span data-stu-id="afa5e-181">Response example (license isn't available)</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 341
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: f4f3b748-8b22-4d07-a5a1-dceb32824192
MS-CV: 5npA0K22CUmWPOzB.0
MS-ServerId: 102030524
Date: Thu, 20 Apr 2017 22:12:36 GMT

{
    "code": 60012,
    "description": "We&#39;re sorry, it looks like you've run out of licenses. Buy more licenses, and then try again.",
    "data": ["LicenseQuotaExceededException : Subscription with Account 0c39d6d5-c70d-4c55-bc02-f620844f3fd1 and SKU f8a1db68-be16-40ed-86d5-cb42ce701560 does not have any available licenses left."],
    "source": "PartnerFD"
}
```
