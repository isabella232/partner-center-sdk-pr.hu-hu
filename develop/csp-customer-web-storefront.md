---
title: CSP-ügyfél – webes áruház oldala
description: Ez a minta webhelykód egy működő online áruházat mutat be, amelyből az ügyfelek Microsoft-termékekre vonatkozó előfizetéseket vásárolhatnak.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d68f17d707731f426cb980a566b6478790d3507c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973332"
---
# <a name="csp-customer-web-storefront"></a><span data-ttu-id="ae3cc-103">CSP-ügyfél – webes áruház oldala</span><span class="sxs-lookup"><span data-stu-id="ae3cc-103">CSP customer web storefront</span></span>

<span data-ttu-id="ae3cc-104">**A következőkre vonatkozik:** Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="ae3cc-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="ae3cc-105">**Nem vonatkozik a következőre:** Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ae3cc-105">**Does not apply to**: Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ae3cc-106">Ez a mintaalkalmazás csak az alkalmazás globális példányára Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="ae3cc-106">This sample app applies only to the global instance of Partner Center.</span></span>

<span data-ttu-id="ae3cc-107">A [Partnerközpont webalkalmazás](https://github.com/Microsoft/Partner-Center-Storefront) egy  online áruház minta webhelye, ahol az ügyfelek Microsoft-termékekre vonatkozó előfizetéseket vásárolhatnak.</span><span class="sxs-lookup"><span data-stu-id="ae3cc-107">The [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) is a **sample website** for an online store that customers can use to buy subscriptions to Microsoft products.</span></span> <span data-ttu-id="ae3cc-108">Ezt a **mintakódot** saját használatra módosíthatja [](#configure-branding)az ajánlatok konfigurálása, [](#configure-offers)márkajelzés hozzáadása és fizetési mód hozzáadása [érdekében.](#configure-payment-types)</span><span class="sxs-lookup"><span data-stu-id="ae3cc-108">You can modify this **sample code** for your own use to [configure the offers](#configure-offers), [add branding](#configure-branding), and [add a payment method](#configure-payment-types).</span></span>

## <a name="sample-code"></a><span data-ttu-id="ae3cc-109">Mintakód</span><span class="sxs-lookup"><span data-stu-id="ae3cc-109">Sample code</span></span>

<span data-ttu-id="ae3cc-110">Töltse le [Partnerközpont áruházbeli mintakódot a](https://github.com/Microsoft/Partner-Center-Storefront) GitHub.</span><span class="sxs-lookup"><span data-stu-id="ae3cc-110">Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) from GitHub.</span></span>

## <a name="configure-authentication"></a><span data-ttu-id="ae3cc-111">A hitelesítés konfigurálása</span><span class="sxs-lookup"><span data-stu-id="ae3cc-111">Configure authentication</span></span>

<span data-ttu-id="ae3cc-112">Az alkalmazás létrehozása előtt frissítse a következő értékeket a Web.config-fájlban, hogy azok a hitelesítés során létrehozott Azure [AD-Partnerközpont tükrözzék.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ae3cc-112">Before you build the application, update the following values in the Web.config file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ae3cc-113">Az integrációs tesztfiók beállításait a fejlesztés korai szakaszában vagy éles környezetben (TiP) való teszteléshez érdemes használni.</span><span class="sxs-lookup"><span data-stu-id="ae3cc-113">You should use your integration sandbox account settings during early development or for testing in production (TiP).</span></span>

- <span data-ttu-id="ae3cc-114">**partnerCenter.applicationId**</span><span class="sxs-lookup"><span data-stu-id="ae3cc-114">**partnerCenter.applicationId**</span></span>
- <span data-ttu-id="ae3cc-115">**partnerCenter.applicationSecret**</span><span class="sxs-lookup"><span data-stu-id="ae3cc-115">**partnerCenter.applicationSecret**</span></span>
- <span data-ttu-id="ae3cc-116">**partnerCenter.domain**</span><span class="sxs-lookup"><span data-stu-id="ae3cc-116">**partnerCenter.domain**</span></span>
- <span data-ttu-id="ae3cc-117">**webPortal.clientId**</span><span class="sxs-lookup"><span data-stu-id="ae3cc-117">**webPortal.clientId**</span></span>
- <span data-ttu-id="ae3cc-118">**webPortal.clientSecret**</span><span class="sxs-lookup"><span data-stu-id="ae3cc-118">**webPortal.clientSecret**</span></span>
- <span data-ttu-id="ae3cc-119">**webPortal.domain**</span><span class="sxs-lookup"><span data-stu-id="ae3cc-119">**webPortal.domain**</span></span>
- <span data-ttu-id="ae3cc-120">**webPortal.azureStorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="ae3cc-120">**webPortal.azureStorageConnectionString**</span></span>

## <a name="configure-offers"></a><span data-ttu-id="ae3cc-121">Ajánlatok konfigurálása</span><span class="sxs-lookup"><span data-stu-id="ae3cc-121">Configure offers</span></span>

<span data-ttu-id="ae3cc-122">Az ajánlatok készletét **(MicrosoftOffer)** az **OfferCatalogViewModel modellben konfigurálhatja.**</span><span class="sxs-lookup"><span data-stu-id="ae3cc-122">You can configure the set of offers (**MicrosoftOffer**) in the **OfferCatalogViewModel**.</span></span>

## <a name="configure-branding"></a><span data-ttu-id="ae3cc-123">Márkajelzés konfigurálása</span><span class="sxs-lookup"><span data-stu-id="ae3cc-123">Configure branding</span></span>

<span data-ttu-id="ae3cc-124">Ez a mintawebhely a következő vállalati és márkainformációkat követi nyomon a *BrandingConfiguration.cs* és *a PortalBranding.cs fájlban:*</span><span class="sxs-lookup"><span data-stu-id="ae3cc-124">This sample website tracks the following company and brand information in *BrandingConfiguration.cs* and *PortalBranding.cs*:</span></span>

- <span data-ttu-id="ae3cc-125">Szervezet neve</span><span class="sxs-lookup"><span data-stu-id="ae3cc-125">Organization name</span></span>
- <span data-ttu-id="ae3cc-126">Szervezeti embléma</span><span class="sxs-lookup"><span data-stu-id="ae3cc-126">Organization logo</span></span>
- <span data-ttu-id="ae3cc-127">Fejléc képe</span><span class="sxs-lookup"><span data-stu-id="ae3cc-127">Header image</span></span>
- <span data-ttu-id="ae3cc-128">Adatvédelmi szerződés</span><span class="sxs-lookup"><span data-stu-id="ae3cc-128">Privacy agreement</span></span>
- <span data-ttu-id="ae3cc-129">Kapcsolattartási e-mail-cím</span><span class="sxs-lookup"><span data-stu-id="ae3cc-129">Contact email</span></span>
- <span data-ttu-id="ae3cc-130">Kapcsolattartási telefonszám</span><span class="sxs-lookup"><span data-stu-id="ae3cc-130">Contact phone number</span></span>
- <span data-ttu-id="ae3cc-131">Támogatási e-mail</span><span class="sxs-lookup"><span data-stu-id="ae3cc-131">Support email</span></span>
- <span data-ttu-id="ae3cc-132">Támogatási telefonszám</span><span class="sxs-lookup"><span data-stu-id="ae3cc-132">Support phone number</span></span>

### <a name="configure-payment-types"></a><span data-ttu-id="ae3cc-133">Fizetési típusok konfigurálása</span><span class="sxs-lookup"><span data-stu-id="ae3cc-133">Configure payment types</span></span>

<span data-ttu-id="ae3cc-134">Az alkalmazás jelenleg egy PayPal a *PayPalGateway.cs fájlban megvalósított átjárót.*</span><span class="sxs-lookup"><span data-stu-id="ae3cc-134">The app currently uses a PayPal gateway, implemented in *PayPalGateway.cs*.</span></span>