---
title: Kosár frissítése
description: Hogyan frissítheti egy ügyfél megrendelését egy kosárban.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8954d4dad39f9b1a1b9a2f213e0231f01856fcd2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446683"
---
# <a name="update-a-cart"></a><span data-ttu-id="8c58f-103">Kosár frissítése</span><span class="sxs-lookup"><span data-stu-id="8c58f-103">Update a cart</span></span>

<span data-ttu-id="8c58f-104">Hogyan frissítheti egy ügyfél megrendelését egy kosárban.</span><span class="sxs-lookup"><span data-stu-id="8c58f-104">How to update an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c58f-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8c58f-105">Prerequisites</span></span>

- <span data-ttu-id="8c58f-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8c58f-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8c58f-107">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="8c58f-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8c58f-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8c58f-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8c58f-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="8c58f-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8c58f-110">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="8c58f-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8c58f-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="8c58f-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8c58f-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="8c58f-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8c58f-113">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8c58f-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8c58f-114">Egy meglévő kosár azonosítója.</span><span class="sxs-lookup"><span data-stu-id="8c58f-114">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="8c58f-115">C\#</span><span class="sxs-lookup"><span data-stu-id="8c58f-115">C\#</span></span>

<span data-ttu-id="8c58f-116">Az ügyfél megrendelésének frissítéséhez szerezze be a kosárt a **Get()** metódussal úgy, hogy a **ById()** függvény használatával ad át az ügyfél- és kosárazonosítókat.</span><span class="sxs-lookup"><span data-stu-id="8c58f-116">To update an order for a customer, get the cart using the **Get()** method by passing the customer and cart IDs using the **ById()** function.</span></span> <span data-ttu-id="8c58f-117">Tegye meg a szükséges módosításokat a kosáron.</span><span class="sxs-lookup"><span data-stu-id="8c58f-117">Make the necessary changes to the cart.</span></span> <span data-ttu-id="8c58f-118">Most hívja meg a **Put** metódust ügyfél- és kosárazonosítók használatával a **ById() metódussal.**</span><span class="sxs-lookup"><span data-stu-id="8c58f-118">Now call the **Put** method by using customer and cart IDs using the **ById()** method.</span></span>

<span data-ttu-id="8c58f-119">Végül hívja meg a **Put() vagy** **PutAsync()** metódust a rendelés létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="8c58f-119">Finally, call the **Put()** or **PutAsync()** method to create the order.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a><span data-ttu-id="8c58f-120">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="8c58f-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8c58f-121">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="8c58f-121">Request syntax</span></span>

