---
title: Felügyelt szolgáltatási erőforrások
description: A felügyelt szolgáltatások olyan szolgáltatások, amelyekhez a partner rendszergazdai jogosultságokat delegált. A partnerek támogatást és fájlszolgáltatás-kéréseket nyújthatnak a felügyelt szolgáltatásaik nevében.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 066c9f2a0d5ca8d03553508c2b471ca49735406a5a0566bf48b0773385c129f7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994387"
---
# <a name="managed-service-resources"></a>Felügyelt szolgáltatási erőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A felügyelt szolgáltatások olyan szolgáltatások, amelyekhez a partner rendszergazdai jogosultságokat delegált. A partnerek támogatást és fájlszolgáltatás-kéréseket nyújthatnak a felügyelt szolgáltatásaik nevében.

## <a name="managedservice"></a>ManagedService

Egy felügyelt szolgáltatást ismertet.

| Tulajdonság   | Típus                | Description                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | sztring              | A felügyelt szolgáltatás azonosítója.                                  |
| Name       | sztring              | A felügyelt szolgáltatás neve.                         |
| GroupName (Csoport neve)  | sztring              | Annak a csoportnak a neve, amelyhez a szolgáltatás tartozik.      |
| Hivatkozások      | ManagedServiceLinks | A felügyelt szolgáltatásnak megfelelő erőforrás-hivatkozások. |
| Attribútumok | ResourceAttributes (Erőforrás-attribútumok)  | A szerződésnek megfelelő metaadat-attribútumok.  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

Tartalmazza azokat a hivatkozásokat, amelyek lehetővé teszik, hogy a delegált rendszergazdai engedélyekkel rendelkező partner támogatást nyújtson a szolgáltatáshoz.

| Tulajdonság      | Típus | Description                 |
|---------------|------|-----------------------------|
| AdminService  | Hivatkozás | A felügyeleti szolgáltatás URI-ját.      |
| ServiceHealth (Szolgáltatás-egészség) | Hivatkozás | A szolgáltatás állapot-URI-ját.     |
| ServiceTicket (Szolgáltatáscsomóta) | Hivatkozás | A szolgáltatásjegy URI-ját.     |
| Self          | Hivatkozás | Az ön-URI.               |
| Következő          | Hivatkozás | Az elemek következő oldala.     |
| Előző      | Hivatkozás | Az elemek előző oldala. |

