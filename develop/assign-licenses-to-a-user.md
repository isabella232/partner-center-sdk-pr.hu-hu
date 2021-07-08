---
title: Licencek hozzárendelése egy felhasználóhoz
description: Megtudhatja, hogyan rendelhet licenceket egy ügyfélfelhasználóhoz Partnerközpont API-kon keresztül, például c vagy \# REST API-k használatával.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 88ce0f185b0b043c4a7862b7f9808fb8805d40b9
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974369"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a><span data-ttu-id="91439-103">Licencek hozzárendelése egy felhasználóhoz Partnerközpont API-kon keresztül</span><span class="sxs-lookup"><span data-stu-id="91439-103">Assign licenses to a user via Partner Center APIs</span></span>

<span data-ttu-id="91439-104">Licencek hozzárendelése egy ügyfélfelhasználóhoz.</span><span class="sxs-lookup"><span data-stu-id="91439-104">How to assign licenses to a customer user.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91439-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="91439-105">Prerequisites</span></span>

- <span data-ttu-id="91439-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="91439-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="91439-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="91439-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="91439-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="91439-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="91439-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="91439-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="91439-110">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="91439-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="91439-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="91439-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="91439-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="91439-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="91439-113">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="91439-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="91439-114">Ügyfélfelhasználó-azonosító.</span><span class="sxs-lookup"><span data-stu-id="91439-114">A customer user identifier.</span></span> <span data-ttu-id="91439-115">Ez az azonosító azonosítja a felhasználót, akihez a licencet hozzá kell rendelni.</span><span class="sxs-lookup"><span data-stu-id="91439-115">This ID identifies the user to whom to assign the license.</span></span>

- <span data-ttu-id="91439-116">A termék termékváltozat-azonosítója, amely azonosítja a terméket a licenchez.</span><span class="sxs-lookup"><span data-stu-id="91439-116">A product SKU identifier that identifies the product for the license.</span></span>

## <a name="assigning-licenses-through-code"></a><span data-ttu-id="91439-117">Licencek kóddal való hozzárendelése</span><span class="sxs-lookup"><span data-stu-id="91439-117">Assigning licenses through code</span></span>

<span data-ttu-id="91439-118">Amikor licenceket rendel egy felhasználóhoz, választania kell az ügyfél előfizetéses termékkód-gyűjteményéből.</span><span class="sxs-lookup"><span data-stu-id="91439-118">When you assign licenses to a user, you must choose from the customer's collection of subscribed SKUs.</span></span> <span data-ttu-id="91439-119">Ezt követően, miután azonosította a hozzárendelni kívánt termékeket, be kell szereznie az egyes termékek termékváltozat-azonosítóját a hozzárendelések kiosztásához.</span><span class="sxs-lookup"><span data-stu-id="91439-119">Then, having identified the products that you want to assign, you must obtain the product SKU ID for each product in order to make the assignments.</span></span> <span data-ttu-id="91439-120">Minden [**SubscribedSku példány**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) tartalmaz egy [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) tulajdonságot, amelyből hivatkozhat a [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) objektumra, és le tudja szerezni az [**azonosítót.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id)</span><span class="sxs-lookup"><span data-stu-id="91439-120">Each [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) instance contains a [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) property from which you can reference the [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) object and get the [**ID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span></span>

<span data-ttu-id="91439-121">A licenc-hozzárendelési kérelemnek egyetlen licenccsoport licencét kell tartalmaznia.</span><span class="sxs-lookup"><span data-stu-id="91439-121">A license assignment request must contain licenses from a single license group.</span></span> <span data-ttu-id="91439-122">Például nem rendelhet licenceket a [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) és **a Group2** csoporthoz ugyanabban a kérésben.</span><span class="sxs-lookup"><span data-stu-id="91439-122">For example, you cannot assign licenses from [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) and **Group2** in the same request.</span></span> <span data-ttu-id="91439-123">Ha egy kérésben egynél több csoport licencét kísérelik meg hozzárendelni, az egy megfelelő hibával meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="91439-123">An attempt to assign licenses from more than one group in a single request will fail with an appropriate error.</span></span> <span data-ttu-id="91439-124">A licenccsoport szerint elérhető licencekről az Elérhető licencek listájának lekért listája [licenccsoport szerint.](get-a-list-of-available-licenses-by-license-group.md)</span><span class="sxs-lookup"><span data-stu-id="91439-124">To find out what licenses are available by license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

<span data-ttu-id="91439-125">A licencek kódon keresztüli hozzárendelésének lépései a következőek:</span><span class="sxs-lookup"><span data-stu-id="91439-125">Here are the steps to assign licenses through code:</span></span>

