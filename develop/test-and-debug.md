---
title: Tesztelés és hibakeresés integrációs homokozóval
description: Megtudhatja, hogyan használhatja a partner Center Integration sandbox-fiókját (és a kapcsolódó jogkivonatokat) a kód teszteléséhez és hibakereséséhez, így nem kell véletlenül új díjakat fizetnie.
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3ff4a7ec3ad984b09c60d3d820423c614fb8020d
ms.sourcegitcommit: 9f8ba784171ab4f980ed0c60ef6f2323849c4a98
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/14/2021
ms.locfileid: "100499881"
---
# <a name="test-and-debug-with-your-partner-center-integration-sandbox-to-avoid-paying-unexpected-charges"></a>Tesztelés és hibakeresés a partner Center-integrációs munkaterülettel a váratlan költségek kifizetésének elkerülése érdekében

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A kód teszteléséhez használja az Integration sandbox-fiókot a partner Centerben (és a hozzá tartozó jogkivonatokban), így nem kell véletlenül új díjakat fizetnie, melyeket a vállalat a fizetésért felelős. További információ erről a tesztelési célú üzemi (TiP) környezetről: [API-hozzáférés beállítása a partner Centerben](set-up-api-access-in-partner-center.md).

## <a name="integration-sandbox-constraints"></a>Integrációs homokozó – korlátozások

Ha automatizált Build-ellenőrzési teszteket futtat, éles tesztelést végez, vagy manuális tesztelést hajt végre az integrációs munkaterületen, az integrációs szolgáltatáshoz tartozó munkaterületre vonatkozó maximális korlátokat is elérheti. Ezek a korlátok 75 ügyfél, 5 előfizetés felhasználónként és 25 licenc/előfizetés.

A 25 licences korlát azt jelenti, hogy nem vásárolhat olyan ajánlatot a homokozóban, amely legalább 25 licenccel meghaladja a licencet. Ez a korlátozás próbaverziókat is tartalmaz.

A homokozóban számos különböző számla-és egyeztetési fájl érhető el, de nem mindegyik a régi vagy a modern platformon érhető el. További részletekért ellenőrizze az alábbi táblázatot.

| **Fájlok**                    | **Elérhető a régiben** | **Elérhető a modern** |
| ---------------------------- | ------------------------ | ------------------------ |
| PDF-formátumú számla                  | Nem                       | Igen                      |
| Számla-egyeztetési fájl | Nem                       | Igen                      |
| Számla becsült fájlja       | Nem                       | Igen                      |
| Napi számlázott használati fájl     | Nem                       | Igen                      |
| Napi nem számlázott használati fájl   | Nem                       | Igen                      |


### <a name="azure-plan"></a>Azure-csomag

Alapértelmezés szerint a partnerek nem tudják kiépíteni az Azure-csomagokat a sandbox-fiókjaik használatával. Azoknak a partnereknek, akiknek a homokozó-fiókjával kell rendelkezniük, hozzáférésre van szükségük. A hozzáférésre való jelentkezéshez lépjen kapcsolatba a Microsoft-fiók Manager vagy a Business Contact szolgáltatással. Azokat a partnereket, akik korábban már alkalmazták az Microsoft Azure (MS-AZR-0145P) előfizetések kiépítésére a sandbox-fiókokban, nem kell újra alkalmazni a hozzáférést. Hozzáférést kapnak az Azure-csomagok automatikus kiépítéséhez.

A következő korlátozások érvényesek azon partnerek számára, akik az Azure-csomagok kiépítéséhez jóváhagyták a sandbox-fiókokat:

- Minden sandbox-partner fiók legfeljebb 10 Azure-csomagot tartalmazhat az összes ügyfél-bérlőn (függetlenül attól, hogy a csomagok hogyan oszlanak el az ügyfelek között).

- A közvetlen számlás partner akár egy Azure-csomagot is létrehozhat egy ügyfél-bérlőn.

