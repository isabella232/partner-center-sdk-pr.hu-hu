---
title: Felügyelt szolgáltatás erőforrásai
description: A felügyelt szolgáltatások olyan szolgáltatások, amelyekhez a partner delegált rendszergazdai jogosultságokkal rendelkezik. A partnerek a felügyelt szolgáltatásaik nevében nyújthatnak támogatást a és a Fájlszolgáltatások számára.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767783"
---
# <a name="managed-service-resources"></a><span data-ttu-id="0a315-104">Felügyelt szolgáltatás erőforrásai</span><span class="sxs-lookup"><span data-stu-id="0a315-104">Managed service resources</span></span>

<span data-ttu-id="0a315-105">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="0a315-105">**Applies To**</span></span>

- <span data-ttu-id="0a315-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="0a315-106">Partner Center</span></span>
- <span data-ttu-id="0a315-107">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="0a315-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="0a315-108">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="0a315-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0a315-109">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="0a315-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0a315-110">A felügyelt szolgáltatások olyan szolgáltatások, amelyekhez a partner delegált rendszergazdai jogosultságokkal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="0a315-110">Managed services are services to which a partner has delegated admin privileges.</span></span> <span data-ttu-id="0a315-111">A partnerek a felügyelt szolgáltatásaik nevében nyújthatnak támogatást a és a Fájlszolgáltatások számára.</span><span class="sxs-lookup"><span data-stu-id="0a315-111">Partners can provide support for and file service requests on the behalf of their managed services.</span></span>

## <a name="managedservice"></a><span data-ttu-id="0a315-112">ManagedService</span><span class="sxs-lookup"><span data-stu-id="0a315-112">ManagedService</span></span>

<span data-ttu-id="0a315-113">A felügyelt szolgáltatás leírása.</span><span class="sxs-lookup"><span data-stu-id="0a315-113">Describes a managed service.</span></span>

| <span data-ttu-id="0a315-114">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="0a315-114">Property</span></span>   | <span data-ttu-id="0a315-115">Típus</span><span class="sxs-lookup"><span data-stu-id="0a315-115">Type</span></span>                | <span data-ttu-id="0a315-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="0a315-116">Description</span></span>                                              |
|------------|---------------------|----------------------------------------------------------|
| <span data-ttu-id="0a315-117">Id</span><span class="sxs-lookup"><span data-stu-id="0a315-117">Id</span></span>         | <span data-ttu-id="0a315-118">sztring</span><span class="sxs-lookup"><span data-stu-id="0a315-118">string</span></span>              | <span data-ttu-id="0a315-119">A felügyelt szolgáltatás azonosítója.</span><span class="sxs-lookup"><span data-stu-id="0a315-119">The managed service id.</span></span>                                  |
| <span data-ttu-id="0a315-120">Name</span><span class="sxs-lookup"><span data-stu-id="0a315-120">Name</span></span>       | <span data-ttu-id="0a315-121">sztring</span><span class="sxs-lookup"><span data-stu-id="0a315-121">string</span></span>              | <span data-ttu-id="0a315-122">A felügyelt szolgáltatás neve.</span><span class="sxs-lookup"><span data-stu-id="0a315-122">The name of the managed service.</span></span>                         |
| <span data-ttu-id="0a315-123">GroupName</span><span class="sxs-lookup"><span data-stu-id="0a315-123">GroupName</span></span>  | <span data-ttu-id="0a315-124">sztring</span><span class="sxs-lookup"><span data-stu-id="0a315-124">string</span></span>              | <span data-ttu-id="0a315-125">Annak a csoportnak a neve, amelyhez a szolgáltatás tartozik.</span><span class="sxs-lookup"><span data-stu-id="0a315-125">The name of the group to which the service belongs.</span></span>      |
| <span data-ttu-id="0a315-126">Hivatkozások</span><span class="sxs-lookup"><span data-stu-id="0a315-126">Links</span></span>      | <span data-ttu-id="0a315-127">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="0a315-127">ManagedServiceLinks</span></span> | <span data-ttu-id="0a315-128">A felügyelt szolgáltatásnak megfelelő erőforrás-hivatkozások.</span><span class="sxs-lookup"><span data-stu-id="0a315-128">The resource links corresponding to the managed service.</span></span> |
| <span data-ttu-id="0a315-129">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="0a315-129">Attributes</span></span> | <span data-ttu-id="0a315-130">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="0a315-130">ResourceAttributes</span></span>  | <span data-ttu-id="0a315-131">A szerződéshez tartozó metaadat-attribútumok.</span><span class="sxs-lookup"><span data-stu-id="0a315-131">The metadata attributes corresponding to the agreement.</span></span>  |