1. <span data-ttu-id="91439-126">Egy [**LicenseAssignment objektum példányosítása.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)</span><span class="sxs-lookup"><span data-stu-id="91439-126">Instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object.</span></span> <span data-ttu-id="91439-127">Ezzel az objektummal adhatja meg a hozzárendelni kívánt termékváltozatot és szolgáltatásterveket.</span><span class="sxs-lookup"><span data-stu-id="91439-127">You use this object to specify the product SKU and service plans to assign.</span></span>

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. <span data-ttu-id="91439-128">Töltse ki az objektum tulajdonságait az alább látható módon.</span><span class="sxs-lookup"><span data-stu-id="91439-128">Populate the object properties as shown below.</span></span> <span data-ttu-id="91439-129">Ez a kód feltételezi, hogy már rendelkezik a termék termékváltozat-azonosítójával, és hogy az összes elérhető szolgáltatás csomag hozzá lesz rendelve (ez azt jelenti, hogy egyik sem lesz kizárva).</span><span class="sxs-lookup"><span data-stu-id="91439-129">This code assumes that you already have the product SKU ID, and that all of the available service plans will be assigned (that is, none will be excluded).</span></span>

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. <span data-ttu-id="91439-130">Ha nem tudja a termék termékváltozat-azonosítóját, le kellkérni az előfizetett termékváltozatok gyűjteményét, és le kell szereznie a termék termékváltozat-azonosítóját az egyikből.</span><span class="sxs-lookup"><span data-stu-id="91439-130">If you don't have the product SKU ID, you need to retrieve the collection of subscribed SKUs and get the product SKU ID from one of them.</span></span> <span data-ttu-id="91439-131">Példa a termékváltozat nevének nevére.</span><span class="sxs-lookup"><span data-stu-id="91439-131">Here is an example if you know the product SKU name.</span></span>

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. <span data-ttu-id="91439-132">Ezután példányositsa a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)típusú új listát, és adja hozzá a licencobjektumot.</span><span class="sxs-lookup"><span data-stu-id="91439-132">Next, instantiate a new list of type [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment), and add the license object.</span></span> <span data-ttu-id="91439-133">Több licencet is hozzárendelhet, ha egyenként hozzáadja azokat a listához.</span><span class="sxs-lookup"><span data-stu-id="91439-133">You can assign more than one license by adding each individually to the list.</span></span> <span data-ttu-id="91439-134">A listában szereplő licenceknek ugyanattól a licenccsoporttól kell tartozni.</span><span class="sxs-lookup"><span data-stu-id="91439-134">The licenses included in this list must be from the same license group.</span></span>

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. <span data-ttu-id="91439-135">Hozzon [**létre egy LicenseUpdate példányt,**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) és rendelje hozzá a licenc-hozzárendelések listáját a [**LicensesToAssign tulajdonsághoz.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)</span><span class="sxs-lookup"><span data-stu-id="91439-135">Create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. <span data-ttu-id="91439-136">Hívja meg [**a Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) vagy [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) metódust, és adja át a licencfrissítési objektumot az alább látható módon a licencek hozzárendeléséhez.</span><span class="sxs-lookup"><span data-stu-id="91439-136">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object as shown below to assign the licenses.</span></span>

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a><span data-ttu-id="91439-137">C\#</span><span class="sxs-lookup"><span data-stu-id="91439-137">C\#</span></span>

<span data-ttu-id="91439-138">Ha egy licencet szeretne hozzárendelni egy ügyfélfelhasználóhoz, először példányosítenie kell egy [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) objektumot, és ki kell feltöltenie az [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) és [**excludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) tulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="91439-138">To assign a license to a customer user, first instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object, and populate the [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) and [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) properties.</span></span> <span data-ttu-id="91439-139">Ezzel az objektummal adhatja meg a hozzárendelni kívánt termékváltozatot és a kizárni kívánt szolgáltatásterveket.</span><span class="sxs-lookup"><span data-stu-id="91439-139">You use this object to specify the product SKU to assign and service plans to exclude.</span></span> <span data-ttu-id="91439-140">Ezután példányositsa a **LicenseAssignment** típusú új listát, és adja hozzá a licencobjektumot a listához.</span><span class="sxs-lookup"><span data-stu-id="91439-140">Next, instantiate a new list of type **LicenseAssignment**, and add the license object to the list.</span></span> <span data-ttu-id="91439-141">Ezután hozzon létre [**egy LicenseUpdate példányt,**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) és rendelje hozzá a licenc-hozzárendelések listáját a [**LicensesToAssign tulajdonsághoz.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)</span><span class="sxs-lookup"><span data-stu-id="91439-141">Then create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

