---
title: Azure-beli költési API-erőforrások
description: Megtudhatja, hogyan használhatnak a CSP-partnerek Partnerközpont API-kat a partneri és ügyfél Azure-kiadások és -használat költségvetéshez való megtekintésére és kezelésére.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 472554de1c354559d5bc4b21959c109467891806
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974318"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a><span data-ttu-id="94f8f-103">Azure-költség API-erőforrások partner- vagy ügyfél-kiadások és -használat költségvetéshez való kezeléséhez</span><span class="sxs-lookup"><span data-stu-id="94f8f-103">Azure spending API resources to manage partner or customer spending and usage against a budget</span></span> 

<span data-ttu-id="94f8f-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="94f8f-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="94f8f-105">Felhőszolgáltató (CSP) partnerek megtekinthetik és kezelhetik Azure-kiadásaikat az Partnerközpont API-kon keresztül.</span><span class="sxs-lookup"><span data-stu-id="94f8f-105">Cloud Solution Provider (CSP) partners can view and manage their Azure spending through Partner Center APIs.</span></span> <span data-ttu-id="94f8f-106">Emellett programozott módon is megtekinthetik az ügyfeleik kiadásait az Azure-költségvetéshez.</span><span class="sxs-lookup"><span data-stu-id="94f8f-106">They can also programmatically view their customers' spending against an Azure spending budget.</span></span>

<span data-ttu-id="94f8f-107">További információért tekintse meg az olyan forgatókönyveket, amelyekben a CSP-partnerek a Partnerközpont API-k használatával kezelhetik az ügyfél- és [partnerfiókokat és -rendeléseket.](scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="94f8f-107">For more information, see [scenarios in which CSP partners can use the Partner Center APIs to manage customer and partner accounts and orders](scenarios.md).</span></span>

## <a name="partner-usage-management"></a><span data-ttu-id="94f8f-108">Partnerhasználat kezelése</span><span class="sxs-lookup"><span data-stu-id="94f8f-108">Partner usage management</span></span>

- <span data-ttu-id="94f8f-109">[Partner használati összegzésének lezása](get-a-partner-usage-summary.md) a **PartnerUsageSummary erőforrás** használatával</span><span class="sxs-lookup"><span data-stu-id="94f8f-109">[Get a partner usage summary](get-a-partner-usage-summary.md) using the **PartnerUsageSummary** resource</span></span>
- <span data-ttu-id="94f8f-110">[A](get-a-customer-s-usage-records.md) **CustomerMonthlyUsageRecord** erőforrást használó összes ügyfél használati rekordjainak lekérte</span><span class="sxs-lookup"><span data-stu-id="94f8f-110">[Get usage records for all customers](get-a-customer-s-usage-records.md) using the **CustomerMonthlyUsageRecord** resource</span></span>

## <a name="customer-usage-management"></a><span data-ttu-id="94f8f-111">Ügyfélhasználat kezelése</span><span class="sxs-lookup"><span data-stu-id="94f8f-111">Customer usage management</span></span>

- <span data-ttu-id="94f8f-112">[Ügyfél használati összegzésének lezása](get-a-customer-usage-summary.md) a **CustomerUsageSummary erőforrás** használatával</span><span class="sxs-lookup"><span data-stu-id="94f8f-112">[Get a customer's usage summary](get-a-customer-usage-summary.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="94f8f-113">[Egy ügyfél összes előfizetés-használati](get-a-customer-subscription-s-usage-records.md) rekordját lekérte a **SubscriptionMonthlyUsageRecord erőforrás** használatával</span><span class="sxs-lookup"><span data-stu-id="94f8f-113">[Get all subscription usage records for a customer](get-a-customer-subscription-s-usage-records.md) using the **SubscriptionMonthlyUsageRecord** resource</span></span>

## <a name="subscription-usage-management"></a><span data-ttu-id="94f8f-114">Előfizetés használatának kezelése</span><span class="sxs-lookup"><span data-stu-id="94f8f-114">Subscription usage management</span></span>

- <span data-ttu-id="94f8f-115">[Az előfizetés használatának összegzése a](get-a-customer-subscription-usage-summary.md) **SubscriptionUsageSummary erőforrás** használatával</span><span class="sxs-lookup"><span data-stu-id="94f8f-115">[Get a subscription usage summary](get-a-customer-subscription-usage-summary.md) using the **SubscriptionUsageSummary** resource</span></span>
- <span data-ttu-id="94f8f-116">[Előfizetés összes havi használati rekordját](get-all-monthly-usage-records-for-a-subscription.md) lekérte az **AzureResourceMonthlyUsageRecord erőforrás** használatával</span><span class="sxs-lookup"><span data-stu-id="94f8f-116">[Get all monthly usage records for a subscription](get-all-monthly-usage-records-for-a-subscription.md) using the **AzureResourceMonthlyUsageRecord** resource</span></span>
- <span data-ttu-id="94f8f-117">[Előfizetés használati adatainak lekérte erőforrás szerint](get-a-customer-subscription-resource-usage-records.md) a **ResourceUsageRecord erőforrás** használatával</span><span class="sxs-lookup"><span data-stu-id="94f8f-117">[Get usage data for a subscription by resource](get-a-customer-subscription-resource-usage-records.md) using the **ResourceUsageRecord** resource</span></span>
- <span data-ttu-id="94f8f-118">[Használati adatok lekérte egy előfizetés használati adatait fogyasztásmérő alapján](get-a-customer-subscription-meter-usage-records.md) a **MeterUsageRecord erőforrás** használatával</span><span class="sxs-lookup"><span data-stu-id="94f8f-118">[Get usage data for a subscription by meter](get-a-customer-subscription-meter-usage-records.md) using the **MeterUsageRecord** resource</span></span>

## <a name="azure-spending-budget-management"></a><span data-ttu-id="94f8f-119">Azure-költségvetések kezelése</span><span class="sxs-lookup"><span data-stu-id="94f8f-119">Azure spending budget management</span></span>

- <span data-ttu-id="94f8f-120">[Az ügyfél használati költségvetésének lekérte](get-a-customer-s-usage-spending-budget.md) a **CustomerUsageSummary erőforrást**</span><span class="sxs-lookup"><span data-stu-id="94f8f-120">[Get a customer's usage budget](get-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="94f8f-121">[Ügyfél használati költségvetésének frissítése](update-a-customer-s-usage-spending-budget.md) a **CustomerUsageSummary erőforrás** használatával</span><span class="sxs-lookup"><span data-stu-id="94f8f-121">[Update a customer's usage budget](update-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
