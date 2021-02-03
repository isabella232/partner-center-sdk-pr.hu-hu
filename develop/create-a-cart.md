---
title: Kosár létrehozása
description: Ismerje meg, hogy a partner Center API-k Hogyan vehetik igénybe az ügyfelek rendelését egy kosárban. A témakör a kosár létrehozásával és az előfeltételekkel kapcsolatos információkat tartalmaz.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a1c559b415a7d42af4e904e09795f92aed7f125f
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768627"
---
# <a name="create-a-cart-with-a-customer-order"></a><span data-ttu-id="dde64-104">Kosár létrehozása az ügyfél megrendelésével</span><span class="sxs-lookup"><span data-stu-id="dde64-104">Create a cart with a customer order</span></span>

<span data-ttu-id="dde64-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="dde64-105">**Applies to:**</span></span>

- <span data-ttu-id="dde64-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="dde64-106">Partner Center</span></span>
- <span data-ttu-id="dde64-107">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="dde64-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="dde64-108">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="dde64-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="dde64-109">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="dde64-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="dde64-110">Megrendelést adhat egy kosárban lévő ügyfélhez.</span><span class="sxs-lookup"><span data-stu-id="dde64-110">You can add an order for a customer in a cart.</span></span> <span data-ttu-id="dde64-111">További információ az értékesítésre jelenleg elérhető termékekről: [partneri ajánlatok a Cloud Solution Provider programban](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="dde64-111">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dde64-112">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="dde64-112">Prerequisites</span></span>

- <span data-ttu-id="dde64-113">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="dde64-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dde64-114">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="dde64-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="dde64-115">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="dde64-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="dde64-116">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="dde64-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="dde64-117">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="dde64-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="dde64-118">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="dde64-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="dde64-119">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="dde64-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="dde64-120">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="dde64-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="dde64-121">C\#</span><span class="sxs-lookup"><span data-stu-id="dde64-121">C\#</span></span>

<span data-ttu-id="dde64-122">Megrendelés létrehozása az ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="dde64-122">To create an order for a customer:</span></span>

1. <span data-ttu-id="dde64-123">Egy cart-objektum példányának létrehozása.</span><span class="sxs-lookup"><span data-stu-id="dde64-123">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="dde64-124">Hozza létre a **CartLineItem** -objektumok listáját, és rendelje hozzá a listát a kosár listaelemek tulajdonságához.</span><span class="sxs-lookup"><span data-stu-id="dde64-124">Create a list of **CartLineItem** objects, and assign the list to the cart's LineItems property.</span></span> <span data-ttu-id="dde64-125">Minden egyes cart-sor egy termék vásárlási információit tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="dde64-125">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="dde64-126">Legalább egy cart-sorral kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="dde64-126">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="dde64-127">Szerezzen be egy felületet a cart-műveletekhez úgy, hogy meghívja a **IAggregatePartner. customers. ById** metódust az ügyfél-azonosítóval, hogy azonosítsa az ügyfelet, majd beolvassa a felületet a **cart** tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="dde64-127">Obtain an interface to cart operations by calling the **IAggregatePartner.Customers.ById** method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

4. <span data-ttu-id="dde64-128">A kosár létrehozásához hívja meg a **create** vagy a **CreateAsync** metódust.</span><span class="sxs-lookup"><span data-stu-id="dde64-128">Call the **Create** or **CreateAsync** method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="dde64-129">C \# példa</span><span class="sxs-lookup"><span data-stu-id="dde64-129">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

var cart = new Cart()
{
    LineItems = new List<CartLineItem>()
    {
        new CartLineItem()
        {
      /* Microsoft Azure Subscription */
            Id = 0,
            CatalogItemId = "MS-AZR-0145P",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1Y"
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 1,
            CatalogItemId = "DZH318Z0BQ36:004G:DZH318Z08C0S",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P1Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 2,
            CatalogItemId = "DZH318Z0BQ36:004J:DZH318Z08B8X",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P3Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Perpetual Software */
            Id = 3,
            CatalogItemId = "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime
        },
        new CartLineItem()
        {
      /* SaaS */
            Id = 4,
            CatalogItemId = "DZH318Z0BXWC:0002:DZH318Z0BMRV",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1M"
        },
        new CartLineItem()
        {
      /* SaaS Free Trial */
            Id = 5,
            CatalogItemId = "DZH318Z0C0WF:0001:DZH318Z0BP69",
            Quantity = 10,
            BillingCycle = BillingCycleType.None,
            TermDuration = "P1M",
            RenewsTo = new RenewsTo
            {
                TermDuration = "P1Y"
            }
        }
    }
};

