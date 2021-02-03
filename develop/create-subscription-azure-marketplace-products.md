---
title: Előfizetés létrehozása kereskedelmi Piactéri termékekhez
description: A fejlesztők a partner Center API-k használatával hozhatnak létre és kezelhetnek előfizetéseket kereskedelmi Piactéri termékekhez.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df2a3707e00ba36a11c404b102304c08d105244e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767748"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a><span data-ttu-id="bf43d-103">Előfizetés létrehozása kereskedelmi Piactéri termékekhez</span><span class="sxs-lookup"><span data-stu-id="bf43d-103">Create a subscription for commercial marketplace products</span></span>

<span data-ttu-id="bf43d-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="bf43d-104">**Applies to:**</span></span>

* <span data-ttu-id="bf43d-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="bf43d-105">Partner Center</span></span>

<span data-ttu-id="bf43d-106">A partner Center API-k használatával előfizetést hozhat létre kereskedelmi piactér-termékekhez.</span><span class="sxs-lookup"><span data-stu-id="bf43d-106">You can create a subscription for commercial marketplace products using Partner Center APIs.</span></span> <span data-ttu-id="bf43d-107">Meg kell [kapnia a piac ajánlatait](#get-a-list-of-offers-for-a-market), létre kell [hoznia és el kell küldenie](#create-and-submit-an-order) egy kereskedelmi piactér-előfizetés rendelését, majd be kell szereznie egy [aktiválási hivatkozást](#get-activation-link).</span><span class="sxs-lookup"><span data-stu-id="bf43d-107">You must [get a list of offers for a market](#get-a-list-of-offers-for-a-market), [create and submit an order](#create-and-submit-an-order) for a commercial marketplace subscription, then [retrieve an activation link](#get-activation-link).</span></span>

<span data-ttu-id="bf43d-108">Az előfizetések esetében is [elvégezheti az életciklus-kezelést](#lifecycle-management) és a [számlák kezelését](#invoice-and-reconciliation) .</span><span class="sxs-lookup"><span data-stu-id="bf43d-108">You can also [perform lifecycle management](#lifecycle-management) and [manage invoices](#invoice-and-reconciliation) for these subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf43d-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="bf43d-109">Prerequisites</span></span>

* <span data-ttu-id="bf43d-110">A [partner központ hitelesítési](partner-center-authentication.md) hitelesítő adatai.</span><span class="sxs-lookup"><span data-stu-id="bf43d-110">[Partner Center authentication](partner-center-authentication.md) credentials.</span></span> <span data-ttu-id="bf43d-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="bf43d-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>
* <span data-ttu-id="bf43d-112">Az ügyfél-azonosító.</span><span class="sxs-lookup"><span data-stu-id="bf43d-112">The customer identifier.</span></span> <span data-ttu-id="bf43d-113">Ha nem rendelkezik ügyfél-azonosítóval, kövesse az [ügyfelek listájának beolvasása](get-a-list-of-customers.md)című témakör lépéseit.</span><span class="sxs-lookup"><span data-stu-id="bf43d-113">If you don't have a customer's identifier, follow the steps in [Get a list of customers](get-a-list-of-customers.md).</span></span> <span data-ttu-id="bf43d-114">Másik lehetőségként jelentkezzen be a partner Centerbe, válassza ki az ügyfelet az ügyfelek listájáról, válassza a **fiók** lehetőséget, majd mentse a **Microsoft-azonosítóját**.</span><span class="sxs-lookup"><span data-stu-id="bf43d-114">Alternatively, sign in to Partner Center, choose the customer from the list of customers, select **Account**, then save their **Microsoft ID**.</span></span>

## <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="bf43d-115">Egy piac ajánlati listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="bf43d-115">Get a list of offers for a market</span></span>

<span data-ttu-id="bf43d-116">A piacon elérhető ajánlatokat a következő partner Center API-modellek segítségével tekintheti meg:</span><span class="sxs-lookup"><span data-stu-id="bf43d-116">You can check the available offers for a market using the following Partner Center API models:</span></span>

* <span data-ttu-id="bf43d-117">**[Termék](product-resources.md#product)**: csoportosítható szerkezet a megvásárolható termékekhez vagy szolgáltatásokhoz.</span><span class="sxs-lookup"><span data-stu-id="bf43d-117">**[Product](product-resources.md#product)**: A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="bf43d-118">Egy termék nem egy megvásárolható tétel.</span><span class="sxs-lookup"><span data-stu-id="bf43d-118">A product itself isn't a purchasable item.</span></span>
* <span data-ttu-id="bf43d-119">**[SKU](product-resources.md#sku)**: egy terméken belül megvásárolható készlet-megőrzési egység (SKU).</span><span class="sxs-lookup"><span data-stu-id="bf43d-119">**[SKU](product-resources.md#sku)**: A purchasable Stock Keeping Unit (SKU) under a product.</span></span> <span data-ttu-id="bf43d-120">Ezek a termék különböző alakzatait jelölik.</span><span class="sxs-lookup"><span data-stu-id="bf43d-120">These represent the different shapes of the product.</span></span>
* <span data-ttu-id="bf43d-121">**[Rendelkezésre állás](product-resources.md#availability)**: olyan konfiguráció, amelyben az SKU megvásárolható (például ország, pénznem vagy iparági szegmens).</span><span class="sxs-lookup"><span data-stu-id="bf43d-121">**[Availability](product-resources.md#availability)**: A configuration in which a SKU is available for purchase (such as country, currency, or industry segment).</span></span>

<span data-ttu-id="bf43d-122">Az Azure-foglalás megvásárlása előtt végezze el a következő lépéseket:</span><span class="sxs-lookup"><span data-stu-id="bf43d-122">Before you purchase an Azure reservation, complete the following steps:</span></span>

1. <span data-ttu-id="bf43d-123">Azonosítsa és kérje le a megvásárolni kívánt terméket és SKU-t.</span><span class="sxs-lookup"><span data-stu-id="bf43d-123">Identify and retrieve the product and SKU that you want to purchase.</span></span> <span data-ttu-id="bf43d-124">Ha már ismeri a termék AZONOSÍTÓját és az SKU AZONOSÍTÓját, válassza ki őket.</span><span class="sxs-lookup"><span data-stu-id="bf43d-124">If you already know the Product ID and SKU ID, select them.</span></span>

    * [<span data-ttu-id="bf43d-125">Termékek listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="bf43d-125">Get a list of products</span></span>](get-a-list-of-products.md)
    * [<span data-ttu-id="bf43d-126">Termék beszerzése a termék AZONOSÍTÓjának használatával</span><span class="sxs-lookup"><span data-stu-id="bf43d-126">Get a product using the product ID</span></span>](get-a-product-by-id.md)
    * [<span data-ttu-id="bf43d-127">A termékhez tartozó SKU-termékek listájának beolvasása</span><span class="sxs-lookup"><span data-stu-id="bf43d-127">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
    * [<span data-ttu-id="bf43d-128">SKU beszerzése az SKU azonosító használatával</span><span class="sxs-lookup"><span data-stu-id="bf43d-128">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

    > [!NOTE]
    > <span data-ttu-id="bf43d-129">Az **"Azure"** **ProductType** -tulajdonsága és a **"Saas"** **altípus** -tulajdonsága alapján azonosíthatók a kereskedelmi piactéren elérhető termékek.</span><span class="sxs-lookup"><span data-stu-id="bf43d-129">You can identify commercial marketplace products by their **ProductType** property of **"Azure"** and their **SubType** property of **"SaaS"**.</span></span>

2. <span data-ttu-id="bf43d-130">Ha az SKU- **InventoryCheck** előfeltételként van megjelölve, [ellenőrizze az SKU leltárát](check-inventory.md).</span><span class="sxs-lookup"><span data-stu-id="bf43d-130">If the SKUs are tagged with an **InventoryCheck** prerequisite, [check the inventory for a SKU](check-inventory.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="bf43d-131">Jelenleg nincs olyan kereskedelmi piactér-termék, amely támogatja a leltár-ellenőrzés használatát, vagy **InventoryCheck** előfeltételként van megjelölve.</span><span class="sxs-lookup"><span data-stu-id="bf43d-131">At this time, there are no commercial marketplace products that support inventory check or are tagged with an **InventoryCheck** prerequisite.</span></span>

3. <span data-ttu-id="bf43d-132">Az SKU rendelkezésre állásának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="bf43d-132">Retrieve the availability for the SKU.</span></span> <span data-ttu-id="bf43d-133">A megrendelés elhelyezésekor szüksége lesz a rendelkezésre állás **CatalogItemId** , amelyet a következő API-kkal kérhet le:</span><span class="sxs-lookup"><span data-stu-id="bf43d-133">You will need the **CatalogItemId** of the availability when placing the order, which you can retrieve through the following APIs:</span></span>

    * [<span data-ttu-id="bf43d-134">Az SKU-ban lévő elérhetőségek listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="bf43d-134">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
    * [<span data-ttu-id="bf43d-135">Rendelkezésre állási azonosító használata</span><span class="sxs-lookup"><span data-stu-id="bf43d-135">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a><span data-ttu-id="bf43d-136">Megrendelés létrehozása és elküldése</span><span class="sxs-lookup"><span data-stu-id="bf43d-136">Create and submit an order</span></span>

<span data-ttu-id="bf43d-137">Az Azure foglalási sorrendjének elküldéséhez kövesse az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="bf43d-137">To submit your Azure reservation order, follow these steps:</span></span>

1. <span data-ttu-id="bf43d-138">[Hozzon létre egy cartot](create-a-cart.md) a megvásárolni kívánt katalógus-elemek gyűjteményének tárolására.</span><span class="sxs-lookup"><span data-stu-id="bf43d-138">[Create a cart](create-a-cart.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="bf43d-139">Amikor létrehoz egy [kosarat](cart-resources.md#cart), a rendszer automatikusan csoportosítja a [szekér elemeit](cart-resources.md#cartlineitem) attól függően, hogy mit vásárolhat együtt ugyanabban a [sorrendben](order-resources.md#order).</span><span class="sxs-lookup"><span data-stu-id="bf43d-139">When you create a [cart](cart-resources.md#cart), the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [order](order-resources.md#order).</span></span> <span data-ttu-id="bf43d-140">( [A kosár frissítését](update-a-cart.md)is végezheti.)</span><span class="sxs-lookup"><span data-stu-id="bf43d-140">(You can also [update a cart](update-a-cart.md).)</span></span>
2. <span data-ttu-id="bf43d-141">[Tekintse meg a kosárt](checkout-a-cart.md), amely egy [megrendelés](order-resources.md#order)létrehozását eredményezi.</span><span class="sxs-lookup"><span data-stu-id="bf43d-141">[Check out the cart](checkout-a-cart.md), which results in the creation of an [order](order-resources.md#order).</span></span>

### <a name="get-order-details"></a><span data-ttu-id="bf43d-142">Megrendelés részleteinek beolvasása</span><span class="sxs-lookup"><span data-stu-id="bf43d-142">Get order details</span></span>

<span data-ttu-id="bf43d-143">[Egy adott megrendelés részleteit a megrendelés azonosítójának használatával](get-an-order-by-id.md)kérheti le.</span><span class="sxs-lookup"><span data-stu-id="bf43d-143">You can [retrieve the details of an individual order using the order ID](get-an-order-by-id.md).</span></span> <span data-ttu-id="bf43d-144">Egy [adott ügyfélhez tartozó összes megrendelés listáját](get-all-of-a-customer-s-orders.md)is lekérheti.</span><span class="sxs-lookup"><span data-stu-id="bf43d-144">You can also [retrieve a list of all orders for a specific customer](get-all-of-a-customer-s-orders.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bf43d-145">Egy megrendelés elküldése után akár 15 percet is igénybe vehet, mielőtt a megrendelés megjelenik az ügyfél rendelési listájában.</span><span class="sxs-lookup"><span data-stu-id="bf43d-145">After an order is submitted, there is a delay of up to 15 minutes before the order appears in that customer's order list.</span></span>

## <a name="get-activation-link"></a><span data-ttu-id="bf43d-146">Aktiválási hivatkozás beolvasása</span><span class="sxs-lookup"><span data-stu-id="bf43d-146">Get activation link</span></span>

<span data-ttu-id="bf43d-147">A partnernek vagy az ügyfélnek aktiválnia kell az Azure Marketplace-termékek előfizetéseit.</span><span class="sxs-lookup"><span data-stu-id="bf43d-147">The partner or customer must activate subscriptions to Azure Marketplace products.</span></span> <span data-ttu-id="bf43d-148">[Az aktiválási hivatkozást megrendelési sor elem alapján](get-activation-link-by-order-line-item.md)kérheti le.</span><span class="sxs-lookup"><span data-stu-id="bf43d-148">You can [get an activation link by order line item](get-activation-link-by-order-line-item.md).</span></span> <span data-ttu-id="bf43d-149">Az [előfizetést azonosító alapján](get-a-subscription-by-id.md)is lekérheti, majd a **hivatkozások** tulajdonság enumerálásával létrehozhatja az aktiválási hivatkozást.</span><span class="sxs-lookup"><span data-stu-id="bf43d-149">You can also [get a subscription by ID](get-a-subscription-by-id.md), then enumerate its **Links** property to create an activation link.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="bf43d-150">Életciklus-kezelés</span><span class="sxs-lookup"><span data-stu-id="bf43d-150">Lifecycle management</span></span>

<span data-ttu-id="bf43d-151">Az előfizetések életciklusát a kereskedelmi piactér termékeire a következő módszerekkel kezelheti:</span><span class="sxs-lookup"><span data-stu-id="bf43d-151">You can manage the lifecycle of your subscriptions to commercial marketplace products using the following methods:</span></span>

* [<span data-ttu-id="bf43d-152">Kereskedelmi piactéri előfizetés lemondása</span><span class="sxs-lookup"><span data-stu-id="bf43d-152">Cancel a commercial marketplace subscription</span></span>](cancel-an-azure-marketplace-subscription.md)
* [<span data-ttu-id="bf43d-153">A kereskedelmi piactér-előfizetés engedélyezése vagy letiltása</span><span class="sxs-lookup"><span data-stu-id="bf43d-153">Enable or disable autorenew for a commercial marketplace subscription</span></span>](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a><span data-ttu-id="bf43d-154">Mennyiségi felügyelet</span><span class="sxs-lookup"><span data-stu-id="bf43d-154">Quantity management</span></span>

<span data-ttu-id="bf43d-155">A kereskedelmi piactér-előfizetés mennyiségének a társított [SKU](product-resources.md#sku) által meghatározott korlátokon belül kell lennie (lásd a **MinimumQuantity** és a **maximumQuantity** attribútumokat).</span><span class="sxs-lookup"><span data-stu-id="bf43d-155">The quantity of a commercial marketplace subscription must be within the limits defined by its associated [SKU](product-resources.md#sku) (see the **minimumQuantity** and **maximumQuantity** attributes).</span></span> <span data-ttu-id="bf43d-156">A kereskedelmi piactér-előfizetés mennyiségének frissítéséhez használja a következő metódust:</span><span class="sxs-lookup"><span data-stu-id="bf43d-156">To update the quantity of a commercial marketplace subscription, use the following method:</span></span>

* [<span data-ttu-id="bf43d-157">Egy előfizetés mennyiségének módosítása</span><span class="sxs-lookup"><span data-stu-id="bf43d-157">Change the quantity of a subscription</span></span>](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="bf43d-158">Számlázás és egyeztetés</span><span class="sxs-lookup"><span data-stu-id="bf43d-158">Invoice and reconciliation</span></span>

<span data-ttu-id="bf43d-159">A következő módszerekkel kezelheti az ügyfelek [számláit](invoice-resources.md) (beleértve a kereskedelmi piactér termékeire vonatkozó előfizetések díját is):</span><span class="sxs-lookup"><span data-stu-id="bf43d-159">You can manage customer [invoices](invoice-resources.md) (including charges for subscriptions to commercial marketplace products) using the following methods:</span></span>

* [<span data-ttu-id="bf43d-160">Számlázott kereskedelmi piactér-felhasználási sorok számlájának beolvasása</span><span class="sxs-lookup"><span data-stu-id="bf43d-160">Get invoice billed commercial marketplace consumption line items</span></span>](get-invoice-billed-consumption-lineitems.md)
* [<span data-ttu-id="bf43d-161">Számlabecslés hivatkozásainak lekérése</span><span class="sxs-lookup"><span data-stu-id="bf43d-161">Get invoice estimate links</span></span>](get-invoice-estimate-links.md)
* [<span data-ttu-id="bf43d-162">Számlázott kereskedelmi piactér-felhasználási sorok számlázása</span><span class="sxs-lookup"><span data-stu-id="bf43d-162">Get invoice unbilled commercial marketplace consumption line items</span></span>](get-invoice-unbilled-consumption-lineitems.md)
* [<span data-ttu-id="bf43d-163">Számlázással kapcsolatos nem számlázott egyeztetési sorok beolvasása</span><span class="sxs-lookup"><span data-stu-id="bf43d-163">Get invoice unbilled reconciliation line items</span></span>](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a><span data-ttu-id="bf43d-164">Tesztelés integrációs homokozó-fiók használatával</span><span class="sxs-lookup"><span data-stu-id="bf43d-164">Test using integration sandbox account</span></span>

<span data-ttu-id="bf43d-165">Éles környezetben, miután létrehozta a kereskedelmi Marketplace SaaS-termékek előfizetését, egy személyre szabott aktiválási hivatkozást kell lekérnie a partner Center webhelyről, és el kell végeznie a közzétevő helyét a telepítési folyamat befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="bf43d-165">In production, after you have created a subscription to commercial marketplace SaaS products, you need to retrieve a personalized activation link from Partner Center and visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="bf43d-166">Az előfizetés számlázása csak a telepítés befejeződése után kezdődik.</span><span class="sxs-lookup"><span data-stu-id="bf43d-166">Subscription billing will begin only after setup is complete.</span></span>

<span data-ttu-id="bf43d-167">A CSP homokozó környezetében nincs integráció az ISV-val.</span><span class="sxs-lookup"><span data-stu-id="bf43d-167">In the CSP sandbox environment, there is no integration with ISVs.</span></span> <span data-ttu-id="bf43d-168">Ha a partner Centerből próbál meg beolvasni egy aktiválási hivatkozást, a rendszer egy dummy-hivatkozást ad vissza.</span><span class="sxs-lookup"><span data-stu-id="bf43d-168">If you try to retrieve an activation link from Partner Center, a dummy link will be returned.</span></span> <span data-ttu-id="bf43d-169">Ez a dummy-hivatkozás nem használható a telepítési folyamat befejezéséhez a közzétevő webhelyén.</span><span class="sxs-lookup"><span data-stu-id="bf43d-169">You cannot use this dummy link to complete the setup process at the publisher's site.</span></span> <span data-ttu-id="bf43d-170">Ha az Integration sandbox-fiókot szeretné használni a kereskedelmi Marketplace SaaS-termékek előfizetések számlázásának teszteléséhez, használja a következő módszert az előfizetés aktiválásához.</span><span class="sxs-lookup"><span data-stu-id="bf43d-170">To use the integration sandbox account to test billing for subscriptions to commercial marketplace SaaS products, use the following method to activate the subscription instead.</span></span> <span data-ttu-id="bf43d-171">Az előfizetés számlázása a sikeres aktiválás után kezdődik:</span><span class="sxs-lookup"><span data-stu-id="bf43d-171">Subscription billing will begin after successful activation:</span></span>

* [<span data-ttu-id="bf43d-172">Homokozó elvű előfizetés aktiválása kereskedelmi piactér-termékekhez</span><span class="sxs-lookup"><span data-stu-id="bf43d-172">Activate a sandbox subscription for commercial marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

