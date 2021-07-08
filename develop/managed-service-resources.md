---
title: Felügyelt szolgáltatási erőforrások
description: A felügyelt szolgáltatások olyan szolgáltatások, amelyekhez a partner rendszergazdai jogosultságokat delegált. A partnerek támogatást és fájlszolgáltatás-kéréseket nyújthatnak a felügyelt szolgáltatásaik nevében.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 582efe75fd18a9174dd5dc173c290bee25443ee9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548124"
---
# <a name="managed-service-resources"></a><span data-ttu-id="415e0-104">Felügyelt szolgáltatási erőforrások</span><span class="sxs-lookup"><span data-stu-id="415e0-104">Managed service resources</span></span>

<span data-ttu-id="415e0-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="415e0-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="415e0-106">A felügyelt szolgáltatások olyan szolgáltatások, amelyekhez a partner rendszergazdai jogosultságokat delegált.</span><span class="sxs-lookup"><span data-stu-id="415e0-106">Managed services are services to which a partner has delegated admin privileges.</span></span> <span data-ttu-id="415e0-107">A partnerek támogatást és fájlszolgáltatás-kéréseket nyújthatnak a felügyelt szolgáltatásaik nevében.</span><span class="sxs-lookup"><span data-stu-id="415e0-107">Partners can provide support for and file service requests on the behalf of their managed services.</span></span>

## <a name="managedservice"></a><span data-ttu-id="415e0-108">ManagedService</span><span class="sxs-lookup"><span data-stu-id="415e0-108">ManagedService</span></span>

<span data-ttu-id="415e0-109">Egy felügyelt szolgáltatást ismertet.</span><span class="sxs-lookup"><span data-stu-id="415e0-109">Describes a managed service.</span></span>

| <span data-ttu-id="415e0-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="415e0-110">Property</span></span>   | <span data-ttu-id="415e0-111">Típus</span><span class="sxs-lookup"><span data-stu-id="415e0-111">Type</span></span>                | <span data-ttu-id="415e0-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="415e0-112">Description</span></span>                                              |
|------------|---------------------|----------------------------------------------------------|
| <span data-ttu-id="415e0-113">Id</span><span class="sxs-lookup"><span data-stu-id="415e0-113">Id</span></span>         | <span data-ttu-id="415e0-114">sztring</span><span class="sxs-lookup"><span data-stu-id="415e0-114">string</span></span>              | <span data-ttu-id="415e0-115">A felügyelt szolgáltatás azonosítója.</span><span class="sxs-lookup"><span data-stu-id="415e0-115">The managed service ID.</span></span>                                  |
| <span data-ttu-id="415e0-116">Name</span><span class="sxs-lookup"><span data-stu-id="415e0-116">Name</span></span>       | <span data-ttu-id="415e0-117">sztring</span><span class="sxs-lookup"><span data-stu-id="415e0-117">string</span></span>              | <span data-ttu-id="415e0-118">A felügyelt szolgáltatás neve.</span><span class="sxs-lookup"><span data-stu-id="415e0-118">The name of the managed service.</span></span>                         |
| <span data-ttu-id="415e0-119">GroupName (Csoportnév)</span><span class="sxs-lookup"><span data-stu-id="415e0-119">GroupName</span></span>  | <span data-ttu-id="415e0-120">sztring</span><span class="sxs-lookup"><span data-stu-id="415e0-120">string</span></span>              | <span data-ttu-id="415e0-121">Annak a csoportnak a neve, amelyhez a szolgáltatás tartozik.</span><span class="sxs-lookup"><span data-stu-id="415e0-121">The name of the group to which the service belongs.</span></span>      |
| <span data-ttu-id="415e0-122">Hivatkozások</span><span class="sxs-lookup"><span data-stu-id="415e0-122">Links</span></span>      | <span data-ttu-id="415e0-123">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="415e0-123">ManagedServiceLinks</span></span> | <span data-ttu-id="415e0-124">A felügyelt szolgáltatásnak megfelelő erőforrás-hivatkozások.</span><span class="sxs-lookup"><span data-stu-id="415e0-124">The resource links corresponding to the managed service.</span></span> |
| <span data-ttu-id="415e0-125">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="415e0-125">Attributes</span></span> | <span data-ttu-id="415e0-126">ResourceAttributes (Erőforrás-attribútumok)</span><span class="sxs-lookup"><span data-stu-id="415e0-126">ResourceAttributes</span></span>  | <span data-ttu-id="415e0-127">A szerződésnek megfelelő metaadat-attribútumok.</span><span class="sxs-lookup"><span data-stu-id="415e0-127">The metadata attributes corresponding to the agreement.</span></span>  |

