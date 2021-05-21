---
title: Közvetett CSP-szolgáltatói képességek a sandboxban
description: A közvetett szolgáltatók tesztelési célból létrehozhatnak közvetett viszonteladókat a tesztkészletben.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: bd0f38103e6b6f93ab5da386042b00801b683ccd
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/21/2021
ms.locfileid: "110244604"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a><span data-ttu-id="71481-103">Közvetett CSP-szolgáltatói sandbox-képességek közvetett viszonteladói fiókok létrehozásához</span><span class="sxs-lookup"><span data-stu-id="71481-103">CSP Indirect provider sandbox capabilities for creating Indirect reseller accounts</span></span> 

<span data-ttu-id="71481-104">**A következőre érvényes:**</span><span class="sxs-lookup"><span data-stu-id="71481-104">**Applies to**</span></span>

- <span data-ttu-id="71481-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="71481-105">Partner Center</span></span>

<span data-ttu-id="71481-106">**Megfelelő szerepkörök**</span><span class="sxs-lookup"><span data-stu-id="71481-106">**Appropriate roles**</span></span>

- <span data-ttu-id="71481-107">Közvetett szolgáltató</span><span class="sxs-lookup"><span data-stu-id="71481-107">Indirect provider</span></span>

<span data-ttu-id="71481-108">A közvetett CSP-szolgáltatók létrehozhatnak egy CSP Indirect Reseller-fiókot a saját 2. rétegbeli sandbox-fiókjukkal a Partnerközpont portálon.</span><span class="sxs-lookup"><span data-stu-id="71481-108">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account via through their own Tier 2 Sandbox account in Partner Center portal.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="71481-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="71481-109">Prerequisites</span></span> 

<span data-ttu-id="71481-110">Partnerközpont (2. réteg) közvetett szolgáltatói hitelesítő adatai.</span><span class="sxs-lookup"><span data-stu-id="71481-110">Partner Center Indirect Provider (Tier 2) sandbox credentials.</span></span> <span data-ttu-id="71481-111">A sandbox forgatókönyv támogatja a hitelesítést az önálló alkalmazás és az App+User hitelesítő adatok használatával.</span><span class="sxs-lookup"><span data-stu-id="71481-111">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span> 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="71481-112">Közvetett sandbox-szolgáltató – Közvetett Partnerközpont létrehozása</span><span class="sxs-lookup"><span data-stu-id="71481-112">Sandbox Indirect Provider – Create Sandbox Indirect Reseller using the Partner Center user interface</span></span> 

 <span data-ttu-id="71481-113">Ez egy csak a sandbox funkció, amely lehetővé teszi a közvetett sandbox-szolgáltatók számára, hogy közvetett viszonteladói fiókot hozzanak létre a Partnerközpont portálon.</span><span class="sxs-lookup"><span data-stu-id="71481-113">This is a Sandbox- only feature that allows Sandbox Indirect Providers the ability to create Sandbox Indirect Reseller account through the Partner Center portal.</span></span>

<span data-ttu-id="71481-114">A közvetett szolgáltatók a következő forgatókönyveket biztosítják a Sandboxban közvetett viszonteladók számára a Partnerközpont felhasználói felületén:</span><span class="sxs-lookup"><span data-stu-id="71481-114">The following scenarios are what Indirect providers can do for indirect resellers in Sandbox through the Partner Center user interface:</span></span> 

1. <span data-ttu-id="71481-115">A közvetett CSP-szolgáltatók létrehozhatnak egy CSP Indirect Reseller-fiókot a saját 2. rétegbeli Partnerközpont keresztül.</span><span class="sxs-lookup"><span data-stu-id="71481-115">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>
2. <span data-ttu-id="71481-116">A közvetett CSP-viszonteladók közvetett szolgáltatók szerint is megtekinthetik az ügyfeleket.</span><span class="sxs-lookup"><span data-stu-id="71481-116">CSP Indirect Resellers can view customer by Indirect Providers.</span></span> 

1. <span data-ttu-id="71481-117">A közvetett CSP-viszonteladók delegált rendszergazdai engedélyekkel kezelhetik az ügyfélfiókot.</span><span class="sxs-lookup"><span data-stu-id="71481-117">CSP Indirect Resellers  can manage the customer account using delegated admin permissions.</span></span>

