---
title: Az alkalmazás adatainak regisztrálása a Microsoft National Cloud Partner Centerhez
description: Megtudhatja, hogyan és miért érdemes regisztrálni az alkalmazással kapcsolatos adatokat az Azure AD-vel az Azure Portal a Microsoft National Cloud-hoz.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 887cb71c752ac5d9c61398536711545c19cc7600
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768634"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a>Az alkalmazás adatainak regisztrálása a Microsoft National Cloud Partner Centerhez a Azure Portal

**A következőkre vonatkozik:**

- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A fejlesztőknek regisztrálniuk kell az alkalmazással kapcsolatos adatokat az Azure AD-vel a Azure Portalon keresztül. Ezzel biztosítható, hogy csak a megadott alkalmazások csatlakozhassanak a partnerekhez és az ügyfelekhez.

Az USA kormányzati szervei számára Microsoft Cloud partneri központ esetében jelenleg a PowerShellen keresztül kell felügyelni az alkalmazásokat. További információ: [Azure PowerShell dokumentáció](/powershell/module/Azuread/#applications).

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Vegye figyelembe a következő további követelményeket, amikor létrehoz egy alkalmazást a Microsoft Cloud Germany vagy a partner Center számára a Microsoft Cloud az Egyesült Államok kormánya számára.

## <a name="web-apps"></a>Webalkalmazások

Webalkalmazások esetén a következő eljárásokkal regisztrálhat az alkalmazás AZONOSÍTÓját.

### <a name="create-or-update-web-app"></a>Webalkalmazás létrehozása vagy frissítése

1. Az alkalmazás regisztrálásához navigáljon a [Azure Portal-Alkalmazásregisztrációk](https://go.microsoft.com/fwlink/?linkid=2083908) lapra. Jelentkezzen be egy munkahelyi vagy iskolai fiókkal vagy a személyes Microsoft-fiókjával az Azure Portalra.

2. Válassza az **új regisztráció** lehetőséget. További információ: gyors útmutató [: alkalmazás regisztrálása a Microsoft Identity platformon](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-web-app"></a>API-hozzáférési engedélyek konfigurálása a webalkalmazáshoz

1. Válassza ki az alkalmazást. Nyissa meg a webalkalmazás **beállításait** .

2. Az **API-hozzáférés** szakaszban válassza a **szükséges engedélyek** lehetőséget.

3. Windows Azure Active Directory-engedélyek esetén:

    1. Válassza a **Windows Azure Active Directory engedélyek** lehetőséget.

    2. Az **alkalmazások engedélyei** területen válassza a címtárbeli információk olvasása elemet.

    3. Mentse az engedélyeket.

4. Jegyezze fel az alkalmazás AZONOSÍTÓját a webalkalmazás **Tulajdonságok** szakaszában.

### <a name="add-a-secret-key-to-your-app"></a>Titkos kulcs hozzáadása az alkalmazáshoz

1. Nyissa meg a webalkalmazás **kulcsok** szakaszát.

2. Adja meg a kulcs leírását, és válassza ki az időtartamot 1 vagy 2 év, ahogy szükséges.

3. Mentse és másolja a titkos kulcs értékét. **Ez az érték nem jelenik meg újra, ha elhagyja ezt a lapot.**

A webalkalmazás-konfigurációból a következő adatokat kell megkapnia:

- Alkalmazásazonosító
- Alkalmazás titkos kódja

### <a name="register-the-web-app-in-partner-center"></a>A webalkalmazás regisztrálása a partner Centerben

1. Jelentkezzen be a alkalmazásba [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) .

2. Válassza az **irányítópult** lehetőséget, majd a **Fiókbeállítások**, majd az **alkalmazás-kezelés** elemet.

3. A **Web App (webalkalmazás** ) szakaszban válassza a **meglévő alkalmazás regisztrálása** lehetőséget.

4. Válassza ki a Azure Portalban létrehozott webalkalmazást.

5. Válassza **az alkalmazás regisztrálása** lehetőséget.

## <a name="native-apps"></a>Natív alkalmazások

A natív alkalmazásokat nem kell regisztrálni a partner Centerben. Ezeket az alkalmazásokat azonban úgy kell konfigurálni, hogy hozzáférést biztosítson a partner Center API-khoz.

>[!NOTE]
>Mielőtt natív alkalmazást hozna létre a Azure Portalban, jelentkezzen be a partner Centerbe a partner bérlője rendszergazdai felhasználói hitelesítő adataival. Ezzel létrehozza a beállításokat a bérlőn az alkalmazás engedélyeinek engedélyezéséhez.

### <a name="create-native-app"></a>Natív alkalmazás létrehozása

1. Az alkalmazás regisztrálásához navigáljon a [Azure Portal-Alkalmazásregisztrációk](https://go.microsoft.com/fwlink/?linkid=2083908) lapra. Jelentkezzen be egy munkahelyi vagy iskolai fiókkal vagy a személyes Microsoft-fiókjával az Azure Portalra.

2. Válassza az **új regisztráció** lehetőséget. További információ: gyors útmutató [: alkalmazás regisztrálása a Microsoft Identity platformon](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-native-app"></a>API-hozzáférési engedélyek konfigurálása natív alkalmazáshoz

1. Válassza ki az alkalmazást. Válassza a **Beállítások lehetőséget**.

2. Az API-hozzáférés területen válassza a **szükséges engedélyek** lehetőséget.

3. Válassza a **Windows Azure Active Directory engedélyek** lehetőséget. A **delegált engedélyek** területen válassza ki az alábbi engedélyeket:

    - **Bejelentkezés és felhasználói profil olvasása**
    - **Címtáradatok olvasása**
    - **A címtár elérése a bejelentkezett felhasználó nevében**
    - **Az összes csoport olvasása**

4. Mentse az engedélyeket.

5. Válassza a **Hozzáadás** a **szükséges engedélyekkel** lehetőséget.

6. Válassza az **API kiválasztása** elemet.

    1. A keresőmezőbe írja be a **Microsoft partner centert** , és válassza ki az eredmények listából.

    2. Válassza a **Kiválasztás** lehetőséget

7. Válassza az **engedélyek kiválasztása** lehetőséget.

    1. Válassza a **hozzáférési partner Center PPE** lehetőséget.
    
    2. Válassza a **Kiválasztás** lehetőséget

8. Válassza a **Kész** lehetőséget.

>[!IMPORTANT]
> Jegyezze fel az alkalmazás AZONOSÍTÓját az alkalmazás tulajdonságainál.

Nem kell natív alkalmazásokat regisztrálnia a partner Centerben, azonban a natív alkalmazásnak rendszergazdai hozzájárulással kell rendelkeznie. Jegyezze fel a natív alkalmazás alkalmazás-AZONOSÍTÓját.