## <a name="managedservicelinks"></a><span data-ttu-id="0a315-132">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="0a315-132">ManagedServiceLinks</span></span>

<span data-ttu-id="0a315-133">Azokat a hivatkozásokat tartalmazza, amelyek lehetővé teszik, hogy a partner delegált rendszergazdai jogosultságokkal támogassa a szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="0a315-133">Contains the links that allow the partner with delegated admin permissions to provide support for the service.</span></span>

| <span data-ttu-id="0a315-134">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="0a315-134">Property</span></span>      | <span data-ttu-id="0a315-135">Típus</span><span class="sxs-lookup"><span data-stu-id="0a315-135">Type</span></span> | <span data-ttu-id="0a315-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="0a315-136">Description</span></span>                 |
|---------------|------|-----------------------------|
| <span data-ttu-id="0a315-137">AdminService</span><span class="sxs-lookup"><span data-stu-id="0a315-137">AdminService</span></span>  | <span data-ttu-id="0a315-138">Hivatkozás</span><span class="sxs-lookup"><span data-stu-id="0a315-138">Link</span></span> | <span data-ttu-id="0a315-139">A felügyeleti szolgáltatás URI-ja.</span><span class="sxs-lookup"><span data-stu-id="0a315-139">The admin service URI.</span></span>      |
| <span data-ttu-id="0a315-140">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="0a315-140">ServiceHealth</span></span> | <span data-ttu-id="0a315-141">Hivatkozás</span><span class="sxs-lookup"><span data-stu-id="0a315-141">Link</span></span> | <span data-ttu-id="0a315-142">A szolgáltatás állapota URI-ja.</span><span class="sxs-lookup"><span data-stu-id="0a315-142">The service health URI.</span></span>     |
| <span data-ttu-id="0a315-143">ServiceTicket</span><span class="sxs-lookup"><span data-stu-id="0a315-143">ServiceTicket</span></span> | <span data-ttu-id="0a315-144">Hivatkozás</span><span class="sxs-lookup"><span data-stu-id="0a315-144">Link</span></span> | <span data-ttu-id="0a315-145">A szolgáltatás jegyének URI-ja.</span><span class="sxs-lookup"><span data-stu-id="0a315-145">The service ticket URI.</span></span>     |
| <span data-ttu-id="0a315-146">Self</span><span class="sxs-lookup"><span data-stu-id="0a315-146">Self</span></span>          | <span data-ttu-id="0a315-147">Hivatkozás</span><span class="sxs-lookup"><span data-stu-id="0a315-147">Link</span></span> | <span data-ttu-id="0a315-148">A saját URI-ja.</span><span class="sxs-lookup"><span data-stu-id="0a315-148">The self URI.</span></span>               |
| <span data-ttu-id="0a315-149">Következő</span><span class="sxs-lookup"><span data-stu-id="0a315-149">Next</span></span>          | <span data-ttu-id="0a315-150">Hivatkozás</span><span class="sxs-lookup"><span data-stu-id="0a315-150">Link</span></span> | <span data-ttu-id="0a315-151">Az elemek következő lapja.</span><span class="sxs-lookup"><span data-stu-id="0a315-151">The next page of items.</span></span>     |
| <span data-ttu-id="0a315-152">Előző</span><span class="sxs-lookup"><span data-stu-id="0a315-152">Previous</span></span>      | <span data-ttu-id="0a315-153">Hivatkozás</span><span class="sxs-lookup"><span data-stu-id="0a315-153">Link</span></span> | <span data-ttu-id="0a315-154">Az elemek előző lapja.</span><span class="sxs-lookup"><span data-stu-id="0a315-154">The previous page of items.</span></span> |

