---
title: A partner Center API-forgatókönyvei
description: Ismerje meg, hogyan használhatják a Cloud Solution Provider program partnerei a partner Center API-t az ügyfelek fiókjainak, rendeléseinek, támogatásának és számlázásának programozott kezeléséhez.
ms.date: 10/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14dbd501e3d075c3880fae6f362feef797cba133
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768512"
---
# <a name="partner-center-api-scenarios-that-let-you-programmatically-manage-customer-accounts"></a>A partner Center API-forgatókönyvei, amelyekkel programozott módon kezelheti az ügyfelek fiókjait

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ez a cikk a felhőalapú megoldás-szolgáltatói programban részt vevő partnerek néhány módját ismerteti a partner Center API-val programozott módon felügyelheti a következő területeket, például:

- Felhasználói fiókok
- Orders (rendelések)
- Előfizetések
- Támogatás
- Számlázás

A partnervállalat különböző verziói érhetők el, amelyek különböző képességekkel rendelkeznek. Nem minden forgatókönyv támogatott a partner Center összes verziójában. További információért lásd: [a Microsoft nemzeti felhőhöz készült partneri központ fejlesztése](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="scenarios-supported-by-the-partner-center-sdk"></a>A partner Center SDK által támogatott forgatókönyvek

A következő forgatókönyvek mindegyike három különböző módon hajtható végre:

- Manuálisan a [partner Center](https://partner.microsoft.com/dashboard) irányítópultján.

- Programozott módon a partner Center által felügyelt API használatával.

- Programozott módon a partner Center REST API használatával.

| További információ a támogatott forgatókönyvekről:  | Tekintse meg ezt az erőforrást:     |
|----------------------------------|--------------------------|
| **Elemzés:** Ismerje meg, hogyan kérhet le elemzési adatokat az Azure-használattal,-előfizetésekkel,-licencekkel vagy-hivatkozásokkal kapcsolatban.         | [Elemzés](usage-analytics.md)  |
| **Naplózási műveletek:** Ismerje meg, hogyan kérheti le a partner Center tevékenységeit és műveleteit tartalmazó korábbi naplózási rekordokat. | [Auditálási műveletek](audit.md)                     |
| **Eszközök üzembe helyezése:** További információ az eszközök konfigurációs házirendjeiről, az eszközök kötegek használatáról és az eszközök metaadatairól. Ezek a forgatókönyvek az eszköz konfigurációs házirendjeinek hozzáadását, törlését, frissítését és beolvasását foglalják magukban.    | [Eszköz üzembe helyezése](device-deployment.md)  |
| **Fiókok és profilok:** Ismerje meg, hogyan kérheti vagy frissítheti a partner számlázási profilokat, a jogi profilokat, az MPN-profilt, az üzleti profilokat vagy a támogatási profilokat Megtekintheti az ügyfelek és a közvetett viszonteladók listáját is. | [Fiókok és profilok kezelése](manage-profiles-and-information.md)                                                                        |
| **Számlázás:** Ismerje meg a számlázási ciklust, az Azure-díjszabást és az Azure-kihasználtsági rekordokat, a számlák beszerzését, a partner folyószámla-egyenlegének beszerzését vagy az ügyfélszolgálati költségek beszerzését.  | [Számlázás kezelése](manage-billing.md)   |
| **Azure-kiadások:** Információk az Azure-költségekről és a partnerek használatáról, az ügyfél-előfizetések használatáról, a mért használatról és az ügyfél-használati költségvetésről. A forgatókönyvek azt is tartalmazzák, hogyan lehet frissíteni az ügyfél-használati költségvetést. | [Azure-költség](azure-spending.md)  |
| **Felhasználói fiókok kezelése:** Ismerje meg, hogyan végezheti el az ügyfél-fiókok felügyeletének számos aspektusát, például az ügyfelek fiókjainak létrehozását és törlését, az ügyfél felhasználói fiókjainak kezelését, az ügyfél-fiókadatok felügyeletét és érvényesítését, a felhasználói fiókok kezelését és a licencek hozzárendelését.  | [Ügyfelek kezelése](manage-customers.md)  |
| **Megrendelések kezelése:** Ismerje meg, hogyan kezelheti az ügyfelek rendeléseit és előfizetéseit programozott módon. Ez a rész magában foglalja az Azure-foglalások megvásárlását, a megrendelések létrehozását, a katalógusból származó ajánlatok beszerzését és a próbaverziós átalakítási ajánlatok   | [Megrendelések kezelése](manage-orders.md)  |
| **Támogatás biztosítása:** Megtudhatja, hogyan felügyelheti az ügyfelek szolgáltatásait, hogyan kérheti le vagy frissítheti az előfizetések támogatási partnereit, és hogyan kezelheti a szolgáltatási kérelmeket.  | [Támogatás biztosítása](provide-support.md)   |
| **Hivatkozások:** Megtudhatja, hogyan hozhat létre átirányítást, hogyan kérheti le az átirányítási listát, vagy frissítheti az átirányítást.  | [Javaslatok](/partner/develop/referrals)  |
| **Segédprogramok:** Megtudhatja, hogyan érvényesítheti a címeket, beolvashatja a címek formázási szabályait a piacon, ellenőrizheti a tartomány elérhetőségét, törölheti az ügyfél fiókját az integrációs munkaterületről, vagy megkérheti a partner Center tevékenységét | [Segédprogramok](utilities.md)  |
| **Biztonság:** A többtényezős hitelesítéssel (MFA) kapcsolatos REST API-k ismertetése a partner Centerben. Ezek az API-k segítenek kikényszeríteni az MFA-t a partner bérlő minden felhasználói fiókjánál.  | [Partneri biztonsági követelmények állapota](partner-security-requirements.md)  |

## <a name="next-steps"></a>Következő lépések

- [Lásd a partneri központ mintáit](partner-center-samples.md)
- [Útmutató az első lépésekhez](get-started.md)