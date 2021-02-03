---
title: Szolgáltatási kérelmek erőforrásai
description: A partnerek a partnerek nevében kérhetik a szolgáltatást a Microsoft által biztosított fennakadások bejelentésére vagy egyéb technikai támogatás igénylésére, amely nem alkalmas a szolgáltatás nyújtására.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 072f9eddaf9d854f1dcc8cc65f7928b6c95700fa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767824"
---
# <a name="service-request-resources"></a>Szolgáltatási kérelmek erőforrásai

**A következőkre vonatkozik**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A partnerek a partnerek nevében kérhetik a szolgáltatást a Microsoft által biztosított fennakadások bejelentésére vagy egyéb technikai támogatás igénylésére, amely nem alkalmas a szolgáltatás nyújtására.

## <a name="servicerequest"></a>ServiceRequest

A partner által benyújtott szolgáltatási kérelmet ismerteti, beleértve a kérés előrehaladását.

| Tulajdonság         | Típus                                                          | Leírás                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Cím            | sztring                                                        | A szolgáltatási kérelem címe.                                                           |
| Description      | sztring                                                        | A leírás.                                                                     |
| Súlyosság         | sztring                                                        | A súlyosság: "ismeretlen", "kritikus", "mérsékelt" vagy "minimális".                       |
| SupportTopicId   | sztring                                                        | A támogatási témakör azonosítója.                                                         |
| SupportTopicName | sztring                                                        | A támogatási témakör neve.                                                       |
| Id               | sztring                                                        | A szolgáltatási kérelem azonosítója.                                                       |
| Állapot           | sztring                                                        | A szolgáltatási kérelem állapota: "nincs", "Open", "Closed" vagy "Figyelem \_ szükséges". |
| Szervezet     | [ServiceRequestOrganization](#servicerequestorganization)     | Az a szervezet, amelyhez a szolgáltatási kérelmet létrehozták.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Az elsődleges kapcsolattartó a szolgáltatási kérelemben.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | "Utolsó frissítés:" Kapcsolatfelvétel a szolgáltatási kérelem módosításaival.                        |
| TermékNév      | sztring                                                        | A szolgáltatási kérelemnek megfelelő termék neve.                     |
| ProductId        | sztring                                                        | A termék azonosítója.                                                               |
| CreatedDate      | dátum                                                          | A szolgáltatási kérelem létrehozásának dátuma.                                          |
| LastModifiedDate | dátum                                                          | A szolgáltatáskérelem utolsó módosításának dátuma.                                 |
| LastClosedDate   | dátum                                                          | A szolgáltatáskérelem utolsó lezárt dátuma.                                   |
| FileLinks        | [fileinfo](utility-resources.md#fileinfo) -erőforrások tömbje | A szolgáltatási kérelemre vonatkozó Fájlszolgáltatások gyűjteménye.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | Megjegyzés is hozzáadható egy meglévő szolgáltatási kérelemhez.                                  |
| Jegyzetek            | [ServiceRequestNotes](#servicerequestnote) tömbje           | A szolgáltatási kérelemhez hozzáadott jegyzetek gyűjteménye.                                  |
| CountryCode      | sztring                                                        | A szolgáltatási kérelemnek megfelelő ország.                                    |
| Attribútumok       | ResourceAttributes                                            | A szolgáltatási kérelemhez tartozó metaadat-attribútumok.                        |

## <a name="servicerequestcontact"></a>ServiceRequestContact

A szolgáltatási kérelmeket létrehozó vagy módosító kapcsolattartót ismerteti.

| Tulajdonság     | Típus                                                      | Leírás                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Szervezet | [ServiceRequestOrganization](#servicerequestorganization) | Az a szervezet, amelyhez a szolgáltatási kérelmet létrehozták. |
| ContactId    | sztring                                                    | A partner egyedi azonosítója.                               |
| LastName     | sztring                                                    | A névjegy vezetékneve.                          |
| FirstName    | sztring                                                    | A partner vezetékneve.                         |
| E-mail        | sztring                                                    | A partner e-mail-címe.                              |
| PhoneNumber  | sztring                                                    | A partner telefonszáma.                       |

## <a name="servicerequestnote"></a>ServiceRequestNote

A szolgáltatási kérelemhez csatolt megjegyzés leírása.

| Tulajdonság      | Típus   | Leírás                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | sztring | A jegyzet létrehozójának neve.         |
| CreatedDate   | dátum   | A Megjegyzés létrehozásának dátuma és időpontja. |
| Szöveg          | sztring | A jegyzet szövege.                        |

## <a name="servicerequestorganization"></a>ServiceRequestOrganization

Leírja azt a szervezetet, amelyhez a szolgáltatási kérelmet létrehozták.

| Tulajdonság    | Típus   | Leírás                           |
|-------------|--------|---------------------------------------|
| Id          | sztring | A szervezet egyedi azonosítója.    |
| Name        | sztring | A szervezet neve.         |
| PhoneNumber | sztring | A szervezet telefonszáma. |

## <a name="supporttopic"></a>SupportTopic

Leírja a támogatási témakört. A szolgáltatási kérelmek olyan támogatási témakört határoznak meg, amely biztosítja, hogy gyorsan és hatékonyan dolgozzák fel őket.

| Tulajdonság    | Típus               | Leírás                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Név        | sztring             | A támogatási témakör neve.                                |
| Description | sztring             | A támogatási témakör leírása.                         |
| Id          | sztring             | A támogatási témakör egyedi azonosítója.                           |
| Attribútumok  | ResourceAttributes | A szolgáltatási kérelemhez tartozó metaadat-attribútumok. |

