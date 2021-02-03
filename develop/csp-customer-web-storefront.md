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
# <a name="csp-customer-web-storefront"></a>CSP-ügyfél – webes áruház oldala

**A következőkre vonatkozik:**

- Partnerközpont

> [!NOTE]
> Ez a minta alkalmazás csak a partneri központ globális példányára vonatkozik. Nem vonatkozik a Microsoft Cloud németországi partner központjára vagy a Microsoft Cloud az USA kormányzati szerveinek.

A [partner Center kirakat](https://github.com/Microsoft/Partner-Center-Storefront) egy online áruházból álló **minta webhely** , amellyel az ügyfelek vásárolhatnak előfizetéseket a Microsoft termékeihez. A saját használatra módosíthatja ezt a **kódot** [az ajánlatok konfigurálásához](#configure-offers), a [branding hozzáadásához](#configure-branding) és [a fizetési mód hozzáadásához](#configure-payment-types).

## <a name="sample-code"></a>Mintakód

Töltse le a [partneri központ kirakati mintáját](https://github.com/Microsoft/Partner-Center-Storefront) a githubról.

## <a name="configure-authentication"></a>A hitelesítés konfigurálása

Az alkalmazás létrehozása előtt frissítse a Web.config fájl következő értékeit, hogy azok tükrözzék a [partner Center-hitelesítésben](partner-center-authentication.md)létrehozott Azure ad-hitelesítési adatokat. Az integrációs munkafolyamatok fiókjának beállításait a korai fejlesztés vagy az éles környezetben történő tesztelés során érdemes használni.

- **partnerCenter. applicationId**
- **partnerCenter.applicationSecret**
- **partnerCenter. domain**
- **Webportal. clientId**
- **Webportal. clientSecret**
- **Webportal. domain**
- **Webportal. azureStorageConnectionString**

## <a name="configure-offers"></a>Ajánlatok konfigurálása

Az ajánlatok (**MicrosoftOffer**) készletét az **OfferCatalogViewModel** is konfigurálhatja.

## <a name="configure-branding"></a>Védjegyezés konfigurálása

Ez a minta webhelye a következő vállalati és Brand-információkat követi nyomon a *BrandingConfiguration.cs* és a *PortalBranding.cs*:

- Szervezet neve
- Szervezet emblémája
- Fejléc képe
- Adatvédelmi szerződés
- Kapcsolattartási e-mail-cím
- Kapcsolattartó telefonszáma
- Támogatási e-mail
- Ügyfélszolgálat telefonszáma

### <a name="configure-payment-types"></a>Fizetési típusok konfigurálása

Az alkalmazás jelenleg a *PayPalGateway.cs*-ben megvalósított PayPal-átjárót használ.