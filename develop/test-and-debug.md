---
title: Tesztelés és hibakeresés az integrációs tesztkészletben
description: Megtudhatja, hogyan használhatja a Partnerközpont-integrációs tesztfiókot (és a kapcsolódó jogkivonatokat) a kód tesztelésére és hibakeresésére, hogy véletlenül ne számítsa fel új díjakat.
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1a446f1d9a9d7370be2715305ccbaa71b09cfd45957cf8663afb42a23706a7be
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989270"
---
# <a name="test-and-debug-with-your-partner-center-integration-sandbox-to-avoid-paying-unexpected-charges"></a>Tesztelje és hibakeresést végezni a Partnerközpont integrációs tesztkészletben a váratlan költségek elkerülése érdekében

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A kód tesztelése érdekében használja az integrációs tesztfiókot az Partnerközpont-ban (és a megfelelő jogkivonatokat), hogy véletlenül ne legyen olyan új díj felszámodása, amelyért a vállalat fizet. További információ erről az éles környezetben való tesztelési (TiP) környezetről: API-hozzáférés beállítása a [Partnerközpont.](set-up-api-access-in-partner-center.md)

## <a name="integration-sandbox-constraints"></a>Integrációs védőfal megkötései

Ha automatizált buildellenőrzési teszteket futtat, éles környezetben végez tesztelést, vagy manuális tesztelést végez az integrációs tesztkészletben, elérheti az integrációs tesztkészlet maximális korlátját. Ez a korlát 75 ügyfél, 5 előfizetés ügyfélenként és 25 licenc előfizetésenként.

A 25 licences korlát azt jelenti, hogy nem szerezhet be olyan ajánlatot a védőfalon, amely legalább 25 licenccel rendelkezik. Ez a korlátozás magában foglalja a próbaverziókat is.

A sandbox környezetekben különböző számla- és egyeztetési fájlok érhetők el, de nem mindegyik érhető el örökölt vagy modern platformokon. További információért ellenőrizze az alábbi táblázatot.

| **Fájlok**                    | **Az örökölt szolgáltatásban érhető el** | **Elérhető a Modernben** |
| ---------------------------- | ------------------------ | ------------------------ |
| PDF-formátumú számla                  | Nem                       | Igen                      |
| Számla egyeztetési fájlja | Nem                       | Igen                      |
| Számlabecslési fájl       | Nem                       | Igen                      |
| Napi számlázható használati adatok fájlja     | Nem                       | Igen                      |
| Napi ki nemszámlázatlan használati fájl   | Nem                       | Igen                      |


### <a name="azure-plan"></a>Azure-csomag

Alapértelmezés szerint a partnerek nem helyezhetnek üzembe Azure-csomagokat a tesztkörnyezeti fiókjukkal. Azoknak a partnereknek, akiknek a tesztkörnyezeti fiókjukkal kell ezt elvégezniük, hozzáférést kell kérniük. A hozzáférés útjára való jelentkezéshez lépjen kapcsolatba Microsoft-fiók felettesével vagy üzleti kapcsolattartóval. Azok a partnerek, akik korábban hozzáférést kértek az Microsoft Azure-előfizetések (MS-AZR-0145P) építéséhez a saját sandbox-fiókjukban, nem kell ismét hozzáférést alkalmazniuk. Automatikusan hozzáférést kapnak az Azure-csomagok építéshez.

Azon partnerekre, akiknek a sandbox-fiókjai jóvá vannak hagyva az Azure-csomagok kiépítése érdekében, a következő korlátok érvényesek:

- Minden egyes sandbox partnerfiók legfeljebb 10 Azure-csomagtal rendelkezik az összes ügyfélbérlőben (függetlenül attól, hogyan oszlik meg a csomagok az ügyfelek között).

- A közvetlen számlázási partnerek ügyfélbérlőnként legfeljebb egy Azure-tervet hozhatnak létre.

