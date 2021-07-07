---
title: Közvetett CSP-szolgáltatói képességek a védőfalon
description: A közvetett szolgáltatók tesztelési célból létrehozhatnak közvetett viszonteladókat a tesztkészletben.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: da35dadd4e13247e923259a1cf3a67852f4b9e00
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445901"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a><span data-ttu-id="6d582-103">Közvetett CSP-szolgáltatói sandbox-képességek közvetett viszonteladói fiókok létrehozásához</span><span class="sxs-lookup"><span data-stu-id="6d582-103">CSP Indirect provider sandbox capabilities for creating Indirect reseller accounts</span></span> 

<span data-ttu-id="6d582-104">**Megfelelő szerepkörök:** Közvetett szolgáltató</span><span class="sxs-lookup"><span data-stu-id="6d582-104">**Appropriate roles**: Indirect provider</span></span>

<span data-ttu-id="6d582-105">A közvetett CSP-szolgáltatók létrehozhatnak egy CSP Indirect Reseller-fiókot a saját 2. rétegbeli sandbox-fiókjukkal a Partnerközpont portálon.</span><span class="sxs-lookup"><span data-stu-id="6d582-105">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account via through their own Tier 2 Sandbox account in Partner Center portal.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6d582-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6d582-106">Prerequisites</span></span> 

<span data-ttu-id="6d582-107">Partnerközpont (2. réteg) közvetett szolgáltatói hitelesítő adatai.</span><span class="sxs-lookup"><span data-stu-id="6d582-107">Partner Center Indirect Provider (Tier 2) sandbox credentials.</span></span> <span data-ttu-id="6d582-108">A sandbox forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="6d582-108">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span> 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="6d582-109">Sandbox Indirect Provider (Közvetett Partnerközpont szolgáltató) – Közvetett Partnerközpont létrehozása</span><span class="sxs-lookup"><span data-stu-id="6d582-109">Sandbox Indirect Provider – Create Sandbox Indirect Reseller using the Partner Center user interface</span></span> 

 <span data-ttu-id="6d582-110">Ez egy csak a védőfalra jellemző funkció, amely lehetővé teszi, hogy közvetett szolgáltatói sandbox közvetett viszonteladói fiókot hozzanak létre a Partnerközpont portálon.</span><span class="sxs-lookup"><span data-stu-id="6d582-110">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to create a Sandbox Indirect Reseller account through the Partner Center portal.</span></span>

<span data-ttu-id="6d582-111">A közvetett szolgáltatók a következő forgatókönyveket biztosítják a Sandboxban közvetett viszonteladók számára a Partnerközpont felhasználói felületén:</span><span class="sxs-lookup"><span data-stu-id="6d582-111">The following scenarios are what Indirect providers can do for indirect resellers in Sandbox through the Partner Center user interface:</span></span> 

1. <span data-ttu-id="6d582-112">A közvetett CSP-szolgáltatók létrehozhatnak egy CSP Indirect Reseller-fiókot a saját 2. rétegbeli Partnerközpont keresztül.</span><span class="sxs-lookup"><span data-stu-id="6d582-112">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>
2. <span data-ttu-id="6d582-113">A közvetett CSP-viszonteladók közvetett szolgáltatók szerint is megtekinthetik az ügyfeleket.</span><span class="sxs-lookup"><span data-stu-id="6d582-113">CSP Indirect Resellers can view customer by Indirect Providers.</span></span> 

1. <span data-ttu-id="6d582-114">A közvetett CSP-viszonteladók delegált rendszergazdai engedélyekkel kezelhetik az ügyfélfiókot.</span><span class="sxs-lookup"><span data-stu-id="6d582-114">CSP Indirect Resellers can manage the customer account using delegated admin permissions.</span></span>

1. <span data-ttu-id="6d582-115">Közvetett CSP-szolgáltatók meghívhat közvetett CSP-viszonteladókat.</span><span class="sxs-lookup"><span data-stu-id="6d582-115">CSP Indirect Providers can invite CSP Indirect Resellers.</span></span>
 
