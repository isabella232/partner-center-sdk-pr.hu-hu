---
title: Ügyfélrendelés létrehozása
description: Megtudhatja, hogyan hozhat létre rendelést Partnerközpont API-k használatával egy ügyfél számára. A cikk előfeltételeket, lépéseket és példákat tartalmaz.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c3a86a99f43bdeec5e4c560ab59e1924b76c0636
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973544"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a><span data-ttu-id="1a466-104">Rendelés létrehozása egy ügyfél számára a Partnerközpont API-k használatával</span><span class="sxs-lookup"><span data-stu-id="1a466-104">Create an order for a customer using Partner Center APIs</span></span>

<span data-ttu-id="1a466-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1a466-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1a466-106">Az **Azure-beli fenntartott VM-példányok termékeire vonatkozó rendelés** létrehozása csak a *következőkre* vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="1a466-106">Creating an **order for Azure reserved VM instance products** applies *only* to:</span></span>

- <span data-ttu-id="1a466-107">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="1a466-107">Partner Center</span></span>

<span data-ttu-id="1a466-108">A jelenleg értékesíthető információkért lásd a partneri ajánlatokat a [Felhőszolgáltató programjában.](/partner-center/csp-offers)</span><span class="sxs-lookup"><span data-stu-id="1a466-108">For information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a466-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="1a466-109">Prerequisites</span></span>

- <span data-ttu-id="1a466-110">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1a466-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1a466-111">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="1a466-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1a466-112">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1a466-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1a466-113">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="1a466-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1a466-114">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="1a466-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1a466-115">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="1a466-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1a466-116">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="1a466-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1a466-117">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1a466-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1a466-118">Egy ajánlatazonosító.</span><span class="sxs-lookup"><span data-stu-id="1a466-118">An offer identifier.</span></span>

## <a name="c"></a><span data-ttu-id="1a466-119">C\#</span><span class="sxs-lookup"><span data-stu-id="1a466-119">C\#</span></span>

<span data-ttu-id="1a466-120">Rendelés létrehozása egy ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="1a466-120">To create an order for a customer:</span></span>

1. <span data-ttu-id="1a466-121">Példányositsa az [**Order**](order-resources.md) objektumot, és állítsa a **ReferenceCustomerID** tulajdonságot az ügyfélazonosítóra az ügyfél rögzítéséhez.</span><span class="sxs-lookup"><span data-stu-id="1a466-121">Instantiate an [**Order**](order-resources.md) object and set the **ReferenceCustomerID** property to the customer ID to record the customer.</span></span>

