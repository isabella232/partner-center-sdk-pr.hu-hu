---
title: A számlázási ciklus módosítása
description: Megtudhatja, hogyan frissítheti az ügyfél-előfizetést havi vagy éves számlázásra a partner Center API-k használatával. Ezt a partner Center irányítópultján is elvégezheti.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 8a2879db061ced799e29d84e71be5b1259b07689
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768600"
---
# <a name="change-a-customer-subscription-billing-cycle"></a><span data-ttu-id="17725-104">Ügyfél-előfizetés számlázási ciklusának módosítása</span><span class="sxs-lookup"><span data-stu-id="17725-104">Change a customer subscription billing cycle</span></span>

<span data-ttu-id="17725-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="17725-105">**Applies to:**</span></span>

- <span data-ttu-id="17725-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="17725-106">Partner Center</span></span>
- <span data-ttu-id="17725-107">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="17725-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="17725-108">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="17725-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="17725-109">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="17725-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="17725-110">Havonta és évenkénti számlázással, vagy éves és havi számlázással frissíti a [rendelést](order-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="17725-110">Updates an [Order](order-resources.md) from monthly to annual billing or from annual to monthly billing.</span></span>

<span data-ttu-id="17725-111">A partneri központ irányítópultján ez a művelet az ügyfél előfizetésének részleteit tartalmazó oldalra navigálva végezhető el.</span><span class="sxs-lookup"><span data-stu-id="17725-111">In the Partner Center dashboard, this operation can be performed by navigating to a customer's subscription details page.</span></span> <span data-ttu-id="17725-112">Ekkor megjelenik egy lehetőség, amely meghatározza az előfizetés aktuális számlázási ciklusát, amely lehetővé teszi a módosítást és a beküldést.</span><span class="sxs-lookup"><span data-stu-id="17725-112">Once there, you will see an option defining the current billing cycle for the subscription with the ability to change and submit it.</span></span>

<span data-ttu-id="17725-113">A cikk **Hatókörön kívüli** :</span><span class="sxs-lookup"><span data-stu-id="17725-113">**Out of scope** for this article:</span></span>

- <span data-ttu-id="17725-114">A számlázási ciklus módosítása a próbaverziók esetében</span><span class="sxs-lookup"><span data-stu-id="17725-114">Changing the billing cycle for trials</span></span>
- <span data-ttu-id="17725-115">A számlázási ciklusok bármely nem éves időszakra vonatkozó ajánlatának módosítása (havi, 6 éves) & Azure-előfizetések</span><span class="sxs-lookup"><span data-stu-id="17725-115">Changing the billing cycles for any non-annual term offers (monthly, 6-year) & Azure subscriptions</span></span>
- <span data-ttu-id="17725-116">Az inaktív előfizetések számlázási ciklusának módosítása</span><span class="sxs-lookup"><span data-stu-id="17725-116">Changing the billing cycles for inactive subscriptions</span></span>
- <span data-ttu-id="17725-117">Számlázási ciklusok módosítása a Microsoft online szolgáltatások licenc-alapú előfizetésekhez</span><span class="sxs-lookup"><span data-stu-id="17725-117">Changing billing cycles for Microsoft online services license-based subscriptions</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17725-118">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="17725-118">Prerequisites</span></span>

- <span data-ttu-id="17725-119">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="17725-119">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="17725-120">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="17725-120">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="17725-121">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="17725-121">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="17725-122">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="17725-122">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="17725-123">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="17725-123">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="17725-124">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="17725-124">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="17725-125">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="17725-125">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="17725-126">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="17725-126">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="17725-127">Egy megrendelés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="17725-127">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="17725-128">C\#</span><span class="sxs-lookup"><span data-stu-id="17725-128">C\#</span></span>

