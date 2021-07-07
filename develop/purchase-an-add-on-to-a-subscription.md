---
title: Bővítmény vásárlása egy előfizetéshez
description: Bővítmény vásárlása meglévő előfizetéshez.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d8b700a2ad41a37ca0ad745f3e7767449974b18a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547682"
---
# <a name="purchase-an-add-on-to-a-subscription"></a><span data-ttu-id="5e217-103">Bővítmény vásárlása egy előfizetéshez</span><span class="sxs-lookup"><span data-stu-id="5e217-103">Purchase an add-on to a subscription</span></span>

<span data-ttu-id="5e217-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5e217-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5e217-105">Bővítmény vásárlása meglévő előfizetéshez.</span><span class="sxs-lookup"><span data-stu-id="5e217-105">How to purchase an add-on to an existing subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e217-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5e217-106">Prerequisites</span></span>

- <span data-ttu-id="5e217-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5e217-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5e217-108">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="5e217-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5e217-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5e217-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5e217-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="5e217-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5e217-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="5e217-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5e217-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="5e217-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5e217-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="5e217-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5e217-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5e217-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5e217-115">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="5e217-115">A subscription ID.</span></span> <span data-ttu-id="5e217-116">Ez az a meglévő előfizetés, amelyhez bővítményajánlatot szeretne vásárolni.</span><span class="sxs-lookup"><span data-stu-id="5e217-116">This is the existing subscription for which to purchase an add-on offer.</span></span>

- <span data-ttu-id="5e217-117">Egy ajánlatazonosító, amely azonosítja a vásárolható bővítményajánlatot.</span><span class="sxs-lookup"><span data-stu-id="5e217-117">An offer ID that identifies the add-on offer to purchase.</span></span>

## <a name="purchasing-an-add-on-through-code"></a><span data-ttu-id="5e217-118">Bővítmény vásárlása kóddal</span><span class="sxs-lookup"><span data-stu-id="5e217-118">Purchasing an add-on through code</span></span>

<span data-ttu-id="5e217-119">Amikor bővítményt vásárol egy előfizetéshez, az eredeti előfizetési rendelést a bővítmény rendelésével frissíti.</span><span class="sxs-lookup"><span data-stu-id="5e217-119">When you purchase an add-on to a subscription, you are updating the original subscription order with the order for the add-on.</span></span> <span data-ttu-id="5e217-120">A következőben a customerId az ügyfél azonosítója, a subscriptionId az előfizetés azonosítója, az addOnOfferId pedig a bővítmény ajánlatazonosítója.</span><span class="sxs-lookup"><span data-stu-id="5e217-120">In the following, customerId is the customer ID, subscriptionId is the subscription ID, and addOnOfferId is the offer ID for the add-on.</span></span>

<span data-ttu-id="5e217-121">A lépések a következők:</span><span class="sxs-lookup"><span data-stu-id="5e217-121">Here are the steps:</span></span>

1.  <span data-ttu-id="5e217-122">Felület lekérte az előfizetés műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="5e217-122">Get an interface to the operations for the subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  <span data-ttu-id="5e217-123">Ezzel a felülettel példányosithat egy előfizetési objektumot.</span><span class="sxs-lookup"><span data-stu-id="5e217-123">Use that interface to instantiate a subscription object.</span></span> <span data-ttu-id="5e217-124">Ez lekérte a szülő-előfizetés adatait, beleértve a rendelés azonosítóját is.</span><span class="sxs-lookup"><span data-stu-id="5e217-124">This gets you the parent subscription details, including the order ID.</span></span>

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  <span data-ttu-id="5e217-125">Új Order objektum [**példányosodása.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order)</span><span class="sxs-lookup"><span data-stu-id="5e217-125">Instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object.</span></span> <span data-ttu-id="5e217-126">Ezzel a rendelési példánysal frissítheti az előfizetés megvásárlásához használt eredeti rendelést.</span><span class="sxs-lookup"><span data-stu-id="5e217-126">This order instance is used to update the original order used to purchase the subscription.</span></span> <span data-ttu-id="5e217-127">Adjon hozzá egy egysoros elemet a bővítményt képviselő sorrendhez.</span><span class="sxs-lookup"><span data-stu-id="5e217-127">Add a single-line item to the order that represents the add-on.</span></span>
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

