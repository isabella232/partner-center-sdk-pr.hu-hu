---
title: Felügyelt szolgáltatási erőforrások
description: A felügyelt szolgáltatások olyan szolgáltatások, amelyekhez a partner rendszergazdai jogosultságokat delegált. A partnerek támogatást és fájlszolgáltatás-kéréseket nyújthatnak a felügyelt szolgáltatásaik nevében.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 582efe75fd18a9174dd5dc173c290bee25443ee9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548124"
---
# <a name="managed-service-resources"></a>Felügyelt szolgáltatási erőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A felügyelt szolgáltatások olyan szolgáltatások, amelyekhez a partner rendszergazdai jogosultságokat delegált. A partnerek támogatást és fájlszolgáltatás-kéréseket nyújthatnak a felügyelt szolgáltatásaik nevében.

## <a name="managedservice"></a>ManagedService

Egy felügyelt szolgáltatást ismertet.

| Tulajdonság   | Típus                | Leírás                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | sztring              | A felügyelt szolgáltatás azonosítója.                                  |
| Name       | sztring              | A felügyelt szolgáltatás neve.                         |
| GroupName (Csoportnév)  | sztring              | Annak a csoportnak a neve, amelyhez a szolgáltatás tartozik.      |
| Hivatkozások      | ManagedServiceLinks | A felügyelt szolgáltatásnak megfelelő erőforrás-hivatkozások. |
| Attribútumok | ResourceAttributes (Erőforrás-attribútumok)  | A szerződésnek megfelelő metaadat-attribútumok.  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

Tartalmazza azokat a hivatkozásokat, amelyek lehetővé teszik, hogy a delegált rendszergazdai engedélyekkel rendelkező partner támogatást nyújtson a szolgáltatáshoz.

| Tulajdonság      | Típus | Leírás                 |
|---------------|------|-----------------------------|
| AdminService  | Hivatkozás | A felügyeleti szolgáltatás URI-ját.      |
| ServiceHealth (Szolgáltatás-egészség) | Hivatkozás | A szolgáltatás állapot-URI-ját.     |
| ServiceTicket (Szolgáltatáscsomóta) | Hivatkozás | A szolgáltatásjegy URI-ját.     |
| Self          | Hivatkozás | Az ön-URI.               |
| Következő          | Hivatkozás | Az elemek következő oldala.     |
| Előző      | Hivatkozás | Az elemek előző oldala. |