<span data-ttu-id="17725-129">A számlázási ciklus gyakoriságának módosításához frissítse a [**Order. BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="17725-129">To change the frequency of the billing cycle, update the [**Order.BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) property.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a><span data-ttu-id="17725-130">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="17725-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="17725-131">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="17725-131">Request syntax</span></span>

| <span data-ttu-id="17725-132">Metódus</span><span class="sxs-lookup"><span data-stu-id="17725-132">Method</span></span>    | <span data-ttu-id="17725-133">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="17725-133">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="17725-134">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="17725-134">**PATCH**</span></span> | <span data-ttu-id="17725-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="17725-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="17725-136">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="17725-136">URI parameter</span></span>

<span data-ttu-id="17725-137">Ez a táblázat felsorolja a szükséges lekérdezési paramétert az előfizetés mennyiségének módosításához.</span><span class="sxs-lookup"><span data-stu-id="17725-137">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="17725-138">Név</span><span class="sxs-lookup"><span data-stu-id="17725-138">Name</span></span>                   | <span data-ttu-id="17725-139">Típus</span><span class="sxs-lookup"><span data-stu-id="17725-139">Type</span></span> | <span data-ttu-id="17725-140">Kötelező</span><span class="sxs-lookup"><span data-stu-id="17725-140">Required</span></span> | <span data-ttu-id="17725-141">Leírás</span><span class="sxs-lookup"><span data-stu-id="17725-141">Description</span></span>                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| <span data-ttu-id="17725-142">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="17725-142">**customer-tenant-id**</span></span> | <span data-ttu-id="17725-143">GUID</span><span class="sxs-lookup"><span data-stu-id="17725-143">GUID</span></span> |    <span data-ttu-id="17725-144">Y</span><span class="sxs-lookup"><span data-stu-id="17725-144">Y</span></span>     | <span data-ttu-id="17725-145">Az ügyfelet azonosító, formázott **ügyfél-bérlői azonosító**</span><span class="sxs-lookup"><span data-stu-id="17725-145">A GUID formatted **customer-tenant-id** that identifies the customer</span></span> |
| <span data-ttu-id="17725-146">**megrendelés azonosítója**</span><span class="sxs-lookup"><span data-stu-id="17725-146">**order-id**</span></span>           | <span data-ttu-id="17725-147">GUID</span><span class="sxs-lookup"><span data-stu-id="17725-147">GUID</span></span> |    <span data-ttu-id="17725-148">Y</span><span class="sxs-lookup"><span data-stu-id="17725-148">Y</span></span>     | <span data-ttu-id="17725-149">A megrendelés azonosítója</span><span class="sxs-lookup"><span data-stu-id="17725-149">The order identifier</span></span>                                                 |

### <a name="request-headers"></a><span data-ttu-id="17725-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="17725-150">Request headers</span></span>

<span data-ttu-id="17725-151">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="17725-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="17725-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="17725-152">Request body</span></span>

<span data-ttu-id="17725-153">A következő táblázatok a kérés törzsének tulajdonságait ismertetik.</span><span class="sxs-lookup"><span data-stu-id="17725-153">The following tables describe the properties in the request body.</span></span>

### <a name="order"></a><span data-ttu-id="17725-154">Sorrend</span><span class="sxs-lookup"><span data-stu-id="17725-154">Order</span></span>

| <span data-ttu-id="17725-155">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="17725-155">Property</span></span>           | <span data-ttu-id="17725-156">Típus</span><span class="sxs-lookup"><span data-stu-id="17725-156">Type</span></span>             | <span data-ttu-id="17725-157">Kötelező</span><span class="sxs-lookup"><span data-stu-id="17725-157">Required</span></span> | <span data-ttu-id="17725-158">Leírás</span><span class="sxs-lookup"><span data-stu-id="17725-158">Description</span></span>                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| <span data-ttu-id="17725-159">Id</span><span class="sxs-lookup"><span data-stu-id="17725-159">Id</span></span>                 | <span data-ttu-id="17725-160">sztring</span><span class="sxs-lookup"><span data-stu-id="17725-160">string</span></span>           |    <span data-ttu-id="17725-161">N</span><span class="sxs-lookup"><span data-stu-id="17725-161">N</span></span>     | <span data-ttu-id="17725-162">A megrendelés sikeres létrehozásakor megadott rendelési azonosító</span><span class="sxs-lookup"><span data-stu-id="17725-162">An order identifier that is supplied upon successful creation of the order</span></span> |
|<span data-ttu-id="17725-163">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="17725-163">ReferenceCustomerId</span></span> | <span data-ttu-id="17725-164">sztring</span><span class="sxs-lookup"><span data-stu-id="17725-164">string</span></span>           |    <span data-ttu-id="17725-165">Y</span><span class="sxs-lookup"><span data-stu-id="17725-165">Y</span></span>     | <span data-ttu-id="17725-166">Az ügyfél azonosítója</span><span class="sxs-lookup"><span data-stu-id="17725-166">The customer identifier</span></span>                                                    |
| <span data-ttu-id="17725-167">BillingCycle</span><span class="sxs-lookup"><span data-stu-id="17725-167">BillingCycle</span></span>       | <span data-ttu-id="17725-168">sztring</span><span class="sxs-lookup"><span data-stu-id="17725-168">string</span></span>           |    <span data-ttu-id="17725-169">Y</span><span class="sxs-lookup"><span data-stu-id="17725-169">Y</span></span>     | <span data-ttu-id="17725-170">Azt jelzi, hogy milyen gyakorisággal történik a partner számlázása ebben a sorrendben.</span><span class="sxs-lookup"><span data-stu-id="17725-170">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="17725-171">A támogatott értékek a [BillingCycleType](product-resources.md#billingcycletype)található tagok nevei.</span><span class="sxs-lookup"><span data-stu-id="17725-171">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> |
| <span data-ttu-id="17725-172">Listaelemek</span><span class="sxs-lookup"><span data-stu-id="17725-172">LineItems</span></span>          | <span data-ttu-id="17725-173">objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="17725-173">array of objects</span></span> |    <span data-ttu-id="17725-174">Y</span><span class="sxs-lookup"><span data-stu-id="17725-174">Y</span></span>     | <span data-ttu-id="17725-175">[OrderLineItem](#orderlineitem) -erőforrások tömbje</span><span class="sxs-lookup"><span data-stu-id="17725-175">An array of [OrderLineItem](#orderlineitem) resources</span></span>                      |
| <span data-ttu-id="17725-176">CreationDate</span><span class="sxs-lookup"><span data-stu-id="17725-176">CreationDate</span></span>       | <span data-ttu-id="17725-177">dátum/idő</span><span class="sxs-lookup"><span data-stu-id="17725-177">datetime</span></span>         |    <span data-ttu-id="17725-178">N</span><span class="sxs-lookup"><span data-stu-id="17725-178">N</span></span>     | <span data-ttu-id="17725-179">A rendelés létrehozásának dátuma dátum-idő formátumban</span><span class="sxs-lookup"><span data-stu-id="17725-179">The date the order was created, in date-time format</span></span>                        |
| <span data-ttu-id="17725-180">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="17725-180">Attributes</span></span>         | <span data-ttu-id="17725-181">Objektum</span><span class="sxs-lookup"><span data-stu-id="17725-181">Object</span></span>           |    <span data-ttu-id="17725-182">N</span><span class="sxs-lookup"><span data-stu-id="17725-182">N</span></span>     | <span data-ttu-id="17725-183">A "objektumtípus": "OrderLineItem" kifejezést tartalmazza</span><span class="sxs-lookup"><span data-stu-id="17725-183">Contains "ObjectType": "OrderLineItem"</span></span>                                     |

### <a name="orderlineitem"></a><span data-ttu-id="17725-184">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="17725-184">OrderLineItem</span></span>

| <span data-ttu-id="17725-185">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="17725-185">Property</span></span>             | <span data-ttu-id="17725-186">Típus</span><span class="sxs-lookup"><span data-stu-id="17725-186">Type</span></span>   | <span data-ttu-id="17725-187">Kötelező</span><span class="sxs-lookup"><span data-stu-id="17725-187">Required</span></span> | <span data-ttu-id="17725-188">Leírás</span><span class="sxs-lookup"><span data-stu-id="17725-188">Description</span></span>                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="17725-189">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="17725-189">LineItemNumber</span></span>       | <span data-ttu-id="17725-190">szám</span><span class="sxs-lookup"><span data-stu-id="17725-190">number</span></span> |    <span data-ttu-id="17725-191">Y</span><span class="sxs-lookup"><span data-stu-id="17725-191">Y</span></span>     | <span data-ttu-id="17725-192">A sor sorszáma, kezdő és 0</span><span class="sxs-lookup"><span data-stu-id="17725-192">The line item number, starting with 0</span></span>                                              |
| <span data-ttu-id="17725-193">OfferId</span><span class="sxs-lookup"><span data-stu-id="17725-193">OfferId</span></span>              | <span data-ttu-id="17725-194">sztring</span><span class="sxs-lookup"><span data-stu-id="17725-194">string</span></span> |    <span data-ttu-id="17725-195">Y</span><span class="sxs-lookup"><span data-stu-id="17725-195">Y</span></span>     | <span data-ttu-id="17725-196">Az ajánlat azonosítója</span><span class="sxs-lookup"><span data-stu-id="17725-196">The ID of the offer</span></span>                                                                |
| <span data-ttu-id="17725-197">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="17725-197">SubscriptionId</span></span>       | <span data-ttu-id="17725-198">sztring</span><span class="sxs-lookup"><span data-stu-id="17725-198">string</span></span> |    <span data-ttu-id="17725-199">Y</span><span class="sxs-lookup"><span data-stu-id="17725-199">Y</span></span>     | <span data-ttu-id="17725-200">Az előfizetés azonosítója</span><span class="sxs-lookup"><span data-stu-id="17725-200">The ID of the subscription</span></span>                                                         |
| <span data-ttu-id="17725-201">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="17725-201">FriendlyName</span></span>         | <span data-ttu-id="17725-202">sztring</span><span class="sxs-lookup"><span data-stu-id="17725-202">string</span></span> |    <span data-ttu-id="17725-203">N</span><span class="sxs-lookup"><span data-stu-id="17725-203">N</span></span>     | <span data-ttu-id="17725-204">A partner által az előfizetéshez megadott rövid név, amely segít a egyértelműsítse</span><span class="sxs-lookup"><span data-stu-id="17725-204">The friendly name for the subscription defined by the partner to help disambiguate</span></span> |
| <span data-ttu-id="17725-205">Mennyiség</span><span class="sxs-lookup"><span data-stu-id="17725-205">Quantity</span></span>             | <span data-ttu-id="17725-206">szám</span><span class="sxs-lookup"><span data-stu-id="17725-206">number</span></span> |    <span data-ttu-id="17725-207">Y</span><span class="sxs-lookup"><span data-stu-id="17725-207">Y</span></span>     | <span data-ttu-id="17725-208">A licencek vagy példányok száma</span><span class="sxs-lookup"><span data-stu-id="17725-208">The number of licenses or instances</span></span>                                                |
| <span data-ttu-id="17725-209">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="17725-209">PartnerIdOnRecord</span></span>    | <span data-ttu-id="17725-210">sztring</span><span class="sxs-lookup"><span data-stu-id="17725-210">string</span></span> |    <span data-ttu-id="17725-211">N</span><span class="sxs-lookup"><span data-stu-id="17725-211">N</span></span>     | <span data-ttu-id="17725-212">A rekord partnerének MPN-azonosítója</span><span class="sxs-lookup"><span data-stu-id="17725-212">The MPN ID of the partner of record</span></span>                                                |
| <span data-ttu-id="17725-213">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="17725-213">Attributes</span></span>           | <span data-ttu-id="17725-214">Objektum</span><span class="sxs-lookup"><span data-stu-id="17725-214">Object</span></span> |    <span data-ttu-id="17725-215">N</span><span class="sxs-lookup"><span data-stu-id="17725-215">N</span></span>     | <span data-ttu-id="17725-216">A "objektumtípus": "OrderLineItem" kifejezést tartalmazza</span><span class="sxs-lookup"><span data-stu-id="17725-216">Contains "ObjectType": "OrderLineItem"</span></span>                                             |

### <a name="request-example"></a><span data-ttu-id="17725-217">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="17725-217">Request example</span></span>

<span data-ttu-id="17725-218">Frissítés az éves számlázásra</span><span class="sxs-lookup"><span data-stu-id="17725-218">Update to annual billing</span></span>

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
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
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

## <a name="rest-response"></a><span data-ttu-id="17725-219">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="17725-219">REST response</span></span>

<span data-ttu-id="17725-220">Ha ez sikeres, a metódus visszaadja a frissített előfizetés sorrendjét a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="17725-220">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="17725-221">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="17725-221">Response success and error codes</span></span>

<span data-ttu-id="17725-222">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="17725-222">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="17725-223">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="17725-223">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="17725-224">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="17725-224">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="17725-225">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="17725-225">Response example</span></span>

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
    "billingCycle": "Annual",
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
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
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