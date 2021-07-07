---
title: Katalóguselemek vásárlása
description: Katalóguselemek vásárlása a Partnerközpont API-val.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d3e0deedff194b1c836d9266c2201a2b3a52cc1b
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445357"
---
# <a name="purchase-catalog-items"></a><span data-ttu-id="fcfca-103">Katalóguselemek vásárlása</span><span class="sxs-lookup"><span data-stu-id="fcfca-103">Purchase catalog items</span></span>

<span data-ttu-id="fcfca-104">A következő forgatókönyv azt az általános folyamatot mutatja be, amikor a katalógusból vásárolnak elemeket a Partnerközpont API-val.</span><span class="sxs-lookup"><span data-stu-id="fcfca-104">The following scenario demonstrates the generic process for purchasing items from the catalog by using the Partner Center API.</span></span>

## <a name="discovery"></a><span data-ttu-id="fcfca-105">Felderítés</span><span class="sxs-lookup"><span data-stu-id="fcfca-105">Discovery</span></span>

<span data-ttu-id="fcfca-106">Válassza a termékek és a termékkódok (SKUs) lehetőséget, és ellenőrizze azok rendelkezésre állását az alábbi Partnerközpont API-modellekkel:</span><span class="sxs-lookup"><span data-stu-id="fcfca-106">Select products and Stock Keeping Units (SKUs) and check their availability using the following Partner Center API models:</span></span>

