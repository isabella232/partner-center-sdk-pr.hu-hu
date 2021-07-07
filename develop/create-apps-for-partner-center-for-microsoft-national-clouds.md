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
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a><span data-ttu-id="f5425-103">Alkalmazásadatok regisztrálása Partnerközpont Microsoft National Cloudhoz az Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f5425-103">Register app details for Partner Center for Microsoft National Cloud through the Azure portal</span></span>

<span data-ttu-id="f5425-104">**A következőkre** vonatkozik: Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f5425-104">**Applies to**: Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f5425-105">A fejlesztőknek regisztrálniuk kell az alkalmazásuk részleteit az Azure AD-ban a Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f5425-105">Developers must register details about their app with Azure AD through the Azure portal.</span></span> <span data-ttu-id="f5425-106">Ez biztosítja, hogy csak a megadott alkalmazások tudjanak csatlakozni a partner- és ügyféladatokhoz.</span><span class="sxs-lookup"><span data-stu-id="f5425-106">This helps ensure that only specified apps are able to connect to partner and customer data.</span></span>

<span data-ttu-id="f5425-107">A Partnerközpont esetében Microsoft Cloud for US Government PowerShellen keresztül kell kezelnie az alkalmazásokat.</span><span class="sxs-lookup"><span data-stu-id="f5425-107">For Partner Center for Microsoft Cloud for US Government, you currently must manage apps through PowerShell.</span></span> <span data-ttu-id="f5425-108">További információért tekintse meg a Azure PowerShell [dokumentációját.](/powershell/module/Azuread/#applications)</span><span class="sxs-lookup"><span data-stu-id="f5425-108">For more information, see the [Azure PowerShell reference documentation](/powershell/module/Azuread/#applications).</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="f5425-109">A Microsoft Cloud Germany vagy a microsoftos felhőszolgáltatásokhoz Partnerközpont alkalmazások létrehozásakor vegye figyelembe a Partnerközpont további Microsoft Cloud for US Government.</span><span class="sxs-lookup"><span data-stu-id="f5425-109">Be aware of the following additional requirements when you create an app for Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government.</span></span>

## <a name="web-apps"></a><span data-ttu-id="f5425-110">Webalkalmazások</span><span class="sxs-lookup"><span data-stu-id="f5425-110">Web apps</span></span>

<span data-ttu-id="f5425-111">Webalkalmazások esetén az alábbi eljárásokkal regisztrálhatja az alkalmazásazonosítót.</span><span class="sxs-lookup"><span data-stu-id="f5425-111">For web apps, use the following procedures to register your application ID.</span></span>

### <a name="create-or-update-web-app"></a><span data-ttu-id="f5425-112">Webalkalmazás létrehozása vagy frissítése</span><span class="sxs-lookup"><span data-stu-id="f5425-112">Create or update web app</span></span>

1. <span data-ttu-id="f5425-113">Nyissa meg a [Azure Portal – Alkalmazásregisztrációk](https://go.microsoft.com/fwlink/?linkid=2083908) oldalt az alkalmazás regisztráláshoz.</span><span class="sxs-lookup"><span data-stu-id="f5425-113">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="f5425-114">Jelentkezzen be egy munkahelyi vagy iskolai fiókkal vagy a személyes Microsoft-fiókjával az Azure Portalra.</span><span class="sxs-lookup"><span data-stu-id="f5425-114">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="f5425-115">Válassza **az Új regisztráció lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f5425-115">Select **New registration**.</span></span> <span data-ttu-id="f5425-116">További információ: [Rövid útmutató: Alkalmazás regisztrálása a Microsoft Identitásplatform.](/azure/active-directory/develop/quickstart-register-app)</span><span class="sxs-lookup"><span data-stu-id="f5425-116">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-web-app"></a><span data-ttu-id="f5425-117">API-hozzáférési engedélyek konfigurálása webalkalmazáshoz</span><span class="sxs-lookup"><span data-stu-id="f5425-117">Configure API access permissions for web app</span></span>

1. <span data-ttu-id="f5425-118">Válassza ki az alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="f5425-118">Choose your app.</span></span> <span data-ttu-id="f5425-119">A **Gépház** indítósávját.</span><span class="sxs-lookup"><span data-stu-id="f5425-119">Go to **Settings** of the Web app.</span></span>

2. <span data-ttu-id="f5425-120">Az **API Access (API-hozzáférés)** szakaszban válassza a **Required permissions (Szükséges engedélyek) lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f5425-120">In **API Access** section, choose **Required permissions**</span></span>

3. <span data-ttu-id="f5425-121">További Windows Azure Active Directory-engedélyekhez:</span><span class="sxs-lookup"><span data-stu-id="f5425-121">For Windows Azure Active directory permissions:</span></span>

    1. <span data-ttu-id="f5425-122">Válassza **Windows Azure Active Directory engedélyek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f5425-122">Choose **Windows Azure Active Directory permissions**.</span></span>

    2. <span data-ttu-id="f5425-123">Az **Alkalmazások engedélyei mezőben** válassza a Címtáradatok olvasása lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="f5425-123">In **Applications permissions**, select Read directory data.</span></span>

    3. <span data-ttu-id="f5425-124">Mentse az engedélyeket.</span><span class="sxs-lookup"><span data-stu-id="f5425-124">Save the permissions.</span></span>

4. <span data-ttu-id="f5425-125">Jegyezze fel a webalkalmazás **Tulajdonságok** szakaszában található alkalmazásazonosítót.</span><span class="sxs-lookup"><span data-stu-id="f5425-125">Note the application ID in the **Properties** section of your web app.</span></span>

### <a name="add-a-secret-key-to-your-app"></a><span data-ttu-id="f5425-126">Titkos kulcs hozzáadása az alkalmazáshoz</span><span class="sxs-lookup"><span data-stu-id="f5425-126">Add a secret key to your app</span></span>

1. <span data-ttu-id="f5425-127">Ugrás a **webalkalmazás** Kulcsok szakaszra.</span><span class="sxs-lookup"><span data-stu-id="f5425-127">Go to the **Keys** section of your web app.</span></span>

2. <span data-ttu-id="f5425-128">Adja meg a kulcs leírását, és szükség szerint válassza az 1 vagy 2 év lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="f5425-128">Enter key description and select duration as 1 or 2 years, as you need.</span></span>

3. <span data-ttu-id="f5425-129">Mentse és másolja ki a titkos kulcs értékét.</span><span class="sxs-lookup"><span data-stu-id="f5425-129">Save and copy the secret key value.</span></span> <span data-ttu-id="f5425-130">**Az oldal elhagyás után ez az érték nem jelenik meg újra.**</span><span class="sxs-lookup"><span data-stu-id="f5425-130">**This value will not be shown again once you leave this page.**</span></span>

<span data-ttu-id="f5425-131">A webalkalmazás konfigurációjában a következő adatoknak kell lennie:</span><span class="sxs-lookup"><span data-stu-id="f5425-131">You should have the following details from the web app configuration:</span></span>

- <span data-ttu-id="f5425-132">Alkalmazásazonosító</span><span class="sxs-lookup"><span data-stu-id="f5425-132">Application ID</span></span>
- <span data-ttu-id="f5425-133">Alkalmazás titkos kódja</span><span class="sxs-lookup"><span data-stu-id="f5425-133">Application secret</span></span>

### <a name="register-the-web-app-in-partner-center"></a><span data-ttu-id="f5425-134">A webalkalmazás regisztrálása a Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f5425-134">Register the Web app in Partner Center</span></span>

1. <span data-ttu-id="f5425-135">Jelentkezzen be itt: [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f5425-135">Sign in to [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span></span>

2. <span data-ttu-id="f5425-136">Válassza **az Irányítópult** lehetőséget, majd a Fiók **Gépház** az **Alkalmazáskezelés lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f5425-136">Choose **Dashboard**, then choose **Account Settings**, then choose **App Management**.</span></span>

3. <span data-ttu-id="f5425-137">A **Webalkalmazás szakaszban válassza** a **Meglévő alkalmazás regisztrálása lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f5425-137">In the **Web App** section, choose **Register existing app**.</span></span>

4. <span data-ttu-id="f5425-138">Válassza ki a Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f5425-138">Select the web app you created in Azure portal.</span></span>

5. <span data-ttu-id="f5425-139">Válassza **az alkalmazás regisztrálása lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f5425-139">Choose **register your app**.</span></span>

## <a name="native-apps"></a><span data-ttu-id="f5425-140">Natív alkalmazások</span><span class="sxs-lookup"><span data-stu-id="f5425-140">Native apps</span></span>

<span data-ttu-id="f5425-141">A natív alkalmazásokat nem kell regisztrálni a Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="f5425-141">Native apps do not need to be registered to Partner Center.</span></span> <span data-ttu-id="f5425-142">Ezeket az alkalmazásokat azonban úgy kell konfigurálni, hogy hozzáférést Partnerközpont API-khoz.</span><span class="sxs-lookup"><span data-stu-id="f5425-142">But these apps need to be configured to provide access to Partner Center APIs.</span></span>

>[!NOTE]
><span data-ttu-id="f5425-143">Mielőtt natív alkalmazást hoz létre a Azure Portal, jelentkezzen be a Partnerközpont a partnerbérlő rendszergazdai felhasználói hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="f5425-143">Before creating a native app in the Azure portal, log in into Partner Center using the admin user credentials from the partner tenant.</span></span> <span data-ttu-id="f5425-144">Ezzel létrehozza a bérlő beállításait az alkalmazásengedélyek engedélyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="f5425-144">This creates the settings on the tenant to enable app permissions.</span></span>

### <a name="create-native-app"></a><span data-ttu-id="f5425-145">Natív alkalmazás létrehozása</span><span class="sxs-lookup"><span data-stu-id="f5425-145">Create native app</span></span>

1. <span data-ttu-id="f5425-146">Nyissa meg a [Azure Portal – Alkalmazásregisztrációk](https://go.microsoft.com/fwlink/?linkid=2083908) oldalt az alkalmazás regisztráláshoz.</span><span class="sxs-lookup"><span data-stu-id="f5425-146">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="f5425-147">Jelentkezzen be egy munkahelyi vagy iskolai fiókkal vagy a személyes Microsoft-fiókjával az Azure Portalra.</span><span class="sxs-lookup"><span data-stu-id="f5425-147">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="f5425-148">Válassza **az Új regisztráció lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f5425-148">Select **New registration**.</span></span> <span data-ttu-id="f5425-149">További információ: [Rövid útmutató: Alkalmazás regisztrálása a Microsoft Identitásplatform.](/azure/active-directory/develop/quickstart-register-app)</span><span class="sxs-lookup"><span data-stu-id="f5425-149">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-native-app"></a><span data-ttu-id="f5425-150">API-hozzáférési engedélyek konfigurálása natív alkalmazáshoz</span><span class="sxs-lookup"><span data-stu-id="f5425-150">Configure API access permissions for native app</span></span>

1. <span data-ttu-id="f5425-151">Válassza ki az alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="f5425-151">Choose your app.</span></span> <span data-ttu-id="f5425-152">Ugrás a **Gépház.**</span><span class="sxs-lookup"><span data-stu-id="f5425-152">Go to **Settings**.</span></span>

2. <span data-ttu-id="f5425-153">Az API Access (API-hozzáférés) csoportban **válassza a Required permissions (Szükséges engedélyek) lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f5425-153">In API Access, choose **Required permissions**.</span></span>

3. <span data-ttu-id="f5425-154">Válassza **Windows Azure Active Directory engedélyek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f5425-154">Choose **Windows Azure Active Directory permissions**.</span></span> <span data-ttu-id="f5425-155">A **Delegált engedélyek beállításnál** válassza ki az alábbi engedélyeket:</span><span class="sxs-lookup"><span data-stu-id="f5425-155">In **Delegated permissions**, select these permissions:</span></span>

    - <span data-ttu-id="f5425-156">**Bejelentkezés és felhasználói profil olvasása**</span><span class="sxs-lookup"><span data-stu-id="f5425-156">**Sign in and read user profile**</span></span>
    - <span data-ttu-id="f5425-157">**Címtáradatok olvasása**</span><span class="sxs-lookup"><span data-stu-id="f5425-157">**Read directory data**</span></span>
    - <span data-ttu-id="f5425-158">**A címtár elérése a bejelentkezett felhasználó nevében**</span><span class="sxs-lookup"><span data-stu-id="f5425-158">**Access the directory as the signed-in user**</span></span>
    - <span data-ttu-id="f5425-159">**Az összes csoport olvasása**</span><span class="sxs-lookup"><span data-stu-id="f5425-159">**Read all groups**</span></span>

4. <span data-ttu-id="f5425-160">Mentse az engedélyeket.</span><span class="sxs-lookup"><span data-stu-id="f5425-160">Save the permissions.</span></span>

5. <span data-ttu-id="f5425-161">A **Szükséges engedélyek** között válassza a Hozzáadás **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f5425-161">Choose **Add** in **Required permissions**.</span></span>

6. <span data-ttu-id="f5425-162">Válassza az **API kiválasztása** elemet.</span><span class="sxs-lookup"><span data-stu-id="f5425-162">Choose **Select an API**.</span></span>

    1. <span data-ttu-id="f5425-163">A keresőmezőbe írja be a **Microsoft Partnerközpont,** és válassza ki a találatok listájából.</span><span class="sxs-lookup"><span data-stu-id="f5425-163">In the search box, enter **Microsoft Partner Center** and select it from the results list.</span></span>

    2. <span data-ttu-id="f5425-164">Válassza a **Kiválasztás** lehetőséget</span><span class="sxs-lookup"><span data-stu-id="f5425-164">Choose **Select**.</span></span>

7. <span data-ttu-id="f5425-165">Válassza **az Engedélyek kiválasztása lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f5425-165">Choose **Select permissions**.</span></span>

    1. <span data-ttu-id="f5425-166">Válassza **az Access Partnerközpont PPE lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f5425-166">Select **Access Partner Center PPE**.</span></span>
    
    2. <span data-ttu-id="f5425-167">Válassza a **Kiválasztás** lehetőséget</span><span class="sxs-lookup"><span data-stu-id="f5425-167">Choose **Select**.</span></span>

8. <span data-ttu-id="f5425-168">Válassza a **Kész** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="f5425-168">Choose **Done**.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="f5425-169">Jegyezze fel az alkalmazásazonosítót az alkalmazás Tulajdonságai között.</span><span class="sxs-lookup"><span data-stu-id="f5425-169">Note the application ID in the Properties of your app.</span></span>

<span data-ttu-id="f5425-170">Nem kell natív alkalmazásokat regisztrálnia a Partnerközpont, de a natív alkalmazást rendszergazdai jóváhagyással kell kiegészítenie.</span><span class="sxs-lookup"><span data-stu-id="f5425-170">You do not need to register native apps in Partner Center, however the native app must be admin consented.</span></span> <span data-ttu-id="f5425-171">Jegyezze fel a natív alkalmazás alkalmazásazonosítóját.</span><span class="sxs-lookup"><span data-stu-id="f5425-171">Note the application ID of your native app.</span></span>
