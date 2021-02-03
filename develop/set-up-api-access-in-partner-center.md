---
title: API hozzáférésének beállítása a Partnerközpontban
description: Fiókok beállítása a partner Center SDK-hoz való fejlesztéshez és teszteléshez az integrációs munkaterületen.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 873ff2ff9cecbfa92429958d3bfe2aa79fc3ad9a
ms.sourcegitcommit: d5de47c08ba661ba5de4935caa6843d7c2c91710
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/28/2020
ms.locfileid: "97768152"
---
# <a name="set-up-api-access-in-partner-center"></a>API hozzáférésének beállítása a Partnerközpontban

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud for US Government Partnerközpontja
- A Microsoft Cloud Germany Partnerközpontja

Ez a cikk azokat a fiókokat ismerteti, amelyeket a partneri központ SDK-val kell fejleszteni. Ez a cikk azt is ismerteti, hogyan lehet [integrációs homokozó-fiókot](#integration-sandbox-account) létrehozni és tesztelni az integrációs homokozóban.

>[!NOTE]
>Az API-k eléréséhez a bérlőnek CSP-Bérlőnek kell lennie, és rendelkeznie kell közvetett szolgáltatóval vagy közvetlen számlázási partnerrel.

## <a name="account-definitions"></a>Fiókok definíciói

Az API-integráció integrálásához és teszteléséhez a partner Center két típusú fiókot támogat:

### <a name="primary-partner-account"></a>Elsődleges partner fiók

Ezzel a fiókkal valódi rendeléseket hozhat létre valódi ügyfelek számára. Ha módosításokat vagy tranzakciókat végez, amikor bejelentkezik az elsődleges fiókba, a partner Center SDK-val vagy a partner irányítópult felhasználói felületével, a rendszer a valódi ügyfelek számára hivatalos megrendelésként kezeli őket. Ezek a számlán jelennek meg, és a vállalat felelős azért, hogy fizessen értük.

### <a name="integration-sandbox-account"></a>Integrációs tesztkörnyezeti fiók

Ez a fiók a kód és a partner Center API-k integrálásának tesztelésére szolgál, mielőtt széleskörűen telepítené. Az integrációs csomagba való bejelentkezéskor elvégzett módosítások és tranzakciók megjelennek a számlán, azonban nem kell megfizetnie a számla összegét. A számla PDF-fájlja a "fizetés nélkül" nyilatkozatot kapja. EZ EGY SANDBOX-SZÁMLA, ÉS NINCS SZÜKSÉG BEAVATKOZÁSRA. "

Az integrációs csomag fiókja és az elsődleges fiók egymástól függetlenül működik, és nem oszt meg rendszergazdai fiókokat, felhasználói fiókokat, ügyfeleket, rendeléseket, előfizetéseket és egyéb adatait.

Az integrációs munkaterületen korlátozott számú ügyféllel, rendeléssel, előfizetéssel és licenccel rendelkező tranzakciók támogatottak.

Házirend szerint az integrációs munkaterületek csak integrációs tesztelési célokat szolgálnak.

Alapértelmezés szerint nincs integrációs tesztkörnyezeti fiók. Létre kell hoznia egyet, ha azt tervezi, hogy a partner Center SDK-t használja.

## <a name="set-up-your-accounts"></a>Fiókok beállítása

Ez a szakasz azt ismerteti, hogyan állíthat be egy elsődleges partneri fiókot és egy integrációs sandbox-fiókot a partner Center SDK-hoz.

### <a name="create-an-integration-sandbox"></a>Integrációs homokozó létrehozása

1. Jelentkezzen be a partner-irányítópultra egy globális rendszergazdai fiókkal (az elsődleges partner fiókjával).

2. A **Beállítások** menüben (fogaskerék ikon) válassza a **partneri beállítások** lehetőséget.

3. Válassza az **integrációs** munkaterületek fület.

    >[!NOTE]
    >Ha nem lát integrációs munkaterületet, előfordulhat, hogy nem rendelkezik globális rendszergazdai fiókkal. Az is előfordulhat, hogy egy integrációs homokozó-fiókot használ, és már be van állítva egy integrációs homokozó.

4. Adja meg az integrációs munkaterülethez tartozó rendszergazdai fiók kapcsolattartási adatait. Ezután válassza a **fiók létrehozása** lehetőséget. Várjon néhány percet, amíg egy megerősítő üzenetben létrejött a fiók.

5. Miután megtalálta a megerősítő üzenetet, jelentkezzen ki a partner irányítópulton.

6. Jelentkezzen be újra az új integrációs homokozó rendszergazdai fiókjával. Ügyeljen arra, hogy a **username@domain** hitelesítő adatok formátumát az imént megadott jelszóval együtt használja.

7. Válassza a **fiók beállítása** a **jelenlegi feladatok** felett lehetőséget a sandbox-fiók beállításának befejezéséhez.

### <a name="enable-api-access"></a>API-hozzáférés engedélyezése

A fiók beállítása után engedélyeznie kell az API-hozzáférést, mielőtt használhatná a Partnerközpont SDK-t az integrációs tesztkörnyezettel. Az API-hoz való hozzáférést külön kell engedélyeznie az elsődleges partnerfiók és az integrációs tesztkörnyezeti fiók esetében is.

1. Jelentkezzen be a partner irányítópultra egy globális rendszergazdai fiók használatával.

2. A **Beállítások** menüben (fogaskerék ikon) válassza a **partneri beállítások** lehetőséget.

3. A **Fiókbeállítások** lapon válassza az alkalmazás- **kezelés** lehetőséget.

4. Ha még nem rendelkezik meglévő alkalmazással, vegyen fel egy új webalkalmazást. Ha van meglévő webalkalmazása, kattintson a **Kulcs hozzáadása** gombra.

5. Másolja az alkalmazás regisztrációs adatait, különösen a **kulcsot** , ha webalkalmazást hoz létre, és tárolja biztonságos helyen.

6. Jelentkezzen ki a partner irányítópultján.

7. Jelentkezzen be a szolgáltatásba az integrációs sandbox-fiókjával. Ismételje meg az 2-5-es lépéseket az API-hozzáférés engedélyezéséhez az integrációs homokozóban.

## <a name="write-and-test-code"></a>Kód írása és tesztelése

Kódot és tesztelési kódot írhat az integrációs homokozóban. A következő információkra lesz szüksége a [partneri központ hitelesítésének beállításához](partner-center-authentication.md) az Azure ad-ben.

| Elemnév | Pont helye |
| --------- | ------------- |
| Alkalmazás azonosítója/ügyfél-azonosítója | A **Beállítások** menüben (fogaskerék ikon) válassza a **partneri beállítások** lehetőséget. A **Fiókbeállítások** lapon válassza az alkalmazás- **kezelés** lehetőséget. Az alkalmazás azonosítója/ügyfél-azonosítója a **regisztrált Application app-azonosítóként** szerepel. |
| Kulcs | Ha létrehozott egy webalkalmazást az API- [hozzáférés engedélyezése](#enable-api-access)szakaszban, akkor ez az 5. lépésben mentett kulcs. |
| Tartomány | Az integrációs homokozó tartománya. |

## <a name="run-tested-code"></a>Tesztelt kód futtatása

Ha valódi ügyféladatokat szeretne használni a megoldásban, az integrációs csomag hitelesítő adatait az elsődleges partneri fiók hitelesítő adataira kell váltania.

Ha készen áll a tesztelt kód használatára az elsődleges partner fiókjában, be kell szereznie egy Azure AD biztonsági jogkivonatot. Ez a biztonsági jogkivonat a partner Center-alkalmazáson, a kulcson és a tartományon alapul (az integrációs homokozó alkalmazás, a kulcs és a tartomány helyett).

1. Kövesse a [partneri központ hitelesítésének](partner-center-authentication.md) lépéseit az Azure ad biztonsági jogkivonat beszerzéséhez az elsődleges partneri központ hitelesítő adataival. (Korábban ezeket a lépéseket követve beszerezhet egy Azure AD biztonsági jogkivonatot az integrációs munkaterülethez.)

2. Cserélje le az integrációs biztonsági tokent a kódban az elsődleges partner fiókjához tartozó új biztonsági jogkivonatra.
