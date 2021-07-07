---
title: Alkalmazásadatok regisztrálása Partnerközpont Microsoft National Cloudhoz
description: Megtudhatja, hogyan és miért kell a Microsoft National Cloudhoz Partnerközpont alkalmazásfejlesztőknek regisztrálniuk az alkalmazásuk részleteit az Azure AD-Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93d46a17bc26e9586e5e773bdf934653a571367f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973451"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a>Alkalmazásadatok regisztrálása Partnerközpont Microsoft National Cloudhoz az Azure Portal

**A következőkre** vonatkozik: Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A fejlesztőknek regisztrálniuk kell az alkalmazásuk részleteit az Azure AD-ban a Azure Portal. Ez biztosítja, hogy csak a megadott alkalmazások tudjanak csatlakozni a partner- és ügyféladatokhoz.

A Partnerközpont esetében Microsoft Cloud for US Government PowerShellen keresztül kell kezelnie az alkalmazásokat. További információért tekintse meg a Azure PowerShell [dokumentációját.](/powershell/module/Azuread/#applications)

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

A Microsoft Cloud Germany vagy a microsoftos felhőszolgáltatásokhoz Partnerközpont alkalmazások létrehozásakor vegye figyelembe a Partnerközpont további Microsoft Cloud for US Government.

## <a name="web-apps"></a>Webalkalmazások

Webalkalmazások esetén az alábbi eljárásokkal regisztrálhatja az alkalmazásazonosítót.

### <a name="create-or-update-web-app"></a>Webalkalmazás létrehozása vagy frissítése

1. Nyissa meg a [Azure Portal – Alkalmazásregisztrációk](https://go.microsoft.com/fwlink/?linkid=2083908) oldalt az alkalmazás regisztráláshoz. Jelentkezzen be egy munkahelyi vagy iskolai fiókkal vagy a személyes Microsoft-fiókjával az Azure Portalra.

2. Válassza **az Új regisztráció lehetőséget.** További információ: [Rövid útmutató: Alkalmazás regisztrálása a Microsoft Identitásplatform.](/azure/active-directory/develop/quickstart-register-app)

### <a name="configure-api-access-permissions-for-web-app"></a>API-hozzáférési engedélyek konfigurálása webalkalmazáshoz

1. Válassza ki az alkalmazást. A **Gépház** indítósávját.

2. Az **API Access (API-hozzáférés)** szakaszban válassza a **Required permissions (Szükséges engedélyek) lehetőséget.**

3. További Windows Azure Active Directory-engedélyekhez:

    1. Válassza **Windows Azure Active Directory engedélyek lehetőséget.**

    2. Az **Alkalmazások engedélyei mezőben** válassza a Címtáradatok olvasása lehetőséget.

    3. Mentse az engedélyeket.

4. Jegyezze fel a webalkalmazás **Tulajdonságok** szakaszában található alkalmazásazonosítót.

### <a name="add-a-secret-key-to-your-app"></a>Titkos kulcs hozzáadása az alkalmazáshoz

1. Ugrás a **webalkalmazás** Kulcsok szakaszra.

2. Adja meg a kulcs leírását, és szükség szerint válassza az 1 vagy 2 év lehetőséget.

3. Mentse és másolja ki a titkos kulcs értékét. **Az oldal elhagyás után ez az érték nem jelenik meg újra.**

A webalkalmazás konfigurációjában a következő adatoknak kell lennie:

- Alkalmazásazonosító
- Alkalmazás titkos kódja

### <a name="register-the-web-app-in-partner-center"></a>A webalkalmazás regisztrálása a Partnerközpont

1. Jelentkezzen be itt: [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).

2. Válassza **az Irányítópult** lehetőséget, majd a Fiók **Gépház** az **Alkalmazáskezelés lehetőséget.**

3. A **Webalkalmazás szakaszban válassza** a **Meglévő alkalmazás regisztrálása lehetőséget.**

4. Válassza ki a Azure Portal.

5. Válassza **az alkalmazás regisztrálása lehetőséget.**

## <a name="native-apps"></a>Natív alkalmazások

A natív alkalmazásokat nem kell regisztrálni a Partnerközpont. Ezeket az alkalmazásokat azonban úgy kell konfigurálni, hogy hozzáférést Partnerközpont API-khoz.

>[!NOTE]
>Mielőtt natív alkalmazást hoz létre a Azure Portal, jelentkezzen be a Partnerközpont a partnerbérlő rendszergazdai felhasználói hitelesítő adataival. Ezzel létrehozza a bérlő beállításait az alkalmazásengedélyek engedélyezéséhez.

### <a name="create-native-app"></a>Natív alkalmazás létrehozása

1. Nyissa meg a [Azure Portal – Alkalmazásregisztrációk](https://go.microsoft.com/fwlink/?linkid=2083908) oldalt az alkalmazás regisztráláshoz. Jelentkezzen be egy munkahelyi vagy iskolai fiókkal vagy a személyes Microsoft-fiókjával az Azure Portalra.

2. Válassza **az Új regisztráció lehetőséget.** További információ: [Rövid útmutató: Alkalmazás regisztrálása a Microsoft Identitásplatform.](/azure/active-directory/develop/quickstart-register-app)

### <a name="configure-api-access-permissions-for-native-app"></a>API-hozzáférési engedélyek konfigurálása natív alkalmazáshoz

1. Válassza ki az alkalmazást. Ugrás a **Gépház.**

2. Az API Access (API-hozzáférés) csoportban **válassza a Required permissions (Szükséges engedélyek) lehetőséget.**

3. Válassza **Windows Azure Active Directory engedélyek lehetőséget.** A **Delegált engedélyek beállításnál** válassza ki az alábbi engedélyeket:

    - **Bejelentkezés és felhasználói profil olvasása**
    - **Címtáradatok olvasása**
    - **A címtár elérése a bejelentkezett felhasználó nevében**
    - **Az összes csoport olvasása**

4. Mentse az engedélyeket.

5. A **Szükséges engedélyek** között válassza a Hozzáadás **lehetőséget.**

6. Válassza az **API kiválasztása** elemet.

    1. A keresőmezőbe írja be a **Microsoft Partnerközpont,** és válassza ki a találatok listájából.

    2. Válassza a **Kiválasztás** lehetőséget

7. Válassza **az Engedélyek kiválasztása lehetőséget.**

    1. Válassza **az Access Partnerközpont PPE lehetőséget.**
    
    2. Válassza a **Kiválasztás** lehetőséget

8. Válassza a **Kész** lehetőséget.

>[!IMPORTANT]
> Jegyezze fel az alkalmazásazonosítót az alkalmazás Tulajdonságai között.

Nem kell natív alkalmazásokat regisztrálnia a Partnerközpont, de a natív alkalmazást rendszergazdai jóváhagyással kell kiegészítenie. Jegyezze fel a natív alkalmazás alkalmazásazonosítóját.
