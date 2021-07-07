---
title: Kosár létrehozása
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat egy ügyfél megrendelésének kosárba való felvételhez. A témakör információkat tartalmaz a kosár létrehozásáról és az előfeltételekről.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: dba54d4f6b97f3d0a51e2f87b32edca686466b89
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973774"
---
# <a name="create-a-cart-with-a-customer-order"></a><span data-ttu-id="d3fee-104">Kosár létrehozása ügyfélrendeléssel</span><span class="sxs-lookup"><span data-stu-id="d3fee-104">Create a cart with a customer order</span></span>

<span data-ttu-id="d3fee-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d3fee-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d3fee-106">Egy ügyfél megrendelését kosárban is hozzáadhatja.</span><span class="sxs-lookup"><span data-stu-id="d3fee-106">You can add an order for a customer in a cart.</span></span> <span data-ttu-id="d3fee-107">A jelenleg értékesíthető adatokkal kapcsolatos további információkért lásd a partneri ajánlatokat a [Felhőszolgáltató programjában.](/partner-center/csp-offers)</span><span class="sxs-lookup"><span data-stu-id="d3fee-107">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3fee-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d3fee-108">Prerequisites</span></span>

- <span data-ttu-id="d3fee-109">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d3fee-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d3fee-110">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="d3fee-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d3fee-111">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d3fee-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d3fee-112">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d3fee-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d3fee-113">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d3fee-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d3fee-114">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d3fee-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d3fee-115">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="d3fee-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d3fee-116">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d3fee-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="d3fee-117">C\#</span><span class="sxs-lookup"><span data-stu-id="d3fee-117">C\#</span></span>

<span data-ttu-id="d3fee-118">Rendelés létrehozása egy ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="d3fee-118">To create an order for a customer:</span></span>

1. <span data-ttu-id="d3fee-119">Cart-objektum példányosodása.</span><span class="sxs-lookup"><span data-stu-id="d3fee-119">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="d3fee-120">Hozza létre a **CartLineItem** objektumok listáját, és rendelje hozzá a listát a kosár LineItems (Soritemek) tulajdonságához.</span><span class="sxs-lookup"><span data-stu-id="d3fee-120">Create a list of **CartLineItem** objects, and assign the list to the cart's LineItems property.</span></span> <span data-ttu-id="d3fee-121">Minden kosársorelem egy adott termék vásárlási adatait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="d3fee-121">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="d3fee-122">Legalább egy kocsisorelemnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="d3fee-122">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="d3fee-123">A kosárműveleteket úgy szerezheti be, ha az ügyfél azonosítójával hívja meg az **IAggregatePartner.Customers.ById** metódust az ügyfél azonosításához, majd lehívja a felületet a **Cart** tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="d3fee-123">Obtain an interface to cart operations by calling the **IAggregatePartner.Customers.ById** method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

4. <span data-ttu-id="d3fee-124">A **kosár létrehozásához** hívja meg a **Create vagy a CreateAsync** metódust.</span><span class="sxs-lookup"><span data-stu-id="d3fee-124">Call the **Create** or **CreateAsync** method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="d3fee-125">C \# példa</span><span class="sxs-lookup"><span data-stu-id="d3fee-125">C\# example</span></span>

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

## <a name="java"></a><span data-ttu-id="d3fee-126">Java</span><span class="sxs-lookup"><span data-stu-id="d3fee-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="d3fee-127">Rendelés létrehozása egy ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="d3fee-127">To create an order for a customer:</span></span>

1. <span data-ttu-id="d3fee-128">Cart-objektum példányosodása.</span><span class="sxs-lookup"><span data-stu-id="d3fee-128">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="d3fee-129">Hozza létre a **CartLineItem** objektumok listáját, és rendelje hozzá a listát a kosár sorelemekhez.</span><span class="sxs-lookup"><span data-stu-id="d3fee-129">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="d3fee-130">Minden kosársorelem egy adott termék vásárlási adatait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="d3fee-130">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="d3fee-131">Legalább egy kocsisorelemnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="d3fee-131">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="d3fee-132">A kosárműveleteket úgy szerezheti be, ha az ügyfél azonosítójával hívja meg az **IAggregatePartner.getCustomers().byId** függvényt az ügyfél azonosításához, majd lehívja a felületet a **getCart függvényből.**</span><span class="sxs-lookup"><span data-stu-id="d3fee-132">Obtain an interface to cart operations by calling the **IAggregatePartner.getCustomers().byId** function with the customer ID to identify the customer, and then retrieving the interface from the **getCart** function.</span></span>

