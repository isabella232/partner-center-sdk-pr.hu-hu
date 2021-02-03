---
title: Felügyelt szolgáltatás erőforrásai
description: A felügyelt szolgáltatások olyan szolgáltatások, amelyekhez a partner delegált rendszergazdai jogosultságokkal rendelkezik. A partnerek a felügyelt szolgáltatásaik nevében nyújthatnak támogatást a és a Fájlszolgáltatások számára.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767783"
---
# <a name="managed-service-resources"></a>Felügyelt szolgáltatás erőforrásai

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A felügyelt szolgáltatások olyan szolgáltatások, amelyekhez a partner delegált rendszergazdai jogosultságokkal rendelkezik. A partnerek a felügyelt szolgáltatásaik nevében nyújthatnak támogatást a és a Fájlszolgáltatások számára.

## <a name="managedservice"></a>ManagedService

A felügyelt szolgáltatás leírása.

| Tulajdonság   | Típus                | Leírás                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | sztring              | A felügyelt szolgáltatás azonosítója.                                  |
| Name       | sztring              | A felügyelt szolgáltatás neve.                         |
| GroupName  | sztring              | Annak a csoportnak a neve, amelyhez a szolgáltatás tartozik.      |
| Hivatkozások      | ManagedServiceLinks | A felügyelt szolgáltatásnak megfelelő erőforrás-hivatkozások. |
| Attribútumok | ResourceAttributes  | A szerződéshez tartozó metaadat-attribútumok.  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

Azokat a hivatkozásokat tartalmazza, amelyek lehetővé teszik, hogy a partner delegált rendszergazdai jogosultságokkal támogassa a szolgáltatást.

| Tulajdonság      | Típus | Leírás                 |
|---------------|------|-----------------------------|
| AdminService  | Hivatkozás | A felügyeleti szolgáltatás URI-ja.      |
| ServiceHealth | Hivatkozás | A szolgáltatás állapota URI-ja.     |
| ServiceTicket | Hivatkozás | A szolgáltatás jegyének URI-ja.     |
| Self          | Hivatkozás | A saját URI-ja.               |
| Következő          | Hivatkozás | Az elemek következő lapja.     |
| Előző      | Hivatkozás | Az elemek előző lapja. |