1. <span data-ttu-id="6d582-116">A közvetett CSP-szolgáltatók törölhetik a CSP Indirect Reseller-fiókot a saját 2. rétegbeli Partnerközpont keresztül.</span><span class="sxs-lookup"><span data-stu-id="6d582-116">CSP Indirect Providers can delete a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>

    <span data-ttu-id="6d582-117">a.</span><span class="sxs-lookup"><span data-stu-id="6d582-117">a.</span></span>  <span data-ttu-id="6d582-118">Amikor a Sandbox Indirect Provider törli a közvetett viszonteladóval való kapcsolatot, ellenőrizze, hogy a közvetett viszonteladónak van-e más kapcsolata más szolgáltatókkal.</span><span class="sxs-lookup"><span data-stu-id="6d582-118">When Sandbox Indirect Provider deletes the relationship with Sandbox Indirect Reseller, check if the Indirect Reseller has any other relationship with other providers.</span></span> <span data-ttu-id="6d582-119">Ha igen, csak az adott közvetett szolgáltatóval való kapcsolat lesz eltávolítva.</span><span class="sxs-lookup"><span data-stu-id="6d582-119">If so, only the relationship with that specific Indirect provider will be removed.</span></span>

    <span data-ttu-id="6d582-120">c.</span><span class="sxs-lookup"><span data-stu-id="6d582-120">c.</span></span> <span data-ttu-id="6d582-121">Ha ez az egyetlen kapcsolat a közvetett viszonteladóhoz, akkor a közvetett viszonteladó törlődik.</span><span class="sxs-lookup"><span data-stu-id="6d582-121">If that is the only relationship for the Indirect Reseller, then the Indirect Reseller will be deleted.</span></span>

1. <span data-ttu-id="6d582-122">A közvetett CSP-szolgáltatók törölhetik a CSP Indirect Reseller.</span><span class="sxs-lookup"><span data-stu-id="6d582-122">CSP Indirect Providers can delete a CSP Indirect Reseller.</span></span>

    <span data-ttu-id="6d582-123">a.</span><span class="sxs-lookup"><span data-stu-id="6d582-123">a.</span></span> <span data-ttu-id="6d582-124">Ez egy csak a védőfalra jellemző funkció, amely lehetővé teszi a közvetett sandbox-szolgáltatók számára a közvetett viszonteladók törlését.</span><span class="sxs-lookup"><span data-stu-id="6d582-124">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to delete Sandbox Indirect Resellers.</span></span>
     
1. <span data-ttu-id="6d582-125">A sandbox indirect reseller törlésének előfeltételei:</span><span class="sxs-lookup"><span data-stu-id="6d582-125">Pre-requisites for deleting a Sandbox Indirect Reseller:</span></span>

    1. <span data-ttu-id="6d582-126">Függessze fel az előfizetéseket a Sandbox Indirect Reseller minden egyes ügyfele esetében.</span><span class="sxs-lookup"><span data-stu-id="6d582-126">Suspend the subscriptions for each customer of Sandbox Indirect Reseller.</span></span>

    1. <span data-ttu-id="6d582-127">Törölje a Közvetett viszonteladó összes ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="6d582-127">Delete all customers of Indirect Reseller.</span></span>

1. <span data-ttu-id="6d582-128">A közvetett viszonteladók által engedélyezett öt közvetett viszonteladóra vonatkozó korlát a közvetett sandbox szolgáltatónként.</span><span class="sxs-lookup"><span data-stu-id="6d582-128">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="6d582-129">A közvetett sandbox viszonteladó törlése után a kvóta alaphelyzetbe áll.</span><span class="sxs-lookup"><span data-stu-id="6d582-129">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="6d582-130">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6d582-130">Pre-requisites</span></span>

- <span data-ttu-id="6d582-131">A közvetett viszonteladók által engedélyezett öt közvetett viszonteladóra vonatkozó korlát a közvetett sandbox szolgáltatónként.</span><span class="sxs-lookup"><span data-stu-id="6d582-131">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> 