- <span data-ttu-id="fcfca-107">[Termék](product-resources.md#product) – Egy csoportosítási szerkezet a cserélhető termékekhez vagy szolgáltatásokhoz.</span><span class="sxs-lookup"><span data-stu-id="fcfca-107">[Product](product-resources.md#product) - A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="fcfca-108">A termék önmagában nem cserélhető elem.</span><span class="sxs-lookup"><span data-stu-id="fcfca-108">A product by itself isn't a purchasable item.</span></span>
- <span data-ttu-id="fcfca-109">[Termékváltozat](product-resources.md#sku) – Egy terméken átvehető termékváltozat.</span><span class="sxs-lookup"><span data-stu-id="fcfca-109">[SKU](product-resources.md#sku) - A purchasable SKU under a product.</span></span> <span data-ttu-id="fcfca-110">Ezek a termék különböző alakjai.</span><span class="sxs-lookup"><span data-stu-id="fcfca-110">These represent the different shapes of the product.</span></span>
- <span data-ttu-id="fcfca-111">[Rendelkezésre állás](product-resources.md#availability) – Olyan konfiguráció, amelyben egy termékváltozat megvásárolható (például ország, pénznem és iparági szegmens).</span><span class="sxs-lookup"><span data-stu-id="fcfca-111">[Availability](product-resources.md#availability) - A configuration in which a SKU is available for purchase (such as country, currency, and industry segment).</span></span>

<span data-ttu-id="fcfca-112">Ha egy elemet meg kell vásárolnia a katalógusból, kövesse az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="fcfca-112">To purchase an item from the catalog, complete the following steps:</span></span>

1. <span data-ttu-id="fcfca-113">Azonosítsa és lekéri a megvásárolni kívánt terméket és termékváltozatot.</span><span class="sxs-lookup"><span data-stu-id="fcfca-113">Identify and retrieve the Product and SKU that you want to purchase.</span></span>

   - [<span data-ttu-id="fcfca-114">Termékek listájának lekért listája</span><span class="sxs-lookup"><span data-stu-id="fcfca-114">Get a list of products</span></span>](get-a-list-of-products.md)
   - [<span data-ttu-id="fcfca-115">Termék lekérte a termékazonosítót</span><span class="sxs-lookup"><span data-stu-id="fcfca-115">Get a product using the product ID</span></span>](get-a-product-by-id.md)
   - [<span data-ttu-id="fcfca-116">Termék termékkel kapcsolatos termékkódok listájának lekért listája</span><span class="sxs-lookup"><span data-stu-id="fcfca-116">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
   - [<span data-ttu-id="fcfca-117">Termékváltozat lekérte a termékváltozat azonosítójával</span><span class="sxs-lookup"><span data-stu-id="fcfca-117">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

2. <span data-ttu-id="fcfca-118">Ellenőrizze a leltárban, hogy van-e termékváltozat.</span><span class="sxs-lookup"><span data-stu-id="fcfca-118">Check the inventory for a SKU.</span></span> <span data-ttu-id="fcfca-119">Erre a lépésre csak az **InventoryCheck** értékkel felcímkézett termékkódok esetén van szükség a [purchasePrerequisites tulajdonságban.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="fcfca-119">This step is only needed for SKUs that are tagged with an **InventoryCheck** value in the [purchasePrerequisites](product-resources.md#sku) property.</span></span>

   - [<span data-ttu-id="fcfca-120">Leltár ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="fcfca-120">Check Inventory</span></span>](check-inventory.md)

3. <span data-ttu-id="fcfca-121">A [termékváltozat rendelkezésre](product-resources.md#availability) [állásának lekérése.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="fcfca-121">Retrieve the [availability](product-resources.md#availability) for the [SKU](product-resources.md#sku).</span></span> <span data-ttu-id="fcfca-122">A rendelés leadáskor szüksége lesz a rendelkezésre állás **CatalogItemId-ére.**</span><span class="sxs-lookup"><span data-stu-id="fcfca-122">You will need the **CatalogItemId** of the availability when placing the order.</span></span> <span data-ttu-id="fcfca-123">Ezt az értéket a következő API-k egyikével használhatja:</span><span class="sxs-lookup"><span data-stu-id="fcfca-123">To get this value, use one of the following APIs:</span></span>

   - [<span data-ttu-id="fcfca-124">Termékváltozatok rendelkezésre állási listájának lekért listája</span><span class="sxs-lookup"><span data-stu-id="fcfca-124">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
   - [<span data-ttu-id="fcfca-125">Rendelkezésre állás le szolgáltatása a rendelkezésre állási azonosítóval</span><span class="sxs-lookup"><span data-stu-id="fcfca-125">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="order-submission"></a><span data-ttu-id="fcfca-126">Rendelés beküldve</span><span class="sxs-lookup"><span data-stu-id="fcfca-126">Order submission</span></span>

<span data-ttu-id="fcfca-127">A katalóguselem-rendelés elküldhez tegye a következőket:</span><span class="sxs-lookup"><span data-stu-id="fcfca-127">To submit your catalog item order, do the following:</span></span>

1. <span data-ttu-id="fcfca-128">Hozzon létre [egy](cart-resources.md) kosárt, amely a megvásárolni kívánt katalóguselemek gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="fcfca-128">Create a [Cart](cart-resources.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="fcfca-129">Amikor kosarat hoz [](cart-resources.md#cartlineitem) létre, a rendszer automatikusan csoportosítja a kosársor elemeit az alapján, hogy mi vásárolható együtt ugyanabban a [rendelésben.](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="fcfca-129">When you create a cart, the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="fcfca-130">Bevásárlókocsi létrehozása</span><span class="sxs-lookup"><span data-stu-id="fcfca-130">Create a shopping cart</span></span>](create-a-cart.md)
   - [<span data-ttu-id="fcfca-131">Bevásárlókocsi frissítése</span><span class="sxs-lookup"><span data-stu-id="fcfca-131">Update a shopping cart</span></span>](update-a-cart.md)

2. <span data-ttu-id="fcfca-132">Nézze meg a kosárt.</span><span class="sxs-lookup"><span data-stu-id="fcfca-132">Check out the cart.</span></span> <span data-ttu-id="fcfca-133">Ha kiveszi a kosárból a rendelést, a rendelés is [létre lesz hozva.](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="fcfca-133">Checking out a cart results in the creation of an [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="fcfca-134">A kosár kiveszi a kosárból</span><span class="sxs-lookup"><span data-stu-id="fcfca-134">Checkout the cart</span></span>](checkout-a-cart.md)

## <a name="get-order-details"></a><span data-ttu-id="fcfca-135">Megrendelés részleteinek lekérte</span><span class="sxs-lookup"><span data-stu-id="fcfca-135">Get order details</span></span>

<span data-ttu-id="fcfca-136">Lekérheti egy adott rendelés részleteit a rendelés azonosítójával, vagy lekérheti egy ügyfél megrendelési listáját.</span><span class="sxs-lookup"><span data-stu-id="fcfca-136">You can retrieve the details of an individual order using the order ID, or get a list of orders for a customer.</span></span> <span data-ttu-id="fcfca-137">A rendelés elküldés és az ügyfél rendelési listájában való megjelenése között akár 15 perces késés is lehet.</span><span class="sxs-lookup"><span data-stu-id="fcfca-137">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a list of a customer's orders.</span></span>

- <span data-ttu-id="fcfca-138">A [rendelésazonosítók használatával](get-an-order-by-id.md) az egyes rendelésekkel kapcsolatos részletekért lásd: Rendelés lekért azonosítója.</span><span class="sxs-lookup"><span data-stu-id="fcfca-138">See [Get an order by ID](get-an-order-by-id.md) to get the details of an individual order using the order IDs.</span></span>

- <span data-ttu-id="fcfca-139">Az [ügyfélazonosítót](get-all-of-a-customer-s-orders.md) használó ügyfél megrendelési listájának lekért listájáért lásd az ügyfél összes rendelésének lekért listáját.</span><span class="sxs-lookup"><span data-stu-id="fcfca-139">See [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) to get a list of orders for a customer using the customer ID.</span></span>

- <span data-ttu-id="fcfca-140">A [rendelések ügyfél-](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) és számlázásiciklus-típusonkénti listájának lekért [](product-resources.md#billingcycletype) listája az ügyfélhez tartozó számlázási ciklus típusa szerint, amely lehetővé teszi a katalóguselem-rendelések (egyszeres díjak) és az éves vagy havi számlázt rendelések külön-külön való felsorolását.</span><span class="sxs-lookup"><span data-stu-id="fcfca-140">See [Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) to get a list of orders for a customer by [billing cycle type](product-resources.md#billingcycletype) allowing you to list catalog item orders (one-time charges) and annual or monthly billed orders separately.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="fcfca-141">Életciklus-kezelés</span><span class="sxs-lookup"><span data-stu-id="fcfca-141">Lifecycle management</span></span>

<span data-ttu-id="fcfca-142">A katalóguselemek életciklusának a Partnerközpont-ban való kezelésének részeként lekérheti a [](entitlement-resources.md)katalóguselem jogosultságai adatait, és lekérheti a foglalás részleteit a foglalási rendelés azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="fcfca-142">As part of managing the lifecycle of your catalog items in Partner Center, you can retrieve information about your catalog item [Entitlements](entitlement-resources.md), and get reservation details using the reservation order ID.</span></span> <span data-ttu-id="fcfca-143">Ennek mikéntjére vonatkozó példákért lásd: [Get entitlements (Jogosultságok lekérte).](get-a-collection-of-entitlements.md)</span><span class="sxs-lookup"><span data-stu-id="fcfca-143">For examples of how to do this, see [Get entitlements](get-a-collection-of-entitlements.md).</span></span>   

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="fcfca-144">Számla és egyeztetés</span><span class="sxs-lookup"><span data-stu-id="fcfca-144">Invoice and reconciliation</span></span>

<span data-ttu-id="fcfca-145">A következő forgatókönyvek azt mutatják be, hogyan [](invoice-resources.md)lehet programozott módon megtekinteni az ügyfél számláit, és hogyan lehet lekérte a fiókegyenlegeket és összegzéseket, amelyek a katalóguselemekre vonatkozó egyszeres díjakat tartalmaznak.</span><span class="sxs-lookup"><span data-stu-id="fcfca-145">The following scenarios show you how to programmatically view your customer's [invoices](invoice-resources.md), and get your account balances and summaries that include one-time charges for catalog items.</span></span>

### <a name="balance-and-payment"></a><span data-ttu-id="fcfca-146">Egyenleg és kifizetés</span><span class="sxs-lookup"><span data-stu-id="fcfca-146">Balance and payment</span></span>

<span data-ttu-id="fcfca-147">Az aktuális számlaegyenleg az ismétlődő és egyszeri (katalóguselem) díjak egyenlegét is elegyenő alapértelmezett pénznemben való lekértért lásd: Az aktuális számlaegyenleg [lekért egyenlege.](get-the-reseller-s-current-account-balance.md)</span><span class="sxs-lookup"><span data-stu-id="fcfca-147">To get current account balance in your default currency type that is a balance of both recurring and one-time (catalog item) charges, see [Get your current account balance](get-the-reseller-s-current-account-balance.md).</span></span>

### <a name="multi-currency-balance-and-payment"></a><span data-ttu-id="fcfca-148">Több pénznem egyenlege és kifizetése</span><span class="sxs-lookup"><span data-stu-id="fcfca-148">Multi-currency balance and payment</span></span>

<span data-ttu-id="fcfca-149">Az aktuális számlaegyenleg és a számlaösszegzéseket tartalmazó számlaösszegzések ismétlődő és egyszeri díjakat tartalmazó gyűjteményét az egyes ügyfelek pénznemtípusával kapcsolatos ismétlődő és egyszeri díjakkal együtt lásd: Számlaösszegzések [lekérte.](get-invoice-summaries.md)</span><span class="sxs-lookup"><span data-stu-id="fcfca-149">To get your current account balance and a collection of invoice summaries containing an invoice summary with both recurring and one-time charges for each of your customer's currency types, see [Get invoice summaries](get-invoice-summaries.md).</span></span>

### <a name="invoices"></a><span data-ttu-id="fcfca-150">Számlák</span><span class="sxs-lookup"><span data-stu-id="fcfca-150">Invoices</span></span>

<span data-ttu-id="fcfca-151">Az ismétlődő és egyszeri díjakat is bemutató számlák gyűjteményének legyűjtéséhez [lásd: Számlák gyűjteményének begyűjtése.](get-a-collection-of-invoices.md)</span><span class="sxs-lookup"><span data-stu-id="fcfca-151">To get a collection of invoices that show both recurring and one-time charges, see [Get a collection of invoices](get-a-collection-of-invoices.md).</span></span> 

### <a name="single-invoice"></a><span data-ttu-id="fcfca-152">Egyetlen számla</span><span class="sxs-lookup"><span data-stu-id="fcfca-152">Single Invoice</span></span>

<span data-ttu-id="fcfca-153">Egy adott számla számlaazonosítóval való lekérését lásd: [Számla lekérése azonosító alapján.](get-invoice-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="fcfca-153">To retrieve a specific invoice using the invoice ID, see [Get an invoice by ID](get-invoice-by-id.md).</span></span>  

### <a name="reconciliation"></a><span data-ttu-id="fcfca-154">Egyeztetés</span><span class="sxs-lookup"><span data-stu-id="fcfca-154">Reconciliation</span></span>

<span data-ttu-id="fcfca-155">Egy adott számlaazonosító számlasorelem-részleteinek (egyeztetési sorelemek) gyűjteményét lásd: [Számlasorelemek begyűjtése.](get-invoiceline-items.md)</span><span class="sxs-lookup"><span data-stu-id="fcfca-155">To get a collection of invoice line item details (Reconciliation line items) for a specific invoice ID, see [Get invoice line items](get-invoiceline-items.md).</span></span>  

### <a name="download-an-invoice-as-a-pdf"></a><span data-ttu-id="fcfca-156">Számla letöltése PDF-fájlként</span><span class="sxs-lookup"><span data-stu-id="fcfca-156">Download an invoice as a PDF</span></span>

<span data-ttu-id="fcfca-157">A számlakivonat PDF formátumban, számlaazonosítóval való lekéréséhez lásd: [Számlakivonat lekérése.](get-invoice-statement.md)</span><span class="sxs-lookup"><span data-stu-id="fcfca-157">To retrieve an invoice statement in PDF form using an invoice ID, see [Get an invoice statement](get-invoice-statement.md).</span></span>
