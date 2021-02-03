---
title: Bővítmény vásárlása egy előfizetéshez
description: Bővítmény vásárlása meglévő előfizetéshez.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 975a2516bccdc6274bfec5d6a3286a649fc4f808
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768312"
---
# <a name="purchase-an-add-on-to-a-subscription"></a><span data-ttu-id="01553-103">Bővítmény vásárlása egy előfizetéshez</span><span class="sxs-lookup"><span data-stu-id="01553-103">Purchase an add-on to a subscription</span></span>

<span data-ttu-id="01553-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="01553-104">**Applies To**</span></span>

- <span data-ttu-id="01553-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="01553-105">Partner Center</span></span>
- <span data-ttu-id="01553-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="01553-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="01553-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="01553-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="01553-108">Bővítmény vásárlása meglévő előfizetéshez.</span><span class="sxs-lookup"><span data-stu-id="01553-108">How to purchase an add-on to an existing subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01553-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="01553-109">Prerequisites</span></span>

- <span data-ttu-id="01553-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="01553-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="01553-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="01553-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="01553-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="01553-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="01553-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="01553-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="01553-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="01553-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="01553-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="01553-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="01553-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="01553-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="01553-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="01553-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="01553-118">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="01553-118">A subscription ID.</span></span> <span data-ttu-id="01553-119">Ezt a meglévő előfizetést kell megvásárolnia.</span><span class="sxs-lookup"><span data-stu-id="01553-119">This is the existing subscription for which to purchase an add-on offer.</span></span>

- <span data-ttu-id="01553-120">A megvásárolni kívánt bővítményt azonosító ajánlat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="01553-120">An offer ID that identifies the add-on offer to purchase.</span></span>

## <a name="purchasing-an-add-on-through-code"></a><span data-ttu-id="01553-121">Kiegészítő csomag megvásárlása kód használatával</span><span class="sxs-lookup"><span data-stu-id="01553-121">Purchasing an add-on through code</span></span>

<span data-ttu-id="01553-122">Ha hozzáad egy bővítményt egy előfizetéshez, az eredeti előfizetési rendelést a bővítmény sorrendjével frissíti.</span><span class="sxs-lookup"><span data-stu-id="01553-122">When you purchase an add-on to a subscription you are updating the original subscription order with the order for the add-on.</span></span> <span data-ttu-id="01553-123">A következő példában a Vevőkód az ügyfél-azonosító, a subscriptionId az előfizetés azonosítója, a addOnOfferId pedig a bővítmény ajánlatának azonosítója.</span><span class="sxs-lookup"><span data-stu-id="01553-123">In the following, customerId is the customer ID, subscriptionId is the subscription ID, and addOnOfferId is the offer ID for the add-on.</span></span>

<span data-ttu-id="01553-124">A lépések a következők:</span><span class="sxs-lookup"><span data-stu-id="01553-124">Here are the steps:</span></span>

1.  <span data-ttu-id="01553-125">Adapter beszerzése az előfizetés műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="01553-125">Get an interface to the operations for the subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  <span data-ttu-id="01553-126">Használja ezt a felületet egy előfizetési objektum létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="01553-126">Use that interface to instantiate a subscription object.</span></span> <span data-ttu-id="01553-127">Így megkapja a szülő-előfizetés részleteit, beleértve a megrendelés azonosítóját is.</span><span class="sxs-lookup"><span data-stu-id="01553-127">This gets you the parent subscription details, including the order id.</span></span>

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  <span data-ttu-id="01553-128">Új [**megrendelési**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) objektum létrehozása</span><span class="sxs-lookup"><span data-stu-id="01553-128">Instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object.</span></span> <span data-ttu-id="01553-129">Ez a megrendelési példány az előfizetés megvásárlásához használt eredeti megrendelés frissítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="01553-129">This order instance is used to update the original order used to purchase the subscription.</span></span> <span data-ttu-id="01553-130">Vegyen fel egy egysoros tételt a bővítményt jelölő sorrendbe.</span><span class="sxs-lookup"><span data-stu-id="01553-130">Add a single line item to the order that represents the add-on.</span></span>
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  <span data-ttu-id="01553-131">Frissítse az előfizetés eredeti sorrendjét a bővítmény új sorrendjével.</span><span class="sxs-lookup"><span data-stu-id="01553-131">Update the original order for the subscription with the new order for the add-on.</span></span>
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a><span data-ttu-id="01553-132">C\#</span><span class="sxs-lookup"><span data-stu-id="01553-132">C\#</span></span>

