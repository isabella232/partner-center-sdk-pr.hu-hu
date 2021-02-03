---
title: Szerződés metaadatainak erőforrásai
description: A AgreementMetadata-erőforrások gyűjteménye leírja, hogy a partnerek milyen típusú megállapodásokat használhatnak az ügyfelek elfogadásának megerősítéséhez.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767767"
---
# <a name="agreement-metadata-resources"></a>Szerződés metaadatainak erőforrásai

**A következőkre vonatkozik:**

- Partnerközpont

A **AgreementMetaData** erőforrást jelenleg csak a *Microsoft nyilvános felhőben* támogatja a partner Center. Ez az erőforrás nem alkalmazható a következőre:

- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A **AgreementMetaData** -gyűjtemény metaadatokat biztosít az összes szerződés típusáról. A partnerek használhatják ezt a gyűjteményt, hogy megerősítsék az ügyfelek elfogadják a szerződéseket. A **AgreementMetaData** -gyűjtemény a szerződési típusok (**Microsoft Cloud szerződés** és a **Microsoft ügyfél-szerződés**) metaadatait adja vissza.

## <a name="agreementmetadata"></a>AgreementMetaData

A visszaadott szerződési metaadatok a következő tulajdonságokat tartalmazzák:

| Tulajdonság      | Típus               | Leírás                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | sztring             | Egy szerződési sablon egyedi azonosítója.                                       |
| típus          | sztring             | Szerződés típusa Jelenleg a támogatott értékek a következők: **MicrosoftCloudAgreement** és **MicrosoftCustomerAgreement** (előzetes verzió). |
| agreementLink | sztring             | A szerződés sablonjának URL-címe.                                                    |
