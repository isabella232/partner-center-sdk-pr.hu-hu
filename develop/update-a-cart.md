---
title: Kosár frissítése
description: Ügyfél rendelésének frissítése egy kosárban.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7c0806ccc87281b9b34005f22cd8d6ad57fb5de5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767835"
---
# <a name="update-a-cart"></a><span data-ttu-id="e6734-103">Kosár frissítése</span><span class="sxs-lookup"><span data-stu-id="e6734-103">Update a cart</span></span>

<span data-ttu-id="e6734-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="e6734-104">**Applies To**</span></span>

- <span data-ttu-id="e6734-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="e6734-105">Partner Center</span></span>

<span data-ttu-id="e6734-106">Ügyfél rendelésének frissítése egy kosárban.</span><span class="sxs-lookup"><span data-stu-id="e6734-106">How to update an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6734-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="e6734-107">Prerequisites</span></span>

- <span data-ttu-id="e6734-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="e6734-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e6734-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="e6734-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e6734-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e6734-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e6734-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="e6734-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e6734-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="e6734-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e6734-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="e6734-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e6734-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="e6734-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e6734-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e6734-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e6734-116">Egy meglévő kosárhoz tartozó kosár-azonosító.</span><span class="sxs-lookup"><span data-stu-id="e6734-116">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="e6734-117">C\#</span><span class="sxs-lookup"><span data-stu-id="e6734-117">C\#</span></span>

<span data-ttu-id="e6734-118">Egy ügyfél rendelésének frissítéséhez szerezze be a kosárt a **Get ()** metódussal, ha az ügyfél és a kosár azonosítóját a **ById ()** függvény használatával adja át.</span><span class="sxs-lookup"><span data-stu-id="e6734-118">To update an order for a customer, get the cart using the **Get()** method by passing the customer and cart ID's using the **ById()** function.</span></span> <span data-ttu-id="e6734-119">Végezze el a szükséges módosításokat a kosárban.</span><span class="sxs-lookup"><span data-stu-id="e6734-119">Make the necessary changes to the cart.</span></span> <span data-ttu-id="e6734-120">Most hívja meg a **put** metódust az ügyfél és a kosár azonosítójának használatával a **ById ()** metódus használatával.</span><span class="sxs-lookup"><span data-stu-id="e6734-120">Now call the **Put** method by using customer and cart ID's using the **ById()** method.</span></span>

<span data-ttu-id="e6734-121">Végül hívja a **put ()** vagy a **PutAsync ()** metódust a rendelés létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="e6734-121">Finally, call the **Put()** or **PutAsync()** method to create the order.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a><span data-ttu-id="e6734-122">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="e6734-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e6734-123">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="e6734-123">Request syntax</span></span>

| <span data-ttu-id="e6734-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="e6734-124">Method</span></span>  | <span data-ttu-id="e6734-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="e6734-125">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e6734-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="e6734-126">**PUT**</span></span> | <span data-ttu-id="e6734-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts/{cart-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="e6734-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span></span>              |

### <a name="uri-parameters"></a><span data-ttu-id="e6734-128">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="e6734-128">URI parameters</span></span>

<span data-ttu-id="e6734-129">A következő elérésiút-paraméterek használatával azonosíthatja az ügyfelet, és megadhatja a frissítendő szekéret.</span><span class="sxs-lookup"><span data-stu-id="e6734-129">Use the following path parameters to identify the customer, and specify the cart to be updated.</span></span>

| <span data-ttu-id="e6734-130">Név</span><span class="sxs-lookup"><span data-stu-id="e6734-130">Name</span></span>            | <span data-ttu-id="e6734-131">Típus</span><span class="sxs-lookup"><span data-stu-id="e6734-131">Type</span></span>     | <span data-ttu-id="e6734-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e6734-132">Required</span></span> | <span data-ttu-id="e6734-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="e6734-133">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="e6734-134">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="e6734-134">**customer-id**</span></span> | <span data-ttu-id="e6734-135">sztring</span><span class="sxs-lookup"><span data-stu-id="e6734-135">string</span></span>   | <span data-ttu-id="e6734-136">Igen</span><span class="sxs-lookup"><span data-stu-id="e6734-136">Yes</span></span>      | <span data-ttu-id="e6734-137">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="e6734-137">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="e6734-138">**kosár-azonosító**</span><span class="sxs-lookup"><span data-stu-id="e6734-138">**cart-id**</span></span>     | <span data-ttu-id="e6734-139">sztring</span><span class="sxs-lookup"><span data-stu-id="e6734-139">string</span></span>   | <span data-ttu-id="e6734-140">Igen</span><span class="sxs-lookup"><span data-stu-id="e6734-140">Yes</span></span>      | <span data-ttu-id="e6734-141">A szekér azonosítására szolgáló GUID formátumú kosár-azonosító.</span><span class="sxs-lookup"><span data-stu-id="e6734-141">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="e6734-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="e6734-142">Request headers</span></span>

