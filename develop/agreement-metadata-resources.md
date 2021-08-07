---
title: A szerződés metaadatainak erőforrásai
description: Az AgreementMetadata erőforrás-gyűjtemény azokat a szerződéstípusokat ismerteti, amelyek segítségével a partnerek megerősítheti az ügyfelek elfogadását.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 7c09dc2a8dd88e3d3a6a7925f6f61737cbbd410eabda6ecb4c3ead13d889de04
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991259"
---
# <a name="agreement-metadata-resources"></a>A szerződés metaadatainak erőforrásai

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az **AgreementMetaData** erőforrást jelenleg csak a Microsoft nyilvános Partnerközpont támogatja. 

Az **AgreementMetaData** gyűjtemény az összes szerződéstípusra vonatkozó metaadatokat biztosít. A partnerek ezzel a gyűjteményrel megerősítheti, hogy az ügyfelek elfogadják a szerződéseket. Az **AgreementMetaData** gyűjtemény metaadatokat ad vissza mindkét szerződéstípushoz (Microsoft Cloud szerződés és **Microsoft Ügyfélszerződés**).

## <a name="agreementmetadata"></a>AgreementMetaData

A visszaadott szerződési metaadatok a következő tulajdonságokat tartalmazzák:

| Tulajdonság      | Típus               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId (sablonazonosító)    | sztring             | A szerződéssablon egyedi azonosítója.                                       |
| típus          | sztring             | Szerződés típusa. Jelenleg a támogatott értékek közé tartozik a **MicrosoftCloudAgreement** és a **MicrosoftCustomerAgreement** (előzetes verzió). |
| agreementLink | sztring             | A szerződéssablon URL-címe.                                                    |
