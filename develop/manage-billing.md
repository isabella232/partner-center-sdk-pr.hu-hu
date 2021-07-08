---
title: Számlázás kezelése
description: Ez a szakasz azt ismerteti Felhőszolgáltató hogyan használhatják a Partnerközpont-t a számlák programozott módon történő megtekintésére és kezelésére, valamint az ügyfelek előrehaladásának az Azure-költségkerethez való vetésében.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: eaf6a426d0702130f31f08a4a30ccdfa00810270
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548362"
---
# <a name="manage-billing"></a><span data-ttu-id="49326-103">Számlázás kezelése</span><span class="sxs-lookup"><span data-stu-id="49326-103">Manage billing</span></span>

<span data-ttu-id="49326-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="49326-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="49326-105">Ez a szakasz azt ismerteti, hogy Felhőszolgáltató hogyan használhatnak Partnerközpont-partnerek a számlák programozott módon történő megtekintésére és kezelésére, valamint az ügyfelek előrehaladásának az Azure-költségkerethez való vetésére.</span><span class="sxs-lookup"><span data-stu-id="49326-105">This section describes the ways that Cloud Solution Provider partners can use Partner Center to programmatically view and manage their invoices, and view their customer's progress against an Azure spending budget.</span></span>

<span data-ttu-id="49326-106">**Számlázási ciklus:**</span><span class="sxs-lookup"><span data-stu-id="49326-106">**Billing Cycle:**</span></span>
- [<span data-ttu-id="49326-107">A számlázási ciklus módosítása</span><span class="sxs-lookup"><span data-stu-id="49326-107">Change the billing cycle</span></span>](change-the-billing-cycle.md)

<span data-ttu-id="49326-108">**Az Azure díjszabása és kihasználtsága:**</span><span class="sxs-lookup"><span data-stu-id="49326-108">**Azure rates and utilization:**</span></span>
- [<span data-ttu-id="49326-109">Ügyfél Azure-használati rekordjainak lekérése</span><span class="sxs-lookup"><span data-stu-id="49326-109">Get a customer's utilization records for Azure</span></span>](get-a-customer-s-utilization-record-for-azure.md)
- [<span data-ttu-id="49326-110">Díjak lekérése a Microsoft Azure-tól</span><span class="sxs-lookup"><span data-stu-id="49326-110">Get prices for Microsoft Azure</span></span>](get-prices-for-microsoft-azure.md)

<span data-ttu-id="49326-111">**Számlák:**</span><span class="sxs-lookup"><span data-stu-id="49326-111">**Invoices:**</span></span>
- [<span data-ttu-id="49326-112">Számlák gyűjteményének lekérése</span><span class="sxs-lookup"><span data-stu-id="49326-112">Get a collection of invoices</span></span>](get-a-collection-of-invoices.md)
- [<span data-ttu-id="49326-113">Számlabecslés hivatkozásainak lekérése</span><span class="sxs-lookup"><span data-stu-id="49326-113">Get invoice estimate links</span></span>](get-invoice-estimate-links.md)
- [<span data-ttu-id="49326-114">Számlázott kereskedelmi piactéri használatsorelemek lekért száma</span><span class="sxs-lookup"><span data-stu-id="49326-114">Get invoice billed commercial marketplace consumption line items</span></span>](get-invoice-billed-consumption-lineitems.md)
- [<span data-ttu-id="49326-115">Számla lekérte azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="49326-115">Get invoice by ID</span></span>](get-invoice-by-id.md)
- [<span data-ttu-id="49326-116">Számla sorelemeinek lekérése</span><span class="sxs-lookup"><span data-stu-id="49326-116">Get invoice line items</span></span>](get-invoiceline-items.md)
- [<span data-ttu-id="49326-117">Számla nyugtakivonatának lekérése</span><span class="sxs-lookup"><span data-stu-id="49326-117">Get invoice receipt statement</span></span>](get-invoice-receipt-statement.md)
- [<span data-ttu-id="49326-118">Számlakivonat lekérése</span><span class="sxs-lookup"><span data-stu-id="49326-118">Get invoice statement</span></span>](get-invoice-statement.md)
- [<span data-ttu-id="49326-119">Számla összegzéseinek lekérése</span><span class="sxs-lookup"><span data-stu-id="49326-119">Get invoice summaries</span></span>](get-invoice-summaries.md)
- [<span data-ttu-id="49326-120">Számlázatlan kereskedelmi piactéri használatsorelemek lekért száma</span><span class="sxs-lookup"><span data-stu-id="49326-120">Get invoice unbilled commercial marketplace consumption line items</span></span>](get-invoice-unbilled-consumption-lineitems.md)
- [<span data-ttu-id="49326-121">Nem számlázott egyeztetési sorelemek lekérése</span><span class="sxs-lookup"><span data-stu-id="49326-121">Get invoice unbilled recon line items</span></span>](get-invoice-unbilled-recon-lineitems.md)
- [<span data-ttu-id="49326-122">A viszonteladó aktuális számlaegyenlegének lekért egyenlege</span><span class="sxs-lookup"><span data-stu-id="49326-122">Get the reseller's current account balance</span></span>](get-the-reseller-s-current-account-balance.md)

<span data-ttu-id="49326-123">**Azure-költségvetés:**</span><span class="sxs-lookup"><span data-stu-id="49326-123">**Azure spending budget:**</span></span>
- <span data-ttu-id="49326-124">[Használati adatok lekérte egy előfizetéshez] (get-all-monthly-usage-records-for-a-subscription.md</span><span class="sxs-lookup"><span data-stu-id="49326-124">[Get usage data for a subscription](get-all-monthly-usage-records-for-a-subscription.md</span></span>
- [<span data-ttu-id="49326-125">Az ügyfél összes előfizetésének használati összegzése</span><span class="sxs-lookup"><span data-stu-id="49326-125">Get usage summary for all of a customer's subscriptions</span></span>](get-a-customer-usage-summary.md)

<span data-ttu-id="49326-126">További információ: [Forgatókönyvek.](scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="49326-126">For more information, see [Scenarios](scenarios.md).</span></span>
