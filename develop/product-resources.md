---
title: Termékek erőforrásai
description: A cserélhető termékeket vagy szolgáltatásokat képviselő erőforrások. Tartalmazza a terméktípus és -alakzat (SKU) leírására, valamint a termék leltárban való elérhetőségének ellenőrzésére vonatkozó forrásokat.
ms.date: 02/16/2016
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3790d8f5ef154c637dfd3f3d014322d314757f26
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456069"
---
# <a name="products-resources"></a>Termékek erőforrásai

A cserélhető termékeket vagy szolgáltatásokat képviselő erőforrások. Tartalmazza a terméktípus és -alakzat (SKU) leírására, valamint a termék leltárban való elérhetőségének ellenőrzésére vonatkozó forrásokat.

## <a name="product"></a>Termék

Egy véglegesen használható jó vagy szolgáltatás. A termék önmagában nem cserélhető elem.

| Tulajdonság           | Típus                          | Description                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | sztring                        | A termék azonosítója.                                                 |
| cím              | sztring                        | A termék címe.                                                       |
| leírás        | sztring                        | A termék leírása.                                                 |
| productType        | [Itemtype](#itemtype)         | A termék típuskategorizálását leíró objektum.     |
| isMicrosoftProduct | logikai                          | Azt jelzi, hogy ez egy Microsoft-termék-e.                          |
| publisherName      | sztring                        | A termék közzétevője neve, ha elérhető.                          |
| Linkek              | [ProductLinks (Termékkapcsolatok)](#productlinks) | A termékben található erőforrás-hivatkozások.                         |

## <a name="itemtype"></a>ItemType

Egy termék típusát jelöli.

| Tulajdonság        | Típus                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | sztring                        | A típusazonosító.                                                                 |
| displayName     | sztring                        | A típus megjelenítendő neve.                                                      |
| Altípus         | [Itemtype](#itemtype)         | Választható. Az elemtípus altípus-kategorizálását leíró objektum.     |

## <a name="productlinks"></a>ProductLinks (Termékkapcsolatok)

Egy termékre mutató hivatkozások [listáját tartalmazza.](#product)

| Tulajdonság        | Típus                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| Skus            | [Hivatkozás](utility-resources.md#link)                             | A mögöttes SKUs elérésére szolgáló hivatkozás.          |
| Linkek           | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)           | Az erőforrásban található erőforrás-hivatkozások.   |

## <a name="sku"></a>SKU

Egy termék alatt található, véglegesen használható termékkészletet (SKU-t) képvisel. Ezek a termék különböző alakjai.

| Tulajdonság               | Típus             | Description                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | sztring           | A termékváltozat azonosítója. Ez az azonosító csak a szülőtermék környezetében egyedi. |
| cím                  | sztring           | A termékváltozat címe.                                                                 |
| leírás            | sztring           | A termékváltozat leírása.                                                           |
| productId              | sztring           | A termékváltozatot tartalmazó szülő [Termék](#product) azonosítója.                      |
| minimumQuantity (minimálisquantitás)        | int              | A vásárláshoz engedélyezett minimális mennyiség.                                            |
| maximumQuantity (Maximálisquantitás)        | int              | A vásárláshoz engedélyezett maximális mennyiség.                                            |
| isTrial (isTrial)                | logikai             | Azt jelzi, hogy ez a termékváltozat próbaverziós elem-e.                                           |
| supportedBillingCycles | sztringek tömbje | Az ehhez a termékváltozathoz támogatott számlázási ciklusok listája. A támogatott értékek a [BillingCycleType](#billingcycletype)típusban található tagnevek. |
| purchasePrerequisites  | sztringek tömbje | Az elem megvásárlása előtt szükséges előfeltételek és műveletek listája. A támogatott értékek a következőek:<br/>  "InventoryCheck" – Azt jelzi, hogy az elem leltárát ki kell értékelni az elem megvásárlása előtt.<br/> "AzureSubscriptionRegistration" – Azt jelzi, hogy azure-előfizetésre van szükség, és regisztrálni kell az elem megvásárlásának megkísérlése előtt.  |
| inventoryVariables (leltárválozók)     | sztringek tömbje | Az elem leltárellenőrzésének végrehajtásához szükséges változók listája. A támogatott értékek a következőek:<br/> "CustomerId" ( Ügyfélazonosító) – Annak az ügyfélnek az azonosítója, akitől a vásárlást adná.<br/> "AzureSubscriptionId" – Az Azure-foglalás vásárlásához használt Azure-előfizetés azonosítója.</br> "ArmRegionName" – Az a régió, amelyben ellenőrizni kell a leltárt. Ennek az értéknek egyeznie kell a termékváltozat DynamicAttributes tulajdonságában megadott "ArmRegionName" értékkel. |
| provisioningVariables  | sztringek tömbje | A kosársorelem kiépítési környezetében meg kell adni [a](cart-resources.md#cartlineitem) változók listáját az elem megvásárlásakor. A támogatott értékek a következőek:<br/> Hatókör – Az Azure-foglalások vásárlásának hatóköre: "Egyetlen", "Megosztott".<br/> "SubscriptionId" – Az Azure-foglalás vásárlásához használt Azure-előfizetés azonosítója.<br/> "Időtartam" – Az Azure-foglalás időtartama: "1Year", "3Year".  |
| dynamicAttributes (dinamikus attribútumok)      | kulcs/érték párok  | Az erre az elemre vonatkozó dinamikus tulajdonságok szótára. A szótár tulajdonságai dinamikusak, és értesítés nélkül változhatnak. Ne hozzon létre erős függőségeket a tulajdonság értékében meglévő adott kulcsokhoz.    |
| Linkek                  | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks) | A termékváltozatban található erőforrás-hivatkozások.                   |
| AttestationProperties (Igazolásitulajdonságok)                  | [AttestationProperties (Igazolásitulajdonságok)](#attestationproperties) | Egy termékváltozat igazolási tulajdonságai.                   |

## <a name="dynamic-sku-attributes"></a>Dinamikus termékváltozat-attribútumok

Az új kereskedelmi licencalapú termékekhez és szolgáltatásokhoz kapcsolódó fontos tulajdonságok.

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesz partnerek számára érhetők el

| Tulajdonság        | Típus                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
|hasConstraints (hasConstraints)|boolean|Leírja, hogy a termékváltozat tartalmaz-e assetContraints adatokat|
|isAddon|boolean|Leírja, hogy a termékváltozat bővítmény-e|
|prerequisiteSkus|sztringek tömbje|Ismerteti azokat a termékeket és terméktermékeket, amelyeken a bővítmény működni tud|
|upgradeTargetOffers|sztringek tömbje|Azon termékek és terméktermékek listája, amelyekre az elem frissíthet|
|converstionInstructions|converstionInstructions listája|A konvergens műveletekre vonatkozó utasítások listája|

## <a name="availability"></a>Rendelkezésre állás

Egy olyan konfigurációt képvisel, amelyben egy termékváltozat megvásárolható (például ország, pénznem és iparági szegmens).

| Tulajdonság        | Típus                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | sztring                        | A rendelkezésre állás azonosítója. Ez az azonosító csak a szülőtermék és a termékváltozat kontextusában [egyedi.](#sku) [](#product) **Megjegyzés** Ez az azonosító idővel változhat. Ezt az értéket a leolvasás után csak rövid időn belül szabad figyelembenia.  |
| productId       | sztring                        | A rendelkezésre állást [tartalmazó](#product) termék azonosítója.           |
| skuId (termékváltozatazonosító)           | sztring                        | A rendelkezésre állást tartalmazó [termékváltozat](#sku) azonosítója.                   |
| catalogItemId (katalógusazonosító)   | sztring                        | Az elem egyedi azonosítója a katalógusban. Ezt az azonosítót kell feltölteni az [OrderLineItem.OfferId](order-resources.md#orderlineitem) vagy [a CartLineItem.CatalogItemId](cart-resources.md#cartlineitem) tulajdonságba a szülő [termékváltozat megvásárlásakor.](#sku) **Megjegyzés** Ez az azonosító idővel változhat. Erre az értékre a leolvasás után rövid időn belül kell támaszkodnia. Csak a vásárláskor szabad hozzáférni és használni.  |
| defaultCurrency (defaultCurrency) | sztring                        | A rendelkezésre álláshoz támogatott alapértelmezett pénznem.                               |
| segment         | sztring                        | A rendelkezésre állás iparági szegmense. A támogatott értékek aek: Kereskedelmi, Oktatási, Kormányzati, Nem Pénzügyi. |
| ország         | sztring                                              | Az ország vagy régió (ISO-országkód formátumban), ahol ez a rendelkezésre állás érvényes. |
| isPurchasable   | logikai                                                | Azt jelzi, hogy ez a rendelkezésre állás cserélhető-e. |
| isRenewable     | logikai                                                | Jelzi, hogy ez a rendelkezésre állás megújítható-e. |
| RenewalInstructions     | RenewalInstruction (Megújítás instruction)                                              | Egy adott rendelkezésre állás megújítási utasításait jelöli. |
| product      | [Product](#product)               | Az a termék, amelyhez ez a rendelkezésre állás tartozik. |
| Sku          | [Sku](#sku)            | Az a termékváltozat, amely ennek a rendelkezésre állásnak felel meg. |
| Feltételek           | [Kifejezés-erőforrások tömbje](#term)  | Az erre a rendelkezésre állásra vonatkozó feltételek gyűjteménye. |
| Linkek           | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks) | A rendelkezésre állásban található erőforrás-hivatkozások. |

## <a name="renewal-instruction"></a>Megújítási utasítás

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesző partnerek számára érhetők el
> 

Egy adott rendelkezésre állás megújítási utasításait jelöli.

| Tulajdonság        | Típus                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------|
| applicableTermIds       | sztringek tömbje                       | Az utasítások által tartalmazott kifejezés-eket |
| RenewalOptions (Megújításilehetőségek)       | RenewalOption tömb                     | Megújításokat meghatározó beállítások |

## <a name="renewaloption"></a>RenewalOption (Megújítási beállítás)    

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesző partnerek számára érhetők el
> 

Egy adott rendelkezésre állás megújítási utasításait jelöli.

| Tulajdonság        | Típus                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------|
| renewToId (megújításiazonosító)       | Sztring       | Azt a terméket és termékváltozatot jelöli, amelybe meg kell újítani |
| isAutoRenewable       | Logikai       | Azt határozza meg, hogy a rendelkezésre állás megújítható-e automatikusan |

## <a name="term"></a>Időszak

Azt az kifejezést jelöli, amelyre a rendelkezésre állás megvásárolható.

| Tulajdonság              | Típus                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| duration              | sztring                                      | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek: P1M (1 hónap), P1Y (1 év) és P3Y (3 év). |
| leírás           | sztring                                      | A kifejezés leírása.           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest (Leltárellenőrzési kérdés)

A leltár bizonyos katalóguselemekre vonatkozó ellenőrzési kérését jelöli.

| Tulajdonság         | Típus                                                | Description                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems (célértékek)      | [InventoryItem tömbje](#inventoryitem)            | A leltárellenőrzés által kiértékelt katalóguselemek listája.                           |
| inventoryContext | kulcs/érték párok                                     | A leltárellenőrzés(nek) elvégzéséhez szükséges környezeti értékek szótára. A [termékek minden termékváltozata](#sku) határozza meg, hogy mely értékekre van szükség (ha vannak) a művelet végrehajtásához.  |
| Linkek            | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks) | A leltárellenőrzési kérelemben található erőforrás-hivatkozások.                            |

## <a name="inventoryitem"></a>InventoryItem (Leltár)

Egy leltárellenőrzési művelet egyetlen elemét jelöli. Ez az erőforrás a bemeneti kérelem cél elemeinek megadására, valamint a leltárellenőrzési művelet kimeneti eredményeinek jelölésére is használatos.

| Tulajdonság         | Típus                                                              | Description                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | sztring                                                            | (Kötelező) A termék [azonosítója.](#product)                            |
| skuId (termékváltozatazonosító)            | sztring                                                            | A termékváltozat [azonosítója.](#sku) Ha ezt az erőforrást használja egy leltárkérés bemeneteként, ez az érték nem kötelező. Ha ez az érték nincs megszabadva, akkor a termék alatt lévő összes terméktermék a leltárellenőrzési művelet célelemeknek minősül.      |
| isRestricted (korlátozás szerint)     | logikai                                                              | Azt jelzi, hogy az elem korlátozott leltárkészlettel van-e.            |
| Korlátozások     | [InventoryRestriction tömb](#inventoryrestriction)            | Az elemre vonatkozó korlátozások részletei. Ez a tulajdonság csak akkor lesz kitöltve, ha **isRestricted** = "true". |

## <a name="inventoryrestriction"></a>InventoryRestriction

Egy leltárkorlátozás részleteit jelöli. Ez csak a leltár-ellenőrzés kimeneti eredményeire vonatkozik, a bemeneti kérések esetén nem.

| Tulajdonság         | Típus                  | Description                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode (okkód)       | sztring                | A korlátozás okát azonosító kód.                                    |
| leírás      | sztring                | A leltárkorlát leírása.                                               |
| properties       | kulcs/érték párok       | A korlátozással kapcsolatos további részleteket tartalmazó tulajdonságok szótára.           |

## <a name="billingcycletype"></a>BillingCycleType (Számlázási ciklus típusa)

Egy [Enum/dotnet/api/system.enum) értékekkel, amelyek a számlázási ciklus típusát jelzik.

| Érték              | Pozíció     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Ismeretlen            | 0            | Felsorolási inicializáló.                                                                          |
| Havonta            | 1            | Azt jelzi, hogy a partnernek havonta kell fizetnie.                                        |
| Évi             | 2            | Azt jelzi, hogy a partnernek évente kell fizetnie.                                       |
| None               | 3            | Azt jelzi, hogy a partner nem számít fel díjat. Ez az érték próbaelemekhez használható.    |
| OneTime (Egyidő)            | 4            | Azt jelzi, hogy a partnernek egyszer kell fizetnie.                                       |

## <a name="attestationproperties"></a>AttestationProperties (Igazolásitulajdonságok)

Egy igazolástípust képvisel, és ha szükséges a vásárláshoz.

| Tulajdonság              | Típus                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType (igazolástípus)              | sztring                                      | Az igazolás típusát jelzi. A Windows 365 esetén a Windows365 az érték. Windows 365-ös igazolási szöveg: "Tisztában vagyok vele, hogy a Windows 365 Business with Windows Hybrid Benefitet használó minden személynek az Windows 10/11 Pro érvényes példányát is telepítenie kell az elsődleges munkahelyi eszközére." |
| enforceAttestation           | boolean                                      | Azt jelzi, hogy a vásárláshoz szükség van-e igazolásra.           |