2. <span data-ttu-id="1a466-122">Hozzon létre egy [**listát az OrderLineItem**](order-resources.md#orderlineitem) objektumokból, és rendelje hozzá a listát a rendelés **LineItems tulajdonságához.**</span><span class="sxs-lookup"><span data-stu-id="1a466-122">Create a list of [**OrderLineItem**](order-resources.md#orderlineitem) objects, and assign the list to the order's **LineItems** property.</span></span> <span data-ttu-id="1a466-123">Minden rendeléssorelem egy adott ajánlat vásárlási adatait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="1a466-123">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="1a466-124">Legalább egy megrendeléssor-elemnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="1a466-124">You must have at least one order line item.</span></span>

3. <span data-ttu-id="1a466-125">Szerezzen be egy interfészt a műveletek megrendelésére.</span><span class="sxs-lookup"><span data-stu-id="1a466-125">Obtain an interface to order operations.</span></span> <span data-ttu-id="1a466-126">Először hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="1a466-126">First, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="1a466-127">Ezután olvassa be az interfészt az [**Orders tulajdonságból.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)</span><span class="sxs-lookup"><span data-stu-id="1a466-127">Next, retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

4. <span data-ttu-id="1a466-128">Hívja meg [**a Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) vagy [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) metódust, és adja át az [**Order objektumot.**](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="1a466-128">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method and pass in the [**Order**](order-resources.md) object.</span></span>

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

<span data-ttu-id="1a466-129">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1a466-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1a466-130">**Project**: Partnerközpont SDK **Osztály:** CreateOrder.cs</span><span class="sxs-lookup"><span data-stu-id="1a466-130">**Project**: Partner Center SDK Samples **Class**: CreateOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1a466-131">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="1a466-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1a466-132">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="1a466-132">Request syntax</span></span>

| <span data-ttu-id="1a466-133">Metódus</span><span class="sxs-lookup"><span data-stu-id="1a466-133">Method</span></span>   | <span data-ttu-id="1a466-134">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="1a466-134">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="1a466-135">**Post**</span><span class="sxs-lookup"><span data-stu-id="1a466-135">**POST**</span></span> | <span data-ttu-id="1a466-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1a466-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="1a466-137">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="1a466-137">URI parameters</span></span>

<span data-ttu-id="1a466-138">Az ügyfél azonosításához használja a következő path paramétert.</span><span class="sxs-lookup"><span data-stu-id="1a466-138">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="1a466-139">Név</span><span class="sxs-lookup"><span data-stu-id="1a466-139">Name</span></span>        | <span data-ttu-id="1a466-140">Típus</span><span class="sxs-lookup"><span data-stu-id="1a466-140">Type</span></span>   | <span data-ttu-id="1a466-141">Kötelező</span><span class="sxs-lookup"><span data-stu-id="1a466-141">Required</span></span> | <span data-ttu-id="1a466-142">Leírás</span><span class="sxs-lookup"><span data-stu-id="1a466-142">Description</span></span>                                                |
|-------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="1a466-143">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="1a466-143">customer-id</span></span> | <span data-ttu-id="1a466-144">sztring</span><span class="sxs-lookup"><span data-stu-id="1a466-144">string</span></span> | <span data-ttu-id="1a466-145">Igen</span><span class="sxs-lookup"><span data-stu-id="1a466-145">Yes</span></span>      | <span data-ttu-id="1a466-146">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="1a466-146">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1a466-147">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="1a466-147">Request headers</span></span>

<span data-ttu-id="1a466-148">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1a466-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1a466-149">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="1a466-149">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="1a466-150">Sorrend</span><span class="sxs-lookup"><span data-stu-id="1a466-150">Order</span></span>

<span data-ttu-id="1a466-151">Ez a táblázat a kérelem törzsében található [Order (Rendelés)](order-resources.md) tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="1a466-151">This table describes the [Order](order-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="1a466-152">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="1a466-152">Property</span></span>             | <span data-ttu-id="1a466-153">Típus</span><span class="sxs-lookup"><span data-stu-id="1a466-153">Type</span></span>                        | <span data-ttu-id="1a466-154">Kötelező</span><span class="sxs-lookup"><span data-stu-id="1a466-154">Required</span></span>                        | <span data-ttu-id="1a466-155">Leírás</span><span class="sxs-lookup"><span data-stu-id="1a466-155">Description</span></span>                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| <span data-ttu-id="1a466-156">id</span><span class="sxs-lookup"><span data-stu-id="1a466-156">id</span></span>                   | <span data-ttu-id="1a466-157">sztring</span><span class="sxs-lookup"><span data-stu-id="1a466-157">string</span></span>                      | <span data-ttu-id="1a466-158">No</span><span class="sxs-lookup"><span data-stu-id="1a466-158">No</span></span>                              | <span data-ttu-id="1a466-159">A rendelés sikeres létrehozása után megadott rendelésazonosító.</span><span class="sxs-lookup"><span data-stu-id="1a466-159">An order identifier that is supplied upon successful creation of the order.</span></span>   |
| <span data-ttu-id="1a466-160">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="1a466-160">referenceCustomerId</span></span>  | <span data-ttu-id="1a466-161">sztring</span><span class="sxs-lookup"><span data-stu-id="1a466-161">string</span></span>                      | <span data-ttu-id="1a466-162">No</span><span class="sxs-lookup"><span data-stu-id="1a466-162">No</span></span>                              | <span data-ttu-id="1a466-163">Az ügyfél azonosítója.</span><span class="sxs-lookup"><span data-stu-id="1a466-163">The customer identifier.</span></span> |
| <span data-ttu-id="1a466-164">billingCycle (számlázási ciklus)</span><span class="sxs-lookup"><span data-stu-id="1a466-164">billingCycle</span></span>         | <span data-ttu-id="1a466-165">sztring</span><span class="sxs-lookup"><span data-stu-id="1a466-165">string</span></span>                      | <span data-ttu-id="1a466-166">No</span><span class="sxs-lookup"><span data-stu-id="1a466-166">No</span></span>                              | <span data-ttu-id="1a466-167">Azt jelzi, hogy milyen gyakorisággal számlázták a partnert a rendelésért.</span><span class="sxs-lookup"><span data-stu-id="1a466-167">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="1a466-168">A támogatott értékek a [BillingCycleType](product-resources.md#billingcycletype)típusban található tagnevek.</span><span class="sxs-lookup"><span data-stu-id="1a466-168">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> <span data-ttu-id="1a466-169">Az alapértelmezett érték a "Havi" vagy a "OneTime" a rendelés létrehozásakor.</span><span class="sxs-lookup"><span data-stu-id="1a466-169">The default is "Monthly" or "OneTime" at order creation.</span></span> <span data-ttu-id="1a466-170">Ez a mező a rendelés sikeres létrehozásakor lesz alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="1a466-170">This field is applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="1a466-171">lineItems (sorsorok)</span><span class="sxs-lookup"><span data-stu-id="1a466-171">lineItems</span></span>            | <span data-ttu-id="1a466-172">[OrderLineItem-erőforrások tömbje](order-resources.md#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="1a466-172">array of [OrderLineItem](order-resources.md#orderlineitem) resources</span></span> | <span data-ttu-id="1a466-173">Igen</span><span class="sxs-lookup"><span data-stu-id="1a466-173">Yes</span></span>      | <span data-ttu-id="1a466-174">Az ügyfél által megvásárolt ajánlatok elemi listája, beleértve a mennyiséget is.</span><span class="sxs-lookup"><span data-stu-id="1a466-174">An itemized list of the offers the customer is purchasing including the quantity.</span></span>        |
| <span data-ttu-id="1a466-175">currencyCode</span><span class="sxs-lookup"><span data-stu-id="1a466-175">currencyCode</span></span>         | <span data-ttu-id="1a466-176">sztring</span><span class="sxs-lookup"><span data-stu-id="1a466-176">string</span></span>                      | <span data-ttu-id="1a466-177">No</span><span class="sxs-lookup"><span data-stu-id="1a466-177">No</span></span>                              | <span data-ttu-id="1a466-178">Csak olvasható.</span><span class="sxs-lookup"><span data-stu-id="1a466-178">Read-only.</span></span> <span data-ttu-id="1a466-179">A rendelés leadáskor használt pénznem.</span><span class="sxs-lookup"><span data-stu-id="1a466-179">The currency used when placing the order.</span></span> <span data-ttu-id="1a466-180">A rendelés sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="1a466-180">Applied upon successful creation of the order.</span></span>           |
| <span data-ttu-id="1a466-181">creationDate (Létrehozás dátuma)</span><span class="sxs-lookup"><span data-stu-id="1a466-181">creationDate</span></span>         | <span data-ttu-id="1a466-182">dátum/idő</span><span class="sxs-lookup"><span data-stu-id="1a466-182">datetime</span></span>                    | <span data-ttu-id="1a466-183">Nem</span><span class="sxs-lookup"><span data-stu-id="1a466-183">No</span></span>                              | <span data-ttu-id="1a466-184">Csak olvasható.</span><span class="sxs-lookup"><span data-stu-id="1a466-184">Read-only.</span></span> <span data-ttu-id="1a466-185">A rendelés létrehozási dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="1a466-185">The date the order was created, in date-time format.</span></span> <span data-ttu-id="1a466-186">A rendelés sikeres létrehozása után alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="1a466-186">Applied upon successful creation of the order.</span></span>                                   |
| <span data-ttu-id="1a466-187">status</span><span class="sxs-lookup"><span data-stu-id="1a466-187">status</span></span>               | <span data-ttu-id="1a466-188">sztring</span><span class="sxs-lookup"><span data-stu-id="1a466-188">string</span></span>                      | <span data-ttu-id="1a466-189">No</span><span class="sxs-lookup"><span data-stu-id="1a466-189">No</span></span>                              | <span data-ttu-id="1a466-190">Csak olvasható.</span><span class="sxs-lookup"><span data-stu-id="1a466-190">Read-only.</span></span> <span data-ttu-id="1a466-191">A rendelés állapota.</span><span class="sxs-lookup"><span data-stu-id="1a466-191">The status of the order.</span></span>  <span data-ttu-id="1a466-192">A támogatott értékek az [OrderStatus](order-resources.md#orderstatus)oszlopban található tagnevek.</span><span class="sxs-lookup"><span data-stu-id="1a466-192">Supported values are the member names found in [OrderStatus](order-resources.md#orderstatus).</span></span>        |
| <span data-ttu-id="1a466-193">Linkek</span><span class="sxs-lookup"><span data-stu-id="1a466-193">links</span></span>                | [<span data-ttu-id="1a466-194">OrderLinks (Megrendelési hivatkozás)</span><span class="sxs-lookup"><span data-stu-id="1a466-194">OrderLinks</span></span>](utility-resources.md#resourcelinks)              | <span data-ttu-id="1a466-195">Nem</span><span class="sxs-lookup"><span data-stu-id="1a466-195">No</span></span>                              | <span data-ttu-id="1a466-196">Az Order (Rendelés) erőforrás-hivatkozások.</span><span class="sxs-lookup"><span data-stu-id="1a466-196">The resource links corresponding to the Order.</span></span> |
| <span data-ttu-id="1a466-197">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="1a466-197">attributes</span></span>           | [<span data-ttu-id="1a466-198">ResourceAttributes (Erőforrás-attribútumok)</span><span class="sxs-lookup"><span data-stu-id="1a466-198">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="1a466-199">Nem</span><span class="sxs-lookup"><span data-stu-id="1a466-199">No</span></span>                              | <span data-ttu-id="1a466-200">Az Order attribútumnak megfelelő metaadat-attribútumok.</span><span class="sxs-lookup"><span data-stu-id="1a466-200">The metadata attributes corresponding to the Order.</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="1a466-201">OrderLineItem (Megrendelési vonal)</span><span class="sxs-lookup"><span data-stu-id="1a466-201">OrderLineItem</span></span>

<span data-ttu-id="1a466-202">Ez a táblázat a kérelem törzsében található [OrderLineItem](order-resources.md#orderlineitem) tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="1a466-202">This table describes the [OrderLineItem](order-resources.md#orderlineitem) properties in the request body.</span></span>

>[!NOTE]
><span data-ttu-id="1a466-203">A partnerIdOnRecord csak akkor biztosított, ha egy közvetett szolgáltató egy közvetett viszonteladó nevében ad ki rendelést.</span><span class="sxs-lookup"><span data-stu-id="1a466-203">The partnerIdOnRecord should only be provided when an indirect provider places an order on behalf of an indirect reseller.</span></span> <span data-ttu-id="1a466-204">Csak a közvetett viszonteladó Microsoft Partner Network tárolására használatos (soha nem a közvetett szolgáltató azonosítója).</span><span class="sxs-lookup"><span data-stu-id="1a466-204">It's used to store the Microsoft Partner Network ID of the indirect reseller only (never the ID of the indirect provider).</span></span>

| <span data-ttu-id="1a466-205">Név</span><span class="sxs-lookup"><span data-stu-id="1a466-205">Name</span></span>                 | <span data-ttu-id="1a466-206">Típus</span><span class="sxs-lookup"><span data-stu-id="1a466-206">Type</span></span>   | <span data-ttu-id="1a466-207">Kötelező</span><span class="sxs-lookup"><span data-stu-id="1a466-207">Required</span></span> | <span data-ttu-id="1a466-208">Leírás</span><span class="sxs-lookup"><span data-stu-id="1a466-208">Description</span></span>                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1a466-209">lineItemNumber (sor száma)</span><span class="sxs-lookup"><span data-stu-id="1a466-209">lineItemNumber</span></span>       | <span data-ttu-id="1a466-210">int</span><span class="sxs-lookup"><span data-stu-id="1a466-210">int</span></span>    | <span data-ttu-id="1a466-211">Igen</span><span class="sxs-lookup"><span data-stu-id="1a466-211">Yes</span></span>      | <span data-ttu-id="1a466-212">A gyűjtemény minden soreleme egyedi sorszámot kap, amely 0-tól count-1-ig számol.</span><span class="sxs-lookup"><span data-stu-id="1a466-212">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span>                                                                                                                                                 |
| <span data-ttu-id="1a466-213">offerId (ajánlatazonosító)</span><span class="sxs-lookup"><span data-stu-id="1a466-213">offerId</span></span>              | <span data-ttu-id="1a466-214">sztring</span><span class="sxs-lookup"><span data-stu-id="1a466-214">string</span></span> | <span data-ttu-id="1a466-215">Igen</span><span class="sxs-lookup"><span data-stu-id="1a466-215">Yes</span></span>      | <span data-ttu-id="1a466-216">Az ajánlat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="1a466-216">The offer identifier.</span></span>                                                                                                                                                                                                                      |
| <span data-ttu-id="1a466-217">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="1a466-217">subscriptionId</span></span>       | <span data-ttu-id="1a466-218">sztring</span><span class="sxs-lookup"><span data-stu-id="1a466-218">string</span></span> | <span data-ttu-id="1a466-219">No</span><span class="sxs-lookup"><span data-stu-id="1a466-219">No</span></span>       | <span data-ttu-id="1a466-220">Az előfizetés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="1a466-220">The subscription identifier.</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="1a466-221">parentSubscriptionId (parentSubscriptionId)</span><span class="sxs-lookup"><span data-stu-id="1a466-221">parentSubscriptionId</span></span> | <span data-ttu-id="1a466-222">sztring</span><span class="sxs-lookup"><span data-stu-id="1a466-222">string</span></span> | <span data-ttu-id="1a466-223">No</span><span class="sxs-lookup"><span data-stu-id="1a466-223">No</span></span>       | <span data-ttu-id="1a466-224">Választható.</span><span class="sxs-lookup"><span data-stu-id="1a466-224">Optional.</span></span> <span data-ttu-id="1a466-225">A szülő-előfizetés azonosítója egy bővítményajánlatban.</span><span class="sxs-lookup"><span data-stu-id="1a466-225">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="1a466-226">Csak a PATCH-re vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="1a466-226">Applies to PATCH only.</span></span>                                                                                                                                                     |
| <span data-ttu-id="1a466-227">friendlyName (rövid név)</span><span class="sxs-lookup"><span data-stu-id="1a466-227">friendlyName</span></span>         | <span data-ttu-id="1a466-228">sztring</span><span class="sxs-lookup"><span data-stu-id="1a466-228">string</span></span> | <span data-ttu-id="1a466-229">No</span><span class="sxs-lookup"><span data-stu-id="1a466-229">No</span></span>       | <span data-ttu-id="1a466-230">Választható.</span><span class="sxs-lookup"><span data-stu-id="1a466-230">Optional.</span></span> <span data-ttu-id="1a466-231">A partner által meghatározott előfizetés rövid neve a egyértelműséghez.</span><span class="sxs-lookup"><span data-stu-id="1a466-231">The friendly name for the subscription defined by the partner to help disambiguate.</span></span>                                                                                                                                              |
| <span data-ttu-id="1a466-232">quantity</span><span class="sxs-lookup"><span data-stu-id="1a466-232">quantity</span></span>             | <span data-ttu-id="1a466-233">int</span><span class="sxs-lookup"><span data-stu-id="1a466-233">int</span></span>    | <span data-ttu-id="1a466-234">Igen</span><span class="sxs-lookup"><span data-stu-id="1a466-234">Yes</span></span>      | <span data-ttu-id="1a466-235">A licencalapú előfizetések licenceinek száma.</span><span class="sxs-lookup"><span data-stu-id="1a466-235">The number of licenses for a license-based subscription.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="1a466-236">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="1a466-236">partnerIdOnRecord</span></span>    | <span data-ttu-id="1a466-237">sztring</span><span class="sxs-lookup"><span data-stu-id="1a466-237">string</span></span> | <span data-ttu-id="1a466-238">No</span><span class="sxs-lookup"><span data-stu-id="1a466-238">No</span></span>       | <span data-ttu-id="1a466-239">Ha egy közvetett szolgáltató egy közvetett viszonteladó nevében ad ki rendelést, akkor ezt a mezőt csak a közvetett viszonteladó MPN-azonosítójával **töltse** fel (soha ne a közvetett szolgáltató azonosítójával).</span><span class="sxs-lookup"><span data-stu-id="1a466-239">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="1a466-240">Ez biztosítja az ösztönzők megfelelő elszámolását.</span><span class="sxs-lookup"><span data-stu-id="1a466-240">This ensures proper accounting for incentives.</span></span> |
| <span data-ttu-id="1a466-241">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="1a466-241">provisioningContext</span></span>  | <span data-ttu-id="1a466-242">Szótár<sztring, sztring></span><span class="sxs-lookup"><span data-stu-id="1a466-242">Dictionary<string, string></span></span>                | <span data-ttu-id="1a466-243">Nem</span><span class="sxs-lookup"><span data-stu-id="1a466-243">No</span></span>       |  <span data-ttu-id="1a466-244">A katalógus egyes elemeinek kiépítéséhez szükséges információk.</span><span class="sxs-lookup"><span data-stu-id="1a466-244">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="1a466-245">A termékváltozat provisioningVariables tulajdonsága jelzi, hogy mely tulajdonságok szükségesek a katalógus adott elemeihez.</span><span class="sxs-lookup"><span data-stu-id="1a466-245">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span>                  |
| <span data-ttu-id="1a466-246">Linkek</span><span class="sxs-lookup"><span data-stu-id="1a466-246">links</span></span>                | [<span data-ttu-id="1a466-247">OrderLineItemLinks</span><span class="sxs-lookup"><span data-stu-id="1a466-247">OrderLineItemLinks</span></span>](order-resources.md#orderlineitemlinks) | <span data-ttu-id="1a466-248">Nem</span><span class="sxs-lookup"><span data-stu-id="1a466-248">No</span></span>       |  <span data-ttu-id="1a466-249">Csak olvasható.</span><span class="sxs-lookup"><span data-stu-id="1a466-249">Read-only.</span></span> <span data-ttu-id="1a466-250">Az Order sorelemnek megfelelő erőforrás-hivatkozások.</span><span class="sxs-lookup"><span data-stu-id="1a466-250">The resource links corresponding to the Order line item.</span></span>  |
| <span data-ttu-id="1a466-251">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="1a466-251">attributes</span></span>           | [<span data-ttu-id="1a466-252">ResourceAttributes (Erőforrás-attribútumok)</span><span class="sxs-lookup"><span data-stu-id="1a466-252">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="1a466-253">Nem</span><span class="sxs-lookup"><span data-stu-id="1a466-253">No</span></span>       | <span data-ttu-id="1a466-254">Az OrderLineItem elemnek megfelelő metaadat-attribútumok.</span><span class="sxs-lookup"><span data-stu-id="1a466-254">The metadata attributes corresponding to the OrderLineItem.</span></span> |
| <span data-ttu-id="1a466-255">renewsTo</span><span class="sxs-lookup"><span data-stu-id="1a466-255">renewsTo</span></span>             | <span data-ttu-id="1a466-256">Objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="1a466-256">Array of objects</span></span>                          | <span data-ttu-id="1a466-257">Nem</span><span class="sxs-lookup"><span data-stu-id="1a466-257">No</span></span>    |<span data-ttu-id="1a466-258">A [RenewsTo erőforrások tömbje.](order-resources.md#renewsto)</span><span class="sxs-lookup"><span data-stu-id="1a466-258">An array of [RenewsTo](order-resources.md#renewsto) resources.</span></span>                                                                            |

##### <a name="renewsto"></a><span data-ttu-id="1a466-259">RenewsTo</span><span class="sxs-lookup"><span data-stu-id="1a466-259">RenewsTo</span></span>

<span data-ttu-id="1a466-260">Ez a táblázat a [kérés törzsében található RenewsTo](order-resources.md#renewsto) tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="1a466-260">This table describes the [RenewsTo](order-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="1a466-261">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="1a466-261">Property</span></span>              | <span data-ttu-id="1a466-262">Típus</span><span class="sxs-lookup"><span data-stu-id="1a466-262">Type</span></span>             | <span data-ttu-id="1a466-263">Kötelező</span><span class="sxs-lookup"><span data-stu-id="1a466-263">Required</span></span>        | <span data-ttu-id="1a466-264">Leírás</span><span class="sxs-lookup"><span data-stu-id="1a466-264">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1a466-265">termDuration (kifejezés-lekértség)</span><span class="sxs-lookup"><span data-stu-id="1a466-265">termDuration</span></span>          | <span data-ttu-id="1a466-266">sztring</span><span class="sxs-lookup"><span data-stu-id="1a466-266">string</span></span>           | <span data-ttu-id="1a466-267">No</span><span class="sxs-lookup"><span data-stu-id="1a466-267">No</span></span>              | <span data-ttu-id="1a466-268">A megújítási időszak időtartamának ISO 8601-es ábrázolása.</span><span class="sxs-lookup"><span data-stu-id="1a466-268">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="1a466-269">A jelenleg támogatott értékek a **P1M (1** hónap) és **a P1Y (1** év).</span><span class="sxs-lookup"><span data-stu-id="1a466-269">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="1a466-270">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="1a466-270">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="1a466-271">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="1a466-271">REST response</span></span>

<span data-ttu-id="1a466-272">Ha a művelet sikeres, a metódus egy [Order](order-resources.md) erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="1a466-272">If successful, the method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1a466-273">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="1a466-273">Response success and error codes</span></span>

<span data-ttu-id="1a466-274">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="1a466-274">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1a466-275">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="1a466-275">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1a466-276">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1a466-276">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1a466-277">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="1a466-277">Response example</span></span>

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
