---
title: Partnerközpont – elemzések
description: Partnerközpont Analytics nyilvános API dokumentációja.
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9028d5e2bdeb2637e35133b2c6dda739e0024ccc2838368a5276b1482af78d7f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997838"
---
# <a name="partner-center-analytics---resources"></a>Partnerközpont-elemzések – forrásanyagok

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az Analytics API lehetővé teszi, hogy programozott módon hozzáférjen a Felhasználói élményben megjelenő adatokhoz.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ezek a forgatókönyvek csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatják.

## <a name="csp-program-azure-usage-analytics"></a>CSP-program: Azure-használatelemzés

A következő forgatókönyv bemutatja, hogyan használhatja az Analytics API-t az azure Partnerközpont összes adatának lekérésére.

- [Az összes Azure-beli használatelemzési adat lekérése](get-all-azure-usage-analytics.md)

Ez a forgatókönyv azure-beli használati erőforrások [gyűjteményében](#azure-usage-resource) adja vissza az elemzési adatokat.

## <a name="azure-usage-resource"></a>Azure használati erőforrás

Az Azure-használat összes elemzési adatát jelöli.

| Tulajdonság | Típus | Description |
|----------|------|-------------|
| CustomerTenantId | sztring | Az ügyfél bérlőazonosítója. |
| customerName (ügyfél neve) | sztring | Az ügyfél neve. |
| subscriptionId | sztring | Az előfizetés azonosítója. |
| subscriptionName | sztring | Az előfizetés neve. |
| usageDate | sztring | A használat dátuma. |
| resourceLocation | sztring | Az adatközpont helye, például Nyugat-Európa. |
| meterCategory | sztring | A fogyasztásmérő kategóriája, például adatkezelés. |
| meterSubcategory | sztring | A fogyasztásmérő alkategóriája, például georedundáns. |
| meterUnit | sztring | A fogyasztásmérő egység, például gigabájt vagy óra. |
| reservationOrderId | sztring | Egy Azure-beli virtuális gép fenntartott példányának foglalási rendelése. |
| reservationId | sztring | Fenntartott példányok egy adott fenntartott példány megrendelése alatt. |
| serviceType (szolgáltatástípus) | sztring | A virtuális gép típusát jelzi. Például: Standard_E4s_v3. |
| quantity | hosszú | A fogyasztásmérő egységben használt számokat jelzi. |

## <a name="csp-program-indirect-resellers-analytics"></a>CSP-program: közvetett viszonteladók elemzése

A következő forgatókönyv bemutatja, hogyan használhatja az Analytics API-t az összes közvetett Partnerközpont viszonteladó elemzési információinak lekérésére.

- [Az összes közvetett viszonteladó elemzési adatainak lekérése](get-all-indirect-resellers-analytics.md)

Ez a forgatókönyv közvetett viszonteladói erőforrások gyűjteményében adja vissza az [elemzési adatokat.](#indirect-resellers-resource)

## <a name="indirect-resellers-resource"></a>Közvetett viszonteladói erőforrás

A közvetett viszonteladók összes elemzési adatát jelöli.

| Tulajdonság | Típus | Description |
|----------|------|-------------|
| partnerTenantId | sztring | Annak a partnernek a bérlőazonosítója, amelyhez közvetett viszonteladói adatokat szeretne lekérni. |
| id | sztring | Közvetett viszonteladó azonosítója. |
| name | sztring | Annak a partnernek a neve, amelyhez közvetett viszonteladói adatokat szeretne lekérni. |
| piac | sztring | Annak a partnernek a piaca, amelyhez közvetett viszonteladói adatokat szeretne lekérni. |
| firstSubscriptionCreationDate (firstSubscriptionCreationDate) | sztring UTC dátum-idő formátumban | Annak az első előfizetésnek a létrehozási dátuma, amely alapján közvetett viszonteladói adatokat szeretne lekérni. |
| latestSubscriptionCreationDate | sztring UTC dátum-idő formátumban | A legújabb előfizetés létrehozásának dátuma. |
| firstSubscriptionEndDate | sztring UTC dátum-idő formátumban | Az első alkalommal, amikor egy előfizetés véget ért. |
| latestSubscriptionEndDate | sztring UTC dátum-idő formátumban | Az előfizetések végének legkésőbbi dátuma. |
| firstSubscriptionSuspendedDate | sztring UTC dátum-idő formátumban | Bármely előfizetés első felfüggesztésekor. |
| latestSubscriptionSuspendedDate | sztring UTC dátum-idő formátumban | Az előfizetés felfüggesztésének utolsó dátuma. |
| firstSubscriptionDeprovisionedDate | sztring UTC dátum-idő formátumban | Az előfizetések első megszüntetésekor. |
| latestSubscriptionDeprovisionedDate | sztring UTC dátum-idő formátumban | Bármely előfizetés megszüntetésének legkésőbbi dátuma. |
| subscriptionCount (előfizetés száma) | double | Előfizetések száma az összes hozzáadott értékkel felkelt viszonteladónál |
| licenseCount (licencszám) | double | Az összes hozzáadott értékkel rendelkező viszonteladó licencszáma |
| indirectResellerCount | double | Közvetett viszonteladók száma |

## <a name="csp-program-subscription-analytics"></a>CSP-program: előfizetés-elemzés

A következő forgatókönyvek azt mutatják be, hogyan használhatja az Analytics API-t az összes Partnerközpont-előfizetés elemzési információinak lekérésére, keresési lekérdezéssel való szűrésére, illetve dátumok vagy kifejezések alapján való csoportosítására.

- [Az összes előfizetés elemzési adatainak lekérése](get-all-subscription-analytics.md)
- [Előfizetés keresési lekérdezés szerint szűrt elemzési adatainak lekérése](get-subscription-analytics-by-search-query.md)
- [Előfizetés dátumok vagy feltételek szerint csoportosított elemzési adatainak lekérése](get-subscription-analytics-grouped-by-dates-or-terms.md)

Az összes ilyen forgatókönyv az előfizetési [](#subscription-resource) erőforrások gyűjteményében adja vissza az elemzési adatokat.

## <a name="subscription-resource"></a>Előfizetési erőforrás

Egy előfizetés összes elemzési adatát jelöli.

|         Tulajdonság          |              Típus              |                                                                      Description                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     customerTenantId (customerTenantId)      |             sztring             |                                              Egy GUID-formátumú sztring, amely azonosítja az ügyfélbérlőt.                                              |
|       customerName (ügyfél neve)        |             sztring             |                                                               Az ügyfél neve.                                                                |
|      customerMarket       |             sztring             |                                                 Az az ország/régió, ahol az ügyfél üzleti tevékenységhez tartozik.                                                 |
|            id             |             sztring             |                                                              Az előfizetés azonosítója.                                                              |
|          status           |             sztring             |                                          Az előfizetés állapota: "ACTIVE", "SUSPENDED" vagy "DEPROVISIONED".                                           |
|        Productname        |             sztring             |                                                                A termék neve.                                                                |
|     subscriptionType (előfizetés típusa)      |             sztring             |       Az előfizetés típusa. **Megjegyzés:** Ez a mező megkülönbözteti a kis- és nagybetűket. Támogatott értékek: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".       |
|     autoRenewEnabled      |            boolean             |                                         Egy érték, amely jelzi, hogy az előfizetés automatikusan megújul-e.                                          |
|         partnerazonosító         |             sztring             | Az Microsoft Partner Network (MPN) azonosítója. Közvetlen viszonteladó esetén ez a paraméter a partner MPN-azonosítója lesz. Közvetett viszonteladó esetén ez a paraméter a közvetett viszonteladó MPN-azonosítója lesz. |
|       friendlyName (rövid név)        |             sztring             |                                                             Az előfizetés neve.                                                              |
|        partnerName        |             sztring             |                                              Annak a partnernek a neve, aki számára az előfizetést megvásárolták                                               |
|       providerName (szolgáltató neve)        |             sztring             |            Ha az előfizetési tranzakció a közvetett viszonteladóra történik, a szolgáltató neve az a közvetett szolgáltató, aki megvásárolta az előfizetést.             |
|    effectiveStartDate     | sztring UTC dátum-idő formátumban |                                                           Az előfizetés kezdési dátuma.                                                            |
|     commitmentEndDate     | sztring UTC dátum-idő formátumban |                                                            Az előfizetés végének dátuma.                                                             |
|    currentStateEndDate    | sztring UTC dátum-idő formátumban |                                           Az előfizetés aktuális állapotának változásának dátuma.                                            |
| trialToPaidConversionDate (trialToPaidConversionDate) | sztring UTC dátum-idő formátumban |                                 Az a dátum, amikor az előfizetés próbaverzióról fizetősre vált. Az alapértelmezett érték a null.                                 |
|      trialStartDate       | sztring UTC dátum-idő formátumban |                                Az előfizetés próbaidőszakának elindulásának dátuma. Az alapértelmezett érték a null.                                 |
|       trialEndDate        | sztring UTC dátum-idő formátumban |                                  Az előfizetés próbaidőszakának végének dátuma. Az alapértelmezett érték a null.                                  |
|       lastUsageDate (lastUsageDate)       | sztring UTC dátum-idő formátumban |                                        Az előfizetés utolsó használt dátuma. Az alapértelmezett érték a null.                                        |
|     megszüntetésDate     | sztring UTC dátum-idő formátumban |                                      Az előfizetés megszüntetésének dátuma. Az alapértelmezett érték a null.                                      |
|      lastRenewalDate (lastRenewalDate)      | sztring UTC dátum-idő formátumban |                                       Az előfizetés utolsó megújításának dátuma. Az alapértelmezett érték a null.                                       |
|       licenseCount (licencszám)        |             szám             |                                                             A licencek teljes száma.                                                              |
|     subscriptionCount (előfizetés száma)     |             szám             |                        Az előfizetések száma. Megjegyzés: Ez az érték csak egy összesítési lekérdezés válaszában jelenik meg.                         |

## <a name="search-analytics"></a>Kereséselemzés

> [!NOTE]
> A CSP-programtagság nem szükséges a keresési elemzésekhez.

A következő forgatókönyv bemutatja, hogyan használhatja az Analytics API-t a keresési Partnerközpont adatok lekérésére.

- [Az összes keresés elemzési adatainak lekérése](get-all-search-analytics.md)

Ez a forgatókönyv keresési erőforrások [](#search-resource) gyűjteményében adja vissza az elemzési adatokat.

## <a name="search-resource"></a>Erőforrás keresése

Egy keresés összes elemzési adatát jelöli.

| Tulajdonság | Típus | Description |
|----------|------|-------------|
| companyName (vállalat neve) | sztring | A számlázási vállalat neve. |
| contactButtonClicked | Logikai | Jelzi, hogy a kapcsolat gombra kattintott-e. |
| keywordCountry (országszám) | sztring | A keresésben megadott ország. |
| detailsViewed (részletekmegtekintve) | Logikai | Jelzi, hogy megtekintett-e keresési adatokat. |
| keywordIndustryFocus | sztring | Az iparág, amelybe például az egészségügyben kell keresni. |
| mpnId | sztring | Az Microsoft Partner Network (MPN) azonosítója. Közvetlen viszonteladó esetén ez a paraméter a partner MPN-azonosítója lesz. Közvetett viszonteladó esetén ez a paraméter a közvetett viszonteladó MPN-azonosítója lesz. |
| partnerMarket | sztring | Az a hely, ahol a partner üzleti tevékenységekkel fog végezni. |
| kulcsszóTermék | sztring | A keresésben megadott termék. |
| referralSubmitted | Logikai | Jelzi, hogy a rendszer elküldt-e egy ajánlást. |
| searchDate (Keresésidátum) | sztring UTC dátum- és időformátumban | A keresési lekérdezés beesésének dátuma. |
| kulcsszóKeresésSzöveg | sztring | A keresésben megadott szöveg. |
| searchResultPageViews | hosszú | Az a szám, a hányszor került fel a partner a keresési eredménybe. Egy válasz egy része csak összesítés esetén.
| contactClicks | hosszú | A kapcsolattartási gombra való kattintások száma. Egy válasz egy része csak összesítés esetén.
| referralCount | hosszú | A keresésből generált hivatkozások száma. Egy válasz egy része csak összesítés esetén.
| profileViews | hosszú | A partnerprofil megtekintésének száma. Egy válasz egy része csak összesítés esetén.

## <a name="referrals-analytics"></a>Ajánlóelemzés

> [!NOTE]
> A CSP-programtagság nem szükséges a hivatkozások elemzéséhez.

A következő forgatókönyv bemutatja, hogyan használhatja az Analytics API-t az összes Partnerközpont elemzési információ lekérésére.

- [Az összes javaslat elemzési adatainak lekérése](get-all-referrals-analytics.md)

Ez a forgatókönyv a hivatkozási erőforrások gyűjteményében adja vissza az elemzési [adatokat.](#referrals-resource)

> [!NOTE]
> A 21Vianet által üzemeltetett Partnerközpont nem érhetők el a hivatkozások elemzései.

## <a name="referrals-resource"></a>Hivatkozási erőforrás

Egy hivatkozás összes elemzési adatát jelöli.

| Tulajdonság | Típus | Description |
|----------|------|-------------|
| id | sztring | Az ügyfél bérlőazonosítója.  |
| status | sztring | Jelzi, hogy a hivatkozás egy ügyfélhez vezetett-e.  |
| customerMarket (customerMarket) | sztring | Az az ország/régió, ahol az ügyfél üzleti tevékenységhez tartozik. |
| customerName (ügyfél neve) | sztring | Az ügyfél neve. |
| customerOrgSize | sztring | Az ügyfél szervezetében dolgozók számát jelző tartomány. Például: "10to50employees". |
| acceptedDate (elfogadvadátum) | sztring UTC dátum- és időformátumban | A hivatkozás elfogadási dátuma. |
| acknowledgedDate (nyugtázásdátum) | sztring UTC dátum- és időformátumban | A hivatkozás nyugtázásának dátuma. |
| archivedDate (archiváltdátum) | sztring UTC dátum- és időformátumban | A hivatkozás archiválásának dátuma. |
| declinedDate (elutasítottddátum) | sztring UTC dátum- és időformátumban | A hivatkozás elutasításának dátuma. |
| expiredDate (lejártdátum) | sztring UTC dátum- és időformátumban | A hivatkozás lejáratának dátuma. |
| LostDate (Elveszettdátum) | sztring UTC dátum- és időformátumban | A hivatkozás elveszett dátuma. |
| missedDate (kihagyottdátum) | sztring UTC dátum- és időformátumban | A hivatkozás kihagyásának dátuma. |
| createdDate (Létrehozásidátum) | sztring UTC dátum- és időformátumban | A hivatkozás létrehozási dátuma. |
| skippedDate (kihagyottdátum) | sztring UTC dátum- és időformátumban | A hivatkozás kihagyásának dátuma. |
| wonDate (wonDate) | sztring UTC dátum- és időformátumban | A hivatkozás megnyert dátuma. |
| partnerMarket | sztring |  Az az ország/régió, ahol a partner üzleti tevékenységhez tartozik. |