<span data-ttu-id="e6734-143">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e6734-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e6734-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="e6734-144">Request body</span></span>

<span data-ttu-id="e6734-145">Ez a táblázat a kérés törzsében lévő [kosár](cart-resources.md) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="e6734-145">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="e6734-146">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="e6734-146">Property</span></span>              | <span data-ttu-id="e6734-147">Típus</span><span class="sxs-lookup"><span data-stu-id="e6734-147">Type</span></span>             | <span data-ttu-id="e6734-148">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e6734-148">Required</span></span>        | <span data-ttu-id="e6734-149">Leírás</span><span class="sxs-lookup"><span data-stu-id="e6734-149">Description</span></span>                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e6734-150">id</span><span class="sxs-lookup"><span data-stu-id="e6734-150">id</span></span>                    | <span data-ttu-id="e6734-151">sztring</span><span class="sxs-lookup"><span data-stu-id="e6734-151">string</span></span>           | <span data-ttu-id="e6734-152">No</span><span class="sxs-lookup"><span data-stu-id="e6734-152">No</span></span>              | <span data-ttu-id="e6734-153">A kosár sikeres létrehozásához megadott cart-azonosító.</span><span class="sxs-lookup"><span data-stu-id="e6734-153">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="e6734-154">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="e6734-154">creationTimeStamp</span></span>     | <span data-ttu-id="e6734-155">DateTime</span><span class="sxs-lookup"><span data-stu-id="e6734-155">DateTime</span></span>         | <span data-ttu-id="e6734-156">Nem</span><span class="sxs-lookup"><span data-stu-id="e6734-156">No</span></span>              | <span data-ttu-id="e6734-157">A kosár létrehozásának dátuma dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="e6734-157">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="e6734-158">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="e6734-158">Applied upon successful creation of the cart.</span></span>        |
| <span data-ttu-id="e6734-159">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="e6734-159">lastModifiedTimeStamp</span></span> | <span data-ttu-id="e6734-160">DateTime</span><span class="sxs-lookup"><span data-stu-id="e6734-160">DateTime</span></span>         | <span data-ttu-id="e6734-161">Nem</span><span class="sxs-lookup"><span data-stu-id="e6734-161">No</span></span>              | <span data-ttu-id="e6734-162">A kosár utolsó frissítésének dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="e6734-162">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="e6734-163">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="e6734-163">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="e6734-164">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="e6734-164">expirationTimeStamp</span></span>   | <span data-ttu-id="e6734-165">DateTime</span><span class="sxs-lookup"><span data-stu-id="e6734-165">DateTime</span></span>         | <span data-ttu-id="e6734-166">Nem</span><span class="sxs-lookup"><span data-stu-id="e6734-166">No</span></span>              | <span data-ttu-id="e6734-167">A kosár lejáratának dátuma dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="e6734-167">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="e6734-168">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="e6734-168">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="e6734-169">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="e6734-169">lastModifiedUser</span></span>      | <span data-ttu-id="e6734-170">sztring</span><span class="sxs-lookup"><span data-stu-id="e6734-170">string</span></span>           | <span data-ttu-id="e6734-171">No</span><span class="sxs-lookup"><span data-stu-id="e6734-171">No</span></span>              | <span data-ttu-id="e6734-172">A kosár utolsó frissítését végző felhasználó.</span><span class="sxs-lookup"><span data-stu-id="e6734-172">The user who last updated the cart.</span></span> <span data-ttu-id="e6734-173">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="e6734-173">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="e6734-174">Listaelemek</span><span class="sxs-lookup"><span data-stu-id="e6734-174">lineItems</span></span>             | <span data-ttu-id="e6734-175">Objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="e6734-175">Array of objects</span></span> | <span data-ttu-id="e6734-176">Igen</span><span class="sxs-lookup"><span data-stu-id="e6734-176">Yes</span></span>             | <span data-ttu-id="e6734-177">[CartLineItem](cart-resources.md#cartlineitem) -erőforrások tömbje.</span><span class="sxs-lookup"><span data-stu-id="e6734-177">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                               |

<span data-ttu-id="e6734-178">Ez a táblázat a kérelem törzsének [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="e6734-178">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="e6734-179">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="e6734-179">Property</span></span>             | <span data-ttu-id="e6734-180">Típus</span><span class="sxs-lookup"><span data-stu-id="e6734-180">Type</span></span>                        | <span data-ttu-id="e6734-181">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e6734-181">Required</span></span>     | <span data-ttu-id="e6734-182">Leírás</span><span class="sxs-lookup"><span data-stu-id="e6734-182">Description</span></span>                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e6734-183">id</span><span class="sxs-lookup"><span data-stu-id="e6734-183">id</span></span>                   | <span data-ttu-id="e6734-184">sztring</span><span class="sxs-lookup"><span data-stu-id="e6734-184">string</span></span>                      | <span data-ttu-id="e6734-185">No</span><span class="sxs-lookup"><span data-stu-id="e6734-185">No</span></span>           | <span data-ttu-id="e6734-186">Egy cart-sor egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="e6734-186">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="e6734-187">A kosár sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="e6734-187">Applied upon successful creation of cart.</span></span>                |
| <span data-ttu-id="e6734-188">catalogId</span><span class="sxs-lookup"><span data-stu-id="e6734-188">catalogId</span></span>            | <span data-ttu-id="e6734-189">sztring</span><span class="sxs-lookup"><span data-stu-id="e6734-189">string</span></span>                      | <span data-ttu-id="e6734-190">Igen</span><span class="sxs-lookup"><span data-stu-id="e6734-190">Yes</span></span>          | <span data-ttu-id="e6734-191">A katalógus-elemek azonosítója.</span><span class="sxs-lookup"><span data-stu-id="e6734-191">The catalog item identifier.</span></span>                                                                       |
| <span data-ttu-id="e6734-192">friendlyName</span><span class="sxs-lookup"><span data-stu-id="e6734-192">friendlyName</span></span>         | <span data-ttu-id="e6734-193">sztring</span><span class="sxs-lookup"><span data-stu-id="e6734-193">string</span></span>                      | <span data-ttu-id="e6734-194">No</span><span class="sxs-lookup"><span data-stu-id="e6734-194">No</span></span>           | <span data-ttu-id="e6734-195">Választható.</span><span class="sxs-lookup"><span data-stu-id="e6734-195">Optional.</span></span> <span data-ttu-id="e6734-196">A partner által a egyértelműsítse segítségére meghatározott rövid név.</span><span class="sxs-lookup"><span data-stu-id="e6734-196">The friendly name for the item defined by the partner to help disambiguate.</span></span>              |
| <span data-ttu-id="e6734-197">quantity</span><span class="sxs-lookup"><span data-stu-id="e6734-197">quantity</span></span>             | <span data-ttu-id="e6734-198">int</span><span class="sxs-lookup"><span data-stu-id="e6734-198">int</span></span>                         | <span data-ttu-id="e6734-199">Igen</span><span class="sxs-lookup"><span data-stu-id="e6734-199">Yes</span></span>          | <span data-ttu-id="e6734-200">A licencek vagy példányok száma.</span><span class="sxs-lookup"><span data-stu-id="e6734-200">The number of licenses or instances.</span></span>     |
| <span data-ttu-id="e6734-201">currencyCode</span><span class="sxs-lookup"><span data-stu-id="e6734-201">currencyCode</span></span>         | <span data-ttu-id="e6734-202">sztring</span><span class="sxs-lookup"><span data-stu-id="e6734-202">string</span></span>                      | <span data-ttu-id="e6734-203">No</span><span class="sxs-lookup"><span data-stu-id="e6734-203">No</span></span>           | <span data-ttu-id="e6734-204">A Pénznemkód.</span><span class="sxs-lookup"><span data-stu-id="e6734-204">The currency code.</span></span>                                                                                 |
| <span data-ttu-id="e6734-205">billingCycle</span><span class="sxs-lookup"><span data-stu-id="e6734-205">billingCycle</span></span>         | <span data-ttu-id="e6734-206">Objektum</span><span class="sxs-lookup"><span data-stu-id="e6734-206">Object</span></span>                      | <span data-ttu-id="e6734-207">Igen</span><span class="sxs-lookup"><span data-stu-id="e6734-207">Yes</span></span>          | <span data-ttu-id="e6734-208">Az aktuális időszakban beállított számlázási ciklus típusa.</span><span class="sxs-lookup"><span data-stu-id="e6734-208">The type of billing cycle set for the current period.</span></span>                                              |
| <span data-ttu-id="e6734-209">résztvevők</span><span class="sxs-lookup"><span data-stu-id="e6734-209">participants</span></span>         | <span data-ttu-id="e6734-210">Az Object string párok listája</span><span class="sxs-lookup"><span data-stu-id="e6734-210">List of Object String pairs</span></span> | <span data-ttu-id="e6734-211">Nem</span><span class="sxs-lookup"><span data-stu-id="e6734-211">No</span></span>           | <span data-ttu-id="e6734-212">A vásárlás résztvevőinek gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="e6734-212">A collection of participants on the purchase.</span></span>                                                      |
| <span data-ttu-id="e6734-213">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="e6734-213">provisioningContext</span></span>  | <span data-ttu-id="e6734-214">Szótár<karakterlánc, karakterlánc></span><span class="sxs-lookup"><span data-stu-id="e6734-214">Dictionary<string, string></span></span>  | <span data-ttu-id="e6734-215">Nem</span><span class="sxs-lookup"><span data-stu-id="e6734-215">No</span></span>           | <span data-ttu-id="e6734-216">Az ajánlat üzembe helyezéséhez használt környezet.</span><span class="sxs-lookup"><span data-stu-id="e6734-216">A context used for provisioning of offer.</span></span>                                                          |
| <span data-ttu-id="e6734-217">orderGroup</span><span class="sxs-lookup"><span data-stu-id="e6734-217">orderGroup</span></span>           | <span data-ttu-id="e6734-218">sztring</span><span class="sxs-lookup"><span data-stu-id="e6734-218">string</span></span>                      | <span data-ttu-id="e6734-219">No</span><span class="sxs-lookup"><span data-stu-id="e6734-219">No</span></span>           | <span data-ttu-id="e6734-220">Egy csoport, amely jelzi, hogy mely elemek helyezhetők el egymásba.</span><span class="sxs-lookup"><span data-stu-id="e6734-220">A group to indicate which items can be placed together.</span></span>                                            |
| <span data-ttu-id="e6734-221">error</span><span class="sxs-lookup"><span data-stu-id="e6734-221">error</span></span>                | <span data-ttu-id="e6734-222">Objektum</span><span class="sxs-lookup"><span data-stu-id="e6734-222">Object</span></span>                      | <span data-ttu-id="e6734-223">Nem</span><span class="sxs-lookup"><span data-stu-id="e6734-223">No</span></span>           | <span data-ttu-id="e6734-224">A kosár létrehozásakor a rendszer hiba esetén alkalmazza.</span><span class="sxs-lookup"><span data-stu-id="e6734-224">Applied after cart is created in case of an error.</span></span>                                                 |

### <a name="request-example"></a><span data-ttu-id="e6734-225">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="e6734-225">Request example</span></span>

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
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
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="e6734-226">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="e6734-226">REST response</span></span>

<span data-ttu-id="e6734-227">Ha ez sikeres, ez a metódus a válasz törzsében lévő feltöltött [kosár](cart-resources.md) -erőforrást adja vissza.</span><span class="sxs-lookup"><span data-stu-id="e6734-227">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e6734-228">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="e6734-228">Response success and error codes</span></span>

<span data-ttu-id="e6734-229">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="e6734-229">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e6734-230">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="e6734-230">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e6734-231">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e6734-231">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e6734-232">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="e6734-232">Response example</span></span>

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
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```
