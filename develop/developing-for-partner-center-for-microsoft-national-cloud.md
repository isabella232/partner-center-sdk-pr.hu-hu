---
title: A Microsoft országos Felhőkhöz készült partneri központ fejlesztése
description: A Microsoft nemzeti Felhőkhöz tartozó partneri központ fejlesztésekor a partner Center SDK-val kapcsolatos különbségek.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7882846de0c591b21fe73345f560613f535d1788
ms.sourcegitcommit: 529b07030a874d644cf947790f4b53cdff438dd4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768148"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>A Microsoft országos Felhőkhöz készült partneri központ fejlesztése

**A következőkre vonatkozik:**

- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A partner Center egyetlen SDK-dokumentációval rendelkezik. Előfordulhat azonban, hogy néhány funkció nem érhető el a Microsoft országos Felhőkhöz tartozó partner Center-verziókban.

A fejlesztőknek meg kell fontolniuk az SDK változásait a partner Center következő verzióiban:

- [A 21Vianet által üzemeltetett partneri központ](#partner-center-operated-by-21vianet)
- [A Microsoft Cloud Germany Partnerközpontja](#partner-center-for-microsoft-cloud-germany)
- [A Microsoft Cloud for US Government Partnerközpontja](#partner-center-for-microsoft-cloud-for-us-government)

Az egyes partneri központ SDK-cikkek a megfelelő fiókpartner-verziókat listázza. Az egyes felügyelt referenciák a szükséges partneri központ-verziókat is felsorolják a **követelmények** szakaszban.

## <a name="partner-center-operated-by-21vianet"></a>A 21Vianet által üzemeltetett partneri központ

A *partner központ* és a *21Vianet által működtetett* partnerek közötti különbségek a következők:

- Felhasználói vagy teljes partner felhasználó jelszava nem állítható be programozott módon.

- Az Azure-előfizetések nem érhetők el.

- Az ügyfél felhasználójának licenceit nem kezelheti. Ehelyett az ügyfeleknek az Office 365 felügyeleti központot kell használniuk a licencek kezeléséhez.

- Az összes támogatási kérést a 21Vianet által működtetett fiókpartner-központ kezeli. A szolgáltatási kérelmek és a szolgáltatási frissítések nem érvényesek.

## <a name="partner-center-for-microsoft-cloud-germany"></a>A Microsoft Cloud Germany Partnerközpontja

> [!IMPORTANT]
> Az ügyfelek szükségleteinek alakulásán alapuló felhőalapú stratégiánk a németországi új Felhőbeli régiókat fogja figyelembe venni, amelyek összhangban vannak a globális felhőalapú ajánlattal. Ebben a fókuszban már nem fogadunk el új ügyfeleket, vagy nem helyezünk üzembe semmilyen új szolgáltatást a jelenleg elérhető Microsoft Cloud Németországon. A meglévő ügyfelek továbbra is használhatják a jelenleg elérhető Cloud Services szolgáltatást, amelyet a szükséges biztonsági frissítésekkel tartunk fenn.
>
> Az új ügyfelek a jelenleg elérhető európai régiókat vagy a németországi új régiókat használhatják, amikor elérhetővé válnak. További információ: a [Microsoft és a Cloud Services elérhetővé nyilvánítása a németországi új adatközpontokból](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/).

A partner *központ* és a *Microsoft Cloud Németország* közötti partner központ közötti különbségek a következők:

- A partnerek nem hozhatnak létre felhasználókat az ügyfél szervezete számára, vagy szerepköröket rendelhetnek hozzájuk.
  - A partnerek elolvashatják a mezőket, de nem tudják írni vagy frissíteni őket.
  - A partnereknek manuálisan kell létrehozniuk vagy frissíteniük az ügyfelek felhasználóit az Office 365 felügyeleti központban vagy a Azure Portalon keresztül. Lásd: [Azure Active Directory dokumentáció](/azure/active-directory/).

- Az ügyfél felhasználói számára a Microsoft Cloud Germany portál vagy API-k esetében nem kezelheti a licenceket. Ehelyett a licencek kezeléséhez az Office 365 felügyeleti központot vagy az Azure aktív közvetlen csoportos licencelés-kezelést (hamarosan) kell használnia.
  - (Nem kötelező) az Azure AD Graph API használhatja. Lásd: [licencek kiosztása felhasználóhoz](/graph/api/user-assignlicense). A Microsoft Cloud Germany-hez készült partner Center esetében ne felejtse el használni a Graph-végpontot `https://graph.cloudapi.de` `https://graph.windows.net` .

- Felhasználói vagy teljes partner felhasználó jelszava nem állítható be programozott módon. Használja az Office 365 felügyeleti központot vagy Azure Portal. Lásd: [a felhasználó jelszavának alaphelyzetbe állítása Azure Active Directoryban](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal). Az 1. lépésben be kell jelentkeznie a Microsoft Cloud Germany Azure Portal.

- A fejlesztőknek manuálisan kell regisztrálniuk az alkalmazás AZONOSÍTÓját a partner Center API/SDK funkcióinak az alkalmazásban való integrálásához a Microsoft Cloud Germany esetében. További információ: az [alkalmazás adatainak regisztrálása a Microsoft National Cloud Partner Centerhez](create-apps-for-partner-center-for-microsoft-national-clouds.md).

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>A Microsoft Cloud for US Government Partnerközpontja

A partner *központ* és a partner központ közötti, az *Egyesült Államok kormányzati* szerveinek Microsoft Cloud közötti különbségek a következők:

- Az Office 365-előfizetések jelenleg nem érhetők el a Microsoft Cloud az USA kormányzati szervei számára.

- Az USA kormányzati szerveinek Microsoft Cloudt támogató meglévő partnereknek új fiókokat kell létrehozniuk a partner Centerben Microsoft Cloud az USA kormányzati szerveinek.

- Microsoft Cloud az USA kormányzati ügyfeleinek egyetlen partnerrel kell tranzakciót biztosítaniuk.
  - A többcsatornás és a többpartneres kapcsolatok és a kérések kapcsolata egy meglévő ügyféllel Microsoft Cloudon belül az Egyesült Államok kormányzati forgatókönyvei esetében nem érvényes. Ez a korlátozás azért van, mert az Office 365 jelenleg nem érhető el.

- A partnerek nem hozhatnak létre felhasználókat az ügyfél szervezete számára, vagy szerepköröket rendelhetnek hozzájuk.
  - A partnerek elolvashatják a mezőket, de nem tudják írni vagy frissíteni őket. A partnereknek manuálisan kell létrehozniuk vagy frissíteniük a felhasználók ügyfeleit a Azure Portalban. Lásd: [Azure Active Directory dokumentáció](/azure/active-directory/).

- Felhasználói vagy teljes partner felhasználó jelszava nem állítható be programozott módon. Használja a Azure Portal. Lásd: [a felhasználó jelszavának alaphelyzetbe állítása Azure Active Directoryban](/azure/active-directory/active-directory-users-reset-password-azure-portal). Az 1. lépésben be kell jelentkeznie a Azure Portalba az Egyesült Államok kormányának Microsoft Cloud.

- A partner központhoz tartozó REST-végpontok a Microsoft Cloud az USA kormányzati szerveinek esetében ugyanazok, mint a partner Centerben: `https://api.partnercenter.microsoft.com` .

- A fejlesztőknek manuálisan kell regisztrálniuk az alkalmazás AZONOSÍTÓját a partner Center API/SDK funkcióinak az alkalmazásban való integrálásához az USA kormányzati szerveinek Microsoft Cloud. További információ: az [alkalmazás adatainak regisztrálása a Microsoft National Cloud Partner Centerhez](create-apps-for-partner-center-for-microsoft-national-clouds.md).
