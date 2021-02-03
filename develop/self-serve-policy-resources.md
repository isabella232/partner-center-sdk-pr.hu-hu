---
title: Önkiszolgáló házirend-erőforrások
description: Egy partner állít be önkiszolgáló házirendeket az ügyfél számára.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04daf6aaeb69153c4139941188f53dbab8979969
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767843"
---
# <a name="selfservepolicy-resource"></a><span data-ttu-id="fab8a-103">SelfServePolicy erőforrás</span><span class="sxs-lookup"><span data-stu-id="fab8a-103">SelfServePolicy resource</span></span>

<span data-ttu-id="fab8a-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="fab8a-104">**Applies to:**</span></span>

- <span data-ttu-id="fab8a-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="fab8a-105">Partner Center</span></span>

<span data-ttu-id="fab8a-106">Egy partner állít be önkiszolgáló házirendeket az ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="fab8a-106">A partner sets self serve policies for a customer.</span></span>

## <a name="selfservepolicy"></a><span data-ttu-id="fab8a-107">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="fab8a-107">SelfServePolicy</span></span>

<span data-ttu-id="fab8a-108">Útmutató a kosárhoz.</span><span class="sxs-lookup"><span data-stu-id="fab8a-108">Describes a cart.</span></span>

| <span data-ttu-id="fab8a-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="fab8a-109">Property</span></span>              | <span data-ttu-id="fab8a-110">Típus</span><span class="sxs-lookup"><span data-stu-id="fab8a-110">Type</span></span>             | <span data-ttu-id="fab8a-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="fab8a-111">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fab8a-112">id</span><span class="sxs-lookup"><span data-stu-id="fab8a-112">id</span></span>                    | <span data-ttu-id="fab8a-113">sztring</span><span class="sxs-lookup"><span data-stu-id="fab8a-113">string</span></span>           | <span data-ttu-id="fab8a-114">Önkiszolgáló házirend-azonosító, amelyet az önkiszolgáló házirend sikeres létrehozásakor kell megadni.</span><span class="sxs-lookup"><span data-stu-id="fab8a-114">A self serve policy identifier that is supplied upon successful creation of the self serve policy.</span></span>     |
| <span data-ttu-id="fab8a-115">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="fab8a-115">SelfServeEntity</span></span>       | <span data-ttu-id="fab8a-116">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="fab8a-116">SelfServeEntity</span></span>  | <span data-ttu-id="fab8a-117">Az önállóan kiszolgált entitás hozzáférést kap.</span><span class="sxs-lookup"><span data-stu-id="fab8a-117">The self serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="fab8a-118">Megadó fél</span><span class="sxs-lookup"><span data-stu-id="fab8a-118">Grantor</span></span>               | <span data-ttu-id="fab8a-119">Megadó fél</span><span class="sxs-lookup"><span data-stu-id="fab8a-119">Grantor</span></span>          | <span data-ttu-id="fab8a-120">A hozzáférést biztosító biztosító.</span><span class="sxs-lookup"><span data-stu-id="fab8a-120">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="fab8a-121">Engedélyek</span><span class="sxs-lookup"><span data-stu-id="fab8a-121">Permissions</span></span>           | <span data-ttu-id="fab8a-122">Engedély tömbje</span><span class="sxs-lookup"><span data-stu-id="fab8a-122">Array of Permission</span></span>| <span data-ttu-id="fab8a-123">[Engedélyezési](#permission) erőforrások tömbje.</span><span class="sxs-lookup"><span data-stu-id="fab8a-123">An Array of [Permission](#permission) resources.</span></span>                                                                     |

## <a name="selfserveentity"></a><span data-ttu-id="fab8a-124">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="fab8a-124">SelfServeEntity</span></span>

<span data-ttu-id="fab8a-125">Az engedélyt képviselő entitást jelöli.</span><span class="sxs-lookup"><span data-stu-id="fab8a-125">Represents the entity being granted permissions.</span></span>

| <span data-ttu-id="fab8a-126">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="fab8a-126">Property</span></span>             | <span data-ttu-id="fab8a-127">Típus</span><span class="sxs-lookup"><span data-stu-id="fab8a-127">Type</span></span>|<span data-ttu-id="fab8a-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="fab8a-128">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="fab8a-129">SelfServeEntityType</span><span class="sxs-lookup"><span data-stu-id="fab8a-129">SelfServeEntityType</span></span>  | <span data-ttu-id="fab8a-130">sztring</span><span class="sxs-lookup"><span data-stu-id="fab8a-130">string</span></span>                           | <span data-ttu-id="fab8a-131">Az entitás hozzáférést kap, elfogadott értékek: ügyfél.</span><span class="sxs-lookup"><span data-stu-id="fab8a-131">The entity being granted access, accepted values: Customer.</span></span>                                 |
| <span data-ttu-id="fab8a-132">TenantID</span><span class="sxs-lookup"><span data-stu-id="fab8a-132">TenantID</span></span>             | <span data-ttu-id="fab8a-133">sztring</span><span class="sxs-lookup"><span data-stu-id="fab8a-133">string</span></span>                           | <span data-ttu-id="fab8a-134">A hozzáférést engedélyező entitás bérlői azonosítója.</span><span class="sxs-lookup"><span data-stu-id="fab8a-134">The tenant identifier of the entity being granted access.</span></span>                                   |

## <a name="grantor"></a><span data-ttu-id="fab8a-135">Megadó fél</span><span class="sxs-lookup"><span data-stu-id="fab8a-135">Grantor</span></span>

<span data-ttu-id="fab8a-136">Az engedélyeket megadó megadót jelöli.</span><span class="sxs-lookup"><span data-stu-id="fab8a-136">Represents the grantor granting the permissions.</span></span>

| <span data-ttu-id="fab8a-137">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="fab8a-137">Property</span></span>             | <span data-ttu-id="fab8a-138">Típus</span><span class="sxs-lookup"><span data-stu-id="fab8a-138">Type</span></span>|<span data-ttu-id="fab8a-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="fab8a-139">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="fab8a-140">GrantorType</span><span class="sxs-lookup"><span data-stu-id="fab8a-140">GrantorType</span></span>          | <span data-ttu-id="fab8a-141">sztring</span><span class="sxs-lookup"><span data-stu-id="fab8a-141">string</span></span>                           | <span data-ttu-id="fab8a-142">A hozzáférést megadó engedélyező, elfogadott értékek: BillToPartner.</span><span class="sxs-lookup"><span data-stu-id="fab8a-142">The grantor granting access, accepted values: BillToPartner.</span></span>                               |
| <span data-ttu-id="fab8a-143">TenantID</span><span class="sxs-lookup"><span data-stu-id="fab8a-143">TenantID</span></span>             | <span data-ttu-id="fab8a-144">sztring</span><span class="sxs-lookup"><span data-stu-id="fab8a-144">string</span></span>                           | <span data-ttu-id="fab8a-145">A hozzáférést biztosító entitás bérlői azonosítója.</span><span class="sxs-lookup"><span data-stu-id="fab8a-145">The tenant identifier of the entity granting access.</span></span>                                       |


## <a name="permission"></a><span data-ttu-id="fab8a-146">Engedély</span><span class="sxs-lookup"><span data-stu-id="fab8a-146">Permission</span></span>

<span data-ttu-id="fab8a-147">Az önkiszolgáló házirendben lévő engedélyt jelöli.</span><span class="sxs-lookup"><span data-stu-id="fab8a-147">Represents a permission in the self serve policy.</span></span>

| <span data-ttu-id="fab8a-148">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="fab8a-148">Property</span></span>             | <span data-ttu-id="fab8a-149">Típus</span><span class="sxs-lookup"><span data-stu-id="fab8a-149">Type</span></span>|<span data-ttu-id="fab8a-150">Leírás</span><span class="sxs-lookup"><span data-stu-id="fab8a-150">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="fab8a-151">Erőforrás</span><span class="sxs-lookup"><span data-stu-id="fab8a-151">Resource</span></span>             | <span data-ttu-id="fab8a-152">sztring</span><span class="sxs-lookup"><span data-stu-id="fab8a-152">string</span></span>                           | <span data-ttu-id="fab8a-153">Az erőforrás-hozzáférés is meg van adva: AzureReservedInstances.</span><span class="sxs-lookup"><span data-stu-id="fab8a-153">The resource access is being granted too: AzureReservedInstances.</span></span>                          |
| <span data-ttu-id="fab8a-154">Művelet</span><span class="sxs-lookup"><span data-stu-id="fab8a-154">Action</span></span>               | <span data-ttu-id="fab8a-155">sztring</span><span class="sxs-lookup"><span data-stu-id="fab8a-155">string</span></span>                           | <span data-ttu-id="fab8a-156">A rendszer a következő műveletekhez biztosít hozzáférést: vásárlás</span><span class="sxs-lookup"><span data-stu-id="fab8a-156">The action access is being granted for: Purchase</span></span>                                           |
