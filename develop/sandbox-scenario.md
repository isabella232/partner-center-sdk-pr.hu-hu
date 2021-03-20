---
title: Viszonteladói kapcsolatot támogató partneri tesztkörnyezet-képességek
description: A partneri homokozó képes támogatni a partner és az ügyfél közötti kapcsolatokat
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: af46811b3615e1f904a9619de85b0aca7622490b
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711865"
---
# <a name="partner-sandbox-capabilities-that-support-reseller-relationship"></a><span data-ttu-id="fc4b2-103">Viszonteladói kapcsolatot támogató partneri tesztkörnyezet-képességek</span><span class="sxs-lookup"><span data-stu-id="fc4b2-103">Partner sandbox capabilities that support reseller relationship</span></span>

<span data-ttu-id="fc4b2-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="fc4b2-104">**Applies to:**</span></span>

- <span data-ttu-id="fc4b2-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="fc4b2-105">Partner Center</span></span>
- <span data-ttu-id="fc4b2-106">A 21Vianet által üzemeltetett Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="fc4b2-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="fc4b2-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="fc4b2-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="fc4b2-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="fc4b2-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fc4b2-109">Ez a cikk ismerteti, hogy a homokozóban milyen támogatott a viszonteladói kapcsolatok a partner és az ügyfél között.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-109">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fc4b2-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="fc4b2-110">Prerequisites</span></span>

- <span data-ttu-id="fc4b2-111">A partneri központ fiókjának hitelesítő adatai.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-111">Partner Center account credentials.</span></span> <span data-ttu-id="fc4b2-112">A sandbox forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-112">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="fc4b2-113">Ügyfél-azonosító (ügyfél-bérlői azonosító).</span><span class="sxs-lookup"><span data-stu-id="fc4b2-113">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="fc4b2-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard/home).</span><span class="sxs-lookup"><span data-stu-id="fc4b2-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="fc4b2-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fc4b2-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fc4b2-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fc4b2-118">A Microsoft ID megegyezik az ügyfél-AZONOSÍTÓval (ügyfél-bérlő-azonosító).</span><span class="sxs-lookup"><span data-stu-id="fc4b2-118">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="fc4b2-119">Az összes Azure Reserved Virtual Machine Instances-és szoftver-beszerzési rendelést meg kell szüntetni, mielőtt törölné egy ügyfelet a tip Integration sandbox-ból.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-119">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="fc4b2-120">Viszonteladói kapcsolatot támogató forgatókönyvek</span><span class="sxs-lookup"><span data-stu-id="fc4b2-120">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="fc4b2-121">A sandbox Direct Bill-partnerek és a közvetett szolgáltatók kapcsolatokat hozhatnak létre a homokozó-ügyféllel.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-121">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="fc4b2-122">A sandbox Direct Bill-partnerek és a közvetett szolgáltatók nem hívhatják meg a sandbox-ügyfeleket.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-122">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>



### <a name="in-the-sandbox"></a><span data-ttu-id="fc4b2-123">A homokozóban</span><span class="sxs-lookup"><span data-stu-id="fc4b2-123">In the Sandbox</span></span>

<span data-ttu-id="fc4b2-124">**Közvetlen számlázási partnerek**:</span><span class="sxs-lookup"><span data-stu-id="fc4b2-124">**Direct bill partners**:</span></span>

<span data-ttu-id="fc4b2-125">• Meglévő ügyfeleket adhat hozzá</span><span class="sxs-lookup"><span data-stu-id="fc4b2-125">•   Can add existing customers</span></span>

<span data-ttu-id="fc4b2-126">• Nem kérhet kapcsolatokat új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="fc4b2-126">•   Cannot request relationships with new customers</span></span>

<span data-ttu-id="fc4b2-127">**Közvetett szolgáltatók**:</span><span class="sxs-lookup"><span data-stu-id="fc4b2-127">**Indirect providers**:</span></span>

<span data-ttu-id="fc4b2-128">• Meglévő ügyfeleket adhat hozzá</span><span class="sxs-lookup"><span data-stu-id="fc4b2-128">•   Can add existing customers</span></span>

<span data-ttu-id="fc4b2-129">• Nem kérhet kapcsolatokat új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="fc4b2-129">•   Cannot request relationships with new customers</span></span>

<span data-ttu-id="fc4b2-130">• Nem lehet közvetett viszonteladóval létesített kapcsolat</span><span class="sxs-lookup"><span data-stu-id="fc4b2-130">•   Cannot have a relationship with an Indirect reseller</span></span>

<span data-ttu-id="fc4b2-131">**Közvetett viszonteladó**: (hamarosan elérhető)</span><span class="sxs-lookup"><span data-stu-id="fc4b2-131">**Indirect reseller**: (coming soon)</span></span>

<span data-ttu-id="fc4b2-132">• Meglévő ügyfelekkel is rendelkezhet kapcsolatokkal</span><span class="sxs-lookup"><span data-stu-id="fc4b2-132">•   Can have a relationships with existing customers</span></span>

<span data-ttu-id="fc4b2-133">• Nem kérhet új kapcsolatokat, és nem vehet fel új ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="fc4b2-133">•   Cannot request new relationships or add new customers</span></span>

