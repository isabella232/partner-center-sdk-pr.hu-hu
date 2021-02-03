---
title: CSP-ügyfél – áruházkészítő – első lépések
description: Hozzon létre egy online piactért a Cloud Solution Provider (CSP) ajánlatok értékesítéséhez a CSP Customer kirakat-készítő használatával.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d64deff9b002b861c9f48d076feb5841af727e3d
ms.sourcegitcommit: 57620e249e218edc4af7c83c2ce8a3008a4adf4e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/04/2020
ms.locfileid: "97768012"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>CSP-ügyfél – áruházkészítő – első lépések

**A következőkre vonatkozik:**

- Partnerközpont

Hozzon létre egy online piactért a Cloud Solution Provider (CSP) ajánlatok értékesítéséhez a CSP Customer kirakat-készítő használatával.

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>A CSP Customer kirakat-készítő bemutatása

A CSP Customer Builder-szerkesztő segítségével a partnereink könnyedén létrehozhatnak egy online piactért a CSP-ajánlatok ügyfeleknek való értékesítéséhez. A legtöbb partner és kisméretű értékesítő szervezet nem az online piactér fejlesztése helyett az értékesítésre koncentrálhat. A partner Center SDK-beli alkalmazásnak a webhelyek létrehozásához és üzembe helyezéséhez szoftverfejlesztői ismeretekre van szüksége. A CSP Customer kirakat-készítő használatával gyorsan és egyszerűen létrehozhatja saját webhelyét. A webhelyet mintakódként is letöltheti, vagy közvetlenül is üzembe helyezheti az Azure-előfizetését, és készen áll a Transact webhelyre.

