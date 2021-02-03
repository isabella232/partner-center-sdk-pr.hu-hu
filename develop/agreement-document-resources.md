---
title: Szerződés – dokumentum erőforrásai
description: A AgreementDocument-erőforrás az előzetes verzióra és a letöltésre vonatkozó Microsoft-szerződési dokumentum. A Microsoft nyilvános felhőben a partner Center támogatja.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 4805d25b0838bf922b81bebd998810c3f6a809c3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768560"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a><span data-ttu-id="ab61e-104">A Microsoft nyilvános felhőben a partner Center által támogatott szerződési dokumentumok erőforrásai</span><span class="sxs-lookup"><span data-stu-id="ab61e-104">Agreement document resources supported by Partner Center in the Microsoft public cloud</span></span>

<span data-ttu-id="ab61e-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="ab61e-105">**Applies to:**</span></span>

- <span data-ttu-id="ab61e-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="ab61e-106">Partner Center</span></span>

<span data-ttu-id="ab61e-107">A **AgreementDocument** erőforrást jelenleg csak a *Microsoft nyilvános felhőben* támogatja a partner Center.</span><span class="sxs-lookup"><span data-stu-id="ab61e-107">The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="ab61e-108">Ez az erőforrás nem alkalmazható a következőre:</span><span class="sxs-lookup"><span data-stu-id="ab61e-108">This resource not applicable to:</span></span>

- <span data-ttu-id="ab61e-109">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="ab61e-109">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="ab61e-110">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="ab61e-110">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ab61e-111">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="ab61e-111">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ab61e-112">A **AgreementDocument** -erőforrás az előzetes verzió és a letöltés számára elérhető Microsoft-szerződési dokumentumot jelöli.</span><span class="sxs-lookup"><span data-stu-id="ab61e-112">The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.</span></span>

## <a name="agreementdocument"></a><span data-ttu-id="ab61e-113">AgreementDocument</span><span class="sxs-lookup"><span data-stu-id="ab61e-113">AgreementDocument</span></span>

<span data-ttu-id="ab61e-114">Az **AgreementDocument** -erőforrás a következő tulajdonságokat tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="ab61e-114">An **AgreementDocument** resource includes the following properties:</span></span>

| <span data-ttu-id="ab61e-115">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="ab61e-115">Property</span></span>       | <span data-ttu-id="ab61e-116">Típus</span><span class="sxs-lookup"><span data-stu-id="ab61e-116">Type</span></span>   | <span data-ttu-id="ab61e-117">Leírás</span><span class="sxs-lookup"><span data-stu-id="ab61e-117">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ab61e-118">ország</span><span class="sxs-lookup"><span data-stu-id="ab61e-118">country</span></span> | <span data-ttu-id="ab61e-119">sztring</span><span class="sxs-lookup"><span data-stu-id="ab61e-119">string</span></span> | <span data-ttu-id="ab61e-120">Az ország vagy piac, amelyre ez a dokumentum vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="ab61e-120">The country or market to which this document applies.</span></span> |
| <span data-ttu-id="ab61e-121">language</span><span class="sxs-lookup"><span data-stu-id="ab61e-121">language</span></span> | <span data-ttu-id="ab61e-122">sztring</span><span class="sxs-lookup"><span data-stu-id="ab61e-122">string</span></span> | <span data-ttu-id="ab61e-123">Az a nyelv, amelyben a dokumentum honosítva van.</span><span class="sxs-lookup"><span data-stu-id="ab61e-123">The language in which this document is localized.</span></span> |
| <span data-ttu-id="ab61e-124">displayUri</span><span class="sxs-lookup"><span data-stu-id="ab61e-124">displayUri</span></span> | <span data-ttu-id="ab61e-125">sztring</span><span class="sxs-lookup"><span data-stu-id="ab61e-125">string</span></span> | <span data-ttu-id="ab61e-126">Egy hivatkozás, amely a szerződés dokumentumának előnézetét jeleníti meg egy böngészőben.</span><span class="sxs-lookup"><span data-stu-id="ab61e-126">A link to preview the agreement document in a browser.</span></span>  |
| <span data-ttu-id="ab61e-127">downloadUri</span><span class="sxs-lookup"><span data-stu-id="ab61e-127">downloadUri</span></span> |<span data-ttu-id="ab61e-128">sztring</span><span class="sxs-lookup"><span data-stu-id="ab61e-128">string</span></span> | <span data-ttu-id="ab61e-129">A szerződési dokumentum letöltésére szolgáló hivatkozás (Microsoft Word Format).</span><span class="sxs-lookup"><span data-stu-id="ab61e-129">A link to download the agreement document (in Microsoft Word format).</span></span> |
