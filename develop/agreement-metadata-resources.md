---
title: Szerződés metaadatainak erőforrásai
description: A AgreementMetadata-erőforrások gyűjteménye leírja, hogy a partnerek milyen típusú megállapodásokat használhatnak az ügyfelek elfogadásának megerősítéséhez.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767767"
---
# <a name="agreement-metadata-resources"></a><span data-ttu-id="778ef-103">Szerződés metaadatainak erőforrásai</span><span class="sxs-lookup"><span data-stu-id="778ef-103">Agreement metadata resources</span></span>

<span data-ttu-id="778ef-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="778ef-104">**Applies to:**</span></span>

- <span data-ttu-id="778ef-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="778ef-105">Partner Center</span></span>

<span data-ttu-id="778ef-106">A **AgreementMetaData** erőforrást jelenleg csak a *Microsoft nyilvános felhőben* támogatja a partner Center.</span><span class="sxs-lookup"><span data-stu-id="778ef-106">The **AgreementMetaData** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="778ef-107">Ez az erőforrás nem alkalmazható a következőre:</span><span class="sxs-lookup"><span data-stu-id="778ef-107">This resource isn't applicable to:</span></span>

- <span data-ttu-id="778ef-108">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="778ef-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="778ef-109">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="778ef-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="778ef-110">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="778ef-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="778ef-111">A **AgreementMetaData** -gyűjtemény metaadatokat biztosít az összes szerződés típusáról.</span><span class="sxs-lookup"><span data-stu-id="778ef-111">The **AgreementMetaData** collection provides metadata about all the agreement types.</span></span> <span data-ttu-id="778ef-112">A partnerek használhatják ezt a gyűjteményt, hogy megerősítsék az ügyfelek elfogadják a szerződéseket.</span><span class="sxs-lookup"><span data-stu-id="778ef-112">Partners can use this collection to provide confirmation of customer acceptance of agreements.</span></span> <span data-ttu-id="778ef-113">A **AgreementMetaData** -gyűjtemény a szerződési típusok (**Microsoft Cloud szerződés** és a **Microsoft ügyfél-szerződés**) metaadatait adja vissza.</span><span class="sxs-lookup"><span data-stu-id="778ef-113">The **AgreementMetaData** collection returns metadata for both agreement types (**Microsoft Cloud Agreement** and **Microsoft Customer Agreement**).</span></span>

## <a name="agreementmetadata"></a><span data-ttu-id="778ef-114">AgreementMetaData</span><span class="sxs-lookup"><span data-stu-id="778ef-114">AgreementMetaData</span></span>

<span data-ttu-id="778ef-115">A visszaadott szerződési metaadatok a következő tulajdonságokat tartalmazzák:</span><span class="sxs-lookup"><span data-stu-id="778ef-115">Agreement metadata returned includes the following properties:</span></span>

| <span data-ttu-id="778ef-116">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="778ef-116">Property</span></span>      | <span data-ttu-id="778ef-117">Típus</span><span class="sxs-lookup"><span data-stu-id="778ef-117">Type</span></span>               | <span data-ttu-id="778ef-118">Leírás</span><span class="sxs-lookup"><span data-stu-id="778ef-118">Description</span></span>                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="778ef-119">templateId</span><span class="sxs-lookup"><span data-stu-id="778ef-119">templateId</span></span>    | <span data-ttu-id="778ef-120">sztring</span><span class="sxs-lookup"><span data-stu-id="778ef-120">string</span></span>             | <span data-ttu-id="778ef-121">Egy szerződési sablon egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="778ef-121">Unique identifier of an agreement template.</span></span>                                       |
| <span data-ttu-id="778ef-122">típus</span><span class="sxs-lookup"><span data-stu-id="778ef-122">type</span></span>          | <span data-ttu-id="778ef-123">sztring</span><span class="sxs-lookup"><span data-stu-id="778ef-123">string</span></span>             | <span data-ttu-id="778ef-124">Szerződés típusa</span><span class="sxs-lookup"><span data-stu-id="778ef-124">Agreement type.</span></span> <span data-ttu-id="778ef-125">Jelenleg a támogatott értékek a következők: **MicrosoftCloudAgreement** és **MicrosoftCustomerAgreement** (előzetes verzió).</span><span class="sxs-lookup"><span data-stu-id="778ef-125">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement** (preview).</span></span> |
| <span data-ttu-id="778ef-126">agreementLink</span><span class="sxs-lookup"><span data-stu-id="778ef-126">agreementLink</span></span> | <span data-ttu-id="778ef-127">sztring</span><span class="sxs-lookup"><span data-stu-id="778ef-127">string</span></span>             | <span data-ttu-id="778ef-128">A szerződés sablonjának URL-címe.</span><span class="sxs-lookup"><span data-stu-id="778ef-128">URL for the agreement template.</span></span>                                                    |
