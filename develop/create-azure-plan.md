---
title: Azure-csomag létrehozása
description: A fejlesztők programozott módon vásárolhatják meg, hozhatják létre és kezelhetik az Azure-terveket a partner Center API-k használatával.
ms.date: 01/02/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: mowrim
ms.author: mowrim
ms.openlocfilehash: 372b94ac7217899ca560cf943bf11a7e8906872d
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768084"
---
# <a name="create-an-azure-plan"></a>Azure-csomag létrehozása

**A következőkre vonatkozik:**

* Partnerközpont

Az Azure-csomagokat a partner Center API-k használatával vásárolhatja meg, hozhatja létre és kezelheti. A folyamat hasonló a Microsoft Azure (MS-AZR-0145P) előfizetés létrehozásához. Be kell [szereznie az Azure-csomag katalógusának elemét](#get-the-catalog-item-for-azure-plan), majd [létre kell hoznia és el kell küldenie egy rendelést](#create-and-submit-an-order).

## <a name="prerequisites"></a>Előfeltételek

* A [partner központ hitelesítési](partner-center-authentication.md) hitelesítő adatai. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.
* Az ügyfél-azonosító. Ha nem rendelkezik ügyfél-azonosítóval, kövesse az [ügyfelek listájának beolvasása](get-a-list-of-customers.md)című témakör lépéseit. Másik lehetőségként jelentkezzen be a partner Centerbe, válassza ki az ügyfelet az ügyfelek listájáról, válassza a **fiók** lehetőséget, majd mentse a **Microsoft-azonosítóját**.
* A [Microsoft ügyfél-szerződés elfogadásának megerősítése](/partner-center/confirm-customer-agreement).

## <a name="get-the-catalog-item-for-azure-plan"></a>Az Azure-csomag katalógusának beolvasása

Ahhoz, hogy egy ügyfél számára Azure-csomagot lehessen létrehozni, le kell kérnie a megfelelő katalógusfájlt. A katalógus-elemet a meglévő partner Center Catalog API-k használatával kérheti le a következő erőforrás-modellekkel.

* **[Termék](product-resources.md#product)**: csoportosítható szerkezet a megvásárolható termékekhez vagy szolgáltatásokhoz. Egy termék nem egy megvásárolható tétel.
* **[SKU](product-resources.md#sku)**: egy terméken belül megvásárolható készlet-megőrzési egység (SKU). A SKU a termék különböző alakzatait jelöli.
* **[Rendelkezésre állás](product-resources.md#availability)**: olyan konfiguráció, amelyben az SKU megvásárolható (például ország, pénznem vagy iparági szegmens).

Az Azure-csomag katalógusának beszerzéséhez hajtsa végre a következő lépéseket:

1. Az Azure-csomag *termékazonosítójának* azonosítása és beolvasása. Kövesse a [termékek listájának lekérése](get-a-list-of-products.md) és a **targetView** **MicrosoftAzure** szerinti megadásának lépéseit. (Ha már ismeri az Azure-csomag *termékazonosítóját* , kövesse a [termék beolvasása a termék azonosítójának használatával](get-a-product-by-id.md) című témakör lépéseit.)

2. Kérje le az **SKU** -t a termékből az Azure-csomagból. Kövesse a [termékhez tartozó SKU-termékek listájának beolvasása](get-a-list-of-skus-for-a-product.md)című témakör lépéseit. Ha már ismeri az Azure-csomag SKU-azonosítóját, kövesse az [SKU beszerzése az SKU-azonosító használatával](get-a-sku-by-id.md) című szakasz lépéseit.

3. Az Azure-csomaghoz tartozó SKU **rendelkezésre állásának** beolvasása. Kövesse a következő témakört: az SKU-ban található [elérhetőségek listájának beolvasása](get-a-list-of-availabilities-for-a-sku.md). Ha már ismeri a szükséges rendelkezésre állás azonosítóját, kövesse a rendelkezésre állás [beszerzése](get-an-availability-by-id.md) a rendelkezésre ÁLLÁSi azonosítóval című szakasz lépéseit. *Ügyeljen arra, hogy az Azure-csomag rendelkezésre állásának **CatalogItemId** tulajdonságának értékét jegyezze fel. A megrendelés létrehozásához szüksége lesz erre az értékre.*

## <a name="create-and-submit-an-order"></a>Megrendelés létrehozása és elküldése

Az Azure-csomag megrendelésének elküldéséhez kövesse az alábbi lépéseket:

1. [Hozzon létre egy cartot](create-a-cart.md) a megvásárolni kívánt katalógus-elemek gyűjteményének tárolására. Amikor létrehoz egy [kosarat](cart-resources.md#cart), a rendszer automatikusan csoportosítja a [szekér elemeit](cart-resources.md#cartlineitem) attól függően, hogy mit vásárolhat együtt ugyanabban a [sorrendben](order-resources.md#order). ( [A kosár frissítését](update-a-cart.md)is végezheti.)

2. [Tekintse meg a kosárt](checkout-a-cart.md), amely egy [megrendelés](order-resources.md#order)létrehozását eredményezi.

## <a name="get-order-details"></a>Megrendelés részleteinek beolvasása

[Egy adott megrendelés részleteit a megrendelés azonosítójának használatával](get-an-order-by-id.md)kérheti le. Egy [adott ügyfélhez tartozó összes megrendelés listáját](get-all-of-a-customer-s-orders.md)is lekérheti.

>[!NOTE]
>Egy megrendelés elküldése után akár 15 percet is igénybe vehet, mielőtt a megrendelés megjelenik az ügyfél rendelési listájában.

## <a name="manage-azure-plans"></a>Azure-csomagok kezelése

A megrendelés sikeres feldolgozása után létrejön egy partner Center- **előfizetési** erőforrás az Azure-csomaghoz. A következő módszerekkel kezelheti a partneri központ **előfizetési** erőforrásait az Azure-csomag kezeléséhez:

* [Egy ügyfél előfizetéseinek lekérése](get-all-of-a-customer-s-subscriptions.md)
* [Az előfizetések listájának lekérése megrendelés alapján](get-a-list-of-subscriptions-by-order.md)

Ha létrejön egy Azure-csomag a partner Centerben, a rendszer az Azure-ban is létrehoz egy megfelelő Azure-használati előfizetést. Az Azure Portal és az Azure API-k használatával további Azure-használati előfizetéseket is létrehozhat ugyanazon Azure-csomag keretében. Az Azure-csomaghoz társított Azure-használati előfizetések azonosítóit az Azure-beli [jogosultságok listájának lekérése a partner Center-előfizetéshez](get-a-list-of-azure-entitlements-for-subscription.md) című cikkben ismertetett lépéseket követve szerezheti be

## <a name="lifecycle-management"></a>Életciklus-kezelés

Egy meglévő Azure-csomag felfüggesztéséhez kövesse az [előfizetés felfüggesztése](suspend-a-subscription.md)című témakör lépéseit.

*Csak akkor lehet felfüggeszteni egy meglévő Azure-csomagot, ha már nincs hozzá társítva aktív használati eszköz, beleértve az Azure-használati előfizetéseket és az Azure-foglalásokat.*

Az Azure-használati előfizetések letiltásával kapcsolatos további információkért lásd: [Azure API az előfizetés életciklusának kezelésében](/rest/api/resources/subscriptions).

A meglévő Azure-foglalások eltávolításához le kell [mondania a foglalásokat](/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation).
Az Azure-csomag felfüggesztését követően újra aktiválhatja.

Az Azure-csomag újraaktiválásával kapcsolatos további információkért lásd [a felfüggesztett előfizetés újraaktiválását](reactivate-a-suspended-a-subscription.md) ismertető témakört.

## <a name="transition-existing-csp-offers-to-azure-plan"></a>Meglévő CSP-ajánlatok átváltása Azure-csomagra 

Nem hozhat létre Azure-csomagot Microsoft Azure- (MS-AZR-0145P) előfizetéssel rendelkező meglévő ügyfél esetében. [Meglévő CSP Azure-ajánlatokból azonban átvihet ügyfeleket Azure-szolgáltatásokba az Azure-csomag keretében](/partner-center/azure-plan-transition) a Partnerközpontban elérhető CSP-program új kereskedelmi felületén. Meglévő ügyfél átviteléhez használja a termékfrissítési API-kat a következő lépések végrehajtásával:

* [Ellenőrizze, hogy az ügyfél jogosult-e az Azure-csomagra való váltásra](get-eligibility-for-product-upgrade.md)
* [Kezdeményezzen termékfrissítést az ügyfél esetében](create-product-upgrade-entity.md)
* [Ellenőrizze a termékfrissítés állapotát](get-product-upgrade-status.md)

## <a name="azure-spending"></a>Azure-költség

Az Azure- [kiadások](azure-spending.md) nyomon követéséhez a használati Összegzés és a részletes használati adatok lekérdezésével a következő módszerek használhatók:

* [A partner használati összegzésének lekérése](get-a-partner-usage-summary.md)
* [Egy partner összes ügyfélhasználati rekordjának lekérése](get-a-customer-s-usage-records.md)
* [Az ügyfél használati összegzésének lekérése](get-a-customer-usage-summary.md)
* [Egy ügyfél összes előfizetés-használati rekordjának lekérése](get-a-customer-subscription-s-usage-records.md)
* [Az előfizetés használati összegzésének lekérése](get-a-customer-subscription-usage-summary.md)
* [Előfizetés használati adatainak lekérése erőforrás szerint](get-a-customer-subscription-resource-usage-records.md)
* [Előfizetés használati adatainak lekérése mérő szerint](get-a-customer-subscription-meter-usage-records.md)
* [Mérőhasználati rekord erőforrásainak lekérése](meter-usage-resources.md)
* [Erőforrás-használati rekord erőforrásainak lekérése](resource-usage-resources.md)

Az ügyfél-használati költségvetést a következő módszerekkel is beállíthatja és kezelheti:

* [Az ügyfél használatalapú költségvetésének lekérése](get-a-customer-s-usage-spending-budget.md)
* [Az ügyfél használatalapú költségvetésének frissítése](update-a-customer-s-usage-spending-budget.md)

## <a name="invoice-and-reconciliation"></a>Számlázás és egyeztetés

A következő módszerekkel kezelheti a számlákat és az egyeztetési műveleteket:

* [Számlák gyűjteményének lekérése](get-a-collection-of-invoices.md)
* [Számlabecslés hivatkozásainak lekérése](get-invoice-estimate-links.md)
* [Számla beolvasása azonosító alapján](get-invoice-by-id.md)
* [Számlakivonat lekérése](get-invoice-statement.md)
* [Számla összegzéseinek lekérése](get-invoice-summaries.md)
* [Számlázott használatalapú sorelemek lekérése](get-invoice-billed-consumption-lineitems.md)
* [Nem számlázott használatalapú sorelemek lekérése](get-invoice-unbilled-consumption-lineitems.md)
* [Számlázott kiszámlázott Recon-sorok beolvasása](get-invoiceline-items.md)
* [Nem számlázott egyeztetési sorelemek lekérése](get-invoice-unbilled-recon-lineitems.md)
