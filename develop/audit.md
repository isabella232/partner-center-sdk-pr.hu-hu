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
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a><span data-ttu-id="eeb4d-103">A partner Center API-n keresztül elérhető naplózási műveletek, amelyek a partner Center-tevékenység rekordját jelenítik meg</span><span class="sxs-lookup"><span data-stu-id="eeb4d-103">Audit operations available via Partner Center API that show a record of Partner Center activity</span></span>

<span data-ttu-id="eeb4d-104">A partner Center API-k naplózási funkciókat biztosítanak, így a partner Center tevékenységeit is lekérheti.</span><span class="sxs-lookup"><span data-stu-id="eeb4d-104">The Partner Center APIs provide auditing features so you can get a record of Partner Center activity.</span></span>

<span data-ttu-id="eeb4d-105">A naplózási rekordokat lekérheti az előző 30 napban az aktuális dátumtól, illetve a kezdő dátummal és/vagy a befejezési dátummal megadott Dátumtartomány alapján.</span><span class="sxs-lookup"><span data-stu-id="eeb4d-105">You can retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="eeb4d-106">Vegye figyelembe azonban, hogy a teljesítmény miatt a tevékenység naplójának adatelérhetősége az előző 90 napra korlátozódik.</span><span class="sxs-lookup"><span data-stu-id="eeb4d-106">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="eeb4d-107">Az aktuális dátum előtt 90 nappal nagyobb kezdési dátummal rendelkező kérések esetén a rendszer rossz kérési kivételt (hibakód: 400) és megfelelő üzenetet kap.</span><span class="sxs-lookup"><span data-stu-id="eeb4d-107">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="retrieve-audit-records"></a><span data-ttu-id="eeb4d-108">Naplózási rekordok beolvasása</span><span class="sxs-lookup"><span data-stu-id="eeb4d-108">Retrieve audit records</span></span>

<span data-ttu-id="eeb4d-109">Egy partner felhasználó vagy alkalmazás által végrehajtott műveletek részletes naplózási rekordjainak beolvasása:</span><span class="sxs-lookup"><span data-stu-id="eeb4d-109">Get detailed historical audit records of operations performed by a partner user or application:</span></span>

- [<span data-ttu-id="eeb4d-110">Partnerközpont-tevékenység rekordjának lekérése</span><span class="sxs-lookup"><span data-stu-id="eeb4d-110">Get a record of Partner Center activity</span></span>](get-a-record-of-partner-center-activity-by-user.md)
- [<span data-ttu-id="eeb4d-111">Erőforrások naplózása</span><span class="sxs-lookup"><span data-stu-id="eeb4d-111">Auditing resources</span></span>](auditing-resources.md)