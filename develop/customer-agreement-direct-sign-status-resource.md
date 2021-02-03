---
title: Egy ügyfél-szerződés közvetlen aláírása (közvetlen elfogadás) állapota.
description: A DirectSignedCustomerAgreementStatus erőforrás az ügyfél-szerződés közvetlen aláírása (közvetlen elfogadás) állapotát jelöli.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767739"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a><span data-ttu-id="cf847-103">Az ügyfél-szerződés közvetlen aláírása (közvetlen elfogadás) állapota</span><span class="sxs-lookup"><span data-stu-id="cf847-103">Direct signing (direct acceptance) status of a customer agreement</span></span>

<span data-ttu-id="cf847-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="cf847-104">**Applies to:**</span></span>

- <span data-ttu-id="cf847-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="cf847-105">Partner Center</span></span>

<span data-ttu-id="cf847-106">A **DirectSignedCustomerAgreementStatus** erőforrást jelenleg csak a Microsoft nyilvános felhőben támogatja a partner Center.</span><span class="sxs-lookup"><span data-stu-id="cf847-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="cf847-107">Ez az erőforrás *nem alkalmazható* a következőre:</span><span class="sxs-lookup"><span data-stu-id="cf847-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="cf847-108">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="cf847-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="cf847-109">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="cf847-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="cf847-110">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="cf847-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cf847-111">A **DirectSignedCustomerAgreementStatus** erőforrás az ügyfél-szerződés közvetlen elfogadásának állapotát jelöli.</span><span class="sxs-lookup"><span data-stu-id="cf847-111">The **DirectSignedCustomerAgreementStatus** resource represents the status of the direct acceptance of a customer agreement.</span></span>

## <a name="directsignedcustomeragreementstatus"></a><span data-ttu-id="cf847-112">DirectSignedCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="cf847-112">DirectSignedCustomerAgreementStatus</span></span>

<span data-ttu-id="cf847-113">A **DirectSignedCustomerAgreementStatus** -erőforrás a következő tulajdonságokat tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="cf847-113">A **DirectSignedCustomerAgreementStatus** resource includes the following properties:</span></span>

| <span data-ttu-id="cf847-114">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="cf847-114">Property</span></span>       | <span data-ttu-id="cf847-115">Típus</span><span class="sxs-lookup"><span data-stu-id="cf847-115">Type</span></span>   | <span data-ttu-id="cf847-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="cf847-116">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cf847-117">isSigned</span><span class="sxs-lookup"><span data-stu-id="cf847-117">isSigned</span></span> | <span data-ttu-id="cf847-118">boolean</span><span class="sxs-lookup"><span data-stu-id="cf847-118">boolean</span></span> | <span data-ttu-id="cf847-119">Azt jelzi, hogy az ügyfél közvetlenül aláírta-e az ügyfél szerződését (elfogadták-e).</span><span class="sxs-lookup"><span data-stu-id="cf847-119">Indicates if the customer agreement has been directly signed (accepted) by the customer.</span></span> |