- A közvetett szolgáltatók legfeljebb három Azure-csomagot hozhatnak létre ügyfél-bérlőként (a partner-rekordként megadott különböző közvetett viszonteladók esetében).

- Minden egyes Azure-csomaghoz legfeljebb három Azure-előfizetés tartozhat.

- A sandbox-fiókhoz tartozó összes CSP Azure-előfizetés egy adatközpontban legfeljebb négy virtuálisgép-maggal rendelkezik. Ezért nem telepíthet olyan virtuálisgép-SKU-ket, amelyek több mint négy virtuálisgép-magot igényelnek. Bizonyos speciális virtuálisgép-SKU-ket, például a GPU-magokat is kizárják.

- Minden egyes sandbox-partneri fiók esetében az összes Azure-csomagra vonatkozó költségkeret $2000 (USD). Ha egy partner eléri a költségkeretet, az összes Azure-csomag átmenetileg le lesz tiltva a következő számlázási ciklusig.

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>Felhőalapú megoldás-szolgáltató (CSP) Azure-előfizetési ajánlatok

A CSP Azure-előfizetési ajánlatok alapértelmezés szerint nem érhetők el a sandbox-fiókok számára. Ezek közé tartozik az MS-AZR-0146P, az MS-AZR-DE-0146P és az MS-AZR-USA KORM.-0146P for CSP Azure-előfizetések a Microsoft nyilvános felhőben, a német felhőben és a kormányzati felhőben. Azoknak a partnereknek, akiknek hozzá kell férniük az ajánlatokhoz a sandbox-fiókkal, hozzáféréssel kell rendelkezniük. A hozzáférésre való jelentkezéshez beszéljen a Microsoft-fiók Manager vagy a Business Contact szolgáltatással.

Az alábbi korlátozások érvényesek azon partnereink számára, akiknek a sandbox-fiókját jóváhagyták a CSP Azure-előfizetési ajánlatok esetében:

- Legfeljebb 375 aktív előfizetéssel (75 ügyfél x 5 előfizetéssel) rendelkezhet. Azonban csak 10 lehet CSP Azure-előfizetés.

- Ha egy CSP Azure-előfizetés eléri a $200 Azure-beli használatot, az erőforrásai átmenetileg le lesznek tiltva a következő számlázási ciklusig. A szolgáltatás továbbra is aktív előfizetésnek minősül, és a 10 aktív Azure-előfizetésre vonatkozó korlátnak számít.

- A sandbox-fiókhoz tartozó összes CSP Azure-előfizetés egy adatközpontban legfeljebb négy virtuálisgép-maggal rendelkezik. Ezért nem telepíthet olyan virtuálisgép-SKU-ket, amelyek több mint négy virtuálisgép-magot igényelnek. Bizonyos speciális virtuálisgép-SKU-ket, például a GPU-magokat is kizárják.

> [!Important]
> Az 2018. augusztus 1. előtt üzembe helyezendő összes meglévő CSP Azure-előfizetés már nem támogatott, és a Microsoft a 2018 október 16 – október 31. között megszűnik. Az előfizetések megszüntetése után azok nem engedélyezhetők újra, és a társított adatai már nem érhetők el. Az Ezen előfizetések alatt tárolt értékes adattal rendelkező partnereknek az 2018. október 16. előtt biztonsági másolatot kell készíteniük az adatról.

### <a name="azure-reserved-vm-instance"></a>Azure-beli fenntartott VM-példány

Ha az Azure-beli [fenntartott VM-példányt vásárolja](purchase-azure-reservations.md) meg a sandbox-fiókjával, az ügyfél két virtuálisgép-példányra korlátozódik. Arra is korlátozódik, hogy csak a következő Azure-beli fenntartott VM-példányokból származó termékekből válasszon ki:

