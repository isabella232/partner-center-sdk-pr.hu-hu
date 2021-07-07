---
title: A számlázási ciklus módosítása
description: Megtudhatja, hogyan frissítheti az ügyfél-előfizetést havi vagy éves számlázásra az Partnerközpont API-k használatával. Ezt az irányítópulton Partnerközpont is.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 435309229e2cb038c936028943f4c2cf27b032a7
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974114"
---
# <a name="change-a-customer-subscription-billing-cycle"></a><span data-ttu-id="fe40c-104">Ügyfél-előfizetés számlázási ciklusának módosítása</span><span class="sxs-lookup"><span data-stu-id="fe40c-104">Change a customer subscription billing cycle</span></span>

<span data-ttu-id="fe40c-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fe40c-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fe40c-106">Frissíti a [rendelést](order-resources.md) haviról éves vagy évesről havi számlázásra.</span><span class="sxs-lookup"><span data-stu-id="fe40c-106">Updates an [Order](order-resources.md) from monthly to annual billing or from annual to monthly billing.</span></span>

<span data-ttu-id="fe40c-107">Az Partnerközpont irányítópulton ezt a műveletet úgy hajthatja végre, hogy megnyitja az ügyfél előfizetési adatait tartalmazó oldalt.</span><span class="sxs-lookup"><span data-stu-id="fe40c-107">In the Partner Center dashboard, this operation can be performed by navigating to a customer's subscription details page.</span></span> <span data-ttu-id="fe40c-108">Itt egy lehetőséget fog látni, amely meghatározza az előfizetés aktuális számlázási ciklusát, és lehetővé teszi a módosítását és elküldét.</span><span class="sxs-lookup"><span data-stu-id="fe40c-108">Once there, you will see an option defining the current billing cycle for the subscription with the ability to change and submit it.</span></span>

<span data-ttu-id="fe40c-109">**A cikk nem terjed** ki a cikkre:</span><span class="sxs-lookup"><span data-stu-id="fe40c-109">**Out of scope** for this article:</span></span>

- <span data-ttu-id="fe40c-110">Próbaverziók számlázási ciklusának módosítása</span><span class="sxs-lookup"><span data-stu-id="fe40c-110">Changing the billing cycle for trials</span></span>
- <span data-ttu-id="fe40c-111">Az Azure-előfizetések nem éves (havi, hat éves) időszakra vonatkozó számlázási ciklusainak & módosítása</span><span class="sxs-lookup"><span data-stu-id="fe40c-111">Changing the billing cycles for any non-annual term offers (monthly, six-year) & Azure subscriptions</span></span>
- <span data-ttu-id="fe40c-112">Inaktív előfizetések számlázási ciklusainak módosítása</span><span class="sxs-lookup"><span data-stu-id="fe40c-112">Changing the billing cycles for inactive subscriptions</span></span>
- <span data-ttu-id="fe40c-113">A Microsoft licencalapú előfizetések online szolgáltatások számlázási ciklusainak módosítása</span><span class="sxs-lookup"><span data-stu-id="fe40c-113">Changing billing cycles for Microsoft online services license-based subscriptions</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe40c-114">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="fe40c-114">Prerequisites</span></span>

- <span data-ttu-id="fe40c-115">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fe40c-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fe40c-116">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="fe40c-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fe40c-117">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fe40c-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fe40c-118">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="fe40c-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fe40c-119">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="fe40c-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fe40c-120">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="fe40c-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fe40c-121">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="fe40c-121">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fe40c-122">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fe40c-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fe40c-123">Egy rendelésazonosító.</span><span class="sxs-lookup"><span data-stu-id="fe40c-123">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="fe40c-124">C\#</span><span class="sxs-lookup"><span data-stu-id="fe40c-124">C\#</span></span>

<span data-ttu-id="fe40c-125">A számlázási ciklus gyakoriságának változásához frissítse az [**Order.BillingCycle tulajdonságot.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle)</span><span class="sxs-lookup"><span data-stu-id="fe40c-125">To change the frequency of the billing cycle, update the [**Order.BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) property.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="fe40c-126">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="fe40c-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fe40c-127">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="fe40c-127">Request syntax</span></span>

| <span data-ttu-id="fe40c-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="fe40c-128">Method</span></span>    | <span data-ttu-id="fe40c-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="fe40c-129">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fe40c-130">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="fe40c-130">**PATCH**</span></span> | <span data-ttu-id="fe40c-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{rendelésazonosító} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fe40c-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fe40c-132">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="fe40c-132">URI parameter</span></span>

