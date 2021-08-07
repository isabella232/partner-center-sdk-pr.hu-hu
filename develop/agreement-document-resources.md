---
title: A szerződés dokumentum-erőforrásai
description: A AgreementDocument erőforrás egy Microsoft-szerződés dokumentuma az előzetes verzióhoz és letöltéshez. Ezt a Microsoft nyilvános Partnerközpont támogatja.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: eddde1e8072c6aeeee814b52f46c7648d870b6ba63c09b20e4270b17f8386383
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991106"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a>A Microsoft nyilvános felhőszolgáltatásában Partnerközpont által támogatott erőforrásokat a szerződés

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A **AgreementDocument** erőforrást jelenleg csak a Microsoft Partnerközpont támogatja.

A **AgreementDocument erőforrás** egy Microsoft-szerződésre vonatkozó dokumentumot jelent, amely előzetes verzióként és letölthetőként érhető el.

## <a name="agreementdocument"></a>AgreementDocument (Szerződésdokumentum)

A **AgreementDocument erőforrás** a következő tulajdonságokat tartalmazza:

| Tulajdonság       | Típus   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| ország | sztring | Az ország vagy piac, amelyre a dokumentum vonatkozik. |
| language | sztring | A dokumentum honosított nyelve. |
| displayUri | sztring | A szerződésdokumentum böngészőben való előnézetére mutató hivatkozás.  |
| downloadUri |sztring | A szerződésdokumentum letöltésére mutató hivatkozás (Microsoft Word formátumban). |
