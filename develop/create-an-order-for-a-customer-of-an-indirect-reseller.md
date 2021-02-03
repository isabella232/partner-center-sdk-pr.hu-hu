---
title: Vevői rendelés létrehozása közvetett viszonteladóhoz
description: Ismerje meg, hogy a partner Center API-k segítségével hogyan hozhat létre rendelést egy közvetett viszonteladó ügyfelének. A cikk az előfeltételeket, a lépéseket és a Exmaples tartalmazza.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f72ecec8d82e6b8a1bc53c277206cafd7d8a4e03
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768636"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a><span data-ttu-id="240d2-104">Megrendelés létrehozása közvetett viszonteladó ügyfelének</span><span class="sxs-lookup"><span data-stu-id="240d2-104">Create an order for a customer of an indirect reseller</span></span>

<span data-ttu-id="240d2-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="240d2-105">**Applies to:**</span></span>

- <span data-ttu-id="240d2-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="240d2-106">Partner Center</span></span>

<span data-ttu-id="240d2-107">Megrendelést hozhat létre egy közvetett viszonteladó ügyfelének.</span><span class="sxs-lookup"><span data-stu-id="240d2-107">How to create an order for a customer of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="240d2-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="240d2-108">Prerequisites</span></span>

- <span data-ttu-id="240d2-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="240d2-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="240d2-110">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="240d2-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="240d2-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="240d2-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="240d2-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="240d2-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="240d2-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="240d2-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="240d2-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="240d2-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="240d2-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="240d2-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="240d2-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="240d2-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="240d2-117">A megvásárolni kívánt tétel ajánlatának azonosítója.</span><span class="sxs-lookup"><span data-stu-id="240d2-117">The offer identifier of the item to purchase.</span></span>

- <span data-ttu-id="240d2-118">A közvetett viszonteladó bérlői azonosítója.</span><span class="sxs-lookup"><span data-stu-id="240d2-118">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="240d2-119">C\#</span><span class="sxs-lookup"><span data-stu-id="240d2-119">C\#</span></span>

<span data-ttu-id="240d2-120">Egy közvetett viszonteladó ügyfelének rendelésének létrehozása:</span><span class="sxs-lookup"><span data-stu-id="240d2-120">To create an order for a customer of an indirect reseller:</span></span>

1. <span data-ttu-id="240d2-121">Szerezze be azon közvetett viszonteladók gyűjteményét, akik kapcsolatban vannak a bejelentkezett partnerrel.</span><span class="sxs-lookup"><span data-stu-id="240d2-121">Get a collection of the indirect resellers that have a relationship with the signed-in partner.</span></span>

2. <span data-ttu-id="240d2-122">Szerezzen be egy helyi változót a gyűjtemény azon eleméhez, amely megfelel a közvetett viszonteladói AZONOSÍTÓnak.</span><span class="sxs-lookup"><span data-stu-id="240d2-122">Get a local variable to the item in the collection that matches the indirect reseller ID.</span></span> <span data-ttu-id="240d2-123">Ez a lépés segít a viszonteladó [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) tulajdonságának elérésében a rendelés létrehozásakor.</span><span class="sxs-lookup"><span data-stu-id="240d2-123">This step helps you access the reseller's [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) property when you create the order.</span></span>

