---
title: Közvetett viszonteladó létrehozása a sandboxban
description: Információkat nyújt a tesztbox közvetett szolgáltatói számára a végpontok közötti tesztelés API-k használatával való engedélyezéséről.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93e26792b66e447a0047bd550f4302c7fca4e87b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973434"
---
# <a name="create-indirect-reseller-in-sandbox"></a><span data-ttu-id="070be-103">Közvetett viszonteladó létrehozása a sandboxban</span><span class="sxs-lookup"><span data-stu-id="070be-103">Create Indirect Reseller in Sandbox</span></span>

<span data-ttu-id="070be-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="070be-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="070be-105">Ez a dokumentum bemutatja, hogyan hozhat létre tesztkészlet közvetett szolgáltatókat, és hogyan engedélyezheti a végpontok közötti tesztelést API-k használatával.</span><span class="sxs-lookup"><span data-stu-id="070be-105">This document shows how to create Sandbox Indirect Providers and enable end-to-end testing using APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="070be-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="070be-106">Prerequisites</span></span>

- <span data-ttu-id="070be-107">A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="070be-107">Credentials as described in [Partner Center Authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="070be-108">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="070be-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="csp-indirect-provider"></a><span data-ttu-id="070be-109">CSP – Közvetett szolgáltató</span><span class="sxs-lookup"><span data-stu-id="070be-109">CSP Indirect Provider</span></span>

| <span data-ttu-id="070be-110">Éles képességek</span><span class="sxs-lookup"><span data-stu-id="070be-110">Production capabilities</span></span>             | <span data-ttu-id="070be-111">A sandbox képességei</span><span class="sxs-lookup"><span data-stu-id="070be-111">Sandbox capabilities</span></span>                            |
|-------------------------------------|-------------------------------------------------|
| <span data-ttu-id="070be-112">Értékesítés a közvetett viszonteladón keresztül a végfelhasználónak</span><span class="sxs-lookup"><span data-stu-id="070be-112">Sells through the indirect reseller to the end customer</span></span> | <span data-ttu-id="070be-113">Támogatott</span><span class="sxs-lookup"><span data-stu-id="070be-113">Supported</span></span> |
| <span data-ttu-id="070be-114">Az összes értékesítés, számlázás, kiépítés és felügyelet/támogatás tulajdonában van</span><span class="sxs-lookup"><span data-stu-id="070be-114">Owns all sales, billing, provisioning, and management/support</span></span> | <span data-ttu-id="070be-115">Támogatott</span><span class="sxs-lookup"><span data-stu-id="070be-115">Supported</span></span> |
| <span data-ttu-id="070be-116">Partnerkapcsolat kérése a viszonteladóktól</span><span class="sxs-lookup"><span data-stu-id="070be-116">Request a partnership with the resellers</span></span> | <span data-ttu-id="070be-117">Támogatott</span><span class="sxs-lookup"><span data-stu-id="070be-117">Supported</span></span> |
| <span data-ttu-id="070be-118">Ügyfelek megtekintése viszonteladó szerint</span><span class="sxs-lookup"><span data-stu-id="070be-118">View customers by Reseller</span></span> | <span data-ttu-id="070be-119">Támogatott</span><span class="sxs-lookup"><span data-stu-id="070be-119">Supported</span></span> |
| <span data-ttu-id="070be-120">Új ügyfelek hozzáadása viszonteladók szerint</span><span class="sxs-lookup"><span data-stu-id="070be-120">Add new customers by resellers</span></span> | <span data-ttu-id="070be-121">Támogatott</span><span class="sxs-lookup"><span data-stu-id="070be-121">Supported</span></span> |
| <span data-ttu-id="070be-122">Ügyfelek meghívása</span><span class="sxs-lookup"><span data-stu-id="070be-122">Invite customers</span></span> | <span data-ttu-id="070be-123">Az ügyfélkapcsolati kérés nem támogatott a sandboxban</span><span class="sxs-lookup"><span data-stu-id="070be-123">Customer relationship request not supported in Sandbox</span></span> |
| <span data-ttu-id="070be-124">A sandbox indirect provider (Sandbox Indirect Provider) kiválaszthatja a Sandbox IR (MPN ID) (Sandbox IR ( MPN-azonosító) lehetőséget a POR-ként a tranzakció elhelyezésekor</span><span class="sxs-lookup"><span data-stu-id="070be-124">Sandbox Indirect Provider can select Sandbox IR (MPN ID) as the POR while placing the transaction</span></span> | <span data-ttu-id="070be-125">Támogatott</span><span class="sxs-lookup"><span data-stu-id="070be-125">Supported</span></span> |
| <span data-ttu-id="070be-126">Éles környezetben nem támogatott</span><span class="sxs-lookup"><span data-stu-id="070be-126">Not supported in production</span></span> | <span data-ttu-id="070be-127">A sandbox indirect provider (Közvetett sandbox-szolgáltató) közvetett viszonteladót hozhat létre</span><span class="sxs-lookup"><span data-stu-id="070be-127">Sandbox Indirect Provider can create Sandbox Indirect Reseller</span></span> |
| <span data-ttu-id="070be-128">A sandbox MPN-azonosítót kell megadni, a termék MPN-azonosítója nem fog működni</span><span class="sxs-lookup"><span data-stu-id="070be-128">Sandbox MPN ID should be entered, the product MPN ID will not work</span></span> | <span data-ttu-id="070be-129">Éles környezetben nem támogatott</span><span class="sxs-lookup"><span data-stu-id="070be-129">Not supported in production</span></span> |
| <span data-ttu-id="070be-130">Éles környezetben nem támogatott</span><span class="sxs-lookup"><span data-stu-id="070be-130">Not supported in production</span></span> | <span data-ttu-id="070be-131">A közvetett sandbox-szolgáltató törölheti a közvetett viszonteladót</span><span class="sxs-lookup"><span data-stu-id="070be-131">Sandbox Indirect Provider can delete Sandbox Indirect Reseller</span></span> |

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller"></a><span data-ttu-id="070be-132">Közvetett sandbox szolgáltató – Közvetett viszonteladó létrehozása a sandboxban</span><span class="sxs-lookup"><span data-stu-id="070be-132">Sandbox Indirect Provider – Create Sandbox Indirect Reseller</span></span>

<span data-ttu-id="070be-133">Ez a funkció csak a Sandboxban érhető el, és lehetővé teszi közvetett viszonteladók létrehozására a Sandbox Indirect Providers (Közvetett viszonteladók) lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="070be-133">This feature is only available in the Sandbox and gives Sandbox Indirect Providers an ability to create Sandbox Indirect Resellers.</span></span>

1. <span data-ttu-id="070be-134">A közvetett viszonteladók által engedélyezett öt közvetett viszonteladóra vonatkozó korlát a közvetett sandbox-szolgáltatónként</span><span class="sxs-lookup"><span data-stu-id="070be-134">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider</span></span>
2. <span data-ttu-id="070be-135">A közvetett sandbox-szolgáltatók közvetett viszonteladóval hozhatnak létre `associatedPartnerId` ügyfeleket</span><span class="sxs-lookup"><span data-stu-id="070be-135">Sandbox Indirect Providers can create customers with `associatedPartnerId` of Sandbox Indirect Reseller</span></span>
3. <span data-ttu-id="070be-136">Adja meg [egy adott régió MPN-azonosítóját](/partner-center/mpn-create-a-partner-center-account) egy közvetett viszonteladó létrehozása során.</span><span class="sxs-lookup"><span data-stu-id="070be-136">Enter the [MPN](/partner-center/mpn-create-a-partner-center-account) ID of a specific region while creating a Sandbox Indirect Reseller.</span></span> <span data-ttu-id="070be-137">Több közvetett viszonteladó is létre lehet hozva ugyanazokkal a sandbox MPN-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="070be-137">Multiple Sandbox Indirect Resellers can be created with the same Sandbox MPN ID.</span></span>
4. <span data-ttu-id="070be-138">Közvetett sandbox-szolgáltatónként csak 75 ügyfél engedélyezett</span><span class="sxs-lookup"><span data-stu-id="070be-138">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="sandbox-indirect-resellers--view-customers"></a><span data-ttu-id="070be-139">Sandbox Indirect Resellers ( Közvetett viszonteladók – Ügyfelek megtekintése)</span><span class="sxs-lookup"><span data-stu-id="070be-139">Sandbox Indirect Resellers – View customers</span></span>

1. <span data-ttu-id="070be-140">A sandbox Indirect Resellers (A közvetett sandbox-viszonteladók) megtekinthetik a sandbox-ügyfelek listáját közvetett sandbox-szolgáltatók szerint.</span><span class="sxs-lookup"><span data-stu-id="070be-140">Sandbox Indirect Resellers can view the list of sandbox customers by Sandbox Indirect providers.</span></span>
2. <span data-ttu-id="070be-141">A közvetett sandbox-viszonteladók delegált rendszergazdai engedélyekkel kezelhetik az ügyfélfiókot.</span><span class="sxs-lookup"><span data-stu-id="070be-141">Sandbox Indirect Resellers can manage the customer account by using delegated administrator permissions.</span></span>

## <a name="create-sandbox-indirect-reseller-through-api"></a><span data-ttu-id="070be-142">Közvetett viszonteladó létrehozása a Sandboxban API-n keresztül</span><span class="sxs-lookup"><span data-stu-id="070be-142">Create Sandbox Indirect Reseller through API</span></span>

### <a name="rest-request"></a><span data-ttu-id="070be-143">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="070be-143">REST request</span></span>

#### <a name="request-syntax"></a><span data-ttu-id="070be-144">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="070be-144">Request syntax</span></span>

| <span data-ttu-id="070be-145">**Metódus**</span><span class="sxs-lookup"><span data-stu-id="070be-145">**Method**</span></span> | <span data-ttu-id="070be-146">**Kérés URI-ja**</span><span class="sxs-lookup"><span data-stu-id="070be-146">**Request URI**</span></span>                                                        |
|------------|------------------------------------------------------------------------|
| <span data-ttu-id="070be-147">**Post**</span><span class="sxs-lookup"><span data-stu-id="070be-147">**POST**</span></span>   | <span data-ttu-id="070be-148">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller</span><span class="sxs-lookup"><span data-stu-id="070be-148">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="070be-149">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="070be-149">Request headers</span></span>

- <span data-ttu-id="070be-150">Ez az API idempotent (nem ad vissza más eredményt, ha többször is meghívja).</span><span class="sxs-lookup"><span data-stu-id="070be-150">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>
- <span data-ttu-id="070be-151">Szükség van egy kérésazonosítóra és egy korrelációs azonosítóra.</span><span class="sxs-lookup"><span data-stu-id="070be-151">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="070be-152">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="070be-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="070be-153">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="070be-153">Request body</span></span>

<span data-ttu-id="070be-154">Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="070be-154">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="070be-155">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="070be-155">Property</span></span>             | <span data-ttu-id="070be-156">Típus</span><span class="sxs-lookup"><span data-stu-id="070be-156">Type</span></span>           | <span data-ttu-id="070be-157">Leírás</span><span class="sxs-lookup"><span data-stu-id="070be-157">Description</span></span>                                      |
|----------------------|----------------|--------------------------------------------------|
| <span data-ttu-id="070be-158">mpnId</span><span class="sxs-lookup"><span data-stu-id="070be-158">mpnId</span></span>                | <span data-ttu-id="070be-159">sztring</span><span class="sxs-lookup"><span data-stu-id="070be-159">string</span></span>         | <span data-ttu-id="070be-160">Az integrációs integrációs csomag MPN-azonosítója egy adott régióban</span><span class="sxs-lookup"><span data-stu-id="070be-160">The MPN ID for the IR in specific region</span></span>         |
| <span data-ttu-id="070be-161">Bérlő</span><span class="sxs-lookup"><span data-stu-id="070be-161">tenant</span></span>               | <span data-ttu-id="070be-162">&lt;Szótárszavak, sztringek&gt;</span><span class="sxs-lookup"><span data-stu-id="070be-162">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="070be-163">A létrehozni szükséges fiókot definiáló alapvető információk gyűjteménye</span><span class="sxs-lookup"><span data-stu-id="070be-163">Collection of basic information that defines an account to be created</span></span> |
| <span data-ttu-id="070be-164">legalBusinessProfile</span><span class="sxs-lookup"><span data-stu-id="070be-164">legalBusinessProfile</span></span> | <span data-ttu-id="070be-165">&lt;Szótárszavak, sztringek&gt;</span><span class="sxs-lookup"><span data-stu-id="070be-165">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="070be-166">A jogi személynek (például kapcsolattartónak, címnek és névnek) megfelelő adatok gyűjteménye</span><span class="sxs-lookup"><span data-stu-id="070be-166">Collection of information that represents the legal business entity such as contact, address, and name</span></span> |
| <span data-ttu-id="070be-167">organizationProfileLanguage</span><span class="sxs-lookup"><span data-stu-id="070be-167">organizationProfileLanguage</span></span> | <span data-ttu-id="070be-168">&lt;Szótárszavak, sztringek&gt;</span><span class="sxs-lookup"><span data-stu-id="070be-168">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="070be-169">A szervezet nyelvazonosítója</span><span class="sxs-lookup"><span data-stu-id="070be-169">The organization language identifier</span></span> |

<span data-ttu-id="070be-170">Ez a táblázat a bérlői attribútumban szükséges **tulajdonságokat ismerteti.**</span><span class="sxs-lookup"><span data-stu-id="070be-170">This table describes the required properties in the **tenant** attribute.</span></span>

| <span data-ttu-id="070be-171">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="070be-171">Property</span></span>           | <span data-ttu-id="070be-172">Típus</span><span class="sxs-lookup"><span data-stu-id="070be-172">Type</span></span>           | <span data-ttu-id="070be-173">Leírás</span><span class="sxs-lookup"><span data-stu-id="070be-173">Description</span></span>                         |
|--------------------|----------------|-------------------------------------|
| <span data-ttu-id="070be-174">domainPrefix (tartomány előtagja)</span><span class="sxs-lookup"><span data-stu-id="070be-174">domainPrefix</span></span>       | <span data-ttu-id="070be-175">Sztring; Egyedi</span><span class="sxs-lookup"><span data-stu-id="070be-175">String; unique</span></span> | <span data-ttu-id="070be-176">A bérlőfiók tartománya</span><span class="sxs-lookup"><span data-stu-id="070be-176">Domain for the tenant account</span></span>       |
| <span data-ttu-id="070be-177">name</span><span class="sxs-lookup"><span data-stu-id="070be-177">name</span></span>               | <span data-ttu-id="070be-178">sztring</span><span class="sxs-lookup"><span data-stu-id="070be-178">string</span></span>         | <span data-ttu-id="070be-179">A bérlő rövid neve</span><span class="sxs-lookup"><span data-stu-id="070be-179">Friendly name of the tenant</span></span>         |
| <span data-ttu-id="070be-180">displayName</span><span class="sxs-lookup"><span data-stu-id="070be-180">displayName</span></span>        | <span data-ttu-id="070be-181">sztring</span><span class="sxs-lookup"><span data-stu-id="070be-181">string</span></span>         | <span data-ttu-id="070be-182">A fiók megjelenítendő neve</span><span class="sxs-lookup"><span data-stu-id="070be-182">Display name for the account</span></span>        |
| <span data-ttu-id="070be-183">adminUserName</span><span class="sxs-lookup"><span data-stu-id="070be-183">adminUserName</span></span>      | <span data-ttu-id="070be-184">sztring</span><span class="sxs-lookup"><span data-stu-id="070be-184">string</span></span>         | <span data-ttu-id="070be-185">A bejelentkezéshez használt fiók felhasználóneve</span><span class="sxs-lookup"><span data-stu-id="070be-185">User name for the account for login</span></span> |
| <span data-ttu-id="070be-186">adminfirstname</span><span class="sxs-lookup"><span data-stu-id="070be-186">adminfirstname</span></span>     | <span data-ttu-id="070be-187">sztring</span><span class="sxs-lookup"><span data-stu-id="070be-187">string</span></span>         | <span data-ttu-id="070be-188">A rendszergazdai felhasználó vezetékneve</span><span class="sxs-lookup"><span data-stu-id="070be-188">First Name for the admin user</span></span>       |
| <span data-ttu-id="070be-189">adminlastname (rendszergazdailastname)</span><span class="sxs-lookup"><span data-stu-id="070be-189">adminlastname</span></span>      | <span data-ttu-id="070be-190">sztring</span><span class="sxs-lookup"><span data-stu-id="070be-190">string</span></span>         | <span data-ttu-id="070be-191">A rendszergazdai felhasználó vezetékneve</span><span class="sxs-lookup"><span data-stu-id="070be-191">Last Name for the admin user</span></span>        |
| <span data-ttu-id="070be-192">adminAle fiókemail</span><span class="sxs-lookup"><span data-stu-id="070be-192">adminAlernateEmail</span></span> | <span data-ttu-id="070be-193">sztring</span><span class="sxs-lookup"><span data-stu-id="070be-193">string</span></span>         | <span data-ttu-id="070be-194">e-mail a rendszergazdai felhasználónak</span><span class="sxs-lookup"><span data-stu-id="070be-194">email for the admin user</span></span>            |
| <span data-ttu-id="070be-195">ország</span><span class="sxs-lookup"><span data-stu-id="070be-195">country</span></span>            | <span data-ttu-id="070be-196">sztring</span><span class="sxs-lookup"><span data-stu-id="070be-196">string</span></span>         | <span data-ttu-id="070be-197">A fiók országa</span><span class="sxs-lookup"><span data-stu-id="070be-197">Country of the account</span></span>              |
| <span data-ttu-id="070be-198">Kultúra</span><span class="sxs-lookup"><span data-stu-id="070be-198">culture</span></span>            | <span data-ttu-id="070be-199">sztring</span><span class="sxs-lookup"><span data-stu-id="070be-199">string</span></span>         | <span data-ttu-id="070be-200">A fiók nyelvi beállítása</span><span class="sxs-lookup"><span data-stu-id="070be-200">Language preference for account</span></span>     |

<span data-ttu-id="070be-201">Ez a táblázat a **legalBusinessProfile attribútumban szükséges tulajdonságokat** ismerteti.</span><span class="sxs-lookup"><span data-stu-id="070be-201">This table describes the required properties in the **legalBusinessProfile** attribute.</span></span>

| <span data-ttu-id="070be-202">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="070be-202">Property</span></span>       | <span data-ttu-id="070be-203">Típus</span><span class="sxs-lookup"><span data-stu-id="070be-203">Type</span></span>                             | <span data-ttu-id="070be-204">Leírás</span><span class="sxs-lookup"><span data-stu-id="070be-204">Description</span></span>                          |
|----------------|----------------------------------|--------------------------------------|
| <span data-ttu-id="070be-205">companyName (vállalat neve)</span><span class="sxs-lookup"><span data-stu-id="070be-205">companyName</span></span>    | <span data-ttu-id="070be-206">sztring</span><span class="sxs-lookup"><span data-stu-id="070be-206">string</span></span>                           | <span data-ttu-id="070be-207">Jogi személy vállalatneve</span><span class="sxs-lookup"><span data-stu-id="070be-207">Company name for legal entity</span></span>        |
| <span data-ttu-id="070be-208">address</span><span class="sxs-lookup"><span data-stu-id="070be-208">address</span></span>        | <span data-ttu-id="070be-209">&lt;Szótárszavak, sztringek&gt;</span><span class="sxs-lookup"><span data-stu-id="070be-209">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="070be-210">A jogi személy helyének címe</span><span class="sxs-lookup"><span data-stu-id="070be-210">Address of the legal entity location</span></span> |
| <span data-ttu-id="070be-211">primaryContact (elsődleges tranzakció)</span><span class="sxs-lookup"><span data-stu-id="070be-211">primaryContact</span></span> | <span data-ttu-id="070be-212">&lt;Szótárszavak, sztringek&gt;</span><span class="sxs-lookup"><span data-stu-id="070be-212">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="070be-213">A vállalat kapcsolattartási adatai</span><span class="sxs-lookup"><span data-stu-id="070be-213">Contact details of the company</span></span>       |
| <span data-ttu-id="070be-214">Kultúra</span><span class="sxs-lookup"><span data-stu-id="070be-214">culture</span></span>        | <span data-ttu-id="070be-215">sztring</span><span class="sxs-lookup"><span data-stu-id="070be-215">string</span></span>                           | <span data-ttu-id="070be-216">A vállalat által előnyben részesített nyelv</span><span class="sxs-lookup"><span data-stu-id="070be-216">Language preferred by the company</span></span>    |

### <a name="request-example"></a><span data-ttu-id="070be-217">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="070be-217">Request Example</span></span>

```http
{
    "mpnId": "6363276",
    "tenant": {
        "domainPrefix": "TipIRIntTest705",
        "name": "TipIRIntTest705",
        "displayName": "TipIRIntTest705",
        "adminUserName": "admin",
        "adminFirstName": "TipIRIntTest705",
        "adminLastName": "TipIRIntTest705",
        "adminAlternateEmail": "TipIRIntTest705@test.com",
        "country": "US",
        "culture": "en-us"
    },
    "legalBusinessProfile": {
        "companyName": "TipIRIntTest705",
        "address": {
            "country": "FR",
            "city": "Issy-les-Moulineaux",
            "state": "",
            "addressLine1": "39-41 quai du Président Roosevelt",
            "addressLine2": "",
            "postalCode": "92130"
        },
        "primaryContact": {
            "firstName": "Sandbox",
            "lastName": "Scenario",
            "email": "Sandbox.Scenario@test.com",
            "phoneNumber": "1234567890"
        },
        "culture": "en-US"
    },
    "organizationProfileLanguage": "en"
}
```

### <a name="rest-response"></a><span data-ttu-id="070be-218">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="070be-218">REST response</span></span>

<span data-ttu-id="070be-219">Ha a művelet sikeres, ez a metódus visszaadja a sandbox ir-erőforrást a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="070be-219">If successful, this method returns the populated Sandbox IR resource in the response body.</span></span>

```http
{

    "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
    "mpnId": "6363276",
    "tenant": {
        "id": "6f94b119-793c-44c7-862b-c327c9057eab",
        "adminUserAccount": "admin@TipIRIntTest705.onmicrosoft.com",
        "password": "\*\*\*\*\*\*”
    },
    "agreementSignature": {
        "id": "30ac23e7-e200-42cf-a5bc-dd9148cdc632",
        "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
        "agreementId": "1e18c5b2-e42a-4b84-82c8-d0155aa94c6e",
        "agreementType": "ValueAddedReseller",
        "dateSigned": "2021-02-23T18:10:14.8461137Z",
        "signedByFirstName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserPrincipalName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserObjectId": "e6e0c29d-acda-4ef2-b370-d37a4e06fb98",
        "signedByUserTenantId": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "attributes": {
            "objectType": "AgreementSignatureResponse"
        }
    },
    "partnerRelationship": {
        "id": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "name": "PLAMUATT2NetNew",
        "relationshipType": "is\_indirect\_reseller\_of",
        "state": "Active",
        "mpnId": "6363276",
        "attributes": {
            "objectType": "PartnerRelationshipResponse"
        }
    }
}
```
