---
title: Számlázás kezelése
description: Ez a szakasz azokat a módszereket ismerteti, amelyekkel a felhőalapú megoldások szolgáltatói partnerei a partner központ használatával programozott módon tekinthetik meg és kezelhetik a számlákat, és megtekinthetik ügyfeleik előrehaladását az Azure-kiadások költségvetésében.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 4d5995ea2abb5968c5ca459b8412b12dfdbbc47b
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768203"
---
# <a name="manage-billing"></a><span data-ttu-id="e97cf-103">Számlázás kezelése</span><span class="sxs-lookup"><span data-stu-id="e97cf-103">Manage billing</span></span>

<span data-ttu-id="e97cf-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="e97cf-104">**Applies To**</span></span>

- <span data-ttu-id="e97cf-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="e97cf-105">Partner Center</span></span>
- <span data-ttu-id="e97cf-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="e97cf-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e97cf-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="e97cf-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e97cf-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="e97cf-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e97cf-109">Ez a szakasz azokat a módszereket ismerteti, amelyekkel a felhőalapú megoldások szolgáltatói partnerei a partner központ használatával programozott módon tekinthetik meg és kezelhetik a számláit, és megtekinthetik ügyfeleik előrehaladását az Azure-kiadások költségkeretén keresztül.</span><span class="sxs-lookup"><span data-stu-id="e97cf-109">This section describes the ways that Cloud Solution Provider partners can use Partner Center to programmatically view and manage their invoices, and view their customer's progress against an Azure spending budget.</span></span>

<span data-ttu-id="e97cf-110">**Számlázási ciklus:**</span><span class="sxs-lookup"><span data-stu-id="e97cf-110">**Billing Cycle:**</span></span>
- [<span data-ttu-id="e97cf-111">A számlázási ciklus módosítása</span><span class="sxs-lookup"><span data-stu-id="e97cf-111">Change the billing cycle</span></span>](change-the-billing-cycle.md)

<span data-ttu-id="e97cf-112">**Az Azure díjszabása és kihasználtsága:**</span><span class="sxs-lookup"><span data-stu-id="e97cf-112">**Azure rates and utilization:**</span></span>
- [<span data-ttu-id="e97cf-113">Ügyfél Azure-használati rekordjainak lekérése</span><span class="sxs-lookup"><span data-stu-id="e97cf-113">Get a customer's utilization records for Azure</span></span>](get-a-customer-s-utilization-record-for-azure.md)
- [<span data-ttu-id="e97cf-114">Díjak lekérése a Microsoft Azure-tól</span><span class="sxs-lookup"><span data-stu-id="e97cf-114">Get prices for Microsoft Azure</span></span>](get-prices-for-microsoft-azure.md)

<span data-ttu-id="e97cf-115">**Számlák**</span><span class="sxs-lookup"><span data-stu-id="e97cf-115">**Invoices:**</span></span>
- [<span data-ttu-id="e97cf-116">Számlák gyűjteményének lekérése</span><span class="sxs-lookup"><span data-stu-id="e97cf-116">Get a collection of invoices</span></span>](get-a-collection-of-invoices.md)
- [<span data-ttu-id="e97cf-117">Számlabecslés hivatkozásainak lekérése</span><span class="sxs-lookup"><span data-stu-id="e97cf-117">Get invoice estimate links</span></span>](get-invoice-estimate-links.md)
- [<span data-ttu-id="e97cf-118">Számlázott kereskedelmi piactér-felhasználási sorok számlájának beolvasása</span><span class="sxs-lookup"><span data-stu-id="e97cf-118">Get invoice billed commercial marketplace consumption line items</span></span>](get-invoice-billed-consumption-lineitems.md)
- [<span data-ttu-id="e97cf-119">Számla beolvasása azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="e97cf-119">Get invoice by ID</span></span>](get-invoice-by-id.md)
- [<span data-ttu-id="e97cf-120">Számla sorelemeinek lekérése</span><span class="sxs-lookup"><span data-stu-id="e97cf-120">Get invoice line items</span></span>](get-invoiceline-items.md)
- [<span data-ttu-id="e97cf-121">Számla nyugtakivonatának lekérése</span><span class="sxs-lookup"><span data-stu-id="e97cf-121">Get invoice receipt statement</span></span>](get-invoice-receipt-statement.md)
- [<span data-ttu-id="e97cf-122">Számlakivonat lekérése</span><span class="sxs-lookup"><span data-stu-id="e97cf-122">Get invoice statement</span></span>](get-invoice-statement.md)
- [<span data-ttu-id="e97cf-123">Számla összegzéseinek lekérése</span><span class="sxs-lookup"><span data-stu-id="e97cf-123">Get invoice summaries</span></span>](get-invoice-summaries.md)
- [<span data-ttu-id="e97cf-124">Számlázott kereskedelmi piactér-felhasználási sorok számlázása</span><span class="sxs-lookup"><span data-stu-id="e97cf-124">Get invoice unbilled commercial marketplace consumption line items</span></span>](get-invoice-unbilled-consumption-lineitems.md)
- [<span data-ttu-id="e97cf-125">Nem számlázott egyeztetési sorelemek lekérése</span><span class="sxs-lookup"><span data-stu-id="e97cf-125">Get invoice unbilled recon line items</span></span>](get-invoice-unbilled-recon-lineitems.md)
- [<span data-ttu-id="e97cf-126">A viszonteladó aktuális fiókjának egyenlegének beolvasása</span><span class="sxs-lookup"><span data-stu-id="e97cf-126">Get the reseller's current account balance</span></span>](get-the-reseller-s-current-account-balance.md)

<span data-ttu-id="e97cf-127">**Azure-kiadások költségvetése:**</span><span class="sxs-lookup"><span data-stu-id="e97cf-127">**Azure spending budget:**</span></span>
- <span data-ttu-id="e97cf-128">[Előfizetéshez tartozó használati adatok beolvasása] (get-all-monthly-usage-records-for-a-subscription.md</span><span class="sxs-lookup"><span data-stu-id="e97cf-128">[Get usage data for a subscription](get-all-monthly-usage-records-for-a-subscription.md</span></span>
- [<span data-ttu-id="e97cf-129">Az ügyfél-előfizetések használati összegzésének beolvasása</span><span class="sxs-lookup"><span data-stu-id="e97cf-129">Get usage summary for all of a customer's subscriptions</span></span>](get-a-customer-usage-summary.md)

<span data-ttu-id="e97cf-130">További információ: [forgatókönyvek](scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="e97cf-130">For more information, see [Scenarios](scenarios.md).</span></span>
