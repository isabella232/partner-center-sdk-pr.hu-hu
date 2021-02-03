---
title: Kosár létrehozása bővítményekkel
description: Megtudhatja, hogyan veheti fel a partner Center API-kat a bővítmények egy kosárba való felvételéhez. Cikk megosztja az előfeltételeket és lépéseket a kosár bővítményekkel való létrehozásához.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 81c41405a2f56eb4d1d3447d14b93e05d550cc70
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768628"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a><span data-ttu-id="667e2-104">Kosár létrehozása az ügyfelek megrendeléséhez bővítményekkel</span><span class="sxs-lookup"><span data-stu-id="667e2-104">Create a cart with add-ons to a customer order</span></span>

<span data-ttu-id="667e2-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="667e2-105">**Applies to:**</span></span>

- <span data-ttu-id="667e2-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="667e2-106">Partner Center</span></span>

<span data-ttu-id="667e2-107">A bővítményeket a kosáron keresztül is megvásárolhatja.</span><span class="sxs-lookup"><span data-stu-id="667e2-107">You can purchase add-ons through a cart.</span></span> <span data-ttu-id="667e2-108">További információ az értékesítésre jelenleg elérhető termékekről: [partneri ajánlatok a Cloud Solution Provider programban](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="667e2-108">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="667e2-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="667e2-109">Prerequisites</span></span>

- <span data-ttu-id="667e2-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="667e2-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="667e2-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="667e2-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="667e2-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="667e2-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="667e2-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="667e2-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="667e2-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="667e2-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="667e2-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="667e2-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="667e2-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="667e2-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="667e2-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="667e2-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="667e2-118">C\#</span><span class="sxs-lookup"><span data-stu-id="667e2-118">C\#</span></span>

<span data-ttu-id="667e2-119">A kosár lehetővé teszi egy alapszintű ajánlat és a hozzájuk tartozó bővítmények megvásárlását.</span><span class="sxs-lookup"><span data-stu-id="667e2-119">A cart enables the purchase of a base offer and its corresponding add-ons.</span></span> <span data-ttu-id="667e2-120">A kosár létrehozásához kövesse az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="667e2-120">Follow these steps to create a cart:</span></span>

1. <span data-ttu-id="667e2-121">Egy [**cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) -objektum példányának létrehozása.</span><span class="sxs-lookup"><span data-stu-id="667e2-121">Instantiate a [**Cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) object.</span></span>

2. <span data-ttu-id="667e2-122">Hozzon létre egy listát az alapajánlat (oka) t képviselő [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) -objektumokról, és rendelje hozzá a listát a kosár [**listaelemek**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) tulajdonságához.</span><span class="sxs-lookup"><span data-stu-id="667e2-122">Create a list of [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objects which represent the base offer(s), and assign the list to the cart's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) property.</span></span>

3. <span data-ttu-id="667e2-123">Az egyes alapajánlatok sorában töltse fel a **AddOnItems** listáját más **CartLineItem** objektumokkal, amelyek mindegyike az adott alapajánlathoz megvásárolt bővítményt képviseli.</span><span class="sxs-lookup"><span data-stu-id="667e2-123">Under each base offer's cart line item, populate the list of **AddOnItems** with other **CartLineItem** objects that each represent an add-on that will be purchased against that base offer.</span></span>

4. <span data-ttu-id="667e2-124">Szerezzen be egy felületet a cart-műveletekhez a [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) használatával, hogy meghívja a [**ICustomerCollection. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, hogy azonosítsa az ügyfelet, majd beolvassa a felületet a **cart** tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="667e2-124">Obtain an interface to cart operations by using [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) to call the [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

5. <span data-ttu-id="667e2-125">Végül hívja meg a [**create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) metódust a kosár létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="667e2-125">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="667e2-126">C \# példa</span><span class="sxs-lookup"><span data-stu-id="667e2-126">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

<span data-ttu-id="667e2-127">Kövesse az alábbi lépéseket egy olyan kosár létrehozásához, amely lehetővé teszi bővítmény (ek) megvásárlását meglévő alapszintű előfizetések esetén:</span><span class="sxs-lookup"><span data-stu-id="667e2-127">Follow these steps to create a cart which will enable the purchase of add-on(s) against existing base subscription(s):</span></span>

1. <span data-ttu-id="667e2-128">Hozzon **létre egy új** **CartLineItem** , amely tartalmazza az előfizetés azonosítóját a **ProvisioningContext** tulajdonságban az "ParentSubscriptionId" kulccsal.</span><span class="sxs-lookup"><span data-stu-id="667e2-128">Create a **Cart** with a new **CartLineItem** containing the subscription ID in the **ProvisioningContext** property with key "ParentSubscriptionId".</span></span>

2. <span data-ttu-id="667e2-129">Hívja meg a **create** vagy a **CreateAsync** metódust.</span><span class="sxs-lookup"><span data-stu-id="667e2-129">Call the **Create** or **CreateAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a><span data-ttu-id="667e2-130">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="667e2-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="667e2-131">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="667e2-131">Request syntax</span></span>

| <span data-ttu-id="667e2-132">Metódus</span><span class="sxs-lookup"><span data-stu-id="667e2-132">Method</span></span>   | <span data-ttu-id="667e2-133">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="667e2-133">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="667e2-134">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="667e2-134">**POST**</span></span> | <span data-ttu-id="667e2-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts http/1.1</span><span class="sxs-lookup"><span data-stu-id="667e2-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

#### <a name="uri-parameter"></a><span data-ttu-id="667e2-136">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="667e2-136">URI parameter</span></span>

<span data-ttu-id="667e2-137">Az ügyfél azonosításához használja a következő Path paramétert.</span><span class="sxs-lookup"><span data-stu-id="667e2-137">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="667e2-138">Név</span><span class="sxs-lookup"><span data-stu-id="667e2-138">Name</span></span>            | <span data-ttu-id="667e2-139">Típus</span><span class="sxs-lookup"><span data-stu-id="667e2-139">Type</span></span>     | <span data-ttu-id="667e2-140">Kötelező</span><span class="sxs-lookup"><span data-stu-id="667e2-140">Required</span></span> | <span data-ttu-id="667e2-141">Leírás</span><span class="sxs-lookup"><span data-stu-id="667e2-141">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="667e2-142">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="667e2-142">**customer-id**</span></span> | <span data-ttu-id="667e2-143">sztring</span><span class="sxs-lookup"><span data-stu-id="667e2-143">string</span></span>   | <span data-ttu-id="667e2-144">Igen</span><span class="sxs-lookup"><span data-stu-id="667e2-144">Yes</span></span>      | <span data-ttu-id="667e2-145">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="667e2-145">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="667e2-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="667e2-146">Request headers</span></span>

<span data-ttu-id="667e2-147">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="667e2-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="667e2-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="667e2-148">Request body</span></span>

<span data-ttu-id="667e2-149">Ez a táblázat a kérés törzsében lévő [kosár](cart-resources.md) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="667e2-149">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="667e2-150">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="667e2-150">Property</span></span>              | <span data-ttu-id="667e2-151">Típus</span><span class="sxs-lookup"><span data-stu-id="667e2-151">Type</span></span>             | <span data-ttu-id="667e2-152">Kötelező</span><span class="sxs-lookup"><span data-stu-id="667e2-152">Required</span></span>        | <span data-ttu-id="667e2-153">Leírás</span><span class="sxs-lookup"><span data-stu-id="667e2-153">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="667e2-154">id</span><span class="sxs-lookup"><span data-stu-id="667e2-154">id</span></span>                    | <span data-ttu-id="667e2-155">sztring</span><span class="sxs-lookup"><span data-stu-id="667e2-155">string</span></span>           | <span data-ttu-id="667e2-156">No</span><span class="sxs-lookup"><span data-stu-id="667e2-156">No</span></span>              | <span data-ttu-id="667e2-157">A kosár sikeres létrehozásához megadott cart-azonosító.</span><span class="sxs-lookup"><span data-stu-id="667e2-157">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="667e2-158">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="667e2-158">creationTimeStamp</span></span>     | <span data-ttu-id="667e2-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="667e2-159">DateTime</span></span>         | <span data-ttu-id="667e2-160">Nem</span><span class="sxs-lookup"><span data-stu-id="667e2-160">No</span></span>              | <span data-ttu-id="667e2-161">A kosár létrehozásának dátuma dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="667e2-161">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="667e2-162">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="667e2-162">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="667e2-163">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="667e2-163">lastModifiedTimeStamp</span></span> | <span data-ttu-id="667e2-164">DateTime</span><span class="sxs-lookup"><span data-stu-id="667e2-164">DateTime</span></span>         | <span data-ttu-id="667e2-165">Nem</span><span class="sxs-lookup"><span data-stu-id="667e2-165">No</span></span>              | <span data-ttu-id="667e2-166">A kosár utolsó frissítésének dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="667e2-166">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="667e2-167">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="667e2-167">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="667e2-168">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="667e2-168">expirationTimeStamp</span></span>   | <span data-ttu-id="667e2-169">DateTime</span><span class="sxs-lookup"><span data-stu-id="667e2-169">DateTime</span></span>         | <span data-ttu-id="667e2-170">Nem</span><span class="sxs-lookup"><span data-stu-id="667e2-170">No</span></span>              | <span data-ttu-id="667e2-171">A kosár lejáratának dátuma dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="667e2-171">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="667e2-172">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="667e2-172">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="667e2-173">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="667e2-173">lastModifiedUser</span></span>      | <span data-ttu-id="667e2-174">sztring</span><span class="sxs-lookup"><span data-stu-id="667e2-174">string</span></span>           | <span data-ttu-id="667e2-175">No</span><span class="sxs-lookup"><span data-stu-id="667e2-175">No</span></span>              | <span data-ttu-id="667e2-176">A kosár utolsó frissítését végző felhasználó.</span><span class="sxs-lookup"><span data-stu-id="667e2-176">The user who last updated the cart.</span></span> <span data-ttu-id="667e2-177">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="667e2-177">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="667e2-178">Listaelemek</span><span class="sxs-lookup"><span data-stu-id="667e2-178">lineItems</span></span>             | <span data-ttu-id="667e2-179">Objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="667e2-179">Array of objects</span></span> | <span data-ttu-id="667e2-180">Igen</span><span class="sxs-lookup"><span data-stu-id="667e2-180">Yes</span></span>             | <span data-ttu-id="667e2-181">[CartLineItem](cart-resources.md#cartlineitem) -erőforrások tömbje.</span><span class="sxs-lookup"><span data-stu-id="667e2-181">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                             |

<span data-ttu-id="667e2-182">Ez a táblázat a kérelem törzsének [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="667e2-182">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="667e2-183">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="667e2-183">Property</span></span>             | <span data-ttu-id="667e2-184">Típus</span><span class="sxs-lookup"><span data-stu-id="667e2-184">Type</span></span>                             | <span data-ttu-id="667e2-185">Leírás</span><span class="sxs-lookup"><span data-stu-id="667e2-185">Description</span></span>                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="667e2-186">id</span><span class="sxs-lookup"><span data-stu-id="667e2-186">id</span></span>                   | <span data-ttu-id="667e2-187">sztring</span><span class="sxs-lookup"><span data-stu-id="667e2-187">string</span></span>                           | <span data-ttu-id="667e2-188">Egy cart-sor egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="667e2-188">A unique identifier for a cart line item.</span></span> <span data-ttu-id="667e2-189">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="667e2-189">Applied upon successful creation of cart.</span></span>                                                                   |
| <span data-ttu-id="667e2-190">catalogId</span><span class="sxs-lookup"><span data-stu-id="667e2-190">catalogId</span></span>            | <span data-ttu-id="667e2-191">sztring</span><span class="sxs-lookup"><span data-stu-id="667e2-191">string</span></span>                           | <span data-ttu-id="667e2-192">A katalógus-elemek azonosítója.</span><span class="sxs-lookup"><span data-stu-id="667e2-192">The catalog item identifier.</span></span>                                                                                                                          |
| <span data-ttu-id="667e2-193">friendlyName</span><span class="sxs-lookup"><span data-stu-id="667e2-193">friendlyName</span></span>         | <span data-ttu-id="667e2-194">sztring</span><span class="sxs-lookup"><span data-stu-id="667e2-194">string</span></span>                           | <span data-ttu-id="667e2-195">Választható.</span><span class="sxs-lookup"><span data-stu-id="667e2-195">Optional.</span></span> <span data-ttu-id="667e2-196">A partner által a egyértelműsítse segítségére meghatározott rövid név.</span><span class="sxs-lookup"><span data-stu-id="667e2-196">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                                 |
| <span data-ttu-id="667e2-197">quantity</span><span class="sxs-lookup"><span data-stu-id="667e2-197">quantity</span></span>             | <span data-ttu-id="667e2-198">int</span><span class="sxs-lookup"><span data-stu-id="667e2-198">int</span></span>                              | <span data-ttu-id="667e2-199">A licencek vagy példányok száma.</span><span class="sxs-lookup"><span data-stu-id="667e2-199">The number of licenses or instances.</span></span>                                                                                                                  |
| <span data-ttu-id="667e2-200">currencyCode</span><span class="sxs-lookup"><span data-stu-id="667e2-200">currencyCode</span></span>         | <span data-ttu-id="667e2-201">sztring</span><span class="sxs-lookup"><span data-stu-id="667e2-201">string</span></span>                           | <span data-ttu-id="667e2-202">A Pénznemkód.</span><span class="sxs-lookup"><span data-stu-id="667e2-202">The currency code.</span></span>                                                                                                                                    |
| <span data-ttu-id="667e2-203">billingCycle</span><span class="sxs-lookup"><span data-stu-id="667e2-203">billingCycle</span></span>         | <span data-ttu-id="667e2-204">Objektum</span><span class="sxs-lookup"><span data-stu-id="667e2-204">Object</span></span>                           | <span data-ttu-id="667e2-205">Az aktuális időszakban beállított számlázási ciklus típusa.</span><span class="sxs-lookup"><span data-stu-id="667e2-205">The type of billing cycle set for the current period.</span></span>                                                                                                 |
| <span data-ttu-id="667e2-206">résztvevők</span><span class="sxs-lookup"><span data-stu-id="667e2-206">participants</span></span>         | <span data-ttu-id="667e2-207">Az Object string párok listája</span><span class="sxs-lookup"><span data-stu-id="667e2-207">List of Object String pairs</span></span>      | <span data-ttu-id="667e2-208">A PartnerId on Record (MPNID) gyűjteménye a vásárláson.</span><span class="sxs-lookup"><span data-stu-id="667e2-208">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                                          |
| <span data-ttu-id="667e2-209">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="667e2-209">provisioningContext</span></span>  | <span data-ttu-id="667e2-210">Szótár<karakterlánc, karakterlánc></span><span class="sxs-lookup"><span data-stu-id="667e2-210">Dictionary<string, string></span></span>       | <span data-ttu-id="667e2-211">Az ajánlat üzembe helyezéséhez használt környezet.</span><span class="sxs-lookup"><span data-stu-id="667e2-211">A context used for provisioning of offer.</span></span>                                                                                                             |
| <span data-ttu-id="667e2-212">orderGroup</span><span class="sxs-lookup"><span data-stu-id="667e2-212">orderGroup</span></span>           | <span data-ttu-id="667e2-213">sztring</span><span class="sxs-lookup"><span data-stu-id="667e2-213">string</span></span>                           | <span data-ttu-id="667e2-214">Egy csoport, amely jelzi, hogy mely elemek helyezhetők el egymásba.</span><span class="sxs-lookup"><span data-stu-id="667e2-214">A group to indicate which items can be placed together.</span></span>                                                                                               |
| <span data-ttu-id="667e2-215">addonItems</span><span class="sxs-lookup"><span data-stu-id="667e2-215">addonItems</span></span>           | <span data-ttu-id="667e2-216">**CartLineItem** -objektumok listája</span><span class="sxs-lookup"><span data-stu-id="667e2-216">List of **CartLineItem** objects</span></span> | <span data-ttu-id="667e2-217">Azon bővítmények gyűjteménye, amelyek az alapelőfizetés azon előfizetéséhez lesznek megvásárolva, amely a fölérendelt cikk megvásárlását eredményezi.</span><span class="sxs-lookup"><span data-stu-id="667e2-217">A collection of cart line items for add-ons that will be purchased towards the base subscription that results from the parent cart line item's purchase.</span></span> |
| <span data-ttu-id="667e2-218">error</span><span class="sxs-lookup"><span data-stu-id="667e2-218">error</span></span>                | <span data-ttu-id="667e2-219">Objektum</span><span class="sxs-lookup"><span data-stu-id="667e2-219">Object</span></span>                           | <span data-ttu-id="667e2-220">A kosár létrehozásakor a rendszer hiba esetén alkalmazza.</span><span class="sxs-lookup"><span data-stu-id="667e2-220">Applied after cart is created in case of an error.</span></span>                                                                                                    |

### <a name="request-example-new-base-subscription"></a><span data-ttu-id="667e2-221">Példa kérésre (új alapszintű előfizetés)</span><span class="sxs-lookup"><span data-stu-id="667e2-221">Request example (new base subscription)</span></span>

<span data-ttu-id="667e2-222">A következő REST-példa azt szemlélteti, hogyan hozható létre egy új alapelőfizetés kiegészítő elemeit tartalmazó kosár.</span><span class="sxs-lookup"><span data-stu-id="667e2-222">The following REST example shows how to create a cart with add-on items for a new base subscription.</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a><span data-ttu-id="667e2-223">Példa kérésre (meglévő alap előfizetés)</span><span class="sxs-lookup"><span data-stu-id="667e2-223">Request example (existing base subscription)</span></span>

<span data-ttu-id="667e2-224">A következő REST-példa azt szemlélteti, hogyan lehet bővítményeket hozzáfűzni egy meglévő alap előfizetéshez.</span><span class="sxs-lookup"><span data-stu-id="667e2-224">The following REST example show how to append add-ons to an existing base subscription.</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="667e2-225">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="667e2-225">REST response</span></span>

<span data-ttu-id="667e2-226">Ha ez sikeres, ez a metódus a válasz törzsében lévő feltöltött [kosár](cart-resources.md) -erőforrást adja vissza.</span><span class="sxs-lookup"><span data-stu-id="667e2-226">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="667e2-227">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="667e2-227">Response success and error codes</span></span>

<span data-ttu-id="667e2-228">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="667e2-228">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="667e2-229">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="667e2-229">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="667e2-230">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="667e2-230">For the full list, see [Error Codes](error-codes.md).</span></span>

#### <a name="response-example-new-base-subscription"></a><span data-ttu-id="667e2-231">Válasz példa (új alapszintű előfizetés)</span><span class="sxs-lookup"><span data-stu-id="667e2-231">Response example (new base subscription)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a><span data-ttu-id="667e2-232">Válasz példa (meglévő alap előfizetés)</span><span class="sxs-lookup"><span data-stu-id="667e2-232">Response example (existing base subscription)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
