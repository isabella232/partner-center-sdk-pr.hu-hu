---
title: Egyszeri vásárlás
description: Szoftver- és foglalási termékek, például szoftver-előfizetések, állandó szoftverek és Azure Reserved Virtual Machine- (VM-) példányok vásárlása az Partnerközpont API használatával.
ms.date: 10/09/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1ca2d5b7ad6ba1196d74a8cdb748ab808192d569
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548379"
---
# <a name="make-a-one-time-purchase"></a>Egyszeri vásárlás

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont a Microsoft Cloud for US Government

Szoftver- és foglalási termékek, például szoftver-előfizetések, állandó szoftverek és Azure Reserved Virtual Machine- (VM-) példányok vásárlása az Partnerközpont API használatával.

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
> | Cocos (Keeling)-szigetek        | Mali                              | St Foga, Ascension, Tristan da Amilyenha   |
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
> A folyamatos szoftver megvásárlásához előzőleg minősített szoftvernek kell lennie. További információért forduljon az ügyfélszolgálathoz.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="making-a-one-time-purchase"></a>Egyszeres vásárlás

Az egyszeres vásárláshoz kövesse az alábbi lépéseket:

1. [Engedélyezés –](#enablement) (csak Azure-beli fenntartott virtuálisgép-példány) Regisztráljon egy aktív CSP Azure-előfizetést, hogy lehetővé tegye számára bármilyen foglalási termék megvásárlását.

2. [Felderítés](#discovery) – Megkeresheti és kiválaszthatja a megvásárolni kívánt termékeket és terméktermékeket, és ellenőrizheti azok rendelkezésre állását.

3. [Megrendelés beküldve](#order-submission) – Hozzon létre egy bevásárlókosarat a rendelésben lévő elemekkel, és küldje el.

4. [Megrendelés részleteinek](#get-order-details) lekérte – Áttekinti egy megrendelés részleteit, az ügyfél összes rendelését, vagy megtekintheti a megrendeléseket a számlázási ciklus típusa szerint.

Az egyszeres vásárlást követően a következő forgatókönyvek azt mutatják be, hogyan kezelheti a termékek életciklusát a jogosultságokkal kapcsolatos információk lekérésével, valamint az egyenleg kimutatások, számlák és számlaösszegzők lekérésével.

- [Életciklus-kezelés](#lifecycle-management)

- [Számla és egyeztetés](#invoice-and-reconciliation)

## <a name="enablement"></a>Engedélyezés

Miután azonosította az aktív előfizetést, amelybe hozzá szeretné adni az Azure-beli fenntartott virtuálisgép-példányt, regisztrálnia kell az előfizetést, hogy engedélyezve legyen. Ha egy meglévő [előfizetési](subscription-resources.md) erőforrást úgy kell regisztrálnia, hogy az engedélyezve legyen, tekintse meg az [előfizetés regisztrálását.](register-a-subscription.md)

Az előfizetés regisztrálása után a regisztrációs állapot ellenőrzésével ellenőriznie kell, hogy a regisztrációs folyamat befejeződött-e. Ehhez a lépéshez lásd: [Előfizetés regisztrációs állapotának lekért állapota.](get-subscription-registration-status.md)

## <a name="discovery"></a>Felderítés

Ha az előfizetés engedélyezve van, kiválaszthatja a termékeket és a terméktermékeket, és ellenőrizheti azok rendelkezésre állását az alábbi api-Partnerközpont használatával:

- [Termék](product-resources.md#product) – Egy csoportosítási szerkezet a cserélhető termékekhez vagy szolgáltatásokhoz. A termék önmagában nem cserélhető elem.

- [Termékváltozat](product-resources.md#sku) – Egy termék alatt található, cserélhető terméken (Stock Keeping Unit, SKU). A termékkódok a termék különböző alakjai.

- [Rendelkezésre állás](product-resources.md#availability) – Olyan konfiguráció, amelyben egy termékváltozat megvásárolható (például ország, pénznem és iparági szegmens).

Az egyszeres vásárlás előtt kövesse az alábbi lépéseket:

1. Azonosítsa és lekéri a megvásárolni kívánt terméket és termékváltozatot. Ezt a lépést a termékek és a termékváltozatok listázásával használhatja először, vagy ha már ismeri a termék és a termékváltozat adatait, jelölje ki őket.

   - [Termékek listájának lekért listája](get-a-list-of-products.md)
   - [Termék lekérte a termékazonosítót](get-a-product-by-id.md)
   - [Termék termékterméktermék-listájának lekért listája](get-a-list-of-skus-for-a-product.md)
   - [Termékváltozat lekérte a termékváltozat azonosítójával](get-a-sku-by-id.md)

2. Ellenőrizze a leltárban, hogy van-e termékváltozat. Erre a lépésre csak az **InventoryCheck** előfeltételként megjelölt termékkódok esetén van szükség.

   - [Leltár ellenőrzése](check-inventory.md)

3. A [termékváltozat](product-resources.md#availability) rendelkezésre [állásának lekérése.](product-resources.md#sku) A rendelés leadáskor szüksége lesz a rendelkezésre állás **CatalogItemId-ére.** Ezt az értéket a következő API-k egyikével használhatja:

   - [Termékváltozatok rendelkezésre állási listájának lekért listája](get-a-list-of-availabilities-for-a-sku.md)
   - [Rendelkezésre állás lekérte a rendelkezésre állási azonosítóval](get-an-availability-by-id.md)

## <a name="order-submission"></a>Rendelés beküldve

A rendelés elküldhez kövesse az alábbi lépéseket:

1. Hozzon létre egy kosárt, amely a megvásárolni kívánt katalóguselemek gyűjteményét tartalmazza. A kosár [létrehozásakor](cart-resources.md)a [](cart-resources.md#cartlineitem) kosársor elemei automatikusan csoportosítva lesznek az alapján, hogy mi vásárolható együtt ugyanabban a [rendelésben.](order-resources.md)

   - [Bevásárlókocsi létrehozása](create-a-cart.md)
   - [Bevásárlókocsi frissítése](update-a-cart.md)

2. Nézze meg a kosárt. A kosár ellenőrzésekor a rendelés is létre lesz [hozva.](order-resources.md)

   - [A kosár kiveszi](checkout-a-cart.md)

## <a name="get-order-details"></a>Megrendelés részleteinek lekérte

Miután létrehozta a rendelést, lekérheti egy adott rendelés részleteit a rendelés azonosítójával, vagy lekérheti egy ügyfél rendelési listáját. A rendelés beküldés és az ügyfél rendelési listájában való megjelenése között akár 15 perces késés is lehet.

- Egy adott rendelés részleteinek lekért adatai a rendelés azonosítójával. Lásd: [Rendelés lekért azonosítója.](get-an-order-by-id.md)

- Egy ügyfél rendelési listájának lekért listája az ügyfél azonosítójával. Lásd: [Egy ügyfél összes rendelésének lekért rendelése.](get-all-of-a-customer-s-orders.md)

- Ha le kell kapnia egy [](product-resources.md#billingcycletype) ügyfél rendelési listáját a számlázási ciklus típusa szerint, amely lehetővé teszi a rendelések (egyszeres díjak) és az éves vagy havi számlázt rendelések külön-külön való felsorolását. Lásd: [Rendelések listájának lekérte ügyfél és számlázási ciklustípus szerint.](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)

## <a name="lifecycle-management"></a>Életciklus-kezelés

Az Partnerközpont-ban az egyszer megvásárolt vásárlások életciklusának részeként lekérheti a jogosultságokkal kapcsolatos információkat, és lekérheti a foglalás részleteit a foglalási rendelés azonosítójával. [](entitlement-resources.md) Erre vonatkozó példákért lásd: [Jogosultságok lekérte.](get-a-collection-of-entitlements.md)

## <a name="invoice-and-reconciliation"></a>Számla és egyeztetés

Az alábbi forgatókönyvek azt mutatják be, hogyan [](invoice-resources.md)lehet programozott módon megtekinteni az ügyfél számláit, és hogyan lehet lekért fiókegyenlegeket és összegzéseket, amelyek tartalmazzák az egyszeres díjakat.

### <a name="balance-and-payment"></a>Egyenleg és kifizetés

Ha az aktuális számlaegyenleget az alapértelmezett pénznemtípusban,amely az ismétlődő és az egyszeri díjak egyenlegét is figyelembe veszi, tekintse meg az aktuális számlaegyenleg [lekért beállítását.](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Több pénznem egyenlege és kifizetése

Az aktuális számlaegyenleg és a számlaösszegzéseket tartalmazó számlaösszegzések gyűjtéséhez, amelyek ismétlődő és egyszeri díjakat is tartalmaznak az egyes ügyfelek pénznemtípusaihoz, lásd: Számlaösszegzések [lekérte.](get-invoice-summaries.md)

### <a name="invoices"></a>Számlák

Az ismétlődő és egyszeri díjakat is bemutató számlák gyűjteményének lekért [lásd: Számlák gyűjteményének begyűjtése.](get-a-collection-of-invoices.md)

### <a name="single-invoice"></a>Egyetlen számla

Egy adott számla számlaazonosítóval való lekérését lásd: [Számla lekérése azonosító alapján.](get-invoice-by-id.md)

### <a name="reconciliation"></a>Egyeztetés

Egy adott számlaazonosító számlasorelem-részleteinek (egyeztetési sorelemek) gyűjteményét lásd: [Számlasorelemek begyűjtése.](get-invoiceline-items.md)

### <a name="download-an-invoice-as-a-pdf"></a>Számla letöltése PDF-fájlként

A számlakivonat PDF formátumban, számlaazonosítóval való lekéréséhez lásd: [Számlakivonat lekérése.](get-invoice-statement.md)
