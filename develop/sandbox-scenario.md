---
title: A viszonteladói kapcsolatokhoz szükséges sandbox-képességek
description: A partneri sandbox képes támogatni a partner és az ügyfél közötti kapcsolatokat
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14133627a607c6e4151a90c37565e5f62823345e007eb55d87100de25d1f161a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996852"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a>A viszonteladói kapcsolatokhoz szükséges sandbox-képességek

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Ez a cikk ismerteti, hogy mit támogat a sandbox a partner és az ügyfél közötti viszonteladói kapcsolatokhoz. 

## <a name="prerequisites"></a>Előfeltételek

- Partnerközpont fiók hitelesítő adatait. A sandbox forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.
- Egy ügyfél-azonosító (customer-tenant-id). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard/home) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval (customer-tenant-id).
- Minden Azure Reserved Virtual Machine Instances és szoftvervásárlási megrendelést meg kell szakítani, mielőtt törölné az ügyfelet a Tip integration sandboxból.

## <a name="scenarios-supporting-reseller-relationship"></a>Viszonteladói kapcsolatot támogató forgatókönyvek

1.  A Sandbox Direct Bill-partnerek és a közvetett szolgáltatók kapcsolatokat hozhatnak létre a sandbox ügyféllel. 
2.  A Sandbox Direct Bill-partnerek és a közvetett szolgáltatók nem hívnak meg sandbox-ügyfeleket.

3. A Sandbox Direct Bill Partner és a Indirect Providers képesek eltávolítani a viszonteladói kapcsolatot Partnerközpont felhasználói felületről és API-ból.

4. A Viszonteladói kapcsolat eltávolítása védőfal hívja meg az Ügyfél törlése API-t. Ezzel eltávolítja a kapcsolatot, és törli az ügyfélbérlőt. {baseURL}/v1/Customers/{customer-Tenant-id}


    ### <a name="in-the-sandbox"></a>A sandboxban

    **Közvetlen számlázási partnerek:**

    - Hozzáadhat meglévő ügyfeleket

    - Nem lehet kapcsolatokat kérni új ügyfelekkel

    **Közvetett szolgáltatók:**

    - Hozzáadhat meglévő ügyfeleket

    - Nem lehet kapcsolatokat kérni új ügyfelekkel

    - Nem lehet kapcsolat közvetett viszonteladóval

    **Közvetett viszonteladó:** 

    -   Kapcsolat lehet meglévő ügyfelekkel

    -   Nem kérhet új kapcsolatokat, és nem adhat hozzá új ügyfeleket

    ### <a name="in-partner-center"></a>A Partnerközpont

    **Közvetlen számlázási partnerek:**

    -   Hozzáadhat új ügyfeleket

    -   Kapcsolatok igénylése új ügyfelekkel

    **Közvetett szolgáltatók:**

    -   Hozzáadhat új ügyfeleket

    -   Kapcsolatok igénylése új ügyfelekkel

    -   Kapcsolat lehet közvetett viszonteladóval

    **Közvetett viszonteladók:**

    -   Nem lehet új ügyfeleket felvenni

    -   Kapcsolatok igénylése új ügyfelekkel


A [részletekért kövesse](remove-a-reseller-relationship-with-a-customer.md) az ügyfél viszonteladói kapcsolatának eltávolítását. Van azonban néhány különbség a Termék és a Sandbox képességei között.

### <a name="request-syntax"></a>KÉRELEMSZINTAXIS

|**Metódus**|**Törlés**|
|-------------|------------|
|Törlés|{baseURL}/v1/Customers/{customer-Tenant-id} |

Kérelem törzse Nincs

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](./error-codes.md)

## <a name="next-steps"></a>Következő lépések

- [Sandbox-előfizetések aktiválása Azure Marketplace termékekhez](activate-sandbox-subscription-azure-marketplace-products.md)

- [Rendelés visszavonása a sandboxból](cancel-an-order-from-the-integration-sandbox.md)

- [Tesztelés és hibakeresés](test-and-debug.md)