| <span data-ttu-id="8c58f-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="8c58f-122">Method</span></span>  | <span data-ttu-id="8c58f-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="8c58f-123">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8c58f-124">**PUT**</span><span class="sxs-lookup"><span data-stu-id="8c58f-124">**PUT**</span></span> | <span data-ttu-id="8c58f-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfél-azonosító}/carts/{cart-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8c58f-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span></span>              |

### <a name="uri-parameters"></a><span data-ttu-id="8c58f-126">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="8c58f-126">URI parameters</span></span>

<span data-ttu-id="8c58f-127">Az alábbi elérésiút-paraméterek használatával azonosíthatja az ügyfelet, és megadhatja a frissíteni kívánt kosárt.</span><span class="sxs-lookup"><span data-stu-id="8c58f-127">Use the following path parameters to identify the customer, and specify the cart to be updated.</span></span>

| <span data-ttu-id="8c58f-128">Név</span><span class="sxs-lookup"><span data-stu-id="8c58f-128">Name</span></span>            | <span data-ttu-id="8c58f-129">Típus</span><span class="sxs-lookup"><span data-stu-id="8c58f-129">Type</span></span>     | <span data-ttu-id="8c58f-130">Kötelező</span><span class="sxs-lookup"><span data-stu-id="8c58f-130">Required</span></span> | <span data-ttu-id="8c58f-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="8c58f-131">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="8c58f-132">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="8c58f-132">**customer-id**</span></span> | <span data-ttu-id="8c58f-133">sztring</span><span class="sxs-lookup"><span data-stu-id="8c58f-133">string</span></span>   | <span data-ttu-id="8c58f-134">Igen</span><span class="sxs-lookup"><span data-stu-id="8c58f-134">Yes</span></span>      | <span data-ttu-id="8c58f-135">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="8c58f-135">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="8c58f-136">**cart-id**</span><span class="sxs-lookup"><span data-stu-id="8c58f-136">**cart-id**</span></span>     | <span data-ttu-id="8c58f-137">sztring</span><span class="sxs-lookup"><span data-stu-id="8c58f-137">string</span></span>   | <span data-ttu-id="8c58f-138">Igen</span><span class="sxs-lookup"><span data-stu-id="8c58f-138">Yes</span></span>      | <span data-ttu-id="8c58f-139">Egy GUID formátumú kocsiazonosító, amely azonosítja a kosárat.</span><span class="sxs-lookup"><span data-stu-id="8c58f-139">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="8c58f-140">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="8c58f-140">Request headers</span></span>

<span data-ttu-id="8c58f-141">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8c58f-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8c58f-142">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="8c58f-142">Request body</span></span>

<span data-ttu-id="8c58f-143">Ez a táblázat a kocsi [tulajdonságait ismerteti](cart-resources.md) a kérés törzsében.</span><span class="sxs-lookup"><span data-stu-id="8c58f-143">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="8c58f-144">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="8c58f-144">Property</span></span>              | <span data-ttu-id="8c58f-145">Típus</span><span class="sxs-lookup"><span data-stu-id="8c58f-145">Type</span></span>             | <span data-ttu-id="8c58f-146">Kötelező</span><span class="sxs-lookup"><span data-stu-id="8c58f-146">Required</span></span>        | <span data-ttu-id="8c58f-147">Leírás</span><span class="sxs-lookup"><span data-stu-id="8c58f-147">Description</span></span>                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8c58f-148">id</span><span class="sxs-lookup"><span data-stu-id="8c58f-148">id</span></span>                    | <span data-ttu-id="8c58f-149">sztring</span><span class="sxs-lookup"><span data-stu-id="8c58f-149">string</span></span>           | <span data-ttu-id="8c58f-150">No</span><span class="sxs-lookup"><span data-stu-id="8c58f-150">No</span></span>              | <span data-ttu-id="8c58f-151">A kosár sikeres létrehozása után megadott bevásárlókocsi-azonosító.</span><span class="sxs-lookup"><span data-stu-id="8c58f-151">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="8c58f-152">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="8c58f-152">creationTimeStamp</span></span>     | <span data-ttu-id="8c58f-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="8c58f-153">DateTime</span></span>         | <span data-ttu-id="8c58f-154">Nem</span><span class="sxs-lookup"><span data-stu-id="8c58f-154">No</span></span>              | <span data-ttu-id="8c58f-155">A kosár létrehozási dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="8c58f-155">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="8c58f-156">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="8c58f-156">Applied upon successful creation of the cart.</span></span>        |
| <span data-ttu-id="8c58f-157">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="8c58f-157">lastModifiedTimeStamp</span></span> | <span data-ttu-id="8c58f-158">DateTime</span><span class="sxs-lookup"><span data-stu-id="8c58f-158">DateTime</span></span>         | <span data-ttu-id="8c58f-159">Nem</span><span class="sxs-lookup"><span data-stu-id="8c58f-159">No</span></span>              | <span data-ttu-id="8c58f-160">A kosár legutóbbi frissítésének dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="8c58f-160">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="8c58f-161">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="8c58f-161">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="8c58f-162">expirationTimeStamp (lejárat ideje)</span><span class="sxs-lookup"><span data-stu-id="8c58f-162">expirationTimeStamp</span></span>   | <span data-ttu-id="8c58f-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="8c58f-163">DateTime</span></span>         | <span data-ttu-id="8c58f-164">Nem</span><span class="sxs-lookup"><span data-stu-id="8c58f-164">No</span></span>              | <span data-ttu-id="8c58f-165">A kosár lejáratának dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="8c58f-165">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="8c58f-166">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="8c58f-166">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="8c58f-167">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="8c58f-167">lastModifiedUser</span></span>      | <span data-ttu-id="8c58f-168">sztring</span><span class="sxs-lookup"><span data-stu-id="8c58f-168">string</span></span>           | <span data-ttu-id="8c58f-169">No</span><span class="sxs-lookup"><span data-stu-id="8c58f-169">No</span></span>              | <span data-ttu-id="8c58f-170">Az a felhasználó, aki utoljára frissítette a kosárat.</span><span class="sxs-lookup"><span data-stu-id="8c58f-170">The user who last updated the cart.</span></span> <span data-ttu-id="8c58f-171">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="8c58f-171">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="8c58f-172">lineItems (sorsorok)</span><span class="sxs-lookup"><span data-stu-id="8c58f-172">lineItems</span></span>             | <span data-ttu-id="8c58f-173">Objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="8c58f-173">Array of objects</span></span> | <span data-ttu-id="8c58f-174">Igen</span><span class="sxs-lookup"><span data-stu-id="8c58f-174">Yes</span></span>             | <span data-ttu-id="8c58f-175">[CartLineItem-erőforrások tömbje.](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="8c58f-175">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                               |

<span data-ttu-id="8c58f-176">Ez a táblázat a [CartLineItem](cart-resources.md#cartlineitem) tulajdonságait ismerteti a kérés törzsében.</span><span class="sxs-lookup"><span data-stu-id="8c58f-176">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="8c58f-177">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="8c58f-177">Property</span></span>             | <span data-ttu-id="8c58f-178">Típus</span><span class="sxs-lookup"><span data-stu-id="8c58f-178">Type</span></span>                        | <span data-ttu-id="8c58f-179">Kötelező</span><span class="sxs-lookup"><span data-stu-id="8c58f-179">Required</span></span>     | <span data-ttu-id="8c58f-180">Leírás</span><span class="sxs-lookup"><span data-stu-id="8c58f-180">Description</span></span>                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8c58f-181">id</span><span class="sxs-lookup"><span data-stu-id="8c58f-181">id</span></span>                   | <span data-ttu-id="8c58f-182">sztring</span><span class="sxs-lookup"><span data-stu-id="8c58f-182">string</span></span>                      | <span data-ttu-id="8c58f-183">No</span><span class="sxs-lookup"><span data-stu-id="8c58f-183">No</span></span>           | <span data-ttu-id="8c58f-184">A kosársorelem egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="8c58f-184">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="8c58f-185">A kosár sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="8c58f-185">Applied upon successful creation of cart.</span></span>                |
| <span data-ttu-id="8c58f-186">catalogId (katalógusazonosító)</span><span class="sxs-lookup"><span data-stu-id="8c58f-186">catalogId</span></span>            | <span data-ttu-id="8c58f-187">sztring</span><span class="sxs-lookup"><span data-stu-id="8c58f-187">string</span></span>                      | <span data-ttu-id="8c58f-188">Igen</span><span class="sxs-lookup"><span data-stu-id="8c58f-188">Yes</span></span>          | <span data-ttu-id="8c58f-189">A katalóguselem azonosítója.</span><span class="sxs-lookup"><span data-stu-id="8c58f-189">The catalog item identifier.</span></span>                                                                       |
| <span data-ttu-id="8c58f-190">friendlyName (rövid név)</span><span class="sxs-lookup"><span data-stu-id="8c58f-190">friendlyName</span></span>         | <span data-ttu-id="8c58f-191">sztring</span><span class="sxs-lookup"><span data-stu-id="8c58f-191">string</span></span>                      | <span data-ttu-id="8c58f-192">No</span><span class="sxs-lookup"><span data-stu-id="8c58f-192">No</span></span>           | <span data-ttu-id="8c58f-193">Választható.</span><span class="sxs-lookup"><span data-stu-id="8c58f-193">Optional.</span></span> <span data-ttu-id="8c58f-194">A partner által meghatározott elem rövid neve, amely segít az egyértelműsségben.</span><span class="sxs-lookup"><span data-stu-id="8c58f-194">The friendly name for the item defined by the partner to help disambiguate.</span></span>              |
| <span data-ttu-id="8c58f-195">quantity</span><span class="sxs-lookup"><span data-stu-id="8c58f-195">quantity</span></span>             | <span data-ttu-id="8c58f-196">int</span><span class="sxs-lookup"><span data-stu-id="8c58f-196">int</span></span>                         | <span data-ttu-id="8c58f-197">Igen</span><span class="sxs-lookup"><span data-stu-id="8c58f-197">Yes</span></span>          | <span data-ttu-id="8c58f-198">A licencek vagy példányok száma.</span><span class="sxs-lookup"><span data-stu-id="8c58f-198">The number of licenses or instances.</span></span>     |
| <span data-ttu-id="8c58f-199">currencyCode</span><span class="sxs-lookup"><span data-stu-id="8c58f-199">currencyCode</span></span>         | <span data-ttu-id="8c58f-200">sztring</span><span class="sxs-lookup"><span data-stu-id="8c58f-200">string</span></span>                      | <span data-ttu-id="8c58f-201">No</span><span class="sxs-lookup"><span data-stu-id="8c58f-201">No</span></span>           | <span data-ttu-id="8c58f-202">A pénznemkód.</span><span class="sxs-lookup"><span data-stu-id="8c58f-202">The currency code.</span></span>                                                                                 |
| <span data-ttu-id="8c58f-203">billingCycle (számlázási ciklus)</span><span class="sxs-lookup"><span data-stu-id="8c58f-203">billingCycle</span></span>         | <span data-ttu-id="8c58f-204">Objektum</span><span class="sxs-lookup"><span data-stu-id="8c58f-204">Object</span></span>                      | <span data-ttu-id="8c58f-205">Igen</span><span class="sxs-lookup"><span data-stu-id="8c58f-205">Yes</span></span>          | <span data-ttu-id="8c58f-206">Az aktuális időszakra beállított számlázási ciklus típusa.</span><span class="sxs-lookup"><span data-stu-id="8c58f-206">The type of billing cycle set for the current period.</span></span>                                              |
| <span data-ttu-id="8c58f-207">Résztvevők</span><span class="sxs-lookup"><span data-stu-id="8c58f-207">participants</span></span>         | <span data-ttu-id="8c58f-208">Objektumsring-párok listája</span><span class="sxs-lookup"><span data-stu-id="8c58f-208">List of Object String pairs</span></span> | <span data-ttu-id="8c58f-209">Nem</span><span class="sxs-lookup"><span data-stu-id="8c58f-209">No</span></span>           | <span data-ttu-id="8c58f-210">A vásárlás résztvevőinek gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="8c58f-210">A collection of participants on the purchase.</span></span>                                                      |
| <span data-ttu-id="8c58f-211">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="8c58f-211">provisioningContext</span></span>  | <span data-ttu-id="8c58f-212">Dictionary<string, string></span><span class="sxs-lookup"><span data-stu-id="8c58f-212">Dictionary<string, string></span></span>  | <span data-ttu-id="8c58f-213">Nem</span><span class="sxs-lookup"><span data-stu-id="8c58f-213">No</span></span>           | <span data-ttu-id="8c58f-214">Az ajánlat építéshez használt környezet.</span><span class="sxs-lookup"><span data-stu-id="8c58f-214">A context used for provisioning of offer.</span></span>                                                          |
| <span data-ttu-id="8c58f-215">orderGroup</span><span class="sxs-lookup"><span data-stu-id="8c58f-215">orderGroup</span></span>           | <span data-ttu-id="8c58f-216">sztring</span><span class="sxs-lookup"><span data-stu-id="8c58f-216">string</span></span>                      | <span data-ttu-id="8c58f-217">No</span><span class="sxs-lookup"><span data-stu-id="8c58f-217">No</span></span>           | <span data-ttu-id="8c58f-218">Egy csoport, amely jelzi, hogy mely elemek helyezhetők el együtt.</span><span class="sxs-lookup"><span data-stu-id="8c58f-218">A group to indicate which items can be placed together.</span></span>                                            |
| <span data-ttu-id="8c58f-219">error</span><span class="sxs-lookup"><span data-stu-id="8c58f-219">error</span></span>                | <span data-ttu-id="8c58f-220">Objektum</span><span class="sxs-lookup"><span data-stu-id="8c58f-220">Object</span></span>                      | <span data-ttu-id="8c58f-221">Nem</span><span class="sxs-lookup"><span data-stu-id="8c58f-221">No</span></span>           | <span data-ttu-id="8c58f-222">A kosár létrehozása után lesz alkalmazva hiba esetén.</span><span class="sxs-lookup"><span data-stu-id="8c58f-222">Applied after cart is created in case of an error.</span></span>                                                 |

### <a name="request-example"></a><span data-ttu-id="8c58f-223">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8c58f-223">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="8c58f-224">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="8c58f-224">REST response</span></span>

<span data-ttu-id="8c58f-225">Ha ez a módszer sikeres, a válasz törzsében adja vissza a megadott [Cart](cart-resources.md) erőforrást.</span><span class="sxs-lookup"><span data-stu-id="8c58f-225">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8c58f-226">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="8c58f-226">Response success and error codes</span></span>

<span data-ttu-id="8c58f-227">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="8c58f-227">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8c58f-228">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="8c58f-228">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8c58f-229">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8c58f-229">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8c58f-230">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8c58f-230">Response example</span></span>

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
