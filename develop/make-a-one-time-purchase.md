---
title: Egyszeri vásárlás
description: Szoftver- és foglalási termékek, például szoftver-előfizetések, folyamatos szoftver és Azure Reserved Virtual Machine- (VM-) példányok egy alkalommal való megvásárlása az Partnerközpont API használatával.
ms.date: 10/09/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: baf0b5d4aaa8957874ab019359aca2662a76194387e0cd06999b0bb329076c80
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994438"
---
# <a name="make-a-one-time-purchase"></a>Egyszeri vásárlás

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont a Microsoft Cloud for US Government

Szoftver- és foglalási termékek, például szoftver-előfizetések, folyamatos szoftver és Azure Reserved Virtual Machine- (VM-) példányok egy alkalommal való megvásárlása az Partnerközpont API használatával.

> [!NOTE]
> A szoftver-előfizetések a következő piacokon nem érhetők el:
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
> | Brit indiai-óceáni terület | Jersey                            | Sémo Tomé és Príncipe                    |
> | Brit Virgin-szigetek         | Kiribati                          | Seychelle-szigetek                               |
> | Burkina Faso                   | Koszovó                            | Sierra Leone                             |
> | Burundi                        | Laosz                              | Sint Eustatius                           |
> | Kambodzsa                       | Lesotho                           | Sint Maarten                             |
> | Közép-afrikai Köztársaság       | Libéria                           | Salamon-szigetek                          |
> | Csád                           | Madagaszkár                        | Szomália                                  |
> | Kína                          | Malawi                            | Dél-Georgia és Déli-Sandwich-szigetek |
> | Karácsony-sziget               | Maldív-szigetek                          | Dél-Szudán                              |
> | Cocos (Keeling)-szigetek        | Mali                              | St Trima, Ascension, Tristan da Canha   |
> | Comore-szigetek                        | Marshall-szigetek                  | Suriname                                 |
> | Kongó                          | Martinique                        | Svalbard                                 |
> | Kongó (KDK)                    | Mauritánia                        | Szváziföld                                |
> | Cook-szigetek                   | Mayotte                           | Timor-Leste                              |
> | Dzsibuti                       | Mikronézia                        | Togo                                     |
> | Dominika                       | Montserrat                        | Tokelau                                  |
> | Egyenlítői-Guinea              | Mozambik                        | Tonga                                    |
> | Eritrea                        | Mianmar                           | Turks- és Caicos-szigetek                 |
> | Falkland-szigetek               | Nauru                             | Tuvalu                                   |
> | Francia Guyana                  | Új-Kaledónia                     | Az Usa-beli, outlying-szigetek                    |
> | Francia Polinézia               | Niger                             | Vanuatu                                  |
> | Francia Déli Területek    | Niue                              | Vatikán                             |
> | Gabon                          | Norfolk-sziget                    | Wallis és Futuna                        |
> | Gambia                         | Északi Mariana-szigetek          | Jemen                                    |
> | Gibraltár                      | Palau                             | &nbsp;                                   |
>
&nbsp;
> [!NOTE]
> Az állandó szoftverek megvásárlásához előzőleg minősített szoftvernek kell lennie. További információért forduljon az ügyfélszolgálathoz.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

## <a name="making-a-one-time-purchase"></a>Egyszeres vásárlás

Az egyszer való vásárláshoz kövesse az alábbi lépéseket:

