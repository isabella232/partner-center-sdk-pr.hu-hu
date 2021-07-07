---
title: API hozzáférésének beállítása a Partnerközpontban
description: Állítson be fiókokat a fejlesztéshez a Partnerközpont SDK és tesztelje az integrációs tesztkészletet.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2c564baa9b626ff6ce21f9bcc517902d7cf99244
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547427"
---
# <a name="set-up-api-access-in-partner-center"></a><span data-ttu-id="e17ca-103">API hozzáférésének beállítása a Partnerközpontban</span><span class="sxs-lookup"><span data-stu-id="e17ca-103">Set up API access in Partner Center</span></span>

<span data-ttu-id="e17ca-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont a Microsoft Cloud for US Government | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="e17ca-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="e17ca-105">Ez a cikk a fejlesztéshez szükséges fiókokat ismerteti Partnerközpont SDK.</span><span class="sxs-lookup"><span data-stu-id="e17ca-105">This article describes the accounts you need to develop against the Partner Center SDK.</span></span> <span data-ttu-id="e17ca-106">Ez a cikk azt is bemutatja, hogyan hozhat létre [integrációs tesztfiókot és](#integration-sandbox-account) tesztelni az integrációs tesztboxban.</span><span class="sxs-lookup"><span data-stu-id="e17ca-106">This article also explains how to create an [integration sandbox account](#integration-sandbox-account) and test in the integration sandbox.</span></span>

>[!NOTE]
><span data-ttu-id="e17ca-107">Az API-khoz való hozzáféréshez a bérlőnek CSP-bérlőnek kell lennie, önnek pedig közvetett szolgáltatónak vagy közvetlen számlázási partnernek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="e17ca-107">To get access to APIs, your tenant must be a CSP tenant and you must be either an indirect provider or a Direct bill partner.</span></span>

## <a name="account-definitions"></a><span data-ttu-id="e17ca-108">Fiókdefiníciók</span><span class="sxs-lookup"><span data-stu-id="e17ca-108">Account definitions</span></span>

<span data-ttu-id="e17ca-109">Az API-integráció integrálása és tesztelése érdekében a Partnerközpont kétféle fiókot támogat:</span><span class="sxs-lookup"><span data-stu-id="e17ca-109">To help you integrate and test your API integration, Partner Center supports two kinds of accounts:</span></span>

### <a name="primary-partner-account"></a><span data-ttu-id="e17ca-110">Elsődleges partnerfiók</span><span class="sxs-lookup"><span data-stu-id="e17ca-110">Primary Partner account</span></span>

<span data-ttu-id="e17ca-111">Ebben a fiókban hozhat létre valós rendeléseket valós ügyfelek számára.</span><span class="sxs-lookup"><span data-stu-id="e17ca-111">This account is where you create real orders for real customers.</span></span> <span data-ttu-id="e17ca-112">Ha módosításokat vagy tranzakciókat kell végeznie, amikor bejelentkezik az elsődleges fiókba, az Partnerközpont SDK vagy a Partner irányítópult felhasználói felületének használatával azok valós ügyfelek hivatalos rendeléseként lesznek kezelve.</span><span class="sxs-lookup"><span data-stu-id="e17ca-112">If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Dashboard UI, they will be treated as official orders for real customers.</span></span> <span data-ttu-id="e17ca-113">Ezek megjelennek a számlán, és a vállalat felelős a fizetésért.</span><span class="sxs-lookup"><span data-stu-id="e17ca-113">They will be reflected in your invoice, and your company is responsible for paying for them.</span></span>

### <a name="integration-sandbox-account"></a><span data-ttu-id="e17ca-114">Integrációs tesztkörnyezeti fiók</span><span class="sxs-lookup"><span data-stu-id="e17ca-114">Integration sandbox account</span></span>

<span data-ttu-id="e17ca-115">Ez a fiók a kód tesztelésére és a Partnerközpont API-okkal való integrációjára való, mielőtt széles körben üzembe helyezi.</span><span class="sxs-lookup"><span data-stu-id="e17ca-115">This account is for testing your code and its integration with the Partner Center APIs before you deploy it broadly.</span></span> <span data-ttu-id="e17ca-116">Az integrációs sandbox-fiókba való bejelentkezve végrehajtott módosítások és tranzakciók megjelennek a számlán, azonban nem kell kifizetnie a számla összegét.</span><span class="sxs-lookup"><span data-stu-id="e17ca-116">Changes and transactions you make when you are signed into the integration sandbox account will appear in your invoice, however, you do not have to pay the invoice amount.</span></span> <span data-ttu-id="e17ca-117">A pdf formátumú számlához a "DO NOT PAY" (NEM FIZET).</span><span class="sxs-lookup"><span data-stu-id="e17ca-117">Invoice pdf will have a disclaimer as "DO NOT PAY.</span></span> <span data-ttu-id="e17ca-118">EZ EGY SANDBOX-SZÁMLA, ÉS NINCS SZÜKSÉG BEAVATKOZÁSRA."</span><span class="sxs-lookup"><span data-stu-id="e17ca-118">THIS IS A SANDBOX INVOICE AND NO ACTION IS REQUIRED."</span></span>

<span data-ttu-id="e17ca-119">Az integrációs sandbox-fiók és az elsődleges fiók egymástól függetlenül működik, és nem oszt meg rendszergazdai fiókokat, felhasználói fiókokat, ügyfeleket, rendeléseket, előfizetéseket és más adatokat.</span><span class="sxs-lookup"><span data-stu-id="e17ca-119">The integration sandbox account and the primary account act independently, and do not share admin accounts, user accounts, customers, orders, subscriptions, or other data.</span></span>

<span data-ttu-id="e17ca-120">Az integrációs védőfal csak korlátozott számú ügyfél, megrendelés, előfizetés, licenc stb. esetén támogatja a tranzakciókat.</span><span class="sxs-lookup"><span data-stu-id="e17ca-120">The integration sandbox supports transactions with a limited number of customers, orders, subscriptions, licenses, etc.</span></span>

<span data-ttu-id="e17ca-121">Szabályzat szerint az integrációs tesztfiókok csak integrációs tesztelési célokra szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="e17ca-121">By policy, integration sandbox accounts are for integration testing purposes only.</span></span>

<span data-ttu-id="e17ca-122">Alapértelmezés szerint nincs integrációs tesztkörnyezeti fiók.</span><span class="sxs-lookup"><span data-stu-id="e17ca-122">By default, there is no integration sandbox account.</span></span> <span data-ttu-id="e17ca-123">Ha az alkalmazás használatát tervezi, saját magának kell létrehoznia Partnerközpont SDK.</span><span class="sxs-lookup"><span data-stu-id="e17ca-123">You must create one yourself if you plan to use the Partner Center SDK.</span></span>

## <a name="set-up-your-accounts"></a><span data-ttu-id="e17ca-124">A fiókok beállítása</span><span class="sxs-lookup"><span data-stu-id="e17ca-124">Set up your accounts</span></span>

<span data-ttu-id="e17ca-125">Ez a szakasz azt ismerteti, hogyan állíthat be elsődleges partnerfiókot és integrációs védőfalat a Partnerközpont SDK.</span><span class="sxs-lookup"><span data-stu-id="e17ca-125">This section describes how to set up a primary Partner account and an integration sandbox account for the Partner Center SDK.</span></span>

### <a name="create-an-integration-sandbox"></a><span data-ttu-id="e17ca-126">Integrációs védőfal létrehozása</span><span class="sxs-lookup"><span data-stu-id="e17ca-126">Create an integration sandbox</span></span>

1. <span data-ttu-id="e17ca-127">Jelentkezzen be a Partner irányítópultra egy globális rendszergazdai fiókkal (az elsődleges partnerfiókkal).</span><span class="sxs-lookup"><span data-stu-id="e17ca-127">Sign in to Partner Dashboard with a global admin account (your primary Partner account.)</span></span>

2. <span data-ttu-id="e17ca-128">A **Gépház** (fogaskerék ikon) válassza a **Partnerbeállítások lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e17ca-128">From the **Settings** menu (gear icon), choose **Partner settings**.</span></span>

3. <span data-ttu-id="e17ca-129">Válassza **az Integrációs védőfal** lapot.</span><span class="sxs-lookup"><span data-stu-id="e17ca-129">Choose **Integration sandbox** tab.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e17ca-130">Ha nem látja az Integrációs védőfal lehetőséget, előfordulhat, hogy nincs globális rendszergazdai fiókja.</span><span class="sxs-lookup"><span data-stu-id="e17ca-130">If you don't see an Integration sandbox option, you might not have a global admin account.</span></span> <span data-ttu-id="e17ca-131">Előfordulhat, hogy integrációs sandbox-fiókot használ, és már be van állítva egy integrációs védőfal.</span><span class="sxs-lookup"><span data-stu-id="e17ca-131">You also might be using an integration sandbox account and an integration sandbox has already been set up.</span></span>

4. <span data-ttu-id="e17ca-132">Adja meg az integrációs védőfal rendszergazdai fiókjának kapcsolattartási adatait.</span><span class="sxs-lookup"><span data-stu-id="e17ca-132">Enter the contact information for the integration sandbox admin account.</span></span> <span data-ttu-id="e17ca-133">Ezután válassza a **Fiók létrehozása lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e17ca-133">Then, choose **Create account**.</span></span> <span data-ttu-id="e17ca-134">Várjon néhány percet, amíg megerősítő üzenet jelenik meg a fiók létrejöttével.</span><span class="sxs-lookup"><span data-stu-id="e17ca-134">Wait a few minutes for a confirmation message that the account has been created.</span></span>

5. <span data-ttu-id="e17ca-135">Miután megjelenik a megerősítést kérő üzenet, jelentkezzen ki a Partner irányítópultjáról.</span><span class="sxs-lookup"><span data-stu-id="e17ca-135">After you see the confirmation message, sign out of Partner Dashboard.</span></span>

6. <span data-ttu-id="e17ca-136">Jelentkezzen be újra az új integrációs sandbox rendszergazdai fiókjával.</span><span class="sxs-lookup"><span data-stu-id="e17ca-136">Sign back in with your new integration sandbox admin account.</span></span> <span data-ttu-id="e17ca-137">Győződjön meg arról, hogy a hitelesítő adatok formátumát és a **username@domain** megadott jelszót használja.</span><span class="sxs-lookup"><span data-stu-id="e17ca-137">Be sure to use the format **username@domain** for your credentials along with the password that you specified.</span></span>

7. <span data-ttu-id="e17ca-138">Válassza **a Fiók beállítása az** Aktuális feladatok fölött **lehetőséget** a sandbox-fiók beállításának befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="e17ca-138">Choose **Set Up Account** above **Current Tasks** to complete the sandbox account setup.</span></span>

### <a name="enable-api-access"></a><span data-ttu-id="e17ca-139">API-hozzáférés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="e17ca-139">Enable API access</span></span>

<span data-ttu-id="e17ca-140">A fiók beállítása után engedélyeznie kell az API-hozzáférést, mielőtt használhatná a Partnerközpont SDK-t az integrációs tesztkörnyezettel.</span><span class="sxs-lookup"><span data-stu-id="e17ca-140">After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox.</span></span> <span data-ttu-id="e17ca-141">Az API-hoz való hozzáférést külön kell engedélyeznie az elsődleges partnerfiók és az integrációs tesztkörnyezeti fiók esetében is.</span><span class="sxs-lookup"><span data-stu-id="e17ca-141">You need to enable access to the API separately for both your primary Partner account and your integration sandbox account.</span></span>

1. <span data-ttu-id="e17ca-142">Jelentkezzen be a Partner irányítópultra egy globális rendszergazdai fiókkal.</span><span class="sxs-lookup"><span data-stu-id="e17ca-142">Sign into Partner Dashboard using a global admin account.</span></span>

2. <span data-ttu-id="e17ca-143">A **Gépház** (fogaskerék ikon) válassza a **Partnerbeállítások lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e17ca-143">From the **Settings** menu (gear icon), select **Partner settings**.</span></span>

3. <span data-ttu-id="e17ca-144">A **Fiókbeállítások lapon** válassza az **Alkalmazáskezelés lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e17ca-144">On the **Account settings** page, choose **App management**.</span></span>

4. <span data-ttu-id="e17ca-145">Ha még nem rendelkezik meglévő alkalmazással, adjon hozzá egy új webalkalmazást.</span><span class="sxs-lookup"><span data-stu-id="e17ca-145">If you do not already have an existing app, add a new web app.</span></span> <span data-ttu-id="e17ca-146">Ha már van webalkalmazása, válassza a Kulcs **hozzáadása** gombot.</span><span class="sxs-lookup"><span data-stu-id="e17ca-146">If you have an existing web app, choose the **Add key** button.</span></span>

5. <span data-ttu-id="e17ca-147">Másolja ki az alkalmazásregisztrációs adatokat, különösen a kulcsot, ha webalkalmazást hoz létre, és tárolja biztonságos helyen. </span><span class="sxs-lookup"><span data-stu-id="e17ca-147">Copy the app registration information, especially the **Key** if you're creating a web app, and store it in a safe place.</span></span>

6. <span data-ttu-id="e17ca-148">Jelentkezzen ki a Partner irányítópultjáról.</span><span class="sxs-lookup"><span data-stu-id="e17ca-148">Sign out of Partner Dashboard.</span></span>

7. <span data-ttu-id="e17ca-149">Jelentkezzen be újra az integrációs sandbox-fiókjával.</span><span class="sxs-lookup"><span data-stu-id="e17ca-149">Sign back in with your integration sandbox account.</span></span> <span data-ttu-id="e17ca-150">Ismételje meg a 2–5. lépést az API-hozzáférés az integrációs védőfalon való engedélyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="e17ca-150">Repeat steps 2-5 to enable API access in the integration sandbox.</span></span>

## <a name="write-and-test-code"></a><span data-ttu-id="e17ca-151">Kód írása és tesztelése</span><span class="sxs-lookup"><span data-stu-id="e17ca-151">Write and test code</span></span>

<span data-ttu-id="e17ca-152">Az integrációs tesztkészletben kódot írhat és tesztelhet.</span><span class="sxs-lookup"><span data-stu-id="e17ca-152">You can write code and test code in the integration sandbox.</span></span> <span data-ttu-id="e17ca-153">A következő információkra lesz szüksége az Azure [AD-Partnerközpont beállításhoz.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e17ca-153">You'll need the following information to [set up Partner Center authentication](partner-center-authentication.md) with Azure AD.</span></span>

| <span data-ttu-id="e17ca-154">Elem neve</span><span class="sxs-lookup"><span data-stu-id="e17ca-154">Item name</span></span> | <span data-ttu-id="e17ca-155">Elem helye</span><span class="sxs-lookup"><span data-stu-id="e17ca-155">Item location</span></span> |
| --------- | ------------- |
| <span data-ttu-id="e17ca-156">Alkalmazásazonosító /ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="e17ca-156">App ID / Client ID</span></span> | <span data-ttu-id="e17ca-157">A **Gépház** (fogaskerék ikon) válassza a **Partnerbeállítások lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e17ca-157">From the **Settings** menu (gear icon), select **Partner settings**.</span></span> <span data-ttu-id="e17ca-158">A **Fiókbeállítások lapon** válassza az **Alkalmazáskezelés lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e17ca-158">On the **Account settings** page, select **App Management**.</span></span> <span data-ttu-id="e17ca-159">Az alkalmazásazonosító/ügyfél-azonosító regisztrált **alkalmazásalkalmazás-azonosítóként szerepel a listában.**</span><span class="sxs-lookup"><span data-stu-id="e17ca-159">The App ID/Client ID is listed as the **Registered application App ID**.</span></span> |
| <span data-ttu-id="e17ca-160">Kulcs</span><span class="sxs-lookup"><span data-stu-id="e17ca-160">Key</span></span> | <span data-ttu-id="e17ca-161">Ha az [API-hozzáférés](#enable-api-access)engedélyezése szakaszban létrehozott egy webalkalmazást, ezt a kulcsot mentette az 5. lépésben.</span><span class="sxs-lookup"><span data-stu-id="e17ca-161">If you created a web app in the section [Enable API access](#enable-api-access), this is the key that you saved in step 5.</span></span> |
| <span data-ttu-id="e17ca-162">Tartomány</span><span class="sxs-lookup"><span data-stu-id="e17ca-162">Domain</span></span> | <span data-ttu-id="e17ca-163">Az integrációs védőfal tartománya.</span><span class="sxs-lookup"><span data-stu-id="e17ca-163">The domain for the integration sandbox.</span></span> |

## <a name="run-tested-code"></a><span data-ttu-id="e17ca-164">Tesztelt kód futtatása</span><span class="sxs-lookup"><span data-stu-id="e17ca-164">Run tested code</span></span>

<span data-ttu-id="e17ca-165">Ahhoz, hogy a megoldást valós ügyféladatokkal használva használva az integrációs védőfal hitelesítő adatairól az elsődleges partnerfiók hitelesítő adataira váltsa.</span><span class="sxs-lookup"><span data-stu-id="e17ca-165">To use your solution with real customer data, you must change from your integration sandbox credentials to your primary Partner account credentials.</span></span>

<span data-ttu-id="e17ca-166">Ha készen áll a tesztelt kód elsődleges partnerfiókban való használatára, be kell szereznie egy Azure AD biztonsági jogkivonatot.</span><span class="sxs-lookup"><span data-stu-id="e17ca-166">When you're ready to use your tested code in your primary Partner account, you must get an Azure AD security token.</span></span> <span data-ttu-id="e17ca-167">Ez a biztonsági jogkivonat a saját Partnerközpont, kulcson és tartományon alapul (az integrációs védőfali alkalmazás, a kulcs és a tartomány helyett).</span><span class="sxs-lookup"><span data-stu-id="e17ca-167">This security token is based on your Partner Center app, key, and domain (instead of your integration sandbox app, key, and domain).</span></span>

1. <span data-ttu-id="e17ca-168">Az Azure AD [Partnerközpont hitelesítő](partner-center-authentication.md) adatait használó Azure AD biztonsági jogkivonat le Partnerközpont lépéseit.</span><span class="sxs-lookup"><span data-stu-id="e17ca-168">Follow the steps in [Partner Center authentication](partner-center-authentication.md) to get an Azure AD security token using your primary Partner Center credentials.</span></span> <span data-ttu-id="e17ca-169">(Korábban ezeket a lépéseket követve lekért egy Azure AD biztonsági jogkivonatot az integrációs védőfalhoz.)</span><span class="sxs-lookup"><span data-stu-id="e17ca-169">(You previously followed these steps to get an Azure AD security token for your integration sandbox.)</span></span>

2. <span data-ttu-id="e17ca-170">Cserélje le a kódban az integrációs biztonsági jogkivonatot az elsődleges partnerfiók új biztonsági jogkivonatával.</span><span class="sxs-lookup"><span data-stu-id="e17ca-170">Replace the integration security token in your code with the new security token for your primary Partner account.</span></span>
