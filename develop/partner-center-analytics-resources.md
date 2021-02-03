---
title: Partnerközpont – elemzések
description: A partner Center Analytics nyilvános API dokumentációja.
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4b14ee929f3020079f409be8817e077673d3219f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767772"
---
# <a name="partner-center-analytics---resources"></a>Partnerközpont-elemzések – forrásanyagok

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Az elemzési API lehetővé teszi, hogy programozott módon hozzáférjen a felhasználói élményben bemutatott adatszolgáltatásokhoz.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ezek a forgatókönyvek csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatják.

## <a name="csp-program-azure-usage-analytics"></a>CSP program: Azure-használati elemzés

A következő forgatókönyv bemutatja, hogyan használhatja az Analytics API-t az összes partner Center Azure-használati elemzési információ lekéréséhez.

- [Az összes Azure-beli használatelemzési adat lekérése](get-all-azure-usage-analytics.md)

Ez a forgatókönyv az [Azure-használati](#azure-usage-resource) erőforrások gyűjteményében lévő elemzési adatokat adja vissza.

## <a name="azure-usage-resource"></a>Azure-használati erőforrás

Az Azure-használat összes analitikai adatait jelöli.

| Tulajdonság | Típus | Leírás |
|----------|------|-------------|
| CustomerTenantId | sztring | Az ügyfél bérlői azonosítója. |
| Customername ( | sztring | Az ügyfél neve. |
| subscriptionId | sztring | Az előfizetés azonosítója. |
| subscriptionName | sztring | Az előfizetés neve. |
| usageDate | sztring | A használat dátuma. |
| resourceLocation | sztring | A Nyugat-Európa adatközpontjának helye, például:. |
| meterCategory | sztring | A mérőszám kategóriája, adatkezelés, például. |
| Fogyasztásmérő alkategóriája | sztring | A fogyasztásmérő alkategóriája, például a redundáns földrajzi érték. |
| meterUnit | sztring | A mérő egység, például gigabájt vagy óra. |
| reservationOrderId | sztring | Egy Azure-beli virtuális gép fenntartott példányának foglalási sorrendje. |
| reservationId | sztring | Fenntartott példányok egy adott RI-sorrendben. |
| serviceType | sztring | Megadja a virtuális gép típusát. Például Standard_E4s_v3. |
| quantity | hosszú | A fogyasztásmérő egységben használt számokat jelzi. |

## <a name="csp-program-indirect-resellers-analytics"></a>CSP-program: közvetett viszonteladói elemzés

A következő forgatókönyv bemutatja, hogyan használhatja az Analytics API-t az összes partner Center közvetett viszonteladó elemzési információjának lekéréséhez.

- [Az összes közvetett viszonteladó elemzési adatainak lekérése](get-all-indirect-resellers-analytics.md)

Ez a forgatókönyv a [közvetett viszonteladói](#indirect-resellers-resource) erőforrások gyűjteményében lévő elemzési adatokat adja vissza.

## <a name="indirect-resellers-resource"></a>Közvetett viszonteladók erőforrásai

A közvetett viszonteladók összes analitikai adatmennyiségét jelöli.

| Tulajdonság | Típus | Leírás |
|----------|------|-------------|
| partnerTenantId | sztring | Annak a partnernek a bérlői azonosítója, amelyhez közvetett viszonteladói adatmennyiséget kíván beolvasni. |
| id | sztring | Közvetett viszonteladó azonosítója. |
| name | sztring | Annak a partnernek a neve, amelyhez közvetett viszonteladói adatmennyiséget kíván beolvasni. |
| piac | sztring | Annak a partnernek a piaca, amelyhez közvetett viszonteladói adatmennyiséget kíván beolvasni. |
| firstSubscriptionCreationDate | karakterlánc UTC-dátum időformátuma | Az első előfizetés létrehozásának dátuma, amely alapján a közvetett viszonteladói adatok lekérését kéri. |
| latestSubscriptionCreationDate | karakterlánc UTC-dátum időformátuma | A legújabb előfizetés létrehozásának dátuma. |
| firstSubscriptionEndDate | karakterlánc UTC-dátum időformátuma | Az előfizetés első befejezése után. |
| latestSubscriptionEndDate | karakterlánc UTC-dátum időformátuma | Az előfizetés befejezésének utolsó dátuma. |
| firstSubscriptionSuspendedDate | karakterlánc UTC-dátum időformátuma | Az előfizetés felfüggesztésének első időpontja. |
| latestSubscriptionSuspendedDate | karakterlánc UTC-dátum időformátuma | Az előfizetés felfüggesztésének utolsó dátuma. |
| firstSubscriptionDeprovisionedDate | karakterlánc UTC-dátum időformátuma | Az előfizetés első kiépítésekor. |
| latestSubscriptionDeprovisionedDate | karakterlánc UTC-dátum időformátuma | Az előfizetés megszűnésének utolsó dátuma. |
| subscriptionCount | double | Az összes hozzáadott értékhez tartozó előfizetés száma |
| licenseCount | double | Az összes hozzáadott értékhez tartozó licencek száma |
| indirectResellerCount | double | Közvetett viszonteladók száma |

## <a name="csp-program-subscription-analytics"></a>CSP-program: előfizetés-elemzés

Az alábbi forgatókönyvek azt mutatják be, hogyan használhatja az Analytics API-t az összes partner Center-előfizetési elemzési adat beolvasására, a keresési lekérdezéssel való szűrésére, vagy a dátumok vagy kifejezések alapján történő csoportosítására.

- [Az összes előfizetés elemzési adatainak lekérése](get-all-subscription-analytics.md)
- [Előfizetés keresési lekérdezés szerint szűrt elemzési adatainak lekérése](get-subscription-analytics-by-search-query.md)
- [Előfizetés dátumok vagy feltételek szerint csoportosított elemzési adatainak lekérése](get-subscription-analytics-grouped-by-dates-or-terms.md)

Az összes ilyen forgatókönyv az elemzési adatokat az [előfizetési](#subscription-resource) erőforrások gyűjteményében adja vissza.

## <a name="subscription-resource"></a>Előfizetési erőforrás

Az előfizetéshez tartozó összes analitikai adatmennyiséget jelöli.

|         Tulajdonság          |              Típus              |                                                                      Leírás                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     customerTenantId      |             sztring             |                                              Egy GUID-formázott karakterlánc, amely azonosítja az ügyfél bérlőjét.                                              |
|       Customername (        |             sztring             |                                                               Az ügyfél neve.                                                                |
|      customerMarket       |             sztring             |                                                 Az az ország/régió, amelyben az ügyfél üzleti tevékenységet végez.                                                 |
|            id             |             sztring             |                                                              Az előfizetés azonosítója.                                                              |
|          status           |             sztring             |                                          Az előfizetés állapota: "ACTIVE", "FELFÜGGESZTett" vagy "kiépített".                                           |
|        productName        |             sztring             |                                                                A termék neve.                                                                |
|     Ügynökparamétert      |             sztring             |       Az előfizetés típusa. **Megjegyzés**: Ez a mező megkülönbözteti a kis-és nagybetűket. A támogatott értékek a következők: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".       |
|     autoRenewEnabled      |            boolean             |                                         Egy érték, amely azt jelzi, hogy az előfizetés automatikusan megújul-e.                                          |
|         partnerId         |             sztring             | Az MPN-azonosító. Közvetlen viszonteladó esetén ez a paraméter lesz a partner MPN-azonosítója. Közvetett viszonteladó esetén ez a paraméter a közvetett viszonteladó MPN-azonosítója lesz. |
|       friendlyName        |             sztring             |                                                             Az előfizetés neve.                                                              |
|        partnerName        |             sztring             |                                              Annak a partnernek a neve, akivel az előfizetést megvásárolták                                               |
|       providerName        |             sztring             |            Ha az előfizetési tranzakció a közvetett viszonteladóhoz kapcsolódik, a szolgáltató neve az a közvetett szolgáltató, aki megvásárolta az előfizetést.             |
|    effectiveStartDate     | karakterlánc UTC-dátum időformátuma |                                                           Az előfizetés megkezdésének dátuma.                                                            |
|     commitmentEndDate     | karakterlánc UTC-dátum időformátuma |                                                            Az előfizetés befejezésének dátuma.                                                             |
|    currentStateEndDate    | karakterlánc UTC-dátum időformátuma |                                           Az előfizetés aktuális állapotának változási dátuma.                                            |
| trialToPaidConversionDate | karakterlánc UTC-dátum időformátuma |                                 Az előfizetés próbaverzióról fizetettre való konvertálása dátuma. Az alapértelmezett érték null.                                 |
|      trialStartDate       | karakterlánc UTC-dátum időformátuma |                                Az előfizetés Próbaidőszakának elindításának dátuma. Az alapértelmezett érték null.                                 |
|       trialEndDate        | karakterlánc UTC-dátum időformátuma |                                  Az előfizetés Próbaidőszakának lejárta. Az alapértelmezett érték null.                                  |
|       lastUsageDate       | karakterlánc UTC-dátum időformátuma |                                        Az előfizetés legutóbbi használatának dátuma. Az alapértelmezett érték null.                                        |
|     deprovisionedDate     | karakterlánc UTC-dátum időformátuma |                                      Az előfizetés megszüntetésének dátuma. Az alapértelmezett érték null.                                      |
|      lastRenewalDate      | karakterlánc UTC-dátum időformátuma |                                       Az előfizetés utolsó megújításának dátuma az alapértelmezett érték null.                                       |
|       licenseCount        |             szám             |                                                             A licencek teljes száma.                                                              |
|     subscriptionCount     |             szám             |                        Az előfizetések száma. Megjegyzés: ez az érték csak az összesítési lekérdezés válaszában jelenik meg.                         |

## <a name="search-analytics"></a>Keresési elemzés

> [!NOTE]
> A keresési elemzés beszerzéséhez nem szükséges a CSP-program tagsága.

A következő forgatókönyv bemutatja, hogyan használhatja az Analytics API-t az összes partner Center keresési elemzési információ lekéréséhez.

- [Az összes keresés elemzési adatainak lekérése](get-all-search-analytics.md)

Ez a forgatókönyv az elemzési információkat a [keresési](#search-resource) erőforrások gyűjteményében adja vissza.

## <a name="search-resource"></a>Erőforrás keresése

A keresés összes analitikai adatmennyiségét jelöli.

| Tulajdonság | Típus | Leírás |
|----------|------|-------------|
| companyName | sztring | A számlázási vállalat neve. |
| contactButtonClicked | Logikai | Azt jelzi, hogy a Contact (kapcsolattartó) gombra kattintott-e. |
| keywordCountry | sztring | A keresésben megadott ország. |
| detailsViewed | Logikai | Azt jelzi, hogy megtörténtek-e a keresési adatok megtekintése. |
| keywordIndustryFocus | sztring | Az iparágban való keresés, például az egészségügy területén. |
| mpnId | sztring | A Microsoft Partner Network (MPN) azonosítója. Közvetlen viszonteladó esetén ez a paraméter lesz a partner MPN-azonosítója. Közvetett viszonteladó esetén ez a paraméter a közvetett viszonteladó MPN-azonosítója lesz. |
| partnerMarket | sztring | Területi beállítás, amelyben a partner üzleti tevékenységet végez. |
| keywordProduct | sztring | A keresésben megadott termék. |
| referralSubmitted | Logikai | Azt jelzi, hogy elküldtek-e egy hivatkozást. |
| searchDate | karakterlánc UTC-dátum időformátuma | A keresési lekérdezés bekövetkezésének dátuma. |
| keywordSearchText | sztring | A keresésben megadott szöveg |
| searchResultPageViews | hosszú | Az a szám, ahányszor a partner megérkezett a keresési eredményben. Egy válasz része csak összesítéssel.
| contactClicks | hosszú | Az a szám, ahányszor a névjegy gombra kattintott. Egy válasz része csak összesítéssel.
| referralCount | hosszú | A keresésből generált átirányítások száma. Egy válasz része csak összesítéssel.
| profileViews | hosszú | A partner profil megtekintésének száma. Egy válasz része csak összesítéssel.

## <a name="referrals-analytics"></a>Átirányítási elemzés

> [!NOTE]
> A CSP-program tagsága nem szükséges az átirányítási elemzések beszerzéséhez.

A következő forgatókönyv bemutatja, hogyan használhatja az Analytics API-t az összes partner Center-hivatkozás elemzési információjának lekéréséhez.

- [Az összes javaslat elemzési adatainak lekérése](get-all-referrals-analytics.md)

Ez a forgatókönyv az elemzési adatokat az [átirányítási](#referrals-resource) erőforrások gyűjteményében adja vissza.

> [!NOTE]
> Az átirányítási elemzés nem érhető el a 21Vianet által működtetett partneri Központ számára.

## <a name="referrals-resource"></a>Átirányítási erőforrások

Az átirányításhoz tartozó összes analitikai adatmennyiséget jelöli.

| Tulajdonság | Típus | Leírás |
|----------|------|-------------|
| id | sztring | Az ügyfél bérlői azonosítója.  |
| status | sztring | Azt jelzi, hogy az átirányítást egy ügyfélhez vezette-e.  |
| customerMarket | sztring | Az az ország/régió, amelyben az ügyfél üzleti tevékenységet végez. |
| Customername ( | sztring | Az ügyfél neve. |
| customerOrgSize | sztring | Az ügyfél szervezetében dolgozó alkalmazottak számát jelző tartomány. Például: "10to50employees". |
| acceptedDate | karakterlánc UTC-dátum időformátuma | Az átirányítás elfogadásának dátuma. |
| acknowledgedDate | karakterlánc UTC-dátum időformátuma | Az átirányítás visszaigazolásának dátuma. |
| archivedDate | karakterlánc UTC-dátum időformátuma | Az átirányítás archiválásának dátuma. |
| declinedDate | karakterlánc UTC-dátum időformátuma | Az átirányítás elutasításának dátuma. |
| expiredDate | karakterlánc UTC-dátum időformátuma | Az átirányítás érvényességének dátuma. |
| lostDate | karakterlánc UTC-dátum időformátuma | Az átirányítás megszakadásának dátuma. |
| missedDate | karakterlánc UTC-dátum időformátuma | Az átirányítás kihagyott dátuma. |
| createdDate | karakterlánc UTC-dátum időformátuma | Az átirányítás létrehozásának dátuma. |
| skippedDate | karakterlánc UTC-dátum időformátuma | Az átirányítás kihagyott dátuma. |
| wonDate | karakterlánc UTC-dátum időformátuma | Az átirányítás megnyerésének dátuma. |
| partnerMarket | sztring |  Az ország/régió, amelyben a partner üzleti tevékenységet végez. |