### <a name="in-partner-center"></a><span data-ttu-id="fc4b2-134">A partner Centerben</span><span class="sxs-lookup"><span data-stu-id="fc4b2-134">In Partner Center</span></span>

<span data-ttu-id="fc4b2-135">**Közvetlen számlázási partnerek**:</span><span class="sxs-lookup"><span data-stu-id="fc4b2-135">**Direct bill partners**:</span></span>

<span data-ttu-id="fc4b2-136">• Új ügyfeleket adhat hozzá</span><span class="sxs-lookup"><span data-stu-id="fc4b2-136">•   Can add new customers</span></span>

<span data-ttu-id="fc4b2-137">• Az új ügyfelekkel is kérhet kapcsolatokat</span><span class="sxs-lookup"><span data-stu-id="fc4b2-137">•   Can request relationships with new customers</span></span>

<span data-ttu-id="fc4b2-138">**Közvetett szolgáltatók**:</span><span class="sxs-lookup"><span data-stu-id="fc4b2-138">**Indirect providers**:</span></span>

<span data-ttu-id="fc4b2-139">• Új ügyfeleket adhat hozzá</span><span class="sxs-lookup"><span data-stu-id="fc4b2-139">•   Can add new customers</span></span>

<span data-ttu-id="fc4b2-140">• Az új ügyfelekkel is kérhet kapcsolatokat</span><span class="sxs-lookup"><span data-stu-id="fc4b2-140">•   Can request relationships with new customers</span></span>

<span data-ttu-id="fc4b2-141">• A kapcsolat közvetett viszonteladókkal is rendelkezhet</span><span class="sxs-lookup"><span data-stu-id="fc4b2-141">•   Can have relationships with indirect resellers</span></span>

<span data-ttu-id="fc4b2-142">**Közvetett viszonteladók**:</span><span class="sxs-lookup"><span data-stu-id="fc4b2-142">**Indirect resellers**:</span></span>

<span data-ttu-id="fc4b2-143">• Nem lehet új ügyfeleket felvenni</span><span class="sxs-lookup"><span data-stu-id="fc4b2-143">•   Can’t add new customers</span></span>

<span data-ttu-id="fc4b2-144">• Az új ügyfelekkel is kérhet kapcsolatokat</span><span class="sxs-lookup"><span data-stu-id="fc4b2-144">•   Can request relationships with new customers</span></span>

3. <span data-ttu-id="fc4b2-145">A sandbox Direct Bill partner és a közvetett szolgáltatók el tudják távolítani a viszonteladói kapcsolatot a partner Center felhasználói felületéről és az API-ból.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-145">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="fc4b2-146">A homokozóban a viszonteladói kapcsolat eltávolítása meghívja a DELETE Customer AP-t.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-146">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="fc4b2-147">Ezzel eltávolítja a kapcsolatot, valamint törli az ügyfél bérlőjét is.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-147">This will remove the relationship as well as delete the customer tenant.</span></span> <span data-ttu-id="fc4b2-148">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="fc4b2-148">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>

<span data-ttu-id="fc4b2-149">A részletekért kövesse az ügyfél [viszonteladói kapcsolatának eltávolítása](remove-a-reseller-relationship-with-a-customer.md) című témakört.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-149">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="fc4b2-150">Van azonban néhány különbség a termék és a homokozó lehetőségei között.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-150">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fc4b2-151">KÉRELEM SZINTAXISA</span><span class="sxs-lookup"><span data-stu-id="fc4b2-151">REQUEST SYNTAX</span></span>

|<span data-ttu-id="fc4b2-152">**Metódus**</span><span class="sxs-lookup"><span data-stu-id="fc4b2-152">**Method**</span></span>|<span data-ttu-id="fc4b2-153">**Törlés**</span><span class="sxs-lookup"><span data-stu-id="fc4b2-153">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="fc4b2-154">Törlés</span><span class="sxs-lookup"><span data-stu-id="fc4b2-154">Delete</span></span>|<span data-ttu-id="fc4b2-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="fc4b2-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="fc4b2-156">A kérelem törzse nincs</span><span class="sxs-lookup"><span data-stu-id="fc4b2-156">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fc4b2-157">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="fc4b2-157">Response success and error codes</span></span>

<span data-ttu-id="fc4b2-158">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fc4b2-159">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fc4b2-160">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](./error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="fc4b2-160">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc4b2-161">Következő lépések</span><span class="sxs-lookup"><span data-stu-id="fc4b2-161">Next steps</span></span>

- [<span data-ttu-id="fc4b2-162">Az Azure Marketplace-termékekhez készült homokozó-előfizetések aktiválása</span><span class="sxs-lookup"><span data-stu-id="fc4b2-162">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="fc4b2-163">Megrendelés megszakítása a Homokozóból</span><span class="sxs-lookup"><span data-stu-id="fc4b2-163">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="fc4b2-164">Tesztelés és hibakeresés</span><span class="sxs-lookup"><span data-stu-id="fc4b2-164">Test and debug</span></span>](test-and-debug.md)