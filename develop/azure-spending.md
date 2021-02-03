---
title: Azure-kiadások API-erőforrásai
description: Ismerje meg, hogy a CSP-partnerek hogyan használhatják a partner Center API-kat a partnerek és az ügyfelek Azure-beli kiadásainak és használatának a költségvetésen keresztüli megtekintéséhez
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 02a2995a06473cc6990d1234acd522a3b38a03d3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768539"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a><span data-ttu-id="0a2a4-103">Az Azure-kiadások API-erőforrásai a partneri és az ügyfél-kiadások, valamint a költségvetéssel való használat kezeléséhez</span><span class="sxs-lookup"><span data-stu-id="0a2a4-103">Azure spending API resources to manage partner or customer spending and usage against a budget</span></span> 

<span data-ttu-id="0a2a4-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="0a2a4-104">**Applies to:**</span></span>

- <span data-ttu-id="0a2a4-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="0a2a4-105">Partner Center</span></span>
- <span data-ttu-id="0a2a4-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="0a2a4-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="0a2a4-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="0a2a4-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0a2a4-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="0a2a4-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0a2a4-109">A Cloud Solution Provider (CSP) partnerei a partner Center API-kon keresztül tekinthetik meg és kezelhetik az Azure-kiadásokat.</span><span class="sxs-lookup"><span data-stu-id="0a2a4-109">Cloud Solution Provider (CSP) partners can view and manage their Azure spending through Partner Center APIs.</span></span> <span data-ttu-id="0a2a4-110">Emellett programozott módon megtekinthetik az ügyfeleik költségeit az Azure-kiadások költségvetésében.</span><span class="sxs-lookup"><span data-stu-id="0a2a4-110">They can also programmatically view their customers' spending against an Azure spending budget.</span></span>

<span data-ttu-id="0a2a4-111">További információ: [olyan forgatókönyvek, amelyekben a CSP-partnerek a partner Center API-kkal kezelhetik az ügyfél-és partneri fiókokat és a rendeléseket](scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="0a2a4-111">For more information, see [scenarios in which CSP partners can use the Partner Center APIs to manage customer and partner accounts and orders](scenarios.md).</span></span>

## <a name="partner-usage-management"></a><span data-ttu-id="0a2a4-112">Partneri használat kezelése</span><span class="sxs-lookup"><span data-stu-id="0a2a4-112">Partner usage management</span></span>

- <span data-ttu-id="0a2a4-113">[Partner-használat összesítésének beszerzése](get-a-partner-usage-summary.md) a **PartnerUsageSummary** -erőforrás használatával</span><span class="sxs-lookup"><span data-stu-id="0a2a4-113">[Get a partner usage summary](get-a-partner-usage-summary.md) using the **PartnerUsageSummary** resource</span></span>
- <span data-ttu-id="0a2a4-114">A **CustomerMonthlyUsageRecord** -erőforrást használó [összes ügyfél használati rekordjainak lekérése](get-a-customer-s-usage-records.md)</span><span class="sxs-lookup"><span data-stu-id="0a2a4-114">[Get usage records for all customers](get-a-customer-s-usage-records.md) using the **CustomerMonthlyUsageRecord** resource</span></span>

## <a name="customer-usage-management"></a><span data-ttu-id="0a2a4-115">Ügyfél-használati felügyelet</span><span class="sxs-lookup"><span data-stu-id="0a2a4-115">Customer usage management</span></span>

- <span data-ttu-id="0a2a4-116">[Ügyfél használati összegzésének beszerzése](get-a-customer-usage-summary.md) a **CustomerUsageSummary** -erőforrás használatával</span><span class="sxs-lookup"><span data-stu-id="0a2a4-116">[Get a customer's usage summary](get-a-customer-usage-summary.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="0a2a4-117">Az [ügyfél összes előfizetés-használati rekordjának lekérése](get-a-customer-subscription-s-usage-records.md) az **SubscriptionMonthlyUsageRecord** erőforrás használatával</span><span class="sxs-lookup"><span data-stu-id="0a2a4-117">[Get all subscription usage records for a customer](get-a-customer-subscription-s-usage-records.md) using the **SubscriptionMonthlyUsageRecord** resource</span></span>

## <a name="subscription-usage-management"></a><span data-ttu-id="0a2a4-118">Előfizetés-használat kezelése</span><span class="sxs-lookup"><span data-stu-id="0a2a4-118">Subscription usage management</span></span>

- <span data-ttu-id="0a2a4-119">[Előfizetés-használati összefoglalás beszerzése](get-a-customer-subscription-usage-summary.md) a **SubscriptionUsageSummary** -erőforrás használatával</span><span class="sxs-lookup"><span data-stu-id="0a2a4-119">[Get a subscription usage summary](get-a-customer-subscription-usage-summary.md) using the **SubscriptionUsageSummary** resource</span></span>
- <span data-ttu-id="0a2a4-120">Az [előfizetéshez tartozó összes havi használati rekord beolvasása](get-all-monthly-usage-records-for-a-subscription.md) a **AzureResourceMonthlyUsageRecord** -erőforrás használatával</span><span class="sxs-lookup"><span data-stu-id="0a2a4-120">[Get all monthly usage records for a subscription](get-all-monthly-usage-records-for-a-subscription.md) using the **AzureResourceMonthlyUsageRecord** resource</span></span>
- <span data-ttu-id="0a2a4-121">[Előfizetéshez tartozó használati adatok lekérése erőforrás alapján](get-a-customer-subscription-resource-usage-records.md) a **ResourceUsageRecord** -erőforrás használatával</span><span class="sxs-lookup"><span data-stu-id="0a2a4-121">[Get usage data for a subscription by resource](get-a-customer-subscription-resource-usage-records.md) using the **ResourceUsageRecord** resource</span></span>
- <span data-ttu-id="0a2a4-122">Az [előfizetéshez tartozó használati adatok lekérése](get-a-customer-subscription-meter-usage-records.md) a **MeterUsageRecord** -erőforrás használatával</span><span class="sxs-lookup"><span data-stu-id="0a2a4-122">[Get usage data for a subscription by meter](get-a-customer-subscription-meter-usage-records.md) using the **MeterUsageRecord** resource</span></span>

## <a name="azure-spending-budget-management"></a><span data-ttu-id="0a2a4-123">Az Azure költségvetés-kezelési kiadásai</span><span class="sxs-lookup"><span data-stu-id="0a2a4-123">Azure spending budget management</span></span>

- <span data-ttu-id="0a2a4-124">[Ügyfél használati költségkeretének beszerzése](get-a-customer-s-usage-spending-budget.md) a **CustomerUsageSummary** -erőforrás használatával</span><span class="sxs-lookup"><span data-stu-id="0a2a4-124">[Get a customer's usage budget](get-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="0a2a4-125">[Ügyfél használati költségkeretének frissítése](update-a-customer-s-usage-spending-budget.md) a **CustomerUsageSummary** -erőforrás használatával</span><span class="sxs-lookup"><span data-stu-id="0a2a4-125">[Update a customer's usage budget](update-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
