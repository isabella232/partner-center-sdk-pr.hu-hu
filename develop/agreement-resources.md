---
title: Szerződés erőforrásai
description: A szerződési erőforrás a Microsoft Cloud Customer-szerződést jelöli a partner által biztosított minősítés részleteivel.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: d964b1c7c6d70814ef68e48f05611ecbb113c8fe
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768555"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a><span data-ttu-id="5424d-103">A Microsoft Cloud Customer-szerződést képviselő, szerződéssel rendelkező erőforrások</span><span class="sxs-lookup"><span data-stu-id="5424d-103">Agreement resources representing a Microsoft cloud customer agreement</span></span>

<span data-ttu-id="5424d-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="5424d-104">**Applies to:**</span></span>

- <span data-ttu-id="5424d-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="5424d-105">Partner Center</span></span>

<span data-ttu-id="5424d-106">A partner Center jelenleg csak a Microsoft nyilvános felhőben támogatja a **szerződési** erőforrást.</span><span class="sxs-lookup"><span data-stu-id="5424d-106">The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="5424d-107">Nem alkalmazható a következőre:</span><span class="sxs-lookup"><span data-stu-id="5424d-107">It isn't applicable to:</span></span>

- <span data-ttu-id="5424d-108">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="5424d-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5424d-109">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5424d-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5424d-110">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5424d-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5424d-111">A **szerződési** erőforrás a Microsoft Cloud Customer-szerződést jelöli.</span><span class="sxs-lookup"><span data-stu-id="5424d-111">The **Agreement** resource represents a Microsoft cloud customer agreement.</span></span>

## <a name="agreement"></a><span data-ttu-id="5424d-112">Megállapodás</span><span class="sxs-lookup"><span data-stu-id="5424d-112">Agreement</span></span>

<span data-ttu-id="5424d-113">A **szerződési** erőforrás a partner által biztosított minősítés részleteit jelöli.</span><span class="sxs-lookup"><span data-stu-id="5424d-113">The **Agreement** resource represents the details of certification provided by the partner.</span></span>

| <span data-ttu-id="5424d-114">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="5424d-114">Property</span></span>       | <span data-ttu-id="5424d-115">Típus</span><span class="sxs-lookup"><span data-stu-id="5424d-115">Type</span></span>   | <span data-ttu-id="5424d-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="5424d-116">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5424d-117">userId</span><span class="sxs-lookup"><span data-stu-id="5424d-117">userId</span></span>         | <span data-ttu-id="5424d-118">sztring</span><span class="sxs-lookup"><span data-stu-id="5424d-118">string</span></span>                         | <span data-ttu-id="5424d-119">A partner bérlő Bejelentkezett felhasználójának objektumazonosító, aki a partner szervezet nevében megerősíti a megerősítést.</span><span class="sxs-lookup"><span data-stu-id="5424d-119">Object identifier of the logged-in user in the partner tenant who is providing confirmation on behalf of the partner organization.</span></span> <span data-ttu-id="5424d-120">Ha app + felhasználói hitelesítést használ a szerződési erőforrások létrehozásához, a partner Center automatikusan származtatja a **userId** attribútum értékét az alkalmazás + felhasználói jogkivonat alapján.</span><span class="sxs-lookup"><span data-stu-id="5424d-120">When using App+User authentication to create an Agreement resource, Partner Center automatically derives the **userId** attribute value from the App+User token.</span></span>                                                                             |
| <span data-ttu-id="5424d-121">primaryContact</span><span class="sxs-lookup"><span data-stu-id="5424d-121">primaryContact</span></span> | [<span data-ttu-id="5424d-122">Kapcsolatfelvétel</span><span class="sxs-lookup"><span data-stu-id="5424d-122">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="5424d-123">Információ a szerződést elfogadó ügyfél-szervezet felhasználója számára, beleértve a következőket:  **firstName**, **lastName**, **e-mail** és **telefonszám** (nem kötelező).</span><span class="sxs-lookup"><span data-stu-id="5424d-123">Information about the user from the customer organization that accepted the agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional).</span></span> |
| <span data-ttu-id="5424d-124">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="5424d-124">dateAgreed</span></span>     | <span data-ttu-id="5424d-125">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="5424d-125">string in UTC date time format</span></span> | <span data-ttu-id="5424d-126">Az a dátum, amikor az ügyfél elfogadta a szerződést.</span><span class="sxs-lookup"><span data-stu-id="5424d-126">The date when the customer accepted the agreement.</span></span>                                 |
| <span data-ttu-id="5424d-127">templateId</span><span class="sxs-lookup"><span data-stu-id="5424d-127">templateId</span></span>     |<span data-ttu-id="5424d-128">sztring</span><span class="sxs-lookup"><span data-stu-id="5424d-128">string</span></span>                          | <span data-ttu-id="5424d-129">Az ügyfél által elfogadott szerződés egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="5424d-129">Unique identifier of the agreement that the customer accepted.</span></span> |
| <span data-ttu-id="5424d-130">típus</span><span class="sxs-lookup"><span data-stu-id="5424d-130">type</span></span>           |<span data-ttu-id="5424d-131">sztring</span><span class="sxs-lookup"><span data-stu-id="5424d-131">string</span></span>                          | <span data-ttu-id="5424d-132">Szerződés típusa</span><span class="sxs-lookup"><span data-stu-id="5424d-132">Agreement type.</span></span> <span data-ttu-id="5424d-133">Jelenleg a támogatott értékek a következők: **MicrosoftCloudAgreement** és **MicrosoftCustomerAgreement**.</span><span class="sxs-lookup"><span data-stu-id="5424d-133">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement**.</span></span>|
| <span data-ttu-id="5424d-134">agreementLink</span><span class="sxs-lookup"><span data-stu-id="5424d-134">agreementLink</span></span>  | <span data-ttu-id="5424d-135">sztring</span><span class="sxs-lookup"><span data-stu-id="5424d-135">string</span></span>                         | <span data-ttu-id="5424d-136">A szerződés sablonjának URL-címe.</span><span class="sxs-lookup"><span data-stu-id="5424d-136">URL for the agreement template.</span></span>                                                    |
