---
title: Fejlesztés a Partnerközpont microsoftos országos felhőkhöz
description: Partnerközpont SDK microsoftos országos felhők Partnerközpont fejlesztése során.
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8b9b3c3b9a1a1173cf8f3e79f60e629e3d34ea13ecce2e7a2c74924bde2b7d1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994863"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Fejlesztés a Partnerközpont microsoftos országos felhőkhöz

**A következőkre** vonatkozik: Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Partnerközpont SDK-dokumentációval rendelkezik. Előfordulhat azonban, hogy egyes funkciók nem érhetők el a Microsoft országos felhőszolgáltatásai Partnerközpont verziójában.

A fejlesztőknek figyelembe kell vennie az SDK módosításait a következő Partnerközpont:

- [A 21Vianet által üzemeltetett Partnerközpont](#partner-center-operated-by-21vianet)
- [A Microsoft Cloud Germany Partnerközpontja](#partner-center-for-microsoft-cloud-germany)
- [A Microsoft Cloud for US Government Partnerközpontja](#partner-center-for-microsoft-cloud-for-us-government)

Minden Partnerközpont SDK cikk a megfelelő Partnerközpont sorolja fel. Az egyes felügyelt referenciacikkek a Követelmények szakaszban Partnerközpont megfelelő verziókat **is felsorolják.**

## <a name="partner-center-operated-by-21vianet"></a>A 21Vianet által üzemeltetett Partnerközpont

A 21Vianet által *Partnerközpont* *21Vianet* által Partnerközpont partnerek közötti különbségek a következőek:

- Az ügyfélfelhasználók és a teljes partnerfelhasználók jelszavát nem állíthatja vissza programozott módon.

- Az Azure-előfizetések nem érhetők el.

- Az ügyfélfelhasználó licenceit nem kezelheti. Ehelyett az ügyfeleknek a felügyeleti Office 365 kell használniuk a licenceik kezeléséhez.

- Az összes támogatási kérelem kezelése a 21Vianet Partnerközpont keresztül, a 21Vianeten keresztül. A szolgáltatáskérések és a szolgáltatásfrissítések nem érvényesek.

## <a name="partner-center-for-microsoft-cloud-germany"></a>A Microsoft Cloud Germany Partnerközpontja

> [!IMPORTANT]
> Az ügyfelek igényeinek fejlődése alapján a németországi felhőstratégia a globális felhőajánlatnak megfelelő új felhőrégiók németországi megvalósításához fog összpontosítani. Ezt szem előtt tartva nem fogadunk új ügyfeleket, és nem helyezünk üzembe semmilyen új szolgáltatást a jelenleg elérhető Microsoft Cloud Germany felhőből. A meglévő ügyfelek továbbra is használhatják a jelenleg elérhető felhőszolgáltatásokat, amelyeket fenntartunk a szükséges biztonsági frissítések biztosításával.
>
> A régióban az új ügyfelek a jelenleg elérhető európai régiókat vagy a németországi új régiókat is használhatja, amikor elérhetővé válnak. További információ: [A Microsoft új adatközpontokból nyújt felhőszolgáltatásokat Németországban](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/).

A Microsoft *Cloud Germany* Partnerközpont *és* Partnerközpont közötti partneri különbségek a következőek:

- A partnerek nem hozhatnak létre felhasználókat az ügyfél szervezetéhez, és nem rendelhetnek hozzá szerepköröket.
  - A partnerek olvashatják a mezőket, de nem írhatják és nem frissítik azokat.
  - A partnereknek manuálisan kell létrehozniuk vagy frissíteniük az ügyfeleik felhasználóit Office 365 felügyeleti központban vagy a Azure Portal. Lásd [Azure Active Directory dokumentációt.](/azure/active-directory/)

- Az ügyfélfelhasználók licencét nem kezelheti a Microsoft Cloud Germany portálra Partnerközpont API-k használatával. Ehelyett a felügyeleti központot vagy Office 365 Azure Active Directly Group licenckezelést kell használnia (hamarosan elérhető) a licencek kezeléséhez.
  - (Nem kötelező) használhatja az Azure AD Graph API-t. Lásd: [Licencek hozzárendelése felhasználóhoz.](/graph/api/user-assignlicense) A Partnerközpont Microsoft Cloud Germany esetében mindenképpen a Graph végpontot használja `https://graph.cloudapi.de` a `https://graph.windows.net` helyett.

- Az ügyfélfelhasználók és a teljes partnerfelhasználók jelszavát nem állíthatja vissza programozott módon. Használja a Office 365 felügyeleti központot vagy Azure Portal. Lásd: [Új jelszó kérése egy felhasználóhoz a Azure Active Directory.](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal) Az 1. lépéshez be kell jelentkeznie a Microsoft Cloud Germany Azure Portal szolgáltatásba.

- A fejlesztőknek manuálisan kell regisztrálniuk az alkalmazásazonosítójukat, hogy Partnerközpont API-/SDK-funkciókat integrálni Partnerközpont Microsoft Cloud Germany számára készült alkalmazásukba. További információ: [Register app details for Partnerközpont for Microsoft National Cloud](create-apps-for-partner-center-for-microsoft-national-clouds.md)..

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>A Microsoft Cloud for US Government Partnerközpontja

A partnerek közötti különbségek a *Partnerközpont* és Partnerközpont *között a Microsoft Cloud for US Government:*

- Office 365 előfizetések jelenleg nem érhetők el Partnerközpont előfizetések Microsoft Cloud for US Government.

- A meglévő partnereknek Microsoft Cloud for US Government új fiókokat kell létrehozniuk a Partnerközpont a Microsoft Cloud for US Government.

- Microsoft Cloud for US Government az ügyfeleknek egyetlen partnerrel kell tranzakciót tranzakciót
  - A többcsatornás és többpartneres és kérelemkapcsolatok a meglévő ügyféllel Microsoft Cloud for US Government forgatókönyvek nem érvényesek. Ez a korlátozás azért van Office 365 jelenleg nem érhető el.

- A partnerek nem hozhatnak létre felhasználókat az ügyfél szervezetéhez, és nem rendelhetnek hozzá szerepköröket.
  - A partnerek olvashatják a mezőket, de nem írhatják és nem frissítik azokat. A partnereknek manuálisan kell létrehozniuk vagy frissíteniük az ügyfeleik felhasználóit a Azure Portal. Lásd [Azure Active Directory dokumentációt.](/azure/active-directory/)

- Az ügyfélfelhasználók és a teljes partnerfelhasználók jelszavát nem állíthatja vissza programozott módon. Használja az Azure Portalt. Lásd: [Új jelszó kérése egy felhasználóhoz a Azure Active Directory.](/azure/active-directory/active-directory-users-reset-password-azure-portal) Az 1. lépésben be kell jelentkeznie a Azure Portal a Microsoft Cloud for US Government.

- A Partnerközpont rest Microsoft Cloud for US Government végpontjai ugyanazok, mint a Partnerközpont: `https://api.partnercenter.microsoft.com` .

- A fejlesztőknek manuálisan kell regisztrálniuk az alkalmazásazonosítójukat, hogy Partnerközpont API-/SDK-funkciókat integrálják az Partnerközpont for Microsoft Cloud for US Government. További információ: [Register app details for Partnerközpont for Microsoft National Cloud](create-apps-for-partner-center-for-microsoft-national-clouds.md)..