4. <span data-ttu-id="d3fee-133">A **kosár létrehozásához** hívja meg a create függvényt.</span><span class="sxs-lookup"><span data-stu-id="d3fee-133">Call the **create** function to create the cart.</span></span>

## <a name="java-example"></a><span data-ttu-id="d3fee-134">Java-példa</span><span class="sxs-lookup"><span data-stu-id="d3fee-134">Java example</span></span>

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

## <a name="powershell"></a><span data-ttu-id="d3fee-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3fee-135">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="d3fee-136">Rendelés létrehozása egy ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="d3fee-136">To create an order for a customer:</span></span>

1. <span data-ttu-id="d3fee-137">Cart-objektum példányosodása.</span><span class="sxs-lookup"><span data-stu-id="d3fee-137">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="d3fee-138">Hozza létre a **CartLineItem** objektumok listáját, és rendelje hozzá a listát a kosár sorelemekhez.</span><span class="sxs-lookup"><span data-stu-id="d3fee-138">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="d3fee-139">Minden kosársorelem egy adott termék vásárlási adatait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="d3fee-139">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="d3fee-140">Legalább egy kocsisorelemnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="d3fee-140">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="d3fee-141">Hajtsa végre a [**New-PartnerCustomerCart parancsot**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) a kosár létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="d3fee-141">Execute the [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) command to create the cart.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="d3fee-142">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d3fee-142">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d3fee-143">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="d3fee-143">Request syntax</span></span>

| <span data-ttu-id="d3fee-144">Metódus</span><span class="sxs-lookup"><span data-stu-id="d3fee-144">Method</span></span>   | <span data-ttu-id="d3fee-145">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d3fee-145">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d3fee-146">**Post**</span><span class="sxs-lookup"><span data-stu-id="d3fee-146">**POST**</span></span> | <span data-ttu-id="d3fee-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/carts HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d3fee-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="d3fee-148">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d3fee-148">URI parameter</span></span>

<span data-ttu-id="d3fee-149">Az ügyfél azonosításához használja a következő elérésiút-paramétert.</span><span class="sxs-lookup"><span data-stu-id="d3fee-149">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="d3fee-150">Név</span><span class="sxs-lookup"><span data-stu-id="d3fee-150">Name</span></span>            | <span data-ttu-id="d3fee-151">Típus</span><span class="sxs-lookup"><span data-stu-id="d3fee-151">Type</span></span>     | <span data-ttu-id="d3fee-152">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d3fee-152">Required</span></span> | <span data-ttu-id="d3fee-153">Leírás</span><span class="sxs-lookup"><span data-stu-id="d3fee-153">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="d3fee-154">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="d3fee-154">**customer-id**</span></span> | <span data-ttu-id="d3fee-155">sztring</span><span class="sxs-lookup"><span data-stu-id="d3fee-155">string</span></span>   | <span data-ttu-id="d3fee-156">Igen</span><span class="sxs-lookup"><span data-stu-id="d3fee-156">Yes</span></span>      | <span data-ttu-id="d3fee-157">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="d3fee-157">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="d3fee-158">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d3fee-158">Request headers</span></span>

<span data-ttu-id="d3fee-159">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d3fee-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d3fee-160">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d3fee-160">Request body</span></span>

