---
title: API hozzáférésének beállítása a Partnerközpontban
description: Fiókok beállítása a partner Center SDK-hoz való fejlesztéshez és teszteléshez az integrációs munkaterületen.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 873ff2ff9cecbfa92429958d3bfe2aa79fc3ad9a
ms.sourcegitcommit: d5de47c08ba661ba5de4935caa6843d7c2c91710
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/28/2020
ms.locfileid: "97768152"
---
# <a name="set-up-api-access-in-partner-center"></a><span data-ttu-id="534b9-103">API hozzáférésének beállítása a Partnerközpontban</span><span class="sxs-lookup"><span data-stu-id="534b9-103">Set up API access in Partner Center</span></span>

<span data-ttu-id="534b9-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="534b9-104">**Applies to:**</span></span>

- <span data-ttu-id="534b9-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="534b9-105">Partner Center</span></span>
- <span data-ttu-id="534b9-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="534b9-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="534b9-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="534b9-107">Partner Center for Microsoft Cloud for US Government</span></span>
- <span data-ttu-id="534b9-108">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="534b9-108">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="534b9-109">Ez a cikk azokat a fiókokat ismerteti, amelyeket a partneri központ SDK-val kell fejleszteni.</span><span class="sxs-lookup"><span data-stu-id="534b9-109">This article describes the accounts you need to develop against the Partner Center SDK.</span></span> <span data-ttu-id="534b9-110">Ez a cikk azt is ismerteti, hogyan lehet [integrációs homokozó-fiókot](#integration-sandbox-account) létrehozni és tesztelni az integrációs homokozóban.</span><span class="sxs-lookup"><span data-stu-id="534b9-110">This article also explains how to create an [integration sandbox account](#integration-sandbox-account) and test in the integration sandbox.</span></span>

>[!NOTE]
><span data-ttu-id="534b9-111">Az API-k eléréséhez a bérlőnek CSP-Bérlőnek kell lennie, és rendelkeznie kell közvetett szolgáltatóval vagy közvetlen számlázási partnerrel.</span><span class="sxs-lookup"><span data-stu-id="534b9-111">To get access to APIs, your tenant must be a CSP tenant and you must be either an indirect provider or a Direct bill partner.</span></span>

## <a name="account-definitions"></a><span data-ttu-id="534b9-112">Fiókok definíciói</span><span class="sxs-lookup"><span data-stu-id="534b9-112">Account definitions</span></span>

<span data-ttu-id="534b9-113">Az API-integráció integrálásához és teszteléséhez a partner Center két típusú fiókot támogat:</span><span class="sxs-lookup"><span data-stu-id="534b9-113">To help you integrate and test your API integration, Partner Center supports two kinds of accounts:</span></span>

### <a name="primary-partner-account"></a><span data-ttu-id="534b9-114">Elsődleges partner fiók</span><span class="sxs-lookup"><span data-stu-id="534b9-114">Primary Partner account</span></span>

<span data-ttu-id="534b9-115">Ezzel a fiókkal valódi rendeléseket hozhat létre valódi ügyfelek számára.</span><span class="sxs-lookup"><span data-stu-id="534b9-115">This account is where you create real orders for real customers.</span></span> <span data-ttu-id="534b9-116">Ha módosításokat vagy tranzakciókat végez, amikor bejelentkezik az elsődleges fiókba, a partner Center SDK-val vagy a partner irányítópult felhasználói felületével, a rendszer a valódi ügyfelek számára hivatalos megrendelésként kezeli őket.</span><span class="sxs-lookup"><span data-stu-id="534b9-116">If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Dashboard UI, they will be treated as official orders for real customers.</span></span> <span data-ttu-id="534b9-117">Ezek a számlán jelennek meg, és a vállalat felelős azért, hogy fizessen értük.</span><span class="sxs-lookup"><span data-stu-id="534b9-117">They will be reflected in your invoice, and your company is responsible for paying for them.</span></span>

### <a name="integration-sandbox-account"></a><span data-ttu-id="534b9-118">Integrációs tesztkörnyezeti fiók</span><span class="sxs-lookup"><span data-stu-id="534b9-118">Integration sandbox account</span></span>

<span data-ttu-id="534b9-119">Ez a fiók a kód és a partner Center API-k integrálásának tesztelésére szolgál, mielőtt széleskörűen telepítené.</span><span class="sxs-lookup"><span data-stu-id="534b9-119">This account is for testing your code and its integration with the Partner Center APIs before you deploy it broadly.</span></span> <span data-ttu-id="534b9-120">Az integrációs csomagba való bejelentkezéskor elvégzett módosítások és tranzakciók megjelennek a számlán, azonban nem kell megfizetnie a számla összegét.</span><span class="sxs-lookup"><span data-stu-id="534b9-120">Changes and transactions you make when you are signed into the integration sandbox account will appear in your invoice, however, you do not have to pay the invoice amount.</span></span> <span data-ttu-id="534b9-121">A számla PDF-fájlja a "fizetés nélkül" nyilatkozatot kapja.</span><span class="sxs-lookup"><span data-stu-id="534b9-121">Invoice pdf will have a disclaimer as "DO NOT PAY.</span></span> <span data-ttu-id="534b9-122">EZ EGY SANDBOX-SZÁMLA, ÉS NINCS SZÜKSÉG BEAVATKOZÁSRA. "</span><span class="sxs-lookup"><span data-stu-id="534b9-122">THIS IS A SANDBOX INVOICE AND NO ACTION IS REQUIRED."</span></span>

<span data-ttu-id="534b9-123">Az integrációs csomag fiókja és az elsődleges fiók egymástól függetlenül működik, és nem oszt meg rendszergazdai fiókokat, felhasználói fiókokat, ügyfeleket, rendeléseket, előfizetéseket és egyéb adatait.</span><span class="sxs-lookup"><span data-stu-id="534b9-123">The integration sandbox account and the primary account act independently, and do not share admin accounts, user accounts, customers, orders, subscriptions, or other data.</span></span>

<span data-ttu-id="534b9-124">Az integrációs munkaterületen korlátozott számú ügyféllel, rendeléssel, előfizetéssel és licenccel rendelkező tranzakciók támogatottak.</span><span class="sxs-lookup"><span data-stu-id="534b9-124">The integration sandbox supports transactions with a limited number of customers, orders, subscriptions, licenses, etc.</span></span>

<span data-ttu-id="534b9-125">Házirend szerint az integrációs munkaterületek csak integrációs tesztelési célokat szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="534b9-125">By policy, integration sandbox accounts are for integration testing purposes only.</span></span>

<span data-ttu-id="534b9-126">Alapértelmezés szerint nincs integrációs tesztkörnyezeti fiók.</span><span class="sxs-lookup"><span data-stu-id="534b9-126">By default, there is no integration sandbox account.</span></span> <span data-ttu-id="534b9-127">Létre kell hoznia egyet, ha azt tervezi, hogy a partner Center SDK-t használja.</span><span class="sxs-lookup"><span data-stu-id="534b9-127">You must create one yourself if you plan to use the Partner Center SDK.</span></span>

## <a name="set-up-your-accounts"></a><span data-ttu-id="534b9-128">Fiókok beállítása</span><span class="sxs-lookup"><span data-stu-id="534b9-128">Set up your accounts</span></span>

<span data-ttu-id="534b9-129">Ez a szakasz azt ismerteti, hogyan állíthat be egy elsődleges partneri fiókot és egy integrációs sandbox-fiókot a partner Center SDK-hoz.</span><span class="sxs-lookup"><span data-stu-id="534b9-129">This section describes how to set up a primary Partner account and an integration sandbox account for the Partner Center SDK.</span></span>

### <a name="create-an-integration-sandbox"></a><span data-ttu-id="534b9-130">Integrációs homokozó létrehozása</span><span class="sxs-lookup"><span data-stu-id="534b9-130">Create an integration sandbox</span></span>

1. <span data-ttu-id="534b9-131">Jelentkezzen be a partner-irányítópultra egy globális rendszergazdai fiókkal (az elsődleges partner fiókjával).</span><span class="sxs-lookup"><span data-stu-id="534b9-131">Sign in to Partner Dashboard with a global admin account (your primary Partner account.)</span></span>

2. <span data-ttu-id="534b9-132">A **Beállítások** menüben (fogaskerék ikon) válassza a **partneri beállítások** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="534b9-132">From the **Settings** menu (gear icon), choose **Partner settings**.</span></span>

3. <span data-ttu-id="534b9-133">Válassza az **integrációs** munkaterületek fület.</span><span class="sxs-lookup"><span data-stu-id="534b9-133">Choose **Integration sandbox** tab.</span></span>

    >[!NOTE]
    ><span data-ttu-id="534b9-134">Ha nem lát integrációs munkaterületet, előfordulhat, hogy nem rendelkezik globális rendszergazdai fiókkal.</span><span class="sxs-lookup"><span data-stu-id="534b9-134">If you don't see an Integration sandbox option, you might not have a global admin account.</span></span> <span data-ttu-id="534b9-135">Az is előfordulhat, hogy egy integrációs homokozó-fiókot használ, és már be van állítva egy integrációs homokozó.</span><span class="sxs-lookup"><span data-stu-id="534b9-135">You also might be using an integration sandbox account and an integration sandbox has already been set up.</span></span>

4. <span data-ttu-id="534b9-136">Adja meg az integrációs munkaterülethez tartozó rendszergazdai fiók kapcsolattartási adatait.</span><span class="sxs-lookup"><span data-stu-id="534b9-136">Enter the contact information for the integration sandbox admin account.</span></span> <span data-ttu-id="534b9-137">Ezután válassza a **fiók létrehozása** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="534b9-137">Then, choose **Create account**.</span></span> <span data-ttu-id="534b9-138">Várjon néhány percet, amíg egy megerősítő üzenetben létrejött a fiók.</span><span class="sxs-lookup"><span data-stu-id="534b9-138">Wait a few minutes for a confirmation message that the account has been created.</span></span>

5. <span data-ttu-id="534b9-139">Miután megtalálta a megerősítő üzenetet, jelentkezzen ki a partner irányítópulton.</span><span class="sxs-lookup"><span data-stu-id="534b9-139">After you see the confirmation message, sign out of Partner Dashboard.</span></span>

6. <span data-ttu-id="534b9-140">Jelentkezzen be újra az új integrációs homokozó rendszergazdai fiókjával.</span><span class="sxs-lookup"><span data-stu-id="534b9-140">Sign back in with your new integration sandbox admin account.</span></span> <span data-ttu-id="534b9-141">Ügyeljen arra, hogy a **username@domain** hitelesítő adatok formátumát az imént megadott jelszóval együtt használja.</span><span class="sxs-lookup"><span data-stu-id="534b9-141">Be sure to use the format **username@domain** for your credentials along with the password that you just specified.</span></span>

7. <span data-ttu-id="534b9-142">Válassza a **fiók beállítása** a **jelenlegi feladatok** felett lehetőséget a sandbox-fiók beállításának befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="534b9-142">Choose **Set Up Account** above **Current Tasks** to complete the sandbox account setup.</span></span>

### <a name="enable-api-access"></a><span data-ttu-id="534b9-143">API-hozzáférés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="534b9-143">Enable API access</span></span>

<span data-ttu-id="534b9-144">A fiók beállítása után engedélyeznie kell az API-hozzáférést, mielőtt használhatná a Partnerközpont SDK-t az integrációs tesztkörnyezettel.</span><span class="sxs-lookup"><span data-stu-id="534b9-144">After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox.</span></span> <span data-ttu-id="534b9-145">Az API-hoz való hozzáférést külön kell engedélyeznie az elsődleges partnerfiók és az integrációs tesztkörnyezeti fiók esetében is.</span><span class="sxs-lookup"><span data-stu-id="534b9-145">You need to enable access to the API separately for both your primary Partner account and your integration sandbox account.</span></span>

1. <span data-ttu-id="534b9-146">Jelentkezzen be a partner irányítópultra egy globális rendszergazdai fiók használatával.</span><span class="sxs-lookup"><span data-stu-id="534b9-146">Sign into Partner Dashboard using a global admin account.</span></span>

2. <span data-ttu-id="534b9-147">A **Beállítások** menüben (fogaskerék ikon) válassza a **partneri beállítások** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="534b9-147">From the **Settings** menu (gear icon), select **Partner settings**.</span></span>

3. <span data-ttu-id="534b9-148">A **Fiókbeállítások** lapon válassza az alkalmazás- **kezelés** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="534b9-148">On the **Account settings** page, choose **App management**.</span></span>

4. <span data-ttu-id="534b9-149">Ha még nem rendelkezik meglévő alkalmazással, vegyen fel egy új webalkalmazást.</span><span class="sxs-lookup"><span data-stu-id="534b9-149">If you do not already have an existing app, add a new web app.</span></span> <span data-ttu-id="534b9-150">Ha van meglévő webalkalmazása, kattintson a **Kulcs hozzáadása** gombra.</span><span class="sxs-lookup"><span data-stu-id="534b9-150">If you have an existing web app, choose the **Add key** button.</span></span>

5. <span data-ttu-id="534b9-151">Másolja az alkalmazás regisztrációs adatait, különösen a **kulcsot** , ha webalkalmazást hoz létre, és tárolja biztonságos helyen.</span><span class="sxs-lookup"><span data-stu-id="534b9-151">Copy the app registration information, especially the **Key** if you're creating a web app, and store it in a safe place.</span></span>

6. <span data-ttu-id="534b9-152">Jelentkezzen ki a partner irányítópultján.</span><span class="sxs-lookup"><span data-stu-id="534b9-152">Sign out of Partner Dashboard.</span></span>

7. <span data-ttu-id="534b9-153">Jelentkezzen be a szolgáltatásba az integrációs sandbox-fiókjával.</span><span class="sxs-lookup"><span data-stu-id="534b9-153">Sign back in with your integration sandbox account.</span></span> <span data-ttu-id="534b9-154">Ismételje meg az 2-5-es lépéseket az API-hozzáférés engedélyezéséhez az integrációs homokozóban.</span><span class="sxs-lookup"><span data-stu-id="534b9-154">Repeat steps 2-5 to enable API access in the integration sandbox.</span></span>

## <a name="write-and-test-code"></a><span data-ttu-id="534b9-155">Kód írása és tesztelése</span><span class="sxs-lookup"><span data-stu-id="534b9-155">Write and test code</span></span>

<span data-ttu-id="534b9-156">Kódot és tesztelési kódot írhat az integrációs homokozóban.</span><span class="sxs-lookup"><span data-stu-id="534b9-156">You can write code and test code in the integration sandbox.</span></span> <span data-ttu-id="534b9-157">A következő információkra lesz szüksége a [partneri központ hitelesítésének beállításához](partner-center-authentication.md) az Azure ad-ben.</span><span class="sxs-lookup"><span data-stu-id="534b9-157">You'll need the following information to [set up Partner Center authentication](partner-center-authentication.md) with Azure AD.</span></span>

| <span data-ttu-id="534b9-158">Elemnév</span><span class="sxs-lookup"><span data-stu-id="534b9-158">Item name</span></span> | <span data-ttu-id="534b9-159">Pont helye</span><span class="sxs-lookup"><span data-stu-id="534b9-159">Item location</span></span> |
| --------- | ------------- |
| <span data-ttu-id="534b9-160">Alkalmazás azonosítója/ügyfél-azonosítója</span><span class="sxs-lookup"><span data-stu-id="534b9-160">App ID / Client ID</span></span> | <span data-ttu-id="534b9-161">A **Beállítások** menüben (fogaskerék ikon) válassza a **partneri beállítások** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="534b9-161">From the **Settings** menu (gear icon), select **Partner settings**.</span></span> <span data-ttu-id="534b9-162">A **Fiókbeállítások** lapon válassza az alkalmazás- **kezelés** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="534b9-162">On the **Account settings** page, select **App Management**.</span></span> <span data-ttu-id="534b9-163">Az alkalmazás azonosítója/ügyfél-azonosítója a **regisztrált Application app-azonosítóként** szerepel.</span><span class="sxs-lookup"><span data-stu-id="534b9-163">The App ID/Client ID is listed as the **Registered application App ID**.</span></span> |
| <span data-ttu-id="534b9-164">Kulcs</span><span class="sxs-lookup"><span data-stu-id="534b9-164">Key</span></span> | <span data-ttu-id="534b9-165">Ha létrehozott egy webalkalmazást az API- [hozzáférés engedélyezése](#enable-api-access)szakaszban, akkor ez az 5. lépésben mentett kulcs.</span><span class="sxs-lookup"><span data-stu-id="534b9-165">If you created a web app in the section [Enable API access](#enable-api-access), this is the key that you saved in step 5.</span></span> |
| <span data-ttu-id="534b9-166">Tartomány</span><span class="sxs-lookup"><span data-stu-id="534b9-166">Domain</span></span> | <span data-ttu-id="534b9-167">Az integrációs homokozó tartománya.</span><span class="sxs-lookup"><span data-stu-id="534b9-167">The domain for the integration sandbox.</span></span> |

## <a name="run-tested-code"></a><span data-ttu-id="534b9-168">Tesztelt kód futtatása</span><span class="sxs-lookup"><span data-stu-id="534b9-168">Run tested code</span></span>

<span data-ttu-id="534b9-169">Ha valódi ügyféladatokat szeretne használni a megoldásban, az integrációs csomag hitelesítő adatait az elsődleges partneri fiók hitelesítő adataira kell váltania.</span><span class="sxs-lookup"><span data-stu-id="534b9-169">To use your solution with real customer data, you must change from your integration sandbox credentials to your primary Partner account credentials.</span></span>

<span data-ttu-id="534b9-170">Ha készen áll a tesztelt kód használatára az elsődleges partner fiókjában, be kell szereznie egy Azure AD biztonsági jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="534b9-170">When you're ready to use your tested code in your primary Partner account, you must get an Azure AD security token.</span></span> <span data-ttu-id="534b9-171">Ez a biztonsági jogkivonat a partner Center-alkalmazáson, a kulcson és a tartományon alapul (az integrációs homokozó alkalmazás, a kulcs és a tartomány helyett).</span><span class="sxs-lookup"><span data-stu-id="534b9-171">This security token is based on your Partner Center app, key and domain (instead of your integration sandbox app, key and domain).</span></span>

1. <span data-ttu-id="534b9-172">Kövesse a [partneri központ hitelesítésének](partner-center-authentication.md) lépéseit az Azure ad biztonsági jogkivonat beszerzéséhez az elsődleges partneri központ hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="534b9-172">Follow the steps in [Partner Center authentication](partner-center-authentication.md) to get an Azure AD security token using your primary Partner Center credentials.</span></span> <span data-ttu-id="534b9-173">(Korábban ezeket a lépéseket követve beszerezhet egy Azure AD biztonsági jogkivonatot az integrációs munkaterülethez.)</span><span class="sxs-lookup"><span data-stu-id="534b9-173">(You previously followed these steps to get an Azure AD security token for your integration sandbox.)</span></span>

2. <span data-ttu-id="534b9-174">Cserélje le az integrációs biztonsági tokent a kódban az elsődleges partner fiókjához tartozó új biztonsági jogkivonatra.</span><span class="sxs-lookup"><span data-stu-id="534b9-174">Replace the integration security token in your code with the new security token for your primary Partner account.</span></span>