<span data-ttu-id="fe40c-133">Ez a táblázat felsorolja az előfizetés mennyiségének változásához szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="fe40c-133">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="fe40c-134">Név</span><span class="sxs-lookup"><span data-stu-id="fe40c-134">Name</span></span>                   | <span data-ttu-id="fe40c-135">Típus</span><span class="sxs-lookup"><span data-stu-id="fe40c-135">Type</span></span> | <span data-ttu-id="fe40c-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="fe40c-136">Required</span></span> | <span data-ttu-id="fe40c-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="fe40c-137">Description</span></span>                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| <span data-ttu-id="fe40c-138">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="fe40c-138">**customer-tenant-id**</span></span> | <span data-ttu-id="fe40c-139">GUID</span><span class="sxs-lookup"><span data-stu-id="fe40c-139">GUID</span></span> |    <span data-ttu-id="fe40c-140">Y</span><span class="sxs-lookup"><span data-stu-id="fe40c-140">Y</span></span>     | <span data-ttu-id="fe40c-141">Egy GUID formátumú **ügyfél-bérlőazonosító,** amely azonosítja az ügyfelet</span><span class="sxs-lookup"><span data-stu-id="fe40c-141">A GUID formatted **customer-tenant-id** that identifies the customer</span></span> |
| <span data-ttu-id="fe40c-142">**order-id (rendelésazonosító)**</span><span class="sxs-lookup"><span data-stu-id="fe40c-142">**order-id**</span></span>           | <span data-ttu-id="fe40c-143">GUID</span><span class="sxs-lookup"><span data-stu-id="fe40c-143">GUID</span></span> |    <span data-ttu-id="fe40c-144">Y</span><span class="sxs-lookup"><span data-stu-id="fe40c-144">Y</span></span>     | <span data-ttu-id="fe40c-145">A rendelés azonosítója</span><span class="sxs-lookup"><span data-stu-id="fe40c-145">The order identifier</span></span>                                                 |

### <a name="request-headers"></a><span data-ttu-id="fe40c-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="fe40c-146">Request headers</span></span>

<span data-ttu-id="fe40c-147">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fe40c-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fe40c-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="fe40c-148">Request body</span></span>

<span data-ttu-id="fe40c-149">Az alábbi táblázatok a kérés törzsében lévő tulajdonságokat ismertetik.</span><span class="sxs-lookup"><span data-stu-id="fe40c-149">The following tables describe the properties in the request body.</span></span>

### <a name="order"></a><span data-ttu-id="fe40c-150">Sorrend</span><span class="sxs-lookup"><span data-stu-id="fe40c-150">Order</span></span>

