---
title: Partnerközpont API-forgatókönyvek
description: Megtudhatja, Felhőszolgáltató programpartnerek hogyan kezelhetik programozott módon az ügyfélfiókokat, a megrendeléseket, a támogatást és a számlázást a Partnerközpont API-val.
ms.date: 10/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d74400a975323d5f0f276dbdece3621d8b47a609
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547478"
---
# <a name="partner-center-api-scenarios-that-let-you-programmatically-manage-customer-accounts"></a>Partnerközpont API-forgatókönyvek, amelyek lehetővé teszi az ügyfélfiókok programozott kezelését

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Középpont a Microsoft Cloud for US Government

Ez a cikk néhány olyan módszert ismertet, amelyek segítségével a Felhőszolgáltató program partnerei a Partnerközpont API-val programozott módon kezelhetik az alábbi területeket:

- Ügyfélfiókok
- Orders (rendelések)
- Előfizetések
- Támogatás
- Számlázás

A szolgáltatásoknak különböző verziói Partnerközpont, amelyek különböző képességeket tartalmaznak. Nem minden forgatókönyv támogatott a Partnerközpont. További információ: Fejlesztés Partnerközpont [a Microsoft országos felhőjében.](developing-for-partner-center-for-microsoft-national-cloud.md)

## <a name="scenarios-supported-by-the-partner-center-sdk"></a>A Partnerközpont SDK

Az alábbi forgatókönyvek közül háromféleképpen teljesíthet:

- Manuálisan a [Partnerközpont](https://partner.microsoft.com/dashboard) irányítópulton.

- Programozott módon, a Partnerközpont API használatával.

- Programozott módon a Partnerközpont REST API.

| További információ a támogatott forgatókönyvekről:  | Tekintse meg ezt az erőforrást:     |
|----------------------------------|--------------------------|
| **Elemzés:** Ismerje meg, hogyan lehet elemzési adatokat lekérni az Azure-használatról, -előfizetésről, -licencekről és -ajánlásokról.         | [Elemzés](usage-analytics.md)  |
| **Naplózási műveletek:** Ismerje meg, hogyan lehet lekérni a Partnerközpont és műveletek előzményrekordjait. | [Auditálási műveletek](audit.md)                     |
| **Eszköztelepítések:** Megismeri az eszközkonfigurációs szabályzatokat, az eszközkötkötekkel való munkát és az eszköz metaadatait. Ilyen forgatókönyv például az eszközkonfigurációs szabályzatok hozzáadása, törlése, frissítése és beolvasása.    | [Eszköz üzembe helyezése](device-deployment.md)  |
| **Fiókok és profilok:** Ismerje meg, hogyan lehet lekért vagy frissíthet partner számlázási profilokat, jogi profilokat, MPN-profilokat, üzleti profilokat vagy támogatási profilokat. Le is kaphatja az ügyfelek vagy közvetett viszonteladók listáját. | [Fiókok és profilok kezelése](manage-profiles-and-information.md)                                                                        |
| **Számlázás:** Olyan területekről tanulhat, mint a számlázási ciklus módosítása, az Azure-díjszabások és az Azure-beli kihasználtsági rekordok lekérte, a számlák lekérte, a partner aktuális számlaegyenlegének lekérte vagy az ügyfélszolgálati költségek lekérte.  | [Számlázás kezelése](manage-billing.md)   |
| **Azure-kiadások:** Információk az Azure-kiadásokról és -partnerek használatáról, az ügyfél-előfizetések használatáról, a forgalmi díjas használatról és az ügyfelek használati költségvetéséről. A forgatókönyvek az ügyfelek használati költségvetésének frissítését is magukban foglalják. | [Azure-költség](azure-spending.md)  |
| **Ügyfélfiókok kezelése:** Megtudhatja, hogyan adhatja meg az ügyfélfiókok kezelésének számos aspektusát, például az ügyfélfiókok vagy az ügyfél felhasználói fiókjainak létrehozását és törlését, az ügyfélfiókok részleteinek kezelését és érvényességét, a felhasználói fiókok kezelését és a licencek hozzárendelését.  | [Ügyfelek kezelése](manage-customers.md)  |
| **Rendelések kezelése:** Ismerje meg, milyen módokon kezelheti programozott módon az ügyfelek rendeléseit és előfizetéseit. Ez a terület magában foglalja az Azure Reservations megvásárlását, a rendelések létrehozását, az ajánlatok katalógusból való beszerzését és a próbakonverziós ajánlatok felügyeletét.   | [Megrendelések kezelése](manage-orders.md)  |
| **Támogatás biztosítása:** Megtudhatja, hogyan felügyelheti az ügyfelek szolgáltatásait, hogyan kérhet le vagy frissíthet támogatási kapcsolattartókat egy előfizetéshez, és hogyan kezelheti a szolgáltatáskéréseket.  | [Támogatás biztosítása](provide-support.md)   |
| **Ajánlások:** Megtudhatja, hogyan hozhat létre terjesztést, hogyan olvashatja be a hivatkozások listáját, és hogyan frissítheti a hivatkozásokat.  | [Javaslatok](/partner/develop/referrals)  |
| **Segédprogramok:** Megtudhatja, hogyan érvényesíthet egy címet, hogyan olvashatja be a címformázási szabályokat piac szerint, hogyan ellenőrizheti a tartományok rendelkezésre állását, hogyan törölheti az ügyfélfiókot az integrációs Partnerközpont vagy hogyan olvashatja be a Partnerközpont rekordját. | [Segédprogramok](utilities.md)  |
| **Biztonság:** Ismerje meg a többtényezős hitelesítéshez (MFA) kapcsolódó REST API-kat a Partnerközpont. Ezek az API-k segítenek kikényszeríteni az MFA-t a partnerbérlő minden felhasználói fiókjához.  | [Partnerbiztonsági követelmények állapota](partner-security-requirements.md)  |

## <a name="next-steps"></a>Következő lépések

- [Lásd a Partnerközpont mintákat](partner-center-samples.md)
- [Útmutató az első lépésekhez](get-started.md)