---
title: Egyezményerőforrások
description: A Szerződés erőforrás egy Microsoft-felhőbeli ügyfélszerződést képvisel, amely tartalmazza a partner által biztosított tanúsítvány részleteit.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 5fa196e711d9ff899b61ba20e75edd92749165e5
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025617"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a><span data-ttu-id="feaec-103">A Microsoft felhőalapú ügyfélszerződését képviselő szerződéserőforrások</span><span class="sxs-lookup"><span data-stu-id="feaec-103">Agreement resources representing a Microsoft cloud customer agreement</span></span>

<span data-ttu-id="feaec-104">**A következőkre vonatkozik:** Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="feaec-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="feaec-105">**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="feaec-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="feaec-106">A **Szerződés** erőforrást jelenleg csak a Microsoft Partnerközpont támogatja.</span><span class="sxs-lookup"><span data-stu-id="feaec-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="feaec-107">A **Szerződés** erőforrás a Microsoft felhőalapú ügyfélszerződését jelöli.</span><span class="sxs-lookup"><span data-stu-id="feaec-107">The **Agreement** resource represents a Microsoft cloud customer agreement.</span></span>

## <a name="agreement"></a><span data-ttu-id="feaec-108">Megállapodás</span><span class="sxs-lookup"><span data-stu-id="feaec-108">Agreement</span></span>

<span data-ttu-id="feaec-109">A **Szerződés** erőforrás a partner által biztosított tanúsítvány részleteit jelöli.</span><span class="sxs-lookup"><span data-stu-id="feaec-109">The **Agreement** resource represents the details of certification provided by the partner.</span></span>

| <span data-ttu-id="feaec-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="feaec-110">Property</span></span>       | <span data-ttu-id="feaec-111">Típus</span><span class="sxs-lookup"><span data-stu-id="feaec-111">Type</span></span>   | <span data-ttu-id="feaec-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="feaec-112">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="feaec-113">userId</span><span class="sxs-lookup"><span data-stu-id="feaec-113">userId</span></span>         | <span data-ttu-id="feaec-114">sztring</span><span class="sxs-lookup"><span data-stu-id="feaec-114">string</span></span>                         | <span data-ttu-id="feaec-115">Annak a partnerbérlőnek a bejelentkezett felhasználójának objektumazonosítója, aki megerősítést küld a partnerszervezet nevében.</span><span class="sxs-lookup"><span data-stu-id="feaec-115">Object identifier of the logged-in user in the partner tenant who is providing confirmation on behalf of the partner organization.</span></span> <span data-ttu-id="feaec-116">Amikor App+User hitelesítést használ egy szerződéserőforrás létrehozásához, a Partnerközpont automatikusan származtatja a **userId** attribútum értékét az App+User jogkivonatból.</span><span class="sxs-lookup"><span data-stu-id="feaec-116">When using App+User authentication to create an Agreement resource, Partner Center automatically derives the **userId** attribute value from the App+User token.</span></span>                                                                             |
| <span data-ttu-id="feaec-117">primaryContact (elsődleges tranzakció)</span><span class="sxs-lookup"><span data-stu-id="feaec-117">primaryContact</span></span> | [<span data-ttu-id="feaec-118">Kapcsolatfelvétel</span><span class="sxs-lookup"><span data-stu-id="feaec-118">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="feaec-119">A szerződést elfogadó ügyfélszervezet felhasználójával kapcsolatos információk, beleértve a következőket:  **firstName,** **lastName,** **e-mail,** és **phoneNumber** (nem kötelező).</span><span class="sxs-lookup"><span data-stu-id="feaec-119">Information about the user from the customer organization that accepted the agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional).</span></span> |
| <span data-ttu-id="feaec-120">dateAgreed (dátum dátuma)</span><span class="sxs-lookup"><span data-stu-id="feaec-120">dateAgreed</span></span>     | <span data-ttu-id="feaec-121">sztring UTC dátum-idő formátumban</span><span class="sxs-lookup"><span data-stu-id="feaec-121">string in UTC date time format</span></span> | <span data-ttu-id="feaec-122">Az a dátum, amikor az ügyfél elfogadta a szerződést.</span><span class="sxs-lookup"><span data-stu-id="feaec-122">The date when the customer accepted the agreement.</span></span>                                 |
| <span data-ttu-id="feaec-123">templateId (sablonazonosító)</span><span class="sxs-lookup"><span data-stu-id="feaec-123">templateId</span></span>     |<span data-ttu-id="feaec-124">sztring</span><span class="sxs-lookup"><span data-stu-id="feaec-124">string</span></span>                          | <span data-ttu-id="feaec-125">Az ügyfél által elfogadott szerződés egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="feaec-125">Unique identifier of the agreement that the customer accepted.</span></span> |
| <span data-ttu-id="feaec-126">típus</span><span class="sxs-lookup"><span data-stu-id="feaec-126">type</span></span>           |<span data-ttu-id="feaec-127">sztring</span><span class="sxs-lookup"><span data-stu-id="feaec-127">string</span></span>                          | <span data-ttu-id="feaec-128">Szerződés típusa.</span><span class="sxs-lookup"><span data-stu-id="feaec-128">Agreement type.</span></span> <span data-ttu-id="feaec-129">A támogatott értékek jelenleg a **MicrosoftCloudAgreement és** a **MicrosoftCustomerAgreement.**</span><span class="sxs-lookup"><span data-stu-id="feaec-129">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement**.</span></span>|
| <span data-ttu-id="feaec-130">agreementLink</span><span class="sxs-lookup"><span data-stu-id="feaec-130">agreementLink</span></span>  | <span data-ttu-id="feaec-131">sztring</span><span class="sxs-lookup"><span data-stu-id="feaec-131">string</span></span>                         | <span data-ttu-id="feaec-132">A szerződéssablon URL-címe.</span><span class="sxs-lookup"><span data-stu-id="feaec-132">URL for the agreement template.</span></span>                                                    |