<span data-ttu-id="d3fee-161">Ez a táblázat a kocsi [tulajdonságait ismerteti](cart-resources.md) a kérés törzsében.</span><span class="sxs-lookup"><span data-stu-id="d3fee-161">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="d3fee-162">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d3fee-162">Property</span></span>              | <span data-ttu-id="d3fee-163">Típus</span><span class="sxs-lookup"><span data-stu-id="d3fee-163">Type</span></span>             | <span data-ttu-id="d3fee-164">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d3fee-164">Required</span></span>        | <span data-ttu-id="d3fee-165">Leírás</span><span class="sxs-lookup"><span data-stu-id="d3fee-165">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d3fee-166">id</span><span class="sxs-lookup"><span data-stu-id="d3fee-166">id</span></span>                    | <span data-ttu-id="d3fee-167">sztring</span><span class="sxs-lookup"><span data-stu-id="d3fee-167">string</span></span>           | <span data-ttu-id="d3fee-168">No</span><span class="sxs-lookup"><span data-stu-id="d3fee-168">No</span></span>              | <span data-ttu-id="d3fee-169">A kosár sikeres létrehozása után megadott kocsiazonosító.</span><span class="sxs-lookup"><span data-stu-id="d3fee-169">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="d3fee-170">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="d3fee-170">creationTimeStamp</span></span>     | <span data-ttu-id="d3fee-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="d3fee-171">DateTime</span></span>         | <span data-ttu-id="d3fee-172">Nem</span><span class="sxs-lookup"><span data-stu-id="d3fee-172">No</span></span>              | <span data-ttu-id="d3fee-173">A kosár létrehozási dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="d3fee-173">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="d3fee-174">Alkalmazva a kosár sikeres létrehozása után.</span><span class="sxs-lookup"><span data-stu-id="d3fee-174">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="d3fee-175">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="d3fee-175">lastModifiedTimeStamp</span></span> | <span data-ttu-id="d3fee-176">DateTime</span><span class="sxs-lookup"><span data-stu-id="d3fee-176">DateTime</span></span>         | <span data-ttu-id="d3fee-177">Nem</span><span class="sxs-lookup"><span data-stu-id="d3fee-177">No</span></span>              | <span data-ttu-id="d3fee-178">A kosár legutóbbi frissítésének dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="d3fee-178">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="d3fee-179">Alkalmazva a kosár sikeres létrehozása után.</span><span class="sxs-lookup"><span data-stu-id="d3fee-179">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="d3fee-180">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="d3fee-180">expirationTimeStamp</span></span>   | <span data-ttu-id="d3fee-181">DateTime</span><span class="sxs-lookup"><span data-stu-id="d3fee-181">DateTime</span></span>         | <span data-ttu-id="d3fee-182">Nem</span><span class="sxs-lookup"><span data-stu-id="d3fee-182">No</span></span>              | <span data-ttu-id="d3fee-183">A kosár lejáratának dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="d3fee-183">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="d3fee-184">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="d3fee-184">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="d3fee-185">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="d3fee-185">lastModifiedUser</span></span>      | <span data-ttu-id="d3fee-186">sztring</span><span class="sxs-lookup"><span data-stu-id="d3fee-186">string</span></span>           | <span data-ttu-id="d3fee-187">No</span><span class="sxs-lookup"><span data-stu-id="d3fee-187">No</span></span>              | <span data-ttu-id="d3fee-188">Az a felhasználó, aki utoljára frissítette a kosárat.</span><span class="sxs-lookup"><span data-stu-id="d3fee-188">The user who last updated the cart.</span></span> <span data-ttu-id="d3fee-189">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="d3fee-189">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="d3fee-190">lineItems (sorsorok)</span><span class="sxs-lookup"><span data-stu-id="d3fee-190">lineItems</span></span>             | <span data-ttu-id="d3fee-191">Objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="d3fee-191">Array of objects</span></span> | <span data-ttu-id="d3fee-192">Igen</span><span class="sxs-lookup"><span data-stu-id="d3fee-192">Yes</span></span>             | <span data-ttu-id="d3fee-193">[CartLineItem-erőforrások tömbje.](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="d3fee-193">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                     |

<span data-ttu-id="d3fee-194">Ez a táblázat ismerteti a [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait a kérelem törzsében.</span><span class="sxs-lookup"><span data-stu-id="d3fee-194">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="d3fee-195">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d3fee-195">Property</span></span>       |            <span data-ttu-id="d3fee-196">Típus</span><span class="sxs-lookup"><span data-stu-id="d3fee-196">Type</span></span>             | <span data-ttu-id="d3fee-197">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d3fee-197">Required</span></span> |                                                                                         <span data-ttu-id="d3fee-198">Leírás</span><span class="sxs-lookup"><span data-stu-id="d3fee-198">Description</span></span>                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         <span data-ttu-id="d3fee-199">id</span><span class="sxs-lookup"><span data-stu-id="d3fee-199">id</span></span>          |           <span data-ttu-id="d3fee-200">sztring</span><span class="sxs-lookup"><span data-stu-id="d3fee-200">string</span></span>            |    <span data-ttu-id="d3fee-201">No</span><span class="sxs-lookup"><span data-stu-id="d3fee-201">No</span></span>    |                                                     <span data-ttu-id="d3fee-202">Egy kocsisorelem egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="d3fee-202">A unique identifier for a cart line item.</span></span> <span data-ttu-id="d3fee-203">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="d3fee-203">Applied upon successful creation of cart.</span></span>                                                     |
|      <span data-ttu-id="d3fee-204">catalogId (katalógusazonosító)</span><span class="sxs-lookup"><span data-stu-id="d3fee-204">catalogId</span></span>      |           <span data-ttu-id="d3fee-205">sztring</span><span class="sxs-lookup"><span data-stu-id="d3fee-205">string</span></span>            |   <span data-ttu-id="d3fee-206">Igen</span><span class="sxs-lookup"><span data-stu-id="d3fee-206">Yes</span></span>    |                                                                                <span data-ttu-id="d3fee-207">A katalóguselem azonosítója.</span><span class="sxs-lookup"><span data-stu-id="d3fee-207">The catalog item identifier.</span></span>                                                                                 |
|    <span data-ttu-id="d3fee-208">friendlyName (rövid név)</span><span class="sxs-lookup"><span data-stu-id="d3fee-208">friendlyName</span></span>     |           <span data-ttu-id="d3fee-209">sztring</span><span class="sxs-lookup"><span data-stu-id="d3fee-209">string</span></span>            |    <span data-ttu-id="d3fee-210">No</span><span class="sxs-lookup"><span data-stu-id="d3fee-210">No</span></span>    |                                                    <span data-ttu-id="d3fee-211">Választható.</span><span class="sxs-lookup"><span data-stu-id="d3fee-211">Optional.</span></span> <span data-ttu-id="d3fee-212">A partner által definiált elem rövid neve, amely segít egyértelműsedni.</span><span class="sxs-lookup"><span data-stu-id="d3fee-212">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                    |
|      <span data-ttu-id="d3fee-213">quantity</span><span class="sxs-lookup"><span data-stu-id="d3fee-213">quantity</span></span>       |             <span data-ttu-id="d3fee-214">int</span><span class="sxs-lookup"><span data-stu-id="d3fee-214">int</span></span>             |   <span data-ttu-id="d3fee-215">Igen</span><span class="sxs-lookup"><span data-stu-id="d3fee-215">Yes</span></span>    |                                                                            <span data-ttu-id="d3fee-216">A licencek vagy példányok száma.</span><span class="sxs-lookup"><span data-stu-id="d3fee-216">The number of licenses or instances.</span></span>                                                                             |
|    <span data-ttu-id="d3fee-217">currencyCode</span><span class="sxs-lookup"><span data-stu-id="d3fee-217">currencyCode</span></span>     |           <span data-ttu-id="d3fee-218">sztring</span><span class="sxs-lookup"><span data-stu-id="d3fee-218">string</span></span>            |    <span data-ttu-id="d3fee-219">No</span><span class="sxs-lookup"><span data-stu-id="d3fee-219">No</span></span>    |                                                                                     <span data-ttu-id="d3fee-220">A pénznemkód.</span><span class="sxs-lookup"><span data-stu-id="d3fee-220">The currency code.</span></span>                                                                                      |
|    <span data-ttu-id="d3fee-221">billingCycle</span><span class="sxs-lookup"><span data-stu-id="d3fee-221">billingCycle</span></span>     |           <span data-ttu-id="d3fee-222">Objektum</span><span class="sxs-lookup"><span data-stu-id="d3fee-222">Object</span></span>            |   <span data-ttu-id="d3fee-223">Igen</span><span class="sxs-lookup"><span data-stu-id="d3fee-223">Yes</span></span>    |                                                                    <span data-ttu-id="d3fee-224">Az aktuális időszakhoz beállított számlázási ciklus típusa.</span><span class="sxs-lookup"><span data-stu-id="d3fee-224">The type of billing cycle set for the current period.</span></span>                                                                    |
|    <span data-ttu-id="d3fee-225">Résztvevők</span><span class="sxs-lookup"><span data-stu-id="d3fee-225">participants</span></span>     | <span data-ttu-id="d3fee-226">Objektums sztringpárok listája</span><span class="sxs-lookup"><span data-stu-id="d3fee-226">List of Object String pairs</span></span> |    <span data-ttu-id="d3fee-227">Nem</span><span class="sxs-lookup"><span data-stu-id="d3fee-227">No</span></span>    |                                                                <span data-ttu-id="d3fee-228">A vásárláskor rekordban (MPNID) vásárolt PartnerId gyűjtemény.</span><span class="sxs-lookup"><span data-stu-id="d3fee-228">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                 |
| <span data-ttu-id="d3fee-229">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="d3fee-229">provisioningContext</span></span> | <span data-ttu-id="d3fee-230">Szótár<sztring, sztring></span><span class="sxs-lookup"><span data-stu-id="d3fee-230">Dictionary<string, string></span></span>  |    <span data-ttu-id="d3fee-231">Nem</span><span class="sxs-lookup"><span data-stu-id="d3fee-231">No</span></span>    | <span data-ttu-id="d3fee-232">A katalógus egyes elemeinek kiépítéséhez szükséges információk.</span><span class="sxs-lookup"><span data-stu-id="d3fee-232">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="d3fee-233">A termékváltozat provisioningVariables tulajdonsága jelzi, hogy mely tulajdonságok szükségesek a katalógus adott elemeihez.</span><span class="sxs-lookup"><span data-stu-id="d3fee-233">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span> |
|     <span data-ttu-id="d3fee-234">orderGroup</span><span class="sxs-lookup"><span data-stu-id="d3fee-234">orderGroup</span></span>      |           <span data-ttu-id="d3fee-235">sztring</span><span class="sxs-lookup"><span data-stu-id="d3fee-235">string</span></span>            |    <span data-ttu-id="d3fee-236">No</span><span class="sxs-lookup"><span data-stu-id="d3fee-236">No</span></span>    |                                                                   <span data-ttu-id="d3fee-237">Egy csoport, amely jelzi, hogy mely elemek helyezhetők együtt.</span><span class="sxs-lookup"><span data-stu-id="d3fee-237">A group to indicate which items can be placed together.</span></span>                                                                   |
|        <span data-ttu-id="d3fee-238">error</span><span class="sxs-lookup"><span data-stu-id="d3fee-238">error</span></span>        |           <span data-ttu-id="d3fee-239">Objektum</span><span class="sxs-lookup"><span data-stu-id="d3fee-239">Object</span></span>            |    <span data-ttu-id="d3fee-240">Nem</span><span class="sxs-lookup"><span data-stu-id="d3fee-240">No</span></span>    |                                                                     <span data-ttu-id="d3fee-241">A kosár létrehozása után alkalmazza, ha hiba történik.</span><span class="sxs-lookup"><span data-stu-id="d3fee-241">Applied after cart is created if there is an error.</span></span>                                                                      |
|     <span data-ttu-id="d3fee-242">renewsTo</span><span class="sxs-lookup"><span data-stu-id="d3fee-242">renewsTo</span></span>        | <span data-ttu-id="d3fee-243">Objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="d3fee-243">Array of objects</span></span>            |    <span data-ttu-id="d3fee-244">Nem</span><span class="sxs-lookup"><span data-stu-id="d3fee-244">No</span></span>    |                                                    <span data-ttu-id="d3fee-245">A [RenewsTo erőforrások tömbje.](cart-resources.md#renewsto)</span><span class="sxs-lookup"><span data-stu-id="d3fee-245">An array of [RenewsTo](cart-resources.md#renewsto) resources.</span></span>                                                                            |

<span data-ttu-id="d3fee-246">Ez a táblázat a [kérés törzsében található RenewsTo](cart-resources.md#renewsto) tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="d3fee-246">This table describes the [RenewsTo](cart-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="d3fee-247">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d3fee-247">Property</span></span>              | <span data-ttu-id="d3fee-248">Típus</span><span class="sxs-lookup"><span data-stu-id="d3fee-248">Type</span></span>             | <span data-ttu-id="d3fee-249">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d3fee-249">Required</span></span>        | <span data-ttu-id="d3fee-250">Leírás</span><span class="sxs-lookup"><span data-stu-id="d3fee-250">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d3fee-251">termDuration (kifejezés-lekértség)</span><span class="sxs-lookup"><span data-stu-id="d3fee-251">termDuration</span></span>          | <span data-ttu-id="d3fee-252">sztring</span><span class="sxs-lookup"><span data-stu-id="d3fee-252">string</span></span>           | <span data-ttu-id="d3fee-253">No</span><span class="sxs-lookup"><span data-stu-id="d3fee-253">No</span></span>              | <span data-ttu-id="d3fee-254">A megújítási időszak időtartamának ISO 8601-es ábrázolása.</span><span class="sxs-lookup"><span data-stu-id="d3fee-254">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="d3fee-255">A jelenleg támogatott értékek a **P1M (1** hónap) és **a P1Y (1** év).</span><span class="sxs-lookup"><span data-stu-id="d3fee-255">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="d3fee-256">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d3fee-256">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="d3fee-257">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d3fee-257">REST response</span></span>

<span data-ttu-id="d3fee-258">Ha a művelet sikeres, ez a metódus visszaadja a válasz törzsében a megadott [Cart](cart-resources.md) erőforrást.</span><span class="sxs-lookup"><span data-stu-id="d3fee-258">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d3fee-259">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d3fee-259">Response success and error codes</span></span>

<span data-ttu-id="d3fee-260">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d3fee-260">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d3fee-261">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d3fee-261">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d3fee-262">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d3fee-262">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d3fee-263">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d3fee-263">Response example</span></span>

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
