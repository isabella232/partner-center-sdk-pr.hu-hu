---
title: Partnerközpont – REST hibakódok
description: A hibakódok és a sikeres válasz leírása a Partnerközpont API-kból.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a26d8bebb79074df1bc962d061d3fd975e5e8e7f
ms.sourcegitcommit: 856c14b6b351697e3b3d33f1fe376adbb80517c5
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/02/2021
ms.locfileid: "129378761"
---
# <a name="partner-center-rest-error-codes"></a>Partnerközpont – REST hibakódok

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A Partnerközpont REST API-k egy állapotkódot tartalmazó JSON-objektumot ad vissza. Ez a kód jelzi, hogy a kérés sikeres volt-e, vagy miért.

## <a name="success-responses"></a>Sikeres válaszok

A **2xx állapotkód** azt jelzi, hogy az ügyfél kérése sikeresen megkapta, megértette és elfogadta.

## <a name="http-status-codes"></a>HTTP-állapotkódok

Az alábbi **4xx és** **5xx** állapotkódok hibát jeleznek:

- 400: Hibás kérés
- 401: Jogosulatlan
- 403: Tiltott
- 404: Nem található
- 405: A metódus nem engedélyezett
- 406: Nem elfogadható
- 408: Kérés időtúllépése
- 409: Ütközés, hibakód
- 412: Az előfeltétel nem teljesült
- 429: Túl sok kérelem
- 500: Belső kiszolgálóhiba
- 501: Nincs megvalósítva
- 502: Hibás átjáró
- 503: A szolgáltatás nem érhető el
- 504: Átjáró időtúllépése

## <a name="error-responses"></a>Hibaválaszok

A **4xx** vagy **5xx** állapotkóddal kapcsolatos válasz tartalmaz egy hibaüzenetet, amely tartalmazza a kód hibaállapota(i) részleteit.

A következő táblázat és kódminta egy hibaválasz sémáját ismerteti:

| Név        | Típus   | Description                                                                                                                                            |
|-------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| code        | sztring | Mindig visszaadva. A bekövetkezett hiba fajtáját jelzi. Nem null.                                                                                  |
| leírás | sztring | Mindig visszaadva. Részletesen ismerteti a hibát, és hibakeresési információkat biztosít. Nem null, nem üres. A maximális hossz 1024 karakter. |
| adatok        | array  | Csak néhány hibatípus esetében ad vissza. A hibaobjektumok listája.                                                                                           |
| source      | sztring | Mindig visszaadva. A hiba forrása.                                                                                                              |

```json
{
  "code": <string>,
  "description": <string>,
  "data": [

  ],
  "source": <string>
}
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}
```

## <a name="error-codes"></a>Hibakódok

Az API-k a következő hibakódokat ják vissza:

