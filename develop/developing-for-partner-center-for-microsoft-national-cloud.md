---
title: Fejlesztés Partnerközpont Microsoft országos felhőihez
description: Partnerközpont SDK microsoftos országos felhők Partnerközpont fejlesztésekor.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d38a35fb88b4835716e429aeed731a0d55d9a669
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906454"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Fejlesztés Partnerközpont Microsoft országos felhőihez

**A következőkre** vonatkozik: Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Partnerközpont SDK-dokumentációval rendelkezik. Előfordulhat azonban, hogy egyes funkciók nem érhetők el a microsoftos Partnerközpont microsoftos országos felhőkre vonatkozó verzióiban.

A fejlesztőknek figyelembe kell vennie az SDK módosításait az alábbi Partnerközpont:

- [A 21Vianet által üzemeltetett Partnerközpont](#partner-center-operated-by-21vianet)
- [A Microsoft Cloud Germany Partnerközpontja](#partner-center-for-microsoft-cloud-germany)
- [A Microsoft Cloud for US Government Partnerközpontja](#partner-center-for-microsoft-cloud-for-us-government)

Minden Partnerközpont SDK cikk a megfelelő Partnerközpont sorolja fel. Az egyes felügyelt referenciacikkek a Követelmények szakaszban Partnerközpont a vonatkozó és újabb **verzióit** is.

## <a name="partner-center-operated-by-21vianet"></a>A 21Vianet által üzemeltetett Partnerközpont

A partnerek és a *21Vianet* *Partnerközpont* Partnerközpont közötti különbségek a következőek:

- Ügyfélfelhasználó vagy teljes partnerfelhasználó jelszavát nem állíthatja vissza programozott módon.

- Az Azure-előfizetések nem érhetők el.

- Az ügyfélfelhasználói licencek nem kezelhetők. Ehelyett az ügyfeleknek a felügyeleti Office 365 kell használniuk a licenceik kezeléséhez.

- Minden támogatási kérelem a 21Vianet Partnerközpont keresztül kezelhető. A szolgáltatáskérések és a szolgáltatásfrissítések nem érvényesek.

## <a name="partner-center-for-microsoft-cloud-germany"></a>A Microsoft Cloud Germany Partnerközpontja

> [!IMPORTANT]
> Az ügyfelek igényeinek fejlődése alapján a németországi felhőstratégia a globális felhőajánlatnak megfelelő új felhőrégiók németországi megvalósításához fog összpontosítani. Ezzel a fókuszban már nem fogadunk új ügyfeleket, és nem helyezünk üzembe új szolgáltatásokat a jelenleg elérhető Microsoft Cloud Germany szolgáltatásból. A meglévő ügyfelek továbbra is használhatjak a jelenleg elérhető felhőszolgáltatásokat, amelyeket a szükséges biztonsági frissítésekkel fogunk karbantartani.
>
> A 2018-ban elérhetővé vált új ügyfelek a jelenleg elérhető európai régiókat vagy a németországi új régiókat is használhatja. További információ: A Microsoft felhőszolgáltatásokat nyújt a németországi új [adatközpontok számára.](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/)

A Microsoft Cloud Germany *Partnerközpont* és Partnerközpont partnerek közötti *különbségek* a következőek:

- A partnerek nem hozhatnak létre felhasználókat az ügyfél szervezetéhez, és nem rendelhetnek hozzá szerepköröket.
  - A partnerek olvashatják a mezőket, de nem írhatják és nem frissítik azokat.
  - A partnereknek manuálisan kell létrehozniuk vagy frissíteniük az ügyfeleik felhasználóit Office 365 felügyeleti központban vagy a Azure Portal. Lásd [a Azure Active Directory dokumentációját.](/azure/active-directory/)

- Az ügyfélfelhasználói licencek nem kezelhetők a Microsoft Cloud Germany portálra vagy API-kra Partnerközpont portálon. Ehelyett a felügyeleti központot Office 365 Azure Active Directly Group licenckezelést kell használnia (hamarosan elérhető) a licencek kezeléséhez.
  - (Nem kötelező) használhatja az Azure AD Graph API-t. Lásd: [Licencek hozzárendelése felhasználóhoz.](/graph/api/user-assignlicense) A Partnerközpont Microsoft Cloud Germany esetében a helyett a Graph `https://graph.cloudapi.de` végpontot `https://graph.windows.net` használja.

- Ügyfélfelhasználó vagy teljes partnerfelhasználó jelszavát nem állíthatja vissza programozott módon. Használja a Office 365 felügyeleti központot vagy Azure Portal. Lásd: [Új jelszó megadása egy felhasználóhoz a Azure Active Directory.](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal) Az 1. lépésben be kell jelentkeznie a Microsoft Cloud Germany Azure Portal szolgáltatásba.

- A fejlesztőknek manuálisan kell regisztrálniuk az alkalmazásazonosítójukat, hogy Partnerközpont API-/SDK-funkciókat integrálni Partnerközpont Microsoft Cloud Germany számára készült alkalmazásukba. További információ: Register app details for Partnerközpont for Microsoft National Cloud (Alkalmazásadatok regisztrálása a [Microsoft országos felhőszolgáltatáshoz).](create-apps-for-partner-center-for-microsoft-national-clouds.md)

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>A Microsoft Cloud for US Government Partnerközpontja

A partnerek közötti különbségek *a* Partnerközpont és Partnerközpont *a Microsoft Cloud for US Government:*

- Office 365 előfizetések jelenleg nem érhetők el Partnerközpont előfizetések Microsoft Cloud for US Government.

- A meglévő partnereknek Microsoft Cloud for US Government új fiókokat kell létrehozniuk a Partnerközpont a Microsoft Cloud for US Government.

- Microsoft Cloud for US Government az ügyfeleknek egyetlen partnerrel kell tranzakciótuk.
  - A többcsatornás, valamint a többpartneres és a kéréskapcsolatok nem érvényesek a Microsoft Cloud for US Government-forgatókönyvekben meglévő ügyféllel. Ennek a korlátozásnak az az oka Office 365 jelenleg nem érhető el.

- A partnerek nem hozhatnak létre felhasználókat az ügyfél szervezetéhez, és nem rendelhetnek hozzá szerepköröket.
  - A partnerek olvashatják a mezőket, de nem írhatják és nem frissítik azokat. A partnereknek manuálisan kell létrehozniuk vagy frissíteniük az ügyfelek felhasználóit a Azure Portal. Lásd [a Azure Active Directory dokumentációját.](/azure/active-directory/)

- Ügyfélfelhasználó vagy teljes partnerfelhasználó jelszavát nem állíthatja vissza programozott módon. Használja az Azure Portalt. Lásd: [Új jelszó megadása egy felhasználóhoz a Azure Active Directory.](/azure/active-directory/active-directory-users-reset-password-azure-portal) Az 1. lépésben be kell jelentkeznie a Azure Portal a Microsoft Cloud for US Government.

- Az alkalmazáshoz Partnerközpont REST Microsoft Cloud for US Government végpont ugyanaz, mint a Partnerközpont: `https://api.partnercenter.microsoft.com` .

- A fejlesztőknek manuálisan kell regisztrálniuk az alkalmazásazonosítójukat, hogy Partnerközpont API-/SDK-funkciókat integrálni Partnerközpont alkalmazásukba Microsoft Cloud for US Government. További információ: Register app details for Partnerközpont for Microsoft National Cloud (Alkalmazásadatok regisztrálása a [Microsoft országos felhőszolgáltatáshoz).](create-apps-for-partner-center-for-microsoft-national-clouds.md)