<span data-ttu-id="01553-133">Egy bővítmény megvásárlásához először az [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust kell beszereznie az ügyfél-azonosítóval, és az [**előfizetések. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódussal kell megadnia azt az előfizetést, amely a kiegészítő ajánlattal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="01553-133">To purchase an add-on, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription that has the add-on offer.</span></span> <span data-ttu-id="01553-134">Ezzel a [**csatolóval**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) kérheti le az előfizetés részleteit a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get)utasítás meghívásával.</span><span class="sxs-lookup"><span data-stu-id="01553-134">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span> <span data-ttu-id="01553-135">Miért van szüksége az előfizetés részleteire?</span><span class="sxs-lookup"><span data-stu-id="01553-135">Why do you need the subscription details?</span></span> <span data-ttu-id="01553-136">Mivel szüksége van az előfizetési rendeléshez tartozó Order ID azonosítóra.</span><span class="sxs-lookup"><span data-stu-id="01553-136">Because you need the order id of the subscription order.</span></span> <span data-ttu-id="01553-137">Ez a bővítmény frissítésének sorrendje.</span><span class="sxs-lookup"><span data-stu-id="01553-137">That's the order to be updated with the add-on.</span></span>

<span data-ttu-id="01553-138">Ezután hozza létre az új [**megrendelési**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) objektumot, és töltse fel egyetlen [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) -példánnyal, amely tartalmazza a bővítmény azonosítására szolgáló adatokat, ahogy az a következő kódrészletben látható.</span><span class="sxs-lookup"><span data-stu-id="01553-138">Next, instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and populate it with a single [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) instance that contains the information to identify the add-on, as shown in the following code snippet.</span></span> <span data-ttu-id="01553-139">Ezzel az új objektummal frissítheti az előfizetési sorrendet a bővítmény használatával.</span><span class="sxs-lookup"><span data-stu-id="01553-139">You'll use this new object to update the subscription order with the add-on.</span></span> <span data-ttu-id="01553-140">Végül hívja meg a [**patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) metódust az előfizetési sorrend frissítéséhez, miután először azonosítja az ügyfelet a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) és a Orders [**. ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span><span class="sxs-lookup"><span data-stu-id="01553-140">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) method to update the subscription order, after first identifying the customer with [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) and the order with [**Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

<span data-ttu-id="01553-141">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="01553-141">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="01553-142">**Projekt**: partner Center SDK Samples **osztály**: AddSubscriptionAddOn.cs</span><span class="sxs-lookup"><span data-stu-id="01553-142">**Project**: Partner Center SDK Samples **Class**: AddSubscriptionAddOn.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="01553-143">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="01553-143">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="01553-144">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="01553-144">Request syntax</span></span>

| <span data-ttu-id="01553-145">Metódus</span><span class="sxs-lookup"><span data-stu-id="01553-145">Method</span></span>    | <span data-ttu-id="01553-146">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="01553-146">Request URI</span></span>                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="01553-147">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="01553-147">**PATCH**</span></span> | <span data-ttu-id="01553-148">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="01553-148">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="01553-149">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="01553-149">URI parameters</span></span>

<span data-ttu-id="01553-150">A következő paraméterek használatával azonosíthatja az ügyfelet és a sorrendet.</span><span class="sxs-lookup"><span data-stu-id="01553-150">Use the following parameters to identify the customer and order.</span></span>

| <span data-ttu-id="01553-151">Név</span><span class="sxs-lookup"><span data-stu-id="01553-151">Name</span></span>                   | <span data-ttu-id="01553-152">Típus</span><span class="sxs-lookup"><span data-stu-id="01553-152">Type</span></span>     | <span data-ttu-id="01553-153">Kötelező</span><span class="sxs-lookup"><span data-stu-id="01553-153">Required</span></span> | <span data-ttu-id="01553-154">Leírás</span><span class="sxs-lookup"><span data-stu-id="01553-154">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="01553-155">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="01553-155">**customer-tenant-id**</span></span> | <span data-ttu-id="01553-156">**guid**</span><span class="sxs-lookup"><span data-stu-id="01553-156">**guid**</span></span> | <span data-ttu-id="01553-157">Y</span><span class="sxs-lookup"><span data-stu-id="01553-157">Y</span></span>        | <span data-ttu-id="01553-158">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító** , amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="01553-158">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="01553-159">**megrendelés azonosítója**</span><span class="sxs-lookup"><span data-stu-id="01553-159">**order-id**</span></span>           | <span data-ttu-id="01553-160">**guid**</span><span class="sxs-lookup"><span data-stu-id="01553-160">**guid**</span></span> | <span data-ttu-id="01553-161">Y</span><span class="sxs-lookup"><span data-stu-id="01553-161">Y</span></span>        | <span data-ttu-id="01553-162">A sorrend azonosítója.</span><span class="sxs-lookup"><span data-stu-id="01553-162">The order identifier.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="01553-163">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="01553-163">Request headers</span></span>

<span data-ttu-id="01553-164">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="01553-164">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="01553-165">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="01553-165">Request body</span></span>

<span data-ttu-id="01553-166">A következő táblázatok a kérés törzsének tulajdonságait ismertetik.</span><span class="sxs-lookup"><span data-stu-id="01553-166">The following tables describe the properties in the request body.</span></span>

## <a name="order"></a><span data-ttu-id="01553-167">Sorrend</span><span class="sxs-lookup"><span data-stu-id="01553-167">Order</span></span>

| <span data-ttu-id="01553-168">Név</span><span class="sxs-lookup"><span data-stu-id="01553-168">Name</span></span>                | <span data-ttu-id="01553-169">Típus</span><span class="sxs-lookup"><span data-stu-id="01553-169">Type</span></span>             | <span data-ttu-id="01553-170">Kötelező</span><span class="sxs-lookup"><span data-stu-id="01553-170">Required</span></span> | <span data-ttu-id="01553-171">Leírás</span><span class="sxs-lookup"><span data-stu-id="01553-171">Description</span></span>                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| <span data-ttu-id="01553-172">Id</span><span class="sxs-lookup"><span data-stu-id="01553-172">Id</span></span>                  | <span data-ttu-id="01553-173">sztring</span><span class="sxs-lookup"><span data-stu-id="01553-173">string</span></span>           | <span data-ttu-id="01553-174">N</span><span class="sxs-lookup"><span data-stu-id="01553-174">N</span></span>        | <span data-ttu-id="01553-175">A megrendelés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="01553-175">The order ID.</span></span>                                        |
| <span data-ttu-id="01553-176">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="01553-176">ReferenceCustomerId</span></span> | <span data-ttu-id="01553-177">sztring</span><span class="sxs-lookup"><span data-stu-id="01553-177">string</span></span>           | <span data-ttu-id="01553-178">Y</span><span class="sxs-lookup"><span data-stu-id="01553-178">Y</span></span>        | <span data-ttu-id="01553-179">Az ügyfél-azonosító.</span><span class="sxs-lookup"><span data-stu-id="01553-179">The customer ID.</span></span>                                     |
| <span data-ttu-id="01553-180">Listaelemek</span><span class="sxs-lookup"><span data-stu-id="01553-180">LineItems</span></span>           | <span data-ttu-id="01553-181">objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="01553-181">array of objects</span></span> | <span data-ttu-id="01553-182">Y</span><span class="sxs-lookup"><span data-stu-id="01553-182">Y</span></span>        | <span data-ttu-id="01553-183">[OrderLineItem](#orderlineitem) objektumok tömbje.</span><span class="sxs-lookup"><span data-stu-id="01553-183">An array of [OrderLineItem](#orderlineitem) objects.</span></span> |
| <span data-ttu-id="01553-184">CreationDate</span><span class="sxs-lookup"><span data-stu-id="01553-184">CreationDate</span></span>        | <span data-ttu-id="01553-185">sztring</span><span class="sxs-lookup"><span data-stu-id="01553-185">string</span></span>           | <span data-ttu-id="01553-186">N</span><span class="sxs-lookup"><span data-stu-id="01553-186">N</span></span>        | <span data-ttu-id="01553-187">A rendelés létrehozásának dátuma dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="01553-187">The date the order was created, in date-time format.</span></span> |
| <span data-ttu-id="01553-188">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="01553-188">Attributes</span></span>          | <span data-ttu-id="01553-189">object</span><span class="sxs-lookup"><span data-stu-id="01553-189">object</span></span>           | <span data-ttu-id="01553-190">N</span><span class="sxs-lookup"><span data-stu-id="01553-190">N</span></span>        | <span data-ttu-id="01553-191">A "objektumtípus": "Order" kifejezést tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="01553-191">Contains "ObjectType": "Order".</span></span>                      |

## <a name="orderlineitem"></a><span data-ttu-id="01553-192">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="01553-192">OrderLineItem</span></span>

| <span data-ttu-id="01553-193">Név</span><span class="sxs-lookup"><span data-stu-id="01553-193">Name</span></span>                 | <span data-ttu-id="01553-194">Típus</span><span class="sxs-lookup"><span data-stu-id="01553-194">Type</span></span>   | <span data-ttu-id="01553-195">Kötelező</span><span class="sxs-lookup"><span data-stu-id="01553-195">Required</span></span> | <span data-ttu-id="01553-196">Leírás</span><span class="sxs-lookup"><span data-stu-id="01553-196">Description</span></span>                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="01553-197">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="01553-197">LineItemNumber</span></span>       | <span data-ttu-id="01553-198">szám</span><span class="sxs-lookup"><span data-stu-id="01553-198">number</span></span> | <span data-ttu-id="01553-199">Y</span><span class="sxs-lookup"><span data-stu-id="01553-199">Y</span></span>        | <span data-ttu-id="01553-200">A sor elemének száma, a 0-tól kezdődően.</span><span class="sxs-lookup"><span data-stu-id="01553-200">The line item number, starting with 0.</span></span>                       |
| <span data-ttu-id="01553-201">OfferId</span><span class="sxs-lookup"><span data-stu-id="01553-201">OfferId</span></span>              | <span data-ttu-id="01553-202">sztring</span><span class="sxs-lookup"><span data-stu-id="01553-202">string</span></span> | <span data-ttu-id="01553-203">Y</span><span class="sxs-lookup"><span data-stu-id="01553-203">Y</span></span>        | <span data-ttu-id="01553-204">A bővítmény ajánlatának azonosítója.</span><span class="sxs-lookup"><span data-stu-id="01553-204">The offer ID of the add-on.</span></span>                                  |
| <span data-ttu-id="01553-205">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="01553-205">SubscriptionId</span></span>       | <span data-ttu-id="01553-206">sztring</span><span class="sxs-lookup"><span data-stu-id="01553-206">string</span></span> | <span data-ttu-id="01553-207">N</span><span class="sxs-lookup"><span data-stu-id="01553-207">N</span></span>        | <span data-ttu-id="01553-208">A megvásárolt bővítmény-előfizetés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="01553-208">The ID of the add-on subscription purchased.</span></span>                 |
| <span data-ttu-id="01553-209">ParentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="01553-209">ParentSubscriptionId</span></span> | <span data-ttu-id="01553-210">sztring</span><span class="sxs-lookup"><span data-stu-id="01553-210">string</span></span> | <span data-ttu-id="01553-211">Y</span><span class="sxs-lookup"><span data-stu-id="01553-211">Y</span></span>        | <span data-ttu-id="01553-212">Annak a szülő-előfizetésnek az azonosítója, amelyhez a kiegészítő ajánlat tartozik.</span><span class="sxs-lookup"><span data-stu-id="01553-212">The ID of the parent subscription that has the add-on offer.</span></span> |
| <span data-ttu-id="01553-213">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="01553-213">FriendlyName</span></span>         | <span data-ttu-id="01553-214">sztring</span><span class="sxs-lookup"><span data-stu-id="01553-214">string</span></span> | <span data-ttu-id="01553-215">N</span><span class="sxs-lookup"><span data-stu-id="01553-215">N</span></span>        | <span data-ttu-id="01553-216">A sorhoz tartozó rövid név</span><span class="sxs-lookup"><span data-stu-id="01553-216">The friendly name for this line item.</span></span>                        |
| <span data-ttu-id="01553-217">Mennyiség</span><span class="sxs-lookup"><span data-stu-id="01553-217">Quantity</span></span>             | <span data-ttu-id="01553-218">szám</span><span class="sxs-lookup"><span data-stu-id="01553-218">number</span></span> | <span data-ttu-id="01553-219">Y</span><span class="sxs-lookup"><span data-stu-id="01553-219">Y</span></span>        | <span data-ttu-id="01553-220">A licencek száma.</span><span class="sxs-lookup"><span data-stu-id="01553-220">The number of licenses.</span></span>                                      |
| <span data-ttu-id="01553-221">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="01553-221">PartnerIdOnRecord</span></span>    | <span data-ttu-id="01553-222">sztring</span><span class="sxs-lookup"><span data-stu-id="01553-222">string</span></span> | <span data-ttu-id="01553-223">N</span><span class="sxs-lookup"><span data-stu-id="01553-223">N</span></span>        | <span data-ttu-id="01553-224">A rekord partnerének MPN-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="01553-224">The MPN ID of the partner of record.</span></span>                         |
| <span data-ttu-id="01553-225">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="01553-225">Attributes</span></span>           | <span data-ttu-id="01553-226">object</span><span class="sxs-lookup"><span data-stu-id="01553-226">object</span></span> | <span data-ttu-id="01553-227">N</span><span class="sxs-lookup"><span data-stu-id="01553-227">N</span></span>        | <span data-ttu-id="01553-228">A "objektumtípus": "OrderLineItem" kifejezést tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="01553-228">Contains "ObjectType": "OrderLineItem".</span></span>                      |

### <a name="request-example"></a><span data-ttu-id="01553-229">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="01553-229">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
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

## <a name="rest-response"></a><span data-ttu-id="01553-230">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="01553-230">REST response</span></span>

<span data-ttu-id="01553-231">Ha ez sikeres, a metódus visszaadja a frissített előfizetés sorrendjét a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="01553-231">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="01553-232">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="01553-232">Response success and error codes</span></span>

<span data-ttu-id="01553-233">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="01553-233">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="01553-234">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="01553-234">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="01553-235">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="01553-235">For the full list, see [Partner Center Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="01553-236">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="01553-236">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "none",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```
