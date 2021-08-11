---
title: Katalóguselemek vásárlása
description: Katalóguselemek vásárlása a Partnerközpont API-val.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 34560ceff2721a805d50cd4bf0702f6e7cf6f473db3f38ee52ea439b7355b786
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997338"
---
# <a name="purchase-catalog-items"></a>Katalóguselemek vásárlása

A következő forgatókönyv azt az általános folyamatot mutatja be, amikor a termékkatalógusból vásárolnak elemeket a Partnerközpont API-val.

## <a name="discovery"></a>Felderítés

Válassza a termékek és a termékkódok (SKUs) lehetőséget, és ellenőrizze azok rendelkezésre állását az alábbi Partnerközpont API-modellekkel:

- [Termék](product-resources.md#product) – A cserélhető termékek vagy szolgáltatások csoportosítási konstrukciója. A termék önmagában nem cserélhető elem.
- [Termékváltozat](product-resources.md#sku) – Egy terméken elérhető SKU. Ezek a termék különböző alakjai.
- [Rendelkezésre állás](product-resources.md#availability) – Olyan konfiguráció, amelyben egy termékváltozat megvásárolható (például ország, pénznem és iparági szegmens).

Ha egy elemet meg kell vásárolnia a katalógusból, kövesse az alábbi lépéseket:

1. Azonosítsa és lekéri a megvásárolni kívánt terméket és termékváltozatot.

   - [Termékek listájának lekért listája](get-a-list-of-products.md)
   - [Termék lekérte a termékazonosítót](get-a-product-by-id.md)
   - [Termék termék termékterméklistáinak lekért listája](get-a-list-of-skus-for-a-product.md)
   - [Termékváltozat lekérte a termékváltozat azonosítóját használva](get-a-sku-by-id.md)

2. Ellenőrizze a leltárban, hogy van-e termékváltozat. Erre a lépésre csak az **InventoryCheck** értékkel felcímkézett termékkódok esetén van szükség a [purchasePrerequisites tulajdonságban.](product-resources.md#sku)

   - [Leltár ellenőrzése](check-inventory.md)

3. A [termékváltozat rendelkezésre](product-resources.md#availability) [állásának lekérése.](product-resources.md#sku) A rendelés leadáskor szüksége lesz a rendelkezésre állás **CatalogItemId-ére.** Ezt az értéket a következő API-k egyikével használhatja:

   - [Termékváltozatok rendelkezésre állási listájának lekért listája](get-a-list-of-availabilities-for-a-sku.md)
   - [Rendelkezésre állás le szolgáltatása a rendelkezésre állási azonosítóval](get-an-availability-by-id.md)

## <a name="order-submission"></a>Rendelés beküldve

A katalóguselem-rendelés elküldhez tegye a következőket:

1. Hozzon létre [egy](cart-resources.md) kosárt, amely a megvásárolni kívánt katalóguselemek gyűjteményét tartalmazza. Amikor kosarat hoz [](cart-resources.md#cartlineitem) létre, a rendszer automatikusan csoportosítja a kosársor elemeit az alapján, hogy mi vásárolható együtt ugyanabban a [rendelésben.](order-resources.md)

   - [Bevásárlókocsi létrehozása](create-a-cart.md)
   - [Bevásárlókocsi frissítése](update-a-cart.md)

2. Nézze meg a kosárt. Ha kiveszi a kosárból a rendelést, a rendelés is [létre lesz hozva.](order-resources.md)

   - [A kosár kiveszi a kosárból](checkout-a-cart.md)

## <a name="get-order-details"></a>Rendelés részleteinek lekérte

Lekérheti egy adott rendelés részleteit a rendelés azonosítójával, vagy lekérheti egy ügyfél megrendelési listáját. A rendelés elküldés és az ügyfél rendelési listájában való megjelenése között akár 15 perces késés is lehet.

- A [rendelésazonosítók használatával](get-an-order-by-id.md) az egyes rendelésekkel kapcsolatos részletekért lásd: Rendelés lekért azonosítója.

- Az [ügyfélazonosítót](get-all-of-a-customer-s-orders.md) használó ügyfél megrendelési listájának lekért listájáért lásd az ügyfél összes rendelésének lekért listáját.

- A [rendelések ügyfél-](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) és számlázásiciklus-típusonkénti listájának lekért [](product-resources.md#billingcycletype) listája az ügyfélhez tartozó számlázási ciklus típusa szerint, amely lehetővé teszi a katalóguselem-rendelések (egyszeres díjak) és az éves vagy havi számlázt rendelések külön-külön való felsorolását.

## <a name="lifecycle-management"></a>Életciklus-kezelés

A katalóguselemek életciklusának a Partnerközpont-ban való kezelésének részeként lekérheti a [](entitlement-resources.md)katalóguselem jogosultságai adatait, és lekérheti a foglalás részleteit a foglalási rendelés azonosítójával. Ennek mikéntjére vonatkozó példákért lásd: [Get entitlements (Jogosultságok lekérte).](get-a-collection-of-entitlements.md)   

## <a name="invoice-and-reconciliation"></a>Számla és egyeztetés

A következő forgatókönyvek azt mutatják be, hogyan [](invoice-resources.md)lehet programozott módon megtekinteni az ügyfél számláit, és lekérte a fiókegyenlegeket és összegzéseket, amelyek a katalóguselemekre vonatkozó egyszeres díjakat tartalmaznak.

### <a name="balance-and-payment"></a>Egyenleg és kifizetés

Az aktuális számlaegyenleg az ismétlődő és egyszeri (katalóguselem) díjak egyenlegét is elegyenő alapértelmezett pénznemben való lekértért lásd: Az aktuális számlaegyenleg [lekért egyenlege.](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Több pénznem egyenlege és kifizetése

Az aktuális számlaegyenleg és a számlaösszegzéseket tartalmazó számlaösszegzések ismétlődő és egyszeri díjakat tartalmazó gyűjteményét az egyes ügyfelek pénznemtípusával kapcsolatos ismétlődő és egyszeri díjakkal együtt lásd: Számlaösszegzések [lekérte.](get-invoice-summaries.md)

### <a name="invoices"></a>Számlák

Az ismétlődő és egyszeri díjakat is bemutató számlák gyűjteményének legyűjtéséhez [lásd: Számlák gyűjteményének begyűjtése.](get-a-collection-of-invoices.md) 

### <a name="single-invoice"></a>Egyetlen számla

Egy adott számla számlaazonosítóval való lekérését lásd: [Számla lekérése azonosító alapján.](get-invoice-by-id.md)  

### <a name="reconciliation"></a>Egyeztetés

Egy adott számlaazonosító számlasorelem-részleteinek (egyeztetési sorelemek) gyűjteményét lásd: [Számlasorelemek begyűjtése.](get-invoiceline-items.md)  

### <a name="download-an-invoice-as-a-pdf"></a>Számla letöltése PDF-fájlként

A számlakivonat PDF formátumban, számlaazonosítóval való lekéréséhez lásd: [Számlakivonat lekérése.](get-invoice-statement.md)
