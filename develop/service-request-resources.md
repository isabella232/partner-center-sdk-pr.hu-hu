---
title: Szolgáltatáskérési erőforrások
description: A partnerek a partnerük nevében bejelentheti a szolgáltatáskimaradásokkal kapcsolatos szolgáltatásokat, vagy olyan műszaki támogatást kérhetnek, amelyet nem tudnak biztosítani.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 02a02e6a873ad8785150368f3d4b89af2b588529
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547359"
---
# <a name="service-request-resources"></a>Szolgáltatáskérési erőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A partnerek a partnerük nevében bejelentheti a szolgáltatáskimaradásokkal kapcsolatos szolgáltatásokat, vagy olyan műszaki támogatást kérhetnek, amelyet nem tudnak biztosítani.

## <a name="servicerequest"></a>ServiceRequest (Szolgáltatásrequest)

A partner által nyújtott szolgáltatáskérést ismerteti, beleértve a kérés előrehaladását.

| Tulajdonság         | Típus                                                          | Leírás                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Cím            | sztring                                                        | A szolgáltatáskérés címe.                                                           |
| Description      | sztring                                                        | A leírás.                                                                     |
| Súlyosság         | sztring                                                        | A súlyosság: "unknown", "critical", "moderate" vagy "minimal".                       |
| TámogatásitopicId (TámogatásitopicId)   | sztring                                                        | A támogatási témakör azonosítója.                                                         |
| TámogatásitopicName | sztring                                                        | A támogatási témakör neve.                                                       |
| Id               | sztring                                                        | A szolgáltatáskérés azonosítója.                                                       |
| Állapot           | sztring                                                        | A szolgáltatáskérés állapota: "nincs", "nyitott", "lezárt" vagy "figyelmet \_ igényel". |
| Szervezet     | [ServiceRequestOrganization](#servicerequestorganization)     | Az a szervezet, amelyhez a szolgáltatáskérés létre lesz hozva.                               |
| PrimaryContact (Elsődleges tranzakció)   | [ServiceRequestContact](#servicerequestcontact)               | A szolgáltatáskérés elsődleges kapcsolattartója.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | "Last Updated By" kapcsolattartó a szolgáltatáskérés módosításaiért.                        |
| TermékNév      | sztring                                                        | A szolgáltatáskérésnek megfelelő termék neve.                     |
| ProductId        | sztring                                                        | A termék azonosítója.                                                               |
| CreatedDate      | dátum                                                          | A szolgáltatáskérés létrehozásának dátuma.                                          |
| LastModifiedDate | dátum                                                          | A szolgáltatáskérés utolsó módosításának dátuma.                                 |
| LastClosedDate (Utolsó bezárás ésdátum)   | dátum                                                          | A szolgáltatáskérés utolsó lezárásának dátuma.                                   |
| FileLinks (Fájlkapcsolatok)        | [FileInfo erőforrások tömbje](utility-resources.md#fileinfo) | A szolgáltatáskéréshez kapcsolódó fájlhivatkozások gyűjteménye.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | Megjegyzés hozzáadható egy meglévő szolgáltatáskéréshez.                                  |
| Jegyzetek            | [ServiceRequestNotes tömb](#servicerequestnote)           | A szolgáltatáskéréshez hozzáadott megjegyzések gyűjteménye.                                  |
| CountryCode      | sztring                                                        | A szolgáltatáskérésnek megfelelő ország.                                    |
| Attribútumok       | ResourceAttributes (Erőforrás-attribútumok)                                            | A szolgáltatáskérésnek megfelelő metaadat-attribútumok.                        |

## <a name="servicerequestcontact"></a>ServiceRequestContact

Egy olyan kapcsolattartót ír le, amely szolgáltatáskérést hoz létre vagy módosít.

| Tulajdonság     | Típus                                                      | Leírás                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Szervezet | [ServiceRequestOrganization](#servicerequestorganization) | Az a szervezet, amelyhez a szolgáltatáskérés létre lesz hozva. |
| ContactId (Kapcsolatazonosító)    | sztring                                                    | A kapcsolattartó egyedi azonosítója.                               |
| LastName     | sztring                                                    | A kapcsolattartó vezetékneve.                          |
| FirstName    | sztring                                                    | A kapcsolattartó vezetékneve.                         |
| E-mail        | sztring                                                    | A kapcsolattartó e-mail-címe.                              |
| PhoneNumber  | sztring                                                    | A kapcsolattartó telefonszáma.                       |

## <a name="servicerequestnote"></a>ServiceRequestNote

Egy szolgáltatáskéréshez csatolt megjegyzést ír le.

| Tulajdonság      | Típus   | Leírás                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName (Létrehozási név) | sztring | A megjegyzés létrehozója neve.         |
| CreatedDate   | dátum   | A megjegyzés létrehozási dátuma és időpontja. |
| Szöveg          | sztring | A megjegyzés szövege.                        |

## <a name="servicerequestorganization"></a>ServiceRequestOrganization

Azt a szervezetet írja le, amelyhez a szolgáltatáskérés létre van hozva.

| Tulajdonság    | Típus   | Leírás                           |
|-------------|--------|---------------------------------------|
| Id          | sztring | A szervezet egyedi azonosítója.    |
| Name        | sztring | A szervezet neve.         |
| PhoneNumber | sztring | A szervezet telefonszáma. |

## <a name="supporttopic"></a>Támogatásitopikus

Egy támogatási témakört ismertet. A szolgáltatáskérések egy támogatási témakört határoznak meg, amely biztosítja azok gyors és hatékony feldolgozását.

| Tulajdonság    | Típus               | Leírás                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Név        | sztring             | A támogatási témakör neve.                                |
| Description | sztring             | A támogatási témakör leírása.                         |
| Id          | sztring             | A támogatási témakör egyedi azonosítója.                           |
| Attribútumok  | ResourceAttributes (Erőforrás-attribútumok) | A szolgáltatáskéréshez tartozó metaadat-attribútumok. |

