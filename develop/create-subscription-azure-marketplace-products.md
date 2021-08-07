---
title: Előfizetés létrehozása kereskedelmi piactéri termékekhez
description: A fejlesztők a kereskedelmi piactéri termékek előfizetését hozhatják létre és kezelhetik Partnerközpont API-k használatával.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7e7a4b96f509ae99cd4933963c04b0f660d7d76410ee86c31256c62b290f122f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991378"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>Előfizetés létrehozása kereskedelmi piactéri termékekhez

A kereskedelmi piactéri termékekhez előfizetést hozhat létre a Partnerközpont API-k használatával. Le kell [kapnia a piaci](#get-a-list-of-offers-for-a-market)ajánlatok [listáját,](#create-and-submit-an-order) létre kell hoznia és be kell nyújtania egy megrendelést egy kereskedelmi piactér-előfizetéshez, majd le kellkérnie [egy aktiválási hivatkozást.](#get-activation-link)

Ezen előfizetések [életciklus-kezelését](#lifecycle-management) [](#invoice-and-reconciliation) és számláit is kezelheti.

## <a name="prerequisites"></a>Előfeltételek

* [Partnerközpont hitelesítő adatok](partner-center-authentication.md) megadása. Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.
* Az ügyfél azonosítója. Ha nem rendelkezik ügyfélazonosítóval, kövesse az Ügyfelek listájának [lekért lépéseit.](get-a-list-of-customers.md) Másik lehetőségként jelentkezzen be a Partnerközpont, válassza ki az ügyfelet az ügyfelek listájából, válassza a **Fiók** lehetőséget, majd mentse **a Microsoft-azonosítóját.**

## <a name="get-a-list-of-offers-for-a-market"></a>Egy piac ajánlati listájának lekérése

A következő API-modellek használatával ellenőrizheti a piachoz elérhető Partnerközpont:

* **[Termék:](product-resources.md#product)** Egy csoportosító szerkezet a cserélhető termékekhez vagy szolgáltatásokhoz. Maga a termék nem cserélhető elem.
* **[Termékváltozat:](product-resources.md#sku)** Egy termék alatt található, cserélhető készletnyilvántartó egység (SKU). Ezek a termék különböző alakjai.
* **[Rendelkezésre állás:](product-resources.md#availability)** Olyan konfiguráció, amelyben egy termékváltozat megvásárolható (például ország, pénznem vagy iparági szegmens).

Azure-foglalás vásárlása előtt kövesse az alábbi lépéseket:

1. Azonosítsa és lekéri a megvásárolni kívánt terméket és termékváltozatot. Ha már ismeri a termékazonosítót és a termékváltozat-azonosítót, jelölje ki őket.

    * [Termékek listájának lekért listája](get-a-list-of-products.md)
    * [Termék lekérte a termékazonosítót](get-a-product-by-id.md)
    * [Termék termékkel kapcsolatos termékkódok listájának lekért listája](get-a-list-of-skus-for-a-product.md)
    * [Termékváltozat lekérte a termékváltozat azonosítójával](get-a-sku-by-id.md)

    > [!NOTE]
    > A kereskedelmi piactéri termékeket az "Azure" **ProductType** tulajdonsága és az **"SaaS"** **SubType** **tulajdonságuk alapján azonosíthatja.**

2. Ha a termékváltozatok **InventoryCheck előfeltételként** vannak megcímkézve, ellenőrizze a leltárban [a termékváltozatot.](check-inventory.md)

    > [!NOTE]
    > Jelenleg nincsenek olyan kereskedelmi piactéri termékek, amelyek támogatják a leltárellenőrzést, vagy az **InventoryCheck** előfeltételként vannak megjelölve.

3. A termékváltozat rendelkezésre állásának lekérése. A rendelés leadáskor szüksége lesz a rendelkezésre állás **CatalogItemId-jára,** amelyet a következő API-kon keresztül lehet lekérni:

    * [Termékváltozatok rendelkezésre állási listájának lekért listája](get-a-list-of-availabilities-for-a-sku.md)
    * [Rendelkezésre állás le szolgáltatása a rendelkezésre állási azonosítóval](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>Rendelés létrehozása és elküldése

Az Azure-beli foglalási rendelés elküldhez kövesse az alábbi lépéseket:

1. [Hozzon létre egy](create-a-cart.md) kosárt, amely a megvásárolni kívánt katalóguselemek gyűjteményét tartalmazza. Amikor [kosarat](cart-resources.md#cart)hoz [](cart-resources.md#cartlineitem) létre, a rendszer automatikusan csoportosítja a kosársor elemeit az alapján, hogy mi vásárolható meg együtt ugyanabban a [sorrendben.](order-resources.md#order) (Kosarat [is frissíthet.)](update-a-cart.md)
2. [Tekintse meg a kosárban](checkout-a-cart.md)a rendelés [létrehozását.](order-resources.md#order)

### <a name="get-order-details"></a>Megrendelés részleteinek lekérte

A [rendelésazonosítóval lekérheti egy](get-an-order-by-id.md)adott rendelés részleteit. Lekérheti egy adott ügyfél [összes rendelésének listáját is.](get-all-of-a-customer-s-orders.md)

> [!NOTE]
> A rendelés beküldtét követően legfeljebb 15 perces késéssel jelenik meg a rendelés az ügyfél rendelési listájában.

## <a name="get-activation-link"></a>Aktiválási hivatkozás lekérte

A partnernek vagy az ügyfélnek aktiválnia kell az előfizetéseket Azure Marketplace termékekhez. Az [aktiválási hivatkozást a megrendelés soreleme alapján kaphatja meg.](get-activation-link-by-order-line-item.md) Az előfizetés azonosító [alapján is](get-a-subscription-by-id.md)lekért, majd a Links (Hivatkozások) tulajdonság **számbavételével** létrehozhat egy aktiválási hivatkozást.

## <a name="lifecycle-management"></a>Életciklus-kezelés

A kereskedelmi piactéren elérhető termékekre való előfizetések életciklusát a következő módszerekkel kezelheti:

* [Kereskedelmi piactéri előfizetés lemondása](cancel-an-azure-marketplace-subscription.md)
* [A kereskedelmi piactér-előfizetés automatikus újraállításának engedélyezése vagy letiltása](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>Mennyiségkezelés

A kereskedelmi piactér-előfizetések mennyiségének a társított [termékváltozat](product-resources.md#sku) által meghatározott korlátokon belül kell lennie (lásd a **minimumQuantity** és **a maximumQuantity** attribútumokat). A kereskedelmi piactér-előfizetések mennyiségének frissítéséhez használja a következő módszert:

* [Egy előfizetés mennyiségének módosítása](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>Számla és egyeztetés

Az [ügyfélszámlákat](invoice-resources.md) (beleértve a kereskedelmi piactéri termékekre való előfizetések díját) a következő módszerekkel kezelheti:

* [Számlázott kereskedelmi piactéri használatú sorelemek lekért száma](get-invoice-billed-consumption-lineitems.md)
* [Számlabecslés hivatkozásainak lekérése](get-invoice-estimate-links.md)
* [Számlázatlan kereskedelmi piactéri használatú sorelemek lekért száma](get-invoice-unbilled-consumption-lineitems.md)
* [Számlázatlan egyeztetési sorelemek lekért száma](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>Tesztelés integrációs tesztfiókkal

Éles környezetben, miután létrehozott egy előfizetést a kereskedelmi piactéri SaaS-termékekre, le kellkérni egy személyre szabott aktiválási hivatkozást az Partnerközpont-ból, és meg kell látogatnia a közzétevő webhelyét a beállítási folyamat befejezéséhez. Az előfizetés számlázása csak a beállítás befejezése után kezdődik meg.

A CSP-védőkörnyezetben nincs integráció a isv-ekkel. Ha egy aktiválási hivatkozást próbál lekérni a Partnerközpont, a rendszer egy üres hivatkozást ad vissza. Ezzel a hely nélküli hivatkozással nem fejezhető be a telepítési folyamat a közzétevő webhelyén. A kereskedelmi piactéri SaaS-termékekre való előfizetések számlázásának az integrációs tesztfiókkal való teszteléséhez használja a következő módszert az előfizetés aktiválásához. Az előfizetés számlázása a sikeres aktiválás után kezdődik:

* [Sandbox-előfizetés aktiválása kereskedelmi piactéri termékekhez](activate-sandbox-subscription-azure-marketplace-products.md)

