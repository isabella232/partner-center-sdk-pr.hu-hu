---
title: Viszonteladói kapcsolatot támogató partneri tesztkörnyezet-képességek
description: A partneri homokozó képes támogatni a partner és az ügyfél közötti kapcsolatokat
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e01dd1a83ca459cbdf12b8e564b43a2d18f5595b
ms.sourcegitcommit: f69ceae441bbb2ddba96e878a1ec8c1a499a4879
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/13/2021
ms.locfileid: "98180731"
---
# <a name="partner-sandbox-capabilities-that-support-reseller-relationship"></a><span data-ttu-id="269f3-103">Viszonteladói kapcsolatot támogató partneri tesztkörnyezet-képességek</span><span class="sxs-lookup"><span data-stu-id="269f3-103">Partner sandbox capabilities that support reseller relationship</span></span>

<span data-ttu-id="269f3-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="269f3-104">**Applies to:**</span></span>

- <span data-ttu-id="269f3-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="269f3-105">Partner Center</span></span>
- <span data-ttu-id="269f3-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="269f3-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="269f3-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="269f3-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="269f3-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="269f3-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="269f3-109">Ez a cikk ismerteti, hogy a homokozóban milyen támogatott a viszonteladói kapcsolatok a partner és az ügyfél között.</span><span class="sxs-lookup"><span data-stu-id="269f3-109">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="269f3-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="269f3-110">Prerequisites</span></span>

- <span data-ttu-id="269f3-111">A partneri központ fiókjának hitelesítő adatai.</span><span class="sxs-lookup"><span data-stu-id="269f3-111">Partner Center account credentials.</span></span> <span data-ttu-id="269f3-112">A sandbox forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="269f3-112">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="269f3-113">Ügyfél-azonosító (ügyfél-bérlői azonosító).</span><span class="sxs-lookup"><span data-stu-id="269f3-113">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="269f3-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard/home).</span><span class="sxs-lookup"><span data-stu-id="269f3-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="269f3-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="269f3-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="269f3-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="269f3-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="269f3-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="269f3-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="269f3-118">A Microsoft ID megegyezik az ügyfél-AZONOSÍTÓval (ügyfél-bérlő-azonosító).</span><span class="sxs-lookup"><span data-stu-id="269f3-118">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="269f3-119">Az összes Azure Reserved Virtual Machine Instances-és szoftver-beszerzési rendelést meg kell szüntetni, mielőtt törölné egy ügyfelet a tip Integration sandbox-ból.</span><span class="sxs-lookup"><span data-stu-id="269f3-119">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="269f3-120">Viszonteladói kapcsolatot támogató forgatókönyvek</span><span class="sxs-lookup"><span data-stu-id="269f3-120">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="269f3-121">A sandbox Direct Bill-partnerek és a közvetett szolgáltatók kapcsolatokat hozhatnak létre a homokozó-ügyféllel.</span><span class="sxs-lookup"><span data-stu-id="269f3-121">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="269f3-122">A sandbox Direct Bill-partnerek és a közvetett szolgáltatók nem hívhatják meg a sandbox-ügyfeleket.</span><span class="sxs-lookup"><span data-stu-id="269f3-122">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>



### <a name="in-the-sandbox"></a><span data-ttu-id="269f3-123">A homokozóban</span><span class="sxs-lookup"><span data-stu-id="269f3-123">In the Sandbox</span></span>

<span data-ttu-id="269f3-124">**Közvetlen számlázási partnerek**:</span><span class="sxs-lookup"><span data-stu-id="269f3-124">**Direct bill partners**:</span></span>

<span data-ttu-id="269f3-125">• Meglévő ügyfeleket adhat hozzá</span><span class="sxs-lookup"><span data-stu-id="269f3-125">•   Can add existing customers</span></span>

<span data-ttu-id="269f3-126">• Nem kérhet kapcsolatokat új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="269f3-126">•   Cannot request relationships with new customers</span></span>

<span data-ttu-id="269f3-127">**Közvetett szolgáltatók**:</span><span class="sxs-lookup"><span data-stu-id="269f3-127">**Indirect providers**:</span></span>

<span data-ttu-id="269f3-128">• Meglévő ügyfeleket adhat hozzá</span><span class="sxs-lookup"><span data-stu-id="269f3-128">•   Can add existing customers</span></span>

<span data-ttu-id="269f3-129">• Nem kérhet kapcsolatokat új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="269f3-129">•   Cannot request relationships with new customers</span></span>

<span data-ttu-id="269f3-130">• Nem lehet közvetett viszonteladóval létesített kapcsolat</span><span class="sxs-lookup"><span data-stu-id="269f3-130">•   Cannot have a relationship with an Indirect reseller</span></span>

<span data-ttu-id="269f3-131">**Közvetett viszonteladó**: (hamarosan elérhető)</span><span class="sxs-lookup"><span data-stu-id="269f3-131">**Indirect reseller**: (coming soon)</span></span>

<span data-ttu-id="269f3-132">• Meglévő ügyfelekkel is rendelkezhet kapcsolatokkal</span><span class="sxs-lookup"><span data-stu-id="269f3-132">•   Can have a relationships with existing customers</span></span>

<span data-ttu-id="269f3-133">• Nem kérhet új kapcsolatokat, és nem vehet fel új ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="269f3-133">•   Cannot request new relationships or add new customers</span></span>

