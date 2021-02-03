---
title: Szolgáltatási költségek erőforrásai
description: Az ügyfél által vásárolt szolgáltatásokhoz kapcsolódó erőforrásokat ismerteti.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c0236329d93d8ddc9019a15fb67a81a3af3e7620
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768007"
---
# <a name="service-costs-resources"></a>Szolgáltatási költségek erőforrásai

**A következőkre vonatkozik:**

- Partnerközpont

Az ügyfél által vásárolt szolgáltatásokhoz kapcsolódó erőforrásokat ismerteti.

## <a name="servicecostssummary"></a>ServiceCostsSummary

A **ServiceCostsSummary** olyan összegzést tartalmaz, amely összesíti az adott ügyfél által a számlázási időszakban megvásárolt összes szolgáltatást.

| Tulajdonság | Típus | Leírás |
| -------- | ---- | ----------- |
| Részletek | [ServiceCostsSummaryDetail](#servicecostssummarydetail) objektumok tömbje | A szolgáltatási díj összegzésének részletes listája, a számla típusa szerint megkülönböztetve.|
| linkek | [ResourceLinks](utility-resources.md#resourcelinks) | Az erőforrás-hivatkozások. |
| attribútumok | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai. |

> [!IMPORTANT]
> **A következő táblázat mezői elavultak.** Az ismétlődő és az egyszeri szolgáltatás díjszabásának beolvasásához használja helyette a **részletek** mezőt. A **részletek** mezőt az előző táblázat ismerteti. Tekintse meg a **részletek** mező megfelelő adatértékeit, de ne a legfelső szintű mezőket.

| Tulajdonság | Típus | Leírás |
| -------- | ---- | ----------- |
| billingStartDate | dátum | A számlázási időszak kezdete. |
| billingEndDate | dátum | A számlázási időszak vége. |
| pretaxTotal | double | Az ügyfélre vonatkozó összes költség előadójának összege. |
| Tax  | double | Az ügyfél által megvásárolt összes elemre felmerült teljes adó. |
| afterTaxTotal | double | Az ügyfél által vásárolt összes elem nettó teljes költsége. |
| currencyCode | sztring | A költségekhez használt pénznemet jelöli. |
| currencySymbol | sztring | A költségekhez használt pénznem szimbóluma. |
| customerId | sztring | Annak az ügyfélnek az azonosítója, amely a vásárlást készíti. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

A **ServiceCostsSummaryDetail** leírja a szolgáltatási díjak összegzését, amely összegzi a megadott ügyfél által a számlázási időszakban megvásárolt összes szolgáltatást (ismétlődő vagy egyszeri számlákból).

| Tulajdonság | Típus | Leírás |
| -------- | ---- | ----------- |
| invoiceType | sztring | Az a invoiceType, amelybe a szolgáltatás díjainak összegzése létrejött. |
| összegzés | [ServiceCostsSummary](#servicecostssummary) | A szolgáltatáshoz tartozó, egyetlen számla típusú ügyfél által összesített szolgáltatási díj összegzése. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

A **ServiceCostLineItem** az ügyfél által megvásárolt egyetlen tételt ismerteti.

> [!IMPORTANT]
> A következő tulajdonságok *csak* a Service Cost line-elemekre vonatkoznak, ahol a termék *egyszeri vásárlás*: **Termékkód**, **productName**, **SkuID**, **skuName**, **availabilityId**, **publisherId**, **közzétevő neve**, **termAndBillingCycle**, **discountDetails**. Ezek a tulajdonságok *nem vonatkoznak* azokra a szervizsorok elemekre, amelyekben a termék *ismétlődő vásárlás*. Ezek a tulajdonságok például *nem vonatkoznak* az előfizetés-alapú Office 365-re és az Azure-ra.

| Tulajdonság                 | Típus                           | Leírás                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| startDate                | karakterlánc UTC dátum-idő formátumban | A díj kezdő dátuma.                                       |
| endDate                  | karakterlánc UTC dátum-idő formátumban | A díj befejezési dátuma.                                         |
| subscriptionFriendlyName | sztring                         | Az előfizetés rövid neve.                              |
| subscriptionId           | sztring                         | Az előfizetés azonosítója.                                         |
| Rendeléskód                  | sztring                         | A sorrend azonosítója.                                                |
| offerId                  | sztring                         | Az ajánlat azonosítója.                                                |
| offerName                | sztring                         | Az ajánlat neve.                                                      |
| resellerMPNId            | sztring                         | Csak kétrétegű partneri forgatókönyvekben használatos. Az MPN-azonosítóra hivatkozik. |
| chargeType               | sztring                         | A társított díj típusa.                                          |
| quantity                 | szám                         | A felhasznált vagy megvásárolt egységek mennyisége.                             |
| unitPrice                | szám                         | Az egységenkénti díj.                                                  |
| pretaxTotal              | szám                         | Az adott tételre vonatkozó teljes díj az adók előtt.                         |
| Tax                      | szám                         | Az adott elemmel kapcsolatban felmerülő teljes adófizetési díj.                         |
| afterTaxTotal            | szám                         | Az adott tételhez tartozó nettó összköltség.                                    |
| currencyCode             | sztring                         | A költségekhez használt pénznemet jelöli.                          |
| currencySymbol           | sztring                         | A költségekhez használt pénznem szimbóluma.                              |
| customerId               | sztring                         | Annak az ügyfélnek az azonosítója, amely a vásárlást készíti.                          |
| Customername (             | sztring                         | Annak az ügyfélnek a neve, amely a vásárlást készíti.                        |
| invoiceNumber            | sztring                         | Annak a számlának a száma, amelyhez ez a tétel tartozik.                   |
| productId                | sztring                         | A termék azonosítója.                                              |
| skuId                    | sztring                         | Az SKU azonosítója.                                                  |
| availabilityId           | sztring                         | A rendelkezésre állás azonosítója.                                         |
| productName              | sztring                         | A termék neve.                                                    |
| skuName                  | sztring                         | Az SKU neve.                                                        |
| publisherName            | sztring                         | A közzétevő neve.                                                  |
| publisherId              | sztring                         | A közzétevő azonosítója.                                            |
| termAndBillingCycle      | sztring                         | A kifejezés és a számlázási ciklus.                                          |
| discountDetails          | sztring                         | A kedvezmény részletei.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| Tulajdonság             | Típus                               | Leírás                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Hivatkozás](utility-resources.md#link) | A sorok beolvasására szolgáló URI. |
| önálló                 | [Hivatkozás](utility-resources.md#link) | A saját URI-ja.                       |
