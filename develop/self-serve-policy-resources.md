---
title: Önkiszolgáló szabályzat erőforrásai
description: A partnerek önkiszolgáló szabályzatokat állít be az ügyfelek számára.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e44581b805e076132984b67280699314e274ca94
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446717"
---
# <a name="selfservepolicy-resource"></a><span data-ttu-id="c0d8b-103">SelfServePolicy erőforrás</span><span class="sxs-lookup"><span data-stu-id="c0d8b-103">SelfServePolicy resource</span></span>

<span data-ttu-id="c0d8b-104">A partnerek önkiszolgáló szabályzatokat állít be az ügyfelek számára.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-104">A partner sets self serve policies for a customer.</span></span>

## <a name="selfservepolicy"></a><span data-ttu-id="c0d8b-105">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="c0d8b-105">SelfServePolicy</span></span>

<span data-ttu-id="c0d8b-106">Egy kosárra ír le.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-106">Describes a cart.</span></span>

| <span data-ttu-id="c0d8b-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="c0d8b-107">Property</span></span>              | <span data-ttu-id="c0d8b-108">Típus</span><span class="sxs-lookup"><span data-stu-id="c0d8b-108">Type</span></span>             | <span data-ttu-id="c0d8b-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="c0d8b-109">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c0d8b-110">id</span><span class="sxs-lookup"><span data-stu-id="c0d8b-110">id</span></span>                    | <span data-ttu-id="c0d8b-111">sztring</span><span class="sxs-lookup"><span data-stu-id="c0d8b-111">string</span></span>           | <span data-ttu-id="c0d8b-112">Önkiszolgáló szabályzatazonosító, amely az önkiszolgáló szabályzat sikeres létrehozásakor lesz megadva.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-112">A self-serve policy identifier that is supplied upon successful creation of the self serve policy.</span></span>     |
| <span data-ttu-id="c0d8b-113">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="c0d8b-113">SelfServeEntity</span></span>       | <span data-ttu-id="c0d8b-114">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="c0d8b-114">SelfServeEntity</span></span>  | <span data-ttu-id="c0d8b-115">Az önkiszolgáló entitás, amely hozzáférést kap.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-115">The self serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="c0d8b-116">Grantor</span><span class="sxs-lookup"><span data-stu-id="c0d8b-116">Grantor</span></span>               | <span data-ttu-id="c0d8b-117">Grantor</span><span class="sxs-lookup"><span data-stu-id="c0d8b-117">Grantor</span></span>          | <span data-ttu-id="c0d8b-118">A hozzáférést engedélyező megadó.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-118">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="c0d8b-119">Engedélyek</span><span class="sxs-lookup"><span data-stu-id="c0d8b-119">Permissions</span></span>           | <span data-ttu-id="c0d8b-120">Engedélytömb</span><span class="sxs-lookup"><span data-stu-id="c0d8b-120">Array of Permission</span></span>| <span data-ttu-id="c0d8b-121">[Engedélyerőforrások tömbje.](#permission)</span><span class="sxs-lookup"><span data-stu-id="c0d8b-121">An Array of [Permission](#permission) resources.</span></span>                                                                     |

## <a name="selfserveentity"></a><span data-ttu-id="c0d8b-122">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="c0d8b-122">SelfServeEntity</span></span>

<span data-ttu-id="c0d8b-123">Az engedélyeket kapott entitást jelöli.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-123">Represents the entity being granted permissions.</span></span>

| <span data-ttu-id="c0d8b-124">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="c0d8b-124">Property</span></span>             | <span data-ttu-id="c0d8b-125">Típus</span><span class="sxs-lookup"><span data-stu-id="c0d8b-125">Type</span></span>|<span data-ttu-id="c0d8b-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="c0d8b-126">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="c0d8b-127">SelfServeEntityType</span><span class="sxs-lookup"><span data-stu-id="c0d8b-127">SelfServeEntityType</span></span>  | <span data-ttu-id="c0d8b-128">sztring</span><span class="sxs-lookup"><span data-stu-id="c0d8b-128">string</span></span>                           | <span data-ttu-id="c0d8b-129">A hozzáférést kapott entitás, elfogadott értékek: Ügyfél.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-129">The entity being granted access, accepted values: Customer.</span></span>                                 |
| <span data-ttu-id="c0d8b-130">TenantID (Bérlőazonosító)</span><span class="sxs-lookup"><span data-stu-id="c0d8b-130">TenantID</span></span>             | <span data-ttu-id="c0d8b-131">sztring</span><span class="sxs-lookup"><span data-stu-id="c0d8b-131">string</span></span>                           | <span data-ttu-id="c0d8b-132">A hozzáférést kapott entitás bérlőazonosítója.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-132">The tenant identifier of the entity being granted access.</span></span>                                   |

## <a name="grantor"></a><span data-ttu-id="c0d8b-133">Grantor</span><span class="sxs-lookup"><span data-stu-id="c0d8b-133">Grantor</span></span>

<span data-ttu-id="c0d8b-134">Az engedélyeket megadó engedélyezőt jelöli.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-134">Represents the grantor granting the permissions.</span></span>

| <span data-ttu-id="c0d8b-135">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="c0d8b-135">Property</span></span>             | <span data-ttu-id="c0d8b-136">Típus</span><span class="sxs-lookup"><span data-stu-id="c0d8b-136">Type</span></span>|<span data-ttu-id="c0d8b-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="c0d8b-137">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="c0d8b-138">GrantorType (GrantorType)</span><span class="sxs-lookup"><span data-stu-id="c0d8b-138">GrantorType</span></span>          | <span data-ttu-id="c0d8b-139">sztring</span><span class="sxs-lookup"><span data-stu-id="c0d8b-139">string</span></span>                           | <span data-ttu-id="c0d8b-140">A hozzáférést engedélyező, elfogadott értékek: BillToPartner.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-140">The grantor granting access, accepted values: BillToPartner.</span></span>                               |
| <span data-ttu-id="c0d8b-141">TenantID (Bérlőazonosító)</span><span class="sxs-lookup"><span data-stu-id="c0d8b-141">TenantID</span></span>             | <span data-ttu-id="c0d8b-142">sztring</span><span class="sxs-lookup"><span data-stu-id="c0d8b-142">string</span></span>                           | <span data-ttu-id="c0d8b-143">A hozzáférést megadó entitás bérlőazonosítója.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-143">The tenant identifier of the entity granting access.</span></span>                                       |


## <a name="permission"></a><span data-ttu-id="c0d8b-144">Engedély</span><span class="sxs-lookup"><span data-stu-id="c0d8b-144">Permission</span></span>

<span data-ttu-id="c0d8b-145">Az önkiszolgáló szabályzatban egy engedélyt képvisel.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-145">Represents a permission in the self serve policy.</span></span>

| <span data-ttu-id="c0d8b-146">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="c0d8b-146">Property</span></span>             | <span data-ttu-id="c0d8b-147">Típus</span><span class="sxs-lookup"><span data-stu-id="c0d8b-147">Type</span></span>|<span data-ttu-id="c0d8b-148">Leírás</span><span class="sxs-lookup"><span data-stu-id="c0d8b-148">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="c0d8b-149">Erőforrás</span><span class="sxs-lookup"><span data-stu-id="c0d8b-149">Resource</span></span>             | <span data-ttu-id="c0d8b-150">sztring</span><span class="sxs-lookup"><span data-stu-id="c0d8b-150">string</span></span>                           | <span data-ttu-id="c0d8b-151">Az erőforrás-hozzáférés is biztosított: AzureReservedInstances.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-151">The resource access is being granted too: AzureReservedInstances.</span></span>                          |
| <span data-ttu-id="c0d8b-152">Művelet</span><span class="sxs-lookup"><span data-stu-id="c0d8b-152">Action</span></span>               | <span data-ttu-id="c0d8b-153">sztring</span><span class="sxs-lookup"><span data-stu-id="c0d8b-153">string</span></span>                           | <span data-ttu-id="c0d8b-154">A művelethez való hozzáférés a következő hez adható meg: Vásárlás</span><span class="sxs-lookup"><span data-stu-id="c0d8b-154">The action access is being granted for: Purchase</span></span>                                           |