1. <span data-ttu-id="71481-118">Közvetett CSP-szolgáltatók meghívhat közvetett CSP-viszonteladókat.</span><span class="sxs-lookup"><span data-stu-id="71481-118">CSP Indirect Providers can invite CSP Indirect Resellers.</span></span>
 
1. <span data-ttu-id="71481-119">A közvetett CSP-szolgáltatók törölhetik a CSP Indirect Reseller-fiókot a saját 2. rétegbeli Partnerközpont keresztül.</span><span class="sxs-lookup"><span data-stu-id="71481-119">CSP Indirect Providers can delete a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>

    <span data-ttu-id="71481-120">a.</span><span class="sxs-lookup"><span data-stu-id="71481-120">a.</span></span>  <span data-ttu-id="71481-121">Amikor a Sandbox Indirect Provider törli a közvetett viszonteladóval való kapcsolatot.</span><span class="sxs-lookup"><span data-stu-id="71481-121">When Sandbox Indirect Provider deletes relationship with Sandbox Indirect Reseller.</span></span>

    <span data-ttu-id="71481-122">b.</span><span class="sxs-lookup"><span data-stu-id="71481-122">b.</span></span>  <span data-ttu-id="71481-123">Ellenőrizze, hogy a közvetett viszonteladónak van-e más kapcsolata más szolgáltatókkal.</span><span class="sxs-lookup"><span data-stu-id="71481-123">Check if the Indirect Reseller has any other relationship with other providers.</span></span> <span data-ttu-id="71481-124">Ha igen, csak az adott közvetett szolgáltatóval való kapcsolat lesz eltávolítva.</span><span class="sxs-lookup"><span data-stu-id="71481-124">If so, only the relationship with that specific Indirect provider will be removed.</span></span>

    <span data-ttu-id="71481-125">c.</span><span class="sxs-lookup"><span data-stu-id="71481-125">c.</span></span> <span data-ttu-id="71481-126">Ha ez az integrációs rendszer egyetlen kapcsolata, akkor az integrációs rendszer törölve lesz.</span><span class="sxs-lookup"><span data-stu-id="71481-126">If that is the only relationship for the IR, then the IR will be deleted.</span></span>

1. <span data-ttu-id="71481-127">CSP Indirect Provider törölhet egy CSP Indirect Reseller.</span><span class="sxs-lookup"><span data-stu-id="71481-127">CSP Indirect Provider can delete a CSP Indirect Reseller.</span></span>

    <span data-ttu-id="71481-128">a.</span><span class="sxs-lookup"><span data-stu-id="71481-128">a.</span></span> <span data-ttu-id="71481-129">Ez egy csak a védőfalra jellemző funkció, amely lehetővé teszi a közvetett sandbox-szolgáltatók számára a közvetett viszonteladók törlését.</span><span class="sxs-lookup"><span data-stu-id="71481-129">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to delete Sandbox Indirect Resellers.</span></span>
     
1. <span data-ttu-id="71481-130">A sandbox indirect reseller törlésének előfeltételei:</span><span class="sxs-lookup"><span data-stu-id="71481-130">Pre-requisites for deleting a Sandbox Indirect Reseller:</span></span>

    1. <span data-ttu-id="71481-131">Függessze fel a közvetett Sandbox-viszonteladó egyes ügyfeleinek előfizetését.</span><span class="sxs-lookup"><span data-stu-id="71481-131">Suspend the subscriptions for each customer of Sandbox Indirect Reseller.</span></span>

    1. <span data-ttu-id="71481-132">Törölje a Közvetett viszonteladó összes ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="71481-132">Delete all customers of Indirect Reseller.</span></span>

1. <span data-ttu-id="71481-133">A közvetett viszonteladók által engedélyezett 5 közvetett viszonteladóra vonatkozó korlát a közvetett sandbox szolgáltatónként.</span><span class="sxs-lookup"><span data-stu-id="71481-133">Limit of 5 Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="71481-134">A közvetett sandbox viszonteladó törlése után a kvóta alaphelyzetbe áll.</span><span class="sxs-lookup"><span data-stu-id="71481-134">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="71481-135">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="71481-135">Pre-requisites</span></span>

