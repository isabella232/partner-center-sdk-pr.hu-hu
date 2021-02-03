---
title: A partner Center tevékenységének naplózási műveletei
description: Ismerje meg a partner Center API-naplózási műveleteinek típusát, amelyekkel a partner Center-tevékenységek rekordját kérheti le.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 019bebe40c43f6ee1c2ac7da381a86ca190702d4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768536"
---
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a>A partner Center API-n keresztül elérhető naplózási műveletek, amelyek a partner Center-tevékenység rekordját jelenítik meg

A partner Center API-k naplózási funkciókat biztosítanak, így a partner Center tevékenységeit is lekérheti.

A naplózási rekordokat lekérheti az előző 30 napban az aktuális dátumtól, illetve a kezdő dátummal és/vagy a befejezési dátummal megadott Dátumtartomány alapján. Vegye figyelembe azonban, hogy a teljesítmény miatt a tevékenység naplójának adatelérhetősége az előző 90 napra korlátozódik. Az aktuális dátum előtt 90 nappal nagyobb kezdési dátummal rendelkező kérések esetén a rendszer rossz kérési kivételt (hibakód: 400) és megfelelő üzenetet kap.

## <a name="retrieve-audit-records"></a>Naplózási rekordok beolvasása

Egy partner felhasználó vagy alkalmazás által végrehajtott műveletek részletes naplózási rekordjainak beolvasása:

- [Partnerközpont-tevékenység rekordjának lekérése](get-a-record-of-partner-center-activity-by-user.md)
- [Erőforrások naplózása](auditing-resources.md)