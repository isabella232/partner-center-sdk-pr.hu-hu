---
title: A viszonteladói kapcsolatokhoz szükséges sandbox-képességek
description: A partneri sandbox képes támogatni a partner és az ügyfél közötti kapcsolatokat
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9bef4a15685ebbdc2212988f5ac5724b946cfd54
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/21/2021
ms.locfileid: "110243384"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a><span data-ttu-id="cf600-103">A viszonteladói kapcsolatokhoz szükséges sandbox-képességek</span><span class="sxs-lookup"><span data-stu-id="cf600-103">Sandbox capabilities for Reseller relationship</span></span>

<span data-ttu-id="cf600-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="cf600-104">**Applies to:**</span></span>

- <span data-ttu-id="cf600-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="cf600-105">Partner Center</span></span>
- <span data-ttu-id="cf600-106">A 21Vianet által üzemeltetett Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="cf600-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="cf600-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="cf600-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="cf600-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="cf600-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cf600-109">Ez a cikk ismerteti, hogy mit támogat a sandbox a partner és az ügyfél közötti viszonteladói kapcsolatokhoz.</span><span class="sxs-lookup"><span data-stu-id="cf600-109">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cf600-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="cf600-110">Prerequisites</span></span>

- <span data-ttu-id="cf600-111">Partnerközpont fiók hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="cf600-111">Partner Center account credentials.</span></span> <span data-ttu-id="cf600-112">A sandbox forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="cf600-112">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="cf600-113">Egy ügyfél-azonosító (customer-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="cf600-113">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="cf600-114">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard/home)</span><span class="sxs-lookup"><span data-stu-id="cf600-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="cf600-115">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="cf600-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cf600-116">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="cf600-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cf600-117">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="cf600-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cf600-118">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval (customer-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="cf600-118">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="cf600-119">Minden Azure Reserved Virtual Machine Instances és szoftvervásárlási megrendelést meg kell szakítani, mielőtt törölné az ügyfelet a Tip integration sandboxból.</span><span class="sxs-lookup"><span data-stu-id="cf600-119">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="cf600-120">Viszonteladói kapcsolatot támogató forgatókönyvek</span><span class="sxs-lookup"><span data-stu-id="cf600-120">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="cf600-121">A Sandbox Direct Bill-partnerek és a közvetett szolgáltatók kapcsolatokat hozhatnak létre a sandbox ügyféllel.</span><span class="sxs-lookup"><span data-stu-id="cf600-121">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="cf600-122">A Sandbox Direct Bill-partnerek és a közvetett szolgáltatók nem hívnak meg sandbox-ügyfeleket.</span><span class="sxs-lookup"><span data-stu-id="cf600-122">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>