- <span data-ttu-id="71481-136">A közvetett viszonteladók által engedélyezett 5 közvetett viszonteladóra vonatkozó korlát a közvetett sandbox szolgáltatónként.</span><span class="sxs-lookup"><span data-stu-id="71481-136">Limit of 5 Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> 

- <span data-ttu-id="71481-137">Ugyanaz az MPN-azonosító több közvetett viszonteladói sandbox-fiók létrehozására is használható, ha az MPN-azonosító országa és a Közvetett viszonteladói védőfal országa azonos.</span><span class="sxs-lookup"><span data-stu-id="71481-137">Same MPN ID can be used to create multiple Indirect Reseller Sandbox accounts if MPN ID country and Indirect Reseller Sandbox country are same.</span></span> <span data-ttu-id="71481-138">Ha van elérhető TESZT MPN-azonosítója, használhatja, vagy le tudja szerezni az MPN-azonosítók listáját a [Yammer-csatornán keresztül.]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 )</span><span class="sxs-lookup"><span data-stu-id="71481-138">If you have a test MPN ID available, you can use it, or you can get a list of MPN IDs through our [Yammer channel]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span></span> <span data-ttu-id="71481-139">Ha nincs hozzáférése a Yammerhez, a Yammer kérni fogja a hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="71481-139">If you don’t have access to Yammer, Yammer will ask you to request access.</span></span>
 
- <span data-ttu-id="71481-140">Közvetett sandbox-szolgáltatónként csak 75 ügyfél engedélyezett</span><span class="sxs-lookup"><span data-stu-id="71481-140">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="create-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="71481-141">CSP Indirect Reseller-fiók létrehozása</span><span class="sxs-lookup"><span data-stu-id="71481-141">Create CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="71481-142">Jelentkezzen be Partnerközpont 2. rétegbeli sandbox-fiókjával.</span><span class="sxs-lookup"><span data-stu-id="71481-142">Sign into Partner Center via your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="71481-143">A bal oldali menüben lépjen a Közvetett viszonteladók menüpontra.</span><span class="sxs-lookup"><span data-stu-id="71481-143">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="71481-144">Kattintson a "Viszonteladói védőfal hozzáadása" gombra.</span><span class="sxs-lookup"><span data-stu-id="71481-144">Click on “Add Reseller Sandbox” button.</span></span> 

4. <span data-ttu-id="71481-145">Töltse ki a fiókregisztrációs űrlapot.</span><span class="sxs-lookup"><span data-stu-id="71481-145">Fill the account enrollment form.</span></span> <span data-ttu-id="71481-146">Ez magától értetődő, de ne feledje, hogy egy közvetett viszonteladóhoz hoz létre sandbox-fiókot.</span><span class="sxs-lookup"><span data-stu-id="71481-146">It's self-explanatory but remember you are creating a Sandbox account for an Indirect Reseller.</span></span> <span data-ttu-id="71481-147">A fiók átvizsgálása nem megy keresztül, és a fiók regisztrálásának befejezése után azonnal aktiválódik.</span><span class="sxs-lookup"><span data-stu-id="71481-147">This account won't undergo vetting and will be activated as soon as you finish the account enrollment.</span></span>  

5. <span data-ttu-id="71481-148">A fiók létrehozása után a portálon le fogja kapni a közvetett viszonteladói sandbox-fiók globális rendszergazdai hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="71481-148">Once the account is created, you will get the Global Admin credentials for the Indirect Reseller sandbox account on the portal.</span></span> <span data-ttu-id="71481-149">Ne felejtse el azonnal menteni, különben nem fog tudni közvetett viszonteladói védőfalként bejelentkezni.</span><span class="sxs-lookup"><span data-stu-id="71481-149">Remember to save it immediately,  otherwise, you won't be able to sign in as an Indirect Reseller Sandbox.</span></span> 