- Egy közvetett szolgáltató ügyfélbérlőnként legfeljebb három Azure-csomag hozható létre (a partnerként megadott különböző közvetett viszonteladók számára).

- Minden Azure-csomag legfeljebb három Azure-előfizetéssel rendelkezik.

- A sandbox-fiókban lévő összes CSP Azure-előfizetés adatközpontonként négy virtuálisgép-magra van korlátozva. Ezért nem létesíthet négynél több virtuálisgép-magot igénylő virtuálisgép-SKUS-okat. Bizonyos speciális virtuálisgép-SKUS-k, például a GPU-magok szintén ki vannak zárva.

- Minden egyes sandbox partnerfiók számlázási ciklusonként 2000 DOLLÁR (USD) költségkeretet kap az összes Azure-csomagra. Ha egy partner eléri a költekedő korlátot, az összes Azure-csomag átmenetileg le lesz tiltva a következő számlázási ciklusig.

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>Felhőszolgáltató (CSP) Azure-előfizetési ajánlatok

A CSP Azure-előfizetési ajánlatok alapértelmezés szerint nem érhetők el a sandbox-fiókokhoz. Ezek közé tartozik az MS-AZR-0146P, az MS-AZR-DE-0146P és az MS-AZR-USGOV-0146P a Microsoft nyilvános felhőben, német felhőben és kormányzati felhőben elérhető CSP Azure-előfizetések esetében. Azok a partnerek, akiknek hozzáférésre van szükségük ezekhez az ajánlatokhoz a saját sandbox-fiókjukkal, hozzáférést kell alkalmazniuk. A hozzáférésre való jelentkezéshez beszéljen Microsoft-fiók felettesével vagy üzleti kapcsolattartóval.

Azok a partnerek, akiknek a sandbox-fiókjait jóváhagyták a CSP Azure-előfizetési ajánlatokhoz, a következő korlátozások érvényesek:

- Legfeljebb 375 aktív előfizetéssel rendelkezik (ügyfélenként 75 ügyfél x 5 előfizetés). Ezekből azonban csak 10 lehet CSP Azure-előfizetés.

- Ha egy CSP Azure-előfizetés eléri a 200 dollárnyi Azure-használatot, az erőforrásai ideiglenesen le vannak tiltva a következő számlázási ciklusig. Továbbra is aktív előfizetésnek számít, és beleszámolt a 10 aktív Azure-előfizetés korlátba.

- A sandbox-fiókban lévő összes CSP Azure-előfizetés adatközpontonként négy virtuálisgép-magra van korlátozva. Ezért nem létesíthet négynél több virtuálisgép-magot igénylő virtuálisgép-SKUS-okat. Bizonyos speciális virtuálisgép-SKUS-k, például a GPU-magok szintén ki vannak zárva.

> [!Important]
> A 2018. augusztus 1. előtt a sandbox-fiókokkal létesített összes meglévő CSP Azure-előfizetés már nem támogatott, és a Microsoft 2018. október 16. és 2018. október 31. között megszünteti őket. Az előfizetések megszüntetése után azok nem engedélyezhetők újra, és a társított adatok már nem érhetők el. Azok a partnerek, akik értékes adatokat tárolnak ezekben az előfizetésekben, 2018. október 16. előtt kell biztonsági adatokat tárolniuk.

### <a name="azure-reserved-vm-instance"></a>Azure-beli fenntartott virtuálisgép-példány

Ha [azure-beli fenntartott virtuálisgép-példányt](purchase-azure-reservations.md) vásárol a saját sandbox-fiókjával, ügyfelenként legfeljebb két virtuálisgép-példányt használhat. Emellett csak a következő Azure-beli fenntartott VM-példány terméktermék-terméktermék-termékből választhat:

