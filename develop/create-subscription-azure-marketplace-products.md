---
title: Előfizetés létrehozása kereskedelmi Piactéri termékekhez
description: A fejlesztők a partner Center API-k használatával hozhatnak létre és kezelhetnek előfizetéseket kereskedelmi Piactéri termékekhez.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df2a3707e00ba36a11c404b102304c08d105244e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767748"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>Előfizetés létrehozása kereskedelmi Piactéri termékekhez

**A következőkre vonatkozik:**

* Partnerközpont

A partner Center API-k használatával előfizetést hozhat létre kereskedelmi piactér-termékekhez. Meg kell [kapnia a piac ajánlatait](#get-a-list-of-offers-for-a-market), létre kell [hoznia és el kell küldenie](#create-and-submit-an-order) egy kereskedelmi piactér-előfizetés rendelését, majd be kell szereznie egy [aktiválási hivatkozást](#get-activation-link).

Az előfizetések esetében is [elvégezheti az életciklus-kezelést](#lifecycle-management) és a [számlák kezelését](#invoice-and-reconciliation) .

## <a name="prerequisites"></a>Előfeltételek

* A [partner központ hitelesítési](partner-center-authentication.md) hitelesítő adatai. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.
* Az ügyfél-azonosító. Ha nem rendelkezik ügyfél-azonosítóval, kövesse az [ügyfelek listájának beolvasása](get-a-list-of-customers.md)című témakör lépéseit. Másik lehetőségként jelentkezzen be a partner Centerbe, válassza ki az ügyfelet az ügyfelek listájáról, válassza a **fiók** lehetőséget, majd mentse a **Microsoft-azonosítóját**.

## <a name="get-a-list-of-offers-for-a-market"></a>Egy piac ajánlati listájának lekérése

A piacon elérhető ajánlatokat a következő partner Center API-modellek segítségével tekintheti meg:

* **[Termék](product-resources.md#product)**: csoportosítható szerkezet a megvásárolható termékekhez vagy szolgáltatásokhoz. Egy termék nem egy megvásárolható tétel.
* **[SKU](product-resources.md#sku)**: egy terméken belül megvásárolható készlet-megőrzési egység (SKU). Ezek a termék különböző alakzatait jelölik.
* **[Rendelkezésre állás](product-resources.md#availability)**: olyan konfiguráció, amelyben az SKU megvásárolható (például ország, pénznem vagy iparági szegmens).

Az Azure-foglalás megvásárlása előtt végezze el a következő lépéseket:

1. Azonosítsa és kérje le a megvásárolni kívánt terméket és SKU-t. Ha már ismeri a termék AZONOSÍTÓját és az SKU AZONOSÍTÓját, válassza ki őket.

    * [Termékek listájának lekérése](get-a-list-of-products.md)
    * [Termék beszerzése a termék AZONOSÍTÓjának használatával](get-a-product-by-id.md)
    * [A termékhez tartozó SKU-termékek listájának beolvasása](get-a-list-of-skus-for-a-product.md)
    * [SKU beszerzése az SKU azonosító használatával](get-a-sku-by-id.md)

    > [!NOTE]
    > Az **"Azure"** **ProductType** -tulajdonsága és a **"Saas"** **altípus** -tulajdonsága alapján azonosíthatók a kereskedelmi piactéren elérhető termékek.

2. Ha az SKU- **InventoryCheck** előfeltételként van megjelölve, [ellenőrizze az SKU leltárát](check-inventory.md).

    > [!NOTE]
    > Jelenleg nincs olyan kereskedelmi piactér-termék, amely támogatja a leltár-ellenőrzés használatát, vagy **InventoryCheck** előfeltételként van megjelölve.

3. Az SKU rendelkezésre állásának beolvasása. A megrendelés elhelyezésekor szüksége lesz a rendelkezésre állás **CatalogItemId** , amelyet a következő API-kkal kérhet le:

    * [Az SKU-ban lévő elérhetőségek listájának lekérése](get-a-list-of-availabilities-for-a-sku.md)
    * [Rendelkezésre állási azonosító használata](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>Megrendelés létrehozása és elküldése

Az Azure foglalási sorrendjének elküldéséhez kövesse az alábbi lépéseket:

1. [Hozzon létre egy cartot](create-a-cart.md) a megvásárolni kívánt katalógus-elemek gyűjteményének tárolására. Amikor létrehoz egy [kosarat](cart-resources.md#cart), a rendszer automatikusan csoportosítja a [szekér elemeit](cart-resources.md#cartlineitem) attól függően, hogy mit vásárolhat együtt ugyanabban a [sorrendben](order-resources.md#order). ( [A kosár frissítését](update-a-cart.md)is végezheti.)
2. [Tekintse meg a kosárt](checkout-a-cart.md), amely egy [megrendelés](order-resources.md#order)létrehozását eredményezi.

### <a name="get-order-details"></a>Megrendelés részleteinek beolvasása

[Egy adott megrendelés részleteit a megrendelés azonosítójának használatával](get-an-order-by-id.md)kérheti le. Egy [adott ügyfélhez tartozó összes megrendelés listáját](get-all-of-a-customer-s-orders.md)is lekérheti.

> [!NOTE]
> Egy megrendelés elküldése után akár 15 percet is igénybe vehet, mielőtt a megrendelés megjelenik az ügyfél rendelési listájában.

## <a name="get-activation-link"></a>Aktiválási hivatkozás beolvasása

A partnernek vagy az ügyfélnek aktiválnia kell az Azure Marketplace-termékek előfizetéseit. [Az aktiválási hivatkozást megrendelési sor elem alapján](get-activation-link-by-order-line-item.md)kérheti le. Az [előfizetést azonosító alapján](get-a-subscription-by-id.md)is lekérheti, majd a **hivatkozások** tulajdonság enumerálásával létrehozhatja az aktiválási hivatkozást.

## <a name="lifecycle-management"></a>Életciklus-kezelés

Az előfizetések életciklusát a kereskedelmi piactér termékeire a következő módszerekkel kezelheti:

* [Kereskedelmi piactéri előfizetés lemondása](cancel-an-azure-marketplace-subscription.md)
* [A kereskedelmi piactér-előfizetés engedélyezése vagy letiltása](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>Mennyiségi felügyelet

A kereskedelmi piactér-előfizetés mennyiségének a társított [SKU](product-resources.md#sku) által meghatározott korlátokon belül kell lennie (lásd a **MinimumQuantity** és a **maximumQuantity** attribútumokat). A kereskedelmi piactér-előfizetés mennyiségének frissítéséhez használja a következő metódust:

* [Egy előfizetés mennyiségének módosítása](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>Számlázás és egyeztetés

A következő módszerekkel kezelheti az ügyfelek [számláit](invoice-resources.md) (beleértve a kereskedelmi piactér termékeire vonatkozó előfizetések díját is):

* [Számlázott kereskedelmi piactér-felhasználási sorok számlájának beolvasása](get-invoice-billed-consumption-lineitems.md)
* [Számlabecslés hivatkozásainak lekérése](get-invoice-estimate-links.md)
* [Számlázott kereskedelmi piactér-felhasználási sorok számlázása](get-invoice-unbilled-consumption-lineitems.md)
* [Számlázással kapcsolatos nem számlázott egyeztetési sorok beolvasása](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>Tesztelés integrációs homokozó-fiók használatával

Éles környezetben, miután létrehozta a kereskedelmi Marketplace SaaS-termékek előfizetését, egy személyre szabott aktiválási hivatkozást kell lekérnie a partner Center webhelyről, és el kell végeznie a közzétevő helyét a telepítési folyamat befejezéséhez. Az előfizetés számlázása csak a telepítés befejeződése után kezdődik.

A CSP homokozó környezetében nincs integráció az ISV-val. Ha a partner Centerből próbál meg beolvasni egy aktiválási hivatkozást, a rendszer egy dummy-hivatkozást ad vissza. Ez a dummy-hivatkozás nem használható a telepítési folyamat befejezéséhez a közzétevő webhelyén. Ha az Integration sandbox-fiókot szeretné használni a kereskedelmi Marketplace SaaS-termékek előfizetések számlázásának teszteléséhez, használja a következő módszert az előfizetés aktiválásához. Az előfizetés számlázása a sikeres aktiválás után kezdődik:

* [Homokozó elvű előfizetés aktiválása kereskedelmi piactér-termékekhez](activate-sandbox-subscription-azure-marketplace-products.md)

