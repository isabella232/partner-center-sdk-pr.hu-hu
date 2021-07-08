---
title: Azure-foglalások megvásárlása
description: Az Azure Reservationst az ügyfelek számára a Partnerközpont API-val vásárolhatja meg a meglévő Microsoft Azure-előfizetésén (MS-AZR-0145P) vagy Azure-csomagon keresztül.
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0b9ce4a808ac12c32bd67888fc92808baeb0e575
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547767"
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
> | Cocos (Keeling)-szigetek        | Mali                              | St Majda, Ascension, Tristan da Canha   |
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

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Aktív CSP Azure-előfizetés vagy Azure-csomag előfizetés-azonosítója.

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Foglalások Microsoft Azure vásárlása

Miután azonosította az aktív CSP Azure-előfizetést, amelybe Azure-foglalást szeretne hozzáadni, a következő lépésekkel vásárolhatja meg:

1. [Engedélyezés – Regisztráljon](#enablement) egy aktív CSP Azure-előfizetést, hogy lehetővé tegye az Azure Reservations megvásárlását.

2. [Felderítés](#discovery) – Keresse meg és válassza ki a megvásárolni kívánt Azure-beli foglalási termékeket és termékegységeket (SKUs), és ellenőrizze azok rendelkezésre állását.

3. [Megrendelés beküldve](#order-submission) – Hozzon létre egy bevásárlókosarat a rendelésben lévő elemekkel, és küldje el.

4. [Megrendelés részleteinek](#get-order-details) lekérte – Áttekinti egy megrendelés részleteit, az ügyfél összes rendelését, vagy megtekintheti a megrendeléseket a számlázási ciklus típusa szerint.

Miután megvásárolta az Azure Reservationst, a következő forgatókönyvek azt mutatják be, hogyan kezelheti az életciklusát az Azure-beli foglalási jogosultságok információinak lekérésével, valamint az egyenlegre vonatkozó utasítások, számlák és számlaösszegzők lekérésével.

- [Életciklus-kezelés](#lifecycle-management)
- [Számla és egyeztetés](#invoice-and-reconciliation)

## <a name="enablement"></a>Engedélyezés

Az engedélyezés azt jelenti, hogy egy meglévő Microsoft Azure-**(MS-AZR-0145P)** előfizetést társít egy Azure-beli fenntartott virtuálisgép-példányhoz úgy, hogy regisztrálja az előfizetést, hogy engedélyezve legyen az Azure Reservations számára. A regisztráció előfeltétele a Azure Reserved VM Instances.

A következő feladatok támogatásához előfizetés szükséges:

1. Annak ellenőrzése, hogy az ügyfél jogosult-e erőforrások üzembe helyezésére, és Azure Reserved VM Instances-előfizetést vásárolni egy régióban vagy sem.

2. Kapacitási prioritást biztosít az előfizetésen üzemelő példányok számára. Ez csak egy hatókörre vonatkozik, Azure Reserved VM Instances a kapacitás prioritása **beállítás** van kiválasztva.

Miután azonosította az aktív előfizetést, amelybe hozzá szeretné adni az Azure-foglalást, regisztrálnia kell az előfizetést, hogy engedélyezve legyen az Azure Reservationshez. Ha regisztrálnia kell egy meglévő [előfizetési](subscription-resources.md) erőforrást, hogy az azure-foglalások rendelése engedélyezve legyen, tekintse meg [az előfizetés regisztrálását.](register-a-subscription.md)

Az előfizetés regisztrálása után a regisztrációs állapot ellenőrzésével ellenőriznie kell, hogy a regisztrációs folyamat befejeződött-e. Ehhez lásd: [Előfizetés regisztrációs állapotának lekért állapota.](get-subscription-registration-status.md)

> [!NOTE]
> Ha azure Microsoft Azure csomaggal vásárol egy ügyfelet, először regisztrálnia kell az Azure-csomagját. A Microsoft Azure (**MS-AZR-0145P**) előfizetéshez hasonlóan az Azure-csomagokat egy [Partnerközpont-előfizetési](subscription-resources.md) erőforrás képviseli. Ezért használhatja ugyanazt az Előfizetés regisztrálása [metódust](register-a-subscription.md) az Azure-csomag regisztrálásához.

## <a name="discovery"></a>Felderítés

Miután engedélyezte az előfizetés számára az Azure Reservations megvásárlását, kiválaszthatja a termékeket és a terméktermékeket, és ellenőrizheti azok rendelkezésre állását az alábbi API-Partnerközpont használatával:

- [Termék](product-resources.md#product) – Egy csoportosítási szerkezet a cserélhető termékekhez vagy szolgáltatásokhoz. A termék önmagában nem cserélhető elem.

- [Termékváltozat](product-resources.md#sku) – Egy terméken elérhető, véglegesen cserélhető termékváltozat. Ezek a termék különböző alakjai.

- [Rendelkezésre állás](product-resources.md#availability) – Olyan konfiguráció, amelyben egy termékváltozat megvásárolható (például ország, pénznem és iparági szegmens).

Azure-foglalás vásárlása előtt kövesse az alábbi lépéseket:

1. Azonosítsa és lekéri a megvásárolni kívánt terméket és termékváltozatot. Ehhez először listázást kell választania a termékekről és a termékváltozatról, vagy ha már ismeri a termék és a termékváltozatok listáját, válassza ki őket.

   - [Termékek listájának lekérése (ország alapján)](get-a-list-of-products.md)
   - [Termék lekérte a termékazonosítót](get-a-product-by-id.md)
   - [Egy termék termékváltozatait tartalmazó lista lekérése (ország alapján)](get-a-list-of-skus-for-a-product.md)
   - [Termékváltozat lekérte a termékváltozat azonosítójával](get-a-sku-by-id.md)

2. Ellenőrizze a leltárban, hogy van-e termékváltozat. Erre a lépésre csak az **InventoryCheck** előfeltételként megjelölt termékkódok esetén van szükség.

   - [Leltár ellenőrzése](check-inventory.md)

3. A [termékváltozat](product-resources.md#availability) rendelkezésre [állásának lekérése.](product-resources.md#sku) A rendelés leadáskor szüksége lesz a rendelkezésre állás **CatalogItemId-ére.** Ezt az értéket a következő API-k egyikével használhatja:

   - [Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ország alapján)](get-a-list-of-availabilities-for-a-sku.md)
   - [Rendelkezésre állás lekérte a rendelkezésre állási azonosítóval](get-an-availability-by-id.md)

> [!IMPORTANT]
> Minden Microsoft Azure termék eltérő Microsoft Azure (**MS-AZR-0145P**) előfizetéshez és Azure-csomaghoz. A terméklistát [(ország szerint)](get-a-list-of-products.md)vagy termékváltozatok listájának lekérte (országonként) vagy egy termékváltozat rendelkezésre állási listájának lekért [listáját (ország szerint),](get-a-list-of-availabilities-for-a-sku.md) adja meg a "reservationScope=AzurePlan" paramétert. [](get-a-list-of-skus-for-a-product.md)

## <a name="order-submission"></a>Rendelés beküldve

Az Azure-foglalási rendelés elküld végrehajtásához tegye a következőket:

1. Hozzon létre egy kosárt, amely a megvásárolni kívánt katalóguselemek gyűjteményét tartalmazza. A kosár [létrehozásakor](cart-resources.md)a [](cart-resources.md#cartlineitem) kosársor elemei automatikusan csoportosítva lesznek az alapján, hogy mi vásárolható együtt ugyanabban a [rendelésben.](order-resources.md)

   - [Bevásárlókocsi létrehozása](create-a-cart.md)
   - [Bevásárlókocsi frissítése](update-a-cart.md)

2. Nézze meg a kosárt. A kosár ellenőrzésekor a rendelés is létre lesz [hozva.](order-resources.md)

   - [A kosár kiveszi](checkout-a-cart.md)

## <a name="get-order-details"></a>Megrendelés részleteinek lekérte

Az Azure-beli foglalási rendelés létrehozása után lekérheti egy adott rendelés részleteit a rendelés azonosítójával, vagy lekérheti egy ügyfél rendelési listáját. A rendelés beküldés és az ügyfél rendelési listájában való megjelenése között akár 15 perces késés is lehet.

- Egy adott rendelés részleteinek lekért adatai a rendelés azonosítójával. Lásd: [Rendelés lekért azonosítója.](get-an-order-by-id.md)

- Egy ügyfél rendelési listájának lekért listája az ügyfél azonosítójával. Lásd: [Egy ügyfél összes rendelésének lekért rendelése.](get-all-of-a-customer-s-orders.md)

- Ha le kell kapnia egy ügyfél rendelési listáját a számlázási ciklus típusa [szerint,](product-resources.md#billingcycletype) amely lehetővé teszi az Azure-beli foglalási rendelések (egyszeres díjak) és az éves vagy havi számlázású rendelések külön-külön való felsorolását. Lásd: [Rendelések listájának lekérte ügyfél és számlázási ciklustípus szerint.](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)

## <a name="lifecycle-management"></a>Életciklus-kezelés

Az Azure Reservations életciklusának Partnerközpont részeként lekérheti az Azure-beli foglalás [](entitlement-resources.md)jogosultságai adatait, és lekérheti a foglalás részleteit a foglalási rendelés azonosítójával. Erre vonatkozó példákért lásd: [Jogosultságok lekérte.](get-a-collection-of-entitlements.md)   

## <a name="invoice-and-reconciliation"></a>Számla és egyeztetés

A következő forgatókönyvek azt mutatják be, hogyan [](invoice-resources.md)lehet programozott módon megtekinteni az ügyfél számláit, és hogyan lehet lekért fiókegyenlegeket és összegzéseket, amelyek tartalmazzák az Azure-foglalások egyszeres díjeit.

### <a name="balance-and-payment"></a>Egyenleg és kifizetés

Ha az aktuális számlaegyenleget az alapértelmezett pénznemtípusban,amely az ismétlődő és az egyszeri (Azure-foglalási) díjak egyenlegét is tartalmazza, lásd: Az aktuális fiókegyenleg [lekért összege](get-the-reseller-s-current-account-balance.md)

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