| Termékcím  | Hatályos dátum  | Termékváltozat címe                                               | Régió [ArmRegionName] | Példánykulcs [ArmSkuName] | Időtartam | Fogyasztásmérő azonosítója       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| B sorozat       | 12/1/2017 0:00  | Fenntartott virtuálisgép-példány, Standard_B1s, Korea déli részén, 1 év    | KoreaSouth             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| B sorozat       | 12/1/2017 0:00  | Fenntartott virtuálisgép-példány, Standard_B1s, USA keleti régiója, 1 év     | eastus                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| B sorozat       | 12/1/2017 0:00  | Fenntartott virtuálisgép-példány, Standard_B1s, USA 2. nyugati régiója, 1 év   | westus2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| B sorozat       | 12/1/2017 0:00  | Fenntartott virtuálisgép-példány, Standard_B1s, USA északi középső középső sarka, 1 év    | northcentralus | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| B sorozat       | 12/1/2017 0:00  | Fenntartott virtuálisgép-példány, Standard_B1s, Kelet-Ca, 1 év     | CanadaEast             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### <a name="subscriptions-for-commercial-marketplace-products"></a>Előfizetések kereskedelmi piactéri termékekhez

Éles környezetben, miután létrehozott egy előfizetést a kereskedelmi piactéri SaaS-termékekre, le kellkérése egy személyre szabott aktiválási hivatkozást a Partnerközpont-ból, majd a telepítési folyamat befejezéséhez látogasson el [a](create-subscription-azure-marketplace-products.md)közzétevő webhelyére. Az előfizetés számlázása csak a beállítás befejezése után kezdődik meg.

A CSP-védőkörnyezetben nincs integráció a isv-ekkel. Ha egy aktiválási hivatkozást próbál lekérni a Partnerközpont, a rendszer egy üres hivatkozást ad vissza. Ezzel a hely nélküli hivatkozással nem fejezhető be a telepítési folyamat a közzétevő webhelyén. A kereskedelmi piactéri SaaS-termékekre való előfizetések számlázásának teszteléséhez használja az integrációs tesztfiókot: Tesztkészlet-előfizetés aktiválása kereskedelmi [piactéri termékekhez.](activate-sandbox-subscription-azure-marketplace-products.md) Az előfizetés számlázása a sikeres aktiválás után kezdődik.

A következő tesztelési körben a következő cikkekben talál helyet, hogy a tesztfutat végén megtisztítsa a adatokat:

- [Ügyfélfiók törlése az integrációs tesztkörnyezetből](delete-a-customer-account-from-the-integration-sandbox.md)

- [Előfizetés mennyiségének csökkentése](change-the-quantity-of-a-subscription.md)

- [Előfizetés felfüggesztése,](suspend-a-subscription.md) hogy eltávolítható legyen.

## <a name="best-practices-for-rest-development"></a>Ajánlott eljárások REST-fejlesztéshez

- Használjon egy hálózati nyomkövetési eszközt, hogy lássa a kérést, a választ, valamint azt, hogy a válasz tartalmaz-e hibákat a HTTP-állapotkódban. További információ a hibakezelésről: Partnerközpont [REST-hibakódok.](error-codes.md)

- Használjon új korrelációs azonosítót a Partnerközpont REST API. Ez a gyakorlat jobb naplózást biztosít, és segít a hibakeresés során. További információ: [REST Partnerközpont fejlécek.](headers.md)

## <a name="troubleshooting-tips-for-common-rest-problems"></a>Hibaelhárítási tippek a REST gyakori problémáihoz

- Tekintse át az összes fejléctulajdonságokat, beleértve az URL-címet és az API-verziót.

- Szükség esetén győződjön meg arról, hogy a tulajdonságok szerepelnek, és megfelelően vannak formázva.

- Gyakori hiba a tömb helytelen formázása.

- **Az ETagek** ideiglenesek, ezért nem tárolhatók. Ha egy függvényhíváshoz szükség van **egy ETagre,** használja a legújabb **ETags** értéket az erőforrás lehívásához. **Az ETag értékeknek** idézőjelek között kell szerepelnie, például sztringként:

   ```rest
   If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
   ```