6. <span data-ttu-id="71481-150">Jelentkezzen ki, majd jelentkezzen be újra Partnerközpont közvetett viszonteladói sandbox új hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="71481-150">Sign out and sign in again to Partner Center using the new credentials for Indirect Reseller Sandbox.</span></span> <span data-ttu-id="71481-151">Megismerheti a közvetett viszonteladóként is használhatja képességeit.</span><span class="sxs-lookup"><span data-stu-id="71481-151">Explore the capabilities you can do as an Indirect Reseller.</span></span> <span data-ttu-id="71481-152">Néhány dolog:</span><span class="sxs-lookup"><span data-stu-id="71481-152">Some things are :</span></span>  

    - <span data-ttu-id="71481-153">Profilok kezelése</span><span class="sxs-lookup"><span data-stu-id="71481-153">Manage profiles</span></span>  

    - <span data-ttu-id="71481-154">Felhasználók és szerepkörök kezelése</span><span class="sxs-lookup"><span data-stu-id="71481-154">Manage users and roles</span></span> 

    - <span data-ttu-id="71481-155">Közvetett szolgáltatók kezelése</span><span class="sxs-lookup"><span data-stu-id="71481-155">Manage Indirect Providers</span></span> 

    - <span data-ttu-id="71481-156">CSP-sandbox-ügyfelek kezelése</span><span class="sxs-lookup"><span data-stu-id="71481-156">Manage CSP Sandbox customers</span></span> 

    - <span data-ttu-id="71481-157">Kapcsolatok kezelése</span><span class="sxs-lookup"><span data-stu-id="71481-157">Manage relationships</span></span>
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="71481-158">Közvetett sandbox-szolgáltató – Közvetett viszonteladó törlése a Partnerközpont felhasználói felület használatával</span><span class="sxs-lookup"><span data-stu-id="71481-158">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller using the Partner Center user interface</span></span>

 <span data-ttu-id="71481-159">Ez egy csak a sandbox funkció, amely lehetővé teszi a közvetett sandbox-szolgáltatók számára egy meglévő közvetett viszonteladói fiók törlését az Partnerközpont portálon keresztül.</span><span class="sxs-lookup"><span data-stu-id="71481-159">This is a Sandbox only feature that allows Sandbox Indirect Providers an ability to delete an existing Sandbox Indirect Reseller account via Partner Center portal.</span></span> 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a><span data-ttu-id="71481-160">A közvetett viszonteladó törlésének előfeltételei:</span><span class="sxs-lookup"><span data-stu-id="71481-160">Pre-requisites to delete sandbox Indirect reseller:</span></span>

<span data-ttu-id="71481-161">Egy meglévő CSP Indirect Reseller fiók, amely a saját CSP Indirect Provider 2. rétegbeli sandbox-fiókjához van társítva.</span><span class="sxs-lookup"><span data-stu-id="71481-161">An existing CSP Indirect Reseller Sandbox account associated with your own CSP Indirect Provider Tier-2 Sandbox account.</span></span>  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="71481-162">A CSP Indirect Reseller-fiók törlése</span><span class="sxs-lookup"><span data-stu-id="71481-162">Delete CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="71481-163">Jelentkezzen be Partnerközpont 2. rétegbeli sandbox-fiókjával.</span><span class="sxs-lookup"><span data-stu-id="71481-163">Sign into Partner Center using your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="71481-164">A bal oldali menüben lépjen a Közvetett viszonteladók menüpontra.</span><span class="sxs-lookup"><span data-stu-id="71481-164">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="71481-165">Kattintson a **Viszonteladói védőfal törlése** hivatkozásra a törölni kívánt közvetett viszonteladói sandbox-fiók mellett.</span><span class="sxs-lookup"><span data-stu-id="71481-165">Click on **Delete Reseller Sandbox** link next to the Indirect Reseller Sandbox account you want to delete.</span></span> <span data-ttu-id="71481-166">A közvetett viszonteladói sandbox-fiók véglegesen törlődik, és nem állítható helyre.</span><span class="sxs-lookup"><span data-stu-id="71481-166">The Indirect Reseller Sandbox account will be permanently deleted and cannot be recovered.</span></span> 

## <a name="api-references"></a><span data-ttu-id="71481-167">API-referenciák</span><span class="sxs-lookup"><span data-stu-id="71481-167">API references</span></span>

- <span data-ttu-id="71481-168">Közvetett viszonteladó létrehozása</span><span class="sxs-lookup"><span data-stu-id="71481-168">Create Indirect Reseller</span></span> 
- <span data-ttu-id="71481-169">Közvetett viszonteladó törlése</span><span class="sxs-lookup"><span data-stu-id="71481-169">Delete Indirect Reseller</span></span> 

 

 