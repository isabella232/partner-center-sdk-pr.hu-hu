---
title: Termékek erőforrásai
description: A megvásárolható termékeket vagy szolgáltatásokat képviselő erőforrások. A termék típusának és alakjának (SKU) leírására, valamint a termék leltárban való rendelkezésre állásának ellenőrzésére szolgáló forrásokat tartalmaz.
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6a3cfacd3654e85a9824759295f97792ff740d85
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768027"
---
# <a name="products-resources"></a>Termékek erőforrásai

**A következőkre vonatkozik**

- Partnerközpont

A megvásárolható termékeket vagy szolgáltatásokat képviselő erőforrások. A termék típusának és alakjának (SKU) leírására, valamint a termék leltárban való rendelkezésre állásának ellenőrzésére szolgáló forrásokat tartalmaz.

## <a name="product"></a>Termék

Egy megvásárolható jó vagy szolgáltatás. Egy termék önmagában nem egy megvásárolható tétel.

| Tulajdonság           | Típus                          | Leírás                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | sztring                        | A termék azonosítója.                                                 |
| cím              | sztring                        | A termék címe.                                                       |
| leírás        | sztring                        | A termék leírása.                                                 |
| productType        | [ItemType](#itemtype)         | Egy olyan objektum, amely leírja a termék kategorizálási (ek) típusát.     |
| isMicrosoftProduct | logikai                          | Azt jelzi, hogy ez egy Microsoft-termék.                          |
| publisherName      | sztring                        | A termék közzétevője neve, ha elérhető.                          |
| linkek              | [ProductLinks](#productlinks) | A terméken belül található erőforrás-hivatkozások.                         |

## <a name="itemtype"></a>ItemType

A termék típusát jelöli.

| Tulajdonság        | Típus                          | Leírás                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | sztring                        | A típusazonosító.                                                                 |
| displayName     | sztring                        | A típus megjelenítendő neve.                                                      |
| Altípus         | [ItemType](#itemtype)         | Választható. Az adott elemtípus altípusának kategorizálását leíró objektum.     |

## <a name="productlinks"></a>ProductLinks

A [termékhez](#product)tartozó hivatkozások listáját tartalmazza.

| Tulajdonság        | Típus                                                          | Leírás                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| SKUs            | [Hivatkozás](utility-resources.md#link)                             | Az alapul szolgáló SKU-kon való hozzáférésre mutató hivatkozás.          |
| linkek           | [ResourceLinks](utility-resources.md#resourcelinks)           | Az erőforráson belül található erőforrások hivatkozásai.   |

## <a name="sku"></a>SKU

Egy terméken belül egy megvásárolható készletezési egységet (SKU) jelöl. Ezek a termék különböző alakzatait jelölik.

| Tulajdonság               | Típus             | Leírás                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | sztring           | Az SKU azonosítója. Ez az azonosító csak a fölérendelt termék kontextusában egyedi. |
| cím                  | sztring           | Az SKU címe.                                                                 |
| leírás            | sztring           | Az SKU leírása.                                                           |
| productId              | sztring           | Az adott SKU-t tartalmazó szülő [termék](#product) azonosítója.                      |
| minimumQuantity        | int              | A vásárláshoz engedélyezett minimális mennyiség.                                            |
| maximumQuantity        | int              | A vásárláshoz engedélyezett maximális mennyiség.                                            |
| Isztriai                | logikai             | Azt jelzi, hogy ez az SKU egy próbaverzió-e.                                           |
| supportedBillingCycles | sztringek tömbje | Az adott SKU által támogatott számlázási ciklusok listája. A támogatott értékek a [BillingCycleType](#billingcycletype)található tagok nevei. |
| purchasePrerequisites  | sztringek tömbje | Az ezen tétel megvásárlása előtt szükséges előfeltételek vagy műveletek listája. A támogatott értékek a következők:<br/>  "InventoryCheck" – azt jelzi, hogy az elem leltárát ki kell értékelni az elem megvásárlásának megkísérlése előtt.<br/> "AzureSubscriptionRegistration" – azt jelzi, hogy szükség van egy Azure-előfizetésre, és regisztrálni kell az elem megvásárlására tett kísérlet előtt.  |
| inventoryVariables     | sztringek tömbje | Az elemre vonatkozó leltár-ellenőrzési művelet végrehajtásához szükséges változók listája. A támogatott értékek a következők:<br/> "Vevőkód" – annak az ügyfélnek az azonosítója, amelyhez a vásárlás kerülne.<br/> "AzureSubscriptionId" – az Azure-előfizetés megvásárlásához használni kívánt Azure-előfizetés azonosítója.</br> "ArmRegionName" – az a régió, amelynek a leltárát ellenőrizni kívánja. Ennek az értéknek meg kell egyeznie az SKU DynamicAttributes lévő "ArmRegionName" értékkel. |
| provisioningVariables  | sztringek tömbje | Azon változók listája, amelyeket az adott cikk megvásárlásakor meg kell adni egy [cart-tétel](cart-resources.md#cartlineitem) kiépítési környezetében. A támogatott értékek a következők:<br/> Hatókör – az Azure foglalások vásárlásának hatóköre: "single", "Shared".<br/> "SubscriptionId" – az Azure-előfizetés megvásárlásához használni kívánt Azure-előfizetés azonosítója.<br/> "Időtartam" – az Azure-foglalás időtartama: "1Year", "3Year".  |
| dynamicAttributes      | kulcs/érték párok  | Az adott elemmel kapcsolatos dinamikus tulajdonságok szótára. Vegye figyelembe, hogy az ebben a szótárban található tulajdonságok dinamikusak, és értesítés nélkül változhatnak. Ne hozzon létre erős függőségeket a tulajdonság értékében meglévő bizonyos kulcsokhoz.    |
| linkek                  | [ResourceLinks](utility-resources.md#resourcelinks) | Az SKU-ban található erőforrás-hivatkozások.                   |

## <a name="availability"></a>Rendelkezésre állás

Olyan konfigurációt jelöl, amelyben az SKU megvásárolható (például ország, pénznem és iparági szegmens).

| Tulajdonság        | Típus                        | Leírás                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | sztring                        | A rendelkezésre állás azonosítója. Ez az azonosító csak a szülő [termék](#product) és [SKU](#sku)környezetében egyedi. **Megjegyzés** Ez az azonosító idővel változhat. Ezt az értéket csak rövid időn belül kell megbíznia a lekérése után.  |
| productId       | sztring                        | A rendelkezésre állást tartalmazó [termék](#product) azonosítója.           |
| skuId           | sztring                        | A rendelkezésre állást tartalmazó [SKU](#sku) azonosítója.                   |
| catalogItemId   | sztring                        | Az adott tétel egyedi azonosítója a katalógusban. Ezt az azonosítót kell kitölteni az [OrderLineItem. OfferID](order-resources.md#orderlineitem) vagy a [CartLineItem. CatalogItemId](cart-resources.md#cartlineitem) tulajdonságban a szülő [SKU](#sku)megvásárlásakor. **Megjegyzés** Ez az azonosító idővel változhat. Ezt az értéket csak rövid időn belül kell kihasználnia a beolvasás után. A szolgáltatás csak a vásárláskor érhető el és használható.  |
| defaultCurrency | sztring                        | A rendelkezésre állás alapértelmezett pénzneme támogatott.                               |
| segment         | sztring                        | A rendelkezésre állás iparági szegmense. A támogatott értékek a következők: kereskedelmi, oktatási, kormányzati, NonProfit. |
| ország         | sztring                                              | Az az ország vagy régió (ISO-országkód formátumban), ahol ez a rendelkezésre állás érvényes. |
| isPurchasable   | logikai                                                | Azt jelzi, hogy a rendelkezésre állás megvásárolható-e. |
| isRenewable     | logikai                                                | Azt jelzi, hogy a rendelkezésre állás megújítható-e. |
| product      | [Product](#product)               | Az a termék, amely megfelel a rendelkezésre állásnak. |
| SKU          | [SKU](#sku)            | A rendelkezésre álláshoz tartozó SKU megfelel a következőnek:. |
| feltételek           | [távú](#term) erőforrások tömbje  | A rendelkezésre állásra vonatkozó feltételek gyűjteménye. |
| linkek           | [ResourceLinks](utility-resources.md#resourcelinks) | A rendelkezésre álláson belül található erőforrás-hivatkozások. |

## <a name="term"></a>Kifejezés

Azt a kifejezést jelöli, amelynek a rendelkezésre állását meg lehet vásárolni.

| Tulajdonság              | Típus                                        | Leírás                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| duration              | sztring                                      | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek a következők: P1M (1 hónap), P1Y (1 év) és P3Y (3 év). |
| leírás           | sztring                                      | A kifejezés leírása.           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

Egy olyan kérést jelöl, amely alapján ellenőrizni lehet a leltárt bizonyos katalógus elemein.

| Tulajdonság         | Típus                                                | Leírás                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | [InventoryItem](#inventoryitem) tömbje            | A leltár-ellenőrzés által kiértékelt katalógus-elemek listája.                           |
| inventoryContext | kulcs/érték párok                                     | A leltár-ellenőrzés végrehajtásához szükséges környezeti értékek szótára. A termékek egyes [SKU](#sku) -jának meghatározásakor a művelet végrehajtásához szükséges értékeket (ha vannak ilyenek) is meg kell adni.  |
| linkek            | [ResourceLinks](utility-resources.md#resourcelinks) | A leltár-ellenőrzési kérelemben szereplő erőforrások hivatkozásai.                            |

## <a name="inventoryitem"></a>InventoryItem

Egy leltár-ellenőrzési művelet egyetlen elemét jelöli. Ez az erőforrás egy bemeneti kérelemben szereplő célcsoportok megadására szolgál, és a leltár-ellenőrzési művelet kimeneti eredményeinek ábrázolására is használható.

| Tulajdonság         | Típus                                                              | Leírás                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | sztring                                                            | Szükséges A [termék](#product)azonosítója.                            |
| skuId            | sztring                                                            | Az [SKU](#sku)azonosítója. Ha ezt az erőforrást egy leltári kérelemhez bemenetként használja, ez az érték nem kötelező. Ha ez az érték nincs megadva, akkor a termékben lévő összes SKU a leltár-ellenőrzési művelet célként megadott elemeinek tekintendő.      |
| isRestricted     | logikai                                                              | Azt jelzi, hogy az adott objektum korlátozott leltárral rendelkezik-e.            |
| korlátozások     | [InventoryRestriction](#inventoryrestriction) tömbje            | Az adott elemmel kapcsolatban talált korlátozások részletei. Ez a tulajdonság csak akkor lesz feltöltve, ha **isRestricted** = "true". |

## <a name="inventoryrestriction"></a>InventoryRestriction

A leltárra vonatkozó korlátozás részleteit jelöli. Ez csak a leltár-ellenőrzési kimenet eredményeire vonatkozik, nem a bemeneti kérésekhez.

| Tulajdonság         | Típus                  | Leírás                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | sztring                | A korlátozás okát azonosító kód.                                    |
| leírás      | sztring                | A leltár korlátozásának leírása.                                               |
| properties       | kulcs/érték párok       | A korlátozással kapcsolatos további részleteket megadható tulajdonságok szótára.           |

## <a name="billingcycletype"></a>BillingCycleType

Egy [Enum/DotNet/API/System. Enum) olyan értékekkel, amelyek a számlázási ciklus típusát jelölik.

| Érték              | Pozíció     | Leírás                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Ismeretlen            | 0            | Enum inicializáló.                                                                          |
| Havonta            | 1            | Azt jelzi, hogy a partner havonta lesz felszámítva.                                        |
| Évi             | 2            | Azt jelzi, hogy a partnert évente számoljuk el.                                       |
| Nincs               | 3            | Azt jelzi, hogy a partner nem lesz felszámítva. Ezt az értéket lehet használni a próbaverziós elemekhez.    |
| Elvégezni            | 4            | Azt jelzi, hogy a partner csak egyszer lesz felszámítva.                                       |