1. [Engedélyezés –](#enablement) (csak Azure-beli fenntartott virtuálisgép-példány) Regisztráljon egy aktív CSP Azure-előfizetést, hogy lehetővé tegye számára bármilyen foglalási termék megvásárlását.

2. [Felderítés](#discovery) – Megkeresheti és kiválaszthatja a megvásárolni kívánt termékeket és terméktermékeket, és ellenőrizheti azok rendelkezésre állását.

3. [Megrendelés beküldve](#order-submission) – Hozzon létre egy bevásárlókosarat a rendelésben lévő elemekkel, és küldje el.

4. [Megrendelés részleteinek](#get-order-details) lekérte – Áttekinti egy megrendelés részleteit, az ügyfél összes rendelését, vagy megtekintheti a megrendeléseket a számlázási ciklus típusa szerint.

Miután megvásárolta az egyszeres vásárlást, a következő forgatókönyvek azt mutatják be, hogyan kezelheti a termékek életciklusát a jogosultságokkal kapcsolatos információk lekérésével, valamint az egyenlegre vonatkozó utasítások, számlák és számlaösszegzők lekérésével.

- [Életciklus-kezelés](#lifecycle-management)

- [Számla és egyeztetés](#invoice-and-reconciliation)

## <a name="enablement"></a>Engedélyezés

Miután azonosította az aktív előfizetést, amelybe hozzá szeretné adni az Azure-beli fenntartott virtuálisgép-példányt, regisztrálnia kell az előfizetést, hogy engedélyezve legyen. Ha egy meglévő [előfizetési](subscription-resources.md) erőforrást úgy regisztrál, hogy az engedélyezve legyen, tekintse meg az [előfizetés regisztrálását.](register-a-subscription.md)

Az előfizetés regisztrálása után a regisztrációs állapot ellenőrzésével ellenőriznie kell, hogy a regisztrációs folyamat befejeződött-e. Ehhez a lépéshez lásd: [Előfizetés regisztrációs állapotának lekért állapota.](get-subscription-registration-status.md)

## <a name="discovery"></a>Felderítés

Az előfizetés engedélyezése után készen áll a termékek és termékkódok kiválasztására, és a rendelkezésre állásuk ellenőrzésére az alábbi api Partnerközpont használatával:

- [Termék](product-resources.md#product) – A cserélhető termékek vagy szolgáltatások csoportosítási konstrukciója. A termék önmagában nem cserélhető elem.

- [Termékváltozat](product-resources.md#sku) – Egy termék alatt található, cserélhető készletnyilvántartó egység (SKU). A termék termékkódok a termék különböző alakjai.

- [Rendelkezésre állás](product-resources.md#availability) – Olyan konfiguráció, amelyben egy termékváltozat megvásárolható (például ország, pénznem és iparági szegmens).

Az egyszeres vásárlás előtt kövesse az alábbi lépéseket:

1. Azonosítsa és lekéri a megvásárolni kívánt terméket és termékváltozatot. Ezt a lépést a termékek és termékváltozatok listázásával használhatja először, vagy ha már ismeri a termék és a termékváltozatok listáját, válassza ki őket.

   - [Termékek listájának lekért listája](get-a-list-of-products.md)
   - [Termék lekérte a termékazonosítót](get-a-product-by-id.md)
   - [Termék termékkel kapcsolatos termékkódok listájának lekért listája](get-a-list-of-skus-for-a-product.md)
   - [Termékváltozat lekérte a termékváltozat azonosítójával](get-a-sku-by-id.md)

2. Ellenőrizze a leltárban, hogy van-e termékváltozat. Erre a lépésre csak az **InventoryCheck** előfeltételként megjelölt termékkódok esetén van szükség.

   - [Leltár ellenőrzése](check-inventory.md)

3. A [termékváltozat rendelkezésre](product-resources.md#availability) [állásának lekérése.](product-resources.md#sku) A rendelés leadáskor szüksége lesz a rendelkezésre állás **CatalogItemId-ére.** Ezt az értéket a következő API-k egyikével használhatja:

   - [Termékváltozatok rendelkezésre állási listájának lekért listája](get-a-list-of-availabilities-for-a-sku.md)
   - [Rendelkezésre állás le szolgáltatása a rendelkezésre állási azonosítóval](get-an-availability-by-id.md)

## <a name="order-submission"></a>Rendelés beküldve

A rendelés elküldhez kövesse az alábbi lépéseket:

1. Hozzon létre egy kosárt, amely a megvásárolni kívánt katalóguselemek gyűjteményét tartalmazza. A kosár [létrehozásakor](cart-resources.md)a [](cart-resources.md#cartlineitem) kosársor elemei automatikusan csoportosítva lesznek az alapján, hogy mi vásárolható együtt ugyanabban a [rendelésben.](order-resources.md)

   - [Bevásárlókocsi létrehozása](create-a-cart.md)
   - [Bevásárlókocsi frissítése](update-a-cart.md)

2. Nézze meg a kosárt. Ha kiveszi a kosárból a rendelést, a rendelés is [létre lesz hozva.](order-resources.md)

   - [A kosár kiveszi a kosárból](checkout-a-cart.md)

## <a name="get-order-details"></a>Megrendelés részleteinek lekérte

Miután létrehozta a rendelést, lekérheti egy adott rendelés részleteit a rendelés azonosítójával, vagy lekérheti egy ügyfél megrendelési listáját. A rendelés elküldés és az ügyfél rendelési listájában való megjelenése között akár 15 perces késés is lehet.

- Egy adott rendelés részleteinek lekért adatai a rendelésazonosítóval. Lásd: [Rendelés lekért azonosítója.](get-an-order-by-id.md)

- Egy ügyfél rendelési listájának lekért listája az ügyfél azonosítójával. Lásd: [Egy ügyfél összes rendelésének lekérte.](get-all-of-a-customer-s-orders.md)

- Egy ügyfél megrendelési listájának [](product-resources.md#billingcycletype) lekért listája a számlázási ciklus típusa szerint, amely lehetővé teszi a rendelések (egyszeres díjak) és az éves vagy havi számlázt rendelések külön-külön való listzását. Lásd: [Rendelések listájának lekérte ügyfél és számlázási ciklustípus szerint.](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)

## <a name="lifecycle-management"></a>Életciklus-kezelés

Az Partnerközpont-ban az egyszer megvásárolt vásárlások életciklusának kezelése során lekérheti a [](entitlement-resources.md)jogosultságokkal kapcsolatos információkat, és lekérheti a foglalás részleteit a foglalási rendelés azonosítójával. Ennek mikéntjére vonatkozó példákért lásd: [Get entitlements (Jogosultságok lekérte).](get-a-collection-of-entitlements.md)

## <a name="invoice-and-reconciliation"></a>Számla és egyeztetés

Az alábbi forgatókönyvek azt mutatják be, hogyan [](invoice-resources.md)lehet programozott módon megtekinteni az ügyfél számláit, és hogyan lehet lekért fiókegyenlegeket és összegzéseket, amelyek tartalmazzák az egyszeres díjakat.

### <a name="balance-and-payment"></a>Egyenleg és kifizetés

Az aktuális számlaegyenleg az ismétlődő és egyszeri díjak egyenlegét is elegyenő alapértelmezett pénznemben való lekértért lásd: Az aktuális fiókegyenleg [lekért egyenlege](get-the-reseller-s-current-account-balance.md)

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