4.  <span data-ttu-id="5e217-128">Frissítse az előfizetés eredeti rendelését a bővítmény új rendelésével.</span><span class="sxs-lookup"><span data-stu-id="5e217-128">Update the original order for the subscription with the new order for the add-on.</span></span>
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a><span data-ttu-id="5e217-129">C\#</span><span class="sxs-lookup"><span data-stu-id="5e217-129">C\#</span></span>

<span data-ttu-id="5e217-130">Bővítmény vásárlásához először szerezzen be egy felületet az előfizetési műveletekhez. Ehhez hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához, és a [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust a bővítményajánlattal kapcsolatos előfizetés azonosításához.</span><span class="sxs-lookup"><span data-stu-id="5e217-130">To purchase an add-on, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription that has the add-on offer.</span></span> <span data-ttu-id="5e217-131">Ezen a [**felületen**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) lekérhetőek az előfizetés részletei a [**Get hívása segítségével.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get)</span><span class="sxs-lookup"><span data-stu-id="5e217-131">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span> <span data-ttu-id="5e217-132">Az előfizetés részletei tartalmazzák az előfizetési rendelés rendelésazonosítóját, amely a bővítménysel frissíthető rendelés.</span><span class="sxs-lookup"><span data-stu-id="5e217-132">The subscription details contain the order ID of the subscription order, which is the order to be updated with the add-on.</span></span>

<span data-ttu-id="5e217-133">Ezután példányosítsa az új [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) objektumot, és töltse fel egyetlen [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) példáncával, amely tartalmazza a bővítmény azonosításához szükséges információkat, ahogyan az alábbi kódrészletben látható.</span><span class="sxs-lookup"><span data-stu-id="5e217-133">Next, instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and populate it with a single [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) instance that contains the information to identify the add-on, as shown in the following code snippet.</span></span> <span data-ttu-id="5e217-134">Ezzel az új objektummal frissítheti az előfizetési rendelést a bővítmény használatával.</span><span class="sxs-lookup"><span data-stu-id="5e217-134">You'll use this new object to update the subscription order with the add-on.</span></span> <span data-ttu-id="5e217-135">Végül hívja meg a [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) metódust az előfizetési rendelés frissítéséhez, miután először azonosította az ügyfelet az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) azonosítóval, a rendelést pedig [**az Orders.ById azonosítóval.**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="5e217-135">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) method to update the subscription order, after first identifying the customer with [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) and the order with [**Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span></span>

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

<span data-ttu-id="5e217-136">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="5e217-136">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5e217-137">**Project**: Partnerközpont SDK **osztály:** AddSubscriptionAddOn.cs</span><span class="sxs-lookup"><span data-stu-id="5e217-137">**Project**: Partner Center SDK Samples **Class**: AddSubscriptionAddOn.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5e217-138">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="5e217-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5e217-139">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5e217-139">Request syntax</span></span>

| <span data-ttu-id="5e217-140">Metódus</span><span class="sxs-lookup"><span data-stu-id="5e217-140">Method</span></span>    | <span data-ttu-id="5e217-141">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5e217-141">Request URI</span></span>                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5e217-142">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="5e217-142">**PATCH**</span></span> | <span data-ttu-id="5e217-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{rendelésazonosító} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5e217-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="5e217-144">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="5e217-144">URI parameters</span></span>

<span data-ttu-id="5e217-145">A következő paraméterekkel azonosíthatja az ügyfelet és a megrendelést.</span><span class="sxs-lookup"><span data-stu-id="5e217-145">Use the following parameters to identify the customer and order.</span></span>

| <span data-ttu-id="5e217-146">Név</span><span class="sxs-lookup"><span data-stu-id="5e217-146">Name</span></span>                   | <span data-ttu-id="5e217-147">Típus</span><span class="sxs-lookup"><span data-stu-id="5e217-147">Type</span></span>     | <span data-ttu-id="5e217-148">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5e217-148">Required</span></span> | <span data-ttu-id="5e217-149">Leírás</span><span class="sxs-lookup"><span data-stu-id="5e217-149">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="5e217-150">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="5e217-150">**customer-tenant-id**</span></span> | <span data-ttu-id="5e217-151">**guid**</span><span class="sxs-lookup"><span data-stu-id="5e217-151">**guid**</span></span> | <span data-ttu-id="5e217-152">Y</span><span class="sxs-lookup"><span data-stu-id="5e217-152">Y</span></span>        | <span data-ttu-id="5e217-153">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="5e217-153">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="5e217-154">**rendelésazonosító**</span><span class="sxs-lookup"><span data-stu-id="5e217-154">**order-id**</span></span>           | <span data-ttu-id="5e217-155">**guid**</span><span class="sxs-lookup"><span data-stu-id="5e217-155">**guid**</span></span> | <span data-ttu-id="5e217-156">Y</span><span class="sxs-lookup"><span data-stu-id="5e217-156">Y</span></span>        | <span data-ttu-id="5e217-157">A rendelés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="5e217-157">The order identifier.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="5e217-158">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5e217-158">Request headers</span></span>

<span data-ttu-id="5e217-159">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5e217-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5e217-160">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="5e217-160">Request body</span></span>

<span data-ttu-id="5e217-161">Az alábbi táblázatok a kérelem törzsében lévő tulajdonságokat ismertetik.</span><span class="sxs-lookup"><span data-stu-id="5e217-161">The following tables describe the properties in the request body.</span></span>

## <a name="order"></a><span data-ttu-id="5e217-162">Sorrend</span><span class="sxs-lookup"><span data-stu-id="5e217-162">Order</span></span>

| <span data-ttu-id="5e217-163">Név</span><span class="sxs-lookup"><span data-stu-id="5e217-163">Name</span></span>                | <span data-ttu-id="5e217-164">Típus</span><span class="sxs-lookup"><span data-stu-id="5e217-164">Type</span></span>             | <span data-ttu-id="5e217-165">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5e217-165">Required</span></span> | <span data-ttu-id="5e217-166">Leírás</span><span class="sxs-lookup"><span data-stu-id="5e217-166">Description</span></span>                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| <span data-ttu-id="5e217-167">Id</span><span class="sxs-lookup"><span data-stu-id="5e217-167">Id</span></span>                  | <span data-ttu-id="5e217-168">sztring</span><span class="sxs-lookup"><span data-stu-id="5e217-168">string</span></span>           | <span data-ttu-id="5e217-169">N</span><span class="sxs-lookup"><span data-stu-id="5e217-169">N</span></span>        | <span data-ttu-id="5e217-170">A rendelés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="5e217-170">The order ID.</span></span>                                        |
| <span data-ttu-id="5e217-171">ReferenceCustomerId (ReferenciacustomerId)</span><span class="sxs-lookup"><span data-stu-id="5e217-171">ReferenceCustomerId</span></span> | <span data-ttu-id="5e217-172">sztring</span><span class="sxs-lookup"><span data-stu-id="5e217-172">string</span></span>           | <span data-ttu-id="5e217-173">Y</span><span class="sxs-lookup"><span data-stu-id="5e217-173">Y</span></span>        | <span data-ttu-id="5e217-174">Az ügyfél azonosítója.</span><span class="sxs-lookup"><span data-stu-id="5e217-174">The customer ID.</span></span>                                     |
| <span data-ttu-id="5e217-175">Sorsorok</span><span class="sxs-lookup"><span data-stu-id="5e217-175">LineItems</span></span>           | <span data-ttu-id="5e217-176">objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="5e217-176">array of objects</span></span> | <span data-ttu-id="5e217-177">Y</span><span class="sxs-lookup"><span data-stu-id="5e217-177">Y</span></span>        | <span data-ttu-id="5e217-178">[OrderLineItem objektumok tömbje.](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="5e217-178">An array of [OrderLineItem](#orderlineitem) objects.</span></span> |
| <span data-ttu-id="5e217-179">CreationDate (Létrehozás dátuma)</span><span class="sxs-lookup"><span data-stu-id="5e217-179">CreationDate</span></span>        | <span data-ttu-id="5e217-180">sztring</span><span class="sxs-lookup"><span data-stu-id="5e217-180">string</span></span>           | <span data-ttu-id="5e217-181">N</span><span class="sxs-lookup"><span data-stu-id="5e217-181">N</span></span>        | <span data-ttu-id="5e217-182">A rendelés létrehozási dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="5e217-182">The date the order was created, in date-time format.</span></span> |
| <span data-ttu-id="5e217-183">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="5e217-183">Attributes</span></span>          | <span data-ttu-id="5e217-184">object</span><span class="sxs-lookup"><span data-stu-id="5e217-184">object</span></span>           | <span data-ttu-id="5e217-185">N</span><span class="sxs-lookup"><span data-stu-id="5e217-185">N</span></span>        | <span data-ttu-id="5e217-186">Tartalmazza az "ObjectType": "Order" típust.</span><span class="sxs-lookup"><span data-stu-id="5e217-186">Contains "ObjectType": "Order".</span></span>                      |

## <a name="orderlineitem"></a><span data-ttu-id="5e217-187">OrderLineItem (Megrendelési vonal)</span><span class="sxs-lookup"><span data-stu-id="5e217-187">OrderLineItem</span></span>

| <span data-ttu-id="5e217-188">Név</span><span class="sxs-lookup"><span data-stu-id="5e217-188">Name</span></span>                 | <span data-ttu-id="5e217-189">Típus</span><span class="sxs-lookup"><span data-stu-id="5e217-189">Type</span></span>   | <span data-ttu-id="5e217-190">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5e217-190">Required</span></span> | <span data-ttu-id="5e217-191">Leírás</span><span class="sxs-lookup"><span data-stu-id="5e217-191">Description</span></span>                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="5e217-192">LineItemNumber (Sor száma)</span><span class="sxs-lookup"><span data-stu-id="5e217-192">LineItemNumber</span></span>       | <span data-ttu-id="5e217-193">szám</span><span class="sxs-lookup"><span data-stu-id="5e217-193">number</span></span> | <span data-ttu-id="5e217-194">Y</span><span class="sxs-lookup"><span data-stu-id="5e217-194">Y</span></span>        | <span data-ttu-id="5e217-195">A sorelem száma, 0-val kezdve.</span><span class="sxs-lookup"><span data-stu-id="5e217-195">The line item number, starting with 0.</span></span>                       |
| <span data-ttu-id="5e217-196">OfferId (Ajánlatazonosító)</span><span class="sxs-lookup"><span data-stu-id="5e217-196">OfferId</span></span>              | <span data-ttu-id="5e217-197">sztring</span><span class="sxs-lookup"><span data-stu-id="5e217-197">string</span></span> | <span data-ttu-id="5e217-198">Y</span><span class="sxs-lookup"><span data-stu-id="5e217-198">Y</span></span>        | <span data-ttu-id="5e217-199">A bővítmény ajánlatazonosítója.</span><span class="sxs-lookup"><span data-stu-id="5e217-199">The offer ID of the add-on.</span></span>                                  |
| <span data-ttu-id="5e217-200">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="5e217-200">SubscriptionId</span></span>       | <span data-ttu-id="5e217-201">sztring</span><span class="sxs-lookup"><span data-stu-id="5e217-201">string</span></span> | <span data-ttu-id="5e217-202">N</span><span class="sxs-lookup"><span data-stu-id="5e217-202">N</span></span>        | <span data-ttu-id="5e217-203">A megvásárolt bővítmény-előfizetés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="5e217-203">The ID of the add-on subscription purchased.</span></span>                 |
| <span data-ttu-id="5e217-204">ParentSubscriptionId (Szülő-előíróazonosító)</span><span class="sxs-lookup"><span data-stu-id="5e217-204">ParentSubscriptionId</span></span> | <span data-ttu-id="5e217-205">sztring</span><span class="sxs-lookup"><span data-stu-id="5e217-205">string</span></span> | <span data-ttu-id="5e217-206">Y</span><span class="sxs-lookup"><span data-stu-id="5e217-206">Y</span></span>        | <span data-ttu-id="5e217-207">Annak a szülő előfizetésnek az azonosítója, amely a bővítményajánlattal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="5e217-207">The ID of the parent subscription that has the add-on offer.</span></span> |
| <span data-ttu-id="5e217-208">FriendlyName (Rövid név)</span><span class="sxs-lookup"><span data-stu-id="5e217-208">FriendlyName</span></span>         | <span data-ttu-id="5e217-209">sztring</span><span class="sxs-lookup"><span data-stu-id="5e217-209">string</span></span> | <span data-ttu-id="5e217-210">N</span><span class="sxs-lookup"><span data-stu-id="5e217-210">N</span></span>        | <span data-ttu-id="5e217-211">A sorelem rövid neve.</span><span class="sxs-lookup"><span data-stu-id="5e217-211">The friendly name for this line item.</span></span>                        |
| <span data-ttu-id="5e217-212">Mennyiség</span><span class="sxs-lookup"><span data-stu-id="5e217-212">Quantity</span></span>             | <span data-ttu-id="5e217-213">szám</span><span class="sxs-lookup"><span data-stu-id="5e217-213">number</span></span> | <span data-ttu-id="5e217-214">Y</span><span class="sxs-lookup"><span data-stu-id="5e217-214">Y</span></span>        | <span data-ttu-id="5e217-215">A licencek száma.</span><span class="sxs-lookup"><span data-stu-id="5e217-215">The number of licenses.</span></span>                                      |
| <span data-ttu-id="5e217-216">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="5e217-216">PartnerIdOnRecord</span></span>    | <span data-ttu-id="5e217-217">sztring</span><span class="sxs-lookup"><span data-stu-id="5e217-217">string</span></span> | <span data-ttu-id="5e217-218">N</span><span class="sxs-lookup"><span data-stu-id="5e217-218">N</span></span>        | <span data-ttu-id="5e217-219">A rekordpartner MPN-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="5e217-219">The MPN ID of the partner of record.</span></span>                         |
| <span data-ttu-id="5e217-220">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="5e217-220">Attributes</span></span>           | <span data-ttu-id="5e217-221">object</span><span class="sxs-lookup"><span data-stu-id="5e217-221">object</span></span> | <span data-ttu-id="5e217-222">N</span><span class="sxs-lookup"><span data-stu-id="5e217-222">N</span></span>        | <span data-ttu-id="5e217-223">Tartalmazza az "ObjectType": "OrderLineItem" adatokat.</span><span class="sxs-lookup"><span data-stu-id="5e217-223">Contains "ObjectType": "OrderLineItem".</span></span>                      |

### <a name="request-example"></a><span data-ttu-id="5e217-224">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5e217-224">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="5e217-225">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5e217-225">REST response</span></span>

<span data-ttu-id="5e217-226">Ha a művelet sikeres, ez a metódus a válasz törzsében adja vissza a frissített előfizetési sorrendet.</span><span class="sxs-lookup"><span data-stu-id="5e217-226">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5e217-227">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5e217-227">Response success and error codes</span></span>

<span data-ttu-id="5e217-228">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="5e217-228">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5e217-229">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="5e217-229">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5e217-230">A teljes listát lásd: Partnerközpont [hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="5e217-230">For the full list, see [Partner Center Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5e217-231">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5e217-231">Response example</span></span>

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
