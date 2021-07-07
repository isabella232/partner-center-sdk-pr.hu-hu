---
title: A szerződés dokumentum-erőforrásai
description: A AgreementDocument erőforrás egy Microsoft-szerződés dokumentuma az előzetes verzióhoz és letöltéshez. A Microsoft nyilvános Partnerközpont támogatja.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 1a81da4f75594f241669db831125bd437872561c
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025666"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a>A Microsoft nyilvános felhőbeli Partnerközpont által támogatott erőforrásokat dokumentáló szerződés

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A **AgreementDocument** erőforrást jelenleg csak a Microsoft nyilvános Partnerközpont támogatja.

A **AgreementDocument erőforrás** egy, az előzetes verzióhoz és letöltéshez elérhető Microsoft-szerződési dokumentumot jelent.

## <a name="agreementdocument"></a>AgreementDocument (Szerződésdokumentum)

A **AgreementDocument erőforrás** a következő tulajdonságokat tartalmazza:

| Tulajdonság       | Típus   | Leírás                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| ország | sztring | Az ország vagy piac, amelyre a dokumentum vonatkozik. |
| language | sztring | A dokumentum honosított nyelve. |
| displayUri | sztring | A szerződésdokumentum böngészőben való előnézetére mutató hivatkozás.  |
| downloadUri |sztring | Hivatkozás a szerződésdokumentum letöltéséhez (Microsoft Word formátumban). |