| HTTP-állapot         | HTTP-hibakód | Hibakód | Description     |
|---------------------|-----------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| OK | 200 | 400072 | Ez az elem nem érhető el. [További információ](https://go.microsoft.com/fwlink/p/?linkid=2164140) |
| Nincs megvalósítva      | 501       | 0          | A kivétel nincs meghatározva       |
| Nem engedélyezett        | 401       | 400        | Hozzáférés megtagadva         |
| NotFound      | 404       | 1000       | Nem található       |
| Forbidden     | 403       | 2006       | A partner nem érvényes az ajánlathoz          |
| BadRequest (Rossz kérdés)          | 400       | 2012       | A kereskedelmi és a Azure Active Directory nem konvertálható.          |
| Forbidden     | 403       | 2030       | A partner nincs az országban való értékesítésre bevetve          |
| Forbidden     | 403       | 2032       | Hozzáférés megtagadva         |
| Forbidden     | 403       | 2091       | Az ajánlat már nem megvásárolható        |
| BadRequest (Rossz kérdés)          | 400       | 2100       | Az Offers API nem támogatja az azonosítójú {0} elemet. Próbálja ki a Products és/vagy a SKUs API-kat      |
| BadRequest (Rossz kérdés)          | 400       | 3000       | Érvénytelen tulajdonság      |
| Forbidden     | 403       | 20002      | A {0} partnerazonosítónak nincs kereskedelmi kapcsolata a ügyfél-azonosítóval. {1}          |
| NotFound      | 404       | 20003      | Az azonosítóval nem {0} található előfizetés.     |
| BadRequest (Rossz kérdés)          | 400       | 27007      | Érvénytelen előléptetési kód         |
| BadRequest (Rossz kérdés)          | 400       | 60000      | Az ügyféllicenc-migrálás meghiúsult     |
| NotFound      | 404       | 60002      | A felhasználói objektum azonosítója nem található       |
| NotFound      | 404       | 60003      | A bérlő nem található      |
| BadRequest (Rossz kérdés)          | 400       | 2001       | Az előfizetések mennyisége nem növelhető vagy csökkenthető az előfizetés felfüggesztése közben          |
| BadRequest (Rossz kérdés)          | 400       | 2002       | Az előfizetési mennyiség nem a minimális és maximálisan engedélyezett mennyiségen belül van     |
| BadRequest (Rossz kérdés)          | 400       | 2006       | Az ajánlathoz nem {0} engedélyezettek az előfizetések frissítései     |
| BadRequest (Rossz kérdés)          | 400       | 2011       | Az azonosítóval és {0} törölt állapottal nem frissíthető előfizetés.         |
| BadRequest (Rossz kérdés)          | 400       | 2054       | Egy meglévő előfizetés számlázási ciklusa nem frissíthető az update-subscription művelettel. Az update-Order művelet használata                |
| BadRequest (Rossz kérdés)          | 400       | 2055       | Az Etag már nem érvényes     |
| BadRequest (Rossz kérdés)          | 400       | 2071       | Az MPN-azonosító nem érvényes Advisor     |
| NotFound      | 404       | 2072       | A közvetett szolgáltató MPN-azonosítója nem érvényes partnerrekordként          |
| Forbidden     | 403       | 2085       | Az ajánlat nem jogosult vásárlásra               |
| BadRequest (Rossz kérdés)          | 400       | 4018       | Nem sikerült feldolgozni ezt a rendelést      |
| BadRequest (Rossz kérdés)          | 400       | 6000       | A számlázási ciklust nem lehetett módosítani, mert a rendelés egy vagy több nem aktív előfizetést tartalmaz         |
| BadRequest (Rossz kérdés)          | 400       | 6001       | A számlázási ciklust nem lehetett módosítani, mert a rendelés egyik ajánlat-terméke nem támogatja a számlázási időszakokat     |
| Forbidden     | 403       | 13605      | A vásárlás befejezéséhez vagy meg kell erősítenie a Microsoft Ügyfélszerződés ügyfél általi elfogadását, vagy az ügyfélnek el kell fogadnia Microsoft Ügyfélszerződés microsoftos felügyeleti központban.           |
| NotFound      | 404       | 20000      | A rendelésazonosító nem található          |
| BadRequest (Rossz kérdés)          | 400       | 27006      | Túllépte az ajánlatazonosítóra vonatkozó korlátot      |
| Ütközés      | 409       | 27009      | Nem engedélyezhető gyermek-előfizetés, ha a szülő előfizetés nem aktív     |
| BadRequest (Rossz kérdés)          | 400       | 600002     | A szervezeti regisztrációs azonosító értéke nem támogatott  <br/><br/>Ez a hiba akkor fordul elő,  ha az ügyfél vállalata/szervezete nem a következő országok valamelyikében található, de a organizationRegistrationNumber értéket próbálta meg megadni. Érintett országok:<br/><br/>– Brazília (AM) <br/>- Egyesült Államok (AZ)<br/>- Majd (BY)<br/>- Magyar (Hu)<br/>- Észak-India (KZ)<br/>- Kirgizisztán (KG)<br/>- Majd (MD)<br/>- Oroszország (RU)<br/>- Tádzsikisztán (TJ)<br/>- Uzbekistan (UZ)<br/>- Egyesült Arab Emírségek |
| BadRequest (Rossz kérdés)          | 400       | 600049     | Hiányoznak a szervezet regisztrációs azonosítójára vonatkozó adatok <br/><br/>Ez a hiba akkor fordul elő, ha az ügyfél vállalata/szervezete a következő országok egyikében található, és a SzervezetRegistrationNumber nem lett megszava. Érintett országok:<br/><br/>– Brazília (AM) <br/>- Egyesült Államok (AZ)<br/>- Majd (BY)<br/>- Magyar (Hu)<br/>- Észak-India (KZ)<br/>- Kirgizisztán (KG)<br/>- Majd (MD)<br/>- Oroszország (RU)<br/>- Tádzsikisztán (TJ)<br/>- Uzbekistan (UZ)<br/>- Egyesült Arab Emírségek       |
| BadRequest (Rossz kérdés)          | 400       | 600050     | A szervezet regisztrációs azonosítójának adatai érvénytelenek, és 0 formátumúnak kell \{ lennie\} <br/><br/>Ez a hiba akkor fordul elő, ha a organizationRegistrationNumber nem érvényes az ügyfél országában található vállalatra. \{A 0 \} a hiba várt reguláriskifejezés-formátumát fogja kapni. Példa: `Organization registration ID information is invalid and should be of the format ^(\\d{7}|\\d{10})$`.          |
| BadRequest (Rossz kérdés)          | 400       | 600051     | Az ügyfél telefonszáma hiányzik <br/><br/>Ez a hiba akkor fordul elő, ha az ügyfél vállalata/szervezete a következő országok egyikében található, de a billingProfile.defaultAddress.phoneNumber nem található meg. Érintett országok:<br/><br/>– Brazília (AM) <br/>- Egyesült Államok (AZ)<br/>- Majd (BY)<br/>- Magyar (Hu)<br/>- Észak-India (KZ)<br/>- Kirgizisztán (KG)<br/>- Majd (MD)<br/>- Oroszország (RU)<br/>- Tádzsikisztán (TJ)<br/>- Uzbekistan (UZ)<br/>- Egyesült Arab Emírségek       |
| Nem engedélyezett        | 401       | 800001     | A partneri jogkivonat hiányzik a kérelem kontextusában             |
| BadRequest (Rossz kérdés)          | 400       | 800002     | Érvénytelen kérelembemenet       |
| InternalServerError | 500       | 800003     | Váratlan szolgáltatáshiba          |
| BadRequest (Rossz kérdés)          | 400       | 800004     | Érvénytelen ajánlatazonosító      |
| InternalServerError | 500       | 800005     | A rendelés létrehozása nem sikerült          |
| NotFound      | 404       | 800007     | Nem sikerült lekérni a kiépítési információkat          |
| NotFound      | 404       | 800008     | Nem sikerült lekérni a kosár azonosítóját        |
| BadRequest (Rossz kérdés)          | 400       | 800009     | Hiba a kocsielem(ék)ékben       |
| BadRequest (Rossz kérdés)          | 400       | 800010     | Az Inventory nem érhető el ehhez a katalóguselemhez     |
| BadRequest (Rossz kérdés)          | 400       | 800011     | Ez az előfizetés nem érvényes Azure-előfizetés        |
| BadRequest (Rossz kérdés)          | 400       | 800012     | Ez az előfizetés nem aktív előfizetés      |
| BadRequest (Rossz kérdés)          | 400       | 800013     | Ez az előfizetés nincs engedélyezve a ri purchase (Ri-vásárlás) funkcióhoz     |
| Ütközés      | 409       | 800014     | Ehhez a rendeléshez függőben lévő módosításra van szükség     |
| NotFound      | 404       | 800015     | Az MPN-azonosító nem található         |
| BadRequest (Rossz kérdés)          | 400       | 800016     | Az MPN-azonosító nem érvényes közvetett viszonteladó              |
| BadRequest (Rossz kérdés)          | 400       | 800017     | A mennyiség ehhez a katalóguselemhez nem érhető el        |
| BadRequest (Rossz kérdés)          | 400       | 800018     | A sandbox korlátja teljesült          |
| Forbidden     | 403       | 800019     | A nem sandbox-bérlők nem szakíthatnak meg vásárlásokat a szoftver-előfizetésen és a folyamatos szoftveren kívül        |
| Forbidden     | 403       | 800020     | A katalóguselem nem jogosult megvásárolni.       |
| BadRequest (Rossz kérdés)          | 400       | 800021     | Ez az előfizetés nem érvényes előfizetés        |
| BadRequest (Rossz kérdés)          | 400       | 800022     | Ön jogosult lehet erre a tranzakcióra. Segítségért forduljon az ügyfélszolgálathoz          |
| Forbidden     | 403       | 800023     | Ön nem jogosult erre a tranzakcióra, mert a kreditkeret nem éri el a vásárlás minimális küszöbértékét. A megrendelés frissítése (vagy) segítségért forduljon az ügyfélszolgálathoz       |
| BadRequest (Rossz kérdés)          | 400       | 800024     | Ön nem jogosult erre a tranzakcióra            |
| BadRequest (Rossz kérdés)          | 400       | 800025     | Ön nem jogosult erre a tranzakcióra, mert a kreditkeret nem éri el a vásárlás minimális küszöbértékét. A megrendelés frissítése (vagy) segítségért forduljon az ügyfélszolgálathoz       |
| BadRequest (Rossz kérdés)          | 400       | 800026     | Ön nem jogosult erre a tranzakcióra            |
| Forbidden     | 403       | 800027     | A katalóguselem nem jogosult mennyiség hozzáadására vagy eltávolítására      |
| Forbidden     | 403       | 800028     | A kezdeti vásárlási időszak már nem érhető el vásárláshoz/frissítéshez         |
| BadRequest (Rossz kérdés)          | 400       | 800029     | A bővítmény nem kapcsolódik a megadott szülő-előfizetéshez         |
| BadRequest (Rossz kérdés)          | 400       | 800030     | Ez az előfizetés nincs regisztrálva     |
| InternalServerError | 500       | 800031     | A vásárlási rendszer nem támogatott     |
| ExpectationFailed   | 417       | 800036     | Az elő feltétel nem sikerült        |
| NotFound      | 404       | 800037     | Az eszközazonosító nem található          |
| NotFound      | 404       | 800038     | Az Asset FutureBillingInfo nem található       |
| Forbidden     | 403       | 800039     | A viszonteladói program állapota nem aktív                |
| BadRequest (Rossz kérdés)          | 400       | 800040     | Az eszköz állapota nem módosítható értékről {0}{1}       |
| BadRequest (Rossz kérdés)          | 400       | 800041     | Ez az elem már aktiválva van                 |
| BadRequest (Rossz kérdés)          | 400       | 800042     | Nem támogatott         |
| Forbidden     | 403       | 800043     | A díjszabási információkhoz való hozzáférés nem biztosított         |
| Ütközés      | 409       | 800060     | A rendelés folyamatban van. Néhány perc alatt ellenőrizheti a legutóbbi rendelési előzményeket           |
| BadRequest (Rossz kérdés)          | 400       | 800061     | A rendelés nem szakítható meg         |
| BadRequest (Rossz kérdés)          | 400       | 800062     | Ön nem jogosult erre a tranzakcióra            |
| BadRequest (Rossz kérdés)          | 400       | 800063     | Ez a {0} rendelés nem szakítható meg. Előfizetések felfüggesztése a PATCH /customers/ {1} /subscriptions/ \<subscriptionId\> használatával          |
| Ütközés      | 409       | 800064     | A {0} kosár feldolgozását egy másik kérés is folyamatban van       |
| BadRequest (Rossz kérdés)          | 400       | 800065     | Nem lehet megnézni egy már elküldött {0} kosárt.      |
| Forbidden     | 403       | 800066     | Az előfizetések kívánt száma túllépte az ügyfélenként engedélyezett előfizetések maximális számát       |
| Forbidden     | 403       | 800067     | A kívánt helyszám túllépte az előfizetésenként engedélyezett maximális helyszámot          |
| Forbidden     | 403       | 800068     | Az előfizetések kívánt száma túllépte a partnerenként engedélyezett Azure-előfizetések maximális számát        |
| Forbidden     | 403       | 800069     | Rendelési hiba – Kockázatkezelés ellenőrzése      |
| BadRequest (Rossz kérdés)          | 400       | 800070     | Az ajánlat nem érhető el a megadott országban      |
| BadRequest (Rossz kérdés)          | 400       | 800071     | A sorelem számának 0-tól a sorelemek darabszáma között kell lennie        |
| BadRequest (Rossz kérdés)          | 400       | 800071     | A sorelem számának 0-tól a sorelemek darabszáma között kell lennie        |
| BadRequest (Rossz kérdés)          | 400       | 800072     | Nem lehet módosítani a számlázási ciklust, ha az előfizetés SyncState (Szinkronizálási állam) művelete nem fejeződött be     |
| Forbidden     | 403       | 800073     | Az ügyfélfiók jelenleg felülvizsgálat alatt áll. Néhány nap múlva vissza kell néznie. Nagyra értékeljük türelmét ebben az időszakban. További információ: {0}              |
| Forbidden     | 403       | 800074     | Az ügyfélfiók jelenleg felülvizsgálat alatt áll. Néhány nap múlva vissza kell néznie. Nagyra értékeljük türelmét ebben az időszakban. További információ: {0}              |
| Forbidden     | 403       | 800075     | helyes válasz. További információért lásd: {0A felhasználói fiókja nem lett jóváhagyva. Az ügyfél tranzakciói nem engedélyezettek. Ellenőrizze az ügyfélfiók adatait}        |
| NotFound      | 404       | 800076     | Az előfizetési előzmények nem találhatók          |
| Forbidden     | 403       | 800077     | A helyalapú SaaS lemondása javítási sorrendben nem támogatott. Használja helyette a patch előfizetést.       |
| BadRequest (Rossz kérdés)          | 400       | 800078     | Érvénytelen előfizetéssel nem lehet átvitelt létrehozni       |
| BadRequest (Rossz kérdés)          | 400       | 800080     | Nem lehet módosítani a számlázási ciklust, ha az előfizetés nincs Mint-fiókhoz társítva        |
| BadRequest (Rossz kérdés)          | 400       | 800081     | Az előfizetés nem frissíthető az aktiválása előtt          |
| BadRequest (Rossz kérdés)          | 400       | 800082     | frissítésre. Próbálkozzon újra, miután az előíró nem áll készen      |
| InternalServerError | 500       | 800083     | A rendelkezésre álláshoz több elérhető mennyiség is rendelkezésre áll         |
| InternalServerError | 500       | 800084     | Nem támogatott időtartam {0}          |
| BadRequest (Rossz kérdés)          | 400       | 800085     | Az előfizetés számlázási ciklusa nem egyezik az eredeti megrendelés számlázási ciklusával        |
| BadRequest (Rossz kérdés)          | 400       | 800086     | Az ügyfélbérlő nem rendelkezik az ajánlathoz szükséges címkékkel        |
| InternalServerError | 500       | 800087     | Probléma van a sorelemekkel.                |
| Forbidden     | 403       | 800088     | A kért hely/s érték túllépte a CatalogID-hez előfizetésenként engedélyezett szabad helyek {0} {1} fennmaradó korlátját – {2}       |
| Forbidden     | 403       | 800089     | Az eszközök/eszközök kért száma túllépte az egyes ügyfelek számára engedélyezett fennmaradó {0} {1} eszközkorlátot         |
| BadRequest (Rossz kérdés)          | 400       | 800090     | Az előfizetések mennyisége nem csökkenthető            |
| BadRequest (Rossz kérdés)          | 400       | 800091     | A felfüggesztett állapotú előfizetés nem frissíthető         |
| BadRequest (Rossz kérdés)          | 400       | 800092     | Nem lehet növelni a licencprogram keretében vásárolt előfizetések Frissítési Garancia számát         |
| BadRequest (Rossz kérdés)          | 400       | 800093     | Az előfizetés nem jogosult automatikus megújításra        |
| InternalServerError | 500       | 800094     | Az előfizetés frissítése nem sikerült                |
| BadRequest (Rossz kérdés)          | 400       | 800095     | Az előfizetéshez nem frissíthető a hely mennyisége      |
| BadRequest (Rossz kérdés)          | 400       | 800096     | Az előfizetés állapota nem frissíthető       |
| BadRequest (Rossz kérdés)          | 400       | 800097     | Az előfizetés számlázási ciklusa nem frissíthető      |
| BadRequest (Rossz kérdés)          | 400       | 800098     | A partner nem frissíthető az előfizetés rekordja alapján        |
| NotFound      | 404       | 800111     | A megadott jogosultságazonosítóval nem található Azure-előfizetés.       |
| Forbidden     | 403       | 800115     | A túlóra már hozzá van rendelve egy másik bérlőhöz. A tulajdonjoggal kapcsolatos kérdések megoldásához lépjen kapcsolatba az ügyféllel.       |
| Forbidden     | 403       | 800114     | Ön nem jogosult az ügyfél túlóra-kezelésére.       |
| Forbidden     | 403       | 800112     | Nem lehet túlárazást beállítani, mert az ügyfél örökölt Azure-előfizetésekkel rendelkezik.       |
| NotFound      | 404       | 900100     | Az átadási kérelem nem található        |
| Ütközés      | 409       | 900101     | Ez az átvitel nem engedélyezett, mert az eredeti {0} átvitel folyamatban van         |
| BadRequest (Rossz kérdés)          | 400       | 900102     | Nem lehet feldolgozni az átadási kérelmet az {1} átvitelhez {0}         |
| InternalServerError | 500       | 900103     | Az átadási rendelés nem sikerült        |
| Ütközés      | 409       | 900104     | Az {0} átvitelt egy másik kérés feldolgozása folyamatban van         |
| Forbidden     | 403       | 900105     | Egy vagy több Azure-előfizetése felfüggesztett állapotban van. Ezek nem lesznek áttűnve az Azure-csomagra          |
| NotFound      | 404       | 900106     | Nem található frissítési kérelem      |
| BadRequest (Rossz kérdés)          | 400       | 900107     | Nem lehet feldolgozni az Azure-frissítést, mert az Azure-katalóguselem nem található          |
| Forbidden     | 403       | 900108     | Az Azure-frissítés nem feldolgozható, mivel az ügyfélnek nincsenek Azure-előfizetései.      |
| Ütközés      | 409       | 900109     | Ez a frissítés nem engedélyezett, mivel az eredeti {0} frissítés folyamatban van     |
| BadRequest (Rossz kérdés)          | 400       | 900110     | Nem lehet feldolgozni a frissítési kérelmet a befejezett frissítéshez {0}     |
| BadRequest (Rossz kérdés)          | 400       | 900111     | A megadott frissítési azonosító nem tartozik az {0} ügyfélhez. Az ügyfél le van leképezve a frissítési azonosítóra {1}     |
| Ütközés      | 409       | 900112     | Ez a vásárlás nem engedélyezett, mert a frissítési {0} kérelem függő állapotban van        |
| Ütközés      | 409       | 900113     | Ez a vásárlás nem engedélyezett, mert a frissítési {0} kérelem folyamatban van       |
| Ütközés      | 409       | 900114     | Ez a vásárlás nem engedélyezett, mert a frissítési kérelem {0} meghiúsult         |
| Forbidden     | 403       | 900115     | Az Azure-csomag nem áthelyezhető felfüggesztett állapotba, mivel egy vagy több Azure-előfizetés aktív állapotban van        |
| BadRequest (Rossz kérdés)          | 400       | 900116     | Nem hozható létre rendelés. A sandbox-fiókokban legfeljebb hány Azure-csomag lehet létrehozni      |
| BadRequest (Rossz kérdés)          | 400       | 900117     | Lejárt a {0} -day lemondási időkeret. Nem tudjuk megszüntetni a vásárlást               |
| BadRequest (Rossz kérdés)          | 400       | 900118     | Érvénytelen ügyfélazonosító         |
| Forbidden     | 403       | 900119     | Nem lehet feldolgozni az Azure-frissítést Azure Partner Shared Services         |
| Forbidden     | 403       | 900120     | Nem lehet feldolgozni az Azure-frissítést      |
| Forbidden     | 403       | 900121     | A rendelés feldolgozása nem sikerült a kreditkorlát hiánya miatt. További segítségért forduljon ucmwrcsp@microsoft.com a kapcsolatfelvételhez        |
| NotFound      | 404       | 900122     | Az Advisor-ajánlat nem található     |
| Forbidden     | 403       | 900123     | Microsoft Partnerszerződés közvetett viszonteladó nem fogadta el         |
| Forbidden     | 403       | 900124     | A vállalat nem fogadta el a Microsoft Partnerszerződés (MPA). A CSP-fiók globális rendszergazdának el kell fogadnia az MPA-t a teljes tranzakciós képesség folytatásához. Keresse meg a globális rendszergazdát, és írja alá az MPA-t az irányítópulton a {0} {1} teljes tranzakciós képességek folytatásához          |
| BadRequest (Rossz kérdés)          | 400       | 900125     | Az Advisor-partner adatai nem találhatók a kérelem kontextusában     |
| BadRequest (Rossz kérdés)          | 400       | 900126     | Nem lehet az enumot elemezni: {0} További információért látogasson el ide: {1}       |
| BadRequest (Rossz kérdés)          | 400       | 900127     | Ez a művelet nem támogatott ebben a környezetben        |
| BadRequest (Rossz kérdés)          | 400       | 900128     | Forgalmi díjas számlázási csomaggal vásárolt SaaS-előfizetéshez Azure-csomag szükséges                 |
| BadRequest (Rossz kérdés)          | 400       | 900129     | A megadott Azure-csomagazonosító nem található, vagy nincsenek benne aktív Azure-előfizetések. A forgalmi díjas számlázási csomaggal vásárolt SaaS-termékhez aktív előfizetés(ök) szükséges         |
| Forbidden     | 403       | 900130     | Egy vagy több Azure-előfizetés nemrég lett megvásárolva, ezek az előfizetések jelenleg nem válthatók át. Próbálkozzon újra később               |
| BadRequest (Rossz kérdés)          | 400       | 900131     | Ez az átadási kérelem nem indítható el, mert az ügyfél örökölt Azure-előfizetéssel rendelkezik              |
| BadRequest (Rossz kérdés)          | 400       | 900132     | Ez az átadási kérelem nem indítható el, mert az Azure-csomag nem aktív. Engedélyezze az Azure-tervet     |
| BadRequest (Rossz kérdés)          | 400       | 900133     | Ez az átadási kérelem nem indítható el, mert az ügyfél nem vásárolt Azure-csomagokat       |
| BadRequest (Rossz kérdés)          | 400       | 900134     | Ez az átadási kérelem nem indítható el, mert az Azure-csomag nem cserélhető     |
| InternalServerError | 500       | 900135     | Az átadási kérelem kezdeményezése sikertelen volt. Próbálkozzon újra később         |
| BadRequest (Rossz kérdés)          | 400       | 900136     | Az átvitel nem kezdeményezhető, mert a forráspartner e-mail-címe/tartományának adatai hiányoznak a kérelemből            |
| Forbidden     | 403       | 900137     | Nem lehet partnerként létrehozni az átvitelt: {0} nincs engedélyezve ehhez a funkcióhoz      |
| Forbidden     | 403       | 900138     | Nem lehet partnerként létrehozni az átvitelt: {0} az országos felhő nem {1} támogatott         |
| Forbidden     | 403       | 900139     | Az átadási kérelem nem fogadható el. Kérje meg a partnert, hogy Hozzon létre átadást Azure-előfizetés(ek) nélkül        |
| NotFound      | 404       | 900140     | Nem sikerült le Azure Active Directory bérlőazonosítóval és forrás-kiépítési {0} azonosítóval{1}     |
| BadRequest (Rossz kérdés)          | 400       | 900141     | Ez a művelet nem támogatott         |
| BadRequest (Rossz kérdés)          | 400       | 900142     | A katalóguselem azonosítója nem található      |
| BadRequest (Rossz kérdés)          | 400       | 900143     | A kérés nem tudta lekérni az összes rendelkezésre állási adatokat a következő termékazonosítóval: {0} , skuId: {1} azonosítóval: {3}     |
| BadRequest (Rossz kérdés)          | 400       | 900144     | A kiépítési termékváltozat azonosítója nincs jelen               |
| BadRequest (Rossz kérdés)          | 400       | 900145     | A számlázási tulajdonjog átadására vonatkozó kérelem nem teljesíthető, mert az Azure Reservations nem lesz átveve az előfizetésekkel. Törölje a kiválasztott előfizetésekkel társított Azure-foglalásokat, majd próbálkozzon újra.         |
| BadRequest (Rossz kérdés)          | 400       | 900146     | A számlázási tulajdonjog átadására vonatkozó kérelem nem teljesíthető, mert a harmadik féltől származó Marketplace-termékek nem átvitele előfizetésekkel. Távolítsa el a külső Marketplace-termékeket a kijelölésből, majd próbálkozzon újra.       |
| BadRequest (Rossz kérdés)          | 400       | 900147     | Adjon meg egy érvényes tartományt, amely az aktuális partnerhez van társítva       |
| BadRequest (Rossz kérdés)          | 400       | 900148     | Az átvitel létrehozása nem sikerült, mert a forráspartner adatai megegyeztek a kérelmező partnerrel                |
| Forbidden     | 403       | 900149     | {0} A program állapota nem aktív.       |
| Forbidden     | 403       | 900150     | A megadott szerepkör nem rendelkezik a kért művelet végrehajtásához szükséges jogosultságokkal      |
| InternalServerError | 500       | 900192     | Hiba történt. Próbálkozzon újra egy kis idő után.       |
| BadRequest (Rossz kérdés)          | 400       | 900203     | CatalogItemId: {0} igazolás elfogadását igényli.        |
| BadRequest (Rossz kérdés)          | 400       | 600049     | A szervezet regisztrációs azonosítójának adatai hiányoznak. Ez a hiba akkor jelenik meg, ha az ügyfél vállalata/szervezete a következő országokban található: Uzbekistan(AZ), Uzbekistan(AZ), Amelyet(BY), To(HU), Mirgyzstan(KZ), Kyrgyzstan(KG), Kyrgyzstan(KG), Torgyzsán (MD), Tajikistan(TJ), Uzbekistan(UZ), Uzbekistan(UA), de organizationRegistrationNumber nem ad át.      |
| BadRequest (Rossz kérdés)          | 400       | 600050     | A szervezet regisztrációs azonosítójának adatai érvénytelenek, és formátumának a következőnek kell lennie: `{0}` . Ez a hiba akkor jelenik meg, ha az átadott organizationRegistrationNumber nem érvényes az ügyfél vállalatának országára. {0} A a hiba várt reguláriskifejezés-formátumát fogja kapni. Például: A szervezet regisztrációs azonosítójának adatai érvénytelenek, és a következő formátumúnak kell lennie: `^(\\d{7}|\\d{10})$`          |
| BadRequest (Rossz kérdés)          | 400       | 600051     | Az ügyfél telefonszáma hiányzik. Ez a hiba akkor jelenik meg, ha az ügyfél vállalata/szervezete a következő országokban található: Uzbekistan(UZ), Uz(AZ), Microsoft(BY), To(HU), Mirgyzstan(KZ), Kyrgyzstan(KG), Torgyzstan(KG), Oroszország(RU), Tajikistan(TJ), Uzbekistan(UZ), Uzbekistan(UA), de billingProfile.defaultAddress.phoneNumber nem ad át.       |
| BadRequest (Rossz kérdés)          | 400       | 600002     | A szervezeti regisztrációs azonosító értéke nem támogatott. Ez a hiba akkor jelenik meg, ha az ügyfél vállalata/szervezete nem a következő országokban található: Uzbekistan(AZ), Uzbekistan(AZ), To(BY), To(HU), Torgyzstan(KZ), Kyrgyzstan(KG), Torgyzstan (KG), Oroszország(RU), Tajikistan(TJ), Uzbekistan(UZ), Uzbekistan(UA), Valamint a OrganizationRegistrationNumber megadásával.       |