3. <span data-ttu-id="cf600-123">A Sandbox Direct Bill Partner és a Indirect Providers képesek eltávolítani a viszonteladói kapcsolatot Partnerközpont felhasználói felületről és API-ból.</span><span class="sxs-lookup"><span data-stu-id="cf600-123">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="cf600-124">A Viszonteladói kapcsolat eltávolítása védőfal hívja meg az Ügyfél törlése API-t.</span><span class="sxs-lookup"><span data-stu-id="cf600-124">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="cf600-125">Ezzel eltávolítja a kapcsolatot, és törli az ügyfélbérlőt is.</span><span class="sxs-lookup"><span data-stu-id="cf600-125">This will remove the relationship as well as delete the customer tenant.</span></span> <span data-ttu-id="cf600-126">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="cf600-126">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>


    ### <a name="in-the-sandbox"></a><span data-ttu-id="cf600-127">A sandboxban</span><span class="sxs-lookup"><span data-stu-id="cf600-127">In the Sandbox</span></span>

    <span data-ttu-id="cf600-128">**Közvetlen számlázási partnerek:**</span><span class="sxs-lookup"><span data-stu-id="cf600-128">**Direct bill partners**:</span></span>

    - <span data-ttu-id="cf600-129">Hozzáadhat meglévő ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="cf600-129">Can add existing customers</span></span>

    - <span data-ttu-id="cf600-130">Nem lehet kapcsolatokat kérni az új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="cf600-130">Cannot request relationships with new customers</span></span>

    <span data-ttu-id="cf600-131">**Közvetett szolgáltatók:**</span><span class="sxs-lookup"><span data-stu-id="cf600-131">**Indirect providers**:</span></span>

    - <span data-ttu-id="cf600-132">Hozzáadhat meglévő ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="cf600-132">Can add existing customers</span></span>

    - <span data-ttu-id="cf600-133">Nem lehet kapcsolatokat kérni az új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="cf600-133">Cannot request relationships with new customers</span></span>

    - <span data-ttu-id="cf600-134">Nem lehet kapcsolat közvetett viszonteladóval</span><span class="sxs-lookup"><span data-stu-id="cf600-134">Cannot have a relationship with an Indirect reseller</span></span>

    <span data-ttu-id="cf600-135">**Közvetett viszonteladó:**</span><span class="sxs-lookup"><span data-stu-id="cf600-135">**Indirect reseller**:</span></span> 

    -   <span data-ttu-id="cf600-136">Meglévő ügyfelekkel is lehet kapcsolat</span><span class="sxs-lookup"><span data-stu-id="cf600-136">Can have a relationships with existing customers</span></span>

    -   <span data-ttu-id="cf600-137">Nem kérhet új kapcsolatokat, és nem adhat hozzá új ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="cf600-137">Cannot request new relationships or add new customers</span></span>

    ### <a name="in-partner-center"></a><span data-ttu-id="cf600-138">A Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="cf600-138">In Partner Center</span></span>

    <span data-ttu-id="cf600-139">**Közvetlen számlázási partnerek:**</span><span class="sxs-lookup"><span data-stu-id="cf600-139">**Direct bill partners**:</span></span>

    -   <span data-ttu-id="cf600-140">Felvehet új ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="cf600-140">Can add new customers</span></span>

    -   <span data-ttu-id="cf600-141">Kapcsolatok kérése új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="cf600-141">Can request relationships with new customers</span></span>

    <span data-ttu-id="cf600-142">**Közvetett szolgáltatók:**</span><span class="sxs-lookup"><span data-stu-id="cf600-142">**Indirect providers**:</span></span>

    -   <span data-ttu-id="cf600-143">Felvehet új ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="cf600-143">Can add new customers</span></span>

    -   <span data-ttu-id="cf600-144">Kapcsolatok kérése új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="cf600-144">Can request relationships with new customers</span></span>

    -   <span data-ttu-id="cf600-145">Kapcsolat lehet közvetett viszonteladókhoz</span><span class="sxs-lookup"><span data-stu-id="cf600-145">Can have relationships with indirect resellers</span></span>

    <span data-ttu-id="cf600-146">**Közvetett viszonteladók:**</span><span class="sxs-lookup"><span data-stu-id="cf600-146">**Indirect resellers**:</span></span>

    -   <span data-ttu-id="cf600-147">Nem lehet új ügyfeleket felvenni</span><span class="sxs-lookup"><span data-stu-id="cf600-147">Can’t add new customers</span></span>

    -   <span data-ttu-id="cf600-148">Kapcsolatok igénylése új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="cf600-148">Can request relationships with new customers</span></span>


<span data-ttu-id="cf600-149">A [részletekért kövesse](remove-a-reseller-relationship-with-a-customer.md) az ügyfél viszonteladói kapcsolatának eltávolítását.</span><span class="sxs-lookup"><span data-stu-id="cf600-149">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="cf600-150">Van azonban néhány különbség a Termék és a Sandbox képességei között.</span><span class="sxs-lookup"><span data-stu-id="cf600-150">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cf600-151">KÉRELEMSZINTAXIS</span><span class="sxs-lookup"><span data-stu-id="cf600-151">REQUEST SYNTAX</span></span>

|<span data-ttu-id="cf600-152">**Metódus**</span><span class="sxs-lookup"><span data-stu-id="cf600-152">**Method**</span></span>|<span data-ttu-id="cf600-153">**Törlés**</span><span class="sxs-lookup"><span data-stu-id="cf600-153">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="cf600-154">Törlés</span><span class="sxs-lookup"><span data-stu-id="cf600-154">Delete</span></span>|<span data-ttu-id="cf600-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="cf600-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="cf600-156">Kérelem törzse Nincs</span><span class="sxs-lookup"><span data-stu-id="cf600-156">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cf600-157">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="cf600-157">Response success and error codes</span></span>

<span data-ttu-id="cf600-158">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="cf600-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cf600-159">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="cf600-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cf600-160">A teljes listát lásd: Partnerközpont [REST-hibakódok.](./error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="cf600-160">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf600-161">Következő lépések</span><span class="sxs-lookup"><span data-stu-id="cf600-161">Next steps</span></span>

- [<span data-ttu-id="cf600-162">Sandbox-előfizetések aktiválása Azure Marketplace termékekhez</span><span class="sxs-lookup"><span data-stu-id="cf600-162">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="cf600-163">Rendelés visszavonása a sandboxból</span><span class="sxs-lookup"><span data-stu-id="cf600-163">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="cf600-164">Tesztelés és hibakeresés</span><span class="sxs-lookup"><span data-stu-id="cf600-164">Test and debug</span></span>](test-and-debug.md)