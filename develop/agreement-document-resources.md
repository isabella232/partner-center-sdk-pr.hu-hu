---
title: A szerződés dokumentum-erőforrásai
description: A AgreementDocument erőforrás egy Microsoft-szerződés dokumentuma az előzetes verzióhoz és letöltéshez. A Microsoft nyilvános Partnerközpont támogatja.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 1a81da4f75594f241669db831125bd437872561c
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025666"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a><span data-ttu-id="3cf47-104">A Microsoft nyilvános felhőbeli Partnerközpont által támogatott erőforrásokat dokumentáló szerződés</span><span class="sxs-lookup"><span data-stu-id="3cf47-104">Agreement document resources supported by Partner Center in the Microsoft public cloud</span></span>

<span data-ttu-id="3cf47-105">**A következőkre vonatkozik:** Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="3cf47-105">**Applies to**: Partner Center</span></span>

<span data-ttu-id="3cf47-106">**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3cf47-106">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3cf47-107">A **AgreementDocument** erőforrást jelenleg csak a Microsoft nyilvános Partnerközpont támogatja.</span><span class="sxs-lookup"><span data-stu-id="3cf47-107">The **AgreementDocument** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="3cf47-108">A **AgreementDocument erőforrás** egy, az előzetes verzióhoz és letöltéshez elérhető Microsoft-szerződési dokumentumot jelent.</span><span class="sxs-lookup"><span data-stu-id="3cf47-108">The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.</span></span>

## <a name="agreementdocument"></a><span data-ttu-id="3cf47-109">AgreementDocument (Szerződésdokumentum)</span><span class="sxs-lookup"><span data-stu-id="3cf47-109">AgreementDocument</span></span>

<span data-ttu-id="3cf47-110">A **AgreementDocument erőforrás** a következő tulajdonságokat tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="3cf47-110">An **AgreementDocument** resource includes the following properties:</span></span>

| <span data-ttu-id="3cf47-111">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="3cf47-111">Property</span></span>       | <span data-ttu-id="3cf47-112">Típus</span><span class="sxs-lookup"><span data-stu-id="3cf47-112">Type</span></span>   | <span data-ttu-id="3cf47-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="3cf47-113">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3cf47-114">ország</span><span class="sxs-lookup"><span data-stu-id="3cf47-114">country</span></span> | <span data-ttu-id="3cf47-115">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf47-115">string</span></span> | <span data-ttu-id="3cf47-116">Az ország vagy piac, amelyre a dokumentum vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="3cf47-116">The country or market to which this document applies.</span></span> |
| <span data-ttu-id="3cf47-117">language</span><span class="sxs-lookup"><span data-stu-id="3cf47-117">language</span></span> | <span data-ttu-id="3cf47-118">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf47-118">string</span></span> | <span data-ttu-id="3cf47-119">A dokumentum honosított nyelve.</span><span class="sxs-lookup"><span data-stu-id="3cf47-119">The language in which this document is localized.</span></span> |
| <span data-ttu-id="3cf47-120">displayUri</span><span class="sxs-lookup"><span data-stu-id="3cf47-120">displayUri</span></span> | <span data-ttu-id="3cf47-121">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf47-121">string</span></span> | <span data-ttu-id="3cf47-122">A szerződésdokumentum böngészőben való előnézetére mutató hivatkozás.</span><span class="sxs-lookup"><span data-stu-id="3cf47-122">A link to preview the agreement document in a browser.</span></span>  |
| <span data-ttu-id="3cf47-123">downloadUri</span><span class="sxs-lookup"><span data-stu-id="3cf47-123">downloadUri</span></span> |<span data-ttu-id="3cf47-124">sztring</span><span class="sxs-lookup"><span data-stu-id="3cf47-124">string</span></span> | <span data-ttu-id="3cf47-125">Hivatkozás a szerződésdokumentum letöltéséhez (Microsoft Word formátumban).</span><span class="sxs-lookup"><span data-stu-id="3cf47-125">A link to download the agreement document (in Microsoft Word format).</span></span> |
