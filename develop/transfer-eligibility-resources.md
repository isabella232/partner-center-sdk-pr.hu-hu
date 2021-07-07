---
title: TransferEligibility erőforrások
description: A partnerek akkor hozhatnak létre átadást, ha az ügyfél a partnerrel való előfizetését egy másik partnernek való átadásra kéri.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f121d499abffb4c4dda688c2a91c25f83d2e863
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530208"
---
# <a name="transfereligibility-resources"></a>TransferEligibility erőforrások

A partnerek akkor hozhatnak létre átadást, ha az ügyfél a partnerrel való előfizetését egy másik partnernek való átadásra kéri. A TransferEligibility használatával ellenőrizheti, hogy egy előfizetés átvihető-e.

## <a name="transfereligibility"></a>TransferEligibility (Átvitelelhetőség)

A transferEligibility (átvitelelhetőség) szakaszt írja le.

| Tulajdonság              | Típus             | Leírás                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | sztring           | Az ügyfél előfizetés-azonosítója.                                                  |
| isEligible            | logikai             | Jelzi, hogy az előfizetés jogosult-e az átadásra.                         |
| Ok                | sztring           | Az ok tulajdonság elmagyarázza, hogy az előfizetés miért nem jogosult az átadásra. |