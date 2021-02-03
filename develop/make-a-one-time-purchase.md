---
title: Egyszeri vásárlás
description: Szoftverek és foglalási termékek, például a szoftveres előfizetések, az örökös szoftverek és az Azure-beli fenntartott virtuálisgép-példányok egyszeri vásárlása a partner Center API használatával.
ms.date: 10/09/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 17a5f5c1e845ba36a94d7ce909df30e0146ba448
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767808"
---
# <a name="make-a-one-time-purchase"></a>Egyszeri vásárlás

**A következőkre vonatkozik**

- Partnerközpont
- A Microsoft Cloud for US Government Partnerközpontja

Szoftverek és foglalási termékek, például a szoftveres előfizetések, az örökös szoftverek és az Azure-beli fenntartott virtuálisgép-példányok egyszeri vásárlása a partner Center API használatával.

> [!NOTE]
> A szoftveres előfizetések nem érhetők el az alábbi piacokon:
>
> | Nem elérhető piacok            | Nem elérhető piacok (folytatás...) | Nem elérhető piacok (folytatás...)      |
> |--------------------------------|-----------------------------------|------------------------------------------|
> | Åland-szigetek                  | Grönland                         | Pápua Új-Guinea                         |
> | Amerikai Szamoa                 | Grenada                           | Pitcairn-szigetek                         |
> | Andorra                        | Guadeloupe                        | Réunion                                  |
> | Anguilla                       | Guam                              | Orosz Föderáció                       |
> | Antarktisz                     | Guernsey                          | Saba                                     |
> | Antigua és Barbuda            | Guinea                            | Saint Barthélemy                         |
> | Aruba                          | Bissau-Guinea                     | Saint Lucia                              |
> | Benin                          | Guyana                            | Saint Martin                             |
> | Bhután                         | Haiti                             | Saint-Pierre és Miquelon                |
> | Bonaire                        | Heard-sziget és McDonald-szigetek | Saint Vincent és Grenadine-szigetek         |
> | Bouvet-sziget                  | Man-sziget                       | Szamoa                                    |
> | Brazília                         | Jan Mayen                         | San Marino                               |
> | Brit indiai-óceáni terület | Jersey                            | São Tomé és Príncipe                    |
> | Brit Virgin-szigetek         | Kiribati                          | Seychelle-szigetek                               |
> | Burkina Faso                   | Koszovó                            | Sierra Leone                             |
> | Burundi                        | Laosz                              | Sint Eustatius                           |
> | Kambodzsa                       | Lesotho                           | Sint Maarten                             |
> | Közép-afrikai Köztársaság       | Libéria                           | Salamon-szigetek                          |
> | Csád                           | Madagaszkár                        | Szomália                                  |
> | Kína                          | Malawi                            | Dél-Georgia és Déli-Sandwich-szigetek |
> | Karácsony-sziget               | Maldív-szigetek                          | Dél-Szudán                              |
> | Cocos (Keeling)-szigetek        | Mali                              | Szent Ilona, Ascension, Tristan da Cunha   |
> | Comore-szigetek                        | Marshall-szigetek                  | Suriname                                 |
> | Kongó                          | Martinique                        | Svalbard                                 |
> | Kongó (KDK)                    | Mauritánia                        | Szváziföld                                |
> | Cook-szigetek                   | Mayotte                           | Timor-Leste                              |
> | Dzsibuti                       | Mikronézia                        | Togo                                     |
> | Dominika                       | Montserrat                        | Tokelau                                  |
> | Egyenlítői-Guinea              | Mozambik                        | Tonga                                    |
> | Eritrea                        | Mianmar                           | Turks- és Caicos-szigetek                 |
> | Falkland-szigetek               | Nauru                             | Tuvalu                                   |
> | Francia Guyana                  | Új-Kaledónia                     | Amerikai Egyesült Államok lakatlan külbirtokai                    |
> | Francia Polinézia               | Niger                             | Vanuatu                                  |
> | Francia Déli Területek    | Niue                              | Vatikán                             |
> | Gabon                          | Norfolk-sziget                    | Wallis és Futuna                        |
> | Gambia                         | Északi Mariana-szigetek          | Jemen                                    |
> | Gibraltár                      | Palau                             | &nbsp;                                   |
>
&nbsp;
> [!NOTE]
> Az örökös szoftverek megvásárlásához előzőleg minősítéssel kell rendelkeznie. További információért forduljon az ügyfélszolgálathoz.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="making-a-one-time-purchase"></a>Egyszeri vásárlás készítése