cart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

## <a name="java"></a><span data-ttu-id="dde64-130">Java</span><span class="sxs-lookup"><span data-stu-id="dde64-130">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="dde64-131">Megrendelés létrehozása az ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="dde64-131">To create an order for a customer:</span></span>

1. <span data-ttu-id="dde64-132">Egy cart-objektum példányának létrehozása.</span><span class="sxs-lookup"><span data-stu-id="dde64-132">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="dde64-133">Hozzon létre egy listát a **CartLineItem** objektumokról, és rendelje hozzá a listát a kosár sorához.</span><span class="sxs-lookup"><span data-stu-id="dde64-133">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="dde64-134">Minden egyes cart-sor egy termék vásárlási információit tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="dde64-134">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="dde64-135">Legalább egy cart-sorral kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="dde64-135">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="dde64-136">Szerezzen be egy felületet a cart-műveletekhez úgy, hogy meghívja a **IAggregatePartner. getCustomers (). byId** függvényt az ügyfél-azonosítóval, hogy azonosítsa az ügyfelet, majd beolvassa a felületet a **getCart** függvényből.</span><span class="sxs-lookup"><span data-stu-id="dde64-136">Obtain an interface to cart operations by calling the **IAggregatePartner.getCustomers().byId** function with the customer ID to identify the customer, and then retrieving the interface from the **getCart** function.</span></span>

4. <span data-ttu-id="dde64-137">Hívja meg a **create** függvényt a kosár létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="dde64-137">Call the **create** function to create the cart.</span></span>

## <a name="java-example"></a><span data-ttu-id="dde64-138">Java-példa</span><span class="sxs-lookup"><span data-stu-id="dde64-138">Java example</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;
// String catalogItemId;

CartLineItem lineItem = new CartLineItem();

lineItem.setBillingCycle(BillingCycleType.OneTime);
lineItem.setCatalogItemId(catalogItemId);
lineItem.setFriendlyName("Sample RI Purchase");
lineItem.setQuantity(1);

Map<String, String> provisioningContext = new HashMap<String,String>();

provisioningContext.put("duration", "3Years");
provisioningContext.put("scope", "shared");
provisioningContext.put("subscriptionId", subscriptionId);

lineItem.setProvisioningContext(provisioningContext);

List<CartLineItem> lineItemList = new ArrayList<CartLineItem>();
lineItemList.add(lineItem);

Cart cart = new Cart();
cart.setLineItems(lineItemList);

Cart cartCreated = partnerOperations.getCustomers().byId(customerId).getCarts().create(cart);
```

## <a name="powershell"></a><span data-ttu-id="dde64-139">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dde64-139">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="dde64-140">Megrendelés létrehozása az ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="dde64-140">To create an order for a customer:</span></span>

1. <span data-ttu-id="dde64-141">Egy cart-objektum példányának létrehozása.</span><span class="sxs-lookup"><span data-stu-id="dde64-141">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="dde64-142">Hozzon létre egy listát a **CartLineItem** objektumokról, és rendelje hozzá a listát a kosár sorához.</span><span class="sxs-lookup"><span data-stu-id="dde64-142">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="dde64-143">Minden egyes cart-sor egy termék vásárlási információit tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="dde64-143">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="dde64-144">Legalább egy cart-sorral kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="dde64-144">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="dde64-145">Futtassa a [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) parancsot a kosár létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="dde64-145">Execute the [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) command to create the cart.</span></span>

```powershell
# $customerId
# $subscriptionId
# $catalogItemId

$lineItem = New-Object -TypeName Microsoft.Store.PartnerCenter.PowerShell.Models.Carts.PSCartLineItem

$lineItem.BillingCycle = 'OneTime'
$lineItem.CatalogItemId = $catalogItemId
$lineItem.FriendlyName = 'Sample RI Purchase'
$lineItem.ProvisioningContext.Add('duration', '1Year')
$lineItem.ProvisioningContext.Add('scope', 'shared')
$lineItem.ProvisioningContext.Add('subscriptionId', $subsciptionId)
$lineItem.Quantity = 10

