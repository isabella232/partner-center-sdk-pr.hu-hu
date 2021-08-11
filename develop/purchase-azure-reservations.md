---
title: Azure-foglalások megvásárlása
description: Az Azure Reservationst a Partnerközpont API-val vásárolhatja meg a meglévő Microsoft Azure-előfizetésén (MS-AZR-0145P) vagy Azure-csomagon keresztül.
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ed8aa12117e9f13f84f39c97fc87e2c8844b223bd913cbaebf870d7022959dbd
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997294"
---
# <a name="purchase-azure-reservations"></a>Azure-foglalások megvásárlása

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont a Microsoft Cloud for US Government

Ahhoz, hogy Azure-foglalást vásároljon egy ügyfél számára a Partnerközpont API-val, meglévő Microsoft Azure-**(MS-AZR-0145P)** előfizetéssel vagy Azure-csomagtal kell rendelkezik számukra.

> [!NOTE]
> Az Azure-foglalások a következő piacokon nem érhetők el:
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

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Aktív CSP Azure-előfizetés vagy Azure-csomag előfizetés-azonosítója.

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Foglalások vásárlása Microsoft Azure vásárlása

Miután azonosította az aktív CSP Azure-előfizetést, amelybe Azure-foglalást szeretne hozzáadni, a következő lépésekkel vásárolhatja meg:

1. [Engedélyezés –](#enablement) Regisztráljon egy aktív CSP Azure-előfizetést, hogy lehetővé tegye az Azure Reservations megvásárlását.

2. [Felderítés](#discovery) – Keresse meg és válassza ki a megvásárolni kívánt Azure-beli foglalási termékeket és termékegységeket (SKUs), és ellenőrizze azok rendelkezésre állását.

3. [Megrendelés beküldve](#order-submission) – Hozzon létre egy bevásárlókosarat a rendelésben lévő elemekkel, és küldje el.

4. [Megrendelés részleteinek](#get-order-details) lekérte – Áttekinti egy megrendelés részleteit, az ügyfél összes rendelését, vagy megtekintheti a megrendeléseket a számlázási ciklus típusa szerint.

Miután megvásárolta az Azure Reservationst, a következő forgatókönyvek azt mutatják be, hogyan kezelheti az életciklusukat az Azure-beli foglalási jogosultságokkal kapcsolatos információk lekérésével, valamint az egyenlegre vonatkozó utasítások, számlák és számlaösszegzők lekérésével.

- [Életciklus-kezelés](#lifecycle-management)
- [Számla és egyeztetés](#invoice-and-reconciliation)

## <a name="enablement"></a>Engedélyezés

Az engedélyezés azt jelenti, hogy egy meglévő Microsoft Azure-**(MS-AZR-0145P)** előfizetést társít egy Azure-beli fenntartott virtuálisgép-példányhoz az előfizetés regisztrálása révén, hogy engedélyezve legyen az Azure Reservations számára. A regisztráció előfeltétele a Azure Reserved VM Instances.

A következő feladatok támogatásához előfizetés szükséges:

1. Annak ellenőrzéséhez, hogy az ügyfél jogosult-e erőforrások üzembe helyezésére, és hogy Azure Reserved VM Instances régióba vagy nem.

2. Kapacitási prioritást biztosít az előfizetésen üzemelő példányok számára. Ez csak egy hatókörre vonatkozik, Azure Reserved VM Instances a kapacitás prioritása **beállítás** van kiválasztva.

Miután azonosította az aktív előfizetést, amelybe hozzá szeretné adni az Azure-foglalást, regisztrálnia kell az előfizetést, hogy engedélyezve legyen az Azure Reservationshez. Ha regisztrálnia kell egy meglévő [előfizetési](subscription-resources.md) erőforrást, hogy az azure reservations rendelése engedélyezve legyen, tekintse meg [az előfizetés regisztrálását.](register-a-subscription.md)

Az előfizetés regisztrálása után a regisztrációs állapot ellenőrzésével ellenőriznie kell, hogy a regisztrációs folyamat befejeződött-e. Ehhez lásd: [Előfizetés regisztrációs állapotának lekért állapota.](get-subscription-registration-status.md)

> [!NOTE]
> Amikor azure Microsoft Azure csomaggal vásárol egy ügyfelet, először regisztrálnia kell az Azure-csomagját. A Microsoft Azure (**MS-AZR-0145P**) előfizetéshez hasonlóan az Azure-csomagokat egy [Partnerközpont-előfizetési erőforrás képviseli.](subscription-resources.md) Ezért használhatja ugyanazt [](register-a-subscription.md) az Előfizetés regisztrálása metódust az Azure-csomag regisztrálásához.

## <a name="discovery"></a>Felderítés

Miután engedélyezte az előfizetés számára az Azure Reservations megvásárlását, kiválaszthatja a termékeket és a termékkódokat, és ellenőrizheti azok rendelkezésre állását az alábbi api-Partnerközpont használatával:

- [Termék](product-resources.md#product) – A cserélhető termékek vagy szolgáltatások csoportosítási konstrukciója. A termék önmagában nem cserélhető elem.

- [Termékváltozat](product-resources.md#sku) – Egy terméken elérhető SKU. Ezek a termék különböző alakjai.

- [Rendelkezésre állás](product-resources.md#availability) – Olyan konfiguráció, amelyben egy termékváltozat megvásárolható (például ország, pénznem és iparági szegmens).

Azure-foglalás vásárlása előtt kövesse az alábbi lépéseket:

1. Azonosítsa és lekéri a megvásárolni kívánt terméket és termékváltozatot. Ehhez először listázást kell választania a termékekről és a termékváltozatról, vagy ha már ismeri a termék és a termékváltozatok listáját, válassza ki őket.

   - [Termékek listájának lekérése (ország alapján)](get-a-list-of-products.md)
   - [Termék lekérte a termékazonosítót](get-a-product-by-id.md)
   - [Egy termék termékváltozatait tartalmazó lista lekérése (ország alapján)](get-a-list-of-skus-for-a-product.md)
   - [Termékváltozat lekérte a termékváltozat azonosítójával](get-a-sku-by-id.md)

2. Ellenőrizze a leltárban, hogy van-e termékváltozat. Erre a lépésre csak az **InventoryCheck** előfeltételként megjelölt termékkódok esetén van szükség.

   - [Leltár ellenőrzése](check-inventory.md)

3. A [termékváltozat rendelkezésre](product-resources.md#availability) [állásának lekérése.](product-resources.md#sku) A rendelés leadáskor szüksége lesz a rendelkezésre állás **CatalogItemId-ére.** Ezt az értéket a következő API-k egyikével használhatja:

   - [Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ország alapján)](get-a-list-of-availabilities-for-a-sku.md)
   - [Rendelkezésre állás le szolgáltatása a rendelkezésre állási azonosítóval](get-an-availability-by-id.md)

> [!IMPORTANT]
> Minden Microsoft Azure termék eltérő Microsoft Azure (**MS-AZR-0145P**) előfizetéshez és Azure-csomaghoz. A terméklistát [(országonként)](get-a-list-of-products.md)vagy termékváltozatok listájának lekérte [(országonként)](get-a-list-of-skus-for-a-product.md)vagy a Termékváltozatok elérhetőségi listájának lekérte [(ország szerint)](get-a-list-of-availabilities-for-a-sku.md) beállításhoz adja meg a "reservationScope=AzurePlan" paramétert.

## <a name="order-submission"></a>Rendelés beküldve

Az Azure-foglalási rendelés elküld végrehajtásához tegye a következőket:

1. Hozzon létre egy kosárt, amely a megvásárolni kívánt katalóguselemek gyűjteményét tartalmazza. A kosár [létrehozásakor](cart-resources.md)a [](cart-resources.md#cartlineitem) kosársor elemei automatikusan csoportosítva lesznek az alapján, hogy mi vásárolható együtt ugyanabban a [rendelésben.](order-resources.md)

   - [Bevásárlókocsi létrehozása](create-a-cart.md)
   - [Bevásárlókocsi frissítése](update-a-cart.md)

2. Nézze meg a kosárt. Ha kiveszi a kosárból a rendelést, a rendelés is [létre lesz hozva.](order-resources.md)

   - [A kosár kiveszi a kosárból](checkout-a-cart.md)

## <a name="get-order-details"></a>Megrendelés részleteinek lekérte

Az Azure-beli foglalási rendelés létrehozása után lekérheti egy adott rendelés részleteit a rendelés azonosítójával, vagy lekérheti egy ügyfél megrendelési listáját. A rendelés elküldés és az ügyfél rendelési listájában való megjelenése között akár 15 perces késés is lehet.

- Egy adott rendelés részleteinek lekért adatai a rendelésazonosítóval. Lásd: [Rendelés lekért azonosítója.](get-an-order-by-id.md)

- Egy ügyfél rendelési listájának lekért listája az ügyfél azonosítójával. Lásd: [Egy ügyfél összes rendelésének lekérte.](get-all-of-a-customer-s-orders.md)

- Ha le kell kapnia egy ügyfél megrendeléseit a számlázási ciklus típusa [alapján,](product-resources.md#billingcycletype) így külön listába foglalhatók az Azure-beli foglalási rendelések (egyszeres díjak) és az éves vagy havi számlázású rendelések. Lásd: [Rendelések listájának lekérte ügyfél és számlázási ciklustípus szerint.](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)

## <a name="lifecycle-management"></a>Életciklus-kezelés

Az Azure-foglalások életciklusának Partnerközpont részeként a foglalási rendelés azonosítójával lekérheti az Azure-beli foglalás jogosultságai adatait, és lekérheti a foglalás részleteit. [](entitlement-resources.md) Ennek mikéntjére vonatkozó példákért lásd: [Get entitlements (Jogosultságok lekérte).](get-a-collection-of-entitlements.md)   

## <a name="invoice-and-reconciliation"></a>Számla és egyeztetés

Az alábbi forgatókönyvek azt mutatják be, hogyan [](invoice-resources.md)lehet programozott módon megtekinteni az ügyfelek számláit, és hogyan lehet lekérte a fiókegyenlegeket és az Azure Reservations-beli egyszer fizetendő díjakat is magukban foglaló összegzéseket.

### <a name="balance-and-payment"></a>Egyenleg és kifizetés

Ha az aktuális számlaegyenleget az alapértelmezett pénznemben,amely az ismétlődő és az egyszeri (Azure-foglalási) díjak egyenlegét is tartalmazza, tekintse meg az aktuális fiókegyenleg lekért [egyenlegét.](get-the-reseller-s-current-account-balance.md)

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