## <a name="managedservicelinks"></a><span data-ttu-id="415e0-128">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="415e0-128">ManagedServiceLinks</span></span>

<span data-ttu-id="415e0-129">Tartalmazza azokat a hivatkozásokat, amelyek lehetővé teszik, hogy a delegált rendszergazdai engedélyekkel rendelkező partner támogatást nyújtson a szolgáltatáshoz.</span><span class="sxs-lookup"><span data-stu-id="415e0-129">Contains the links that allow the partner with delegated admin permissions to provide support for the service.</span></span>

| <span data-ttu-id="415e0-130">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="415e0-130">Property</span></span>      | <span data-ttu-id="415e0-131">Típus</span><span class="sxs-lookup"><span data-stu-id="415e0-131">Type</span></span> | <span data-ttu-id="415e0-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="415e0-132">Description</span></span>                 |
|---------------|------|-----------------------------|
| <span data-ttu-id="415e0-133">AdminService</span><span class="sxs-lookup"><span data-stu-id="415e0-133">AdminService</span></span>  | <span data-ttu-id="415e0-134">Hivatkozás</span><span class="sxs-lookup"><span data-stu-id="415e0-134">Link</span></span> | <span data-ttu-id="415e0-135">A felügyeleti szolgáltatás URI-ját.</span><span class="sxs-lookup"><span data-stu-id="415e0-135">The admin service URI.</span></span>      |
| <span data-ttu-id="415e0-136">ServiceHealth (Szolgáltatás-egészség)</span><span class="sxs-lookup"><span data-stu-id="415e0-136">ServiceHealth</span></span> | <span data-ttu-id="415e0-137">Hivatkozás</span><span class="sxs-lookup"><span data-stu-id="415e0-137">Link</span></span> | <span data-ttu-id="415e0-138">A szolgáltatás állapot-URI-ját.</span><span class="sxs-lookup"><span data-stu-id="415e0-138">The service health URI.</span></span>     |
| <span data-ttu-id="415e0-139">ServiceTicket (Szolgáltatáscsomóta)</span><span class="sxs-lookup"><span data-stu-id="415e0-139">ServiceTicket</span></span> | <span data-ttu-id="415e0-140">Hivatkozás</span><span class="sxs-lookup"><span data-stu-id="415e0-140">Link</span></span> | <span data-ttu-id="415e0-141">A szolgáltatásjegy URI-ját.</span><span class="sxs-lookup"><span data-stu-id="415e0-141">The service ticket URI.</span></span>     |
| <span data-ttu-id="415e0-142">Self</span><span class="sxs-lookup"><span data-stu-id="415e0-142">Self</span></span>          | <span data-ttu-id="415e0-143">Hivatkozás</span><span class="sxs-lookup"><span data-stu-id="415e0-143">Link</span></span> | <span data-ttu-id="415e0-144">Az ön-URI.</span><span class="sxs-lookup"><span data-stu-id="415e0-144">The self-URI.</span></span>               |
| <span data-ttu-id="415e0-145">Következő</span><span class="sxs-lookup"><span data-stu-id="415e0-145">Next</span></span>          | <span data-ttu-id="415e0-146">Hivatkozás</span><span class="sxs-lookup"><span data-stu-id="415e0-146">Link</span></span> | <span data-ttu-id="415e0-147">Az elemek következő oldala.</span><span class="sxs-lookup"><span data-stu-id="415e0-147">The next page of items.</span></span>     |
| <span data-ttu-id="415e0-148">Előző</span><span class="sxs-lookup"><span data-stu-id="415e0-148">Previous</span></span>      | <span data-ttu-id="415e0-149">Hivatkozás</span><span class="sxs-lookup"><span data-stu-id="415e0-149">Link</span></span> | <span data-ttu-id="415e0-150">Az elemek előző oldala.</span><span class="sxs-lookup"><span data-stu-id="415e0-150">The previous page of items.</span></span> |