New-PartnerCustomerCart -CustomerId $customerId -LineItems $lineItem
```

## <a name="rest-request"></a><span data-ttu-id="dde64-146">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="dde64-146">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dde64-147">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="dde64-147">Request syntax</span></span>

| <span data-ttu-id="dde64-148">Metódus</span><span class="sxs-lookup"><span data-stu-id="dde64-148">Method</span></span>   | <span data-ttu-id="dde64-149">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="dde64-149">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dde64-150">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="dde64-150">**POST**</span></span> | <span data-ttu-id="dde64-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts http/1.1</span><span class="sxs-lookup"><span data-stu-id="dde64-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="dde64-152">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="dde64-152">URI parameter</span></span>

<span data-ttu-id="dde64-153">Az ügyfél azonosításához használja a következő Path paramétert.</span><span class="sxs-lookup"><span data-stu-id="dde64-153">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="dde64-154">Név</span><span class="sxs-lookup"><span data-stu-id="dde64-154">Name</span></span>            | <span data-ttu-id="dde64-155">Típus</span><span class="sxs-lookup"><span data-stu-id="dde64-155">Type</span></span>     | <span data-ttu-id="dde64-156">Kötelező</span><span class="sxs-lookup"><span data-stu-id="dde64-156">Required</span></span> | <span data-ttu-id="dde64-157">Leírás</span><span class="sxs-lookup"><span data-stu-id="dde64-157">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="dde64-158">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="dde64-158">**customer-id**</span></span> | <span data-ttu-id="dde64-159">sztring</span><span class="sxs-lookup"><span data-stu-id="dde64-159">string</span></span>   | <span data-ttu-id="dde64-160">Igen</span><span class="sxs-lookup"><span data-stu-id="dde64-160">Yes</span></span>      | <span data-ttu-id="dde64-161">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="dde64-161">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="dde64-162">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="dde64-162">Request headers</span></span>

<span data-ttu-id="dde64-163">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="dde64-163">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dde64-164">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="dde64-164">Request body</span></span>

<span data-ttu-id="dde64-165">Ez a táblázat a kérés törzsében lévő [kosár](cart-resources.md) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="dde64-165">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="dde64-166">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="dde64-166">Property</span></span>              | <span data-ttu-id="dde64-167">Típus</span><span class="sxs-lookup"><span data-stu-id="dde64-167">Type</span></span>             | <span data-ttu-id="dde64-168">Kötelező</span><span class="sxs-lookup"><span data-stu-id="dde64-168">Required</span></span>        | <span data-ttu-id="dde64-169">Leírás</span><span class="sxs-lookup"><span data-stu-id="dde64-169">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dde64-170">id</span><span class="sxs-lookup"><span data-stu-id="dde64-170">id</span></span>                    | <span data-ttu-id="dde64-171">sztring</span><span class="sxs-lookup"><span data-stu-id="dde64-171">string</span></span>           | <span data-ttu-id="dde64-172">No</span><span class="sxs-lookup"><span data-stu-id="dde64-172">No</span></span>              | <span data-ttu-id="dde64-173">A kosár sikeres létrehozásához megadott cart-azonosító.</span><span class="sxs-lookup"><span data-stu-id="dde64-173">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="dde64-174">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="dde64-174">creationTimeStamp</span></span>     | <span data-ttu-id="dde64-175">DateTime</span><span class="sxs-lookup"><span data-stu-id="dde64-175">DateTime</span></span>         | <span data-ttu-id="dde64-176">Nem</span><span class="sxs-lookup"><span data-stu-id="dde64-176">No</span></span>              | <span data-ttu-id="dde64-177">A kosár létrehozásának dátuma dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="dde64-177">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="dde64-178">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="dde64-178">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="dde64-179">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="dde64-179">lastModifiedTimeStamp</span></span> | <span data-ttu-id="dde64-180">DateTime</span><span class="sxs-lookup"><span data-stu-id="dde64-180">DateTime</span></span>         | <span data-ttu-id="dde64-181">Nem</span><span class="sxs-lookup"><span data-stu-id="dde64-181">No</span></span>              | <span data-ttu-id="dde64-182">A kosár utolsó frissítésének dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="dde64-182">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="dde64-183">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="dde64-183">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="dde64-184">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="dde64-184">expirationTimeStamp</span></span>   | <span data-ttu-id="dde64-185">DateTime</span><span class="sxs-lookup"><span data-stu-id="dde64-185">DateTime</span></span>         | <span data-ttu-id="dde64-186">Nem</span><span class="sxs-lookup"><span data-stu-id="dde64-186">No</span></span>              | <span data-ttu-id="dde64-187">A kosár lejáratának dátuma dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="dde64-187">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="dde64-188">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="dde64-188">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="dde64-189">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="dde64-189">lastModifiedUser</span></span>      | <span data-ttu-id="dde64-190">sztring</span><span class="sxs-lookup"><span data-stu-id="dde64-190">string</span></span>           | <span data-ttu-id="dde64-191">No</span><span class="sxs-lookup"><span data-stu-id="dde64-191">No</span></span>              | <span data-ttu-id="dde64-192">A kosár utolsó frissítését végző felhasználó.</span><span class="sxs-lookup"><span data-stu-id="dde64-192">The user who last updated the cart.</span></span> <span data-ttu-id="dde64-193">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="dde64-193">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="dde64-194">Listaelemek</span><span class="sxs-lookup"><span data-stu-id="dde64-194">lineItems</span></span>             | <span data-ttu-id="dde64-195">Objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="dde64-195">Array of objects</span></span> | <span data-ttu-id="dde64-196">Igen</span><span class="sxs-lookup"><span data-stu-id="dde64-196">Yes</span></span>             | <span data-ttu-id="dde64-197">[CartLineItem](cart-resources.md#cartlineitem) -erőforrások tömbje.</span><span class="sxs-lookup"><span data-stu-id="dde64-197">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                     |

<span data-ttu-id="dde64-198">Ez a táblázat a kérelem törzsének [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="dde64-198">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="dde64-199">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="dde64-199">Property</span></span>       |            <span data-ttu-id="dde64-200">Típus</span><span class="sxs-lookup"><span data-stu-id="dde64-200">Type</span></span>             | <span data-ttu-id="dde64-201">Kötelező</span><span class="sxs-lookup"><span data-stu-id="dde64-201">Required</span></span> |                                                                                         <span data-ttu-id="dde64-202">Leírás</span><span class="sxs-lookup"><span data-stu-id="dde64-202">Description</span></span>                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         <span data-ttu-id="dde64-203">id</span><span class="sxs-lookup"><span data-stu-id="dde64-203">id</span></span>          |           <span data-ttu-id="dde64-204">sztring</span><span class="sxs-lookup"><span data-stu-id="dde64-204">string</span></span>            |    <span data-ttu-id="dde64-205">No</span><span class="sxs-lookup"><span data-stu-id="dde64-205">No</span></span>    |                                                     <span data-ttu-id="dde64-206">Egy cart-sor egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="dde64-206">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="dde64-207">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="dde64-207">Applied upon successful creation of cart.</span></span>                                                     |
|      <span data-ttu-id="dde64-208">catalogId</span><span class="sxs-lookup"><span data-stu-id="dde64-208">catalogId</span></span>      |           <span data-ttu-id="dde64-209">sztring</span><span class="sxs-lookup"><span data-stu-id="dde64-209">string</span></span>            |   <span data-ttu-id="dde64-210">Igen</span><span class="sxs-lookup"><span data-stu-id="dde64-210">Yes</span></span>    |                                                                                <span data-ttu-id="dde64-211">A katalógus-elemek azonosítója.</span><span class="sxs-lookup"><span data-stu-id="dde64-211">The catalog item identifier.</span></span>                                                                                 |
|    <span data-ttu-id="dde64-212">friendlyName</span><span class="sxs-lookup"><span data-stu-id="dde64-212">friendlyName</span></span>     |           <span data-ttu-id="dde64-213">sztring</span><span class="sxs-lookup"><span data-stu-id="dde64-213">string</span></span>            |    <span data-ttu-id="dde64-214">No</span><span class="sxs-lookup"><span data-stu-id="dde64-214">No</span></span>    |                                                    <span data-ttu-id="dde64-215">Választható.</span><span class="sxs-lookup"><span data-stu-id="dde64-215">Optional.</span></span> <span data-ttu-id="dde64-216">A partner által a egyértelműsítse segítségére meghatározott rövid név.</span><span class="sxs-lookup"><span data-stu-id="dde64-216">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                    |
|      <span data-ttu-id="dde64-217">quantity</span><span class="sxs-lookup"><span data-stu-id="dde64-217">quantity</span></span>       |             <span data-ttu-id="dde64-218">int</span><span class="sxs-lookup"><span data-stu-id="dde64-218">int</span></span>             |   <span data-ttu-id="dde64-219">Igen</span><span class="sxs-lookup"><span data-stu-id="dde64-219">Yes</span></span>    |                                                                            <span data-ttu-id="dde64-220">A licencek vagy példányok száma.</span><span class="sxs-lookup"><span data-stu-id="dde64-220">The number of licenses or instances.</span></span>                                                                             |
|    <span data-ttu-id="dde64-221">currencyCode</span><span class="sxs-lookup"><span data-stu-id="dde64-221">currencyCode</span></span>     |           <span data-ttu-id="dde64-222">sztring</span><span class="sxs-lookup"><span data-stu-id="dde64-222">string</span></span>            |    <span data-ttu-id="dde64-223">No</span><span class="sxs-lookup"><span data-stu-id="dde64-223">No</span></span>    |                                                                                     <span data-ttu-id="dde64-224">A Pénznemkód.</span><span class="sxs-lookup"><span data-stu-id="dde64-224">The currency code.</span></span>                                                                                      |
|    <span data-ttu-id="dde64-225">billingCycle</span><span class="sxs-lookup"><span data-stu-id="dde64-225">billingCycle</span></span>     |           <span data-ttu-id="dde64-226">Objektum</span><span class="sxs-lookup"><span data-stu-id="dde64-226">Object</span></span>            |   <span data-ttu-id="dde64-227">Igen</span><span class="sxs-lookup"><span data-stu-id="dde64-227">Yes</span></span>    |                                                                    <span data-ttu-id="dde64-228">Az aktuális időszakban beállított számlázási ciklus típusa.</span><span class="sxs-lookup"><span data-stu-id="dde64-228">The type of billing cycle set for the current period.</span></span>                                                                    |
|    <span data-ttu-id="dde64-229">résztvevők</span><span class="sxs-lookup"><span data-stu-id="dde64-229">participants</span></span>     | <span data-ttu-id="dde64-230">Az Object string párok listája</span><span class="sxs-lookup"><span data-stu-id="dde64-230">List of Object String pairs</span></span> |    <span data-ttu-id="dde64-231">Nem</span><span class="sxs-lookup"><span data-stu-id="dde64-231">No</span></span>    |                                                                <span data-ttu-id="dde64-232">A PartnerId on Record (MPNID) gyűjteménye a vásárláson.</span><span class="sxs-lookup"><span data-stu-id="dde64-232">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                 |
| <span data-ttu-id="dde64-233">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="dde64-233">provisioningContext</span></span> | <span data-ttu-id="dde64-234">Szótár<karakterlánc, karakterlánc></span><span class="sxs-lookup"><span data-stu-id="dde64-234">Dictionary<string, string></span></span>  |    <span data-ttu-id="dde64-235">Nem</span><span class="sxs-lookup"><span data-stu-id="dde64-235">No</span></span>    | <span data-ttu-id="dde64-236">A katalógus egyes elemeinek kiépítési feladataihoz szükséges információk.</span><span class="sxs-lookup"><span data-stu-id="dde64-236">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="dde64-237">Az SKU provisioningVariables tulajdonsága azt jelzi, hogy mely tulajdonságok szükségesek a katalógus adott elemeihez.</span><span class="sxs-lookup"><span data-stu-id="dde64-237">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span> |
|     <span data-ttu-id="dde64-238">orderGroup</span><span class="sxs-lookup"><span data-stu-id="dde64-238">orderGroup</span></span>      |           <span data-ttu-id="dde64-239">sztring</span><span class="sxs-lookup"><span data-stu-id="dde64-239">string</span></span>            |    <span data-ttu-id="dde64-240">No</span><span class="sxs-lookup"><span data-stu-id="dde64-240">No</span></span>    |                                                                   <span data-ttu-id="dde64-241">Egy csoport, amely jelzi, hogy mely elemek helyezhetők el egymásba.</span><span class="sxs-lookup"><span data-stu-id="dde64-241">A group to indicate which items can be placed together.</span></span>                                                                   |
|        <span data-ttu-id="dde64-242">error</span><span class="sxs-lookup"><span data-stu-id="dde64-242">error</span></span>        |           <span data-ttu-id="dde64-243">Objektum</span><span class="sxs-lookup"><span data-stu-id="dde64-243">Object</span></span>            |    <span data-ttu-id="dde64-244">Nem</span><span class="sxs-lookup"><span data-stu-id="dde64-244">No</span></span>    |                                                                     <span data-ttu-id="dde64-245">A kosár létrehozásakor a rendszer hiba esetén alkalmazza.</span><span class="sxs-lookup"><span data-stu-id="dde64-245">Applied after cart is created in case of an error.</span></span>                                                                      |
|     <span data-ttu-id="dde64-246">renewsTo</span><span class="sxs-lookup"><span data-stu-id="dde64-246">renewsTo</span></span>        | <span data-ttu-id="dde64-247">Objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="dde64-247">Array of objects</span></span>            |    <span data-ttu-id="dde64-248">Nem</span><span class="sxs-lookup"><span data-stu-id="dde64-248">No</span></span>    |                                                    <span data-ttu-id="dde64-249">[RenewsTo](cart-resources.md#renewsto) -erőforrások tömbje.</span><span class="sxs-lookup"><span data-stu-id="dde64-249">An array of [RenewsTo](cart-resources.md#renewsto) resources.</span></span>                                                                            |

<span data-ttu-id="dde64-250">Ez a táblázat a kérelem törzsének [RenewsTo](cart-resources.md#renewsto) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="dde64-250">This table describes the [RenewsTo](cart-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="dde64-251">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="dde64-251">Property</span></span>              | <span data-ttu-id="dde64-252">Típus</span><span class="sxs-lookup"><span data-stu-id="dde64-252">Type</span></span>             | <span data-ttu-id="dde64-253">Kötelező</span><span class="sxs-lookup"><span data-stu-id="dde64-253">Required</span></span>        | <span data-ttu-id="dde64-254">Leírás</span><span class="sxs-lookup"><span data-stu-id="dde64-254">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dde64-255">termDuration</span><span class="sxs-lookup"><span data-stu-id="dde64-255">termDuration</span></span>          | <span data-ttu-id="dde64-256">sztring</span><span class="sxs-lookup"><span data-stu-id="dde64-256">string</span></span>           | <span data-ttu-id="dde64-257">No</span><span class="sxs-lookup"><span data-stu-id="dde64-257">No</span></span>              | <span data-ttu-id="dde64-258">A megújítási időszak érvényességének ISO 8601-es ábrázolása.</span><span class="sxs-lookup"><span data-stu-id="dde64-258">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="dde64-259">A jelenleg támogatott értékek a következők: **P1M** (1 hónap) és **P1Y** (1 év).</span><span class="sxs-lookup"><span data-stu-id="dde64-259">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="dde64-260">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="dde64-260">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
  "lineItems": [
    {
    /* Microsoft Azure Subscription */
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1Y"
    },
    {
    /* Azure Reserved Instance */
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      }
    },
    {
    /* Azure Reserved Instance */
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "single"
      }
    },
    {
    /* Perpetual Software */
      "id": 3,
      "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSFM",
      "quantity": 1,
      "billingCycle": "one_time"
    },
    {
    /* SaaS */
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1M"
    },
  {
    /* SaaS Free Trial */
       "id": 5,
       "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
       "quantity": 10,
       "billingCycle": "none",
       "termDuration": "P1M",
       "renewsTo": {
         "termDuration": "P1Y"
       }
    }
  ]
}
```

