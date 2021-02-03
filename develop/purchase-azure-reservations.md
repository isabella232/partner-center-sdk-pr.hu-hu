---
title: Azure-foglalások megvásárlása
description: A partner Center API-val a meglévő Microsoft Azure-előfizetéssel (MS-AZR-0145P) vagy az Azure-csomaggal vásárolhat Azure-foglalásokat az ügyfelek számára.
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c09f65ae5105a74be41a7ec45824e3889217a1c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767863"
---
# <a name="purchase-azure-reservations"></a>Azure-foglalások megvásárlása

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud for US Government Partnerközpontja

Ha a partner Center API-val szeretne Azure-foglalást vásárolni egy ügyfélhez, meglévő Microsoft Azure (**MS-AZR-0145P**) előfizetéssel vagy Azure-csomaggal kell rendelkeznie.

> [!NOTE]
> Az Azure-foglalások nem érhetők el az alábbi piacokon:
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

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Egy aktív CSP Azure-előfizetés vagy egy Azure-csomag előfizetés-azonosítója.

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Microsoft Azure foglalások megvásárlása

Miután azonosította az aktív CSP Azure-előfizetést, amelyhez Azure-foglalást kíván hozzáadni a alkalmazáshoz, a következő lépésekkel vásárolhatja meg:

1. [Engedélyezés](#enablement) – aktív CSP Azure-előfizetés regisztrálása, amely lehetővé teszi az Azure-foglalások megvásárlását.

2. [Felderítés](#discovery) – keresse meg és válassza ki a megvásárolni kívánt Azure foglalási termékeket és SKU-ket, és ellenőrizze azok rendelkezésre állását.

3. [Rendelés beküldése](#order-submission) – hozzon létre egy bevásárlókocsiot a megrendelés elemeivel, és küldje el.

4. [Rendelési adatok beolvasása](#get-order-details) – megtekintheti egy megrendelés részleteit, az ügyfél összes rendelését, vagy megtekintheti a rendeléseket számlázási ciklus típusa szerint.

Az Azure-foglalások megvásárlása után az alábbi forgatókönyvek azt mutatják be, hogyan kezelheti az életciklusát az Azure-beli foglalási jogosultságokkal kapcsolatos információk beszerzésével, valamint az egyenleg-utasítások, a számlák és a számlázási összefoglalók beolvasásának módjával.

- [Életciklus-kezelés](#lifecycle-management)
- [Számlázás és egyeztetés](#invoice-and-reconciliation)

## <a name="enablement"></a>Engedélyezés

Az engedélyezés azt jelenti, hogy egy meglévő Microsoft Azure (**MS-AZR-0145P**) előfizetés egy Azure-beli fenntartott VM-példányhoz való társításához regisztrálja az előfizetést, hogy az engedélyezve legyen az Azure-foglalásokhoz. A regisztráció a Azure Reserved VM Instances megvásárlásának előfeltétele.

A következők miatt előfizetésre van szükség:

1. Annak ellenőrzését, hogy az ügyfél jogosult-e az erőforrások üzembe helyezésére, és így a Azure Reserved VM Instances vásárlása egy adott régióban vagy sem.

2. A kapacitás prioritásának biztosítása az előfizetésben üzemelő példányok számára. Ez csak az egyetlen hatókörű Azure Reserved VM Instancesre vonatkozik, ha a **kapacitás prioritása** lehetőség ki van választva.

Miután azonosította azt az aktív előfizetést, amelyhez hozzá kívánja adni az Azure-foglalást, regisztrálnia kell az előfizetést, hogy az engedélyezve legyen az Azure-foglalásokhoz. Meglévő [előfizetési](subscription-resources.md) erőforrás regisztrálásához, hogy engedélyezve legyen az Azure-foglalások rendezése, lásd: [előfizetés regisztrálása](register-a-subscription.md).

Az előfizetés regisztrálása után ellenőrizze, hogy a regisztrációs folyamat befejeződött-e a regisztráció állapotának ellenőrzésével. Ehhez tekintse meg az [előfizetés regisztrációs állapotának beszerzése](get-subscription-registration-status.md)című témakört.

> [!NOTE]
> Az Azure-csomaggal rendelkező ügyfelek Microsoft Azure foglalásának megvásárlásakor először regisztrálnia kell az Azure-csomagot. A Microsoft Azure (**MS-AZR-0145P**) előfizetéshez hasonlóan az Azure-csomagot egy partner Center- [előfizetési](subscription-resources.md) erőforrás képviseli. Ezért ugyanezt a [regisztrációs előfizetési](register-a-subscription.md) módszert használhatja az Azure-csomag regisztrálásához.

## <a name="discovery"></a>Felderítés

Ha az előfizetés engedélyezve van az Azure-foglalások megvásárlásához, készen áll a termékek és az SKU-k kiválasztására, és a rendelkezésre állásuk ellenőrzését a következő partner Center API-modellekkel:

- [Termék](product-resources.md#product) – a megvásárolható termékek vagy szolgáltatások csoportosítási konstrukciója. Egy termék önmagában nem egy megvásárolható tétel.

- [SKU](product-resources.md#sku) – egy terméken belül megvásárolható készlet-tartási egység (SKU). Ezek a termék különböző alakzatait jelölik.

- [Rendelkezésre állás](product-resources.md#availability) – olyan konfiguráció, amelyben az SKU megvásárolható (például ország, pénznem és iparági szegmens).

Az Azure-foglalás megvásárlása előtt végezze el a következő lépéseket:

1. Azonosítsa és kérje le a megvásárolni kívánt terméket és SKU-t. Ezt úgy teheti meg, hogy először felsorolja a termékeket és az SKU-t, vagy ha már ismeri a termék és az SKU azonosítóit, és kiválasztja őket.

   - [Termékek listájának lekérése (ország alapján)](get-a-list-of-products.md)
   - [Termék beszerzése a termék AZONOSÍTÓjának használatával](get-a-product-by-id.md)
   - [Egy termék termékváltozatait tartalmazó lista lekérése (ország alapján)](get-a-list-of-skus-for-a-product.md)
   - [SKU beszerzése az SKU azonosító használatával](get-a-sku-by-id.md)

2. Egy SKU leltárának keresése. Erre a lépésre csak a **InventoryCheck** előfeltételként megjelölt SKU-ra van szükség.

   - [Leltár ellenőrzése](check-inventory.md)

3. Az [SKU](product-resources.md#sku) [rendelkezésre állásának](product-resources.md#availability) beolvasása. A megrendelés elhelyezésekor szüksége lesz a rendelkezésre állás **CatalogItemId** . Az érték beszerzéséhez használja a következő API-k egyikét:

   - [Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ország alapján)](get-a-list-of-availabilities-for-a-sku.md)
   - [Rendelkezésre állási azonosító használata](get-an-availability-by-id.md)

> [!IMPORTANT]
> Minden Microsoft Azure foglalási termék különböző elérhetőséggel rendelkezik Microsoft Azure (**MS-AZR-0145P**) előfizetéshez és az Azure-csomaghoz. A [termékek (országonként) listájának](get-a-list-of-products.md)lekéréséhez vagy a [termékhez tartozó SKU-EK listájának](get-a-list-of-skus-for-a-product.md)lekéréséhez, vagy az Azure-csomaghoz tartozó [SKU (ország szerint) elérhetőségi listájának](get-a-list-of-availabilities-for-a-sku.md) lekéréséhez a "reservationScope = AzurePlan" paramétert kell megadnia.

## <a name="order-submission"></a>Megrendelés beküldése

Az Azure foglalási sorrendjének elküldéséhez tegye a következőket:

1. Hozzon létre egy cartot a megvásárolni kívánt katalógus-elemek gyűjteményének tárolására. Amikor létrehoz egy [kosarat](cart-resources.md), a rendszer automatikusan csoportosítja a [szekér elemeit](cart-resources.md#cartlineitem) attól függően, hogy mit vásárolhat együtt ugyanabban a [sorrendben](order-resources.md).

   - [Bevásárlókocsi létrehozása](create-a-cart.md)
   - [Bevásárlókocsi frissítése](update-a-cart.md)

2. Látogasson el a kosárba. A kosár megkeresése egy [megrendelés](order-resources.md)létrehozását eredményezi.

   - [A kosár pénztárának kifizetése](checkout-a-cart.md)

## <a name="get-order-details"></a>Megrendelés részleteinek beolvasása

Miután létrehozta az Azure foglalási sorrendjét, lekérheti egy adott megrendelés részleteit a megrendelés azonosítójával, vagy megtekintheti az ügyfél rendeléseinek listáját. A megrendelés elküldése és az ügyfél rendeléseinek listájában akár 15 percet is igénybe vehet.

- Egy adott megrendelés részleteinek beszerzése a megrendelés AZONOSÍTÓjának használatával. Lásd: [Order by id](get-an-order-by-id.md).

- Az ügyfél-AZONOSÍTÓval rendelkező ügyfél rendeléseinek listájának lekérése. Lásd: az [összes ügyfél rendelésének beolvasása](get-all-of-a-customer-s-orders.md).

- A [számlázási ciklus típusa](product-resources.md#billingcycletype) alapján megjelenő megrendelések listájának lekéréséhez, amely lehetővé teszi, hogy az Azure foglalási rendeléseket (egyszeri költségek) és az éves vagy havi számlázott rendeléseket külön lehessen kilistázni. Lásd: [a megrendelések listájának lekérése az ügyfél és a számlázási ciklus típusa alapján](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Életciklus-kezelés

Az Azure-foglalások a partner Centerben való kezelésének részeként lekérheti az Azure-beli foglalási [jogosultságokkal](entitlement-resources.md)kapcsolatos információkat, és lekérheti a foglalás részleteit a foglalási rendelés azonosítójának használatával. Ennek módjáról a [jogosultságok beszerzése](get-a-collection-of-entitlements.md)című témakörben talál példákat.   

## <a name="invoice-and-reconciliation"></a>Számlázás és egyeztetés

Az alábbi forgatókönyvek azt mutatják be, hogyan lehet programozott módon megtekinteni az ügyfél [számláit](invoice-resources.md), és beolvasni a fiók egyenlegeit és összegzéseit, amelyek az Azure-foglalások egyszeri díjait tartalmazzák.

### <a name="balance-and-payment"></a>Egyenleg és fizetés

Az aktuális fiók egyenlegének alapértelmezett pénznembeli beszerzéséhez, amely az ismétlődő és egyszeri (Azure-foglalási) díjak egyenlege, lásd: [az aktuális fiók egyenlegének beolvasása](get-the-reseller-s-current-account-balance.md) .

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
