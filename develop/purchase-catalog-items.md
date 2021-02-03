---
title: Katalóguselemek vásárlása
description: Katalógus-elemek vásárlása a partner Center API használatával.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f2b3a34cdb6b29cb7eaaf5d977e4588f538fff09
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767796"
---
# <a name="purchase-catalog-items"></a><span data-ttu-id="ac0c9-103">Katalóguselemek vásárlása</span><span class="sxs-lookup"><span data-stu-id="ac0c9-103">Purchase catalog items</span></span>

<span data-ttu-id="ac0c9-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="ac0c9-104">**Applies To**</span></span>

- <span data-ttu-id="ac0c9-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="ac0c9-105">Partner Center</span></span>

<span data-ttu-id="ac0c9-106">A következő forgatókönyv bemutatja, hogyan vásárolhat elemeket a katalógusból a partner Center API használatával.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-106">The following scenario demonstrates the generic process for purchasing items from the catalog by using the Partner Center API.</span></span>

## <a name="discovery"></a><span data-ttu-id="ac0c9-107">Felderítés</span><span class="sxs-lookup"><span data-stu-id="ac0c9-107">Discovery</span></span>

<span data-ttu-id="ac0c9-108">Válassza ki a termékeket és az SKU-t, és tekintse meg a rendelkezésre állást a következő partner Center API-modellek használatával</span><span class="sxs-lookup"><span data-stu-id="ac0c9-108">Select products and SKUs and check their availability using the following Partner Center API models:</span></span>

