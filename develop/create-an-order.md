---
title: Ügyfél rendelésének létrehozása
description: Megtudhatja, hogyan hozhat létre rendelést egy ügyfél számára a partner Center API-k használatával. A cikk előfeltételeket, lépéseket és példákat tartalmaz.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ce176909a1f9c350f1c16615171de57a7beb888d
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768624"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a><span data-ttu-id="3cf72-104">Megrendelés létrehozása egy ügyfél számára a partner Center API-k használatával</span><span class="sxs-lookup"><span data-stu-id="3cf72-104">Create an order for a customer using Partner Center APIs</span></span>

<span data-ttu-id="3cf72-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="3cf72-105">**Applies to:**</span></span>

- <span data-ttu-id="3cf72-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="3cf72-106">Partner Center</span></span>
- <span data-ttu-id="3cf72-107">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="3cf72-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="3cf72-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="3cf72-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3cf72-109">Az Azure-beli **fenntartott VM-példányok termékeinek rendelése** *csak* a következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="3cf72-109">Creating an **order for Azure reserved VM instance products** applies *only* to:</span></span>

- <span data-ttu-id="3cf72-110">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="3cf72-110">Partner Center</span></span>

<span data-ttu-id="3cf72-111">További információ a jelenleg elérhető értékesítésről: [partneri ajánlatok a Cloud Solution Provider programban](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="3cf72-111">For information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cf72-112">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="3cf72-112">Prerequisites</span></span>

- <span data-ttu-id="3cf72-113">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="3cf72-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3cf72-114">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="3cf72-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3cf72-115">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3cf72-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3cf72-116">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="3cf72-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3cf72-117">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="3cf72-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3cf72-118">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="3cf72-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3cf72-119">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="3cf72-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3cf72-120">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3cf72-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3cf72-121">Egy ajánlat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="3cf72-121">An offer identifier.</span></span>

## <a name="c"></a><span data-ttu-id="3cf72-122">C\#</span><span class="sxs-lookup"><span data-stu-id="3cf72-122">C\#</span></span>

<span data-ttu-id="3cf72-123">Megrendelés létrehozása az ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="3cf72-123">To create an order for a customer:</span></span>

1. <span data-ttu-id="3cf72-124">Hozzon létre egy [**Order**](order-resources.md) objektumot, és állítsa a **ReferenceCustomerID** tulajdonságot az ügyfél-azonosítóra az ügyfél rögzítéséhez.</span><span class="sxs-lookup"><span data-stu-id="3cf72-124">Instantiate an [**Order**](order-resources.md) object and set the **ReferenceCustomerID** property to the customer ID to record the customer.</span></span>

2. <span data-ttu-id="3cf72-125">Hozza létre a [**OrderLineItem**](order-resources.md#orderlineitem) -objektumok listáját, és rendelje hozzá a listát a rendelés **listaelemek** tulajdonságához.</span><span class="sxs-lookup"><span data-stu-id="3cf72-125">Create a list of [**OrderLineItem**](order-resources.md#orderlineitem) objects, and assign the list to the order's **LineItems** property.</span></span> <span data-ttu-id="3cf72-126">Az egyes rendelési sorok egy adott ajánlat vásárlási információit tartalmazzák.</span><span class="sxs-lookup"><span data-stu-id="3cf72-126">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="3cf72-127">Legalább egy Order line-elemmel kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="3cf72-127">You must have at least one order line item.</span></span>

3. <span data-ttu-id="3cf72-128">Szerezzen be egy illesztőfelületet a rendelési műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="3cf72-128">Obtain an interface to order operations.</span></span> <span data-ttu-id="3cf72-129">Először hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="3cf72-129">First, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="3cf72-130">Ezután kérje le a felületet az [**orders (megrendelések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) ) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="3cf72-130">Next, retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

4. <span data-ttu-id="3cf72-131">Hívja meg a [**create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) metódust, és adja meg a [**sorrend**](order-resources.md) objektumot.</span><span class="sxs-lookup"><span data-stu-id="3cf72-131">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method and pass in the [**Order**](order-resources.md) object.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

<span data-ttu-id="3cf72-132">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3cf72-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3cf72-133">**Projekt**: partner Center SDK Samples **osztály**: CreateOrder.cs</span><span class="sxs-lookup"><span data-stu-id="3cf72-133">**Project**: Partner Center SDK Samples **Class**: CreateOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="3cf72-134">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="3cf72-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3cf72-135">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="3cf72-135">Request syntax</span></span>

| <span data-ttu-id="3cf72-136">Metódus</span><span class="sxs-lookup"><span data-stu-id="3cf72-136">Method</span></span>   | <span data-ttu-id="3cf72-137">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="3cf72-137">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="3cf72-138">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="3cf72-138">**POST**</span></span> | <span data-ttu-id="3cf72-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="3cf72-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="3cf72-140">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="3cf72-140">URI parameters</span></span>

<span data-ttu-id="3cf72-141">Az ügyfél azonosításához használja a következő Path paramétert.</span><span class="sxs-lookup"><span data-stu-id="3cf72-141">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="3cf72-142">Név</span><span class="sxs-lookup"><span data-stu-id="3cf72-142">Name</span></span>        | <span data-ttu-id="3cf72-143">Típus</span><span class="sxs-lookup"><span data-stu-id="3cf72-143">Type</span></span>   | <span data-ttu-id="3cf72-144">Kötelező</span><span class="sxs-lookup"><span data-stu-id="3cf72-144">Required</span></span> | <span data-ttu-id="3cf72-145">Leírás</span><span class="sxs-lookup"><span data-stu-id="3cf72-145">Description</span></span>                                                |
|-------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="3cf72-146">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="3cf72-146">customer-id</span></span> | <span data-ttu-id="3cf72-147">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf72-147">string</span></span> | <span data-ttu-id="3cf72-148">Igen</span><span class="sxs-lookup"><span data-stu-id="3cf72-148">Yes</span></span>      | <span data-ttu-id="3cf72-149">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="3cf72-149">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3cf72-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="3cf72-150">Request headers</span></span>

<span data-ttu-id="3cf72-151">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3cf72-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3cf72-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="3cf72-152">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="3cf72-153">Sorrend</span><span class="sxs-lookup"><span data-stu-id="3cf72-153">Order</span></span>

<span data-ttu-id="3cf72-154">Ez a tábla a kérelem törzsének [Order (rendelés](order-resources.md) ) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="3cf72-154">This table describes the [Order](order-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="3cf72-155">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="3cf72-155">Property</span></span>             | <span data-ttu-id="3cf72-156">Típus</span><span class="sxs-lookup"><span data-stu-id="3cf72-156">Type</span></span>                        | <span data-ttu-id="3cf72-157">Kötelező</span><span class="sxs-lookup"><span data-stu-id="3cf72-157">Required</span></span>                        | <span data-ttu-id="3cf72-158">Leírás</span><span class="sxs-lookup"><span data-stu-id="3cf72-158">Description</span></span>                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| <span data-ttu-id="3cf72-159">id</span><span class="sxs-lookup"><span data-stu-id="3cf72-159">id</span></span>                   | <span data-ttu-id="3cf72-160">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf72-160">string</span></span>                      | <span data-ttu-id="3cf72-161">No</span><span class="sxs-lookup"><span data-stu-id="3cf72-161">No</span></span>                              | <span data-ttu-id="3cf72-162">A megrendelés sikeres létrehozásakor megadott rendelési azonosító.</span><span class="sxs-lookup"><span data-stu-id="3cf72-162">An order identifier that is supplied upon successful creation of the order.</span></span>   |
| <span data-ttu-id="3cf72-163">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="3cf72-163">referenceCustomerId</span></span>  | <span data-ttu-id="3cf72-164">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf72-164">string</span></span>                      | <span data-ttu-id="3cf72-165">No</span><span class="sxs-lookup"><span data-stu-id="3cf72-165">No</span></span>                              | <span data-ttu-id="3cf72-166">Az ügyfél-azonosító.</span><span class="sxs-lookup"><span data-stu-id="3cf72-166">The customer identifier.</span></span> |
| <span data-ttu-id="3cf72-167">billingCycle</span><span class="sxs-lookup"><span data-stu-id="3cf72-167">billingCycle</span></span>         | <span data-ttu-id="3cf72-168">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf72-168">string</span></span>                      | <span data-ttu-id="3cf72-169">No</span><span class="sxs-lookup"><span data-stu-id="3cf72-169">No</span></span>                              | <span data-ttu-id="3cf72-170">Azt jelzi, hogy milyen gyakorisággal történik a partner számlázása ebben a sorrendben.</span><span class="sxs-lookup"><span data-stu-id="3cf72-170">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="3cf72-171">A támogatott értékek a [BillingCycleType](product-resources.md#billingcycletype)található tagok nevei.</span><span class="sxs-lookup"><span data-stu-id="3cf72-171">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> <span data-ttu-id="3cf72-172">Az alapértelmezett érték a "havonta" vagy az "egykori" a megrendelés létrehozásakor.</span><span class="sxs-lookup"><span data-stu-id="3cf72-172">The default is "Monthly" or "OneTime" at order creation.</span></span> <span data-ttu-id="3cf72-173">Ez a mező a megrendelés sikeres létrehozásakor lesz alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="3cf72-173">This field is applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="3cf72-174">Listaelemek</span><span class="sxs-lookup"><span data-stu-id="3cf72-174">lineItems</span></span>            | <span data-ttu-id="3cf72-175">[OrderLineItem](order-resources.md#orderlineitem) -erőforrások tömbje</span><span class="sxs-lookup"><span data-stu-id="3cf72-175">array of [OrderLineItem](order-resources.md#orderlineitem) resources</span></span> | <span data-ttu-id="3cf72-176">Igen</span><span class="sxs-lookup"><span data-stu-id="3cf72-176">Yes</span></span>      | <span data-ttu-id="3cf72-177">Az ügyfél által megvásárolt ajánlatok részletezett listája, beleértve a mennyiséget is.</span><span class="sxs-lookup"><span data-stu-id="3cf72-177">An itemized list of the offers the customer is purchasing including the quantity.</span></span>        |
| <span data-ttu-id="3cf72-178">currencyCode</span><span class="sxs-lookup"><span data-stu-id="3cf72-178">currencyCode</span></span>         | <span data-ttu-id="3cf72-179">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf72-179">string</span></span>                      | <span data-ttu-id="3cf72-180">No</span><span class="sxs-lookup"><span data-stu-id="3cf72-180">No</span></span>                              | <span data-ttu-id="3cf72-181">Csak olvasható.</span><span class="sxs-lookup"><span data-stu-id="3cf72-181">Read-only.</span></span> <span data-ttu-id="3cf72-182">A megrendelés elhelyezésekor használt pénznem.</span><span class="sxs-lookup"><span data-stu-id="3cf72-182">The currency used when placing the order.</span></span> <span data-ttu-id="3cf72-183">A megrendelés sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="3cf72-183">Applied upon successful creation of the order.</span></span>           |
| <span data-ttu-id="3cf72-184">creationDate</span><span class="sxs-lookup"><span data-stu-id="3cf72-184">creationDate</span></span>         | <span data-ttu-id="3cf72-185">dátum/idő</span><span class="sxs-lookup"><span data-stu-id="3cf72-185">datetime</span></span>                    | <span data-ttu-id="3cf72-186">Nem</span><span class="sxs-lookup"><span data-stu-id="3cf72-186">No</span></span>                              | <span data-ttu-id="3cf72-187">Csak olvasható.</span><span class="sxs-lookup"><span data-stu-id="3cf72-187">Read-only.</span></span> <span data-ttu-id="3cf72-188">A rendelés létrehozásának dátuma dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="3cf72-188">The date the order was created, in date-time format.</span></span> <span data-ttu-id="3cf72-189">A megrendelés sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="3cf72-189">Applied upon successful creation of the order.</span></span>                                   |
| <span data-ttu-id="3cf72-190">status</span><span class="sxs-lookup"><span data-stu-id="3cf72-190">status</span></span>               | <span data-ttu-id="3cf72-191">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf72-191">string</span></span>                      | <span data-ttu-id="3cf72-192">No</span><span class="sxs-lookup"><span data-stu-id="3cf72-192">No</span></span>                              | <span data-ttu-id="3cf72-193">Csak olvasható.</span><span class="sxs-lookup"><span data-stu-id="3cf72-193">Read-only.</span></span> <span data-ttu-id="3cf72-194">A megrendelés állapota.</span><span class="sxs-lookup"><span data-stu-id="3cf72-194">The status of the order.</span></span>  <span data-ttu-id="3cf72-195">A támogatott értékek a [OrderStatus](order-resources.md#orderstatus)található tagok nevei.</span><span class="sxs-lookup"><span data-stu-id="3cf72-195">Supported values are the member names found in [OrderStatus](order-resources.md#orderstatus).</span></span>        |
| <span data-ttu-id="3cf72-196">linkek</span><span class="sxs-lookup"><span data-stu-id="3cf72-196">links</span></span>                | [<span data-ttu-id="3cf72-197">OrderLinks</span><span class="sxs-lookup"><span data-stu-id="3cf72-197">OrderLinks</span></span>](utility-resources.md#resourcelinks)              | <span data-ttu-id="3cf72-198">Nem</span><span class="sxs-lookup"><span data-stu-id="3cf72-198">No</span></span>                              | <span data-ttu-id="3cf72-199">A rendelésnek megfelelő erőforrás-hivatkozások.</span><span class="sxs-lookup"><span data-stu-id="3cf72-199">The resource links corresponding to the Order.</span></span> |
| <span data-ttu-id="3cf72-200">attribútumok</span><span class="sxs-lookup"><span data-stu-id="3cf72-200">attributes</span></span>           | [<span data-ttu-id="3cf72-201">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="3cf72-201">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="3cf72-202">Nem</span><span class="sxs-lookup"><span data-stu-id="3cf72-202">No</span></span>                              | <span data-ttu-id="3cf72-203">A sorrendnek megfelelő metaadat-attribútumok.</span><span class="sxs-lookup"><span data-stu-id="3cf72-203">The metadata attributes corresponding to the Order.</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="3cf72-204">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="3cf72-204">OrderLineItem</span></span>

<span data-ttu-id="3cf72-205">Ez a táblázat a kérelem törzsének [OrderLineItem](order-resources.md#orderlineitem) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="3cf72-205">This table describes the [OrderLineItem](order-resources.md#orderlineitem) properties in the request body.</span></span>

>[!NOTE]
><span data-ttu-id="3cf72-206">A partnerIdOnRecord csak akkor adható meg, ha egy közvetett szolgáltató egy közvetett viszonteladó nevében rendezi a rendelést.</span><span class="sxs-lookup"><span data-stu-id="3cf72-206">The partnerIdOnRecord should only be provided when an indirect provider places an order on behalf of an indirect reseller.</span></span> <span data-ttu-id="3cf72-207">A rendszer a közvetett viszonteladó Microsoft Partner Network-AZONOSÍTÓját tárolja (soha nem a közvetett szolgáltató AZONOSÍTÓját).</span><span class="sxs-lookup"><span data-stu-id="3cf72-207">It's used to store the Microsoft Partner Network ID of the indirect reseller only (never the ID of the indirect provider).</span></span>

| <span data-ttu-id="3cf72-208">Név</span><span class="sxs-lookup"><span data-stu-id="3cf72-208">Name</span></span>                 | <span data-ttu-id="3cf72-209">Típus</span><span class="sxs-lookup"><span data-stu-id="3cf72-209">Type</span></span>   | <span data-ttu-id="3cf72-210">Kötelező</span><span class="sxs-lookup"><span data-stu-id="3cf72-210">Required</span></span> | <span data-ttu-id="3cf72-211">Leírás</span><span class="sxs-lookup"><span data-stu-id="3cf72-211">Description</span></span>                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3cf72-212">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="3cf72-212">lineItemNumber</span></span>       | <span data-ttu-id="3cf72-213">int</span><span class="sxs-lookup"><span data-stu-id="3cf72-213">int</span></span>    | <span data-ttu-id="3cf72-214">Igen</span><span class="sxs-lookup"><span data-stu-id="3cf72-214">Yes</span></span>      | <span data-ttu-id="3cf72-215">A gyűjtemény minden egyes sora egy egyedi sorszámot kap, amely a 0 és Count-1 közötti számlálást eredményezi.</span><span class="sxs-lookup"><span data-stu-id="3cf72-215">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span>                                                                                                                                                 |
| <span data-ttu-id="3cf72-216">offerId</span><span class="sxs-lookup"><span data-stu-id="3cf72-216">offerId</span></span>              | <span data-ttu-id="3cf72-217">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf72-217">string</span></span> | <span data-ttu-id="3cf72-218">Igen</span><span class="sxs-lookup"><span data-stu-id="3cf72-218">Yes</span></span>      | <span data-ttu-id="3cf72-219">Az ajánlat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="3cf72-219">The offer identifier.</span></span>                                                                                                                                                                                                                      |
| <span data-ttu-id="3cf72-220">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="3cf72-220">subscriptionId</span></span>       | <span data-ttu-id="3cf72-221">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf72-221">string</span></span> | <span data-ttu-id="3cf72-222">No</span><span class="sxs-lookup"><span data-stu-id="3cf72-222">No</span></span>       | <span data-ttu-id="3cf72-223">Az előfizetés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="3cf72-223">The subscription identifier.</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="3cf72-224">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="3cf72-224">parentSubscriptionId</span></span> | <span data-ttu-id="3cf72-225">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf72-225">string</span></span> | <span data-ttu-id="3cf72-226">No</span><span class="sxs-lookup"><span data-stu-id="3cf72-226">No</span></span>       | <span data-ttu-id="3cf72-227">Választható.</span><span class="sxs-lookup"><span data-stu-id="3cf72-227">Optional.</span></span> <span data-ttu-id="3cf72-228">A szülő-előfizetés azonosítója egy kiegészítő ajánlatban.</span><span class="sxs-lookup"><span data-stu-id="3cf72-228">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="3cf72-229">Csak a JAVÍTÁSra vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="3cf72-229">Applies to PATCH only.</span></span>                                                                                                                                                     |
| <span data-ttu-id="3cf72-230">friendlyName</span><span class="sxs-lookup"><span data-stu-id="3cf72-230">friendlyName</span></span>         | <span data-ttu-id="3cf72-231">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf72-231">string</span></span> | <span data-ttu-id="3cf72-232">No</span><span class="sxs-lookup"><span data-stu-id="3cf72-232">No</span></span>       | <span data-ttu-id="3cf72-233">Választható.</span><span class="sxs-lookup"><span data-stu-id="3cf72-233">Optional.</span></span> <span data-ttu-id="3cf72-234">A partner által az előfizetéshez megadott rövid név, amely segít a egyértelműsítse.</span><span class="sxs-lookup"><span data-stu-id="3cf72-234">The friendly name for the subscription defined by the partner to help disambiguate.</span></span>                                                                                                                                              |
| <span data-ttu-id="3cf72-235">quantity</span><span class="sxs-lookup"><span data-stu-id="3cf72-235">quantity</span></span>             | <span data-ttu-id="3cf72-236">int</span><span class="sxs-lookup"><span data-stu-id="3cf72-236">int</span></span>    | <span data-ttu-id="3cf72-237">Igen</span><span class="sxs-lookup"><span data-stu-id="3cf72-237">Yes</span></span>      | <span data-ttu-id="3cf72-238">A licenc alapú előfizetéshez tartozó licencek száma.</span><span class="sxs-lookup"><span data-stu-id="3cf72-238">The number of licenses for a license-based subscription.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="3cf72-239">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="3cf72-239">partnerIdOnRecord</span></span>    | <span data-ttu-id="3cf72-240">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf72-240">string</span></span> | <span data-ttu-id="3cf72-241">No</span><span class="sxs-lookup"><span data-stu-id="3cf72-241">No</span></span>       | <span data-ttu-id="3cf72-242">Ha egy közvetett szolgáltató egy megrendelést helyez el egy közvetett viszonteladó nevében, töltse ki ezt a mezőt a **közvetett viszonteladóhoz** tartozó MPN-azonosítóval (soha nem a közvetett szolgáltató azonosítója).</span><span class="sxs-lookup"><span data-stu-id="3cf72-242">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="3cf72-243">Ez biztosítja az ösztönzők megfelelő könyvelését.</span><span class="sxs-lookup"><span data-stu-id="3cf72-243">This ensures proper accounting for incentives.</span></span> |
| <span data-ttu-id="3cf72-244">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="3cf72-244">provisioningContext</span></span>  | <span data-ttu-id="3cf72-245">Szótár<karakterlánc, karakterlánc></span><span class="sxs-lookup"><span data-stu-id="3cf72-245">Dictionary<string, string></span></span>                | <span data-ttu-id="3cf72-246">Nem</span><span class="sxs-lookup"><span data-stu-id="3cf72-246">No</span></span>       |  <span data-ttu-id="3cf72-247">A katalógus egyes elemeinek kiépítési feladataihoz szükséges információk.</span><span class="sxs-lookup"><span data-stu-id="3cf72-247">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="3cf72-248">Az SKU provisioningVariables tulajdonsága azt jelzi, hogy mely tulajdonságok szükségesek a katalógus adott elemeihez.</span><span class="sxs-lookup"><span data-stu-id="3cf72-248">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span>                  |
| <span data-ttu-id="3cf72-249">linkek</span><span class="sxs-lookup"><span data-stu-id="3cf72-249">links</span></span>                | [<span data-ttu-id="3cf72-250">OrderLineItemLinks</span><span class="sxs-lookup"><span data-stu-id="3cf72-250">OrderLineItemLinks</span></span>](order-resources.md#orderlineitemlinks) | <span data-ttu-id="3cf72-251">Nem</span><span class="sxs-lookup"><span data-stu-id="3cf72-251">No</span></span>       |  <span data-ttu-id="3cf72-252">Csak olvasható.</span><span class="sxs-lookup"><span data-stu-id="3cf72-252">Read-only.</span></span> <span data-ttu-id="3cf72-253">A rendelési sorhoz tartozó erőforrás-hivatkozások.</span><span class="sxs-lookup"><span data-stu-id="3cf72-253">The resource links corresponding to the Order line item.</span></span>  |
| <span data-ttu-id="3cf72-254">attribútumok</span><span class="sxs-lookup"><span data-stu-id="3cf72-254">attributes</span></span>           | [<span data-ttu-id="3cf72-255">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="3cf72-255">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="3cf72-256">Nem</span><span class="sxs-lookup"><span data-stu-id="3cf72-256">No</span></span>       | <span data-ttu-id="3cf72-257">A OrderLineItem megfelelő metaadat-attribútumok.</span><span class="sxs-lookup"><span data-stu-id="3cf72-257">The metadata attributes corresponding to the OrderLineItem.</span></span> |
| <span data-ttu-id="3cf72-258">renewsTo</span><span class="sxs-lookup"><span data-stu-id="3cf72-258">renewsTo</span></span>             | <span data-ttu-id="3cf72-259">Objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="3cf72-259">Array of objects</span></span>                          | <span data-ttu-id="3cf72-260">Nem</span><span class="sxs-lookup"><span data-stu-id="3cf72-260">No</span></span>    |<span data-ttu-id="3cf72-261">[RenewsTo](order-resources.md#renewsto) -erőforrások tömbje.</span><span class="sxs-lookup"><span data-stu-id="3cf72-261">An array of [RenewsTo](order-resources.md#renewsto) resources.</span></span>                                                                            |

##### <a name="renewsto"></a><span data-ttu-id="3cf72-262">RenewsTo</span><span class="sxs-lookup"><span data-stu-id="3cf72-262">RenewsTo</span></span>

<span data-ttu-id="3cf72-263">Ez a táblázat a kérelem törzsének [RenewsTo](order-resources.md#renewsto) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="3cf72-263">This table describes the [RenewsTo](order-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="3cf72-264">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="3cf72-264">Property</span></span>              | <span data-ttu-id="3cf72-265">Típus</span><span class="sxs-lookup"><span data-stu-id="3cf72-265">Type</span></span>             | <span data-ttu-id="3cf72-266">Kötelező</span><span class="sxs-lookup"><span data-stu-id="3cf72-266">Required</span></span>        | <span data-ttu-id="3cf72-267">Leírás</span><span class="sxs-lookup"><span data-stu-id="3cf72-267">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3cf72-268">termDuration</span><span class="sxs-lookup"><span data-stu-id="3cf72-268">termDuration</span></span>          | <span data-ttu-id="3cf72-269">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf72-269">string</span></span>           | <span data-ttu-id="3cf72-270">No</span><span class="sxs-lookup"><span data-stu-id="3cf72-270">No</span></span>              | <span data-ttu-id="3cf72-271">A megújítási időszak érvényességének ISO 8601-es ábrázolása.</span><span class="sxs-lookup"><span data-stu-id="3cf72-271">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="3cf72-272">A jelenleg támogatott értékek a következők: **P1M** (1 hónap) és **P1Y** (1 év).</span><span class="sxs-lookup"><span data-stu-id="3cf72-272">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="3cf72-273">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="3cf72-273">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a><span data-ttu-id="3cf72-274">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="3cf72-274">REST response</span></span>

<span data-ttu-id="3cf72-275">Ha a művelet sikeres, a metódus egy [Order](order-resources.md) erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="3cf72-275">If successful, the method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3cf72-276">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="3cf72-276">Response success and error codes</span></span>

<span data-ttu-id="3cf72-277">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="3cf72-277">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3cf72-278">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="3cf72-278">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3cf72-279">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3cf72-279">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3cf72-280">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="3cf72-280">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
