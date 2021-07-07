---
title: A szerződés metaadatainak erőforrásai
description: Az AgreementMetadata erőforrás-gyűjtemény azokat a szerződéstípusokat ismerteti, amelyek használatával a partnerek megerősítheti az ügyfelek elfogadását.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: b930e3691b9d269ddb8d76ae18b6b26a217123c0
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025628"
---
# <a name="agreement-metadata-resources"></a>A szerződés metaadatainak erőforrásai

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az **AgreementMetaData** erőforrást jelenleg csak a Microsoft Partnerközpont támogatja. 

Az **AgreementMetaData** gyűjtemény az összes szerződéstípusra vonatkozó metaadatokat biztosít. A partnerek ezzel a gyűjteményrel megerősítheti, hogy az ügyfelek elfogadják a szerződéseket. Az **AgreementMetaData** gyűjtemény metaadatokat ad vissza mindkét szerződéstípushoz ( Microsoft Cloud szerződés és **Microsoft Ügyfélszerződés**).

## <a name="agreementmetadata"></a>AgreementMetaData (SzerződésmetaData)

A visszaadott szerződési metaadatok a következő tulajdonságokat tartalmazzák:

| Tulajdonság      | Típus               | Leírás                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId (sablonazonosító)    | sztring             | A szerződéssablon egyedi azonosítója.                                       |
| típus          | sztring             | Szerződés típusa. Jelenleg a támogatott értékek közé tartozik a **MicrosoftCloudAgreement** és a **MicrosoftCustomerAgreement** (előzetes verzió). |
| agreementLink | sztring             | A szerződéssablon URL-címe.                                                    |
