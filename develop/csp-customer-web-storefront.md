---
title: CSP-ügyfél – webes áruház oldala
description: Ez a minta webhely-kód egy működő online áruházban jeleníti meg az ügyfeleket a Microsoft-termékek előfizetésének vásárlásához.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd488b9b9bf2c1df4bebc8513d230a02b06b2ce4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767740"
---
# <a name="csp-customer-web-storefront"></a><span data-ttu-id="b640a-103">CSP-ügyfél – webes áruház oldala</span><span class="sxs-lookup"><span data-stu-id="b640a-103">CSP customer web storefront</span></span>

<span data-ttu-id="b640a-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="b640a-104">**Applies to:**</span></span>

- <span data-ttu-id="b640a-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="b640a-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="b640a-106">Ez a minta alkalmazás csak a partneri központ globális példányára vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="b640a-106">This sample app applies only to the global instance of Partner Center.</span></span> <span data-ttu-id="b640a-107">Nem vonatkozik a Microsoft Cloud németországi partner központjára vagy a Microsoft Cloud az USA kormányzati szerveinek.</span><span class="sxs-lookup"><span data-stu-id="b640a-107">It does not apply to Partner Center for Microsoft Cloud Germany or to Partner Center for Microsoft Cloud for US Government.</span></span>

<span data-ttu-id="b640a-108">A [partner Center kirakat](https://github.com/Microsoft/Partner-Center-Storefront) egy online áruházból álló **minta webhely** , amellyel az ügyfelek vásárolhatnak előfizetéseket a Microsoft termékeihez.</span><span class="sxs-lookup"><span data-stu-id="b640a-108">The [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) is a **sample website** for an online store that customers can use to buy subscriptions to Microsoft products.</span></span> <span data-ttu-id="b640a-109">A saját használatra módosíthatja ezt a **kódot** [az ajánlatok konfigurálásához](#configure-offers), a [branding hozzáadásához](#configure-branding) és [a fizetési mód hozzáadásához](#configure-payment-types).</span><span class="sxs-lookup"><span data-stu-id="b640a-109">You can modify this **sample code** for your own use to [configure the offers](#configure-offers), [add branding](#configure-branding) and [add a payment method](#configure-payment-types).</span></span>

## <a name="sample-code"></a><span data-ttu-id="b640a-110">Mintakód</span><span class="sxs-lookup"><span data-stu-id="b640a-110">Sample code</span></span>

<span data-ttu-id="b640a-111">Töltse le a [partneri központ kirakati mintáját](https://github.com/Microsoft/Partner-Center-Storefront) a githubról.</span><span class="sxs-lookup"><span data-stu-id="b640a-111">Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) from GitHub.</span></span>

## <a name="configure-authentication"></a><span data-ttu-id="b640a-112">A hitelesítés konfigurálása</span><span class="sxs-lookup"><span data-stu-id="b640a-112">Configure authentication</span></span>

<span data-ttu-id="b640a-113">Az alkalmazás létrehozása előtt frissítse a Web.config fájl következő értékeit, hogy azok tükrözzék a [partner Center-hitelesítésben](partner-center-authentication.md)létrehozott Azure ad-hitelesítési adatokat.</span><span class="sxs-lookup"><span data-stu-id="b640a-113">Before you build the application, update the following values in the Web.config file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b640a-114">Az integrációs munkafolyamatok fiókjának beállításait a korai fejlesztés vagy az éles környezetben történő tesztelés során érdemes használni.</span><span class="sxs-lookup"><span data-stu-id="b640a-114">You should use your integration sandbox account settings during early development or for testing in production (TiP).</span></span>

- <span data-ttu-id="b640a-115">**partnerCenter. applicationId**</span><span class="sxs-lookup"><span data-stu-id="b640a-115">**partnerCenter.applicationId**</span></span>
- <span data-ttu-id="b640a-116">**partnerCenter.applicationSecret**</span><span class="sxs-lookup"><span data-stu-id="b640a-116">**partnerCenter.applicationSecret**</span></span>
- <span data-ttu-id="b640a-117">**partnerCenter. domain**</span><span class="sxs-lookup"><span data-stu-id="b640a-117">**partnerCenter.domain**</span></span>
- <span data-ttu-id="b640a-118">**Webportal. clientId**</span><span class="sxs-lookup"><span data-stu-id="b640a-118">**webPortal.clientId**</span></span>
- <span data-ttu-id="b640a-119">**Webportal. clientSecret**</span><span class="sxs-lookup"><span data-stu-id="b640a-119">**webPortal.clientSecret**</span></span>
- <span data-ttu-id="b640a-120">**Webportal. domain**</span><span class="sxs-lookup"><span data-stu-id="b640a-120">**webPortal.domain**</span></span>
- <span data-ttu-id="b640a-121">**Webportal. azureStorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="b640a-121">**webPortal.azureStorageConnectionString**</span></span>

## <a name="configure-offers"></a><span data-ttu-id="b640a-122">Ajánlatok konfigurálása</span><span class="sxs-lookup"><span data-stu-id="b640a-122">Configure offers</span></span>

<span data-ttu-id="b640a-123">Az ajánlatok (**MicrosoftOffer**) készletét az **OfferCatalogViewModel** is konfigurálhatja.</span><span class="sxs-lookup"><span data-stu-id="b640a-123">You can configure the set of offers (**MicrosoftOffer**) in the **OfferCatalogViewModel**.</span></span>

## <a name="configure-branding"></a><span data-ttu-id="b640a-124">Védjegyezés konfigurálása</span><span class="sxs-lookup"><span data-stu-id="b640a-124">Configure branding</span></span>

<span data-ttu-id="b640a-125">Ez a minta webhelye a következő vállalati és Brand-információkat követi nyomon a *BrandingConfiguration.cs* és a *PortalBranding.cs*:</span><span class="sxs-lookup"><span data-stu-id="b640a-125">This sample website tracks the following company and brand information in *BrandingConfiguration.cs* and *PortalBranding.cs*:</span></span>

- <span data-ttu-id="b640a-126">Szervezet neve</span><span class="sxs-lookup"><span data-stu-id="b640a-126">Organization name</span></span>
- <span data-ttu-id="b640a-127">Szervezet emblémája</span><span class="sxs-lookup"><span data-stu-id="b640a-127">Organization logo</span></span>
- <span data-ttu-id="b640a-128">Fejléc képe</span><span class="sxs-lookup"><span data-stu-id="b640a-128">Header image</span></span>
- <span data-ttu-id="b640a-129">Adatvédelmi szerződés</span><span class="sxs-lookup"><span data-stu-id="b640a-129">Privacy agreement</span></span>
- <span data-ttu-id="b640a-130">Kapcsolattartási e-mail-cím</span><span class="sxs-lookup"><span data-stu-id="b640a-130">Contact email</span></span>
- <span data-ttu-id="b640a-131">Kapcsolattartó telefonszáma</span><span class="sxs-lookup"><span data-stu-id="b640a-131">Contact phone number</span></span>
- <span data-ttu-id="b640a-132">Támogatási e-mail</span><span class="sxs-lookup"><span data-stu-id="b640a-132">Support email</span></span>
- <span data-ttu-id="b640a-133">Ügyfélszolgálat telefonszáma</span><span class="sxs-lookup"><span data-stu-id="b640a-133">Support phone number</span></span>

### <a name="configure-payment-types"></a><span data-ttu-id="b640a-134">Fizetési típusok konfigurálása</span><span class="sxs-lookup"><span data-stu-id="b640a-134">Configure payment types</span></span>

<span data-ttu-id="b640a-135">Az alkalmazás jelenleg a *PayPalGateway.cs*-ben megvalósított PayPal-átjárót használ.</span><span class="sxs-lookup"><span data-stu-id="b640a-135">The app currently uses a PayPal gateway, implemented in *PayPalGateway.cs*.</span></span>