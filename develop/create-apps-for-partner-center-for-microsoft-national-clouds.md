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
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a><span data-ttu-id="7f0c9-103">Az alkalmazás adatainak regisztrálása a Microsoft National Cloud Partner Centerhez a Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7f0c9-103">Register app details for Partner Center for Microsoft National Cloud through the Azure portal</span></span>

<span data-ttu-id="7f0c9-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="7f0c9-104">**Applies to:**</span></span>

- <span data-ttu-id="7f0c9-105">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="7f0c9-105">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7f0c9-106">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="7f0c9-106">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7f0c9-107">A fejlesztőknek regisztrálniuk kell az alkalmazással kapcsolatos adatokat az Azure AD-vel a Azure Portalon keresztül.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-107">Developers must register details about their app with Azure AD through the Azure portal.</span></span> <span data-ttu-id="7f0c9-108">Ezzel biztosítható, hogy csak a megadott alkalmazások csatlakozhassanak a partnerekhez és az ügyfelekhez.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-108">This helps ensure that only specified apps are able to connect to partner and customer data.</span></span>

<span data-ttu-id="7f0c9-109">Az USA kormányzati szervei számára Microsoft Cloud partneri központ esetében jelenleg a PowerShellen keresztül kell felügyelni az alkalmazásokat.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-109">For Partner Center for Microsoft Cloud for US Government, you currently must manage apps through PowerShell.</span></span> <span data-ttu-id="7f0c9-110">További információ: [Azure PowerShell dokumentáció](/powershell/module/Azuread/#applications).</span><span class="sxs-lookup"><span data-stu-id="7f0c9-110">For more information, see the [Azure PowerShell reference documentation](/powershell/module/Azuread/#applications).</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="7f0c9-111">Vegye figyelembe a következő további követelményeket, amikor létrehoz egy alkalmazást a Microsoft Cloud Germany vagy a partner Center számára a Microsoft Cloud az Egyesült Államok kormánya számára.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-111">Be aware of the following additional requirements when you create an app for Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government.</span></span>

## <a name="web-apps"></a><span data-ttu-id="7f0c9-112">Webalkalmazások</span><span class="sxs-lookup"><span data-stu-id="7f0c9-112">Web apps</span></span>

<span data-ttu-id="7f0c9-113">Webalkalmazások esetén a következő eljárásokkal regisztrálhat az alkalmazás AZONOSÍTÓját.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-113">For web apps, use the following procedures to register your application ID.</span></span>

### <a name="create-or-update-web-app"></a><span data-ttu-id="7f0c9-114">Webalkalmazás létrehozása vagy frissítése</span><span class="sxs-lookup"><span data-stu-id="7f0c9-114">Create or update web app</span></span>

