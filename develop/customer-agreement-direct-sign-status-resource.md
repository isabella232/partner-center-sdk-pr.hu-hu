---
title: Egy ügyfél-szerződés közvetlen aláírása (közvetlen elfogadás) állapota.
description: A DirectSignedCustomerAgreementStatus erőforrás az ügyfél-szerződés közvetlen aláírása (közvetlen elfogadás) állapotát jelöli.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767739"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a>Az ügyfél-szerződés közvetlen aláírása (közvetlen elfogadás) állapota

**A következőkre vonatkozik:**

- Partnerközpont

A **DirectSignedCustomerAgreementStatus** erőforrást jelenleg csak a Microsoft nyilvános felhőben támogatja a partner Center.

Ez az erőforrás *nem alkalmazható* a következőre:

- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A **DirectSignedCustomerAgreementStatus** erőforrás az ügyfél-szerződés közvetlen elfogadásának állapotát jelöli.

## <a name="directsignedcustomeragreementstatus"></a>DirectSignedCustomerAgreementStatus

A **DirectSignedCustomerAgreementStatus** -erőforrás a következő tulajdonságokat tartalmazza:

| Tulajdonság       | Típus   | Leírás                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| isSigned | boolean | Azt jelzi, hogy az ügyfél közvetlenül aláírta-e az ügyfél szerződését (elfogadták-e). |
