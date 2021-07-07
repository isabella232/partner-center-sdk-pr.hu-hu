---
title: Ügyfélrendelés létrehozása közvetett viszonteladó számára
description: Megtudhatja, hogyan hozhat létre rendelést egy közvetett viszonteladó ügyfele számára a Partnerközpont API-k használatával. A cikk előfeltételeket, lépéseket és példákat tartalmaz.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253ba2289ea1f58e7d8eaa960d7d0daaa887f0d
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973543"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a><span data-ttu-id="07550-104">Megrendelés létrehozása közvetett viszonteladó ügyfelének</span><span class="sxs-lookup"><span data-stu-id="07550-104">Create an order for a customer of an indirect reseller</span></span>

<span data-ttu-id="07550-105">Rendelés létrehozása egy közvetett viszonteladó ügyfele számára.</span><span class="sxs-lookup"><span data-stu-id="07550-105">How to create an order for a customer of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07550-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="07550-106">Prerequisites</span></span>

- <span data-ttu-id="07550-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="07550-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="07550-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="07550-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="07550-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="07550-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="07550-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="07550-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="07550-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="07550-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="07550-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="07550-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="07550-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="07550-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="07550-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="07550-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="07550-115">A megvásárolni kívánt tétel ajánlatazonosítója.</span><span class="sxs-lookup"><span data-stu-id="07550-115">The offer identifier of the item to purchase.</span></span>

- <span data-ttu-id="07550-116">A közvetett viszonteladó bérlőazonosítója.</span><span class="sxs-lookup"><span data-stu-id="07550-116">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="07550-117">C\#</span><span class="sxs-lookup"><span data-stu-id="07550-117">C\#</span></span>

<span data-ttu-id="07550-118">Rendelés létrehozása egy közvetett viszonteladó ügyfele számára:</span><span class="sxs-lookup"><span data-stu-id="07550-118">To create an order for a customer of an indirect reseller:</span></span>

1. <span data-ttu-id="07550-119">Szerezze be a közvetett viszonteladók gyűjteményét, amelyek kapcsolatban vannak a bejelentkezett partnerrel.</span><span class="sxs-lookup"><span data-stu-id="07550-119">Get a collection of the indirect resellers that have a relationship with the signed-in partner.</span></span>

2. <span data-ttu-id="07550-120">Lekért egy helyi változót ahhoz a gyűjteményhez, amely megfelel a közvetett viszonteladó azonosítójának.</span><span class="sxs-lookup"><span data-stu-id="07550-120">Get a local variable to the item in the collection that matches the indirect reseller ID.</span></span> <span data-ttu-id="07550-121">Ez a lépés segít elérni a viszonteladó [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) tulajdonságát a rendelés létrehozásakor.</span><span class="sxs-lookup"><span data-stu-id="07550-121">This step helps you access the reseller's [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) property when you create the order.</span></span>

