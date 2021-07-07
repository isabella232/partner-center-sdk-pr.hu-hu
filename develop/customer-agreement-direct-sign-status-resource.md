---
title: Az ügyfélszerződés közvetlen aláírási (közvetlen elfogadási) állapota.
description: A DirectSignedCustomerAgreementStatus erőforrás az ügyfélszerződés közvetlen aláírásának (közvetlen elfogadásának) állapotát jelöli.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: d4d97667b5fd6b92c85889f1288dd770c2d1c035
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973111"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a><span data-ttu-id="0a8a1-103">Az ügyfélszerződés közvetlen aláírási (közvetlen elfogadási) állapota</span><span class="sxs-lookup"><span data-stu-id="0a8a1-103">Direct signing (direct acceptance) status of a customer agreement</span></span>

<span data-ttu-id="0a8a1-104">**A következőkre vonatkozik:** Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="0a8a1-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="0a8a1-105">**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0a8a1-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0a8a1-106">A **DirectSignedCustomerAgreementStatus** erőforrást jelenleg csak a Microsoft nyilvános Partnerközpont támogatja.</span><span class="sxs-lookup"><span data-stu-id="0a8a1-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="0a8a1-107">A **DirectSignedCustomerAgreementStatus** erőforrás az ügyfélszerződés közvetlen elfogadásának állapotát jelöli.</span><span class="sxs-lookup"><span data-stu-id="0a8a1-107">The **DirectSignedCustomerAgreementStatus** resource represents the status of the direct acceptance of a customer agreement.</span></span>

## <a name="directsignedcustomeragreementstatus"></a><span data-ttu-id="0a8a1-108">DirectSignedCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="0a8a1-108">DirectSignedCustomerAgreementStatus</span></span>

<span data-ttu-id="0a8a1-109">A **DirectSignedCustomerAgreementStatus erőforrás** a következő tulajdonságokat tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="0a8a1-109">A **DirectSignedCustomerAgreementStatus** resource includes the following properties:</span></span>

| <span data-ttu-id="0a8a1-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="0a8a1-110">Property</span></span>       | <span data-ttu-id="0a8a1-111">Típus</span><span class="sxs-lookup"><span data-stu-id="0a8a1-111">Type</span></span>   | <span data-ttu-id="0a8a1-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="0a8a1-112">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0a8a1-113">isSigned</span><span class="sxs-lookup"><span data-stu-id="0a8a1-113">isSigned</span></span> | <span data-ttu-id="0a8a1-114">boolean</span><span class="sxs-lookup"><span data-stu-id="0a8a1-114">boolean</span></span> | <span data-ttu-id="0a8a1-115">Jelzi, hogy az ügyfélszerződést közvetlenül írta-e alá (elfogadta) az ügyfél.</span><span class="sxs-lookup"><span data-stu-id="0a8a1-115">Indicates if the customer agreement has been directly signed (accepted) by the customer.</span></span> |
