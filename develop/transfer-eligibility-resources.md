---
title: TransferEligibility-erőforrások
description: Egy partner akkor hozza létre az átvitelt, ha az ügyfél előfizetését a partnerrel egy másik partnernek kívánja átvinni.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac5724a1f708bc540a3aac7ce74b2eda60a296
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767848"
---
# <a name="transfereligibility-resources"></a><span data-ttu-id="33408-103">TransferEligibility-erőforrások</span><span class="sxs-lookup"><span data-stu-id="33408-103">TransferEligibility resources</span></span>

<span data-ttu-id="33408-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="33408-104">**Applies to:**</span></span>

- <span data-ttu-id="33408-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="33408-105">Partner Center</span></span>

<span data-ttu-id="33408-106">Egy partner akkor hozza létre az átvitelt, ha az ügyfél előfizetését a partnerrel egy másik partnernek kívánja átvinni.</span><span class="sxs-lookup"><span data-stu-id="33408-106">A partner creates a transfer when a customer wants their subscription with the partner to be transferred to another partner.</span></span>

## <a name="transfereligibility"></a><span data-ttu-id="33408-107">TransferEligibility</span><span class="sxs-lookup"><span data-stu-id="33408-107">TransferEligibility</span></span>

<span data-ttu-id="33408-108">Leírja a transferEligibility.</span><span class="sxs-lookup"><span data-stu-id="33408-108">Describes a transferEligibility.</span></span>

| <span data-ttu-id="33408-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="33408-109">Property</span></span>              | <span data-ttu-id="33408-110">Típus</span><span class="sxs-lookup"><span data-stu-id="33408-110">Type</span></span>             | <span data-ttu-id="33408-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="33408-111">Description</span></span>                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="33408-112">id</span><span class="sxs-lookup"><span data-stu-id="33408-112">id</span></span>                    | <span data-ttu-id="33408-113">sztring</span><span class="sxs-lookup"><span data-stu-id="33408-113">string</span></span>           | <span data-ttu-id="33408-114">Az ügyfél előfizetés-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="33408-114">The customer's subscription identifier.</span></span>                                                  |
| <span data-ttu-id="33408-115">isEligible</span><span class="sxs-lookup"><span data-stu-id="33408-115">isEligible</span></span>            | <span data-ttu-id="33408-116">logikai</span><span class="sxs-lookup"><span data-stu-id="33408-116">bool</span></span>             | <span data-ttu-id="33408-117">Azt jelzi, hogy az előfizetés jogosult-e az átvitelre.</span><span class="sxs-lookup"><span data-stu-id="33408-117">Indicates whether the subscription is eligible for the transfer.</span></span>                         |
| <span data-ttu-id="33408-118">Ok</span><span class="sxs-lookup"><span data-stu-id="33408-118">Reason</span></span>                | <span data-ttu-id="33408-119">sztring</span><span class="sxs-lookup"><span data-stu-id="33408-119">string</span></span>           | <span data-ttu-id="33408-120">Az OK tulajdonság megmagyarázza, hogy az előfizetés miért nem jogosult az átvitelre.</span><span class="sxs-lookup"><span data-stu-id="33408-120">The reason property explains why the subscription isn't eligible for transfer.</span></span> |