Egyszeri vásárláshoz hajtsa végre a következő lépéseket:

1. [Engedélyezés](#enablement) – (csak Azure-beli fenntartott VM-példány) regisztráljon egy aktív CSP Azure-előfizetést, amely lehetővé teszi a foglalási termékek megvásárlását.

2. [Felderítés](#discovery) – keresse meg és válassza ki a megvásárolni kívánt termékeket és SKU-ket, és ellenőrizze azok rendelkezésre állását.

3. [Rendelés beküldése](#order-submission) – hozzon létre egy bevásárlókocsiot a megrendelés elemeivel, és küldje el.

4. [Rendelési adatok beolvasása](#get-order-details) – megtekintheti egy megrendelés részleteit, az ügyfél összes rendelését, vagy megtekintheti a rendeléseket számlázási ciklus típusa szerint.

Az egyszeri vásárlást követően a következő forgatókönyvek bemutatják, hogyan kezelheti a termékeinek életciklusát a jogosultságokkal kapcsolatos információk beszerzésével, valamint az egyenleg-utasítások, a számlák és a számlázási összefoglalók beolvasásával.

- [Életciklus-kezelés](#lifecycle-management)

- [Számlázás és egyeztetés](#invoice-and-reconciliation)

## <a name="enablement"></a>Engedélyezés

Miután azonosította azt az aktív előfizetést, amelyhez hozzá kívánja adni az Azure-beli fenntartott VM-példányt, regisztrálnia kell az előfizetést, hogy az engedélyezve legyen. Egy meglévő [előfizetési](subscription-resources.md) erőforrás regisztrálásához, hogy az engedélyezve legyen, tekintse meg az [előfizetés regisztrálása](register-a-subscription.md)című témakört.

Az előfizetés regisztrálása után ellenőrizze, hogy a regisztrációs folyamat befejeződött-e a regisztráció állapotának ellenőrzésével. A lépés elvégzéséhez lásd: [előfizetés-regisztráció állapotának beolvasása](get-subscription-registration-status.md).

## <a name="discovery"></a>Felderítés

Ha az előfizetés engedélyezve lett, készen áll a termékek és az SKU-k kiválasztására, és a rendelkezésre állásuk ellenőrzését a következő partner Center API-modellek használatával:

- [Termék](product-resources.md#product) – a megvásárolható termékek vagy szolgáltatások csoportosítási konstrukciója. Egy termék önmagában nem egy megvásárolható tétel.

- [SKU](product-resources.md#sku) – egy terméken belül megvásárolható készlet-tartási egység (SKU). A SKU a termék különböző alakzatait jelöli.

- [Rendelkezésre állás](product-resources.md#availability) – olyan konfiguráció, amelyben az SKU megvásárolható (például ország, pénznem és iparági szegmens).

Egyszeri vásárlás előtt végezze el a következő lépéseket:

1. Azonosítsa és kérje le a megvásárolni kívánt terméket és SKU-t. Ezt a lépést először a termékek és az SKU listázásával, vagy ha már ismeri a termék és az SKU azonosítóit, jelölje ki őket.

   - [Termékek listájának lekérése](get-a-list-of-products.md)
   - [Termék beszerzése a termék AZONOSÍTÓjának használatával](get-a-product-by-id.md)
   - [A termékhez tartozó SKU-termékek listájának beolvasása](get-a-list-of-skus-for-a-product.md)
   - [SKU beszerzése az SKU azonosító használatával](get-a-sku-by-id.md)

2. Egy SKU leltárának keresése. Erre a lépésre csak a **InventoryCheck** előfeltételként megjelölt SKU-ra van szükség.

   - [Leltár ellenőrzése](check-inventory.md)

3. Az [SKU](product-resources.md#sku) [rendelkezésre állásának](product-resources.md#availability) beolvasása. A megrendelés elhelyezésekor szüksége lesz a rendelkezésre állás **CatalogItemId** . Az érték beszerzéséhez használja a következő API-k egyikét:

   - [Az SKU-ban lévő elérhetőségek listájának lekérése](get-a-list-of-availabilities-for-a-sku.md)
   - [Rendelkezésre állási azonosító használata](get-an-availability-by-id.md)

## <a name="order-submission"></a>Megrendelés beküldése

A megrendelés elküldéséhez kövesse az alábbi lépéseket:

1. Hozzon létre egy cartot a megvásárolni kívánt katalógus-elemek gyűjteményének tárolására. Amikor létrehoz egy [kosarat](cart-resources.md), a rendszer automatikusan csoportosítja a [szekér elemeit](cart-resources.md#cartlineitem) attól függően, hogy mit vásárolhat együtt ugyanabban a [sorrendben](order-resources.md).

   - [Bevásárlókocsi létrehozása](create-a-cart.md)
   - [Bevásárlókocsi frissítése](update-a-cart.md)

2. Látogasson el a kosárba. A kosár megkeresése egy [megrendelés](order-resources.md)létrehozását eredményezi.

   - [A kosár pénztárának kifizetése](checkout-a-cart.md)

## <a name="get-order-details"></a>Megrendelés részleteinek beolvasása

Miután létrehozta a rendelést, lekérheti egy adott megrendelés részleteit a megrendelés AZONOSÍTÓjának használatával, vagy megtekintheti az ügyfél rendeléseinek listáját. A megrendelés elküldése és az ügyfél rendeléseinek listájában akár 15 percet is igénybe vehet.

- Egy adott megrendelés részleteinek beszerzése a megrendelés AZONOSÍTÓjának használatával. Lásd: [Order by id](get-an-order-by-id.md).

- Az ügyfél-AZONOSÍTÓval rendelkező ügyfél rendeléseinek listájának lekérése. Lásd: az [összes ügyfél rendelésének beolvasása](get-all-of-a-customer-s-orders.md).

- Annak érdekében, hogy egy adott ügyfélhez tartozó megrendelések listáját lekérje a [számlázási ciklus típusa](product-resources.md#billingcycletype) alapján, amely lehetővé teszi a megrendelések (egyszeri költségek) és az éves vagy havi számlázott rendelések külön rendelését. Lásd: [a megrendelések listájának lekérése az ügyfél és a számlázási ciklus típusa alapján](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Életciklus-kezelés

A fiókpartner egyszeri vásárlások életciklusának kezelésének részeként lekérheti a [jogosultságokkal](entitlement-resources.md)kapcsolatos információkat, és lekérheti a foglalás részleteit a foglalási rendelés azonosítójának használatával. Ennek módjáról a [jogosultságok beszerzése](get-a-collection-of-entitlements.md)című témakörben talál példákat.

## <a name="invoice-and-reconciliation"></a>Számlázás és egyeztetés

Az alábbi forgatókönyvek azt mutatják be, hogyan lehet programozott módon megtekinteni az ügyfél [számláit](invoice-resources.md), és beolvasni a fiók egyenlegeit és összegzéseit, amelyek egyszeri díjat tartalmaznak.

### <a name="balance-and-payment"></a>Egyenleg és fizetés

Az aktuális fiók egyenlegének alapértelmezett pénznemben való beszerzéséhez, amely az ismétlődő és az egyszeri költségek egyenlege, tekintse [meg az aktuális fiók egyenlegének beolvasása](get-the-reseller-s-current-account-balance.md) című témakört.

### <a name="multi-currency-balance-and-payment"></a>Több pénznemre kiterjedő egyenleg és fizetés

Az aktuális fiók egyenlegének beszerzéséhez, valamint a számla összegzésének összefoglalásához, amely tartalmazza az egyes ügyfelek pénznem-típusaira vonatkozó ismétlődő és egyszeri díjat is, tekintse meg a [számla összegzésének beolvasása](get-invoice-summaries.md)című témakört.

### <a name="invoices"></a>Számlák

Az ismétlődő és egy egyszeri díjat is tartalmazó számlák gyűjteményének beszerzéséhez tekintse meg [a számlák gyűjteményének beolvasása](get-a-collection-of-invoices.md)című témakört.

### <a name="single-invoice"></a>Egyetlen számla

Ha a számla AZONOSÍTÓjának használatával szeretne beolvasni egy adott számlát, tekintse meg a [számla beszerzése azonosító alapján](get-invoice-by-id.md)című témakört.

### <a name="reconciliation"></a>Licencegyeztetési

A számlasor-elemek részleteinek (egyeztetési sorok) egy adott AZONOSÍTÓhoz tartozó gyűjteményének lekéréséhez tekintse meg a [Számlázási sorok beolvasása](get-invoiceline-items.md)című cikket.

### <a name="download-an-invoice-as-a-pdf"></a>Számla letöltése PDF-ként

Ha a számla AZONOSÍTÓjának használatával szeretne beolvasni egy számlafogadó-utasítást a PDF-űrlapon, olvassa el a [Számlakivonat beolvasása](get-invoice-statement.md)című témakört.
