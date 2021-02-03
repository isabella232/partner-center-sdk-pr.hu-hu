---
title: Szerződés – dokumentum erőforrásai
description: A AgreementDocument-erőforrás az előzetes verzióra és a letöltésre vonatkozó Microsoft-szerződési dokumentum. A Microsoft nyilvános felhőben a partner Center támogatja.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 4805d25b0838bf922b81bebd998810c3f6a809c3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768560"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a>A Microsoft nyilvános felhőben a partner Center által támogatott szerződési dokumentumok erőforrásai

**A következőkre vonatkozik:**

- Partnerközpont

A **AgreementDocument** erőforrást jelenleg csak a *Microsoft nyilvános felhőben* támogatja a partner Center. Ez az erőforrás nem alkalmazható a következőre:

- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A **AgreementDocument** -erőforrás az előzetes verzió és a letöltés számára elérhető Microsoft-szerződési dokumentumot jelöli.

## <a name="agreementdocument"></a>AgreementDocument

Az **AgreementDocument** -erőforrás a következő tulajdonságokat tartalmazza:

| Tulajdonság       | Típus   | Leírás                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| ország | sztring | Az ország vagy piac, amelyre ez a dokumentum vonatkozik. |
| language | sztring | Az a nyelv, amelyben a dokumentum honosítva van. |
| displayUri | sztring | Egy hivatkozás, amely a szerződés dokumentumának előnézetét jeleníti meg egy böngészőben.  |
| downloadUri |sztring | A szerződési dokumentum letöltésére szolgáló hivatkozás (Microsoft Word Format). |
