---
title: CSP-ügyfél – webes áruház oldala
description: Ez a minta webhelykód egy működő online áruházat mutat be, amelyből az ügyfelek Microsoft-termékekre való előfizetéseket vásárolhatnak.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 07020c365db2ad578e7ff75602519d06eabb2a3bebf0913899fcd8b5345a0365
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995203"
---
# <a name="csp-customer-web-storefront"></a>CSP-ügyfél – webes áruház oldala

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Ez a mintaalkalmazás csak az alkalmazás globális példányára Partnerközpont.

A [Partnerközpont áruház egy](https://github.com/Microsoft/Partner-Center-Storefront)  online áruház minta webhelye, ahol az ügyfelek Microsoft-termékekre vonatkozó előfizetéseket vásárolhatnak. Ezt a **mintakódot** saját használatra módosíthatja [](#configure-branding)az ajánlatok konfigurálása, [](#configure-offers)védjegyezés hozzáadása és fizetési mód hozzáadása [érdekében.](#configure-payment-types)

## <a name="sample-code"></a>Mintakód

Töltse le [Partnerközpont áruházbeli mintakódot a](https://github.com/Microsoft/Partner-Center-Storefront) GitHub.

## <a name="configure-authentication"></a>A hitelesítés konfigurálása

Az alkalmazás létrehozása előtt frissítse a következő értékeket a Web.config-fájlban, hogy tükrözze a hitelesítés során létrehozott Azure [AD-Partnerközpont adatait.](partner-center-authentication.md) Az integrációs tesztfiók beállításait a fejlesztés korai szakaszában vagy éles környezetben (TiP) kell használnia.

- **partnerCenter.applicationId**
- **partnerCenter.applicationSecret**
- **partnerCenter.domain**
- **webPortal.clientId**
- **webPortal.clientSecret**
- **webPortal.domain**
- **webPortal.azureStorageConnectionString**

## <a name="configure-offers"></a>Ajánlatok konfigurálása

Az ajánlatok készletét **(MicrosoftOffer)** az **OfferCatalogViewModel** modellben konfigurálhatja.

## <a name="configure-branding"></a>Márkajelzés konfigurálása

Ez a mintawebhely a következő vállalati és márkainformációkat követi nyomon a *BrandingConfiguration.cs* és *a PortalBranding.cs fájlban:*

- Szervezet neve
- Szervezeti embléma
- Fejléc képe
- Adatvédelmi szerződés
- Kapcsolattartási e-mail-cím
- Kapcsolattartási telefonszám
- Támogatási e-mail
- Támogatási telefonszám

### <a name="configure-payment-types"></a>Fizetési típusok konfigurálása

Az alkalmazás jelenleg egy PayPal, amely a *PayPalGateway.cs* fájlban van megvalósítva.