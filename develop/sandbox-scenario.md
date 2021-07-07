---
title: A viszonteladói kapcsolatokhoz szükséges sandbox-képességek
description: A partneri sandbox képes támogatni a partner és az ügyfél közötti kapcsolatokat
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aa6c4fb9ef71bacfad7e0f1510fec15f6af60a05
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547393"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a><span data-ttu-id="6c2e2-103">A viszonteladói kapcsolatokhoz szükséges sandbox-képességek</span><span class="sxs-lookup"><span data-stu-id="6c2e2-103">Sandbox capabilities for Reseller relationship</span></span>

<span data-ttu-id="6c2e2-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6c2e2-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6c2e2-105">Ez a cikk ismerteti, hogy mit támogat a sandbox a partner és az ügyfél közötti viszonteladói kapcsolatokhoz.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-105">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6c2e2-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6c2e2-106">Prerequisites</span></span>

- <span data-ttu-id="6c2e2-107">Partnerközpont fiók hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-107">Partner Center account credentials.</span></span> <span data-ttu-id="6c2e2-108">A sandbox forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-108">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="6c2e2-109">Egy ügyfél-azonosító (customer-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="6c2e2-109">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="6c2e2-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard/home)</span><span class="sxs-lookup"><span data-stu-id="6c2e2-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="6c2e2-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="6c2e2-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6c2e2-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="6c2e2-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6c2e2-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="6c2e2-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6c2e2-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval (customer-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="6c2e2-114">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="6c2e2-115">Minden Azure Reserved Virtual Machine Instances és szoftvervásárlási megrendelést meg kell szakítani, mielőtt törölné az ügyfelet a Tip integration sandboxból.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-115">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="6c2e2-116">Viszonteladói kapcsolatot támogató forgatókönyvek</span><span class="sxs-lookup"><span data-stu-id="6c2e2-116">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="6c2e2-117">A Sandbox Direct Bill-partnerek és a közvetett szolgáltatók kapcsolatokat hozhatnak létre a sandbox ügyféllel.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-117">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="6c2e2-118">A Sandbox Direct Bill-partnerek és a közvetett szolgáltatók nem hívnak meg sandbox-ügyfeleket.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-118">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>

3. <span data-ttu-id="6c2e2-119">A Sandbox Direct Bill Partner és a Indirect Providers el tudják távolítani a viszonteladói kapcsolatot Partnerközpont felhasználói felületről és API-ból.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-119">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="6c2e2-120">A Viszonteladói kapcsolat eltávolítása védőfal hívja meg az Ügyfél törlése API-t.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-120">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="6c2e2-121">Ezzel eltávolítja a kapcsolatot, és törli az ügyfélbérlőt.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-121">This will remove the relationship and delete the customer tenant.</span></span> <span data-ttu-id="6c2e2-122">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="6c2e2-122">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>


    ### <a name="in-the-sandbox"></a><span data-ttu-id="6c2e2-123">A sandboxban</span><span class="sxs-lookup"><span data-stu-id="6c2e2-123">In the Sandbox</span></span>

    <span data-ttu-id="6c2e2-124">**Közvetlen számlázási partnerek:**</span><span class="sxs-lookup"><span data-stu-id="6c2e2-124">**Direct bill partners**:</span></span>

    - <span data-ttu-id="6c2e2-125">Hozzáadhat meglévő ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="6c2e2-125">Can add existing customers</span></span>

    - <span data-ttu-id="6c2e2-126">Nem lehet kapcsolatokat kérni új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="6c2e2-126">Cannot request relationships with new customers</span></span>

    <span data-ttu-id="6c2e2-127">**Közvetett szolgáltatók:**</span><span class="sxs-lookup"><span data-stu-id="6c2e2-127">**Indirect providers**:</span></span>

    - <span data-ttu-id="6c2e2-128">Hozzáadhat meglévő ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="6c2e2-128">Can add existing customers</span></span>

    - <span data-ttu-id="6c2e2-129">Nem lehet kapcsolatokat kérni új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="6c2e2-129">Cannot request relationships with new customers</span></span>

    - <span data-ttu-id="6c2e2-130">Nem lehet kapcsolat közvetett viszonteladóval</span><span class="sxs-lookup"><span data-stu-id="6c2e2-130">Cannot have a relationship with an Indirect reseller</span></span>

    <span data-ttu-id="6c2e2-131">**Közvetett viszonteladó:**</span><span class="sxs-lookup"><span data-stu-id="6c2e2-131">**Indirect reseller**:</span></span> 

    -   <span data-ttu-id="6c2e2-132">Kapcsolat lehet meglévő ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="6c2e2-132">Can have relationships with existing customers</span></span>

    -   <span data-ttu-id="6c2e2-133">Nem kérhet új kapcsolatokat, és nem adhat hozzá új ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="6c2e2-133">Cannot request new relationships or add new customers</span></span>

    ### <a name="in-partner-center"></a><span data-ttu-id="6c2e2-134">A Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="6c2e2-134">In Partner Center</span></span>

    <span data-ttu-id="6c2e2-135">**Közvetlen számlázási partnerek:**</span><span class="sxs-lookup"><span data-stu-id="6c2e2-135">**Direct bill partners**:</span></span>

    -   <span data-ttu-id="6c2e2-136">Hozzáadhat új ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="6c2e2-136">Can add new customers</span></span>

    -   <span data-ttu-id="6c2e2-137">Kapcsolatok igénylése új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="6c2e2-137">Can request relationships with new customers</span></span>

    <span data-ttu-id="6c2e2-138">**Közvetett szolgáltatók:**</span><span class="sxs-lookup"><span data-stu-id="6c2e2-138">**Indirect providers**:</span></span>

    -   <span data-ttu-id="6c2e2-139">Hozzáadhat új ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="6c2e2-139">Can add new customers</span></span>

    -   <span data-ttu-id="6c2e2-140">Kapcsolatok igénylése új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="6c2e2-140">Can request relationships with new customers</span></span>

    -   <span data-ttu-id="6c2e2-141">Kapcsolat lehet közvetett viszonteladóval</span><span class="sxs-lookup"><span data-stu-id="6c2e2-141">Can have relationships with indirect resellers</span></span>

    <span data-ttu-id="6c2e2-142">**Közvetett viszonteladók:**</span><span class="sxs-lookup"><span data-stu-id="6c2e2-142">**Indirect resellers**:</span></span>

    -   <span data-ttu-id="6c2e2-143">Nem lehet új ügyfeleket felvenni</span><span class="sxs-lookup"><span data-stu-id="6c2e2-143">Can’t add new customers</span></span>

    -   <span data-ttu-id="6c2e2-144">Kapcsolatok igénylése új ügyfelekkel</span><span class="sxs-lookup"><span data-stu-id="6c2e2-144">Can request relationships with new customers</span></span>


<span data-ttu-id="6c2e2-145">A [részletekért kövesse](remove-a-reseller-relationship-with-a-customer.md) az ügyfél viszonteladói kapcsolatának eltávolítását.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-145">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="6c2e2-146">Van azonban néhány különbség a Termék és a Sandbox képességei között.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-146">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6c2e2-147">KÉRELEMSZINTAXIS</span><span class="sxs-lookup"><span data-stu-id="6c2e2-147">REQUEST SYNTAX</span></span>

|<span data-ttu-id="6c2e2-148">**Metódus**</span><span class="sxs-lookup"><span data-stu-id="6c2e2-148">**Method**</span></span>|<span data-ttu-id="6c2e2-149">**Törlés**</span><span class="sxs-lookup"><span data-stu-id="6c2e2-149">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="6c2e2-150">Törlés</span><span class="sxs-lookup"><span data-stu-id="6c2e2-150">Delete</span></span>|<span data-ttu-id="6c2e2-151">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="6c2e2-151">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="6c2e2-152">Kérelem törzse Nincs</span><span class="sxs-lookup"><span data-stu-id="6c2e2-152">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6c2e2-153">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="6c2e2-153">Response success and error codes</span></span>

<span data-ttu-id="6c2e2-154">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6c2e2-155">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="6c2e2-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6c2e2-156">A teljes listát lásd: Partnerközpont [REST-hibakódok.](./error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6c2e2-156">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c2e2-157">Következő lépések</span><span class="sxs-lookup"><span data-stu-id="6c2e2-157">Next steps</span></span>

- [<span data-ttu-id="6c2e2-158">Sandbox-előfizetések aktiválása Azure Marketplace termékekhez</span><span class="sxs-lookup"><span data-stu-id="6c2e2-158">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="6c2e2-159">Rendelés visszavonása a sandboxból</span><span class="sxs-lookup"><span data-stu-id="6c2e2-159">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="6c2e2-160">Tesztelés és hibakeresés</span><span class="sxs-lookup"><span data-stu-id="6c2e2-160">Test and debug</span></span>](test-and-debug.md)