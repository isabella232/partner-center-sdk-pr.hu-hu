---
title: Új kereskedelmi licencalapú szolgáltatások vásárlása
description: A fejlesztők új kereskedelmi licencalapú szolgáltatásokat vásárolhatnak, hozhatnak létre és kezelnek az Partnerközpont API-kkel.
ms.date: 02/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: dd3aebdb0a670449d3a39f67fc2ad6c7ef8df8e5
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457314"
---
# <a name="purchasing-new-commerce-license-based-services"></a>Új kereskedelmi licencalapú szolgáltatások vásárlása

**A következőkre vonatkozik:**

* Partnerközpont

> [!Note] 
> Az új kereskedelmi módosítások jelenleg csak az M365/D365 új kereskedelmi felhasználói élmény technikai előzetesének részét képezi partnerek számára érhetők el.

Új kereskedelmiélmény-licencalapú szolgáltatásokat vásárolhat, hozhat létre és kezelhet a Partnerközpont API-okkal. A folyamat hasonló az Azure-csomaghoz és a Marketplace-ajánlatokhoz.

## <a name="prerequisites"></a>Előfeltételek

* [Partnerközpont hitelesítő adatok](partner-center-authentication.md) megadása. Az új kereskedelmi felület támogatja az önálló alkalmazással és az Alkalmazás+Felhasználó hitelesítő adatokkal történő hitelesítést.
* Az ügyfél azonosítója. Ha nem rendelkezik ügyfélazonosítóval, kövesse az Ügyfelek listájának [lekért lépéseit.](get-a-list-of-customers.md) Másik lehetőségként jelentkezzen be a Partnerközpont, válassza ki az ügyfelet az ügyfelek listájából, válassza a **Fiók** lehetőséget, majd mentse **a Microsoft-azonosítóját.**
* [Annak megerősítése, hogy az](/partner-center/confirm-customer-agreement)ügyfél elfogadta a Microsoft Ügyfélszerződés.

## <a name="get-the-catalog-item-for-new-commerce-license-based-services"></a>Katalóguselem lekérte az új kereskedelmi licencalapú szolgáltatásokhoz

Új kereskedelmi licencalapú szolgáltatáskatalógus-elemeket kell lekérni. Katalóguselemek lekérése a meglévő Partnerközpont api-k használatával a következő erőforrásmodellekkel:

* **[Termék:](product-resources.md#product)** Egy csoportosítási szerkezet a cserélhető termékekhez vagy szolgáltatásokhoz. Maga a termék nem cserélhető elem.
* **[Termékváltozat:](product-resources.md#sku)** Egy termék alatt található, véglegesen cserélhető termékegység (SKU). Az SKUs a termék különböző alakjainak oszlott meg.
* **[Rendelkezésre állás:](product-resources.md#availability)** Olyan konfiguráció, amelyben egy termékváltozat megvásárolható (például ország, pénznem vagy iparági szegmens).

Az új kereskedelmi licencalapú szolgáltatásokhoz tartozó katalóguselemek beszerzése:

1. Kövesse a [Termékek listájának](get-a-list-of-products.md) lekért lépéseit, és adja meg a **targetView** értéket **OnlineServices értékként.** (Ha már ismeri a megvásárolni kívánt ajánlat termékazonosítóját, kövesse a Termék beszerzése [a](get-a-product-by-id.md) termékazonosító használatával lépéseit.)

2. A keresett **ajánlat termékváltozatának** lekérése. Kövesse a termék termékkel kapcsolatos termékkódok [listájának lekért lépéseit.](get-a-list-of-skus-for-a-product.md) (Ha már ismeri a kívánt ajánlat termékváltozat-azonosítóját, ehelyett kövesse [a Termékváltozat](get-a-sku-by-id.md) lekérte a termékváltozat-azonosító használatával lépéseit.)

3. A rendelkezésre **állás lekérése** az ajánlat termékváltozatában. A különböző ajánlatok meghatározott feltételeket támogatnak. Egyes termékkódok több rendelkezésre állási okkal is rendelkezésre állnak. Kövesse a [Termékváltozatok rendelkezésre állási listájának lekért lépéseit.](get-a-list-of-availabilities-for-a-sku.md) (Ha már ismeri a szükséges rendelkezésre állás azonosítóját, kövesse a Rendelkezésre állás lekérte [a](get-an-availability-by-id.md) rendelkezésre állási azonosító használatával ehelyett lépéseit.) Ügyeljen arra, hogy jegyezze fel az ajánlat rendelkezésre ***állásának CatalogItemId** tulajdonságának értékét. Erre az értékre szüksége lesz egy rendelés létrehozásához.*

## <a name="create-and-submit-an-order"></a>Rendelés létrehozása és elküldése

Az Azure-csomagra (beleértve az új kereskedelmi rendeléseket is) vonatkozó megrendelés elküld útjára az alábbi lépéseket követve:

1. [Hozzon létre egy kosárt,](create-a-cart.md) amely a megvásárolni kívánt katalóguselemek gyűjteményét tartalmazza. Amikor létrehoz egy [kosárt,](cart-resources.md#cart)a rendszer automatikusan csoportosítja a kosársor elemeit az alapján, hogy mi vásárolható meg együtt ugyanabban a [](cart-resources.md#cartlineitem) [sorrendben.](order-resources.md#order) (Kosarat [is frissíthet.)](update-a-cart.md)

2. [Tekintse meg a kosárban](checkout-a-cart.md)a rendelés [létrehozását.](order-resources.md#order)

## <a name="get-order-details"></a>Megrendelés részleteinek lekérte

Egy adott [rendelés részleteit a rendelésazonosítóval lehet lekérni.](get-an-order-by-id.md) Lekérheti egy adott ügyfél [összes rendelésének listáját is.](get-all-of-a-customer-s-orders.md)

>[!NOTE]
>A megrendelés elküldése után legfeljebb 15 perc késéssel jelenik meg a rendelés az ügyfél rendelési listájában. Jelenleg az EU-partnerek csak a következőre vásárolhatnak új kereskedelmi ajánlatokat: 1. Új ügyfelek 2. Meglévő ügyfelek, akik nem rendelkezik már meglévő Azure-csomaggal, Piactérrel, szoftver-előfizetésekkel vagy állandó szoftverekkel a partner országának pénznemén kívül.

## <a name="manage-new-commerce-subscriptions"></a>Új kereskedelmi előfizetések kezelése

A rendelés sikeres feldolgozása után létrejön egy Partnerközpont **Előfizetés** erőforrás az Azure-csomaghoz. Az Azure-csomag kezeléséhez a következő módszereket használhatja Partnerközpont **előfizetési** erőforrások kezeléséhez:

* [Egy ügyfél előfizetéseinek lekérése](get-all-of-a-customer-s-subscriptions.md)
* [Az előfizetések listájának lekérése megrendelés alapján](get-a-list-of-subscriptions-by-order.md)

Vannak különbségek és új képességek, amelyek az új kereskedelemre vonatkoznak.

## <a name="invoice-and-reconciliation"></a>Számla és egyeztetés

A számlákat és az egyeztetési adatokat a következő módszerekkel kezelheti:

* [Számlák gyűjteményének lekérése](get-a-collection-of-invoices.md)
* [Számlabecslés hivatkozásainak lekérése](get-invoice-estimate-links.md)
* [Számla lekérte azonosító alapján](get-invoice-by-id.md)
* [Számlakivonat lekérése](get-invoice-statement.md)
* [Számla összegzéseinek lekérése](get-invoice-summaries.md)
* [Számlázott használatalapú sorelemek lekérése](get-invoice-billed-consumption-lineitems.md)
* [Nem számlázott használatalapú sorelemek lekérése](get-invoice-unbilled-consumption-lineitems.md)
* [Számlázott recon-sorelemek lekért száma](get-invoiceline-items.md)
* [Nem számlázott egyeztetési sorelemek lekérése](get-invoice-unbilled-recon-lineitems.md)