### <a name="in-partner-center"></a><span data-ttu-id="269f3-134">A partner Centerben</span><span class="sxs-lookup"><span data-stu-id="269f3-134">In Partner Center</span></span>

<span data-ttu-id="269f3-135">**Közvetlen számlázási partnerek**:</span><span class="sxs-lookup"><span data-stu-id="269f3-135">**Direct bill partners**:</span></span>

<span data-ttu-id="269f3-136">• Új ügyfeleket adhat hozzá</span><span class="sxs-lookup"><span data-stu-id="269f3-136">•   Can add new customers</span></span>

<span data-ttu-id="269f3-137">• Az új ügyfelekkel is kérhet kapcsolatokat</span><span class="sxs-lookup"><span data-stu-id="269f3-137">•   Can request relationships with new customers</span></span>

<span data-ttu-id="269f3-138">**Közvetett szolgáltatók**:</span><span class="sxs-lookup"><span data-stu-id="269f3-138">**Indirect providers**:</span></span>

<span data-ttu-id="269f3-139">• Új ügyfeleket adhat hozzá</span><span class="sxs-lookup"><span data-stu-id="269f3-139">•   Can add new customers</span></span>

<span data-ttu-id="269f3-140">• Az új ügyfelekkel is kérhet kapcsolatokat</span><span class="sxs-lookup"><span data-stu-id="269f3-140">•   Can request relationships with new customers</span></span>

<span data-ttu-id="269f3-141">• A kapcsolat közvetett viszonteladókkal is rendelkezhet</span><span class="sxs-lookup"><span data-stu-id="269f3-141">•   Can have relationships with indirect resellers</span></span>

<span data-ttu-id="269f3-142">**Közvetett viszonteladók**:</span><span class="sxs-lookup"><span data-stu-id="269f3-142">**Indirect resellers**:</span></span>

<span data-ttu-id="269f3-143">• Nem lehet új ügyfeleket felvenni</span><span class="sxs-lookup"><span data-stu-id="269f3-143">•   Can’t add new customers</span></span>

<span data-ttu-id="269f3-144">• Az új ügyfelekkel is kérhet kapcsolatokat</span><span class="sxs-lookup"><span data-stu-id="269f3-144">•   Can request relationships with new customers</span></span>

3. <span data-ttu-id="269f3-145">A sandbox Direct Bill partner és a közvetett szolgáltatók el tudják távolítani a viszonteladói kapcsolatot a partner Center felhasználói felületéről és az API-ból.</span><span class="sxs-lookup"><span data-stu-id="269f3-145">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="269f3-146">A homokozóban a viszonteladói kapcsolat eltávolítása meghívja a DELETE Customer AP-t.</span><span class="sxs-lookup"><span data-stu-id="269f3-146">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="269f3-147">Ezzel eltávolítja a kapcsolatot, valamint törli az ügyfél bérlőjét is.</span><span class="sxs-lookup"><span data-stu-id="269f3-147">This will remove the relationship as well as delete the customer tenant.</span></span> <span data-ttu-id="269f3-148">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="269f3-148">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>

<span data-ttu-id="269f3-149">A részletekért kövesse az ügyfél [viszonteladói kapcsolatának eltávolítása](remove-a-reseller-relationship-with-a-customer.md) című témakört.</span><span class="sxs-lookup"><span data-stu-id="269f3-149">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="269f3-150">Van azonban néhány különbség a termék és a homokozó lehetőségei között.</span><span class="sxs-lookup"><span data-stu-id="269f3-150">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="269f3-151">KÉRELEM SZINTAXISA</span><span class="sxs-lookup"><span data-stu-id="269f3-151">REQUEST SYNTAX</span></span>

|<span data-ttu-id="269f3-152">**Metódus**</span><span class="sxs-lookup"><span data-stu-id="269f3-152">**Method**</span></span>|<span data-ttu-id="269f3-153">**Törlés**</span><span class="sxs-lookup"><span data-stu-id="269f3-153">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="269f3-154">Törlés</span><span class="sxs-lookup"><span data-stu-id="269f3-154">Delete</span></span>|<span data-ttu-id="269f3-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="269f3-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="269f3-156">A kérelem törzse nincs</span><span class="sxs-lookup"><span data-stu-id="269f3-156">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="269f3-157">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="269f3-157">Response success and error codes</span></span>

<span data-ttu-id="269f3-158">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="269f3-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="269f3-159">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="269f3-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="269f3-160">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](https://docs.microsoft.com/partner-center/develop/error-codes)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="269f3-160">For the full list, see [Partner Center REST error codes](https://docs.microsoft.com/partner-center/develop/error-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="269f3-161">Következő lépések</span><span class="sxs-lookup"><span data-stu-id="269f3-161">Next steps</span></span>

- [<span data-ttu-id="269f3-162">Az Azure Marketplace-termékekhez készült homokozó-előfizetések aktiválása</span><span class="sxs-lookup"><span data-stu-id="269f3-162">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="269f3-163">Megrendelés megszakítása a Homokozóból</span><span class="sxs-lookup"><span data-stu-id="269f3-163">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="269f3-164">Tesztelés és hibakeresés</span><span class="sxs-lookup"><span data-stu-id="269f3-164">Test and debug</span></span>](test-and-debug.md) 