## <a name="rest-response"></a><span data-ttu-id="dde64-261">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="dde64-261">REST response</span></span>

<span data-ttu-id="dde64-262">Ha ez sikeres, ez a metódus a válasz törzsében lévő feltöltött [kosár](cart-resources.md) -erőforrást adja vissza.</span><span class="sxs-lookup"><span data-stu-id="dde64-262">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dde64-263">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="dde64-263">Response success and error codes</span></span>

<span data-ttu-id="dde64-264">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="dde64-264">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dde64-265">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="dde64-265">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dde64-266">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dde64-266">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dde64-267">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="dde64-267">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
  "id": "3655b1a0-b1c9-4268-9824-577fdbc4d0be",
  "creationTimestamp": "2019-01-16T00:45:41.6062996Z",
  "lastModifiedTimestamp": "2019-01-16T00:45:41.6062996Z",
  "expirationTimestamp": "2019-01-16T01:00:54.4188497Z",
  "lastModifiedUser": "1824b7fc-2fac-4478-b177-66823c40ab75",
  "status": "Active",
  "lineItems": [
    {
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1Y",
      "orderGroup": "OMS-0"
    },
    {
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 3,
      "catalogItemId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "orderGroup": "0"
    },
    {
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1M",
      "orderGroup": "1"
    },
  {
      "id": 5,
      "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
      "quantity": 10,
      "currencyCode": "USD",
      "billingCycle": "none",
      "termDuration": "P1M",
      "renewsTo": {
  "termDuration": "P1Y"
      },
    "orderGroup": "2"
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/28045616-f6b9-462f-9701-0d89b5e65c44/carts/3655b1a0-b1c9-4268-9824-577fdbc4d0be",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Cart"
  }
}
```
