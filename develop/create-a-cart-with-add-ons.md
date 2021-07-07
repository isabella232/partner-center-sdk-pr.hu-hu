---
title: Kosár létrehozása bővítményekkel
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat arra, hogy hozzáadja az ügyfélrendeléseket bővítmények segítségével egy kosárban. A cikk a bővítményeket is hozzátenő kosár létrehozásához szükséges előfeltételeket és lépéseket osztja meg.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 513a9607b9194c36253630c91de9622325317c3a
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973757"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a><span data-ttu-id="486f9-104">Bevásárlókocsi létrehozása az ügyfélrendeléshez szükséges bővítményekkel</span><span class="sxs-lookup"><span data-stu-id="486f9-104">Create a cart with add-ons to a customer order</span></span>

<span data-ttu-id="486f9-105">A bővítményeket kosárban vásárolhatja meg.</span><span class="sxs-lookup"><span data-stu-id="486f9-105">You can purchase add-ons through a cart.</span></span> <span data-ttu-id="486f9-106">Az aktuálisan értékesíthető ajánlatokkal kapcsolatos további információkért lásd a partneri [ajánlatokat a Felhőszolgáltató programjában.](/partner-center/csp-offers)</span><span class="sxs-lookup"><span data-stu-id="486f9-106">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="486f9-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="486f9-107">Prerequisites</span></span>

- <span data-ttu-id="486f9-108">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="486f9-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="486f9-109">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="486f9-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="486f9-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="486f9-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="486f9-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="486f9-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="486f9-112">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="486f9-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="486f9-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="486f9-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="486f9-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="486f9-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="486f9-115">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="486f9-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="486f9-116">C\#</span><span class="sxs-lookup"><span data-stu-id="486f9-116">C\#</span></span>

<span data-ttu-id="486f9-117">A kosár lehetővé teszi egy alapajánlat és a hozzá tartozó bővítmények megvásárlását.</span><span class="sxs-lookup"><span data-stu-id="486f9-117">A cart enables the purchase of a base offer and its corresponding add-ons.</span></span> <span data-ttu-id="486f9-118">A kosár létrehozásához kövesse az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="486f9-118">Follow these steps to create a cart:</span></span>

1. <span data-ttu-id="486f9-119">Cart-objektum [**példányosodása.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart)</span><span class="sxs-lookup"><span data-stu-id="486f9-119">Instantiate a [**Cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) object.</span></span>

