---
title: TransferEligibility erőforrások
description: A partnerek akkor hozhatnak létre átadást, ha az ügyfél a partnerrel való előfizetését egy másik partnernek való átadásra kéri.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ffe72aa04de17cf6e45e49e9fdbec8ba08da2deed89f5d54425a17825c91a53a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996648"
---
# <a name="transfereligibility-resources"></a>TransferEligibility erőforrások

A partnerek akkor hozhatnak létre átadást, ha az ügyfél a partnerrel való előfizetését egy másik partnernek való átadásra kéri. A TransferEligibility használatával ellenőrizheti, hogy az előfizetés átvihető-e.

## <a name="transfereligibility"></a>TransferEligibility (Átvitelelhetőség)

A transferEligibility (átvitelelhetőség) szakaszt írja le.

| Tulajdonság              | Típus             | Description                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | sztring           | Az ügyfél előfizetés-azonosítója.                                                  |
| isEligible            | logikai             | Jelzi, hogy az előfizetés jogosult-e az átadásra.                         |
| Ok                | sztring           | Az ok tulajdonság elmagyarázza, hogy az előfizetés miért nem jogosult az átadásra. |