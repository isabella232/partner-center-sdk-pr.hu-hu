---
title: Azure-csomag létrehozása
description: A fejlesztők programozott módon vásárolhatnak, hozhatnak létre és kezelhet Azure-csomagokat Partnerközpont API-k használatával.
ms.date: 07/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: mowrim
ms.author: mowrim
ms.openlocfilehash: 5083f7aa8ea274b5210d88085d26376dadbc0c4d1a0dd6e1babe59c94d7a6f9c
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991480"
---
# <a name="create-an-azure-plan"></a>Azure-csomag létrehozása

Azure-csomagokat vásárolhat, hozhat létre és kezelhet a Partnerközpont API-k használatával. A folyamat hasonló a Microsoft Azure ([MS-AZR-0145P](https://go.microsoft.com/fwlink/p/?linkid=2164140)) előfizetés létrehozásához. Be kell [szereznie az Azure-csomag katalóguselemét,](#get-the-catalog-item-for-azure-plan)majd létre kell [hoznia és el kell küldenie egy megrendelést.](#create-and-submit-an-order)

## <a name="prerequisites"></a>Előfeltételek

* [Partnerközpont hitelesítő adatok](partner-center-authentication.md) megadása. Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.
* Az ügyfél azonosítója. Ha nem rendelkezik ügyfélazonosítóval, kövesse az Ügyfelek listájának [lekért lépéseit.](get-a-list-of-customers.md) Másik lehetőségként jelentkezzen be a Partnerközpont, válassza ki az ügyfelet az ügyfelek listájából, válassza a **Fiók** lehetőséget, majd mentse **a Microsoft-azonosítóját.**
* [Annak megerősítése, hogy az](/partner-center/confirm-customer-agreement)ügyfél elfogadta a Microsoft Ügyfélszerződés.

## <a name="get-the-catalog-item-for-azure-plan"></a>Az Azure-csomag katalóguselemének lekért része

Ahhoz, hogy Azure-csomagokat hoz létre egy ügyfél számára, le kellkérni a megfelelő katalóguselemet. A katalóguselemet a meglévő katalógus API Partnerközpont a következő erőforrásmodellekkel lehet lekérni.

* **[Termék:](product-resources.md#product)** Egy csoportosító szerkezet a cserélhető termékekhez vagy szolgáltatásokhoz. Maga a termék nem cserélhető elem.
* **[Termékváltozat:](product-resources.md#sku)** Egy termék alatt található, cserélhető készletnyilvántartó egység (SKU). A termék termékkódok a termék különböző alakjai.
* **[Rendelkezésre állás:](product-resources.md#availability)** Olyan konfiguráció, amelyben egy termékváltozat megvásárolható (például ország, pénznem vagy iparági szegmens).

Egy Azure-csomag katalóguselemének beszerzéséhez kövesse az alábbi lépéseket:

1. Azonosítsa és lekéri *az* Azure-csomag termékazonosítóját. Kövesse a [Termékek listájának lekért lépéseit,](get-a-list-of-products.md) és adja meg a **targetView** értéket **MicrosoftAzure-ként.** (Ha már ismeri  az Azure-csomag termékazonosítóját, kövesse a Termék lekérte [a](get-a-product-by-id.md) termékazonosító használatával lépéseit.)

2. Az **Azure-csomag termékváltozatának** lekérése. Kövesse a termék termékkel kapcsolatos termékkódok listájának [lekért lépéseit.](get-a-list-of-skus-for-a-product.md) Ha már ismeri az Azure-csomag termékváltozat-azonosítóját, kövesse a Termékváltozat lekérte ehelyett a termékváltozat [azonosítójának használatával lépéseit.](get-a-sku-by-id.md)

3. A rendelkezésre **állás lekérése** az Azure-csomag termékváltozatában. Kövesse a [Termékváltozatok rendelkezésre állási listájának lekért lépéseit.](get-a-list-of-availabilities-for-a-sku.md) Ha már ismeri a szükséges rendelkezésre állás azonosítóját, kövesse a Rendelkezésre állás lekérte a rendelkezésre állási azonosító használatával [lépéseit.](get-an-availability-by-id.md) *Ügyeljen arra, hogy jegyezze fel az Azure-csomag rendelkezésre állásának **CatalogItemId** tulajdonságát. Erre az értékre szüksége lesz a rendelés létrehozásához.*

## <a name="create-and-submit-an-order"></a>Rendelés létrehozása és elküldése

Az Azure-csomagra vonatkozó megrendelés elküld küldve az alábbi lépésekkel:

1. [Hozzon létre egy](create-a-cart.md) kosárt, amely a megvásárolni kívánt katalóguselemek gyűjteményét tartalmazza. Amikor [kosarat](cart-resources.md#cart)hoz [](cart-resources.md#cartlineitem) létre, a rendszer automatikusan csoportosítja a kosársor elemeit az alapján, hogy mi vásárolható meg együtt ugyanabban a [sorrendben.](order-resources.md#order) (Kosarat [is frissíthet.)](update-a-cart.md)

2. [Tekintse meg a kosárban](checkout-a-cart.md)a rendelés [létrehozását.](order-resources.md#order)

## <a name="get-order-details"></a>Megrendelés részleteinek lekérte

A [rendelésazonosítóval lekérheti egy](get-an-order-by-id.md)adott rendelés részleteit. Lekérheti egy adott ügyfél [összes rendelésének listáját is.](get-all-of-a-customer-s-orders.md)

>[!NOTE]
>A rendelés beküldtét követően legfeljebb 15 perces késéssel jelenik meg a rendelés az ügyfél rendelési listájában.

## <a name="manage-azure-plans"></a>Azure-csomagok kezelése

A rendelés sikeres feldolgozása után létrejön egy  Partnerközpont Előfizetés erőforrás az Azure-csomaghoz. Az Azure-csomag kezeléséhez Partnerközpont **következő** módszereket használhatja az előfizetési erőforrások kezeléséhez:

* [Egy ügyfél előfizetéseinek lekérése](get-all-of-a-customer-s-subscriptions.md)
* [Az előfizetések listájának lekérése megrendelés alapján](get-a-list-of-subscriptions-by-order.md)

Amikor létrehoz egy Azure-Partnerközpont, egy megfelelő Azure-használati előfizetés is létrejön az Azure-ban. További Azure-használati előfizetéseket is létrehozhat ugyanabban az Azure-csomagban a Azure Portal Azure API-k használatával. Az Azure-csomaghoz társított összes Azure-használati előfizetés azonosítóit a következő cikk lépéseit követve szerezheti be: Azure-jogosultságok listájának le Partnerközpont [előfizetéshez](get-a-list-of-azure-entitlements-for-subscription.md)

## <a name="lifecycle-management"></a>Életciklus-kezelés

A meglévő Azure-csomagokat az Előfizetés felfüggesztése lépéseit követve [függesztheti fel.](suspend-a-subscription.md)

*A meglévő Azure-csomagokat csak akkor függesztheti fel, ha már nem rendelkezik aktív használati eszközökkel, beleértve az Azure-használati előfizetéseket és az Azure Reservationst.*

Az Azure-használati előfizetések letiltására vonatkozó részletekért lásd: Azure API az előfizetés [életciklus-felügyeletében.](/rest/api/resources/subscriptions)

A meglévő Azure-foglalások eltávolításához le kell [mondania a foglalásokat.](/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation)
Az Azure-csomag felfüggesztése után újraaktiválhatja azt.

Az Azure-csomag újraaktiválásának részleteiért lásd: Felfüggesztett előfizetés [újraaktiválása](reactivate-a-suspended-a-subscription.md)

## <a name="transition-existing-csp-offers-to-azure-plan"></a>Meglévő CSP-ajánlatok átváltása Azure-csomagra 

Nem hozhat létre Azure-csomagot Microsoft Azure- (MS-AZR-0145P) előfizetéssel rendelkező meglévő ügyfél esetében. [Meglévő CSP Azure-ajánlatokból azonban átvihet ügyfeleket Azure-szolgáltatásokba az Azure-csomag keretében](/partner-center/azure-plan-transition) a Partnerközpontban elérhető CSP-program új kereskedelmi felületén. Meglévő ügyfél átviteléhez használja a termékfrissítési API-kat a következő lépések végrehajtásával:

* [Ellenőrizze, hogy az ügyfél jogosult-e az Azure-csomagra való váltásra](get-eligibility-for-product-upgrade.md)
* [Kezdeményezzen termékfrissítést az ügyfél esetében](create-product-upgrade-entity.md)
* [Ellenőrizze a termékfrissítés állapotát](get-product-upgrade-status.md)

## <a name="azure-spending"></a>Azure-költség

Az Azure-kiadásokat [a](azure-spending.md) használati adatok összegzésének és részletes használati rekordjainak lekérdezésével követheti nyomon a következő módszerekkel:

* [A partner használati összegzésének lekérése](get-a-partner-usage-summary.md)
* [Egy partner összes ügyfélhasználati rekordjának lekérése](get-a-customer-s-usage-records.md)
* [Az ügyfél használati összegzésének lekérése](get-a-customer-usage-summary.md)
* [Egy ügyfél összes előfizetés-használati rekordjának lekérése](get-a-customer-subscription-s-usage-records.md)
* [Az előfizetés használati összegzésének lekérése](get-a-customer-subscription-usage-summary.md)
* [Előfizetés használati adatainak lekérése erőforrás szerint](get-a-customer-subscription-resource-usage-records.md)
* [Előfizetés használati adatainak lekérése mérő szerint](get-a-customer-subscription-meter-usage-records.md)
* [Mérőhasználati rekord erőforrásainak lekérése](meter-usage-resources.md)
* [Erőforrás-használati rekord erőforrásainak lekérése](resource-usage-resources.md)

Az alábbi módszerekkel is beállíthatja és kezelheti az ügyfelek használati költségvetését:

* [Az ügyfél használatalapú költségvetésének lekérése](get-a-customer-s-usage-spending-budget.md)
* [Az ügyfél használatalapú költségvetésének frissítése](update-a-customer-s-usage-spending-budget.md)

## <a name="invoice-and-reconciliation"></a>Számla és egyeztetés

A számlákat és az egyeztetési adatokat a következő módszerekkel kezelheti:

* [Számlák gyűjteményének lekérése](get-a-collection-of-invoices.md)
* [Számlabecslés hivatkozásainak lekérése](get-invoice-estimate-links.md)
* [Számla lekért azonosítója alapján](get-invoice-by-id.md)
* [Számlakivonat lekérése](get-invoice-statement.md)
* [Számla összegzéseinek lekérése](get-invoice-summaries.md)
* [Számlázott használatalapú sorelemek lekérése](get-invoice-billed-consumption-lineitems.md)
* [Nem számlázott használatalapú sorelemek lekérése](get-invoice-unbilled-consumption-lineitems.md)
* [Számlázott recon-sorelemek lekért száma](get-invoiceline-items.md)
* [Nem számlázott egyeztetési sorelemek lekérése](get-invoice-unbilled-recon-lineitems.md)
