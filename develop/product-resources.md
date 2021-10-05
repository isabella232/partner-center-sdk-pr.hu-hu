---
title: Termékek erőforrásai
description: A cserélhető termékeket vagy szolgáltatásokat képviselő erőforrások. A termék típusának és alakjának (SKU) leírására, valamint a termék leltárban való elérhetőségének ellenőrzésére vonatkozó forrásokat tartalmaz.
ms.date: 02/16/2016
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 20e2d7bcaf1041f186f0723d7ff453bebbe46dd2
ms.sourcegitcommit: f112efee7344d739bdbf385adba0c554ea2a63e3
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/04/2021
ms.locfileid: "129439361"
---
# <a name="products-resources"></a>Termékek erőforrásai

A cserélhető termékeket vagy szolgáltatásokat képviselő erőforrások. A termék típusának és alakjának (SKU) leírására, valamint a termék leltárban való elérhetőségének ellenőrzésére vonatkozó forrásokat tartalmaz.

## <a name="product"></a>Termék

Egy véglegesen használható jó vagy szolgáltatás. A termék önmagában nem cserélhető elem.

| Tulajdonság           | Típus                          | Leírás                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | sztring                        | A termék azonosítója.                                                 |
| cím              | sztring                        | A termék címe.                                                       |
| leírás        | sztring                        | A termék leírása.                                                 |
| productType        | [Itemtype](#itemtype)         | A termék típuskategorizálását leíró objektum.     |
| isMicrosoftProduct | logikai                          | Jelzi, hogy ez egy Microsoft-termék-e.                          |
| publisherName      | sztring                        | A termék közzétevője neve, ha elérhető.                          |
| Linkek              | [ProductLinks (Termékkapcsolatok)](#productlinks) | A termékben található erőforrás-hivatkozások.                         |

## <a name="itemtype"></a>ItemType

Egy termék típusát jelöli.

| Tulajdonság        | Típus                          | Leírás                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | sztring                        | A típusazonosító.                                                                 |
| displayName     | sztring                        | A típus megjelenítendő neve.                                                      |
| Altípus         | [Itemtype](#itemtype)         | Választható. Az elemtípus altípusának kategorizálását leíró objektum.     |

## <a name="productlinks"></a>ProductLinks (Termékkapcsolatok)

Egy termékre mutató hivatkozások [listáját tartalmazza.](#product)

| Tulajdonság        | Típus                                                          | Leírás                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| Skus            | [Link](utility-resources.md#link)                             | A mögöttes SKUs elérésére szolgáló hivatkozás.          |
| Linkek           | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | Az erőforrásban található erőforrás-hivatkozások.   |

## <a name="sku"></a>SKU

Egy termék alatt található, cserélhető készletnyilvántartó egységet (SKU- t) képvisel. Ezek a termék különböző alakjai.

| Tulajdonság               | Típus             | Leírás                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | sztring           | A termékváltozat azonosítója. Ez az azonosító csak a szülőtermék környezetében egyedi. |
| cím                  | sztring           | A termékváltozat címe.                                                                 |
| leírás            | sztring           | A termékváltozat leírása.                                                           |
| productId              | sztring           | A termékváltozatot tartalmazó szülő [termék](#product) azonosítója.                      |
| minimumQuantity        | int              | A vásárláshoz engedélyezett minimális mennyiség.                                            |
| maximumQuantity        | int              | A vásárláshoz engedélyezett maximális mennyiség.                                            |
| isTrial (isTrial)                | logikai             | Azt jelzi, hogy ez a termékváltozat próbaverziós elem-e.                                           |
| supportedBillingCycles | sztringek tömbje | Az ehhez a termékváltozathoz támogatott számlázási ciklusok listája. A támogatott értékek a [BillingCycleType](#billingcycletype)típusban található tagnevek. |
| purchasePrerequisites  | sztringek tömbje | Az elem megvásárlása előtt szükséges előfeltételek és műveletek listája. A támogatott értékek a következőek:<br/>  "InventoryCheck" – Azt jelzi, hogy az elem leltárát ki kell értékelni az elem megvásárlása előtt.<br/> "AzureSubscriptionRegistration" – Azt jelzi, hogy Azure-előfizetésre van szükség, és a vásárlás előtt regisztrálni kell.  |
| inventoryVariables     | sztringek tömbje | Az elem leltárellenőrzésének végrehajtásához szükséges változók listája. A támogatott értékek a következőek:<br/> "CustomerId" ( Ügyfélazonosító) – Annak az ügyfélnek az azonosítója, aki számára a vásárlást szeretné.<br/> "AzureSubscriptionId" – Az Azure-foglalás vásárlásához használt Azure-előfizetés azonosítója.</br> "ArmRegionName" – Az a régió, amelyben ellenőrizni kell a leltárt. Ennek az értéknek meg kell egyeznie a termékváltozat DynamicAttributes tulajdonságában megadott "ArmRegionName" értékkel. |
| provisioningVariables  | sztringek tömbje | Azon változók listája, amelyek a kosársorelem [](cart-resources.md#cartlineitem) kiépítési környezetében vannak megtéve az elem megvásárlásakor. A támogatott értékek a következőek:<br/> Hatókör – Az Azure-foglalás vásárlásának hatóköre: "Egy", "Megosztott".<br/> "SubscriptionId" – Az Azure-foglalás vásárlásához használt Azure-előfizetés azonosítója.<br/> "Időtartam" – Az Azure-foglalás időtartama: "1Év", "3Év".  |
| dynamicAttributes (dinamikus attribútumok)      | kulcs/érték párok  | Az erre az elemre vonatkozó dinamikus tulajdonságok szótára. A szótárban a tulajdonságok dinamikusak, és értesítés nélkül változhatnak. Ne hozzon létre erős függőségeket a tulajdonság értékében meglévő adott kulcsokhoz.    |
| Linkek                  | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks) | A termékváltozatban található erőforrás-hivatkozások.                   |
| AttestationProperties (Igazolástulajdonságok)                  | [AttestationProperties (Igazolástulajdonságok)](#attestationproperties) | Egy termékváltozat igazolási tulajdonságai.                   |
| consumptionType (felhasználási típus)                  | sztring | Csak akkor érhető el, ha a termékváltozat támogatja a használatot, például *a túlfelhasználást.*               |

## <a name="dynamic-sku-attributes"></a>Dinamikus termékváltozat-attribútumok

Az új kereskedelmi licencalapú termékekhez és szolgáltatásokhoz kapcsolódó fontos tulajdonságok.

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesző partnerek számára érhetők el

| Tulajdonság        | Típus                        | Leírás                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
|hasConstraints (hasConstraints)|boolean|Leírja, hogy a termékváltozat tartalmaz-e assetContraints adatokat|
|isAddon|boolean|Leírja, hogy a termékváltozat bővítmény-e|
|prerequisiteSkus|sztringek tömbje|Ismerteti azokat a termékeket és terméktermékeket, amelyeken a bővítmény működni tud|
|upgradeTargetOffers|sztringek tömbje|Azon termékek és terméktermékek listája, amelyekre az elem frissíthet|
|converstionInstructions|converstionInstructions listája|A konvergens műveletekre vonatkozó utasítások listája|

## <a name="availability"></a>Rendelkezésre állás

Olyan konfigurációt képvisel, amelyben egy termékváltozat megvásárolható (például ország, pénznem és iparági szegmens).

| Tulajdonság        | Típus                        | Leírás                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | sztring                        | A rendelkezésre állás azonosítója. Ez az azonosító csak a szülőtermék és a termékváltozat kontextusában [egyedi.](#sku) [](#product) **Megjegyzés** Ez az azonosító idővel változhat. Erre az értékre a leolvasás után csak rövid időn belül szabad támaszkodnia.  |
| productId       | sztring                        | A rendelkezésre állást [tartalmazó](#product) termék azonosítója.           |
| skuId (termékváltozat-azonosító)           | sztring                        | A rendelkezésre állást tartalmazó [termékváltozat](#sku) azonosítója.                   |
| catalogItemId (katalógusazonosító)   | sztring                        | Az elem egyedi azonosítója a katalógusban. Ezt az azonosítót kell feltölteni az [OrderLineItem.OfferId](order-resources.md#orderlineitem) vagy [a CartLineItem.CatalogItemId](cart-resources.md#cartlineitem) tulajdonságokba a szülő [termékváltozat megvásárlásakor.](#sku) **Megjegyzés** Ez az azonosító idővel változhat. Erre az értékre a lekért adatok beolvasása után rövid időn belül támaszkodhat. Csak a vásárláskor szabad hozzáférni és használni.  |
| defaultCurrency (alapértelmezettcurrency) | sztring                        | A rendelkezésre álláshoz támogatott alapértelmezett pénznem.                               |
| segment         | sztring                        | A rendelkezésre állás iparági szegmense. Támogatott értékek: Kereskedelmi, Oktatási, Kormányzati, Non Profit. |
| ország         | sztring                                              | Az ország vagy régió (ISO országkód-formátumban), ahol ez a rendelkezésre állás érvényes. |
| isPurchasable   | logikai                                                | Azt jelzi, hogy ez a rendelkezésre állás cserélhető-e. |
| isRenewable     | logikai                                                | Jelzi, hogy ez a rendelkezésre állás megújítható-e. |
| RenewalInstructions     | RenewalInstruction                                              | Egy adott rendelkezésre állás megújítási utasításait jelöli. |
| product      | [Product](#product)               | Az a termék, amely ennek a rendelkezésre állásnak felel meg. |
| Sku          | [Sku](#sku)            | Az a termékváltozat, amely ennek a rendelkezésre állásnak felel meg. |
| Feltételek           | [Kifejezés-erőforrások tömbje](#term)  | Az erre a rendelkezésre állásra vonatkozó feltételek gyűjteménye. |
| Linkek           | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks) | A rendelkezésre állásban található erőforrás-hivatkozások. |

## <a name="renewal-instruction"></a>Megújítási utasítás

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesz partnerek számára érhetők el
> 

Egy adott rendelkezésre állás megújítási utasításait jelöli.

| Tulajdonság        | Típus                        | Leírás                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------|
| applicableTermIds (érvényes időazonosítók)       | sztringek tömbje                       | Az utasítások által tartalmazott kifejezés-edik |
| RenewalOptions (Megújításilehetőségek)       | RenewalOption tömb                     | Megújításokat definiáló beállítások |

## <a name="renewaloption"></a>RenewalOption (Megújítási beállítás)    

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesz partnerek számára érhetők el
> 

Egy adott rendelkezésre állás megújítási utasításait jelöli.

| Tulajdonság        | Típus                        | Leírás                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------|
| renewToId (megújításiazonosító)       | Sztring       | Azt a terméket és termékváltozatot jelöli, amelybe meg kell újítani |
| isAutoRenewable       | Logikai       | Azt határozza meg, hogy a rendelkezésre állás megújítható-e automatikusan |

## <a name="term"></a>Időszak

Egy olyan időszak, amelyre a rendelkezésre állás megvásárolható.

| Tulajdonság              | Típus                                        | Leírás                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| duration              | sztring                                      | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek: P1M (1 hónap), P1Y (1 év) és P3Y (3 év). |
| leírás           | sztring                                      | A kifejezés leírása.           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest (Leltárellenőrzési kérdés)

A leltár bizonyos katalóguselemekre vonatkozó ellenőrzési kérését jelöli.

| Tulajdonság         | Típus                                                | Leírás                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems (célértékek)      | [InventoryItem tömbje](#inventoryitem)            | A leltárellenőrzés által kiértékelt katalóguselemek listája.                           |
| inventoryContext | kulcs/érték párok                                     | A leltár-ellenőrzés elvégzéséhez szükséges környezeti értékek szótára. A [termékek minden termékváltozata](#sku) határozza meg, hogy a művelet végrehajtásához mely értékekre van szükség (ha van ilyen).  |
| Linkek            | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks) | A leltárellenőrzési kérelemben található erőforrás-hivatkozások.                            |

## <a name="inventoryitem"></a>InventoryItem (Leltár)

Egy leltárellenőrzési művelet egyetlen elemét jelöli. Ez az erőforrás a célelemek megadására használatos egy bemeneti kérelemben, és a készletellenőrzési művelet kimeneti eredményeinek jelölésére is használható.

| Tulajdonság         | Típus                                                              | Leírás                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | sztring                                                            | (Kötelező) A termék [azonosítója.](#product)                            |
| skuId (termékváltozatazonosító)            | sztring                                                            | A termékváltozat [azonosítója.](#sku) Ha ezt az erőforrást használja egy leltárkérés bemeneteként, ez az érték nem kötelező. Ha ez az érték nincs megszava, akkor a termék alatt lévő összes terméktermék a leltárellenőrzési művelet céljaként lesz figyelembe véve.      |
| isRestricted     | logikai                                                              | Azt jelzi, hogy az elem korlátozott leltárkészlettel van-e.            |
| Korlátozások     | [InventoryRestriction tömb](#inventoryrestriction)            | Az elemre vonatkozó korlátozások részletei. Ez a tulajdonság csak akkor lesz kitöltve, **ha isRestricted** = "true". |

## <a name="inventoryrestriction"></a>InventoryRestriction (InventoryRestriction)

Egy leltárkorlát részleteit jelöli. Ez csak a leltár-ellenőrzés kimeneti eredményeire vonatkozik, a bemeneti kérések esetén nem.

| Tulajdonság         | Típus                  | Leírás                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode (okkód)       | sztring                | A korlátozás okát azonosító kód.                                    |
| leírás      | sztring                | A leltárkorlát leírása.                                               |
| properties       | kulcs/érték párok       | A korlátozással kapcsolatos további részleteket tartalmazó tulajdonságok szótára.           |

## <a name="billingcycletype"></a>BillingCycleType (Számlázási ciklustípus)

Egy [Enum/dotnet/api/system.enum), amely a számlázási ciklus típusát jelző értékeket tartalmaz.

| Érték              | Pozíció     | Leírás                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Ismeretlen            | 0            | Enum initializer.                                                                          |
| Havonta            | 1            | Azt jelzi, hogy a partnernek havonta kell fizetnie.                                        |
| Évi             | 2            | Azt jelzi, hogy a partnernek évente kell fizetnie.                                       |
| None               | 3            | Azt jelzi, hogy a partner nem számít fel díjat. Ez az érték próbaelemekhez használható.    |
| OneTime (Egyidő)            | 4            | Azt jelzi, hogy a partnernek egyszer kell fizetnie.                                       |

## <a name="attestationproperties"></a>AttestationProperties (Igazolástulajdonságok)

Egy igazolástípust és azt jelöli, hogy szükséges-e a vásárláshoz.

| Tulajdonság              | Típus                                        | Leírás                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType (igazolás típusa)              | sztring                                      | Az igazolás típusát jelzi. A Windows 365 esetén az érték Windows365. Windows 365-ös igazolás szövege: "Megértettem, hogy a Windows 365 Business with Windows Hybrid Benefitet használó minden személynek az Windows 10/11 Pro érvényes példányát is telepítenie kell az elsődleges munkahelyi eszközére." |
| enforceAttestation           | boolean                                      | Azt jelzi, hogy a vásárláshoz szükség van-e igazolásra.           |
