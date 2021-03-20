---
title: Viszonteladói kapcsolatot támogató partneri tesztkörnyezet-képességek
description: A partneri homokozó képes támogatni a partner és az ügyfél közötti kapcsolatokat
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: af46811b3615e1f904a9619de85b0aca7622490b
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711865"
---
# <a name="partner-sandbox-capabilities-that-support-reseller-relationship"></a>Viszonteladói kapcsolatot támogató partneri tesztkörnyezet-képességek

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ez a cikk ismerteti, hogy a homokozóban milyen támogatott a viszonteladói kapcsolatok a partner és az ügyfél között. 

## <a name="prerequisites"></a>Előfeltételek

- A partneri központ fiókjának hitelesítő adatai. A sandbox forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.
- Ügyfél-azonosító (ügyfél-bérlői azonosító). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard/home). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft ID megegyezik az ügyfél-AZONOSÍTÓval (ügyfél-bérlő-azonosító).
- Az összes Azure Reserved Virtual Machine Instances-és szoftver-beszerzési rendelést meg kell szüntetni, mielőtt törölné egy ügyfelet a tip Integration sandbox-ból.

## <a name="scenarios-supporting-reseller-relationship"></a>Viszonteladói kapcsolatot támogató forgatókönyvek

1.  A sandbox Direct Bill-partnerek és a közvetett szolgáltatók kapcsolatokat hozhatnak létre a homokozó-ügyféllel. 
2.  A sandbox Direct Bill-partnerek és a közvetett szolgáltatók nem hívhatják meg a sandbox-ügyfeleket.



### <a name="in-the-sandbox"></a>A homokozóban

**Közvetlen számlázási partnerek**:

• Meglévő ügyfeleket adhat hozzá

• Nem kérhet kapcsolatokat új ügyfelekkel

**Közvetett szolgáltatók**:

• Meglévő ügyfeleket adhat hozzá

• Nem kérhet kapcsolatokat új ügyfelekkel

• Nem lehet közvetett viszonteladóval létesített kapcsolat

**Közvetett viszonteladó**: (hamarosan elérhető)

• Meglévő ügyfelekkel is rendelkezhet kapcsolatokkal

• Nem kérhet új kapcsolatokat, és nem vehet fel új ügyfeleket

### <a name="in-partner-center"></a>A partner Centerben

**Közvetlen számlázási partnerek**:

• Új ügyfeleket adhat hozzá

• Az új ügyfelekkel is kérhet kapcsolatokat

**Közvetett szolgáltatók**:

• Új ügyfeleket adhat hozzá

• Az új ügyfelekkel is kérhet kapcsolatokat

• A kapcsolat közvetett viszonteladókkal is rendelkezhet

**Közvetett viszonteladók**:

• Nem lehet új ügyfeleket felvenni

• Az új ügyfelekkel is kérhet kapcsolatokat

3. A sandbox Direct Bill partner és a közvetett szolgáltatók el tudják távolítani a viszonteladói kapcsolatot a partner Center felhasználói felületéről és az API-ból.

4. A homokozóban a viszonteladói kapcsolat eltávolítása meghívja a DELETE Customer AP-t. Ezzel eltávolítja a kapcsolatot, valamint törli az ügyfél bérlőjét is. {baseURL}/v1/Customers/{customer-Tenant-id}

A részletekért kövesse az ügyfél [viszonteladói kapcsolatának eltávolítása](remove-a-reseller-relationship-with-a-customer.md) című témakört. Van azonban néhány különbség a termék és a homokozó lehetőségei között.

### <a name="request-syntax"></a>KÉRELEM SZINTAXISA

|**Metódus**|**Törlés**|
|-------------|------------|
|Törlés|{baseURL}/v1/Customers/{customer-Tenant-id} |

A kérelem törzse nincs

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](./error-codes.md)-hibakódok.

## <a name="next-steps"></a>Következő lépések

- [Az Azure Marketplace-termékekhez készült homokozó-előfizetések aktiválása](activate-sandbox-subscription-azure-marketplace-products.md)

- [Megrendelés megszakítása a Homokozóból](cancel-an-order-from-the-integration-sandbox.md)

- [Tesztelés és hibakeresés](test-and-debug.md)