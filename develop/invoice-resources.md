---
title: Számlaerőforrások
description: Több számlához kapcsolódó erőforrás is elérhető a Partnerközpont API-kon keresztül. Ezek az erőforrások a számla és a sortétel részleteihez kapcsolódnak.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b07b7ad14c136eac988eeb12391c24a6cf996b39
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548425"
---
# <a name="invoice-resources"></a>Számlaerőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A következő, számlával kapcsolatos erőforrások érhetők el a Partnerközpont API-kon keresztül.

## <a name="invoice"></a>Számla

| Tulajdonság | Típus | Leírás |
| -------- | ---- | ----------- |
| id | sztring | A számlaazonosító. |
| invoiceDate (számla dátuma) | sztring UTC dátum-idő formátumban | A számla keletkeztének dátuma. |
| billingPeriodStartDate | sztring UTC dátum-idő formátumban | Számlázási időszak kezdődátuma (UTC). |
| billingPeriodEndDate | sztring UTC dátum-idő formátumban   | Számlázási időszak záró dátuma (UTC). |
| totalCharges | szám | A teljes díj. Tartalmazza a tranzakciók és a kiigazítások díját.     |
| paidAmount (fizetős összeg) | szám  | A partner által kifizetett összeg. Negatív, ha kifizetés érkezett.  |
| currencyCode | sztring  | Egy kód, amely a számlatételek összes összegére és végösszegére használt pénznemet jelzi. |
| currencySymbol  | sztring | A számlatételek összegeihez és végösszegeihez használt pénznemszimbólum. |
| pdfDownloadLink | sztring  | A számla PDF formátumban való letöltésére mutató hivatkozás. Ez a hivatkozás nem lesz visszaadva a keresési eredmények részeként, és csak akkor lesz feltöltve, ha azonosító alapján fér hozzá a számlához. Ez a hivatkozás 30 percen belül automatikusan lejár. |
| invoiceDetails (számlarészletek)  | [InvoiceDetail objektumok tömbje](#invoicedetail)  | A számla részletei.  |
| Módosítások      | [Számlaobjektumok tömbje](#invoice)   | A számla módosításai.  |
| documentType (documentType)    | sztring | A számla dokumentumtípusa: "Jóváírási megjegyzés", "Számla". |
| aszitikákOf        | sztring | Annak a dokumentumnak a hivatkozási száma, amelynek ez a dokumentum a módosítása.  |
| invoiceType (számla típusa)     | sztring  | A számla típusa: "ismétlődő", \_ "egyszeri".   |
| Linkek           | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)  | Az erőforrás-hivatkozások.  |
| Attribútumok      | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.  |

## <a name="invoicedetail"></a>InvoiceDetail (Számlarészlet)

A számla számlázott tételek gyűjteményét tartalmazza, és mindegyik tételt egy InvoiceDetail erőforrás képviseli.

| Tulajdonság            | Típus                                                           | Leírás                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | sztring                                                         | A számla részleteinek típusa: "none", "usage \_ line \_ items", "billing \_ line \_ items". |
| billingProvider     | sztring                                                         | A számlázási szolgáltató: "nincs", "office", "azure" vagy "azure \_ data \_ market".         |
| Linkek               | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | Az erőforrás-hivatkozások.                                                               |
| Attribútumok          | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

A számlán belül minden egyes díj InvoiceLineItemként van ábrázolva.

| Tulajdonság            | Típus                                                           | Leírás                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | sztring                                                         | A számlasorelem típusa: "none", "usage \_ line \_ items", "billing \_ line \_ items". |
| billingProvider     | sztring                                                         | A számlázási szolgáltató: "nincs", "office", "azure" vagy "azure \_ data \_ market".            |
| Attribútumok          | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                                             |

## <a name="invoicesummary"></a>InvoiceSummary (Számla összege)

Egy számla egyenlegének és teljes díjának összegzését ismerteti.

| Tulajdonság                 | Típus                                                           | Leírás                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount (egyenleg)            | szám                                                         | A számla egyenlege. Ez a ki nem fizetett számlák teljes összege. |
| currencyCode             | sztring                                                         | Az egyenleghez használt pénznemet jelző kód.       |
| currencySymbol           | sztring                                                         | A használt pénznemszimbólum.                                             |
| accountingDate (könyvelésidátum)           | sztring UTC dátum-idő formátumban                                 | Az egyenleg összegének utolsó frissítésének dátuma.                         |
| firstInvoiceCreationDate | sztring UTC dátum-idő formátumban                                 | Az ügyfél első számlájának létrehozási dátuma.              |
| lastPaymentDate (utolsó fizetés összege)          | sztring UTC dátum-idő formátumban                                 | Az utolsó kifizetés dátuma.                                         |
| lastPaymentAmount        | szám                                                         | Az utolsó kifizetés összege.                                       |
| latestInvoiceDate (legfrissebb számladátum)        | sztring UTC dátum-idő formátumban                                 | Az a dátum, amikor az ügyfél utolsó számlája létrejött.               |
| Részletek                  | [InvoiceSummaryDetail objektumok tömbje](#invoicesummarydetail) | A számla összegzésének részletei.                                           |
| Linkek                    | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)            | Az erőforrás-hivatkozások.                                                   |
| Attribútumok               | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail (Számlaösszegrészlet)

Egy számlatípus (például ismétlődő, egyszeri) egyedi részleteinek \_ összegzését jelöli.

| Tulajdonság            | Típus                                                           | Leírás                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType (számla típusa)         | sztring                                                         | A számla típusa: "ismétlődő", \_ "egyszeri".                                       |
| összegzés             | [InvoiceSummary](#invoicesummary) objektum                       | A számla összegzése számlatípusonként.                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries (Számlaösszegek)

Egy [InvoiceSummary](#invoicesummary) típusú gyűjteményt képvisel, amely a számlatípus pénznemenkénti egyedi adatait tartalmazza.

| Tulajdonság            | Típus                                                           | Leírás                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary (gyűjteményofSummary) | [InvoiceSummary objektumok tömbje](#invoicesummary)             | A számla összegzése számlatípusonként pénznemenként.                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem (LicencbesoroltlineItem)

Licencalapú előfizetések számlázási sortételét jelöli.

| Tulajdonság                 | Típus                                                           | Leírás                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| Összeg                   | sztring                                                         | Lekért vagy beállítja a teljes összeget. Teljes összeg = egységár * mennyiség.  |
| Attribútumok               | sztring                                                         | Lekérte az attribútumokat.                                                  |
| billingCycleType (számlázási ciklustípus)         | sztring                                                         | Lekért vagy beállítja a számlázási ciklus típusát.                                  |
| billingProvider          | sztring                                                         | Lekérte a számlázási szolgáltatót.                                            |
| chargeEndDate            | sztring UTC dátum-idő formátumban                                 | Lekért vagy beállítja a díj záró dátumát.                             |
| chargeStartDate (költségindításidátum)          | sztring UTC dátum-idő formátumban                                 | Lekért vagy beállítja a díj kezdő dátumát.                           |
| chargeType               | sztring                                                         | Lekért vagy beállítja a díj típusát.                                      |
| currency                 | sztring                                                         | Lekért vagy beállítja a sorelemhez használt pénznemet.                    |
| customerId               | sztring                                                         | Lekért vagy beállítja az ügyfél egyedi azonosítóját a Microsoft számlázási platformon.  |
| customerName (ügyfél neve)             | sztring UTC dátum-idő formátumban                                 | Lekért vagy beállítja az ügyfél nevét.                                       |
| Tartománynév               | sztring                                                         | Lekért vagy beállítja a tartománynevet.                                             |
| durableOfferId           | sztring                                                         | Lekért vagy beállítja a tartós ajánlat egyedi azonosítóját.                     |
| invoiceLineItemType      | sztring                                                         | Lekérte a számlasorelem típusát.                                   |
| mpnId                    | szám                                                         | Lekért vagy beállítja a sorelemhez társított MPN-azonosítót. Közvetlen viszonteladók esetén ez a viszonteladó MPN-azonosítója. Közvetett viszonteladók esetén ez az értékkel hozzáadott viszonteladó (VAR) MPN-azonosítója.                                   |
| offerId (ajánlatazonosító)                  | sztring                                                         | Lekért vagy beállítja az ajánlat egyedi azonosítóját.                             |
| offerName (ajánlat neve)                | sztring                                                         | Lekért vagy beállítja az ajánlat nevét.                                          |
| orderId (rendelésazonosító)                  | sztring                                                         | Lekért vagy beállítja a rendelés egyedi azonosítóját.                             |
| partnerazonosító                | sztring                                                         | Lekérte vagy beállítja a partner Azure Active Directory-bérlőazonosítóját.            |
| quantity                 | szám                                                         | Lekért vagy beállítja a sorelemhez társított egységek számát.      |
| subscriptionDescription (előfizetési leírás)  | sztring                                                         | Lekért vagy beállítja az előfizetés leírását.                            |
| subscriptionEndDate      | sztring UTC dátum-idő formátumban                                 | Lekért vagy beállítja az előfizetés lejáratának dátumát.                      |
| subscriptionId           | sztring                                                         | Lekért vagy beállítja az előfizetés egyedi azonosítóját.                      |
| subscriptionName         | sztring                                                         | Lekért vagy beállítja az előfizetés nevét.                                   |
| subscriptionStartDate    | sztring UTC dátum-idő formátumban                                 | Lekért vagy beállítja az előfizetés elindulásának dátumát.                   |
| Részösszeg                 | szám                                                         | Lekért vagy beállítja az összeget a kedvezmény után.                               |
| syndicationPartnerSubscriptionNumber | sztring                                             | Lekért vagy beállítja a szindikációs partner előfizetési számát.             |
| Adó                      | szám                                                         | Lekért vagy beállítja a fizetendő adókat.                                       |
| tier2MpnId               | szám                                                         | Lehívja vagy beállítja a sorelemhez társított 2. rétegbeli partner MPN-azonosítóját. |
| totalForCustomer         | szám                                                         | Lekért vagy beállítja a teljes összeget a kedvezmény és az adó után.                 |
| totalOtherDiscount       | szám                                                         | Lekért vagy beállítja a vásárláshoz társított kedvezményt.              |
| unitPrice                | szám                                                         | Lekért vagy beállítja az egységárat.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

A használatalapú előfizetések számlázási sortételét jelöli.

| Tulajdonság                 | Típus                                                           | Leírás                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| Attribútumok               | sztring                                                         | Lekérte az attribútumokat.                                                  |
| billingCycleType         | sztring                                                         | Lekért vagy beállítja a számlázási ciklus típusát.                                  |
| billingProvider          | sztring                                                         | Lekérte a számlázási szolgáltatót.                                            |
| chargeEndDate            | sztring UTC dátum-idő formátumban                                 | Lekért vagy beállítja a díj záró dátumát.                             |
| chargeStartDate (díjindításidátum)          | sztring UTC dátum-idő formátumban                                 | Lekért vagy beállítja a díj kezdő dátumát.                           |
| chargeType               | sztring                                                         | Lekért vagy beállítja a díj típusát.                                      |
| consumedQuantity         | szám                                                         | Lekért vagy beállítja a felhasznált összes egységet.                                |
| consumptionDiscount      | sztring                                                         | Lekért vagy beállítja a használatra vonatkozó kedvezményt.                             |
| consumptionPrice (fogyasztási ár)         | sztring                                                         | Lekért vagy beállítja a felhasznált mennyiség árát.                          |
| currency                 | sztring                                                         | Lekért vagy beállítja az árakhoz társított pénznemet.                 |
| customerName (ügyfél neve)             | sztring                                                         | Lekérte vagy beállítja az ügyfél nevét.                                       |
| customerId               | sztring                                                         | Lekért vagy beállítja az ügyfél egyedi azonosítóját.                          |
| detailLineItemId (RészletekLineItemId)         | szám                                                         | Lekért vagy beállítja a részletsor elemazonosítóját. Egyedileg azonosítja azokat a sorelemeket, ahol a számítás eltér a felhasznált egységeknél. Példa: A felhasznált mennyiség összesen = 1338, 1024 díj egy díj alapján van felszámva, a 314 más díjakkal.        |
| Tartománynév               | sztring                                                         | Lekért vagy beállítja a tartománynevet.                                             |
| includedQuantity         | szám                                                         | Lekért vagy beállítja a rendelésben szereplő egységeket.                         |
| invoiceLineItemType      | sztring                                                         | Lekérte a számlasorelem típusát.                                   |
| invoiceNumber (számlaszám)            | sztring                                                         | Lekért vagy beállítja a számlaszámot.                                      |
| listPrice (árlista)                | szám                                                         | Lekért vagy beállítja az egyes egységek árát.                                  |
| mpnId                    | szám                                                         | Lekért vagy beállítja a sorelemhez társított MPN-azonosítót. Közvetlen viszonteladók esetén ez a viszonteladó MPN-azonosítója. Közvetett viszonteladók esetén ez az értékkel hozzáadott viszonteladó (VAR) MPN-azonosítója.                                   |
| orderId (rendelésazonosító)                  | sztring                                                         | Lekért vagy beállítja a rendelés egyedi azonosítóját.                             |
| overageQuantity (túl nagyság)          | szám                                                         | Lekért vagy beállítja az engedélyezett használat feletti felhasznált mennyiséget.               |
| partnerBillableAccountId | sztring                                                         | Lekért vagy beállítja a partner számlázható fiókazonosítóját.                         |
| partnerazonosító                | sztring                                                         | Lekért vagy beállítja a partner Azure Active Directory-bérlőazonosítóját.            |
| partnerName              | sztring                                                         | Lekérte vagy beállítja a partner nevét.                                      |
| postTaxEffectiveRate     | szám                                                         | Lekért vagy beállítja a tényleges árat az adók után.                         |
| postTaxTotal (postTaxTotal)             | szám                                                         | Lekért vagy beállítja az adó utáni teljes díjakat. Adók előtti díjak + adó összege |
| preTaxCharges            | szám                                                         | Lekért vagy beállítja az adók nélkül felszámított árat.                          |
| preTaxEffectiveRate      | szám                                                         | Lekért vagy beállítja az adók előtti tényleges árat.                        |
| régió                   | sztring                                                         | Lekért vagy beállítja az erőforráspéldányhoz társított régiót.        |
| resourceGuid (erőforrásguid)             | sztring                                                         | Lekért vagy beállítja az erőforrás-azonosítót.                                 |
| resourceName             | sztring                                                         | Lekért vagy beállítja az erőforrás nevét. Például: Adatbázis (GB/hó).         |
| serviceName (szolgáltatásnév)              | sztring                                                         | Lekért vagy beállítja a szolgáltatás nevét. Például: Azure Data Service.           |
| serviceType (szolgáltatástípus)              | sztring                                                         | Lekért vagy beállítja a szolgáltatás típusát. Például: Azure SQL Azure DB.           |
| Sku                      | sztring                                                         | Lekért vagy beállítja a szolgáltatás termékváltozatát.                                         |
| subscriptionDescription (subscriptionDescription)  | sztring                                                         | Lekért vagy beállítja az előfizetés leírását.                            |
| subscriptionId           | sztring                                                         | Lekért vagy beállítja az előfizetés egyedi azonosítóját.                      |
| subscriptionName         | sztring                                                         | Lekérte vagy beállítja az előfizetés nevét.                                   |
| taxAmount (taxAmount)                | szám                                                         | Lekért vagy beállítja a felszámított adó összegét.                               |
| tier2MpnId               | szám                                                         | Lekért vagy beállítja a sorelemhez társított 2. rétegbeli partner MPN-azonosítóját. |
| egység                     | sztring                                                         | Lekérjük vagy beállítja az Azure-használat mértékegységét.                     |

## <a name="invoicestatement"></a>InvoiceStatement (Számla összege)

Az alkalmazás/pdf formátumú számlakivonaton elérhető műveleteket jelöli.

| Tulajdonság                 | Típus                                                           | Leírás                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | ByteArrayContent contentType = application/pdf értékekkel.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Licencalapú előfizetések számlázási sortételét jelöli.

| Tulajdonság | Típus | Leírás |
| --- | --- | --- |
| Partnerazonosító | sztring | Lekért vagy beállítja a partner bérlőazonosítóját. |
| CustomerId | sztring | Lekért vagy beállítja az ügyfél bérlőazonosítóját. |
| CustomerName | sztring | Lekért vagy beállítja az ügyfél nevét. |
| CustomerDomainName (Ügyféltartományneve) | sztring | Lekért vagy beállítja az ügyfél tartománynevét. |
| CustomerCountry (Ügyfél országa) | sztring | Lekérte vagy beállítja az ügyfél országát. |
| InvoiceNumber (Számlaszám) | sztring | Lekért vagy beállítja a számlaszámot. |
| MpnId | sztring | Lekért vagy beállítja a sorelemhez társított MPN-azonosítót. |
| ResellerMpnId | int | Lekért vagy beállítja a rendelés egyedi azonosítóját. |
| OrderDate | DateTime | Lekért vagy beállítja a rendelés létrehozási dátumát. |
| ProductId | sztring | Lekért vagy beállítja a termék egyedi azonosítóját. |
| SkuId (Termékváltozatazonosító) | sztring | Lekért vagy beállítja a termékváltozat egyedi azonosítóját. |
| AvailabilityId (Rendelkezésre állásiid) | sztring | Lekért vagy beállítja a rendelkezésre állás egyedi azonosítóját. |
| TermékNév | sztring | Lekért vagy beállítja a termék nevét. |
| SkuName | sztring | Lekért vagy beállítja a termékváltozat nevét. |
| ChargeType | sztring | Lekért vagy beállítja a díj típusát. |
| UnitPrice | tizedes tört | Lekért vagy beállítja az egységárat. |
| EffectiveUnitPrice (Tényleges egységár) | tizedes tört | Lekért vagy beállítja a tényleges egységárat. |
| UnitType (Egységtípus) | sztring | Lekért vagy beállítja az egység típusát. |
| Mennyiség | int | Lekért vagy beállítja a sorelemhez társított egységek számát. |
| Részösszeg | tizedes tört | Lekért vagy beállítja az összeget a kedvezmény után. |
| TaxTotal (Adóösszeg) | tizedes tört | Lekért vagy beállítja a felszámított adókat. |
| TotalForCustomer | tizedes tört | Lekért vagy beállítja a kedvezmény és az adó utáni teljes összeget. |
| Pénznem | sztring | Lekért vagy beállítja a sorelemhez használt pénznemet. |
| Közzétevő neve | sztring | Lekért vagy beállítja a vásárláshoz társított közzétevő nevét. |
| PublisherId | sztring | Lekért vagy beállítja a vásárláshoz társított közzétevő-azonosítót. |
| SubscriptionDescription (Előfizetés-leírás) | sztring | Lekért vagy beállítja a vásárláshoz társított előfizetés leírását. |
| SubscriptionId | sztring | Lekért vagy beállítja a vásárláshoz társított előfizetés-azonosítót. |
| ChargeStartDate (Költségindításidátum) | DateTime | Lekért vagy beállítja a vásárláshoz társított díj kezdő dátumát. |
| ChargeEndDate (Költség és költségdátum) | DateTime | Lekért vagy beállítja a vásárláshoz társított díj záró dátumát. |
| TermAndBillingCycle | sztring | Lekért vagy beállítja a vásárláshoz kapcsolódó adatokat és számlázási ciklusokat. |
| AlternateId (Alternatívazonosító) | sztring | Lekérése vagy beállítja a másodlagos azonosítót (ajánlatazonosító). |
| PriceAdjustmentDescription (Áradjustmentdescription) | sztring | Lekért vagy beállítja az árkorrekció leírását. |
| CreditReasonCode | sztring | Lekért vagy beállítja a jóváírási ok kódját. |
| DiscountDetails (Kedvezményrészletek) | sztring |  **Elavult.** Lekért vagy beállítja a vásárláshoz társított kedvezmény részleteit. |
| PricingCurrency | sztring | Lekért vagy beállítja a díjszabás pénznemkódját. |
| PCToBCExchangeRate (PcToBCExchangeRate) | tizedes tört | Lekérte vagy beállítja a díjszabási pénznemet a számlázási pénznem átváltási árfolyamára. |
| PCToBCExchangeRateDate (PcToBCExchangeRateDate) | DateTime | Lekért vagy beállítja az árfolyam dátumát, amikor a díjszabási pénznemet a számlázási pénznem árfolyamának határozzák meg. |
| BillableQuantity (Számlázható számlázás) | tizedes tört | Lekért vagy beállítja a megvásárolt egységeket. Minden **BillableQuantity** nevű tervezési oszlophoz. |
| MeterDescription (MeterDescription) | sztring | Lekért vagy beállítja a fogyasztásmérő leírását a fogyasztásvonal-elemhez. |
| ReservationOrderId | sztring | Lekért vagy beállítja egy Azure RI Purchase foglalási rendelésének azonosítóját. |
| BillingFrequency (Számlázási sorszám) | sztring | Lekért vagy beállítja a számlázási gyakoriságot. |
| InvoiceLineItemType (Számlasor típusa) | InvoiceLineItemType (Számlasor típusa) | A számlasorelem típusát adja vissza. |
| BillingProvider | BillingProvider | A számlázási szolgáltatót adja vissza. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

A napi minősített használat számlázatlan, számlázatlan egyeztetési sorelemeket jelöli.

| Tulajdonság | Típus | Leírás |
| --- | --- | --- |
| Partnerazonosító | sztring | Lekért vagy beállítja a partner bérlőazonosítóját. |
| PartnerName | sztring | Lekérte vagy beállítja a partner nevét. |
| CustomerId | sztring | Lekért vagy beállítja annak az ügyfélnek a bérlőazonosítóját, amelyhez a használat tartozik. |
| CustomerName | sztring | Lekért vagy beállítja annak az ügyfélvállalatnak a nevét, amelyhez a használat tartozik. |
| CustomerDomainName (Ügyféltartományneve) | sztring | Lekért vagy beállítja annak az ügyfélnek a tartománynevét, amelyhez a használat tartozik. |
| InvoiceNumber (Számlaszám) | sztring | Lekért vagy beállítja annak a számlának az azonosítóját, amelyhez a használat tartozik. |
| ProductId | sztring | Lekért vagy beállítja a termék egyedi azonosítóját. |
| SkuId (Termékváltozatazonosító) | sztring | Lekért vagy beállítja a termékváltozat egyedi azonosítóját. |
| AvailabilityId (Rendelkezésre állásiid) | sztring | Lekért vagy beállítja a rendelkezésre állás egyedi azonosítóját. |
| SkuName | sztring | Lekért vagy beállítja a szolgáltatás termékváltozatának nevét. |
| TermékNév | sztring | Lekért vagy beállítja a termék nevét. |
| Közzétevő neve | sztring | Lekért vagy beállítja a közzétevő nevét. |
| PublisherId | sztring | Lekérte vagy beállítja a közzétevő azonosítóját. |
| SubscriptionId | sztring | Lekért vagy beállítja az előfizetés azonosítóját. |
| SubscriptionDescription (Előfizetés-leírás) | sztring | Lekért vagy beállítja az előfizetés leírását. |
| ChargeStartDate (Költségindításidátum) | DateTime | Lekért vagy beállítja a díj kezdő dátumát. |
| ChargeEndDate (Költség és költségdátum) | DateTime | Lekért vagy beállítja a díj záró dátumát. |
| UsageDate | DateTime | Lekért vagy beállítja a használati dátumot. |
| MeterType (Mérőtípus) | sztring | Lekért vagy beállítja a fogyasztásmérő típusát. |
| MeterCategory | sztring | Lekért vagy beállítja a fogyasztásmérő kategóriáját. |
| MeterId | sztring | Lekért vagy beállítja a fogyasztásmérő azonosítóját (GUID). |
| MeterSubCategory | sztring | Lekért vagy beállítja a fogyasztásmérő alkategóriáját. |
| MeterName | sztring | Lekért vagy beállítja a mérő nevét. |
| MeterRegion | sztring | Lekért vagy beállítja a fogyasztásmérő régióját. |
| UnitOfMeasure | sztring | Lekért vagy beállítja a mértékegységet. |
| ResourceLocation | sztring | Lekért vagy beállítja az erőforrás helyét. |
| ConsumedService | sztring | Lekért vagy beállítja a felhasznált szolgáltatás nevét. |
| ResourceGroup | sztring | Lekért vagy beállítja az erőforráscsoport nevét. |
| ResourceUri (Erőforrás-azonosító) | sztring | Lekért vagy beállítja annak az erőforráspéldánynak az URI-ját, amelyről a használat szól. |
| Címkék | sztring | Lekért vagy beállítja az ügyfél által hozzáadott címkéket. |
| AdditionalInfo | sztring | Lekért vagy beállítja a szolgáltatásspecifikus metaadatokat. Például egy virtuális gép rendszerképének típusa. |
| ServiceInfo1 | sztring | Beszeri vagy beállítja az Azure-szolgáltatások belső metaadatait. |
| ServiceInfo2 | sztring | Lekért vagy beállítja a szolgáltatásadatokat, például egy virtuális gép rendszerképtípusát és az ExpressRoute internetszolgáltatói nevét. |
| CustomerCountry (Ügyfél országa) | sztring | Lekért vagy beállítja az ügyfél országát. |
| MpnId | sztring | Lekért vagy beállítja a sorelemhez társított MPN-azonosítót. |
| ResellerMpnId (Viszonteladóimpn-azonosító) | sztring | Lehívja vagy beállítja a sorelemhez társított 2. rétegbeli partner viszonteladói MPN-azonosítóját. |
| ChargeType | sztring | Lekért vagy beállítja a díj típusát. |
| UnitPrice | tizedes tört | Lekért vagy beállítja az egység árát. |
| Mennyiség | tizedes tört | Lekért vagy beállítja a használat mennyiségét. |
| UnitType (Egységtípus) | sztring | Lekért vagy beállítja az egység típusát (például 1 óra). |
| BillingPreTaxTotal | tizedes tört | Lekért vagy beállítja az adóz előtti kiterjesztett költséget vagy teljes költséget az ügyfél vagy a számlázási pénznem helyi pénznemében. |
| BillingCurrency | sztring | Lekért vagy beállítja az ISO-pénznemet, amelyben a mérőszámért az ügyfél vagy a számlázási pénznem helyi pénznemében kell fizetni. |
| PricingPreTaxTotal | tizedes tört | Lekért vagy beállítja a kiterjesztett, adózható költségeket USD-ben vagy katalógusban, a minősítéshez használt pénznemben. |
| PricingCurrency | sztring | Lekért vagy beállítja azt az ISO-pénznemet, amelyben a fogyasztásmérőnek amerikai dollárban kell fizetnie, vagy a katalógusban az értékeléshez használt pénznemet. |
| EntitlementId (Jogosultságazonosító) | sztring | Lekért vagy beállítja a jogosultság (Azure-előfizetés) azonosítóját. |
| EntitlementDescription (Jogosultságleíró) | sztring | Lekért vagy beállítja a jogosultság leírását (Azure-előfizetés). |
| PCToBCExchangeRate | sztring | Lekért vagy beállítja a díjszabási pénznemet a számlázási pénznem átváltási árfolyamára. |
| PCToBCExchangeRateDate | DateTime | Lekért vagy beállítja a díjszabási pénznemet a számlázási pénznem átváltási árfolyamának dátumára. |
| EffectiveUnitPrice (Hatályos egységár) | tizedes tört | Lekért vagy beállítja a tényleges egységárat. |
| RateOfPartnerEarnedCredit | tizedes tört | Lekért vagy beállítja a partneri jóváírás mértékét. |
| HasPartnerEarnedCredit | logikai | A be- vagy beírás a partneri jóváírás alkalmazása. |
| RateOfCredit | tizedes tört | Lekért vagy beállítja az adott kredittípushoz kapott kreditek kamatlábát. |
| CreditType (Kredittípus) | sztring | Lekért vagy beállítja a kredit típusát. |
| InvoiceLineItemType (Számlasor típusa) | InvoiceLineItemType (Számlasor típusa) | A számlasorelem típusát adja vissza. |
| BillingProvider | BillingProvider | A számlázási szolgáltatót adja vissza. |
