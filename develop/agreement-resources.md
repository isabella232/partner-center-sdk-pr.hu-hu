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
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a>A Microsoft felhőalapú ügyfélszerződését képviselő szerződéserőforrások

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A **Szerződés** erőforrást jelenleg csak a Microsoft Partnerközpont támogatja.

A **Szerződés** erőforrás a Microsoft felhőalapú ügyfélszerződését jelöli.

## <a name="agreement"></a>Megállapodás

A **Szerződés** erőforrás a partner által biztosított tanúsítvány részleteit jelöli.

| Tulajdonság       | Típus   | Leírás                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | sztring                         | Annak a partnerbérlőnek a bejelentkezett felhasználójának objektumazonosítója, aki megerősítést küld a partnerszervezet nevében. Amikor App+User hitelesítést használ egy szerződéserőforrás létrehozásához, a Partnerközpont automatikusan származtatja a **userId** attribútum értékét az App+User jogkivonatból.                                                                             |
| primaryContact (elsődleges tranzakció) | [Kapcsolatfelvétel](./utility-resources.md#contact) | A szerződést elfogadó ügyfélszervezet felhasználójával kapcsolatos információk, beleértve a következőket:  **firstName,** **lastName,** **e-mail,** és **phoneNumber** (nem kötelező). |
| dateAgreed (dátum dátuma)     | sztring UTC dátum-idő formátumban | Az a dátum, amikor az ügyfél elfogadta a szerződést.                                 |
| templateId (sablonazonosító)     |sztring                          | Az ügyfél által elfogadott szerződés egyedi azonosítója. |
| típus           |sztring                          | Szerződés típusa. A támogatott értékek jelenleg a **MicrosoftCloudAgreement és** a **MicrosoftCustomerAgreement.**|
| agreementLink  | sztring                         | A szerződéssablon URL-címe.                                                    |