Ez a webhely a partnerek teljes tulajdonú, támogatott és karbantartott, és a Microsoft nem gyűjt adatokat és telemetria a webhelyről. A CSP Customer kirakat-készítő létrehoz egy webhelyet a partnernek, amely teljes mértékben megfelel a [Payment Card Industry adatbiztonsági szabványának](https://www.pcisecuritystandards.org/) (PCI DSS).

A CSP Customer kirakat-készítő kódja a [partner Center SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK)-ban elérhető licenc hatálya alá esik.

>[!NOTE]
>Ön felelős a kirakati webhelyek kezelésével, karbantartásával és a webhelyek létrehozásával kapcsolatos esetleges problémákkal. Olvassa el és Ismerje meg a [partner Center SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK)-ban szereplő feltételeket.

További információkat a következő cikkekben talál: [CSP Customer web kirakat](csp-customer-web-storefront.md) és [Console test app](console-test-app.md).

## <a name="considerations"></a>Megfontolandó szempontok

A CSP Customer kirakat-készítő célja a webhelyek létrehozásának gyors módja. A tervezés során a következő szempontokat kell figyelembe vennie:

- Az üzembe helyezést követően a Microsoft és a partner Center nem őrzi meg a partner webhelyének másolatát, illetve a CSP Customer kirakat-szerkesztőben hozzáadott adatokat.

- A partner Center csak a CSP Customer kirakatok webhelyét helyezheti üzembe egy partner Azure-előfizetésében.

- A webhely üzembe helyezése után a partner teljes mértékben tulajdonosa és felügyeli. A Microsoft nem fér hozzá ehhez a webhelyhez vagy a webhelyhez kapcsolódó bármilyen adathoz. A partnerek felelősek a webhely karbantartásával és felügyeletével kapcsolatban. A Microsoft nem biztosít élő webhelyeket vagy más, a CSP Customer kirakat-készítővel vagy a CSP-vel létrehozott webhelyekkel kapcsolatos egyéb támogatást.

- A partner Center nem tud közvetlenül hozzáférni vagy frissíteni a webhelyet új vagy módosított SDK-vagy API-funkciókkal. Minden új funkciónak vagy fejlesztésnek a partnereknek kell lennie, fejlesztenie és kezelnie kell, beleértve az új partner Center SDK vagy API-funkciók hozzáadását.

- A CSP Customer kirakat-készítő jelenleg lehetőséget biztosít a PayPal Pro/PayU Money (India) fiókhoz való fizetés konfigurálására. Ha a partnereknek módosítaniuk kell a fizetési processzort, módosítaniuk kell a kódot, hogy támogassák az előnyben részesített fizetési módot.

- A CSP Customer kirakatban hozzáadott fizetéssel kapcsolatos információk nem tárolódnak és nem maradnak meg a partner Centerben.

- A PayPal-fizetési konfiguráció minden olyan földrajzi helyen működni fog, ahol a PayPal elérhető. A PayPal rendelkezésre állását és támogatását kizárólag a PayPal vezérli, és a PayPal bármikor megszüntethető.

- A PayU-fizetési konfiguráció csak Indiában működik. A PayU rendelkezésre állását és támogatását kizárólag a PayU vezérli, és a PayU bármikor megszüntethető.

- Olvassa el és Ismerje meg a [partner Center SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK)-ban szereplő feltételeket.

## <a name="using-the-csp-customer-storefront-builder"></a>A CSP Customer kirakat-készítő használata

A partner Centerben lévő CSP-partneri rendszergazdák közvetlenül a partnervállalat központból telepíthetik a CSP-ügyfelet. Minimális erőfeszítéssel új webhely helyezhető üzembe a partner bérlője számára. A üzembe helyezést követően a partnerek a webhely használatával konfigurálhatják a branding, az ajánlatokat és a fizetéssel kapcsolatos információkat, majd megoszthatják a webhely URL-címét az ügyfelekkel.

A kirakati webhely létrehozási folyamata a következő:

1. [A webhely üzembe helyezése](#deploy)

2. [A kirakat konfigurálása](#configure)

3. [A kirakaton lévő Transact](#transact)

### <a name="deploy"></a>Üzembe helyezés

Központi telepítési beállítások:

- A [partner Center kirakat mintakód](https://github.com/Microsoft/Partner-Center-Storefront) letöltése a githubról
- Integráció az Azure-nal a konfigurált webhely üzembe helyezéséhez
- Üzembe helyezés meglévő előfizetésen vagy saját előfizetés használata

### <a name="configure"></a>Konfigurálás

A kirakat testreszabásához nem szükségesek fejlesztési ismeretek.

A konfiguráláshoz jelentkezzen be a partner Center rendszergazdai hitelesítő adataival:

- **Branding**: cég neve, embléma, névjegyek és egyebek.

- **Ajánlatok**: az összes CSP-ajánlat megtekintése. Kiválaszthatja, hogy az ügyfelek mely ajánlatokat tekinthetik meg és vásárolhatják meg. Emellett személyre szabhatja az ajánlat adatait, és hozzáadhatja az árát.

- **PayPal-fizetési konfiguráció**: adja meg a PayPal fizetési fiókjának adatait. Ha nem rendelkezik PayPal-fiókkal, látogasson el [https://www.paypal.com](https://www.paypal.com) és hozzon létre egy új fiókot. A rendszer ezt a fiókot használja a PayPal számára az ügyfelek által teljesített kifizetések jóváírására. *A Microsoft nem felelős a partnerek és a PayPal közötti kapcsolatért. A PayPal használata a partner vagy a partner ügyfeleinek is megkövetelheti a további feltételek elfogadását.*

- (*India esetében*) **PayU-fizetési konfiguráció**: adja meg a PayU pénz fizetési fiókjának adatait. Ha nem rendelkezik PayU-fiókkal, látogasson el [https://www.payumoney.com/](https://www.payumoney.com/) és hozzon létre egy új fiókot. A rendszer ezt a fiókot használja a PayU az ügyfelek által teljesített kifizetések jóváírására. *A Microsoft nem felelős a partnerek és a PayU közötti kapcsolatért. A PayU használata a partner vagy a partner ügyfeleinek is megkövetelheti a további feltételek elfogadását.*

### <a name="transact"></a>Tranzakciós

- Az üzembe helyezést követően az ügyfelek azonnal vásárolhatnak és tranzakciókat.

- Az ügyfelek közvetlenül a partner Center SDK-val integrált partner portálról vásárolhatnak.

#### <a name="customer-countries"></a>Vásárlói országok

Az ügyfelek a következő országokhoz tartozhatnak:

| Országkód | Ország neve   |
|--------------|----------------|
| AU           | Ausztrália      |
| AT           | Ausztria        |
| BE           | Belgium        |
| BG           | Bulgária       |
| CA           | Kanada         |
| HR           | Horvátország        |
| CY           | Ciprus         |
| CZ           | Cseh Köztársaság |
| DK           | Dánia        |
| EE           | Észtország        |
| FI           | Finnország        |
| JK           | Franciaország         |
| DE           | Németország        |
| GR           | Görögország         |
| HU           | Magyarország        |
| IS           | Izland        |
| IN           | India          |
| IE           | Írország        |
| IT           | Olaszország          |
| JP           | Japán          |
| LV           | Lettország         |
| LI           | Liechtenstein  |
| LT           | Litvánia      |
| LU           | Luxemburg     |
| MT           | Málta          |
| MC           | Monaco         |
| NL           | Hollandia    |
| NZ           | Új-Zéland    |
| NO           | Norvégia         |
| ENER           | Lengyelország         |
| PT           | Portugália       |
| RO           | Románia        |
| SK           | Szlovákia       |
| SL           | Szlovénia       |
| ES           | Spanyolország          |
| SE           | Svédország         |
| CH           | Svájc    |
| GB           | Egyesült Királyság |
| USA           | Egyesült Államok  |

## <a name="partner-experience-scenarios"></a>A partneri élmény forgatókönyvei

### <a name="deployment-scenario"></a>Központi telepítési forgatókönyv

Bővített vagy testreszabott CSP ügyfél-kirakat üzembe helyezése:

- Töltse le a [partneri központ kirakati mintáját](https://github.com/Microsoft/Partner-Center-Storefront) , hogy további testreszabásokat hajtson végre.

- A fejlesztéshez használja a Microsoft Visual Studio 2015 (vagy újabb) verzióját.

- További változásokat és fejlesztéseket (beleértve az engedélyeket, a tanúsítványokat, a jegyzék változásait és az egyéb elemeket) is kiépítheti.

### <a name="configuration-scenario"></a>Konfigurációs forgatókönyv

- Az újonnan létrehozott webhely társítva van egy partner bérlőhöz, és hozzáfér a partner bérlő összes rendszergazdai fiókjához.

  - A partnerek a partner Center rendszergazdai hitelesítő adataikkal jelentkezhetnek be erre az új webhelyre.

- A kirakati alkalmazás jelenleg a francia, a spanyol, a holland, a német, a japán és az angol nyelveket támogatja. (Az angol a tartalék nyelvként szolgál.)

  - A kirakat konfigurálja a területi beállításokat a partner alapértelmezett területi beállításaként a partner központjában található partner profiljában. Ez a területi beállítás a pénznemek, a dátumformátum és a honosított ajánlatok konfigurálására szolgál a tárházban.

- A partnerek a branding, az ajánlatokat és a PayPal-vagy PayU (India) fizetési adatokat is konfigurálhatják.

- A partnerek frissíthetik a cég nevét, a céges emblémát, a fejléc képét, az értékesítési és támogatási partnereket, és így tovább.

- A partnerek az összes, a saját területük alapján elérhető CSP-ajánlatot megtekinthetik.

  - A partnerek kiválaszthatják, hogy mely ajánlatokat szeretnék megjeleníteni az összes ügyfelünk számára.

  - A CSP-partnerek kijelölhetnek egy vagy több ajánlatot, és frissíthetik a nevet, a mennyiséget, a szolgáltatás leírását és az árat.
  - Az ár az éves díj. Ügyfeleinknek évente kell fizetniük.

- A partnerek bármikor konfigurálhatják az előre jóváhagyott tranzakciókat a (a) összes jelenlegi és jövőbeli ügyfelének, vagy (b) adott ügyfélnek.

  - Az előzetesen jóváhagyott ügyfeleknek nem kell fizetniük a portálon, amikor új előfizetéseket vesznek fel, további licenceket vásárolnak a meglévő előfizetésekhez, vagy megújítanak egy előfizetést.

  - Az előzetesen jóváhagyott ügyfelek nem lesznek átirányítva a PayPal szolgáltatásba vagy a PayU (India esetében) a tranzakciók során történő fizetésre.

  - Az előzetesen jóváhagyott ügyfél-tranzakciók lehetővé teszik, hogy a partnerek offline számlázást és számlázást végezzenek az előre jóváhagyott ügyfelek számára.

- A CSP-partnerek megadhatják a PayPal-fiókjuk adatait, például a PayPal-ügyfél AZONOSÍTÓját és a titkos kulcsot. A CSP-partner azt is kiválaszthatja, hogy egy sandbox vagy egy élő fiók használatával szeretne-e tesztelni.

  - A partnerek megtalálhatják ezeket az információkat a [https://developer.paypal.com/](https://developer.paypal.com/) **saját alkalmazások & hitelesítő adataival**. Ezt az információt egy aktuális alkalmazásból is beszerezheti, vagy létrehozhat egy új alkalmazást a PayPalben.
  - Ha még nem rendelkezik ilyennel, hozzon létre egy új PayPal-fiókot. A rendszer ezt a fiókot használja a PayPal számára az ügyfelek által teljesített kifizetések jóváírására.

    - A PayPal üzleti fiók megnyitásával kapcsolatban lásd: [https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register](https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register) .

    - A PayPal-beli homokozó-fiók létrehozásához lásd: [https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/](https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/) .

- (India esetében) a CSP-partner beviheti a PayU-fiók adatait, például a PayU ügyfél-azonosítót és a jelszót. A partnerek további információkat is találhatnak a szolgáltatással kapcsolatban [https://developer.payumoney.com/](https://developer.payumoney.com/) .

  - Ha még nem rendelkezik ilyennel, hozzon létre egy új PayU pénz-fiókot. PayU-fiók megnyitásához látogasson el a következő oldalra: [https://www.payumoney.com/merchant-account/#/](https://www.payumoney.com/merchant-account/#/) . A rendszer ezt a fiókot használja a PayU az ügyfelek által teljesített kifizetések jóváírására.

## <a name="customer-experience-scenarios"></a>Felhasználói élmény forgatókönyvei

### <a name="new-customer-sign-up-scenario"></a>Új ügyfél-regisztrálási forgatókönyv

- Alapértelmezés szerint a webhely nyilvánosan elérhető, és megjeleníti a partner katalógusát a kezdőlapon.

- Az ügyfelek mostantól nagy számú [ügyfélhez](#customer-countries)tartozhatnak.

- A hangsúly az Európai Szabadkereskedelmi Társulás (EFTA) országai, Észak-Amerika, Japán, India, Ausztrália és Új-Zéland régiójában volt.
  - Ez a szolgáltatás a partner Center SDK-ban a regionális engedélyezési támogatást használja.

- Az ügyfelek választhatnak egy ajánlatot a katalógusból a vásárláshoz.
  - Hozzáadhatják az ügyfél nevét, a lakcímét és a tartományhoz kapcsolódó információkat.

- Az ügyfeleket a PayPal-vagy PayU (India) pénztári felhasználói felületre irányítjuk. Az ügyfelek a következőkkel biztosíthatják a fizetést:
  - Meglévő PayPal-vagy PayU-fiókja (India)
  - Az országukban a PayPal vagy a PayU (India) által támogatott finanszírozási eszközök. Ezek közé tartozhatnak a hitelkártyák, a bankkártyák és a bankszámlák is.

- A rendszer létrehoz egy ügyfél-bérlőt ehhez az ügyfélhez. A bérlői megrendelés sikeres létrehozása után az ügyfeleknek meg kell adni a fiók felhasználónevét, jelszavát és az előfizetés részleteit.
  - Az ügyfelek megmenthetik a felhasználónevet és a jelszót, hogy továbbra is bejelentkezve maradjanak a további vásárlások.
  - Minden előfizetés egy évig vásárolható meg, az ügyfelek pedig az előfizetés befejezési dátumát megelőző 30 napon belül megújíthatók.

### <a name="view-prior-purchases-scenario"></a>Korábbi vásárlási forgatókönyv megtekintése

- Az ügyfél bejelentkezik az ügyfél bérlői felhasználónevével és jelszavával, és a **saját megrendelések** szakaszra kerül.

- Az ügyfelek megtekinthetik a **saját megrendelések** lapot, ahol megtekinthetik a megvásárolt előfizetéseket, és igény szerint frissíthetik a frissítéseket.

- Az ügyfelek a **saját előfizetések** oldalra is felkereshetik, ahol megtekinthetik az összes előfizetést (a licenc-alapú és a használaton alapuló), beleértve a partner Centerben karbantartott felhasználókat is.

### <a name="add-licenses-to-existing-subscriptions-scenario"></a>Licencek hozzáadása meglévő előfizetésekhez forgatókönyv

- A Custom **orders (megrendelések** ) szakaszban az ügyfelek további licenceket adhatnak hozzá a meglévő előfizetésekhez. Az ügyfelek bármikor hozzáadhatnak további licenceket az előfizetési év során.

- Az egyes hozzáadott licencek nem változtatják meg az előfizetés befejezési dátumát. Az előfizetés díja azonban attól függően változik, hogy mikor adja hozzá a licencet, és ha ez a dátum az évben van. A díjszabást napi rendszerességgel számoljuk el, hogy csak az év hátralévő napjaiért számítson fel díjat.

### <a name="add-more-subscriptions-scenario"></a>További előfizetési forgatókönyv hozzáadása

- Az ügyfelek tetszőleges számú előfizetést vásárolhatnak az **előfizetések hozzáadása** szakaszban, a **saját megrendelések** menüpontban.

- Az ügyfél kiválaszthat egy előfizetést, hozzáadhat egy mennyiséget, és kifizetheti a tranzakció befejezését, és azonnal megkezdheti az előfizetés használatát. Ha az ügyfél előzetesen jóváhagyott ügyfél, az előfizetés azonnal használatba vehető, és a rendszer elküld egy számlát az ügyfélnek fizetésre.

### <a name="renew-subscription-scenario"></a>Előfizetési forgatókönyv megújítása

- Egy ügyfél megújíthat egy előfizetést az utolsó 30 napban az előfizetés befejezési dátuma előtt.

- Ez csak az elmúlt 30 napban érhető el.

- Ha az utolsó 30 napban nem újítják meg az előfizetést, az előfizetés el lesz távolítva az ügyfél-bérlőhöz tartozó előfizetések listájából.

- A mennyiség nem frissíthető a megújítás során.

### <a name="payments-scenario"></a>Fizetési forgatókönyv

- Ha az ügyfelet előzetesen jóváhagyják a rendszergazda által végzett tranzakciókra, a fenti forgatókönyvek esetében nem jelenik meg a fizetési élmény. Ehelyett a partner az előzetesen jóváhagyott ügyfélnek küldheti el a fizetési számlát.

- Minden új vásárláshoz hozzáadhat további licenceket, előfizetéseket adhat hozzá, és megújíthatja azokat. Az ügyfél a webhely használatával fizethet a PayPal vagy a PayU (India) segítségével.

- Ez a webhely integrálva van a PayPal vagy a PayU (India esetében), és lehetővé teszi, hogy a partnerek elfogadják az ügyfelektől érkező kifizetéseket. A PayPal vagy a PayU (India) ezen összeget a partner számlájára jóváírja. PayPal-vagy PayU (India) a bankszámla-felügyelet ezen a webhelyen kívül van, és a PayPal.com vagy PayUmoney.com felügyeli.

- Ez attól függ, hogy a partnerek a PayPal-orPayU (India) a PayPal.com vagy a PayUmoney.com-ben konfigurált fizetési konfigurációt konfigurálják. A Microsoft nem menti ezeket az információkat vagy a tényleges fizetési tranzakciókat a beállítás használatából eredően.

### <a name="prorated-pricing-scenario"></a>Arányos árképzési forgatókönyv

- Ez a webhely olyan esetekben támogatja az arányos díjszabást, amikor az ügyfelek további licenceket vesznek fel egy meglévő előfizetésbe.

- Minden előfizetés egy év után lejár, és az előfizetés megvásárlása után nem módosítható.

- Az előfizetés záró dátuma nem változik további licencek hozzáadásával. A lejárati dátumig a hátralévő napok száma után kell fizetni. Ha például az első napon az előfizetés költsége $365, és egy további licencet ad hozzá a második napon, akkor az új licenc díja $364 lesz. Ha újabb 10 nappal később ad hozzá egy licencet, a díj $354 lesz.