3. <span data-ttu-id="07550-122">Példányositsa az [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) objektumot, és állítsa a [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) tulajdonságot az ügyfélazonosítóra az ügyfél rögzítéséhez.</span><span class="sxs-lookup"><span data-stu-id="07550-122">Instantiate an [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and set the [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) property to the customer identifier in order to record the customer.</span></span>

4. <span data-ttu-id="07550-123">Hozzon létre egy [**listát az OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objektumokból, és rendelje hozzá a listát a rendelés [**LineItems tulajdonságához.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems)</span><span class="sxs-lookup"><span data-stu-id="07550-123">Create a list of [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objects, and assign the list to the order's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) property.</span></span> <span data-ttu-id="07550-124">Minden rendeléssorelem egy adott ajánlat vásárlási adatait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="07550-124">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="07550-125">Minden sorelemben töltse fel a [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) tulajdonságot a közvetett viszonteladó MPN-azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="07550-125">Be sure to populate the [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) property in each line item with the MPN ID of the indirect reseller.</span></span> <span data-ttu-id="07550-126">Legalább egy megrendeléssor-elemnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="07550-126">You must have at least one order line item.</span></span>

5. <span data-ttu-id="07550-127">Szerezzen be egy interfészt a műveletek megrendelésére az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódus ügyfél-azonosítóval való hívásával az ügyfél azonosításához, majd a felület az Orders tulajdonságból [**való lekérésével.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)</span><span class="sxs-lookup"><span data-stu-id="07550-127">Obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

6. <span data-ttu-id="07550-128">A rendelés [**létrehozásához**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) hívja meg a Create vagy [**a CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="07550-128">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method to create the order.</span></span>

### <a name="c-example"></a><span data-ttu-id="07550-129">C \# példa</span><span class="sxs-lookup"><span data-stu-id="07550-129">C\# example</span></span>

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

<span data-ttu-id="07550-130">**Minta:** [Konzoltesztelő](console-test-app.md)**alkalmazás Project:** Partnerközpont SDK Samples **Class**: PlaceOrderForCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="07550-130">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: PlaceOrderForCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="07550-131">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="07550-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="07550-132">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="07550-132">Request syntax</span></span>

| <span data-ttu-id="07550-133">Metódus</span><span class="sxs-lookup"><span data-stu-id="07550-133">Method</span></span>   | <span data-ttu-id="07550-134">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="07550-134">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="07550-135">**Post**</span><span class="sxs-lookup"><span data-stu-id="07550-135">**POST**</span></span> | <span data-ttu-id="07550-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="07550-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="07550-137">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="07550-137">URI parameters</span></span>

<span data-ttu-id="07550-138">Az ügyfél azonosításához használja a következő path paramétert.</span><span class="sxs-lookup"><span data-stu-id="07550-138">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="07550-139">Név</span><span class="sxs-lookup"><span data-stu-id="07550-139">Name</span></span>        | <span data-ttu-id="07550-140">Típus</span><span class="sxs-lookup"><span data-stu-id="07550-140">Type</span></span>   | <span data-ttu-id="07550-141">Kötelező</span><span class="sxs-lookup"><span data-stu-id="07550-141">Required</span></span> | <span data-ttu-id="07550-142">Leírás</span><span class="sxs-lookup"><span data-stu-id="07550-142">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="07550-143">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="07550-143">customer-id</span></span> | <span data-ttu-id="07550-144">sztring</span><span class="sxs-lookup"><span data-stu-id="07550-144">string</span></span> | <span data-ttu-id="07550-145">Igen</span><span class="sxs-lookup"><span data-stu-id="07550-145">Yes</span></span>      | <span data-ttu-id="07550-146">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="07550-146">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="07550-147">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="07550-147">Request headers</span></span>

<span data-ttu-id="07550-148">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="07550-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="07550-149">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="07550-149">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="07550-150">Sorrend</span><span class="sxs-lookup"><span data-stu-id="07550-150">Order</span></span>

<span data-ttu-id="07550-151">Ez a táblázat a kérelem törzsében található **Order (Rendelés)** tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="07550-151">This table describes the **Order** properties in the request body.</span></span>

| <span data-ttu-id="07550-152">Név</span><span class="sxs-lookup"><span data-stu-id="07550-152">Name</span></span> | <span data-ttu-id="07550-153">Típus</span><span class="sxs-lookup"><span data-stu-id="07550-153">Type</span></span> | <span data-ttu-id="07550-154">Kötelező</span><span class="sxs-lookup"><span data-stu-id="07550-154">Required</span></span> | <span data-ttu-id="07550-155">Leírás</span><span class="sxs-lookup"><span data-stu-id="07550-155">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="07550-156">id</span><span class="sxs-lookup"><span data-stu-id="07550-156">id</span></span> | <span data-ttu-id="07550-157">sztring</span><span class="sxs-lookup"><span data-stu-id="07550-157">string</span></span> | <span data-ttu-id="07550-158">No</span><span class="sxs-lookup"><span data-stu-id="07550-158">No</span></span> | <span data-ttu-id="07550-159">A rendelés sikeres létrehozása után megadott rendelésazonosító.</span><span class="sxs-lookup"><span data-stu-id="07550-159">An order identifier that is supplied upon successful creation of the order.</span></span> |
| <span data-ttu-id="07550-160">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="07550-160">referenceCustomerId</span></span> | <span data-ttu-id="07550-161">sztring</span><span class="sxs-lookup"><span data-stu-id="07550-161">string</span></span> | <span data-ttu-id="07550-162">Igen</span><span class="sxs-lookup"><span data-stu-id="07550-162">Yes</span></span> | <span data-ttu-id="07550-163">Az ügyfél azonosítója.</span><span class="sxs-lookup"><span data-stu-id="07550-163">The customer identifier.</span></span> |
| <span data-ttu-id="07550-164">billingCycle</span><span class="sxs-lookup"><span data-stu-id="07550-164">billingCycle</span></span> | <span data-ttu-id="07550-165">sztring</span><span class="sxs-lookup"><span data-stu-id="07550-165">string</span></span> | <span data-ttu-id="07550-166">No</span><span class="sxs-lookup"><span data-stu-id="07550-166">No</span></span> | <span data-ttu-id="07550-167">A partner számlázásának gyakorisága a rendeléshez.</span><span class="sxs-lookup"><span data-stu-id="07550-167">The frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="07550-168">Az alapértelmezett érték a Havi, és a rendelés &quot; sikeres létrehozásakor lesz &quot; alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="07550-168">The default is &quot;Monthly&quot; and is applied upon successful creation of the order.</span></span> <span data-ttu-id="07550-169">A támogatott értékek a [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype)típusban található tagnevek.</span><span class="sxs-lookup"><span data-stu-id="07550-169">Supported values are the member names found in [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span></span> <span data-ttu-id="07550-170">Megjegyzés: Az éves számlázási funkció még nem általánosan elérhető.</span><span class="sxs-lookup"><span data-stu-id="07550-170">Note: the annual billing feature isn't yet generally available.</span></span> <span data-ttu-id="07550-171">Az éves számlázás támogatása hamarosan 2017-hez közeledik.</span><span class="sxs-lookup"><span data-stu-id="07550-171">Support for annual billing is coming soon.</span></span> |
| <span data-ttu-id="07550-172">lineItems (sorsorok)</span><span class="sxs-lookup"><span data-stu-id="07550-172">lineItems</span></span> | <span data-ttu-id="07550-173">objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="07550-173">array of objects</span></span> | <span data-ttu-id="07550-174">Igen</span><span class="sxs-lookup"><span data-stu-id="07550-174">Yes</span></span> | <span data-ttu-id="07550-175">[**OrderLineItem**](#orderlineitem) erőforrások tömbje.</span><span class="sxs-lookup"><span data-stu-id="07550-175">An array of [**OrderLineItem**](#orderlineitem) resources.</span></span> |
| <span data-ttu-id="07550-176">creationDate (Létrehozás dátuma)</span><span class="sxs-lookup"><span data-stu-id="07550-176">creationDate</span></span> | <span data-ttu-id="07550-177">sztring</span><span class="sxs-lookup"><span data-stu-id="07550-177">string</span></span> | <span data-ttu-id="07550-178">No</span><span class="sxs-lookup"><span data-stu-id="07550-178">No</span></span> | <span data-ttu-id="07550-179">A rendelés létrehozási dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="07550-179">The date the order was created, in date-time format.</span></span> <span data-ttu-id="07550-180">A rendelés sikeres létrehozásakor alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="07550-180">Applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="07550-181">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="07550-181">attributes</span></span> | <span data-ttu-id="07550-182">object</span><span class="sxs-lookup"><span data-stu-id="07550-182">object</span></span> | <span data-ttu-id="07550-183">Nem</span><span class="sxs-lookup"><span data-stu-id="07550-183">No</span></span> | <span data-ttu-id="07550-184">Tartalmazza az "ObjectType": "Order" típust.</span><span class="sxs-lookup"><span data-stu-id="07550-184">Contains "ObjectType": "Order".</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="07550-185">OrderLineItem (Megrendelési vonal)</span><span class="sxs-lookup"><span data-stu-id="07550-185">OrderLineItem</span></span>

<span data-ttu-id="07550-186">Ez a táblázat a kérelem törzsében található **OrderLineItem** tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="07550-186">This table describes the **OrderLineItem** properties in the request body.</span></span>

| <span data-ttu-id="07550-187">Név</span><span class="sxs-lookup"><span data-stu-id="07550-187">Name</span></span> | <span data-ttu-id="07550-188">Típus</span><span class="sxs-lookup"><span data-stu-id="07550-188">Type</span></span> | <span data-ttu-id="07550-189">Kötelező</span><span class="sxs-lookup"><span data-stu-id="07550-189">Required</span></span> | <span data-ttu-id="07550-190">Leírás</span><span class="sxs-lookup"><span data-stu-id="07550-190">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="07550-191">lineItemNumber (sortem száma)</span><span class="sxs-lookup"><span data-stu-id="07550-191">lineItemNumber</span></span> | <span data-ttu-id="07550-192">int</span><span class="sxs-lookup"><span data-stu-id="07550-192">int</span></span> | <span data-ttu-id="07550-193">Igen</span><span class="sxs-lookup"><span data-stu-id="07550-193">Yes</span></span> | <span data-ttu-id="07550-194">A gyűjtemény minden soreleme egyedi sorszámot kap, amely 0-tól count-1-ig számol.</span><span class="sxs-lookup"><span data-stu-id="07550-194">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span> |
| <span data-ttu-id="07550-195">offerId (ajánlatazonosító)</span><span class="sxs-lookup"><span data-stu-id="07550-195">offerId</span></span> | <span data-ttu-id="07550-196">sztring</span><span class="sxs-lookup"><span data-stu-id="07550-196">string</span></span> | <span data-ttu-id="07550-197">Igen</span><span class="sxs-lookup"><span data-stu-id="07550-197">Yes</span></span> | <span data-ttu-id="07550-198">Az ajánlat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="07550-198">The offer identifier.</span></span> |
| <span data-ttu-id="07550-199">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="07550-199">subscriptionId</span></span> | <span data-ttu-id="07550-200">sztring</span><span class="sxs-lookup"><span data-stu-id="07550-200">string</span></span> | <span data-ttu-id="07550-201">No</span><span class="sxs-lookup"><span data-stu-id="07550-201">No</span></span> | <span data-ttu-id="07550-202">Az előfizetés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="07550-202">The subscription identifier.</span></span> |
| <span data-ttu-id="07550-203">parentSubscriptionId (parentSubscriptionId)</span><span class="sxs-lookup"><span data-stu-id="07550-203">parentSubscriptionId</span></span> | <span data-ttu-id="07550-204">sztring</span><span class="sxs-lookup"><span data-stu-id="07550-204">string</span></span> | <span data-ttu-id="07550-205">No</span><span class="sxs-lookup"><span data-stu-id="07550-205">No</span></span> | <span data-ttu-id="07550-206">Választható.</span><span class="sxs-lookup"><span data-stu-id="07550-206">Optional.</span></span> <span data-ttu-id="07550-207">A szülő-előfizetés azonosítója egy bővítményajánlatban.</span><span class="sxs-lookup"><span data-stu-id="07550-207">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="07550-208">Csak a PATCH-re vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="07550-208">Applies to PATCH only.</span></span> |
| <span data-ttu-id="07550-209">friendlyName (rövid név)</span><span class="sxs-lookup"><span data-stu-id="07550-209">friendlyName</span></span> | <span data-ttu-id="07550-210">sztring</span><span class="sxs-lookup"><span data-stu-id="07550-210">string</span></span> | <span data-ttu-id="07550-211">No</span><span class="sxs-lookup"><span data-stu-id="07550-211">No</span></span> | <span data-ttu-id="07550-212">Választható.</span><span class="sxs-lookup"><span data-stu-id="07550-212">Optional.</span></span> <span data-ttu-id="07550-213">A partner által meghatározott előfizetés rövid neve a egyértelműséghez.</span><span class="sxs-lookup"><span data-stu-id="07550-213">The friendly name for the subscription defined by the partner to help disambiguate.</span></span> |
| <span data-ttu-id="07550-214">quantity</span><span class="sxs-lookup"><span data-stu-id="07550-214">quantity</span></span> | <span data-ttu-id="07550-215">int</span><span class="sxs-lookup"><span data-stu-id="07550-215">int</span></span> | <span data-ttu-id="07550-216">Igen</span><span class="sxs-lookup"><span data-stu-id="07550-216">Yes</span></span> | <span data-ttu-id="07550-217">A licencalapú előfizetések licenceinek száma.</span><span class="sxs-lookup"><span data-stu-id="07550-217">The number of licenses for a license-based subscription.</span></span> |
| <span data-ttu-id="07550-218">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="07550-218">partnerIdOnRecord</span></span> | <span data-ttu-id="07550-219">sztring</span><span class="sxs-lookup"><span data-stu-id="07550-219">string</span></span> | <span data-ttu-id="07550-220">No</span><span class="sxs-lookup"><span data-stu-id="07550-220">No</span></span> | <span data-ttu-id="07550-221">Ha egy közvetett szolgáltató egy közvetett viszonteladó nevében ad ki rendelést, akkor ezt a mezőt csak a közvetett viszonteladó MPN-azonosítójával **töltse** fel (soha ne a közvetett szolgáltató azonosítójával).</span><span class="sxs-lookup"><span data-stu-id="07550-221">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="07550-222">Ez biztosítja az ösztönzők megfelelő elszámolását.</span><span class="sxs-lookup"><span data-stu-id="07550-222">This ensures proper accounting for incentives.</span></span> <span data-ttu-id="07550-223">**Ha nem adja meg a viszonteladó MPN-azonosítóját, a rendelés nem fog meghiúsulni. A viszonteladót azonban nem rögzíti a rendszer, ezért előfordulhat, hogy az ösztönzők számításai nem tartalmazzák az értékesítést.**</span><span class="sxs-lookup"><span data-stu-id="07550-223">**Failure to provide the reseller MPN ID does not cause the order to fail. However, the reseller isn't recorded and as a consequence incentive calculations may not include the sale.**</span></span> |
| <span data-ttu-id="07550-224">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="07550-224">attributes</span></span> | <span data-ttu-id="07550-225">object</span><span class="sxs-lookup"><span data-stu-id="07550-225">object</span></span> | <span data-ttu-id="07550-226">Nem</span><span class="sxs-lookup"><span data-stu-id="07550-226">No</span></span> | <span data-ttu-id="07550-227">Az "ObjectType":"OrderLineItem" adatokat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="07550-227">Contains "ObjectType":"OrderLineItem".</span></span> |

### <a name="request-example"></a><span data-ttu-id="07550-228">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="07550-228">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="07550-229">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="07550-229">REST response</span></span>

<span data-ttu-id="07550-230">Ha a művelet sikeres, a válasz törzse tartalmazza a kitöltve [order erőforrást.](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="07550-230">If successful, the response body contains the populated [Order](order-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="07550-231">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="07550-231">Response success and error codes</span></span>

<span data-ttu-id="07550-232">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="07550-232">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="07550-233">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="07550-233">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="07550-234">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="07550-234">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="07550-235">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="07550-235">Response example</span></span>

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
