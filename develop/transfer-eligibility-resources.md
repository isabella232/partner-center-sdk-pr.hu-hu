---
title: TransferEligibility erőforrások
description: A partnerek akkor hozhatnak létre átadást, ha az ügyfél a partnerrel való előfizetését egy másik partnernek való átadásra kéri.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f121d499abffb4c4dda688c2a91c25f83d2e863
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530208"
---
# <a name="transfereligibility-resources"></a><span data-ttu-id="21a7f-103">TransferEligibility erőforrások</span><span class="sxs-lookup"><span data-stu-id="21a7f-103">TransferEligibility resources</span></span>

<span data-ttu-id="21a7f-104">A partnerek akkor hozhatnak létre átadást, ha az ügyfél a partnerrel való előfizetését egy másik partnernek való átadásra kéri.</span><span class="sxs-lookup"><span data-stu-id="21a7f-104">A partner can create a transfer when a customer requests their subscription with the partner to be transferred to another partner.</span></span> <span data-ttu-id="21a7f-105">A TransferEligibility használatával ellenőrizheti, hogy egy előfizetés átvihető-e.</span><span class="sxs-lookup"><span data-stu-id="21a7f-105">Use TransferEligibility to check whether a subscription is eligible to be transferred.</span></span>

## <a name="transfereligibility"></a><span data-ttu-id="21a7f-106">TransferEligibility (Átvitelelhetőség)</span><span class="sxs-lookup"><span data-stu-id="21a7f-106">TransferEligibility</span></span>

<span data-ttu-id="21a7f-107">A transferEligibility (átvitelelhetőség) szakaszt írja le.</span><span class="sxs-lookup"><span data-stu-id="21a7f-107">Describes a transferEligibility.</span></span>

| <span data-ttu-id="21a7f-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="21a7f-108">Property</span></span>              | <span data-ttu-id="21a7f-109">Típus</span><span class="sxs-lookup"><span data-stu-id="21a7f-109">Type</span></span>             | <span data-ttu-id="21a7f-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="21a7f-110">Description</span></span>                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="21a7f-111">id</span><span class="sxs-lookup"><span data-stu-id="21a7f-111">id</span></span>                    | <span data-ttu-id="21a7f-112">sztring</span><span class="sxs-lookup"><span data-stu-id="21a7f-112">string</span></span>           | <span data-ttu-id="21a7f-113">Az ügyfél előfizetés-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="21a7f-113">The customer's subscription identifier.</span></span>                                                  |
| <span data-ttu-id="21a7f-114">isEligible</span><span class="sxs-lookup"><span data-stu-id="21a7f-114">isEligible</span></span>            | <span data-ttu-id="21a7f-115">logikai</span><span class="sxs-lookup"><span data-stu-id="21a7f-115">bool</span></span>             | <span data-ttu-id="21a7f-116">Jelzi, hogy az előfizetés jogosult-e az átadásra.</span><span class="sxs-lookup"><span data-stu-id="21a7f-116">Indicates whether the subscription is eligible for the transfer.</span></span>                         |
| <span data-ttu-id="21a7f-117">Ok</span><span class="sxs-lookup"><span data-stu-id="21a7f-117">Reason</span></span>                | <span data-ttu-id="21a7f-118">sztring</span><span class="sxs-lookup"><span data-stu-id="21a7f-118">string</span></span>           | <span data-ttu-id="21a7f-119">Az ok tulajdonság elmagyarázza, hogy az előfizetés miért nem jogosult az átadásra.</span><span class="sxs-lookup"><span data-stu-id="21a7f-119">The reason property explains why the subscription isn't eligible for transfer.</span></span> |