3. <span data-ttu-id="240d2-124">Hozzon létre egy [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) objektumot, és állítsa az [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) tulajdonságot az ügyfél-azonosítóra, hogy rögzítse az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="240d2-124">Instantiate an [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and set the [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) property to the customer identifier in order to record the customer.</span></span>

4. <span data-ttu-id="240d2-125">Hozza létre a [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) -objektumok listáját, és rendelje hozzá a listát a rendelés [**listaelemek**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) tulajdonságához.</span><span class="sxs-lookup"><span data-stu-id="240d2-125">Create a list of [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objects, and assign the list to the order's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) property.</span></span> <span data-ttu-id="240d2-126">Az egyes rendelési sorok egy adott ajánlat vásárlási információit tartalmazzák.</span><span class="sxs-lookup"><span data-stu-id="240d2-126">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="240d2-127">Ügyeljen arra, hogy az egyes sorokban található [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) tulajdonságot a közvetett viszonteladó MPN-azonosítójával feltöltse.</span><span class="sxs-lookup"><span data-stu-id="240d2-127">Be sure to populate the [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) property in each line item with the MPN ID of the indirect reseller.</span></span> <span data-ttu-id="240d2-128">Legalább egy Order line-elemmel kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="240d2-128">You must have at least one order line item.</span></span>

5. <span data-ttu-id="240d2-129">Szerezzen be egy felületet a megrendelési műveletekhez úgy, hogy meghívja a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához, majd lekéri a felületet a [**megrendelések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="240d2-129">Obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

6. <span data-ttu-id="240d2-130">Hívja meg a [**create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) metódust a rendelés létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="240d2-130">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method to create the order.</span></span>

### <a name="c-example"></a><span data-ttu-id="240d2-131">C \# példa</span><span class="sxs-lookup"><span data-stu-id="240d2-131">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

<span data-ttu-id="240d2-132">**Minta**: [Console test app](console-test-app.md)**Project**: a partner Center SDK Samples **osztálya**: PlaceOrderForCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="240d2-132">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: PlaceOrderForCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="240d2-133">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="240d2-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="240d2-134">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="240d2-134">Request syntax</span></span>

| <span data-ttu-id="240d2-135">Metódus</span><span class="sxs-lookup"><span data-stu-id="240d2-135">Method</span></span>   | <span data-ttu-id="240d2-136">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="240d2-136">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="240d2-137">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="240d2-137">**POST**</span></span> | <span data-ttu-id="240d2-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="240d2-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="240d2-139">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="240d2-139">URI parameters</span></span>

<span data-ttu-id="240d2-140">Az ügyfél azonosításához használja a következő Path paramétert.</span><span class="sxs-lookup"><span data-stu-id="240d2-140">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="240d2-141">Név</span><span class="sxs-lookup"><span data-stu-id="240d2-141">Name</span></span>        | <span data-ttu-id="240d2-142">Típus</span><span class="sxs-lookup"><span data-stu-id="240d2-142">Type</span></span>   | <span data-ttu-id="240d2-143">Kötelező</span><span class="sxs-lookup"><span data-stu-id="240d2-143">Required</span></span> | <span data-ttu-id="240d2-144">Leírás</span><span class="sxs-lookup"><span data-stu-id="240d2-144">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="240d2-145">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="240d2-145">customer-id</span></span> | <span data-ttu-id="240d2-146">sztring</span><span class="sxs-lookup"><span data-stu-id="240d2-146">string</span></span> | <span data-ttu-id="240d2-147">Igen</span><span class="sxs-lookup"><span data-stu-id="240d2-147">Yes</span></span>      | <span data-ttu-id="240d2-148">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="240d2-148">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="240d2-149">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="240d2-149">Request headers</span></span>

<span data-ttu-id="240d2-150">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="240d2-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="240d2-151">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="240d2-151">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="240d2-152">Sorrend</span><span class="sxs-lookup"><span data-stu-id="240d2-152">Order</span></span>

<span data-ttu-id="240d2-153">Ez a tábla a kérelem törzsének **Order (rendelés** ) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="240d2-153">This table describes the **Order** properties in the request body.</span></span>

| <span data-ttu-id="240d2-154">Név</span><span class="sxs-lookup"><span data-stu-id="240d2-154">Name</span></span> | <span data-ttu-id="240d2-155">Típus</span><span class="sxs-lookup"><span data-stu-id="240d2-155">Type</span></span> | <span data-ttu-id="240d2-156">Kötelező</span><span class="sxs-lookup"><span data-stu-id="240d2-156">Required</span></span> | <span data-ttu-id="240d2-157">Leírás</span><span class="sxs-lookup"><span data-stu-id="240d2-157">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="240d2-158">id</span><span class="sxs-lookup"><span data-stu-id="240d2-158">id</span></span> | <span data-ttu-id="240d2-159">sztring</span><span class="sxs-lookup"><span data-stu-id="240d2-159">string</span></span> | <span data-ttu-id="240d2-160">No</span><span class="sxs-lookup"><span data-stu-id="240d2-160">No</span></span> | <span data-ttu-id="240d2-161">A megrendelés sikeres létrehozásakor megadott rendelési azonosító.</span><span class="sxs-lookup"><span data-stu-id="240d2-161">An order identifier that is supplied upon successful creation of the order.</span></span> |
| <span data-ttu-id="240d2-162">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="240d2-162">referenceCustomerId</span></span> | <span data-ttu-id="240d2-163">sztring</span><span class="sxs-lookup"><span data-stu-id="240d2-163">string</span></span> | <span data-ttu-id="240d2-164">Igen</span><span class="sxs-lookup"><span data-stu-id="240d2-164">Yes</span></span> | <span data-ttu-id="240d2-165">Az ügyfél-azonosító.</span><span class="sxs-lookup"><span data-stu-id="240d2-165">The customer identifier.</span></span> |
| <span data-ttu-id="240d2-166">billingCycle</span><span class="sxs-lookup"><span data-stu-id="240d2-166">billingCycle</span></span> | <span data-ttu-id="240d2-167">sztring</span><span class="sxs-lookup"><span data-stu-id="240d2-167">string</span></span> | <span data-ttu-id="240d2-168">No</span><span class="sxs-lookup"><span data-stu-id="240d2-168">No</span></span> | <span data-ttu-id="240d2-169">Az a gyakoriság, amellyel a partnert számlázzák a rendelésért.</span><span class="sxs-lookup"><span data-stu-id="240d2-169">The frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="240d2-170">Az alapértelmezett érték &quot; havonta történik &quot; , és a rendszer a megrendelés sikeres létrehozása után alkalmazza.</span><span class="sxs-lookup"><span data-stu-id="240d2-170">The default is &quot;Monthly&quot; and is applied upon successful creation of the order.</span></span> <span data-ttu-id="240d2-171">A támogatott értékek a [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype)található tagok nevei.</span><span class="sxs-lookup"><span data-stu-id="240d2-171">Supported values are the member names found in [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span></span> <span data-ttu-id="240d2-172">Megjegyzés: az éves számlázási funkció még nem általánosan elérhető.</span><span class="sxs-lookup"><span data-stu-id="240d2-172">Note: the annual billing feature isn't yet generally available.</span></span> <span data-ttu-id="240d2-173">Az éves számlázási támogatás hamarosan elérhető lesz.</span><span class="sxs-lookup"><span data-stu-id="240d2-173">Support for annual billing is coming soon.</span></span> |
| <span data-ttu-id="240d2-174">Listaelemek</span><span class="sxs-lookup"><span data-stu-id="240d2-174">lineItems</span></span> | <span data-ttu-id="240d2-175">objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="240d2-175">array of objects</span></span> | <span data-ttu-id="240d2-176">Igen</span><span class="sxs-lookup"><span data-stu-id="240d2-176">Yes</span></span> | <span data-ttu-id="240d2-177">[**OrderLineItem**](#orderlineitem) -erőforrások tömbje.</span><span class="sxs-lookup"><span data-stu-id="240d2-177">An array of [**OrderLineItem**](#orderlineitem) resources.</span></span> |
| <span data-ttu-id="240d2-178">creationDate</span><span class="sxs-lookup"><span data-stu-id="240d2-178">creationDate</span></span> | <span data-ttu-id="240d2-179">sztring</span><span class="sxs-lookup"><span data-stu-id="240d2-179">string</span></span> | <span data-ttu-id="240d2-180">No</span><span class="sxs-lookup"><span data-stu-id="240d2-180">No</span></span> | <span data-ttu-id="240d2-181">A rendelés létrehozásának dátuma dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="240d2-181">The date the order was created, in date-time format.</span></span> <span data-ttu-id="240d2-182">A megrendelés sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="240d2-182">Applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="240d2-183">attribútumok</span><span class="sxs-lookup"><span data-stu-id="240d2-183">attributes</span></span> | <span data-ttu-id="240d2-184">object</span><span class="sxs-lookup"><span data-stu-id="240d2-184">object</span></span> | <span data-ttu-id="240d2-185">Nem</span><span class="sxs-lookup"><span data-stu-id="240d2-185">No</span></span> | <span data-ttu-id="240d2-186">A "objektumtípus": "Order" kifejezést tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="240d2-186">Contains "ObjectType": "Order".</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="240d2-187">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="240d2-187">OrderLineItem</span></span>

<span data-ttu-id="240d2-188">Ez a táblázat a kérelem törzsének **OrderLineItem** tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="240d2-188">This table describes the **OrderLineItem** properties in the request body.</span></span>

| <span data-ttu-id="240d2-189">Név</span><span class="sxs-lookup"><span data-stu-id="240d2-189">Name</span></span> | <span data-ttu-id="240d2-190">Típus</span><span class="sxs-lookup"><span data-stu-id="240d2-190">Type</span></span> | <span data-ttu-id="240d2-191">Kötelező</span><span class="sxs-lookup"><span data-stu-id="240d2-191">Required</span></span> | <span data-ttu-id="240d2-192">Leírás</span><span class="sxs-lookup"><span data-stu-id="240d2-192">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="240d2-193">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="240d2-193">lineItemNumber</span></span> | <span data-ttu-id="240d2-194">int</span><span class="sxs-lookup"><span data-stu-id="240d2-194">int</span></span> | <span data-ttu-id="240d2-195">Igen</span><span class="sxs-lookup"><span data-stu-id="240d2-195">Yes</span></span> | <span data-ttu-id="240d2-196">A gyűjtemény minden egyes sora egy egyedi sorszámot kap, amely a 0 és Count-1 közötti számlálást eredményezi.</span><span class="sxs-lookup"><span data-stu-id="240d2-196">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span> |
| <span data-ttu-id="240d2-197">offerId</span><span class="sxs-lookup"><span data-stu-id="240d2-197">offerId</span></span> | <span data-ttu-id="240d2-198">sztring</span><span class="sxs-lookup"><span data-stu-id="240d2-198">string</span></span> | <span data-ttu-id="240d2-199">Igen</span><span class="sxs-lookup"><span data-stu-id="240d2-199">Yes</span></span> | <span data-ttu-id="240d2-200">Az ajánlat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="240d2-200">The offer identifier.</span></span> |
| <span data-ttu-id="240d2-201">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="240d2-201">subscriptionId</span></span> | <span data-ttu-id="240d2-202">sztring</span><span class="sxs-lookup"><span data-stu-id="240d2-202">string</span></span> | <span data-ttu-id="240d2-203">No</span><span class="sxs-lookup"><span data-stu-id="240d2-203">No</span></span> | <span data-ttu-id="240d2-204">Az előfizetés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="240d2-204">The subscription identifier.</span></span> |
| <span data-ttu-id="240d2-205">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="240d2-205">parentSubscriptionId</span></span> | <span data-ttu-id="240d2-206">sztring</span><span class="sxs-lookup"><span data-stu-id="240d2-206">string</span></span> | <span data-ttu-id="240d2-207">No</span><span class="sxs-lookup"><span data-stu-id="240d2-207">No</span></span> | <span data-ttu-id="240d2-208">Választható.</span><span class="sxs-lookup"><span data-stu-id="240d2-208">Optional.</span></span> <span data-ttu-id="240d2-209">A szülő-előfizetés azonosítója egy kiegészítő ajánlatban.</span><span class="sxs-lookup"><span data-stu-id="240d2-209">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="240d2-210">Csak a JAVÍTÁSra vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="240d2-210">Applies to PATCH only.</span></span> |
| <span data-ttu-id="240d2-211">friendlyName</span><span class="sxs-lookup"><span data-stu-id="240d2-211">friendlyName</span></span> | <span data-ttu-id="240d2-212">sztring</span><span class="sxs-lookup"><span data-stu-id="240d2-212">string</span></span> | <span data-ttu-id="240d2-213">No</span><span class="sxs-lookup"><span data-stu-id="240d2-213">No</span></span> | <span data-ttu-id="240d2-214">Választható.</span><span class="sxs-lookup"><span data-stu-id="240d2-214">Optional.</span></span> <span data-ttu-id="240d2-215">A partner által az előfizetéshez megadott rövid név, amely segít a egyértelműsítse.</span><span class="sxs-lookup"><span data-stu-id="240d2-215">The friendly name for the subscription defined by the partner to help disambiguate.</span></span> |
| <span data-ttu-id="240d2-216">quantity</span><span class="sxs-lookup"><span data-stu-id="240d2-216">quantity</span></span> | <span data-ttu-id="240d2-217">int</span><span class="sxs-lookup"><span data-stu-id="240d2-217">int</span></span> | <span data-ttu-id="240d2-218">Igen</span><span class="sxs-lookup"><span data-stu-id="240d2-218">Yes</span></span> | <span data-ttu-id="240d2-219">A licenc alapú előfizetéshez tartozó licencek száma.</span><span class="sxs-lookup"><span data-stu-id="240d2-219">The number of licenses for a license-based subscription.</span></span> |
| <span data-ttu-id="240d2-220">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="240d2-220">partnerIdOnRecord</span></span> | <span data-ttu-id="240d2-221">sztring</span><span class="sxs-lookup"><span data-stu-id="240d2-221">string</span></span> | <span data-ttu-id="240d2-222">No</span><span class="sxs-lookup"><span data-stu-id="240d2-222">No</span></span> | <span data-ttu-id="240d2-223">Ha egy közvetett szolgáltató egy megrendelést helyez el egy közvetett viszonteladó nevében, töltse ki ezt a mezőt a **közvetett viszonteladóhoz** tartozó MPN-azonosítóval (soha nem a közvetett szolgáltató azonosítója).</span><span class="sxs-lookup"><span data-stu-id="240d2-223">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="240d2-224">Ez biztosítja az ösztönzők megfelelő könyvelését.</span><span class="sxs-lookup"><span data-stu-id="240d2-224">This ensures proper accounting for incentives.</span></span> <span data-ttu-id="240d2-225">**Nem sikerült megadni a viszonteladói MPN-azonosítót, mert a rendelés sikertelen lesz. Azonban a viszonteladó nem kerül rögzítésre, és a következményi ösztönző számítások nem tartalmazzák az értékesítést.**</span><span class="sxs-lookup"><span data-stu-id="240d2-225">**Failure to provide the reseller MPN ID does not cause the order to fail. However, the reseller isn't recorded and as a consequence incentive calculations may not include the sale.**</span></span> |
| <span data-ttu-id="240d2-226">attribútumok</span><span class="sxs-lookup"><span data-stu-id="240d2-226">attributes</span></span> | <span data-ttu-id="240d2-227">object</span><span class="sxs-lookup"><span data-stu-id="240d2-227">object</span></span> | <span data-ttu-id="240d2-228">Nem</span><span class="sxs-lookup"><span data-stu-id="240d2-228">No</span></span> | <span data-ttu-id="240d2-229">A "objektumtípus": "OrderLineItem" kifejezést tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="240d2-229">Contains "ObjectType":"OrderLineItem".</span></span> |

### <a name="request-example"></a><span data-ttu-id="240d2-230">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="240d2-230">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="240d2-231">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="240d2-231">REST response</span></span>

<span data-ttu-id="240d2-232">Ha a művelet sikeres, a válasz törzse tartalmazza a feltöltött [megrendelés](order-resources.md) erőforrását.</span><span class="sxs-lookup"><span data-stu-id="240d2-232">If successful, the response body contains the populated [Order](order-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="240d2-233">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="240d2-233">Response success and error codes</span></span>

<span data-ttu-id="240d2-234">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="240d2-234">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="240d2-235">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="240d2-235">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="240d2-236">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="240d2-236">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="240d2-237">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="240d2-237">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```
