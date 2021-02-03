---
title: Számlázási erőforrások
description: A partner Center API-kon keresztül több számlával kapcsolatos erőforrás érhető el. Ezek az erőforrások a számla és a tétel részleteivel kapcsolatosak.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd2caefe4ae18c81a31083d084f1e87da1288dd9
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767811"
---
# <a name="invoice-resources"></a>Számlázási erőforrások

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A következő számlával kapcsolatos erőforrások a partner Center API-kon keresztül érhetők el.

## <a name="invoice"></a>Számla

| Tulajdonság | Típus | Leírás |
| -------- | ---- | ----------- |
| id | sztring | A számla azonosítója. |
| invoiceDate | karakterlánc UTC dátum-idő formátumban | A számla létrehozásának dátuma. |
| billingPeriodStartDate | karakterlánc UTC dátum-idő formátumban | Számlázási időszak kezdő dátuma (UTC). |
| billingPeriodEndDate | karakterlánc UTC dátum-idő formátumban   | A számlázási időszak záró dátuma (UTC). |
| totalCharges | szám | A teljes díj. A tranzakciók és az egyéb módosítások díját is tartalmazza.     |
| paidAmount | szám  | A partner által fizetett összeg. Negatív, ha fizetés érkezett.  |
| currencyCode | sztring  | Egy kód, amely az összes számlázási tételhez és összeghez használt pénznemet jelzi. |
| currencySymbol  | sztring | Az összes számlázási tételhez és összeghez használt pénznemszimbólum |
| pdfDownloadLink | sztring  | Hivatkozás a számla PDF formátumban való letöltéséhez. Ez a hivatkozás nem jelenik meg a keresési eredmények részeként, és csak akkor lesz feltöltve, ha a számlát azonosító alapján érik el. A hivatkozás automatikus érvényessége 30 percen belül lejár. |
| invoiceDetails  | [InvoiceDetail](#invoicedetail) objektumok tömbje  | A számla részletei.  |
| módosítások      | [számlafogadó](#invoice) -objektumok tömbje   | A számla módosításai.  |
| documentType    | sztring | A számla dokumentumtípus: "jóváírás", "számla". |
| amendsOf        | sztring | Annak a dokumentumnak a hivatkozási száma, amelynek a dokumentum a módosítása.  |
| invoiceType     | sztring  | A számla típusa: "ismétlődő", "One \_ Time".   |
| linkek           | [ResourceLinks](utility-resources.md#resourcelinks)  | Az erőforrás-hivatkozások.  |
| attribútumok      | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.  |

## <a name="invoicedetail"></a>InvoiceDetail

A számla számlázott elemek gyűjteményét tartalmazza, és minden elemet egy InvoiceDetail-erőforrás képvisel.

| Tulajdonság            | Típus                                                           | Leírás                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | sztring                                                         | A számla részleteinek típusa: "None", "használati \_ sor \_ elemek", "számlázási \_ sorok \_ ". |
| billingProvider     | sztring                                                         | A számlázási szolgáltató: "None", "Office", "Azure" vagy "Azure-beli \_ \_ adatpiac".         |
| linkek               | [ResourceLinks](utility-resources.md#resourcelinks)           | Az erőforrás-hivatkozások.                                                               |
| attribútumok          | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

A számlán belül minden egyes díj egy InvoiceLineItem jelenik meg.

| Tulajdonság            | Típus                                                           | Leírás                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | sztring                                                         | A számlasorok-elem típusa: "None", "felhasználási \_ sor \_ elemek", "számlázási \_ sorok \_ ". |
| billingProvider     | sztring                                                         | A számlázási szolgáltató: "None", "Office", "Azure" vagy "Azure-beli \_ \_ adatpiac".            |
| attribútumok          | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

A számla egyenlegének és teljes díjainak összegzését ismerteti.

| Tulajdonság                 | Típus                                                           | Leírás                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount            | szám                                                         | A számla egyenlege. Ez a fizetetlen számlák teljes mennyisége. |
| currencyCode             | sztring                                                         | Egy kód, amely az egyenleg összegéhez használt pénznemet jelzi.       |
| currencySymbol           | sztring                                                         | A használt pénznem szimbóluma.                                             |
| accountingDate           | karakterlánc UTC dátum-idő formátumban                                 | Az egyenleg összegének utolsó frissítésének dátuma.                         |
| firstInvoiceCreationDate | karakterlánc UTC dátum-idő formátumban                                 | Az ügyfélhez tartozó első számla létrehozásának dátuma.              |
| lastPaymentDate          | karakterlánc UTC dátum-idő formátumban                                 | Az utolsó fizetés dátuma.                                         |
| lastPaymentAmount        | szám                                                         | Az utolsó fizetés mennyisége.                                       |
| latestInvoiceDate        | karakterlánc UTC dátum-idő formátumban                                 | Az ügyfélhez tartozó utolsó számla létrehozásának dátuma.               |
| Részletek                  | [InvoiceSummaryDetail](#invoicesummarydetail) objektumok tömbje | A számla összegzésének részletei.                                           |
| linkek                    | [ResourceLinks](utility-resources.md#resourcelinks)            | Az erőforrás-hivatkozások.                                                   |
| attribútumok               | [ResourceAttributes](utility-resources.md#resourceattributes)  | A metaadatok attribútumai.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

A számla típusának egyedi részletei (például ismétlődő, egyszeri) összegzését jelöli \_ .

| Tulajdonság            | Típus                                                           | Leírás                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | sztring                                                         | A számla típusa: "ismétlődő", "One \_ Time".                                       |
| összegzés             | [InvoiceSummary](#invoicesummary) objektum                       | A számla és a számla típusának összefoglalása.                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

A [InvoiceSummary](#invoicesummary) típusú gyűjteményt jelöli, amely a számla típusának egyedi részleteit tartalmazza pénznemben.

| Tulajdonság            | Típus                                                           | Leírás                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | [InvoiceSummary](#invoicesummary) objektumok tömbje             | A számla összefoglalása a számla típusú számlánként.                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem

A licencelt alapú előfizetések számlázási sorát jelöli.

| Tulajdonság                 | Típus                                                           | Leírás                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| összeg                   | sztring                                                         | Lekérdezi vagy beállítja a teljes mennyiséget. Teljes összeg = egység ára * mennyiség.  |
| attribútumok               | sztring                                                         | Az attribútumok beolvasása.                                                  |
| billingCycleType         | sztring                                                         | Lekérdezi vagy beállítja a számlázási ciklus típusát.                                  |
| billingProvider          | sztring                                                         | Lekéri a számlázási szolgáltatót.                                            |
| chargeEndDate            | karakterlánc UTC dátum-idő formátumban                                 | Lekérdezi vagy beállítja a díj befejezési dátumát.                             |
| chargeStartDate          | karakterlánc UTC dátum-idő formátumban                                 | Lekérdezi vagy beállítja a díj kezdő dátumát.                           |
| chargeType               | sztring                                                         | Lekérdezi vagy beállítja a díj típusát.                                      |
| currency                 | sztring                                                         | Lekérdezi vagy beállítja a tételhez használt pénznemet.                    |
| customerId               | sztring                                                         | Lekérdezi vagy beállítja az ügyfél egyedi azonosítóját a Microsoft számlázási platformon.  |
| Customername (             | karakterlánc UTC dátum-idő formátumban                                 | Lekérdezi vagy beállítja az ügyfél nevét.                                       |
| domainName               | sztring                                                         | Lekérdezi vagy beállítja a tartománynevet.                                             |
| durableOfferId           | sztring                                                         | Lekérdezi vagy beállítja a tartós ajánlat egyedi azonosítóját.                     |
| invoiceLineItemType      | sztring                                                         | Lekérdezi a számlasor-tétel típusát.                                   |
| mpnId                    | szám                                                         | Lekérdezi vagy beállítja az ehhez a sorhoz társított MPN-azonosítót. A közvetlen viszonteladók esetében ez a viszonteladó MPN-azonosítója. A közvetett viszonteladók esetében ez a hozzáadott érték (VAR) MPN-azonosítója.                                   |
| offerId                  | sztring                                                         | Lekérdezi vagy beállítja az ajánlat egyedi azonosítóját.                             |
| offerName                | sztring                                                         | Lekérdezi vagy beállítja az ajánlat nevét.                                          |
| Rendeléskód                  | sztring                                                         | Lekérdezi vagy beállítja a rendelés egyedi azonosítóját.                             |
| partnerId                | sztring                                                         | Lekérdezi vagy beállítja a partner Azure Active Directory-bérlői AZONOSÍTÓját.            |
| quantity                 | szám                                                         | Lekérdezi vagy beállítja az ehhez a sorhoz társított egységek számát.      |
| subscriptionDescription  | sztring                                                         | Lekérdezi vagy beállítja az előfizetés leírását.                            |
| subscriptionEndDate      | karakterlánc UTC dátum-idő formátumban                                 | Lekérdezi vagy beállítja azt a dátumot, amikor lejár az előfizetés.                      |
| subscriptionId           | sztring                                                         | Lekérdezi vagy beállítja az előfizetés egyedi azonosítóját.                      |
| subscriptionName         | sztring                                                         | Lekérdezi vagy beállítja az előfizetés nevét.                                   |
| subscriptionStartDate    | karakterlánc UTC dátum-idő formátumban                                 | Lekérdezi vagy beállítja azt a dátumot, amikor az előfizetés elindul.                   |
| Részösszeg                 | szám                                                         | Lekérdezi vagy beállítja a kedvezmény utáni összeget.                               |
| syndicationPartnerSubscriptionNumber | sztring                                             | Lekérdezi vagy beállítja a szindikált partner előfizetés számát.             |
| Tax                      | szám                                                         | Lekérdezi vagy beállítja a felszámított adókat.                                       |
| tier2MpnId               | szám                                                         | Lekérdezi vagy beállítja az ehhez a sorhoz tartozó 2. szintű partner MPN-AZONOSÍTÓját. |
| totalForCustomer         | szám                                                         | Lekérdezi vagy beállítja a teljes összeget a kedvezmény és az adó után.                 |
| totalOtherDiscount       | szám                                                         | Lekérdezi vagy beállítja a vásárláshoz társított kedvezményt.              |
| unitPrice                | szám                                                         | Lekérdezi vagy beállítja az egység árát.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

A használati alapú előfizetések számlázási sor tételét jelöli.

| Tulajdonság                 | Típus                                                           | Leírás                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| attribútumok               | sztring                                                         | Az attribútumok beolvasása.                                                  |
| billingCycleType         | sztring                                                         | Lekérdezi vagy beállítja a számlázási ciklus típusát.                                  |
| billingProvider          | sztring                                                         | Lekéri a számlázási szolgáltatót.                                            |
| chargeEndDate            | karakterlánc UTC dátum-idő formátumban                                 | Lekérdezi vagy beállítja a díj befejezési dátumát.                             |
| chargeStartDate          | karakterlánc UTC dátum-idő formátumban                                 | Lekérdezi vagy beállítja a díj kezdő dátumát.                           |
| chargeType               | sztring                                                         | Lekérdezi vagy beállítja a díj típusát.                                      |
| consumedQuantity         | szám                                                         | Lekérdezi vagy beállítja az összes felhasznált egységet.                                |
| consumptionDiscount      | sztring                                                         | Lekérdezi vagy beállítja a használaton belüli kedvezményt.                             |
| consumptionPrice         | sztring                                                         | Lekérdezi vagy beállítja a felhasznált mennyiség árát.                          |
| currency                 | sztring                                                         | Lekérdezi vagy beállítja az árakhoz társított pénznemet.                 |
| Customername (             | sztring                                                         | Lekérdezi vagy beállítja az ügyfél nevét.                                       |
| customerId               | sztring                                                         | Lekérdezi vagy beállítja az ügyfél egyedi azonosítóját.                          |
| detailLineItemId         | szám                                                         | Lekérdezi vagy beállítja a részletes sor AZONOSÍTÓját. Egyedileg azonosítja azokat az eseteket, ahol a számítás eltérő a felhasznált egységek esetében. Példa: teljes felhasznált mennyiség = 1338, 1024 egy díj ellenében díjat számítunk fel, az 314 díja eltérő.        |
| domainName               | sztring                                                         | Lekérdezi vagy beállítja a tartománynevet.                                             |
| includedQuantity         | szám                                                         | Lekérdezi vagy beállítja a sorrendbe foglalt egységeket.                         |
| invoiceLineItemType      | sztring                                                         | Lekérdezi a számlasor-tétel típusát.                                   |
| invoiceNumber            | sztring                                                         | Lekérdezi vagy beállítja a számla számát.                                      |
| listPrice                | szám                                                         | Lekérdezi vagy beállítja az egyes egységek árát.                                  |
| mpnId                    | szám                                                         | Lekérdezi vagy beállítja az ehhez a sorhoz társított MPN-azonosítót. A közvetlen viszonteladók esetében ez a viszonteladó MPN-azonosítója. A közvetett viszonteladók esetében ez a hozzáadott érték (VAR) MPN-azonosítója.                                   |
| Rendeléskód                  | sztring                                                         | Lekérdezi vagy beállítja a rendelés egyedi azonosítóját.                             |
| overageQuantity          | szám                                                         | Lekérdezi vagy beállítja az engedélyezett használat felett felhasznált mennyiséget.               |
| partnerBillableAccountId | sztring                                                         | Lekérdezi vagy beállítja a partner számlázandó fiókjának AZONOSÍTÓját.                         |
| partnerId                | sztring                                                         | Lekérdezi vagy beállítja a partner Azure Active Directory-bérlői AZONOSÍTÓját.            |
| partnerName              | sztring                                                         | Lekérdezi vagy beállítja a partner nevét.                                      |
| postTaxEffectiveRate     | szám                                                         | Lekérdezi vagy beállítja a hatályos árat az adók után.                         |
| postTaxTotal             | szám                                                         | Lekérdezi vagy beállítja a teljes díjat az adó után. ÁFA-díjak + áfa összege |
| preTaxCharges            | szám                                                         | Lekérdezi vagy beállítja az adók előtt fizetendő árat.                          |
| preTaxEffectiveRate      | szám                                                         | Lekérdezi vagy beállítja a hatályos árat az adók előtt.                        |
| régió                   | sztring                                                         | Lekérdezi vagy beállítja az erőforrás-példánnyal társított régiót.        |
| Erőforrás GUID azonosítója             | sztring                                                         | Lekérdezi vagy beállítja az erőforrás-azonosítót.                                 |
| resourceName             | sztring                                                         | Lekérdezi vagy beállítja az erőforrás nevét. Példa: adatbázis (GB/hónap).         |
| serviceName              | sztring                                                         | Lekérdezi vagy beállítja a szolgáltatás nevét. Példa: Azure-adatszolgáltatás.           |
| serviceType              | sztring                                                         | Lekérdezi vagy beállítja a szolgáltatás típusát. Példa: Azure SQL Azure DB.           |
| SKU                      | sztring                                                         | Lekérdezi vagy beállítja a szolgáltatási SKU-t.                                         |
| subscriptionDescription  | sztring                                                         | Lekérdezi vagy beállítja az előfizetés leírását.                            |
| subscriptionId           | sztring                                                         | Lekérdezi vagy beállítja az előfizetés egyedi azonosítóját.                      |
| subscriptionName         | sztring                                                         | Lekérdezi vagy beállítja az előfizetés nevét.                                   |
| taxAmount                | szám                                                         | Lekérdezi vagy beállítja a fizetendő adó összegét.                               |
| tier2MpnId               | szám                                                         | Lekérdezi vagy beállítja az ehhez a sorhoz tartozó 2. szintű partner MPN-AZONOSÍTÓját. |
| egység                     | sztring                                                         | Lekérdezi vagy beállítja az Azure-használat mértékegységét.                     |

## <a name="invoicestatement"></a>InvoiceStatement

Az Application/PDF-ben egy számlafogadó utasításban elérhető műveleteket jelöli.

| Tulajdonság                 | Típus                                                           | Leírás                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | ByteArrayContent a contentType = Application/PDF formátumban.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

A licenccel rendelkező előfizetések számlázási sorát jelöli.

| Tulajdonság | Típus | Leírás |
| --- | --- | --- |
| PartnerId | sztring | Lekérdezi vagy beállítja a partner bérlői AZONOSÍTÓját. |
| CustomerId | sztring | Lekérdezi vagy beállítja az ügyfél bérlői AZONOSÍTÓját. |
| CustomerName | sztring | Lekérdezi vagy beállítja az ügyfél nevét. |
| CustomerDomainName | sztring | Lekérdezi vagy beállítja az ügyfél tartományának nevét. |
| CustomerCountry | sztring | Lekérdezi vagy beállítja az ügyfél országát. |
| InvoiceNumber | sztring | Lekérdezi vagy beállítja a számla számát. |
| MpnId | sztring | Lekérdezi vagy beállítja az ehhez a sorhoz társított MPN-azonosítót. |
| ResellerMpnId | int | Lekérdezi vagy beállítja a rendelés egyedi azonosítóját. |
| OrderDate | DateTime | Lekérdezi vagy beállítja a rendelés létrehozásának dátumát. |
| ProductId | sztring | Lekérdezi vagy beállítja a termék egyedi azonosítóját. |
| SkuId | sztring | Lekérdezi vagy beállítja az SKU egyedi azonosítóját. |
| AvailabilityId | sztring | Lekérdezi vagy beállítja a rendelkezésre állás egyedi azonosítóját. |
| TermékNév | sztring | Lekérdezi vagy beállítja a terméknév nevét. |
| SkuName | sztring | Lekérdezi vagy beállítja az SKU nevét. |
| ChargeType | sztring | Lekérdezi vagy beállítja a díj típusát. |
| UnitPrice | decimal | Lekérdezi vagy beállítja az egység árát. |
| EffectiveUnitPrice | decimal | Lekérdezi vagy beállítja a hatályos egység árát. |
| UnitType | sztring | Lekérdezi vagy beállítja az egység típusát. |
| Mennyiség | int | Lekérdezi vagy beállítja az ehhez a sorhoz társított egységek számát. |
| Részösszeg | decimal | Lekérdezi vagy beállítja a kedvezmény utáni összeget. |
| TaxTotal | decimal | Lekérdezi vagy beállítja a felszámított adókat. |
| TotalForCustomer | decimal | Lekérdezi vagy beállítja a teljes összeget a kedvezmény és az adó után. |
| Pénznem | sztring | Lekérdezi vagy beállítja a tételhez használt pénznemet. |
| Közzétevő neve | sztring | Lekérdezi vagy beállítja a vásárláshoz társított közzétevő nevét. |
| PublisherId | sztring | Lekérdezi vagy beállítja a vásárláshoz társított közzétevő AZONOSÍTÓját. |
| SubscriptionDescription | sztring | Lekérdezi vagy beállítja a vásárláshoz társított előfizetés leírását. |
| SubscriptionId | sztring | Lekérdezi vagy beállítja a vásárláshoz társított előfizetés-azonosítót. |
| ChargeStartDate | DateTime | Lekérdezi vagy beállítja a vásárláshoz társított díj kezdő dátumát. |
| ChargeEndDate | DateTime | Lekérdezi vagy beállítja a vásárláshoz társított díj befejezési dátumát. |
| TermAndBillingCycle | sztring | Lekérdezi vagy beállítja a vásárláshoz társított kifejezést és számlázási ciklust. |
| AlternateId | sztring | Lekérdezi vagy beállítja a helyettesítő azonosítót (azonosító azonosító). |
| PriceAdjustmentDescription | sztring | Lekérdezi vagy beállítja az ár-helyesbítés leírását. |
| DiscountDetails | sztring |  **Elavult**. Lekérdezi vagy beállítja a vásárláshoz tartozó kedvezményes adatokat. |
| PricingCurrency | sztring | Lekérdezi vagy beállítja az árképzési pénznem kódját. |
| PCToBCExchangeRate | decimal | Lekérdezi vagy beállítja a díjszabási pénznemet a számlázási valuta árfolyamán. |
| PCToBCExchangeRateDate | DateTime | Lekérdezi vagy beállítja azt az árfolyam-időpontot, amelyen az árképzési pénznemet a számlázási valuta árfolyama alapján állapították meg. |
| BillableQuantity | decimal | Lekérdezi vagy beállítja a megvásárolt egységeket. Minden **BillableQuantity** nevű tervezési oszlop esetében. |
| MeterDescription | sztring | Lekérdezi vagy beállítja a használati sorok mérési leírását. |
| ReservationOrderId | sztring | Lekérdezi vagy beállítja az Azure RI-vásárlás foglalási rendelésének azonosítóját. |
| BillingFrequency | sztring | Lekérdezi vagy beállítja a számlázási gyakoriságot. |
| InvoiceLineItemType | InvoiceLineItemType | A számlasor-elemek típusát adja vissza. |
| BillingProvider | BillingProvider | A számlázási szolgáltatót adja vissza. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

A nem számlázott, számlázott egyeztetési sorok a napi névleges használatot jelentik.

| Tulajdonság | Típus | Leírás |
| --- | --- | --- |
| PartnerId | sztring | Lekérdezi vagy beállítja a partner bérlői AZONOSÍTÓját. |
| PartnerName | sztring | Lekérdezi vagy beállítja a partner nevét. |
| CustomerId | sztring | Lekérdezi vagy beállítja annak az ügyfélnek a bérlői AZONOSÍTÓját, amelyhez a használat tartozik. |
| CustomerName | sztring | Lekérdezi vagy beállítja annak az ügyfél-vállalatnak a nevét, amelyhez a használat tartozik. |
| CustomerDomainName | sztring | Lekérdezi vagy beállítja annak az ügyfélnek a tartománynevét, amely a használathoz tartozik. |
| InvoiceNumber | sztring | Lekérdezi vagy beállítja annak a számlának az AZONOSÍTÓját, amelyhez a használat tartozik. |
| ProductId | sztring | Lekérdezi vagy beállítja a termék egyedi azonosítóját. |
| SkuId | sztring | Lekérdezi vagy beállítja az SKU egyedi azonosítóját. |
| AvailabilityId | sztring | Lekérdezi vagy beállítja a rendelkezésre állás egyedi azonosítóját. |
| SkuName | sztring | Lekérdezi vagy beállítja a szolgáltatás SKU-nevét. |
| TermékNév | sztring | Lekérdezi vagy beállítja a termék nevét. |
| Közzétevő neve | sztring | Lekérdezi vagy beállítja a közzétevő nevét. |
| PublisherId | sztring | Lekérdezi vagy beállítja a közzétevő AZONOSÍTÓját. |
| SubscriptionId | sztring | Lekérdezi vagy beállítja az előfizetés AZONOSÍTÓját. |
| SubscriptionDescription | sztring | Lekérdezi vagy beállítja az előfizetés leírását. |
| ChargeStartDate | DateTime | Lekérdezi vagy beállítja a díj kezdő dátumát. |
| ChargeEndDate | DateTime | Lekérdezi vagy beállítja a díj befejezési dátumát. |
| UsageDate | DateTime | Lekérdezi vagy beállítja a használat dátumát. |
| MeterType | sztring | Lekérdezi vagy beállítja a mérési típust. |
| MeterCategory | sztring | Lekérdezi vagy beállítja a fogyasztásmérő kategóriáját. |
| MeterId | sztring | Lekérdezi vagy beállítja a mérőszám AZONOSÍTÓját (GUID). |
| MeterSubCategory | sztring | Lekérdezi vagy beállítja a mérési alkategóriát. |
| MeterName | sztring | Lekérdezi vagy beállítja a mérőszám nevét. |
| MeterRegion | sztring | Lekérdezi vagy beállítja a mérési régiót. |
| UnitOfMeasure | sztring | Lekérdezi vagy beállítja a mértékegységet. |
| ResourceLocation | sztring | Lekérdezi vagy beállítja az erőforrás helyét. |
| ConsumedService | sztring | Lekérdezi vagy beállítja a felhasznált szolgáltatásnév nevét. |
| ResourceGroup | sztring | Lekérdezi vagy beállítja az erőforráscsoport nevét. |
| ResourceUri | sztring | Lekérdezi vagy beállítja a használathoz használt erőforrás-példány URI-ját. |
| Címkék | sztring | Lekérdezi vagy beállítja az ügyfél által hozzáadott címkéket. |
| AdditionalInfo | sztring | Lekérdezi vagy beállítja a szolgáltatásra vonatkozó metaadatokat. Például egy virtuális gép rendszerképének típusa. |
| ServiceInfo1 | sztring | A belső Azure-szolgáltatás metaadatainak beolvasása vagy beállítása. |
| ServiceInfo2 | sztring | Lekérdezi vagy beállítja a szolgáltatás adatait, például egy virtuális gép és az INTERNETSZOLGÁLTATÓ nevét a ExpressRoute számára. |
| CustomerCountry | sztring | Lekérdezi vagy beállítja az ügyfél országát. |
| MpnId | sztring | Lekérdezi vagy beállítja az ehhez a sorhoz társított MPN-azonosítót. |
| ResellerMpnId | sztring | Lekérdezi vagy beállítja az ehhez a sorhoz tartozó 2. szintű partner viszonteladói MPN-AZONOSÍTÓját. |
| ChargeType | sztring | Lekérdezi vagy beállítja a díj típusát. |
| UnitPrice | decimal | Lekérdezi vagy beállítja az egység árát. |
| Mennyiség | decimal | Lekérdezi vagy beállítja a használat mennyiségét. |
| UnitType | sztring | Lekérdezi vagy beállítja az egység típusát (például 1 óra). |
| BillingPreTaxTotal | decimal | Lekérdezi vagy beállítja az ügyfél vagy a számlázási pénznem helyi pénznemében megjelenő adózás előtti kibővített költségeket vagy teljes költségeket. |
| BillingCurrency | sztring | Lekérdezi vagy beállítja az ISO-pénznemet, amelyben a mérőszámot az ügyfél vagy a számlázási pénznem helyi pénznemében számítjuk fel. |
| PricingPreTaxTotal | decimal | Lekérdezi vagy beállítja a kibővített költségeket vagy a teljes díjat, mielőtt az USD vagy a katalógus pénznemét az értékeléshez használják. |
| PricingCurrency | sztring | Lekérdezi vagy beállítja azt az ISO-pénznemet, amelyben a mérőszámot USD vagy katalógus pénznemben számítjuk fel a minősítéshez. |
| EntitlementId | sztring | Lekérdezi vagy beállítja a jogosultság (Azure-előfizetés) AZONOSÍTÓját. |
| EntitlementDescription | sztring | Lekérdezi vagy beállítja a jogosultság (Azure-előfizetés) leírását. |
| PCToBCExchangeRate | sztring | Lekérdezi vagy beállítja a díjszabási pénznemet a számlázási valuta árfolyamán. |
| PCToBCExchangeRateDate | DateTime | Lekérdezi vagy beállítja az árképzési pénznemet a számlázási valuta árfolyamának dátumára. |
| EffectiveUnitPrice | decimal | Lekérdezi vagy beállítja a hatályos egység árát. |
| RateOfPartnerEarnedCredit | decimal | Lekérdezi vagy beállítja a partner által létrehozott kreditek arányát. |
| hasPartnerEarnedCredit | logikai | Lekérdezi vagy beállítja a partner által létrehozott kreditet. |
| InvoiceLineItemType | InvoiceLineItemType | A számlasor-elemek típusát adja vissza. |
| BillingProvider | BillingProvider | A számlázási szolgáltatót adja vissza. |
