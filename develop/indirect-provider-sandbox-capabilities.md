---
title: Közvetett CSP-szolgáltatói képességek a védőfalon
description: A közvetett szolgáltatók tesztelési célból létrehozhatnak közvetett viszonteladókat a tesztkészletben.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: da35dadd4e13247e923259a1cf3a67852f4b9e00
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445901"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a>Közvetett CSP-szolgáltatói sandbox-képességek közvetett viszonteladói fiókok létrehozásához 

**Megfelelő szerepkörök:** Közvetett szolgáltató

A közvetett CSP-szolgáltatók létrehozhatnak egy CSP Indirect Reseller-fiókot a saját 2. rétegbeli sandbox-fiókjukkal a Partnerközpont portálon.


## <a name="prerequisites"></a>Előfeltételek 

Partnerközpont (2. réteg) közvetett szolgáltatói hitelesítő adatai. A sandbox forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal. 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Sandbox Indirect Provider (Közvetett Partnerközpont szolgáltató) – Közvetett Partnerközpont létrehozása 

 Ez egy csak a védőfalra jellemző funkció, amely lehetővé teszi, hogy közvetett szolgáltatói sandbox közvetett viszonteladói fiókot hozzanak létre a Partnerközpont portálon.

A közvetett szolgáltatók a következő forgatókönyveket biztosítják a Sandboxban közvetett viszonteladók számára a Partnerközpont felhasználói felületén: 

1. A közvetett CSP-szolgáltatók létrehozhatnak egy CSP Indirect Reseller-fiókot a saját 2. rétegbeli Partnerközpont keresztül.
2. A közvetett CSP-viszonteladók közvetett szolgáltatók szerint is megtekinthetik az ügyfeleket. 

1. A közvetett CSP-viszonteladók delegált rendszergazdai engedélyekkel kezelhetik az ügyfélfiókot.

1. Közvetett CSP-szolgáltatók meghívhat közvetett CSP-viszonteladókat.
 
1. A közvetett CSP-szolgáltatók törölhetik a CSP Indirect Reseller-fiókot a saját 2. rétegbeli Partnerközpont keresztül.

    a.  Amikor a Sandbox Indirect Provider törli a közvetett viszonteladóval való kapcsolatot, ellenőrizze, hogy a közvetett viszonteladónak van-e más kapcsolata más szolgáltatókkal. Ha igen, csak az adott közvetett szolgáltatóval való kapcsolat lesz eltávolítva.

    c. Ha ez az egyetlen kapcsolat a közvetett viszonteladóhoz, akkor a közvetett viszonteladó törlődik.

1. A közvetett CSP-szolgáltatók törölhetik a CSP Indirect Reseller.

    a. Ez egy csak a védőfalra jellemző funkció, amely lehetővé teszi a közvetett sandbox-szolgáltatók számára a közvetett viszonteladók törlését.
     
1. A sandbox indirect reseller törlésének előfeltételei:

    1. Függessze fel az előfizetéseket a Sandbox Indirect Reseller minden egyes ügyfele esetében.

    1. Törölje a Közvetett viszonteladó összes ügyfelet.

1. A közvetett viszonteladók által engedélyezett öt közvetett viszonteladóra vonatkozó korlát a közvetett sandbox szolgáltatónként. A közvetett sandbox viszonteladó törlése után a kvóta alaphelyzetbe áll.

### <a name="pre-requisites"></a>Előfeltételek

- A közvetett viszonteladók által engedélyezett öt közvetett viszonteladóra vonatkozó korlát a közvetett sandbox szolgáltatónként. 

- Ugyanaz az MPN-azonosító több közvetett viszonteladói sandbox-fiók létrehozására is használható, ha az MPN-azonosító országa és a Közvetett viszonteladói védőfal országa azonos. Ha van elérhető MPN-tesztazonosítója, használhatja, vagy le tudja szerezni az MPN-azonosítók listáját a Yammer [csatornán.]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ) Ha nem rendelkezik hozzáféréssel a Yammer, Yammer kérni fogja a hozzáférést.
 
- Közvetett sandbox-szolgáltatónként csak 75 ügyfél engedélyezett

## <a name="create-csp-indirect-reseller-sandbox-account"></a>CSP Indirect Reseller-fiók létrehozása

1. Jelentkezzen be Partnerközpont 2. rétegbeli sandbox-fiókjával. 

2. A bal oldali menüben lépjen a Közvetett viszonteladók menüpontra. 

3. Válassza a **Viszonteladói sandbox hozzáadása gombot.** 

4. Töltse ki a fiókregisztrációs űrlapot. Ez magától értetődő, de ne feledje, hogy egy közvetett viszonteladóhoz hoz létre sandbox-fiókot. A fiók átvizsgálása nem megy keresztül, és a fiók regisztrálásának befejezése után azonnal aktiválódik.  

5. A fiók létrehozása után a portálon le fogja kapni a közvetett viszonteladói sandbox-fiók globális rendszergazdai hitelesítő adatait. Ne felejtse el azonnal menteni, ellenkező esetben nem fog tudni közvetett viszonteladói védőfalként bejelentkezni. 

6. Jelentkezzen ki, majd jelentkezzen be újra Partnerközpont közvetett viszonteladói sandbox új hitelesítő adataival. Megismerheti a közvetett viszonteladóként is használhatja képességeit. Néhány dolog:  

    - Profilok kezelése  

    - Felhasználók és szerepkörök kezelése 

    - Közvetett szolgáltatók kezelése 

    - CSP-sandbox-ügyfelek kezelése 

    - Kapcsolatok kezelése
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Közvetett sandbox-szolgáltató – Közvetett Partnerközpont törlése a Partnerközpont felületén

 Ez egy csak a sandbox funkció, amely lehetővé teszi a közvetett sandbox-szolgáltatók számára egy meglévő közvetett viszonteladói fiók törlését a Partnerközpont portálon. 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a>A közvetett viszonteladó törlésének előfeltételei:

Egy meglévő CSP Indirect Reseller fiók, amely a saját CSP Indirect Provider 2. rétegbeli sandbox-fiókjához van társítva.  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a>A CSP Indirect Reseller-fiók törlése

1. Jelentkezzen be Partnerközpont a 2. rétegbeli sandbox-fiókjával. 

2. A bal oldali menüben lépjen a Közvetett viszonteladók menüpontra. 

3. Válassza **a Viszonteladói védőfal** törlése hivatkozást a törölni kívánt közvetett viszonteladói sandbox-fiók mellett. A közvetett viszonteladói sandbox-fiók véglegesen törölve lesz, és nem állítható helyre. 

## <a name="api-references"></a>API-referenciák

- Közvetett viszonteladó létrehozása 
- Közvetett viszonteladó törlése 

 

 