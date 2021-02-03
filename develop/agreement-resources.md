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
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a>A Microsoft Cloud Customer-szerződést képviselő, szerződéssel rendelkező erőforrások

**A következőkre vonatkozik:**

- Partnerközpont

A partner Center jelenleg csak a Microsoft nyilvános felhőben támogatja a **szerződési** erőforrást. Nem alkalmazható a következőre:

- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A **szerződési** erőforrás a Microsoft Cloud Customer-szerződést jelöli.

## <a name="agreement"></a>Megállapodás

A **szerződési** erőforrás a partner által biztosított minősítés részleteit jelöli.

| Tulajdonság       | Típus   | Leírás                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | sztring                         | A partner bérlő Bejelentkezett felhasználójának objektumazonosító, aki a partner szervezet nevében megerősíti a megerősítést. Ha app + felhasználói hitelesítést használ a szerződési erőforrások létrehozásához, a partner Center automatikusan származtatja a **userId** attribútum értékét az alkalmazás + felhasználói jogkivonat alapján.                                                                             |
| primaryContact | [Kapcsolatfelvétel](./utility-resources.md#contact) | Információ a szerződést elfogadó ügyfél-szervezet felhasználója számára, beleértve a következőket:  **firstName**, **lastName**, **e-mail** és **telefonszám** (nem kötelező). |
| dateAgreed     | karakterlánc UTC-dátum időformátuma | Az a dátum, amikor az ügyfél elfogadta a szerződést.                                 |
| templateId     |sztring                          | Az ügyfél által elfogadott szerződés egyedi azonosítója. |
| típus           |sztring                          | Szerződés típusa Jelenleg a támogatott értékek a következők: **MicrosoftCloudAgreement** és **MicrosoftCustomerAgreement**.|
| agreementLink  | sztring                         | A szerződés sablonjának URL-címe.                                                    |