- <span data-ttu-id="6d582-132">Ugyanaz az MPN-azonosító több közvetett viszonteladói sandbox-fiók létrehozására is használható, ha az MPN-azonosító országa és a Közvetett viszonteladói védőfal országa azonos.</span><span class="sxs-lookup"><span data-stu-id="6d582-132">Same MPN ID can be used to create multiple Indirect Reseller Sandbox accounts if MPN ID country and Indirect Reseller Sandbox country are same.</span></span> <span data-ttu-id="6d582-133">Ha van elérhető MPN-tesztazonosítója, használhatja, vagy le tudja szerezni az MPN-azonosítók listáját a Yammer [csatornán.]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 )</span><span class="sxs-lookup"><span data-stu-id="6d582-133">If you have a test MPN ID available, you can use it, or you can get a list of MPN IDs through our [Yammer channel]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span></span> <span data-ttu-id="6d582-134">Ha nem rendelkezik hozzáféréssel a Yammer, Yammer kérni fogja a hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="6d582-134">If you don’t have access to Yammer, Yammer will ask you to request access.</span></span>
 
- <span data-ttu-id="6d582-135">Közvetett sandbox-szolgáltatónként csak 75 ügyfél engedélyezett</span><span class="sxs-lookup"><span data-stu-id="6d582-135">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="create-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="6d582-136">CSP Indirect Reseller-fiók létrehozása</span><span class="sxs-lookup"><span data-stu-id="6d582-136">Create CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="6d582-137">Jelentkezzen be Partnerközpont 2. rétegbeli sandbox-fiókjával.</span><span class="sxs-lookup"><span data-stu-id="6d582-137">Sign into Partner Center via your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="6d582-138">A bal oldali menüben lépjen a Közvetett viszonteladók menüpontra.</span><span class="sxs-lookup"><span data-stu-id="6d582-138">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="6d582-139">Válassza a **Viszonteladói sandbox hozzáadása gombot.**</span><span class="sxs-lookup"><span data-stu-id="6d582-139">Select the **Add Reseller Sandbox** button.</span></span> 

4. <span data-ttu-id="6d582-140">Töltse ki a fiókregisztrációs űrlapot.</span><span class="sxs-lookup"><span data-stu-id="6d582-140">Fill the account enrollment form.</span></span> <span data-ttu-id="6d582-141">Ez magától értetődő, de ne feledje, hogy egy közvetett viszonteladóhoz hoz létre sandbox-fiókot.</span><span class="sxs-lookup"><span data-stu-id="6d582-141">It's self-explanatory but remember you are creating a Sandbox account for an Indirect Reseller.</span></span> <span data-ttu-id="6d582-142">A fiók átvizsgálása nem megy keresztül, és a fiók regisztrálásának befejezése után azonnal aktiválódik.</span><span class="sxs-lookup"><span data-stu-id="6d582-142">This account won't undergo vetting and will be activated as soon as you finish the account enrollment.</span></span>  

5. <span data-ttu-id="6d582-143">A fiók létrehozása után a portálon le fogja kapni a közvetett viszonteladói sandbox-fiók globális rendszergazdai hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="6d582-143">Once the account is created, you will get the Global Admin credentials for the Indirect Reseller sandbox account on the portal.</span></span> <span data-ttu-id="6d582-144">Ne felejtse el azonnal menteni, ellenkező esetben nem fog tudni közvetett viszonteladói védőfalként bejelentkezni.</span><span class="sxs-lookup"><span data-stu-id="6d582-144">Remember to save it immediately,  otherwise, you won't be able to sign in as an Indirect Reseller Sandbox.</span></span> 

