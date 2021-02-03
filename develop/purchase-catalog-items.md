---
title: Katalóguselemek vásárlása
description: Katalógus-elemek vásárlása a partner Center API használatával.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f2b3a34cdb6b29cb7eaaf5d977e4588f538fff09
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767796"
---
# <a name="purchase-catalog-items"></a>Katalóguselemek vásárlása

**A következőkre vonatkozik**

- Partnerközpont

A következő forgatókönyv bemutatja, hogyan vásárolhat elemeket a katalógusból a partner Center API használatával.

## <a name="discovery"></a>Felderítés

Válassza ki a termékeket és az SKU-t, és tekintse meg a rendelkezésre állást a következő partner Center API-modellek használatával

- [Termék](product-resources.md#product) – a megvásárolható termékek vagy szolgáltatások csoportosítási konstrukciója. Egy termék önmagában nem egy megvásárolható tétel.
- [SKU](product-resources.md#sku) – egy terméken belül megvásárolható készlet-tartási egység (SKU). Ezek a termék különböző alakzatait jelölik.
- [Rendelkezésre állás](product-resources.md#availability) – olyan konfiguráció, amelyben az SKU megvásárolható (például ország, pénznem és iparági szegmens).

Ha egy elemet szeretne megvásárolni a katalógusból, hajtsa végre a következő lépéseket:

1. Azonosítsa és kérje le a megvásárolni kívánt terméket és SKU-t.

   - [Termékek listájának lekérése](get-a-list-of-products.md)
   - [Termék beszerzése a termék AZONOSÍTÓjának használatával](get-a-product-by-id.md)
   - [A termékhez tartozó SKU-termékek listájának beolvasása](get-a-list-of-skus-for-a-product.md)
   - [SKU beszerzése az SKU azonosító használatával](get-a-sku-by-id.md)

2. Egy SKU leltárának keresése. Erre a lépésre csak olyan SKU-azonosítók esetében van szükség, amelyek **InventoryCheck** -értékkel vannak megjelölve a [purchasePrerequisites](product-resources.md#sku) tulajdonságban.

   - [Leltár ellenőrzése](check-inventory.md)

3. Az [SKU](product-resources.md#sku) [rendelkezésre állásának](product-resources.md#availability) beolvasása. A megrendelés elhelyezésekor szüksége lesz a rendelkezésre állás **CatalogItemId** . Az érték beszerzéséhez használja a következő API-k egyikét:

   - [Az SKU-ban lévő elérhetőségek listájának lekérése](get-a-list-of-availabilities-for-a-sku.md)
   - [Rendelkezésre állási azonosító használata](get-an-availability-by-id.md)

## <a name="order-submission"></a>Megrendelés beküldése

A katalógus-elemek sorrendjének elküldéséhez tegye a következőket:

1. Hozzon létre egy [cartot](cart-resources.md) a megvásárolni kívánt katalógus-elemek gyűjteményének tárolására. Amikor létrehoz egy kosarat, a rendszer automatikusan csoportosítja a [szekér elemeit](cart-resources.md#cartlineitem) attól függően, hogy mit vásárolhat együtt ugyanabban a [sorrendben](order-resources.md).

   - [Bevásárlókocsi létrehozása](create-a-cart.md)
   - [Bevásárlókocsi frissítése](update-a-cart.md)

2. Látogasson el a kosárba. A kosár megkeresése egy [megrendelés](order-resources.md)létrehozását eredményezi.

   - [A kosár pénztárának kifizetése](checkout-a-cart.md)

## <a name="get-order-details"></a>Megrendelés részleteinek beolvasása

Egy adott megrendelés részleteit a megrendelés AZONOSÍTÓjának használatával kérheti le, vagy megtekintheti az ügyfél rendeléseinek listáját. A megrendelés elküldése és az ügyfél rendeléseinek listájában akár 15 percet is igénybe vehet.

- Tekintse meg az [Order by id beszerzése](get-an-order-by-id.md) című témakört, amely a sorrendi azonosítók használatával beolvassa egy adott megrendelés részleteit.

- Az ügyfél-AZONOSÍTÓval rendelkező ügyfél rendeléseinek megtekintéséhez tekintse [meg az ügyfelek rendeléseinek lekérése](get-all-of-a-customer-s-orders.md) című témakört.

- Tekintse meg az [ügyfelek és a számlázási ciklusok listájának lekérése](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) lehetőséget, hogy lekérje az ügyfél által a [számlázási ciklus típusa](product-resources.md#billingcycletype) alapján megrendelt megrendelések listáját, amely lehetővé teszi, hogy a katalógusbeli elemek rendeléseit (egyszeri díj) és az éves vagy havi számlázott rendeléseket külön adja meg.

## <a name="lifecycle-management"></a>Életciklus-kezelés

A katalógus elemeinek életciklusa kezelésének részeként a partner Centerben lekérheti a katalógus-elemek [jogosultságait](entitlement-resources.md), és lekérheti a foglalás részleteit a foglalási rendelés azonosítójának használatával. Ennek módjáról a [jogosultságok beszerzése](get-a-collection-of-entitlements.md)című témakörben talál példákat.   

## <a name="invoice-and-reconciliation"></a>Számlázás és egyeztetés

A következő forgatókönyvek azt mutatják be, hogyan lehet programozott módon megtekinteni az ügyfél [számláit](invoice-resources.md), és beolvasni a fiók egyenlegeit és összegzéseit, amelyek tartalmazzák a katalógus-elemek egyszeri díját.

### <a name="balance-and-payment"></a>Egyenleg és fizetés

Az aktuális fiók egyenlegének alapértelmezett pénznemben való lekéréséhez, amely az ismétlődő és egyszeri (katalógus-) díjak egyenlege, lásd: [az aktuális fiók egyenlegének beolvasása](get-the-reseller-s-current-account-balance.md).

### <a name="multi-currency-balance-and-payment"></a>Több pénznemre kiterjedő egyenleg és fizetés

Az aktuális fiók egyenlegének beszerzéséhez, valamint a számla összegzésének összefoglalásához, amely tartalmazza az egyes ügyfelek pénznem-típusaira vonatkozó ismétlődő és egyszeri díjat is, tekintse meg a [számla összegzésének beolvasása](get-invoice-summaries.md)című témakört.

### <a name="invoices"></a>Számlák

Az ismétlődő és egyszeri díjat is tartalmazó számlák gyűjteményének beszerzéséhez tekintse meg a következő témakört: [számlák gyűjteményének beolvasása](get-a-collection-of-invoices.md). 

### <a name="single-invoice"></a>Egyetlen számla

Ha a számla AZONOSÍTÓjának használatával szeretne beolvasni egy adott számlát, tekintse meg a [számla beszerzése azonosító alapján](get-invoice-by-id.md)című témakört.  

### <a name="reconciliation"></a>Licencegyeztetési

A számlasor-elemek részleteinek (egyeztetési sorok) egy adott AZONOSÍTÓhoz tartozó gyűjteményének lekéréséhez tekintse meg a [Számlázási sorok beolvasása](get-invoiceline-items.md)című cikket.  

### <a name="download-an-invoice-as-a-pdf"></a>Számla letöltése PDF-ként

Ha a számla AZONOSÍTÓjának használatával szeretne beolvasni egy számlafogadó-utasítást a PDF-űrlapon, olvassa el a [Számlakivonat beolvasása](get-invoice-statement.md)című témakört.