<span data-ttu-id="91439-142">Ezután használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához, a [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust pedig a felhasználói azonosítóval a felhasználó azonosításához.</span><span class="sxs-lookup"><span data-stu-id="91439-142">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="91439-143">Ezután szerezze be az ügyfélfelhasználói licencfrissítési műveletek felületét a [**LicenseUpdates tulajdonságból.**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates)</span><span class="sxs-lookup"><span data-stu-id="91439-143">Then get an interface to customer user license update operations from the [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) property.</span></span>

<span data-ttu-id="91439-144">Végül hívja meg a [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) vagy [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) metódust, és adja át a licencfrissítési objektumot a licenc hozzárendeléséhez.</span><span class="sxs-lookup"><span data-stu-id="91439-144">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object to assign the license.</span></span>

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

<span data-ttu-id="91439-145">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="91439-145">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="91439-146">**Project**: Partnerközpont SDK **Osztály:** CustomerUserAssignLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="91439-146">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="91439-147">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="91439-147">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="91439-148">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="91439-148">Request syntax</span></span>

| <span data-ttu-id="91439-149">Metódus</span><span class="sxs-lookup"><span data-stu-id="91439-149">Method</span></span>   | <span data-ttu-id="91439-150">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="91439-150">Request URI</span></span>                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="91439-151">**Post**</span><span class="sxs-lookup"><span data-stu-id="91439-151">**POST**</span></span> | <span data-ttu-id="91439-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/users/{felhasználói azonosító}/licenseupdates HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="91439-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="91439-153">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="91439-153">URI parameters</span></span>

<span data-ttu-id="91439-154">Az ügyfél és a felhasználó azonosításához használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="91439-154">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="91439-155">Név</span><span class="sxs-lookup"><span data-stu-id="91439-155">Name</span></span>        | <span data-ttu-id="91439-156">Típus</span><span class="sxs-lookup"><span data-stu-id="91439-156">Type</span></span>   | <span data-ttu-id="91439-157">Kötelező</span><span class="sxs-lookup"><span data-stu-id="91439-157">Required</span></span> | <span data-ttu-id="91439-158">Leírás</span><span class="sxs-lookup"><span data-stu-id="91439-158">Description</span></span>                                       |
|-------------|--------|----------|---------------------------------------------------|
| <span data-ttu-id="91439-159">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="91439-159">customer-id</span></span> | <span data-ttu-id="91439-160">sztring</span><span class="sxs-lookup"><span data-stu-id="91439-160">string</span></span> | <span data-ttu-id="91439-161">Igen</span><span class="sxs-lookup"><span data-stu-id="91439-161">Yes</span></span>      | <span data-ttu-id="91439-162">Egy GUID formátumú azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="91439-162">A GUID formatted ID that identifies the customer.</span></span> |
| <span data-ttu-id="91439-163">felhasználói azonosító</span><span class="sxs-lookup"><span data-stu-id="91439-163">user-id</span></span>     | <span data-ttu-id="91439-164">sztring</span><span class="sxs-lookup"><span data-stu-id="91439-164">string</span></span> | <span data-ttu-id="91439-165">Igen</span><span class="sxs-lookup"><span data-stu-id="91439-165">Yes</span></span>      | <span data-ttu-id="91439-166">A felhasználót azonosító GUID formátumú azonosító.</span><span class="sxs-lookup"><span data-stu-id="91439-166">A GUID formatted ID that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="91439-167">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="91439-167">Request headers</span></span>

<span data-ttu-id="91439-168">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="91439-168">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="91439-169">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="91439-169">Request body</span></span>

<span data-ttu-id="91439-170">Foglaljon bele [egy LicenseUpdate erőforrást](license-resources.md#licenseupdate) a kérelem törzsébe, amely megadja a hozzárendelni szükséges licenceket.</span><span class="sxs-lookup"><span data-stu-id="91439-170">Include a [LicenseUpdate](license-resources.md#licenseupdate) resource in the request body that specifies the licenses to assign.</span></span>

### <a name="request-example"></a><span data-ttu-id="91439-171">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="91439-171">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="91439-172">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="91439-172">REST response</span></span>

<span data-ttu-id="91439-173">Sikeres művelet esetén a rendszer visszaad egy 201-es HTTP-válaszállapotkódot, és a válasz törzse tartalmaz egy [LicenseUpdate](license-resources.md#licenseupdate) erőforrást a licencinformációk alapján.</span><span class="sxs-lookup"><span data-stu-id="91439-173">If successful, an HTTP response status code 201 is returned and the response body contains a [LicenseUpdate](license-resources.md#licenseupdate) resource with the license information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="91439-174">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="91439-174">Response success and error codes</span></span>

<span data-ttu-id="91439-175">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="91439-175">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="91439-176">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="91439-176">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="91439-177">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="91439-177">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="91439-178">Válasz példa (sikeres)</span><span class="sxs-lookup"><span data-stu-id="91439-178">Response example (success)</span></span>

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

### <a name="response-example-license-isnt-available"></a><span data-ttu-id="91439-179">Példaválasz (a licenc nem érhető el)</span><span class="sxs-lookup"><span data-stu-id="91439-179">Response example (license isn't available)</span></span>

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
