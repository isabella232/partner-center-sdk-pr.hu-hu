---
title: CSP-ügyfél – áruházkészítő – első lépések
description: Hozzon létre egy online piacteret a felhőszolgáltatói (CSP-) ajánlatok a CSP Customer Storefront Builder használatával való értékesítéshez.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8550492c7a4201a955c7b051b453103628612f3e
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973349"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>CSP-ügyfél – áruházkészítő – első lépések

Hozzon létre egy online piacteret a felhőszolgáltatói (CSP-) ajánlatok a CSP Customer Storefront Builder használatával való értékesítéshez.

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>A CSP Customer Storefront Builder bemutatása

A CSP Customer Storefront Builder segítségével a partnerek könnyedén létrehozhatnak egy online piacteret, ahol CSP-ajánlatokat értékesíthet az ügyfeleiknek. A legtöbb partner és kis értékesítési szervezet az értékesítésre szeretne összpontosítani egy online piactér fejlesztése helyett. A Partnerközpont SDK mintaalkalmazás szoftverfejlesztői készségeket igényel egy webhely létrehozásához és üzembe helyezéséhez. A CSP Customer Storefront Builder segítségével gyorsan és egyszerűen hozhat létre saját webhelyet. A webhelyet mintakódként is letöltheti, vagy közvetlenül üzembe helyezheti az Azure-előfizetésében egy Tranzakcióra kész webalkalmazással.