2. <span data-ttu-id="486f9-120">Hozzon létre egy listát a [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objektumokról, amelyek az alapajánlat(okat) képviselik, és rendelje hozzá a listát a kosár [**LineItems (Soritemek) tulajdonságához.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems)</span><span class="sxs-lookup"><span data-stu-id="486f9-120">Create a list of [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objects that represent the base offer(s), and assign the list to the cart's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) property.</span></span>

3. <span data-ttu-id="486f9-121">Az alapajánlatok kocsisorelemei alatt töltse fel az **AddOnItems** (Hozzáadások) listáját más **CartLineItem** objektumokkal, amelyek mindegyike egy-egy bővítményt képvisel, és amely az adott alapajánlathoz lesz megvásárolva.</span><span class="sxs-lookup"><span data-stu-id="486f9-121">Under each base offer's cart line item, populate the list of **AddOnItems** with other **CartLineItem** objects that each represent an add-on that will be purchased against that base offer.</span></span>

4. <span data-ttu-id="486f9-122">Szerezzen be egy interfészt a kosaras műveletekhez az [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) használatával, hogy az ügyfél azonosítójával hívja meg az [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosításához, majd lehívja a felületet a **Cart** tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="486f9-122">Obtain an interface to cart operations by using [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) to call the [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

5. <span data-ttu-id="486f9-123">Végül hívja meg a [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) vagy [**CreateAsync metódust**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) a kosár létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="486f9-123">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="486f9-124">C \# példa</span><span class="sxs-lookup"><span data-stu-id="486f9-124">C\# example</span></span>

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

<span data-ttu-id="486f9-125">Kövesse az alábbi lépéseket egy olyan kosár létrehozásához, amely lehetővé teszi bővítmények vásárlását a meglévő alap-előfizetés(ekkel) szemben:</span><span class="sxs-lookup"><span data-stu-id="486f9-125">Follow these steps to create a cart that will enable the purchase of add-on(s) against existing base subscription(s):</span></span>

1. <span data-ttu-id="486f9-126">Hozzon  létre egy új **CartLineItem** kosarat, amely tartalmazza az előfizetés azonosítóját a **ProvisioningContext** tulajdonságban a "ParentSubscriptionId" kulccsal.</span><span class="sxs-lookup"><span data-stu-id="486f9-126">Create a **Cart** with a new **CartLineItem** containing the subscription ID in the **ProvisioningContext** property with key "ParentSubscriptionId".</span></span>

2. <span data-ttu-id="486f9-127">Hívja meg a **Create** vagy **CreateAsync metódust.**</span><span class="sxs-lookup"><span data-stu-id="486f9-127">Call the **Create** or **CreateAsync** method.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="486f9-128">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="486f9-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="486f9-129">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="486f9-129">Request syntax</span></span>

| <span data-ttu-id="486f9-130">Metódus</span><span class="sxs-lookup"><span data-stu-id="486f9-130">Method</span></span>   | <span data-ttu-id="486f9-131">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="486f9-131">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="486f9-132">**Post**</span><span class="sxs-lookup"><span data-stu-id="486f9-132">**POST**</span></span> | <span data-ttu-id="486f9-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfél-azonosító}/carts HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="486f9-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

#### <a name="uri-parameter"></a><span data-ttu-id="486f9-134">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="486f9-134">URI parameter</span></span>

<span data-ttu-id="486f9-135">Az ügyfél azonosításához használja a következő path paramétert.</span><span class="sxs-lookup"><span data-stu-id="486f9-135">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="486f9-136">Név</span><span class="sxs-lookup"><span data-stu-id="486f9-136">Name</span></span>            | <span data-ttu-id="486f9-137">Típus</span><span class="sxs-lookup"><span data-stu-id="486f9-137">Type</span></span>     | <span data-ttu-id="486f9-138">Kötelező</span><span class="sxs-lookup"><span data-stu-id="486f9-138">Required</span></span> | <span data-ttu-id="486f9-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="486f9-139">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="486f9-140">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="486f9-140">**customer-id**</span></span> | <span data-ttu-id="486f9-141">sztring</span><span class="sxs-lookup"><span data-stu-id="486f9-141">string</span></span>   | <span data-ttu-id="486f9-142">Igen</span><span class="sxs-lookup"><span data-stu-id="486f9-142">Yes</span></span>      | <span data-ttu-id="486f9-143">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="486f9-143">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="486f9-144">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="486f9-144">Request headers</span></span>

<span data-ttu-id="486f9-145">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="486f9-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="486f9-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="486f9-146">Request body</span></span>

<span data-ttu-id="486f9-147">Ez a táblázat a kocsi [tulajdonságait ismerteti](cart-resources.md) a kérés törzsében.</span><span class="sxs-lookup"><span data-stu-id="486f9-147">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="486f9-148">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="486f9-148">Property</span></span>              | <span data-ttu-id="486f9-149">Típus</span><span class="sxs-lookup"><span data-stu-id="486f9-149">Type</span></span>             | <span data-ttu-id="486f9-150">Kötelező</span><span class="sxs-lookup"><span data-stu-id="486f9-150">Required</span></span>        | <span data-ttu-id="486f9-151">Leírás</span><span class="sxs-lookup"><span data-stu-id="486f9-151">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="486f9-152">id</span><span class="sxs-lookup"><span data-stu-id="486f9-152">id</span></span>                    | <span data-ttu-id="486f9-153">sztring</span><span class="sxs-lookup"><span data-stu-id="486f9-153">string</span></span>           | <span data-ttu-id="486f9-154">No</span><span class="sxs-lookup"><span data-stu-id="486f9-154">No</span></span>              | <span data-ttu-id="486f9-155">A kosár sikeres létrehozása után megadott bevásárlókocsi-azonosító.</span><span class="sxs-lookup"><span data-stu-id="486f9-155">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="486f9-156">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="486f9-156">creationTimeStamp</span></span>     | <span data-ttu-id="486f9-157">DateTime</span><span class="sxs-lookup"><span data-stu-id="486f9-157">DateTime</span></span>         | <span data-ttu-id="486f9-158">Nem</span><span class="sxs-lookup"><span data-stu-id="486f9-158">No</span></span>              | <span data-ttu-id="486f9-159">A kosár létrehozási dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="486f9-159">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="486f9-160">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="486f9-160">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="486f9-161">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="486f9-161">lastModifiedTimeStamp</span></span> | <span data-ttu-id="486f9-162">DateTime</span><span class="sxs-lookup"><span data-stu-id="486f9-162">DateTime</span></span>         | <span data-ttu-id="486f9-163">Nem</span><span class="sxs-lookup"><span data-stu-id="486f9-163">No</span></span>              | <span data-ttu-id="486f9-164">A kosár legutóbbi frissítésének dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="486f9-164">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="486f9-165">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="486f9-165">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="486f9-166">expirationTimeStamp (lejárat ideje)</span><span class="sxs-lookup"><span data-stu-id="486f9-166">expirationTimeStamp</span></span>   | <span data-ttu-id="486f9-167">DateTime</span><span class="sxs-lookup"><span data-stu-id="486f9-167">DateTime</span></span>         | <span data-ttu-id="486f9-168">Nem</span><span class="sxs-lookup"><span data-stu-id="486f9-168">No</span></span>              | <span data-ttu-id="486f9-169">A kosár lejáratának dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="486f9-169">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="486f9-170">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="486f9-170">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="486f9-171">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="486f9-171">lastModifiedUser</span></span>      | <span data-ttu-id="486f9-172">sztring</span><span class="sxs-lookup"><span data-stu-id="486f9-172">string</span></span>           | <span data-ttu-id="486f9-173">No</span><span class="sxs-lookup"><span data-stu-id="486f9-173">No</span></span>              | <span data-ttu-id="486f9-174">Az a felhasználó, aki utoljára frissítette a kosárat.</span><span class="sxs-lookup"><span data-stu-id="486f9-174">The user who last updated the cart.</span></span> <span data-ttu-id="486f9-175">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="486f9-175">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="486f9-176">lineItems (sorsorok)</span><span class="sxs-lookup"><span data-stu-id="486f9-176">lineItems</span></span>             | <span data-ttu-id="486f9-177">Objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="486f9-177">Array of objects</span></span> | <span data-ttu-id="486f9-178">Igen</span><span class="sxs-lookup"><span data-stu-id="486f9-178">Yes</span></span>             | <span data-ttu-id="486f9-179">[CartLineItem-erőforrások tömbje.](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="486f9-179">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                             |

<span data-ttu-id="486f9-180">Ez a táblázat a [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait ismerteti a kérés törzsében.</span><span class="sxs-lookup"><span data-stu-id="486f9-180">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="486f9-181">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="486f9-181">Property</span></span>             | <span data-ttu-id="486f9-182">Típus</span><span class="sxs-lookup"><span data-stu-id="486f9-182">Type</span></span>                             | <span data-ttu-id="486f9-183">Leírás</span><span class="sxs-lookup"><span data-stu-id="486f9-183">Description</span></span>                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="486f9-184">id</span><span class="sxs-lookup"><span data-stu-id="486f9-184">id</span></span>                   | <span data-ttu-id="486f9-185">sztring</span><span class="sxs-lookup"><span data-stu-id="486f9-185">string</span></span>                           | <span data-ttu-id="486f9-186">A kosársorelem egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="486f9-186">A unique identifier for a cart line item.</span></span> <span data-ttu-id="486f9-187">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="486f9-187">Applied upon successful creation of cart.</span></span>                                                                   |
| <span data-ttu-id="486f9-188">catalogId (katalógusazonosító)</span><span class="sxs-lookup"><span data-stu-id="486f9-188">catalogId</span></span>            | <span data-ttu-id="486f9-189">sztring</span><span class="sxs-lookup"><span data-stu-id="486f9-189">string</span></span>                           | <span data-ttu-id="486f9-190">A katalóguselem azonosítója.</span><span class="sxs-lookup"><span data-stu-id="486f9-190">The catalog item identifier.</span></span>                                                                                                                          |
| <span data-ttu-id="486f9-191">friendlyName (rövid név)</span><span class="sxs-lookup"><span data-stu-id="486f9-191">friendlyName</span></span>         | <span data-ttu-id="486f9-192">sztring</span><span class="sxs-lookup"><span data-stu-id="486f9-192">string</span></span>                           | <span data-ttu-id="486f9-193">Választható.</span><span class="sxs-lookup"><span data-stu-id="486f9-193">Optional.</span></span> <span data-ttu-id="486f9-194">A partner által meghatározott elem rövid neve, amely segít az egyértelműsségben.</span><span class="sxs-lookup"><span data-stu-id="486f9-194">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                                 |
| <span data-ttu-id="486f9-195">quantity</span><span class="sxs-lookup"><span data-stu-id="486f9-195">quantity</span></span>             | <span data-ttu-id="486f9-196">int</span><span class="sxs-lookup"><span data-stu-id="486f9-196">int</span></span>                              | <span data-ttu-id="486f9-197">A licencek vagy példányok száma.</span><span class="sxs-lookup"><span data-stu-id="486f9-197">The number of licenses or instances.</span></span>                                                                                                                  |
| <span data-ttu-id="486f9-198">currencyCode</span><span class="sxs-lookup"><span data-stu-id="486f9-198">currencyCode</span></span>         | <span data-ttu-id="486f9-199">sztring</span><span class="sxs-lookup"><span data-stu-id="486f9-199">string</span></span>                           | <span data-ttu-id="486f9-200">A pénznemkód.</span><span class="sxs-lookup"><span data-stu-id="486f9-200">The currency code.</span></span>                                                                                                                                    |
| <span data-ttu-id="486f9-201">billingCycle</span><span class="sxs-lookup"><span data-stu-id="486f9-201">billingCycle</span></span>         | <span data-ttu-id="486f9-202">Objektum</span><span class="sxs-lookup"><span data-stu-id="486f9-202">Object</span></span>                           | <span data-ttu-id="486f9-203">Az aktuális időszakra beállított számlázási ciklus típusa.</span><span class="sxs-lookup"><span data-stu-id="486f9-203">The type of billing cycle set for the current period.</span></span>                                                                                                 |
| <span data-ttu-id="486f9-204">Résztvevők</span><span class="sxs-lookup"><span data-stu-id="486f9-204">participants</span></span>         | <span data-ttu-id="486f9-205">Objektumsring-párok listája</span><span class="sxs-lookup"><span data-stu-id="486f9-205">List of Object String pairs</span></span>      | <span data-ttu-id="486f9-206">PartnerAzonosító gyűjtemény a vásárláskor rekordban (MPN-azonosító).</span><span class="sxs-lookup"><span data-stu-id="486f9-206">A collection of PartnerId on Record (MPN ID) on the purchase.</span></span>                                                                                          |
| <span data-ttu-id="486f9-207">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="486f9-207">provisioningContext</span></span>  | <span data-ttu-id="486f9-208">Dictionary<string, string></span><span class="sxs-lookup"><span data-stu-id="486f9-208">Dictionary<string, string></span></span>       | <span data-ttu-id="486f9-209">Az ajánlat építéshez használt környezet.</span><span class="sxs-lookup"><span data-stu-id="486f9-209">A context used for provisioning of offer.</span></span>                                                                                                             |
| <span data-ttu-id="486f9-210">orderGroup</span><span class="sxs-lookup"><span data-stu-id="486f9-210">orderGroup</span></span>           | <span data-ttu-id="486f9-211">sztring</span><span class="sxs-lookup"><span data-stu-id="486f9-211">string</span></span>                           | <span data-ttu-id="486f9-212">Egy csoport, amely jelzi, hogy mely elemek helyezhetők el együtt.</span><span class="sxs-lookup"><span data-stu-id="486f9-212">A group to indicate which items can be placed together.</span></span>                                                                                               |
| <span data-ttu-id="486f9-213">addonItems (bővítmények)</span><span class="sxs-lookup"><span data-stu-id="486f9-213">addonItems</span></span>           | <span data-ttu-id="486f9-214">**CartLineItem-objektumok** listája</span><span class="sxs-lookup"><span data-stu-id="486f9-214">List of **CartLineItem** objects</span></span> | <span data-ttu-id="486f9-215">A kosársorelemek gyűjteménye bővítményekhez, amelyek a szülőkocsisor tételének megvásárlásából származó alap előfizetéshez lesznek megvásárolva.</span><span class="sxs-lookup"><span data-stu-id="486f9-215">A collection of cart line items for add-ons that will be purchased towards the base subscription that results from the parent cart line item's purchase.</span></span> |
| <span data-ttu-id="486f9-216">error</span><span class="sxs-lookup"><span data-stu-id="486f9-216">error</span></span>                | <span data-ttu-id="486f9-217">Objektum</span><span class="sxs-lookup"><span data-stu-id="486f9-217">Object</span></span>                           | <span data-ttu-id="486f9-218">A kocsi létrehozása után lesz alkalmazva, ha hiba történik.</span><span class="sxs-lookup"><span data-stu-id="486f9-218">Applied after cart is created if there is an error.</span></span>                                                                                                    |

### <a name="request-example-new-base-subscription"></a><span data-ttu-id="486f9-219">Példakérés (új alap előfizetés)</span><span class="sxs-lookup"><span data-stu-id="486f9-219">Request example (new base subscription)</span></span>

<span data-ttu-id="486f9-220">Az alábbi REST-példa bemutatja, hogyan hozhat létre egy új alap-előfizetéshez bővítményt is a kosárban.</span><span class="sxs-lookup"><span data-stu-id="486f9-220">The following REST example shows how to create a cart with add-on items for a new base subscription.</span></span>

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

#### <a name="request-example-existing-base-subscription"></a><span data-ttu-id="486f9-221">Példakérés (meglévő alap előfizetés)</span><span class="sxs-lookup"><span data-stu-id="486f9-221">Request example (existing base subscription)</span></span>

<span data-ttu-id="486f9-222">Az alábbi REST-példa bemutatja, hogyan fűzhet bővítményeket egy meglévő alap előfizetéshez.</span><span class="sxs-lookup"><span data-stu-id="486f9-222">The following REST example shows how to append add-ons to an existing base subscription.</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="486f9-223">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="486f9-223">REST response</span></span>

<span data-ttu-id="486f9-224">Ha ez a módszer sikeres, a válasz törzsében adja vissza a megadott [Cart](cart-resources.md) erőforrást.</span><span class="sxs-lookup"><span data-stu-id="486f9-224">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="486f9-225">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="486f9-225">Response success and error codes</span></span>

<span data-ttu-id="486f9-226">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="486f9-226">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="486f9-227">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="486f9-227">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="486f9-228">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="486f9-228">For the full list, see [Error Codes](error-codes.md).</span></span>

#### <a name="response-example-new-base-subscription"></a><span data-ttu-id="486f9-229">Válasz példa (új alap előfizetés)</span><span class="sxs-lookup"><span data-stu-id="486f9-229">Response example (new base subscription)</span></span>

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

#### <a name="response-example-existing-base-subscription"></a><span data-ttu-id="486f9-230">Válasz példa (meglévő alap előfizetés)</span><span class="sxs-lookup"><span data-stu-id="486f9-230">Response example (existing base subscription)</span></span>

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