- <span data-ttu-id="ac0c9-109">[Termék](product-resources.md#product) – a megvásárolható termékek vagy szolgáltatások csoportosítási konstrukciója.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-109">[Product](product-resources.md#product) - A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="ac0c9-110">Egy termék önmagában nem egy megvásárolható tétel.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-110">A product by itself isn't a purchasable item.</span></span>
- <span data-ttu-id="ac0c9-111">[SKU](product-resources.md#sku) – egy terméken belül megvásárolható készlet-tartási egység (SKU).</span><span class="sxs-lookup"><span data-stu-id="ac0c9-111">[SKU](product-resources.md#sku) - A purchasable Stock Keeping Unit (SKU) under a product.</span></span> <span data-ttu-id="ac0c9-112">Ezek a termék különböző alakzatait jelölik.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-112">These represent the different shapes of the product.</span></span>
- <span data-ttu-id="ac0c9-113">[Rendelkezésre állás](product-resources.md#availability) – olyan konfiguráció, amelyben az SKU megvásárolható (például ország, pénznem és iparági szegmens).</span><span class="sxs-lookup"><span data-stu-id="ac0c9-113">[Availability](product-resources.md#availability) - A configuration in which a SKU is available for purchase (such as country, currency and industry segment).</span></span>

<span data-ttu-id="ac0c9-114">Ha egy elemet szeretne megvásárolni a katalógusból, hajtsa végre a következő lépéseket:</span><span class="sxs-lookup"><span data-stu-id="ac0c9-114">To purchase an item from the catalog, complete the following steps:</span></span>

1. <span data-ttu-id="ac0c9-115">Azonosítsa és kérje le a megvásárolni kívánt terméket és SKU-t.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-115">Identify and retrieve the Product and SKU that you want to purchase.</span></span>

   - [<span data-ttu-id="ac0c9-116">Termékek listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="ac0c9-116">Get a list of products</span></span>](get-a-list-of-products.md)
   - [<span data-ttu-id="ac0c9-117">Termék beszerzése a termék AZONOSÍTÓjának használatával</span><span class="sxs-lookup"><span data-stu-id="ac0c9-117">Get a product using the product ID</span></span>](get-a-product-by-id.md)
   - [<span data-ttu-id="ac0c9-118">A termékhez tartozó SKU-termékek listájának beolvasása</span><span class="sxs-lookup"><span data-stu-id="ac0c9-118">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
   - [<span data-ttu-id="ac0c9-119">SKU beszerzése az SKU azonosító használatával</span><span class="sxs-lookup"><span data-stu-id="ac0c9-119">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

2. <span data-ttu-id="ac0c9-120">Egy SKU leltárának keresése.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-120">Check the inventory for a SKU.</span></span> <span data-ttu-id="ac0c9-121">Erre a lépésre csak olyan SKU-azonosítók esetében van szükség, amelyek **InventoryCheck** -értékkel vannak megjelölve a [purchasePrerequisites](product-resources.md#sku) tulajdonságban.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-121">This step is only needed for SKUs that are tagged with an **InventoryCheck** value in the [purchasePrerequisites](product-resources.md#sku) property.</span></span>

   - [<span data-ttu-id="ac0c9-122">Leltár ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="ac0c9-122">Check Inventory</span></span>](check-inventory.md)

3. <span data-ttu-id="ac0c9-123">Az [SKU](product-resources.md#sku) [rendelkezésre állásának](product-resources.md#availability) beolvasása.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-123">Retrieve the [availability](product-resources.md#availability) for the [SKU](product-resources.md#sku).</span></span> <span data-ttu-id="ac0c9-124">A megrendelés elhelyezésekor szüksége lesz a rendelkezésre állás **CatalogItemId** .</span><span class="sxs-lookup"><span data-stu-id="ac0c9-124">You will need the **CatalogItemId** of the availability when placing the order.</span></span> <span data-ttu-id="ac0c9-125">Az érték beszerzéséhez használja a következő API-k egyikét:</span><span class="sxs-lookup"><span data-stu-id="ac0c9-125">To get this value, use one of the following APIs:</span></span>

   - [<span data-ttu-id="ac0c9-126">Az SKU-ban lévő elérhetőségek listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="ac0c9-126">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
   - [<span data-ttu-id="ac0c9-127">Rendelkezésre állási azonosító használata</span><span class="sxs-lookup"><span data-stu-id="ac0c9-127">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="order-submission"></a><span data-ttu-id="ac0c9-128">Megrendelés beküldése</span><span class="sxs-lookup"><span data-stu-id="ac0c9-128">Order submission</span></span>

<span data-ttu-id="ac0c9-129">A katalógus-elemek sorrendjének elküldéséhez tegye a következőket:</span><span class="sxs-lookup"><span data-stu-id="ac0c9-129">To submit your catalog item order, do the following:</span></span>

1. <span data-ttu-id="ac0c9-130">Hozzon létre egy [cartot](cart-resources.md) a megvásárolni kívánt katalógus-elemek gyűjteményének tárolására.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-130">Create a [Cart](cart-resources.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="ac0c9-131">Amikor létrehoz egy kosarat, a rendszer automatikusan csoportosítja a [szekér elemeit](cart-resources.md#cartlineitem) attól függően, hogy mit vásárolhat együtt ugyanabban a [sorrendben](order-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ac0c9-131">When you create a cart, the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="ac0c9-132">Bevásárlókocsi létrehozása</span><span class="sxs-lookup"><span data-stu-id="ac0c9-132">Create a shopping cart</span></span>](create-a-cart.md)
   - [<span data-ttu-id="ac0c9-133">Bevásárlókocsi frissítése</span><span class="sxs-lookup"><span data-stu-id="ac0c9-133">Update a shopping cart</span></span>](update-a-cart.md)

2. <span data-ttu-id="ac0c9-134">Látogasson el a kosárba.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-134">Check out the cart.</span></span> <span data-ttu-id="ac0c9-135">A kosár megkeresése egy [megrendelés](order-resources.md)létrehozását eredményezi.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-135">Checking out a cart results in the creation of an [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="ac0c9-136">A kosár pénztárának kifizetése</span><span class="sxs-lookup"><span data-stu-id="ac0c9-136">Checkout the cart</span></span>](checkout-a-cart.md)

## <a name="get-order-details"></a><span data-ttu-id="ac0c9-137">Megrendelés részleteinek beolvasása</span><span class="sxs-lookup"><span data-stu-id="ac0c9-137">Get order details</span></span>

<span data-ttu-id="ac0c9-138">Egy adott megrendelés részleteit a megrendelés AZONOSÍTÓjának használatával kérheti le, vagy megtekintheti az ügyfél rendeléseinek listáját.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-138">You can retrieve the details of an individual order using the order ID, or get a list of orders for a customer.</span></span> <span data-ttu-id="ac0c9-139">A megrendelés elküldése és az ügyfél rendeléseinek listájában akár 15 percet is igénybe vehet.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-139">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a list of a customer's orders.</span></span>

- <span data-ttu-id="ac0c9-140">Tekintse meg az [Order by id beszerzése](get-an-order-by-id.md) című témakört, amely a sorrendi azonosítók használatával beolvassa egy adott megrendelés részleteit.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-140">See [Get an order by ID](get-an-order-by-id.md) to get the details of an individual order using the order IDs.</span></span>

- <span data-ttu-id="ac0c9-141">Az ügyfél-AZONOSÍTÓval rendelkező ügyfél rendeléseinek megtekintéséhez tekintse [meg az ügyfelek rendeléseinek lekérése](get-all-of-a-customer-s-orders.md) című témakört.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-141">See [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) to get a list of orders for a customer using the customer ID.</span></span>

- <span data-ttu-id="ac0c9-142">Tekintse meg az [ügyfelek és a számlázási ciklusok listájának lekérése](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) lehetőséget, hogy lekérje az ügyfél által a [számlázási ciklus típusa](product-resources.md#billingcycletype) alapján megrendelt megrendelések listáját, amely lehetővé teszi, hogy a katalógusbeli elemek rendeléseit (egyszeri díj) és az éves vagy havi számlázott rendeléseket külön adja meg.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-142">See [Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) to get a list of orders for a customer by [billing cycle type](product-resources.md#billingcycletype) allowing you to list catalog item orders (one-time charges) and annual or monthly billed orders separately.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="ac0c9-143">Életciklus-kezelés</span><span class="sxs-lookup"><span data-stu-id="ac0c9-143">Lifecycle management</span></span>

<span data-ttu-id="ac0c9-144">A katalógus elemeinek életciklusa kezelésének részeként a partner Centerben lekérheti a katalógus-elemek [jogosultságait](entitlement-resources.md), és lekérheti a foglalás részleteit a foglalási rendelés azonosítójának használatával.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-144">As part of managing the lifecycle of your catalog items in Partner Center, you can retrieve information about your catalog item [Entitlements](entitlement-resources.md), and get reservation details using the reservation order ID.</span></span> <span data-ttu-id="ac0c9-145">Ennek módjáról a [jogosultságok beszerzése](get-a-collection-of-entitlements.md)című témakörben talál példákat.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-145">For examples of how to do this, see [Get entitlements](get-a-collection-of-entitlements.md).</span></span>   

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="ac0c9-146">Számlázás és egyeztetés</span><span class="sxs-lookup"><span data-stu-id="ac0c9-146">Invoice and reconciliation</span></span>

<span data-ttu-id="ac0c9-147">A következő forgatókönyvek azt mutatják be, hogyan lehet programozott módon megtekinteni az ügyfél [számláit](invoice-resources.md), és beolvasni a fiók egyenlegeit és összegzéseit, amelyek tartalmazzák a katalógus-elemek egyszeri díját.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-147">The following scenarios show you how to programmatically view your customer's [invoices](invoice-resources.md), and get your account balances and summaries that include one-time charges for catalog items.</span></span>

### <a name="balance-and-payment"></a><span data-ttu-id="ac0c9-148">Egyenleg és fizetés</span><span class="sxs-lookup"><span data-stu-id="ac0c9-148">Balance and payment</span></span>

<span data-ttu-id="ac0c9-149">Az aktuális fiók egyenlegének alapértelmezett pénznemben való lekéréséhez, amely az ismétlődő és egyszeri (katalógus-) díjak egyenlege, lásd: [az aktuális fiók egyenlegének beolvasása](get-the-reseller-s-current-account-balance.md).</span><span class="sxs-lookup"><span data-stu-id="ac0c9-149">To get current account balance in your default currency type that is a balance of both recurring and one-time (catalog item) charges, see [Get your current account balance](get-the-reseller-s-current-account-balance.md).</span></span>

### <a name="multi-currency-balance-and-payment"></a><span data-ttu-id="ac0c9-150">Több pénznemre kiterjedő egyenleg és fizetés</span><span class="sxs-lookup"><span data-stu-id="ac0c9-150">Multi-currency balance and payment</span></span>

<span data-ttu-id="ac0c9-151">Az aktuális fiók egyenlegének beszerzéséhez, valamint a számla összegzésének összefoglalásához, amely tartalmazza az egyes ügyfelek pénznem-típusaira vonatkozó ismétlődő és egyszeri díjat is, tekintse meg a [számla összegzésének beolvasása](get-invoice-summaries.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-151">To get your current account balance and a collection of invoice summaries containing an invoice summary with both recurring and one-time charges for each of your customer's currency types, see [Get invoice summaries](get-invoice-summaries.md).</span></span>

### <a name="invoices"></a><span data-ttu-id="ac0c9-152">Számlák</span><span class="sxs-lookup"><span data-stu-id="ac0c9-152">Invoices</span></span>

<span data-ttu-id="ac0c9-153">Az ismétlődő és egyszeri díjat is tartalmazó számlák gyűjteményének beszerzéséhez tekintse meg a következő témakört: [számlák gyűjteményének beolvasása](get-a-collection-of-invoices.md).</span><span class="sxs-lookup"><span data-stu-id="ac0c9-153">To get a collection of invoices that show both recurring and one-time charges, see [Get a collection of invoices](get-a-collection-of-invoices.md).</span></span> 

### <a name="single-invoice"></a><span data-ttu-id="ac0c9-154">Egyetlen számla</span><span class="sxs-lookup"><span data-stu-id="ac0c9-154">Single Invoice</span></span>

<span data-ttu-id="ac0c9-155">Ha a számla AZONOSÍTÓjának használatával szeretne beolvasni egy adott számlát, tekintse meg a [számla beszerzése azonosító alapján](get-invoice-by-id.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-155">To retrieve a specific invoice using the invoice ID, see [Get an invoice by ID](get-invoice-by-id.md).</span></span>  

### <a name="reconciliation"></a><span data-ttu-id="ac0c9-156">Licencegyeztetési</span><span class="sxs-lookup"><span data-stu-id="ac0c9-156">Reconciliation</span></span>

<span data-ttu-id="ac0c9-157">A számlasor-elemek részleteinek (egyeztetési sorok) egy adott AZONOSÍTÓhoz tartozó gyűjteményének lekéréséhez tekintse meg a [Számlázási sorok beolvasása](get-invoiceline-items.md)című cikket.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-157">To get a collection of invoice line item details (Reconciliation line items) for a specific invoice ID, see [Get invoice line items](get-invoiceline-items.md).</span></span>  

### <a name="download-an-invoice-as-a-pdf"></a><span data-ttu-id="ac0c9-158">Számla letöltése PDF-ként</span><span class="sxs-lookup"><span data-stu-id="ac0c9-158">Download an invoice as a PDF</span></span>

<span data-ttu-id="ac0c9-159">Ha a számla AZONOSÍTÓjának használatával szeretne beolvasni egy számlafogadó-utasítást a PDF-űrlapon, olvassa el a [Számlakivonat beolvasása](get-invoice-statement.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="ac0c9-159">To retrieve an invoice statement in PDF form using an invoice ID, see [Get an invoice statement](get-invoice-statement.md).</span></span>
