---
title: Partnerközpont API-forgatókönyvek
description: Megtudhatja, Felhőszolgáltató programpartnerek hogyan kezelhetik programozott módon az ügyfélfiókokat, a megrendeléseket, a támogatást és a számlázást a Partnerközpont API-val.
ms.date: 10/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a5aac400e115ef0e58452e41edd9846d683d0b6912a9f651ea49d75d5f15bbf7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989491"
---
# <a name="partner-center-api-scenarios-that-let-you-programmatically-manage-customer-accounts"></a>Partnerközpont API-forgatókönyvek, amelyek lehetővé teszi az ügyfélfiókok programozott kezelését

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Középre Microsoft Cloud for US Government

Ez a cikk néhány olyan módszert ismertet, amelyek segítségével a Felhőszolgáltató program partnerei a Partnerközpont API-val programozott módon kezelhetik a következő területeket:

- Ügyfélfiókok
- Orders (rendelések)
- Előfizetések
- Támogatás
- Számlázás

A szolgáltatásnak különböző verziói Partnerközpont, amelyek különböző képességeket tartalmaznak. Nem minden forgatókönyv támogatott a Partnerközpont. További információ: [Developing for Partnerközpont for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md)..

## <a name="scenarios-supported-by-the-partner-center-sdk"></a>A Partnerközpont SDK

Az alábbi forgatókönyvek közül háromféleképpen teljesíthet:

- Manuálisan a [Partnerközpont](https://partner.microsoft.com/dashboard) irányítópulton.

- Programozott módon, a Partnerközpont API használatával.

- Programozott módon, a Partnerközpont REST API.

| További információ a támogatott forgatókönyvekről:  | Tekintse meg ezt az erőforrást:     |
|----------------------------------|--------------------------|
| **Elemzés:** Ismerje meg, hogyan lehet elemzési adatokat lekérni az Azure-használatról, -előfizetésről, -licencekről és -ajánlásokról.         | [Elemzés](usage-analytics.md)  |
| **Naplózási műveletek:** Ismerje meg, hogyan lehet lekérni a Partnerközpont és műveletek előzményrekordjait. | [Auditálási műveletek](audit.md)                     |
| **Eszköztelepítések:** Megismeri az eszközkonfigurációs szabályzatokat, az eszközkötkötekkel való munkát és az eszköz metaadatait. Ilyen forgatókönyv például az eszközkonfigurációs szabályzatok hozzáadása, törlése, frissítése és leolvasása.    | [Eszköz üzembe helyezése](device-deployment.md)  |
| **Fiókok és profilok:** Megtudhatja, hogyan szerezheti be vagy frissítheti a partner számlázási profiljait, jogi profiljait, MPN-profiljait, üzleti profiljait vagy támogatási profiljait. Le is kaphatja az ügyfelek vagy közvetett viszonteladók listáját. | [Fiókok és profilok kezelése](manage-profiles-and-information.md)                                                                        |
| **Számlázás:** Ismerje meg a számlázási ciklust, az Azure-díjszabások és az Azure-kihasználtsági rekordok lekért, a számlák lekért, a partner aktuális számlaegyenlegének lekért vagy az ügyfélszolgálati költségek lekért adatait.  | [Számlázás kezelése](manage-billing.md)   |
| **Azure-kiadások:** Lekért információk az Azure-kiadásokról és -partnerhasználatról, az ügyfél-előfizetések használatáról, a forgalmi díjas használatról és az ügyfelek használati költségvetéséről. A forgatókönyvek az ügyfelek használati költségvetésének frissítését is magukban foglalják. | [Azure-költség](azure-spending.md)  |
| **Ügyfélfiókok kezelése:** Megtudhatja, hogyan adhatja meg az ügyfélfiókok kezelésének számos aspektusát, például hogyan lehet létrehozni és törölni az ügyfélfiókokat vagy az ügyfelek felhasználói fiókjait, hogyan lehet az ügyfélfiókok adatait kezelik és érvényesítik, hogyan kezelik a felhasználói fiókokat és hogyan rendelhetnek hozzá licenceket.  | [Ügyfelek kezelése](manage-customers.md)  |
| **Rendelések kezelése:** Ismerje meg, milyen módokon kezelheti programozott módon az ügyfelek rendeléseit és előfizetéseit. Ez a terület magában foglalja az Azure Reservations megvásárlását, a megrendelések létrehozását, az ajánlatok katalógusból való beszerzését és a próbakonverziós ajánlatok felügyeletét.   | [Megrendelések kezelése](manage-orders.md)  |
| **Támogatás biztosítása:** Megtudhatja, hogyan felügyelheti az ügyfelek szolgáltatásait, hogyan kérhet le vagy frissíthet támogatási kapcsolattartókat egy előfizetéshez, és hogyan kezelheti a szolgáltatáskéréseket.  | [Támogatás biztosítása](provide-support.md)   |
| **Hivatkozások:** Megtudhatja, hogyan hozhat létre terjesztést, hogyan olvashatja be a hivatkozások listáját, vagy frissítheti a terjesztést.  | [Javaslatok](/partner/develop/referrals)  |
| **Segédprogramok:** Megtudhatja, hogyan ellenőrizheti a címeket, hogyan olvashatja be a címformázási szabályokat piac szerint, hogyan ellenőrizheti a tartományok rendelkezésre állását, hogyan törölhet ügyfélfiókot az integrációs Partnerközpont vagy hogyan Partnerközpont le. | [Segédprogramok](utilities.md)  |
| **Biztonság:** Ismerje meg a többtényezős hitelesítéshez (MFA) kapcsolódó REST API-kat a Partnerközpont. Ezek az API-k segítenek kikényszeríteni az MFA-t a partnerbérlőben minden egyes felhasználói fiókhoz.  | [Partnerbiztonsági követelmények állapota](partner-security-requirements.md)  |

## <a name="next-steps"></a>Következő lépések

- [Lásd a Partnerközpont mintákat](partner-center-samples.md)
- [Útmutató az első lépésekhez](get-started.md)