| <span data-ttu-id="fe40c-151">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="fe40c-151">Property</span></span>           | <span data-ttu-id="fe40c-152">Típus</span><span class="sxs-lookup"><span data-stu-id="fe40c-152">Type</span></span>             | <span data-ttu-id="fe40c-153">Kötelező</span><span class="sxs-lookup"><span data-stu-id="fe40c-153">Required</span></span> | <span data-ttu-id="fe40c-154">Leírás</span><span class="sxs-lookup"><span data-stu-id="fe40c-154">Description</span></span>                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| <span data-ttu-id="fe40c-155">Id</span><span class="sxs-lookup"><span data-stu-id="fe40c-155">Id</span></span>                 | <span data-ttu-id="fe40c-156">sztring</span><span class="sxs-lookup"><span data-stu-id="fe40c-156">string</span></span>           |    <span data-ttu-id="fe40c-157">N</span><span class="sxs-lookup"><span data-stu-id="fe40c-157">N</span></span>     | <span data-ttu-id="fe40c-158">A rendelés sikeres létrehozása után megadott rendelésazonosító</span><span class="sxs-lookup"><span data-stu-id="fe40c-158">An order identifier that is supplied upon successful creation of the order</span></span> |
|<span data-ttu-id="fe40c-159">ReferenceCustomerId (ReferenciacustomerId)</span><span class="sxs-lookup"><span data-stu-id="fe40c-159">ReferenceCustomerId</span></span> | <span data-ttu-id="fe40c-160">sztring</span><span class="sxs-lookup"><span data-stu-id="fe40c-160">string</span></span>           |    <span data-ttu-id="fe40c-161">Y</span><span class="sxs-lookup"><span data-stu-id="fe40c-161">Y</span></span>     | <span data-ttu-id="fe40c-162">Az ügyfél azonosítója</span><span class="sxs-lookup"><span data-stu-id="fe40c-162">The customer identifier</span></span>                                                    |
| <span data-ttu-id="fe40c-163">BillingCycle</span><span class="sxs-lookup"><span data-stu-id="fe40c-163">BillingCycle</span></span>       | <span data-ttu-id="fe40c-164">sztring</span><span class="sxs-lookup"><span data-stu-id="fe40c-164">string</span></span>           |    <span data-ttu-id="fe40c-165">Y</span><span class="sxs-lookup"><span data-stu-id="fe40c-165">Y</span></span>     | <span data-ttu-id="fe40c-166">Azt jelzi, hogy milyen gyakorisággal számlázták a partnert a rendelésért.</span><span class="sxs-lookup"><span data-stu-id="fe40c-166">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="fe40c-167">A támogatott értékek a [BillingCycleType](product-resources.md#billingcycletype)típusban található tagnevek.</span><span class="sxs-lookup"><span data-stu-id="fe40c-167">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> |
| <span data-ttu-id="fe40c-168">Sorsorok</span><span class="sxs-lookup"><span data-stu-id="fe40c-168">LineItems</span></span>          | <span data-ttu-id="fe40c-169">objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="fe40c-169">array of objects</span></span> |    <span data-ttu-id="fe40c-170">Y</span><span class="sxs-lookup"><span data-stu-id="fe40c-170">Y</span></span>     | <span data-ttu-id="fe40c-171">[OrderLineItem-erőforrások tömbje](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="fe40c-171">An array of [OrderLineItem](#orderlineitem) resources</span></span>                      |
| <span data-ttu-id="fe40c-172">CreationDate (Létrehozás dátuma)</span><span class="sxs-lookup"><span data-stu-id="fe40c-172">CreationDate</span></span>       | <span data-ttu-id="fe40c-173">dátum/idő</span><span class="sxs-lookup"><span data-stu-id="fe40c-173">datetime</span></span>         |    <span data-ttu-id="fe40c-174">N</span><span class="sxs-lookup"><span data-stu-id="fe40c-174">N</span></span>     | <span data-ttu-id="fe40c-175">A rendelés létrehozási dátuma, dátum és idő formátumban</span><span class="sxs-lookup"><span data-stu-id="fe40c-175">The date the order was created, in date-time format</span></span>                        |
| <span data-ttu-id="fe40c-176">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="fe40c-176">Attributes</span></span>         | <span data-ttu-id="fe40c-177">Objektum</span><span class="sxs-lookup"><span data-stu-id="fe40c-177">Object</span></span>           |    <span data-ttu-id="fe40c-178">N</span><span class="sxs-lookup"><span data-stu-id="fe40c-178">N</span></span>     | <span data-ttu-id="fe40c-179">Tartalmazza az "ObjectType": "OrderLineItem" adatokat</span><span class="sxs-lookup"><span data-stu-id="fe40c-179">Contains "ObjectType": "OrderLineItem"</span></span>                                     |

### <a name="orderlineitem"></a><span data-ttu-id="fe40c-180">OrderLineItem (Megrendelési vonal)</span><span class="sxs-lookup"><span data-stu-id="fe40c-180">OrderLineItem</span></span>

| <span data-ttu-id="fe40c-181">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="fe40c-181">Property</span></span>             | <span data-ttu-id="fe40c-182">Típus</span><span class="sxs-lookup"><span data-stu-id="fe40c-182">Type</span></span>   | <span data-ttu-id="fe40c-183">Kötelező</span><span class="sxs-lookup"><span data-stu-id="fe40c-183">Required</span></span> | <span data-ttu-id="fe40c-184">Leírás</span><span class="sxs-lookup"><span data-stu-id="fe40c-184">Description</span></span>                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="fe40c-185">LineItemNumber (Sortem száma)</span><span class="sxs-lookup"><span data-stu-id="fe40c-185">LineItemNumber</span></span>       | <span data-ttu-id="fe40c-186">szám</span><span class="sxs-lookup"><span data-stu-id="fe40c-186">number</span></span> |    <span data-ttu-id="fe40c-187">Y</span><span class="sxs-lookup"><span data-stu-id="fe40c-187">Y</span></span>     | <span data-ttu-id="fe40c-188">A sorelem száma, 0-val kezdve</span><span class="sxs-lookup"><span data-stu-id="fe40c-188">The line item number, starting with 0</span></span>                                              |
| <span data-ttu-id="fe40c-189">OfferId (Ajánlatazonosító)</span><span class="sxs-lookup"><span data-stu-id="fe40c-189">OfferId</span></span>              | <span data-ttu-id="fe40c-190">sztring</span><span class="sxs-lookup"><span data-stu-id="fe40c-190">string</span></span> |    <span data-ttu-id="fe40c-191">Y</span><span class="sxs-lookup"><span data-stu-id="fe40c-191">Y</span></span>     | <span data-ttu-id="fe40c-192">Az ajánlat azonosítója</span><span class="sxs-lookup"><span data-stu-id="fe40c-192">The ID of the offer</span></span>                                                                |
| <span data-ttu-id="fe40c-193">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="fe40c-193">SubscriptionId</span></span>       | <span data-ttu-id="fe40c-194">sztring</span><span class="sxs-lookup"><span data-stu-id="fe40c-194">string</span></span> |    <span data-ttu-id="fe40c-195">Y</span><span class="sxs-lookup"><span data-stu-id="fe40c-195">Y</span></span>     | <span data-ttu-id="fe40c-196">Az előfizetés azonosítója</span><span class="sxs-lookup"><span data-stu-id="fe40c-196">The ID of the subscription</span></span>                                                         |
| <span data-ttu-id="fe40c-197">FriendlyName (Rövid név)</span><span class="sxs-lookup"><span data-stu-id="fe40c-197">FriendlyName</span></span>         | <span data-ttu-id="fe40c-198">sztring</span><span class="sxs-lookup"><span data-stu-id="fe40c-198">string</span></span> |    <span data-ttu-id="fe40c-199">N</span><span class="sxs-lookup"><span data-stu-id="fe40c-199">N</span></span>     | <span data-ttu-id="fe40c-200">A partner által meghatározott előfizetés rövid neve, amely segít egyértelműsni</span><span class="sxs-lookup"><span data-stu-id="fe40c-200">The friendly name for the subscription defined by the partner to help disambiguate</span></span> |
| <span data-ttu-id="fe40c-201">Mennyiség</span><span class="sxs-lookup"><span data-stu-id="fe40c-201">Quantity</span></span>             | <span data-ttu-id="fe40c-202">szám</span><span class="sxs-lookup"><span data-stu-id="fe40c-202">number</span></span> |    <span data-ttu-id="fe40c-203">Y</span><span class="sxs-lookup"><span data-stu-id="fe40c-203">Y</span></span>     | <span data-ttu-id="fe40c-204">Licencek vagy példányok száma</span><span class="sxs-lookup"><span data-stu-id="fe40c-204">The number of licenses or instances</span></span>                                                |
| <span data-ttu-id="fe40c-205">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="fe40c-205">PartnerIdOnRecord</span></span>    | <span data-ttu-id="fe40c-206">sztring</span><span class="sxs-lookup"><span data-stu-id="fe40c-206">string</span></span> |    <span data-ttu-id="fe40c-207">N</span><span class="sxs-lookup"><span data-stu-id="fe40c-207">N</span></span>     | <span data-ttu-id="fe40c-208">A rekordpartner MPN-azonosítója</span><span class="sxs-lookup"><span data-stu-id="fe40c-208">The MPN ID of the partner of record</span></span>                                                |
| <span data-ttu-id="fe40c-209">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="fe40c-209">Attributes</span></span>           | <span data-ttu-id="fe40c-210">Objektum</span><span class="sxs-lookup"><span data-stu-id="fe40c-210">Object</span></span> |    <span data-ttu-id="fe40c-211">N</span><span class="sxs-lookup"><span data-stu-id="fe40c-211">N</span></span>     | <span data-ttu-id="fe40c-212">Tartalmazza az "ObjectType": "OrderLineItem" adatokat</span><span class="sxs-lookup"><span data-stu-id="fe40c-212">Contains "ObjectType": "OrderLineItem"</span></span>                                             |

### <a name="request-example"></a><span data-ttu-id="fe40c-213">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="fe40c-213">Request example</span></span>

<span data-ttu-id="fe40c-214">Frissítés éves számlázásra</span><span class="sxs-lookup"><span data-stu-id="fe40c-214">Update to annual billing</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="fe40c-215">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="fe40c-215">REST response</span></span>

<span data-ttu-id="fe40c-216">Ha a művelet sikeres, ez a metódus a válasz törzsében adja vissza a frissített előfizetési sorrendet.</span><span class="sxs-lookup"><span data-stu-id="fe40c-216">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fe40c-217">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="fe40c-217">Response success and error codes</span></span>

<span data-ttu-id="fe40c-218">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="fe40c-218">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fe40c-219">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="fe40c-219">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fe40c-220">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="fe40c-220">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fe40c-221">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="fe40c-221">Response example</span></span>

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