Ez a webhely teljes mértékben a partnerek tulajdonában áll, támogatott és karbantartott, és a Microsoft nem gyűjt adatokat vagy telemetriai adatokat a webhelyről. A CSP Customer Storefront Builder létrehoz egy webhelyet a partner számára, amely teljes mértékben megfelel a [Payment Card Industry Data Security Standard](https://www.pcisecuritystandards.org/) (PCI DSS).

A CSP Customer Storefront Builder kódja a következő licencszerződésben Partnerközpont SDK [vonatkozik.](/legal/partner-center/eula-partner-center-sdk)

>[!NOTE]
>Ön felelős az áruházi webhely kezeléséért, karbantartásáért, valamint a webhely létrehozásából eredő problémákért. Olvassa el és értse meg a jelen Partnerközpont SDK [EULA-ban.](/legal/partner-center/eula-partner-center-sdk)

További információkért tekintse meg a következő cikkeket is: [CSP-ügyfél webáruháza és](csp-customer-web-storefront.md) [konzoltesztelő alkalmazás.](console-test-app.md)

## <a name="considerations"></a>Megfontolandó szempontok

A CSP Customer Storefront Builder egy webhely gyors létrehozására szolgál. A tervezés során vegye figyelembe az alábbi szempontokat:

- Az üzembe helyezést Partnerközpont Microsoft és a microsoft nem tartja karban a partner webhelyének másolatát vagy a CSP Customer Storefront Builderhez hozzáadott adatokat.

- Partnerközpont csp ügyfél-áruház webhelyet csak egy partner Azure-előfizetésében helyezhet üzembe.

- Az üzembe helyezés után ez a webhely teljes mértékben a partner tulajdonában van, és a partner kezeli. A Microsoft nem rendelkezik hozzáféréssel ehhez a webhelyhez vagy a webhelyhez kapcsolódó adatokhoz. A partnerek felelnek a webhely karbantartásáért és kezeléséért. A Microsoft nem biztosít semmilyen élő webhelyet vagy egyéb támogatást a CSP Customer Storefront Builderrel vagy a CSP Customer Storefront Builderrel létrehozott webhelyekkel kapcsolatban.

- Partnerközpont nem tudja közvetlenül elérni vagy frissíteni ezt a webhelyet az új vagy módosított SDK- vagy API-funkciókkal. Minden új funkciót vagy fejlesztést a partnereknek kell birtokolni, fejleszteniük és kezelniük, beleértve az új funkciók Partnerközpont SDK API-funkciókat.

- Ez a CSP Customer Storefront Builder jelenleg lehetővé teszi egy PayPal Pro/payU money (for India) fiókra történő fizetés konfigurálását. Ha a partnereknek módosítaniuk kell a fizetési feldolgozót, módosítaniuk kell a kódot, hogy támogassák az előnyben részesített fizetési módot.

- A CSP Customer Storefront Builderben hozzáadott fizetéssel kapcsolatos információkat a rendszer nem tárolja és nem tartja Partnerközpont.

- PayPal fizetési konfiguráció minden olyan földrajzi helyen működik, ahol PayPal van. PayPal rendelkezésre állás és támogatás kizárólag a PayPal szabályozható, és a szolgáltatás bármikor megszüntetheti PayPal.

- A payU fizetési konfiguráció jelenleg csak Indiában működik. A PayU rendelkezésre állását és támogatását kizárólag a PayU vezérli, és a PayU bármikor megszüntetheti.

- Olvassa el és értse meg a jelen Partnerközpont SDK [EULA-ban.](/legal/partner-center/eula-partner-center-sdk)

## <a name="using-the-csp-customer-storefront-builder"></a>A CSP Customer Storefront Builder használata

A CSP-partnerek rendszergazdái Partnerközpont csp-ügyféltárolót közvetlenül a Partnerközpont. Minimális erőfeszítéssel új webhely helyezhető üzembe a partner bérlője számára. Az üzembe helyezést követően a partnerek a webhely használatával konfigurálják a márkajelzést, az ajánlatokat és a fizetéssel kapcsolatos információkat, majd megoszthatják a webhely URL-címét az ügyfelekkel.

Az áruházbeli webhely létrehozásának folyamata a következő:

1. [A webhely üzembe helyezése](#deploy)

2. [Az áruház konfigurálása](#configure)

3. [Tranzakció a áruházban](#transact)

### <a name="deploy"></a>Üzembe helyezés

Üzembe helyezési lehetőségek:

- Töltse le [Partnerközpont áruház mintakódját a](https://github.com/Microsoft/Partner-Center-Storefront) GitHub
- Integrálás az Azure-ral a konfigurált webhely üzembe helyezéséhez
- Üzembe helyezés meglévő előfizetésen vagy saját előfizetéssel

### <a name="configure"></a>Konfigurálás

Az áruház testreszabásához nincs szükség fejlesztési készségekre.

A konfiguráláshoz jelentkezzen be Partnerközpont rendszergazdai hitelesítő adataival:

- **Védjegyezés:** vállalatnév, embléma, névjegyek stb.

- **Ajánlatok:** megtekintheti az összes CSP-ajánlatot. Kiválaszthatja, hogy az ügyfelek mely ajánlatokat nézik meg és vásárolhatják meg. Személyre szabhatja az ajánlat adatait, és hozzáadhatja az árat.

- **PayPal konfigurálása:** adja meg PayPal fizetési fiókjának adatait. Ha még nincs fiókkal PayPal, látogasson el ide, és hozzon létre [https://www.paypal.com](https://www.paypal.com) egy új fiókot. A fiók az ügyfelek PayPal jóváírására lesz használva. *A partnerek és a partnerek közötti kapcsolatért nem a Microsoft PayPal. A PayPal megkövetelheti, hogy a partner vagy a partner ügyfelei további feltételeket is elfogadjanak.*

- (*India esetében*) **PayU payment configuration**(Fizetési konfiguráció): adja meg a PayU Money fizetési fiók adatait. Ha még nincs PayU-fiókja, látogasson el ide, és hozzon létre [https://www.payumoney.com/](https://www.payumoney.com/) egy új fiókot. Ez a fiók lesz használva a PayU-hoz az ügyfelek által történt kifizetések jóváírására. *A partnerek és a PayU közötti kapcsolatért nem a Microsoft a felelős. A PayU használata megkövetelheti, hogy a partner vagy a partner ügyfelei további feltételeket is elfogadjanak.*

### <a name="transact"></a>Tranzakciós

- Az üzembe helyezést követően az ügyfelek azonnal vásárolhatnak és tranzakciót is el tudnak kezdeni.

- Az ügyfelek közvetlenül a partnerportálon vásárolhatnak, amely integrálva van a Partnerközpont SDK.

#### <a name="customer-countries"></a>Ügyfél országok

Az ügyfelek a következő országokhoz tartoznak:

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
| Po           | Lengyelország         |
| PT           | Portugália       |
| RO           | Románia        |
| SK           | Szlovákia       |
| SL           | Szlovénia       |
| ES           | Spanyolország          |
| SE           | Svédország         |
| CH           | Svájc    |
| GB           | Egyesült Királyság |
| USA           | Egyesült Államok  |

## <a name="partner-experience-scenarios"></a>Partneri élmények forgatókönyvei

### <a name="deployment-scenario"></a>Központi telepítési forgatókönyv

Továbbfejlesztett vagy testreszabott CSP-ügyféltároló üzembe helyezése:

- Töltse le [Partnerközpont áruházbeli mintakódot](https://github.com/Microsoft/Partner-Center-Storefront) a további testreszabások éhez.

- A Microsoft Visual Studio 2015 (vagy újabb) használatával fejleszthet.

- További módosításokat és fejlesztéseket (például engedélyeket, tanúsítványokat, jegyzékváltozásokat és más elemeket) is felépíthet.

### <a name="configuration-scenario"></a>Konfigurációs forgatókönyv

- Az újonnan létrehozott webhely egy partnerbérlőhöz van kapcsolva, és hozzáféréssel rendelkezik a partnerbérlő összes rendszergazdai fiókhoz.

  - A partnerek bejelentkeznek erre az új webhelyre a Partnerközpont hitelesítő adataik használatával.

- A storefront alkalmazás jelenleg a francia, a spanyol, a holland, a német, a japán és az angol nyelvet támogatja. (Az angol a tartalék nyelv.)

  - Az áruház a partner alapértelmezett területi beállítását használva konfigurálja a területi beállítást a Partnerközpont. Ezzel a területi beállításokkal konfigurálhatók a pénznemek, a dátumformátumok és a honosított ajánlatok az adattárban.

- A partnerek konfigurálják a márkajelzést, az ajánlatokat PayPal vagy a payU (for India) fizetési adatait.

- A partnerek frissítheti a vállalat nevét, cégemblémát, fejlécképet, értékesítési és támogatási kapcsolattartókat stb.

- A partnerek a saját területük alapján minden elérhető CSP-ajánlatot láthatnak.

  - A partnerek kiválaszthatja, hogy mely ajánlatokat szeretnék megmutatni az összes ügyfélnek.

  - Egy CSP-partner kiválaszthat egy vagy több ajánlatot, és frissítheti a nevet, a mennyiséget, a funkció leírását és az árat.
  - Az ár az éves ár. Az ügyfelek évente iratkoznak fel.

- A partnerek bármikor konfigurálhat előre jóváhagyott tranzakciókat (a) az összes jelenlegi és jövőbeli ügyfélhez vagy (b) adott ügyfélhez.

  - Az előzetesen jóváhagyott ügyfeleknek nem kell fizetniük a portálon, amikor új előfizetéseket adnak hozzá, további licenceket vásárolnak a meglévő előfizetéshez, vagy megújítják az előfizetést.

  - Az előzetesen jóváhagyott ügyfelek nem lesznek átirányítva a PayPal vagy PayU-hoz (India esetén) a tranzakciók során történő fizetésért.

  - Az előre jóváhagyott ügyféltranzakciók lehetővé teszik, hogy a partner offline számlázást és számlázást végezzen az előre jóváhagyott ügyfeleinek.

- A CSP-partnerek meg PayPal a fiókjuk adatait, például PayPal ügyfél-azonosítót és titkos adatokat. A CSP-partnerek azt is kiválaszthatja, hogy tesztgépet vagy élő fiókot szeretnék-e használni.

  - A partnerek a hitelesítő adataimban [https://developer.paypal.com/](https://developer.paypal.com/) találhatják meg **& információkat.** Ezt az információt le is kaphatja egy aktuális alkalmazásból, vagy egy új alkalmazás létrehozásával a PayPal.
  - Hozzon létre egy PayPal fiókot, ha még nem rendelkezik fiókkal. A fiók az ügyfelek PayPal jóváírására lesz használva.

    - Üzleti fiók megnyitásához PayPal lásd: [https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register](https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register) .

    - Az új PayPal lásd: [https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/](https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/) .

- (Indiában) egy CSP-partner meg tudja megadni a PayU-pénzfiók adatait, például a PayU-ügyfél azonosítóját és jelszavát. A partnerek további információt találhatnak a rel [https://developer.payumoney.com/](https://developer.payumoney.com/) kapcsolatban.

  - Hozzon létre egy új PayU Money-fiókot, ha még nem rendelkezik ilyen fiókkal. A PayU Money-fiók megnyitásához látogasson el a [https://www.payumoney.com/merchant-account/#/](https://www.payumoney.com/merchant-account/#/) webhelyre. Ez a fiók lesz használva a PayU-hoz az ügyfelek által történt kifizetések jóváírására.

## <a name="customer-experience-scenarios"></a>Felhasználói élmény forgatókönyvei

### <a name="new-customer-sign-up-scenario"></a>Új ügyfél-regisztráció forgatókönyve

- Alapértelmezés szerint a webhely nyilvánosan elérhető, és a partner katalógusát jeleníti meg a kezdőlapon.

- Az ügyfelek mostantól nagy számú ügyfél [országhoz is tartoznak.](#customer-countries)

- A hangsúly az Európai Szabad trade Association (EFTA) országok, a Észak-Amerika, Japán, India, Ausztrália és Új-Zéland régióira koncentrált.
  - Ez a funkció a regionális engedélyezési támogatást használja a Partnerközpont SDK.

- Az ügyfelek a katalógusból választhatják ki a megvásárolni kívánt ajánlatot.
  - Hozzáadhatják az ügyfélnevet, a címet és a tartománnyal kapcsolatos információkat.

- Az ügyfelek a fizetési PayPal (India esetében) lesznek irányítva. Az ügyfelek a következő módokon fizethet:
  - Meglévő PayPal vagy PayU-fiókjuk (India esetében)
  - Az országuk által támogatott támogatási eszközök PayPal vagy PayU (India esetén). Ide tartozhatnak például a hitelkártyák, a bankkártyák és a banki fiókok.

- Ehhez az ügyfélhez létrejön egy ügyfélbérlő. A bérlői rendelés sikeres létrehozása után az ügyfeleknek meg kell adni a fiók felhasználónevét, jelszavát és előfizetési adatait.
  - Az ügyfelek mentheti a felhasználónevet és a jelszót, hogy bejelentkezve maradjanak a további vásárlások érdekében.
  - Minden előfizetést egy évig vásárolnak, és az ügyfelek az előfizetés záró dátumát megelőző 30 napon belül újíthatók meg.

### <a name="view-prior-purchases-scenario"></a>Korábbi vásárlások forgatókönyvének megtekintése

- Az ügyfél az Ügyfél bérlői felhasználónevével és jelszavával jelentkezik be, és a Saját **rendelések szakaszra** kerül.

- Az ügyfelek a Saját rendelések oldalra **navigálva** megtekinthetik a megvásárolt előfizetéseket, és szükség esetén frissítéseket is el tudnak látni.

- Az ügyfelek a Saját **előfizetések** oldalra navigálva megtekinthetik az összes előfizetést (licencalapú és használatalapú), beleértve az előfizetésben fenntartott előfizetéseket Partnerközpont.

### <a name="add-licenses-to-existing-subscriptions-scenario"></a>Licencek hozzáadása meglévő előfizetési forgatókönyvekhez

- A Saját **rendelések szakaszban** az ügyfelek további licenceket adhatnak hozzá a meglévő előfizetésekhez. Az ügyfelek az előfizetési év során bármikor további licenceket adhatnak hozzá.

- Minden hozzáadott licenc nem módosítja az előfizetés záró dátumát. Az előfizetés ára azonban a licenc hozzáadásának dátuma és az év dátuma alapján változik. A díjszabás napi rendszerességgel van időzített, és csak az év hátralévő napjaiért kell díjat fizetni.

### <a name="add-more-subscriptions-scenario"></a>További előfizetések hozzáadása forgatókönyv

- Az ügyfelek bármikor vásárolhatnak bármilyen számú előfizetést a Saját rendelések területen található **Előfizetések** hozzáadása **szakaszban.**

- Az ügyfél kiválaszthat egy előfizetést, hozzáadhat egy mennyiséget, és fizethet a tranzakció befejezéséhez, és azonnal elkezdheti használni az előfizetést. Ha az ügyfél egy előre jóváhagyott ügyfél, az előfizetés azonnal használatra elérhető, és a rendszer számlát küld az ügyfélnek fizetésre.

### <a name="renew-subscription-scenario"></a>Előfizetés megújítása forgatókönyv

- Az ügyfél az előfizetés záró dátumát megelőző 30 napban újíthatja meg az előfizetést.

- Ez csak az elmúlt 30 napban érhető el.

- Ha az elmúlt 30 napban nem újította meg az előfizetést, az előfizetés el lesz távolítva az ügyfélbérlő előfizetési listájából.

- A megújítás során nem frissítheti a mennyiséget.

### <a name="payments-scenario"></a>Fizetési forgatókönyv

- Ha az ügyfelet előzetesen jóváhagyták a tranzakciókhoz a rendszergazda, a fenti forgatókönyvekben nem jelennek meg a fizetési mód. Ehelyett a partner elküldheti a számlát az előre jóváhagyott ügyfélnek.

- Minden új vásárláshoz további licenceket adhat hozzá, előfizetéseket adhat hozzá és újíthat meg. Az ügyfél ezen a webhelyen keresztül fizethet egy partnernek PayPal vagy PayU-val (India esetén).

- Ez a webhely integrálva van PayPal vagy PayU-val (India esetén), és lehetővé teszi a partnerek számára, hogy fogadjanak el fizetéseket az ügyfeleiktől. PayPal vagy PayU -kreditek (India esetében) ezt az összeget egy partner fiókjában. PayPal vagy PayU (for India) banki számlakezelése ezen a webhelyen kívül található, és a PayPal.com vagy PayUmoney.com felügyelt.

- Ez attól függ, hogy a partnerek a PayPal.com vagy a PayPal.com webhelyen vagy az PayUmoney.com. A Microsoft nem menti ezeket az adatokat és a tényleges fizetési tranzakciókat, amelyek ennek a lehetőségnek a használata miatt adódnak.

### <a name="prorated-pricing-scenario"></a>Díjszabási forgatókönyv

- Ez a webhely támogatja az árrített díjszabást olyan esetekben, amikor az ügyfelek további licenceket adnak hozzá egy meglévő előfizetéshez.

- Minden előfizetés egy év után lejár, és az előfizetés vásárlása után nem módosítható.

- Az előfizetés záró dátuma nem változik további licencek hozzáadásával. Az ügyfelek a záró dátumig hátralévő napokért díjat számítunk fel. Ha például az első napon az előfizetés költsége 365 dollár, és hozzáad egy további licencet a második napon, az új licenc ára 364 dollár lesz. Ha 10 nappal később hozzáad még egy licencet, az ára 354 dollár lesz.
