---
title: Naplózási tevékenység Partnerközpont naplózása
description: Megismerheti a Partnerközpont API naplózási műveleteinek típusát, amelyek segítségével rögzítheti a Partnerközpont tevékenységeket.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0e8010bde75bee4c4954034d8f61f19b076d96349e4a05807e272ca88efbc2fa
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994268"
---
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a>Az API-Partnerközpont elérhető naplózási műveletek, amelyek a Partnerközpont rekordját mutatják

A Partnerközpont API-k naplózási funkciókat biztosítanak, így ön rögzítheti a Partnerközpont tevékenységeket.

Az előző 30 nap naplórekordjait az aktuális dátumból vagy a kezdő és/vagy a záró dátum megadva megadott dátumtartományból is lekérheti. Vegye figyelembe azonban, hogy teljesítménybeli okokból a tevékenységnapló adatainak rendelkezésre állása az előző 90 napra van korlátozva. Az aktuális dátum előtti 90 napnál korábbi kezdési dátumú kérések hibás kérési kivételt (hibakód: 400) és egy megfelelő üzenetet kapnak.

## <a name="retrieve-audit-records"></a>Naplórekordok lekérése

Lekérte a partnerfelhasználó vagy alkalmazás által végrehajtott műveletek részletes naplórekordjait:

- [Partnerközpont-tevékenység rekordjának lekérése](get-a-record-of-partner-center-activity-by-user.md)
- [Erőforrások naplózása](auditing-resources.md)