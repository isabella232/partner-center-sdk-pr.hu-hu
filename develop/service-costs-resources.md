---
title: Szolgáltatási költségek erőforrásai
description: Az ügyfél által megvásárolt szolgáltatásokhoz kapcsolódó erőforrásokat ismerteti.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dbddc1973dd9a904cedd549c1772cd4c74c69a60
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547410"
---
# <a name="service-costs-resources"></a>Szolgáltatási költségek erőforrásai

Az ügyfél által megvásárolt szolgáltatásokhoz kapcsolódó erőforrásokat ismerteti.

## <a name="servicecostssummary"></a>ServiceCostsSummary

**A ServiceCostsSummary** egy összegzést tartalmaz, amely a megadott ügyfél által a számlázási időszakban megvásárolt összes szolgáltatást összesíti.

| Tulajdonság | Típus | Leírás |
| -------- | ---- | ----------- |
| Részletek | [ServiceCostsSummaryDetail objektumok tömbje](#servicecostssummarydetail) | A szolgáltatás költségösszegzési részleteinek listája, a számla típusa alapján megkülönböztetve.|
| Linkek | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks) | Az erőforrás-hivatkozások. |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok. |

> [!IMPORTANT]
> **Az alábbi táblázat mezői elavultak.** Az ismétlődő és egyszeri szolgáltatásköltség-összegzések lekérése helyett használja a **Részletek** mezőt. A **részleteket** tartalmazó mezőt az előző táblázat ismerteti. Tekintse meg **a részletek mező** megfelelő adatértékét, de a gyökérszintű mezőket ne.

| Tulajdonság | Típus | Leírás |
| -------- | ---- | ----------- |
| billingStartDate (számlázás kezdődátum) | dátum | A számlázási időszak kezdete. |
| billingEndDate (számlázási dátum) | dátum | A számlázási időszak vége. |
| pretaxTotal | double | Az ügyfél összes költségének adók előtti összege. |
| Adó  | double | Az ügyfél által megvásárolt összes tételre vonatkozó teljes adó. |
| afterTaxTotal | double | Az ügyfél által megvásárolt összes tétel nettó teljes költsége. |
| currencyCode | sztring | A költségekhez használt pénznemet jelöli. |
| currencySymbol | sztring | A költségekhez használt pénznemszimbólum. |
| customerId | sztring | A vásárlást meghozó ügyfél azonosítója. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**A ServiceCostsSummaryDetail** egy szolgáltatási költség összegzését ismerteti, amely a megadott ügyfél által a számlázási időszakban vásárolt összes szolgáltatást összesíti (ismétlődő vagy egyszeri számlákból).

| Tulajdonság | Típus | Leírás |
| -------- | ---- | ----------- |
| invoiceType (számla típusa) | sztring | Az invoiceType tulajdonság, amely alapján a szolgáltatás költségösszegzése létre lett hozva. |
| összegzés | [ServiceCostsSummary](#servicecostssummary) | A szolgáltatás költségeinek összegzése egy ügyfél szerint, egy számlatípus szerint. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**A ServiceCostLineItem** az ügyfél által megvásárolt egyetlen tételt írja le.

> [!IMPORTANT]
> A következő  tulajdonságok csak azokra a szolgáltatási *költségsorelemekre* vonatkoznak, ahol a termék egy alkalommal vásárolható meg: **productId**, **productName,** **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**. Ezek a *tulajdonságok nem vonatkoznak azokra* a szolgáltatássorelemekre, ahol a termék ismétlődő *vásárlás.* Ezek a tulajdonságok például *nem vonatkoznak az* előfizetés-alapú Office 365 azure-ban.

| Tulajdonság                 | Típus                           | Leírás                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| startDate (kezdőDátum)                | sztring UTC dátum-idő formátumban | A díj kezdő dátuma.                                       |
| endDate (záródátum)                  | sztring UTC dátum-idő formátumban | A díj záró dátuma.                                         |
| subscriptionFriendlyName | sztring                         | Az előfizetés rövid neve.                              |
| subscriptionId           | sztring                         | Az előfizetés azonosítója.                                         |
| orderId (rendelésazonosító)                  | sztring                         | A rendelés azonosítója.                                                |
| offerId (ajánlatazonosító)                  | sztring                         | Az ajánlat azonosítója.                                                |
| offerName (ajánlat neve)                | sztring                         | Az ajánlat neve.                                                      |
| resellerMPNId            | sztring                         | Csak kétszintű partneri forgatókönyvekben használatos. Az MPN-azonosítóra hivatkozik. |
| chargeType               | sztring                         | A társított díj típusa.                                          |
| quantity                 | szám                         | A felhasznált vagy megvásárolt egységek mennyisége.                             |
| unitPrice                | szám                         | Az egységenkénti ár.                                                  |
| pretaxTotal              | szám                         | A tétel adók előtti teljes díjában.                         |
| Adó                      | szám                         | Az adott tételre vonatkozó teljes adóköltség.                         |
| afterTaxTotal            | szám                         | Az elem nettó teljes költsége.                                    |
| currencyCode             | sztring                         | A költségekhez használt pénznemet jelöli.                          |
| currencySymbol           | sztring                         | A költségekhez használt pénznemszimbólum.                              |
| customerId               | sztring                         | A vásárlást meghozó ügyfél azonosítója.                          |
| customerName (ügyfél neve)             | sztring                         | A vásárlást megtenő ügyfél neve.                        |
| invoiceNumber (számlaszám)            | sztring                         | A számla száma, amelyhez ez a sorelem tartozik.                   |
| productId                | sztring                         | A termékazonosító.                                              |
| skuId (termékváltozatazonosító)                    | sztring                         | A termékváltozat-azonosító.                                                  |
| availabilityId (rendelkezésre állásiid)           | sztring                         | A rendelkezésre állási azonosító.                                         |
| Productname              | sztring                         | A termék neve.                                                    |
| skuName                  | sztring                         | A termékváltozat neve.                                                        |
| publisherName            | sztring                         | A közzétevő neve.                                                  |
| publisherId (közzétevőiazonosító              | sztring                         | A közzétevő azonosítója.                                            |
| termAndBillingCycle      | sztring                         | A kifejezés és a számlázási ciklus.                                          |
| discountDetails (részletek discountDetails)          | sztring                         | A kedvezmény részletei.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| Tulajdonság             | Típus                               | Leírás                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Link](utility-resources.md#link) | A sorelemek lekérésének URI-ját. |
| Önálló                 | [Link](utility-resources.md#link) | Az ön-URI.                       |
