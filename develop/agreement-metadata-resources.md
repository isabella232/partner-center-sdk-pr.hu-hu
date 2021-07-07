---
title: A szerződés metaadatainak erőforrásai
description: Az AgreementMetadata erőforrás-gyűjtemény azokat a szerződéstípusokat ismerteti, amelyek használatával a partnerek megerősítheti az ügyfelek elfogadását.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: b930e3691b9d269ddb8d76ae18b6b26a217123c0
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025628"
---
# <a name="agreement-metadata-resources"></a><span data-ttu-id="d7ef6-103">A szerződés metaadatainak erőforrásai</span><span class="sxs-lookup"><span data-stu-id="d7ef6-103">Agreement metadata resources</span></span>

<span data-ttu-id="d7ef6-104">**A következőkre vonatkozik:** Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="d7ef6-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="d7ef6-105">**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d7ef6-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d7ef6-106">Az **AgreementMetaData** erőforrást jelenleg csak a Microsoft Partnerközpont támogatja.</span><span class="sxs-lookup"><span data-stu-id="d7ef6-106">The **AgreementMetaData** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span> 

<span data-ttu-id="d7ef6-107">Az **AgreementMetaData** gyűjtemény az összes szerződéstípusra vonatkozó metaadatokat biztosít.</span><span class="sxs-lookup"><span data-stu-id="d7ef6-107">The **AgreementMetaData** collection provides metadata about all the agreement types.</span></span> <span data-ttu-id="d7ef6-108">A partnerek ezzel a gyűjteményrel megerősítheti, hogy az ügyfelek elfogadják a szerződéseket.</span><span class="sxs-lookup"><span data-stu-id="d7ef6-108">Partners can use this collection to provide confirmation of customer acceptance of agreements.</span></span> <span data-ttu-id="d7ef6-109">Az **AgreementMetaData** gyűjtemény metaadatokat ad vissza mindkét szerződéstípushoz ( Microsoft Cloud szerződés és **Microsoft Ügyfélszerződés**).</span><span class="sxs-lookup"><span data-stu-id="d7ef6-109">The **AgreementMetaData** collection returns metadata for both agreement types (**Microsoft Cloud Agreement** and **Microsoft Customer Agreement**).</span></span>

## <a name="agreementmetadata"></a><span data-ttu-id="d7ef6-110">AgreementMetaData (SzerződésmetaData)</span><span class="sxs-lookup"><span data-stu-id="d7ef6-110">AgreementMetaData</span></span>

<span data-ttu-id="d7ef6-111">A visszaadott szerződési metaadatok a következő tulajdonságokat tartalmazzák:</span><span class="sxs-lookup"><span data-stu-id="d7ef6-111">Agreement metadata returned includes the following properties:</span></span>

| <span data-ttu-id="d7ef6-112">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d7ef6-112">Property</span></span>      | <span data-ttu-id="d7ef6-113">Típus</span><span class="sxs-lookup"><span data-stu-id="d7ef6-113">Type</span></span>               | <span data-ttu-id="d7ef6-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="d7ef6-114">Description</span></span>                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="d7ef6-115">templateId (sablonazonosító)</span><span class="sxs-lookup"><span data-stu-id="d7ef6-115">templateId</span></span>    | <span data-ttu-id="d7ef6-116">sztring</span><span class="sxs-lookup"><span data-stu-id="d7ef6-116">string</span></span>             | <span data-ttu-id="d7ef6-117">A szerződéssablon egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="d7ef6-117">Unique identifier of an agreement template.</span></span>                                       |
| <span data-ttu-id="d7ef6-118">típus</span><span class="sxs-lookup"><span data-stu-id="d7ef6-118">type</span></span>          | <span data-ttu-id="d7ef6-119">sztring</span><span class="sxs-lookup"><span data-stu-id="d7ef6-119">string</span></span>             | <span data-ttu-id="d7ef6-120">Szerződés típusa.</span><span class="sxs-lookup"><span data-stu-id="d7ef6-120">Agreement type.</span></span> <span data-ttu-id="d7ef6-121">Jelenleg a támogatott értékek közé tartozik a **MicrosoftCloudAgreement** és a **MicrosoftCustomerAgreement** (előzetes verzió).</span><span class="sxs-lookup"><span data-stu-id="d7ef6-121">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement** (preview).</span></span> |
| <span data-ttu-id="d7ef6-122">agreementLink</span><span class="sxs-lookup"><span data-stu-id="d7ef6-122">agreementLink</span></span> | <span data-ttu-id="d7ef6-123">sztring</span><span class="sxs-lookup"><span data-stu-id="d7ef6-123">string</span></span>             | <span data-ttu-id="d7ef6-124">A szerződéssablon URL-címe.</span><span class="sxs-lookup"><span data-stu-id="d7ef6-124">URL for the agreement template.</span></span>                                                    |