| Termék címe  | Hatálybalépés dátuma  | SKU címe                                               | Régió [ArmRegionName] | Példány kulcsa [ArmSkuName] | Időtartam | Felhasználási mérőszám azonosítója       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| B sorozat       | 12/1/2017 0:00  | Fenntartott VM-példány, Standard_B1s, Korea déli régiója, 1 év    | KoreaSouth             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| B sorozat       | 12/1/2017 0:00  | Fenntartott VM-példány, Standard_B1s, USA keleti régiója, 1 év     | eastus                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| B sorozat       | 12/1/2017 0:00  | Fenntartott VM-példány, Standard_B1s, USA 2. nyugati régiója, 1 év   | westus2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| B sorozat       | 12/1/2017 0:00  | Fenntartott VM-példány, Standard_B1s, USA északi középső régiója, 1 év    | northcentralus | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| B sorozat       | 12/1/2017 0:00  | Fenntartott VM-példány, Standard_B1s, CA keleti régiója, 1 év     | CanadaEast             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### <a name="subscriptions-for-commercial-marketplace-products"></a>Kereskedelmi Piactéri termékek előfizetései

Éles környezetben, miután [létrehozta a kereskedelmi Marketplace SaaS-termékek előfizetését](create-subscription-azure-marketplace-products.md), egy személyre szabott aktiválási hivatkozást kell lekérnie a partner Center webhelyről, és el kell végeznie a közzétevő helyét a telepítési folyamat befejezéséhez. Az előfizetés számlázása csak a telepítés befejeződése után kezdődik.

A CSP homokozó környezetében nincs integráció az ISV-val. Ha a partner Centerből próbál meg beolvasni egy aktiválási hivatkozást, a rendszer egy dummy-hivatkozást ad vissza. Ez a dummy-hivatkozás nem használható a telepítési folyamat befejezéséhez a közzétevő webhelyén. A kereskedelmi Piactéri SaaS-termékekhez való előfizetés számlázásának teszteléséhez az Integration sandbox-fiók használatával a kereskedelmi [Piactéri termékekhez készült homokozó-előfizetés aktiválása](activate-sandbox-subscription-azure-marketplace-products.md) című témakörben talál helyet. Az előfizetés számlázása a sikeres aktiválás után kezdődik.

Ha a teszt végén szeretné megtisztítani a műveletet, hogy a következő tesztelési fordulóra van-e hely, tekintse meg a következő cikkeket:

- [Ügyfélfiók törlése az integrációs tesztkörnyezetből](delete-a-customer-account-from-the-integration-sandbox.md)

- [Előfizetés mennyiségének csökkentése](change-the-quantity-of-a-subscription.md)

- [Felfüggesztheti az előfizetést](suspend-a-subscription.md) , hogy el tudja távolítani.

## <a name="best-practices-for-rest-development"></a>Ajánlott eljárások a REST-fejlesztéshez

- Használjon hálózati nyomkövetési eszközt, hogy megtekintse a kérést, a választ, és ha a válaszban hiba történt a HTTP-állapotkódot illetően. A hibakezelés részletes ismertetését lásd: a [partneri központ Rest](error-codes.md)-hibakódai.

- Használjon egy új korrelációs azonosítót a partner Center REST API minden hívásához. Ez a gyakorlat biztosítja a jobb naplózást, és segítséget nyújt a hibakereséshez. További információ: a [partneri központ Rest-fejlécei](headers.md).

## <a name="troubleshooting-tips-for-common-rest-problems"></a>Hibaelhárítási tippek a REST gyakori problémáihoz

- Tekintse át az összes fejléc-tulajdonságot, beleértve az URL-címet és az API-verziót.

- Szükség esetén győződjön meg arról, hogy a tulajdonságok megfelelően vannak formázva.

- A tömb formázásának helytelen formázása gyakori hiba.

- A **etagek** ideiglenesek, és az eredmény nem tárolható. Ha egy függvény hívásához **etagek** szükséges, használja a legújabb **etagek** értéket az erőforrás újbóli lekérésével. A **etagek** értékeket idézőjelek közé kell foglalni, például egy sztringet:

   ```rest
   If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
   ```