1. <span data-ttu-id="7f0c9-115">Az alkalmazás regisztrálásához navigáljon a [Azure Portal-Alkalmazásregisztrációk](https://go.microsoft.com/fwlink/?linkid=2083908) lapra.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-115">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="7f0c9-116">Jelentkezzen be egy munkahelyi vagy iskolai fiókkal vagy a személyes Microsoft-fiókjával az Azure Portalra.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-116">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="7f0c9-117">Válassza az **új regisztráció** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-117">Select **New registration**.</span></span> <span data-ttu-id="7f0c9-118">További információ: gyors útmutató [: alkalmazás regisztrálása a Microsoft Identity platformon](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="7f0c9-118">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-web-app"></a><span data-ttu-id="7f0c9-119">API-hozzáférési engedélyek konfigurálása a webalkalmazáshoz</span><span class="sxs-lookup"><span data-stu-id="7f0c9-119">Configure API access permissions for web app</span></span>

1. <span data-ttu-id="7f0c9-120">Válassza ki az alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-120">Choose your app.</span></span> <span data-ttu-id="7f0c9-121">Nyissa meg a webalkalmazás **beállításait** .</span><span class="sxs-lookup"><span data-stu-id="7f0c9-121">Go to **Settings** of the Web app.</span></span>

2. <span data-ttu-id="7f0c9-122">Az **API-hozzáférés** szakaszban válassza a **szükséges engedélyek** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-122">In **API Access** section, choose **Required permissions**</span></span>

3. <span data-ttu-id="7f0c9-123">Windows Azure Active Directory-engedélyek esetén:</span><span class="sxs-lookup"><span data-stu-id="7f0c9-123">For Windows Azure Active directory permissions:</span></span>

    1. <span data-ttu-id="7f0c9-124">Válassza a **Windows Azure Active Directory engedélyek** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-124">Choose **Windows Azure Active Directory permissions**.</span></span>

    2. <span data-ttu-id="7f0c9-125">Az **alkalmazások engedélyei** területen válassza a címtárbeli információk olvasása elemet.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-125">In **Applications permissions**, select Read directory data.</span></span>

    3. <span data-ttu-id="7f0c9-126">Mentse az engedélyeket.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-126">Save the permissions.</span></span>

4. <span data-ttu-id="7f0c9-127">Jegyezze fel az alkalmazás AZONOSÍTÓját a webalkalmazás **Tulajdonságok** szakaszában.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-127">Note the application ID in the **Properties** section of your web app.</span></span>

### <a name="add-a-secret-key-to-your-app"></a><span data-ttu-id="7f0c9-128">Titkos kulcs hozzáadása az alkalmazáshoz</span><span class="sxs-lookup"><span data-stu-id="7f0c9-128">Add a secret key to your app</span></span>

1. <span data-ttu-id="7f0c9-129">Nyissa meg a webalkalmazás **kulcsok** szakaszát.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-129">Go to the **Keys** section of your web app.</span></span>

2. <span data-ttu-id="7f0c9-130">Adja meg a kulcs leírását, és válassza ki az időtartamot 1 vagy 2 év, ahogy szükséges.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-130">Enter key description and select duration as 1 or 2 years, as you need.</span></span>

3. <span data-ttu-id="7f0c9-131">Mentse és másolja a titkos kulcs értékét.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-131">Save and copy the secret key value.</span></span> <span data-ttu-id="7f0c9-132">**Ez az érték nem jelenik meg újra, ha elhagyja ezt a lapot.**</span><span class="sxs-lookup"><span data-stu-id="7f0c9-132">**This value will not be shown again once you leave this page.**</span></span>

<span data-ttu-id="7f0c9-133">A webalkalmazás-konfigurációból a következő adatokat kell megkapnia:</span><span class="sxs-lookup"><span data-stu-id="7f0c9-133">You should have the following details from the web app configuration:</span></span>

- <span data-ttu-id="7f0c9-134">Alkalmazásazonosító</span><span class="sxs-lookup"><span data-stu-id="7f0c9-134">Application ID</span></span>
- <span data-ttu-id="7f0c9-135">Alkalmazás titkos kódja</span><span class="sxs-lookup"><span data-stu-id="7f0c9-135">Application secret</span></span>

### <a name="register-the-web-app-in-partner-center"></a><span data-ttu-id="7f0c9-136">A webalkalmazás regisztrálása a partner Centerben</span><span class="sxs-lookup"><span data-stu-id="7f0c9-136">Register the Web app in Partner Center</span></span>

1. <span data-ttu-id="7f0c9-137">Jelentkezzen be a alkalmazásba [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) .</span><span class="sxs-lookup"><span data-stu-id="7f0c9-137">Log in to [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span></span>

2. <span data-ttu-id="7f0c9-138">Válassza az **irányítópult** lehetőséget, majd a **Fiókbeállítások**, majd az **alkalmazás-kezelés** elemet.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-138">Choose **Dashboard**, then choose **Account Settings**, then choose **App Management**.</span></span>

3. <span data-ttu-id="7f0c9-139">A **Web App (webalkalmazás** ) szakaszban válassza a **meglévő alkalmazás regisztrálása** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-139">In the **Web App** section, choose **Register existing app**.</span></span>

4. <span data-ttu-id="7f0c9-140">Válassza ki a Azure Portalban létrehozott webalkalmazást.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-140">Select the web app you created in Azure portal.</span></span>

5. <span data-ttu-id="7f0c9-141">Válassza **az alkalmazás regisztrálása** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-141">Choose **register your app**.</span></span>

## <a name="native-apps"></a><span data-ttu-id="7f0c9-142">Natív alkalmazások</span><span class="sxs-lookup"><span data-stu-id="7f0c9-142">Native apps</span></span>

<span data-ttu-id="7f0c9-143">A natív alkalmazásokat nem kell regisztrálni a partner Centerben.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-143">Native apps do not need to be registered to Partner Center.</span></span> <span data-ttu-id="7f0c9-144">Ezeket az alkalmazásokat azonban úgy kell konfigurálni, hogy hozzáférést biztosítson a partner Center API-khoz.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-144">But these apps need to be configured to provide access to Partner Center APIs.</span></span>

>[!NOTE]
><span data-ttu-id="7f0c9-145">Mielőtt natív alkalmazást hozna létre a Azure Portalban, jelentkezzen be a partner Centerbe a partner bérlője rendszergazdai felhasználói hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-145">Before creating a native app in the Azure portal, log in into Partner Center using the admin user credentials from the partner tenant.</span></span> <span data-ttu-id="7f0c9-146">Ezzel létrehozza a beállításokat a bérlőn az alkalmazás engedélyeinek engedélyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-146">This creates the settings on the tenant to enable app permissions.</span></span>

### <a name="create-native-app"></a><span data-ttu-id="7f0c9-147">Natív alkalmazás létrehozása</span><span class="sxs-lookup"><span data-stu-id="7f0c9-147">Create native app</span></span>

1. <span data-ttu-id="7f0c9-148">Az alkalmazás regisztrálásához navigáljon a [Azure Portal-Alkalmazásregisztrációk](https://go.microsoft.com/fwlink/?linkid=2083908) lapra.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-148">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="7f0c9-149">Jelentkezzen be egy munkahelyi vagy iskolai fiókkal vagy a személyes Microsoft-fiókjával az Azure Portalra.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-149">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="7f0c9-150">Válassza az **új regisztráció** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-150">Select **New registration**.</span></span> <span data-ttu-id="7f0c9-151">További információ: gyors útmutató [: alkalmazás regisztrálása a Microsoft Identity platformon](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="7f0c9-151">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-native-app"></a><span data-ttu-id="7f0c9-152">API-hozzáférési engedélyek konfigurálása natív alkalmazáshoz</span><span class="sxs-lookup"><span data-stu-id="7f0c9-152">Configure API access permissions for native app</span></span>

1. <span data-ttu-id="7f0c9-153">Válassza ki az alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-153">Choose your app.</span></span> <span data-ttu-id="7f0c9-154">Válassza a **Beállítások lehetőséget**.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-154">Go to **Settings**.</span></span>

2. <span data-ttu-id="7f0c9-155">Az API-hozzáférés területen válassza a **szükséges engedélyek** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-155">In API Access, choose **Required permissions**.</span></span>

3. <span data-ttu-id="7f0c9-156">Válassza a **Windows Azure Active Directory engedélyek** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-156">Choose **Windows Azure Active Directory permissions**.</span></span> <span data-ttu-id="7f0c9-157">A **delegált engedélyek** területen válassza ki az alábbi engedélyeket:</span><span class="sxs-lookup"><span data-stu-id="7f0c9-157">In **Delegated permissions**, select these permissions:</span></span>

    - <span data-ttu-id="7f0c9-158">**Bejelentkezés és felhasználói profil olvasása**</span><span class="sxs-lookup"><span data-stu-id="7f0c9-158">**Sign in and read user profile**</span></span>
    - <span data-ttu-id="7f0c9-159">**Címtáradatok olvasása**</span><span class="sxs-lookup"><span data-stu-id="7f0c9-159">**Read directory data**</span></span>
    - <span data-ttu-id="7f0c9-160">**A címtár elérése a bejelentkezett felhasználó nevében**</span><span class="sxs-lookup"><span data-stu-id="7f0c9-160">**Access the directory as the signed-in user**</span></span>
    - <span data-ttu-id="7f0c9-161">**Az összes csoport olvasása**</span><span class="sxs-lookup"><span data-stu-id="7f0c9-161">**Read all groups**</span></span>

4. <span data-ttu-id="7f0c9-162">Mentse az engedélyeket.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-162">Save the permissions.</span></span>

5. <span data-ttu-id="7f0c9-163">Válassza a **Hozzáadás** a **szükséges engedélyekkel** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-163">Choose **Add** in **Required permissions**.</span></span>

6. <span data-ttu-id="7f0c9-164">Válassza az **API kiválasztása** elemet.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-164">Choose **Select an API**.</span></span>

    1. <span data-ttu-id="7f0c9-165">A keresőmezőbe írja be a **Microsoft partner centert** , és válassza ki az eredmények listából.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-165">In the search box, enter **Microsoft Partner Center** and select it from the results list.</span></span>

    2. <span data-ttu-id="7f0c9-166">Válassza a **Kiválasztás** lehetőséget</span><span class="sxs-lookup"><span data-stu-id="7f0c9-166">Choose **Select**.</span></span>

7. <span data-ttu-id="7f0c9-167">Válassza az **engedélyek kiválasztása** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-167">Choose **Select permissions**.</span></span>

    1. <span data-ttu-id="7f0c9-168">Válassza a **hozzáférési partner Center PPE** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-168">Select **Access Partner Center PPE**.</span></span>
    
    2. <span data-ttu-id="7f0c9-169">Válassza a **Kiválasztás** lehetőséget</span><span class="sxs-lookup"><span data-stu-id="7f0c9-169">Choose **Select**.</span></span>

8. <span data-ttu-id="7f0c9-170">Válassza a **Kész** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-170">Choose **Done**.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="7f0c9-171">Jegyezze fel az alkalmazás AZONOSÍTÓját az alkalmazás tulajdonságainál.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-171">Note the application ID in the Properties of your app.</span></span>

<span data-ttu-id="7f0c9-172">Nem kell natív alkalmazásokat regisztrálnia a partner Centerben, azonban a natív alkalmazásnak rendszergazdai hozzájárulással kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-172">You do not need to register native apps in Partner Center, however the native app must be admin consented .</span></span> <span data-ttu-id="7f0c9-173">Jegyezze fel a natív alkalmazás alkalmazás-AZONOSÍTÓját.</span><span class="sxs-lookup"><span data-stu-id="7f0c9-173">Note the application ID of your native app.</span></span>