6. <span data-ttu-id="6d582-145">Jelentkezzen ki, majd jelentkezzen be újra Partnerközpont közvetett viszonteladói sandbox új hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="6d582-145">Sign out and sign in again to Partner Center using the new credentials for Indirect Reseller Sandbox.</span></span> <span data-ttu-id="6d582-146">Megismerheti a közvetett viszonteladóként is használhatja képességeit.</span><span class="sxs-lookup"><span data-stu-id="6d582-146">Explore the capabilities you can do as an Indirect Reseller.</span></span> <span data-ttu-id="6d582-147">Néhány dolog:</span><span class="sxs-lookup"><span data-stu-id="6d582-147">Some things are:</span></span>  

    - <span data-ttu-id="6d582-148">Profilok kezelése</span><span class="sxs-lookup"><span data-stu-id="6d582-148">Manage profiles</span></span>  

    - <span data-ttu-id="6d582-149">Felhasználók és szerepkörök kezelése</span><span class="sxs-lookup"><span data-stu-id="6d582-149">Manage users and roles</span></span> 

    - <span data-ttu-id="6d582-150">Közvetett szolgáltatók kezelése</span><span class="sxs-lookup"><span data-stu-id="6d582-150">Manage Indirect Providers</span></span> 

    - <span data-ttu-id="6d582-151">CSP-sandbox-ügyfelek kezelése</span><span class="sxs-lookup"><span data-stu-id="6d582-151">Manage CSP Sandbox customers</span></span> 

    - <span data-ttu-id="6d582-152">Kapcsolatok kezelése</span><span class="sxs-lookup"><span data-stu-id="6d582-152">Manage relationships</span></span>
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="6d582-153">Közvetett sandbox-szolgáltató – Közvetett Partnerközpont törlése a Partnerközpont felületén</span><span class="sxs-lookup"><span data-stu-id="6d582-153">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller using the Partner Center user interface</span></span>

 <span data-ttu-id="6d582-154">Ez egy csak a sandbox funkció, amely lehetővé teszi a közvetett sandbox-szolgáltatók számára egy meglévő közvetett viszonteladói fiók törlését a Partnerközpont portálon.</span><span class="sxs-lookup"><span data-stu-id="6d582-154">This is a Sandbox only feature that allows Sandbox Indirect Providers an ability to delete an existing Sandbox Indirect Reseller account via Partner Center portal.</span></span> 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a><span data-ttu-id="6d582-155">A közvetett viszonteladó törlésének előfeltételei:</span><span class="sxs-lookup"><span data-stu-id="6d582-155">Pre-requisites to delete sandbox Indirect reseller:</span></span>

<span data-ttu-id="6d582-156">Egy meglévő CSP Indirect Reseller fiók, amely a saját CSP Indirect Provider 2. rétegbeli sandbox-fiókjához van társítva.</span><span class="sxs-lookup"><span data-stu-id="6d582-156">An existing CSP Indirect Reseller Sandbox account associated with your own CSP Indirect Provider Tier-2 Sandbox account.</span></span>  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="6d582-157">A CSP Indirect Reseller-fiók törlése</span><span class="sxs-lookup"><span data-stu-id="6d582-157">Delete CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="6d582-158">Jelentkezzen be Partnerközpont a 2. rétegbeli sandbox-fiókjával.</span><span class="sxs-lookup"><span data-stu-id="6d582-158">Sign into Partner Center using your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="6d582-159">A bal oldali menüben lépjen a Közvetett viszonteladók menüpontra.</span><span class="sxs-lookup"><span data-stu-id="6d582-159">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="6d582-160">Válassza **a Viszonteladói védőfal** törlése hivatkozást a törölni kívánt közvetett viszonteladói sandbox-fiók mellett.</span><span class="sxs-lookup"><span data-stu-id="6d582-160">Select the **Delete Reseller Sandbox** link next to the Indirect Reseller Sandbox account you want to delete.</span></span> <span data-ttu-id="6d582-161">A közvetett viszonteladói sandbox-fiók véglegesen törölve lesz, és nem állítható helyre.</span><span class="sxs-lookup"><span data-stu-id="6d582-161">The Indirect Reseller Sandbox account will be permanently deleted and cannot be recovered.</span></span> 

## <a name="api-references"></a><span data-ttu-id="6d582-162">API-referenciák</span><span class="sxs-lookup"><span data-stu-id="6d582-162">API references</span></span>

- <span data-ttu-id="6d582-163">Közvetett viszonteladó létrehozása</span><span class="sxs-lookup"><span data-stu-id="6d582-163">Create Indirect Reseller</span></span> 
- <span data-ttu-id="6d582-164">Közvetett viszonteladó törlése</span><span class="sxs-lookup"><span data-stu-id="6d582-164">Delete Indirect Reseller</span></span> 

 

 