---
title: API hozzáférésének beállítása a Partnerközpontban
description: Állítson be fiókokat a fejlesztéshez a Partnerközpont SDK és tesztelje az integrációs tesztkészletet.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2c564baa9b626ff6ce21f9bcc517902d7cf99244
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547427"
---
# <a name="set-up-api-access-in-partner-center"></a>API hozzáférésének beállítása a Partnerközpontban

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont a Microsoft Cloud for US Government | Partnerközpont Microsoft Cloud Németországhoz

Ez a cikk a fejlesztéshez szükséges fiókokat ismerteti Partnerközpont SDK. Ez a cikk azt is bemutatja, hogyan hozhat létre [integrációs tesztfiókot és](#integration-sandbox-account) tesztelni az integrációs tesztboxban.

>[!NOTE]
>Az API-khoz való hozzáféréshez a bérlőnek CSP-bérlőnek kell lennie, önnek pedig közvetett szolgáltatónak vagy közvetlen számlázási partnernek kell lennie.

## <a name="account-definitions"></a>Fiókdefiníciók

Az API-integráció integrálása és tesztelése érdekében a Partnerközpont kétféle fiókot támogat:

### <a name="primary-partner-account"></a>Elsődleges partnerfiók

Ebben a fiókban hozhat létre valós rendeléseket valós ügyfelek számára. Ha módosításokat vagy tranzakciókat kell végeznie, amikor bejelentkezik az elsődleges fiókba, az Partnerközpont SDK vagy a Partner irányítópult felhasználói felületének használatával azok valós ügyfelek hivatalos rendeléseként lesznek kezelve. Ezek megjelennek a számlán, és a vállalat felelős a fizetésért.

### <a name="integration-sandbox-account"></a>Integrációs tesztkörnyezeti fiók

Ez a fiók a kód tesztelésére és a Partnerközpont API-okkal való integrációjára való, mielőtt széles körben üzembe helyezi. Az integrációs sandbox-fiókba való bejelentkezve végrehajtott módosítások és tranzakciók megjelennek a számlán, azonban nem kell kifizetnie a számla összegét. A pdf formátumú számlához a "DO NOT PAY" (NEM FIZET). EZ EGY SANDBOX-SZÁMLA, ÉS NINCS SZÜKSÉG BEAVATKOZÁSRA."

Az integrációs sandbox-fiók és az elsődleges fiók egymástól függetlenül működik, és nem oszt meg rendszergazdai fiókokat, felhasználói fiókokat, ügyfeleket, rendeléseket, előfizetéseket és más adatokat.

Az integrációs védőfal csak korlátozott számú ügyfél, megrendelés, előfizetés, licenc stb. esetén támogatja a tranzakciókat.

Szabályzat szerint az integrációs tesztfiókok csak integrációs tesztelési célokra szolgálnak.

Alapértelmezés szerint nincs integrációs tesztkörnyezeti fiók. Ha az alkalmazás használatát tervezi, saját magának kell létrehoznia Partnerközpont SDK.

## <a name="set-up-your-accounts"></a>A fiókok beállítása

Ez a szakasz azt ismerteti, hogyan állíthat be elsődleges partnerfiókot és integrációs védőfalat a Partnerközpont SDK.

### <a name="create-an-integration-sandbox"></a>Integrációs védőfal létrehozása

1. Jelentkezzen be a Partner irányítópultra egy globális rendszergazdai fiókkal (az elsődleges partnerfiókkal).

2. A **Gépház** (fogaskerék ikon) válassza a **Partnerbeállítások lehetőséget.**

3. Válassza **az Integrációs védőfal** lapot.

    >[!NOTE]
    >Ha nem látja az Integrációs védőfal lehetőséget, előfordulhat, hogy nincs globális rendszergazdai fiókja. Előfordulhat, hogy integrációs sandbox-fiókot használ, és már be van állítva egy integrációs védőfal.

4. Adja meg az integrációs védőfal rendszergazdai fiókjának kapcsolattartási adatait. Ezután válassza a **Fiók létrehozása lehetőséget.** Várjon néhány percet, amíg megerősítő üzenet jelenik meg a fiók létrejöttével.

5. Miután megjelenik a megerősítést kérő üzenet, jelentkezzen ki a Partner irányítópultjáról.

6. Jelentkezzen be újra az új integrációs sandbox rendszergazdai fiókjával. Győződjön meg arról, hogy a hitelesítő adatok formátumát és a **username@domain** megadott jelszót használja.

7. Válassza **a Fiók beállítása az** Aktuális feladatok fölött **lehetőséget** a sandbox-fiók beállításának befejezéséhez.

### <a name="enable-api-access"></a>API-hozzáférés engedélyezése

A fiók beállítása után engedélyeznie kell az API-hozzáférést, mielőtt használhatná a Partnerközpont SDK-t az integrációs tesztkörnyezettel. Az API-hoz való hozzáférést külön kell engedélyeznie az elsődleges partnerfiók és az integrációs tesztkörnyezeti fiók esetében is.

1. Jelentkezzen be a Partner irányítópultra egy globális rendszergazdai fiókkal.

2. A **Gépház** (fogaskerék ikon) válassza a **Partnerbeállítások lehetőséget.**

3. A **Fiókbeállítások lapon** válassza az **Alkalmazáskezelés lehetőséget.**

4. Ha még nem rendelkezik meglévő alkalmazással, adjon hozzá egy új webalkalmazást. Ha már van webalkalmazása, válassza a Kulcs **hozzáadása** gombot.

5. Másolja ki az alkalmazásregisztrációs adatokat, különösen a kulcsot, ha webalkalmazást hoz létre, és tárolja biztonságos helyen. 

6. Jelentkezzen ki a Partner irányítópultjáról.

7. Jelentkezzen be újra az integrációs sandbox-fiókjával. Ismételje meg a 2–5. lépést az API-hozzáférés az integrációs védőfalon való engedélyezéséhez.

## <a name="write-and-test-code"></a>Kód írása és tesztelése

Az integrációs tesztkészletben kódot írhat és tesztelhet. A következő információkra lesz szüksége az Azure [AD-Partnerközpont beállításhoz.](partner-center-authentication.md)

| Elem neve | Elem helye |
| --------- | ------------- |
| Alkalmazásazonosító /ügyfél-azonosító | A **Gépház** (fogaskerék ikon) válassza a **Partnerbeállítások lehetőséget.** A **Fiókbeállítások lapon** válassza az **Alkalmazáskezelés lehetőséget.** Az alkalmazásazonosító/ügyfél-azonosító regisztrált **alkalmazásalkalmazás-azonosítóként szerepel a listában.** |
| Kulcs | Ha az [API-hozzáférés](#enable-api-access)engedélyezése szakaszban létrehozott egy webalkalmazást, ezt a kulcsot mentette az 5. lépésben. |
| Tartomány | Az integrációs védőfal tartománya. |

## <a name="run-tested-code"></a>Tesztelt kód futtatása

Ahhoz, hogy a megoldást valós ügyféladatokkal használva használva az integrációs védőfal hitelesítő adatairól az elsődleges partnerfiók hitelesítő adataira váltsa.

Ha készen áll a tesztelt kód elsődleges partnerfiókban való használatára, be kell szereznie egy Azure AD biztonsági jogkivonatot. Ez a biztonsági jogkivonat a saját Partnerközpont, kulcson és tartományon alapul (az integrációs védőfali alkalmazás, a kulcs és a tartomány helyett).

1. Az Azure AD [Partnerközpont hitelesítő](partner-center-authentication.md) adatait használó Azure AD biztonsági jogkivonat le Partnerközpont lépéseit. (Korábban ezeket a lépéseket követve lekért egy Azure AD biztonsági jogkivonatot az integrációs védőfalhoz.)

2. Cserélje le a kódban az integrációs biztonsági jogkivonatot az elsődleges partnerfiók új biztonsági jogkivonatával.
