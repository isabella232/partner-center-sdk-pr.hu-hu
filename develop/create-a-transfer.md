---
title: Átvitel létrehozása
description: Előfizetések átvitelének létrehozása egy ügyfél számára.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d459a0a96912ab27f312bc73af16af2d4fdb518c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973706"
---
# <a name="create-a-transfer"></a><span data-ttu-id="d799d-103">Átvitel létrehozása</span><span class="sxs-lookup"><span data-stu-id="d799d-103">Create a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d799d-104">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d799d-104">Prerequisites</span></span>

- <span data-ttu-id="d799d-105">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d799d-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d799d-106">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="d799d-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d799d-107">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d799d-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d799d-108">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d799d-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d799d-109">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d799d-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d799d-110">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d799d-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d799d-111">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="d799d-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d799d-112">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d799d-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="d799d-113">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d799d-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d799d-114">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="d799d-114">Request syntax</span></span>

| <span data-ttu-id="d799d-115">Metódus</span><span class="sxs-lookup"><span data-stu-id="d799d-115">Method</span></span>   | <span data-ttu-id="d799d-116">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d799d-116">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d799d-117">**Post**</span><span class="sxs-lookup"><span data-stu-id="d799d-117">**POST**</span></span> | <span data-ttu-id="d799d-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/transfers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d799d-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="d799d-119">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d799d-119">URI parameter</span></span>

<span data-ttu-id="d799d-120">Az ügyfél azonosításához használja a következő elérésiút-paramétert.</span><span class="sxs-lookup"><span data-stu-id="d799d-120">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="d799d-121">Név</span><span class="sxs-lookup"><span data-stu-id="d799d-121">Name</span></span>            | <span data-ttu-id="d799d-122">Típus</span><span class="sxs-lookup"><span data-stu-id="d799d-122">Type</span></span>     | <span data-ttu-id="d799d-123">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d799d-123">Required</span></span> | <span data-ttu-id="d799d-124">Leírás</span><span class="sxs-lookup"><span data-stu-id="d799d-124">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="d799d-125">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="d799d-125">**customer-id**</span></span> | <span data-ttu-id="d799d-126">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-126">string</span></span>   | <span data-ttu-id="d799d-127">Igen</span><span class="sxs-lookup"><span data-stu-id="d799d-127">Yes</span></span>      | <span data-ttu-id="d799d-128">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="d799d-128">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="d799d-129">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d799d-129">Request headers</span></span>

<span data-ttu-id="d799d-130">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d799d-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d799d-131">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d799d-131">Request body</span></span>

<span data-ttu-id="d799d-132">Ez a táblázat a [kérés törzsében található TransferEntity](transfer-entity-resources.md) tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="d799d-132">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="d799d-133">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d799d-133">Property</span></span>              | <span data-ttu-id="d799d-134">Típus</span><span class="sxs-lookup"><span data-stu-id="d799d-134">Type</span></span>          | <span data-ttu-id="d799d-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d799d-135">Required</span></span>  | <span data-ttu-id="d799d-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="d799d-136">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="d799d-137">id</span><span class="sxs-lookup"><span data-stu-id="d799d-137">id</span></span>                    | <span data-ttu-id="d799d-138">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-138">string</span></span>        | <span data-ttu-id="d799d-139">No</span><span class="sxs-lookup"><span data-stu-id="d799d-139">No</span></span>    | <span data-ttu-id="d799d-140">A transferEntity sikeres létrehozása után megadott transferEntity azonosító.</span><span class="sxs-lookup"><span data-stu-id="d799d-140">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="d799d-141">createdTime (létrehozás ideje)</span><span class="sxs-lookup"><span data-stu-id="d799d-141">createdTime</span></span>           | <span data-ttu-id="d799d-142">DateTime</span><span class="sxs-lookup"><span data-stu-id="d799d-142">DateTime</span></span>      | <span data-ttu-id="d799d-143">Nem</span><span class="sxs-lookup"><span data-stu-id="d799d-143">No</span></span>    | <span data-ttu-id="d799d-144">A transferEntity létrejöttének dátuma dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="d799d-144">The date the transferEntity was created, in date-time format.</span></span> <span data-ttu-id="d799d-145">Alkalmazva a transferEntity sikeres létrehozásakor.</span><span class="sxs-lookup"><span data-stu-id="d799d-145">Applied upon successful creation of the transferEntity.</span></span>      |
| <span data-ttu-id="d799d-146">lastModifiedTime (lastModifiedTime)</span><span class="sxs-lookup"><span data-stu-id="d799d-146">lastModifiedTime</span></span>      | <span data-ttu-id="d799d-147">DateTime</span><span class="sxs-lookup"><span data-stu-id="d799d-147">DateTime</span></span>      | <span data-ttu-id="d799d-148">Nem</span><span class="sxs-lookup"><span data-stu-id="d799d-148">No</span></span>    | <span data-ttu-id="d799d-149">A transferEntity utolsó frissítésének dátuma dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="d799d-149">The date the transferEntity was last updated, in date-time format.</span></span> <span data-ttu-id="d799d-150">Alkalmazva a transferEntity sikeres létrehozásakor.</span><span class="sxs-lookup"><span data-stu-id="d799d-150">Applied upon successful creation of the transferEntity.</span></span> |
| <span data-ttu-id="d799d-151">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="d799d-151">lastModifiedUser</span></span>      | <span data-ttu-id="d799d-152">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-152">string</span></span>        | <span data-ttu-id="d799d-153">No</span><span class="sxs-lookup"><span data-stu-id="d799d-153">No</span></span>    | <span data-ttu-id="d799d-154">Az a felhasználó, aki utoljára frissítette a transferEntity adatokat.</span><span class="sxs-lookup"><span data-stu-id="d799d-154">The user who last updated the transferEntity.</span></span> <span data-ttu-id="d799d-155">Alkalmazva a transferEntity sikeres létrehozásakor.</span><span class="sxs-lookup"><span data-stu-id="d799d-155">Applied upon successful creation of transferEntity.</span></span>                          |
| <span data-ttu-id="d799d-156">customerName (ügyfél neve)</span><span class="sxs-lookup"><span data-stu-id="d799d-156">customerName</span></span>          | <span data-ttu-id="d799d-157">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-157">string</span></span>        | <span data-ttu-id="d799d-158">No</span><span class="sxs-lookup"><span data-stu-id="d799d-158">No</span></span>    | <span data-ttu-id="d799d-159">Választható.</span><span class="sxs-lookup"><span data-stu-id="d799d-159">Optional.</span></span> <span data-ttu-id="d799d-160">Annak az ügyfélnek a neve, akinek az előfizetései átadása folyamatban van.</span><span class="sxs-lookup"><span data-stu-id="d799d-160">The name of the customer whose subscriptions are being transferred.</span></span>                                              |
| <span data-ttu-id="d799d-161">customerTenantId (customerTenantId)</span><span class="sxs-lookup"><span data-stu-id="d799d-161">customerTenantId</span></span>      | <span data-ttu-id="d799d-162">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-162">string</span></span>        | <span data-ttu-id="d799d-163">No</span><span class="sxs-lookup"><span data-stu-id="d799d-163">No</span></span>    | <span data-ttu-id="d799d-164">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="d799d-164">A GUID formatted customer-id that identifies the customer.</span></span> <span data-ttu-id="d799d-165">Alkalmazva a transferEntity sikeres létrehozásakor.</span><span class="sxs-lookup"><span data-stu-id="d799d-165">Applied upon successful creation of the transferEntity.</span></span>         |
| <span data-ttu-id="d799d-166">partnertenantid</span><span class="sxs-lookup"><span data-stu-id="d799d-166">partnertenantid</span></span>       | <span data-ttu-id="d799d-167">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-167">string</span></span>        | <span data-ttu-id="d799d-168">No</span><span class="sxs-lookup"><span data-stu-id="d799d-168">No</span></span>    | <span data-ttu-id="d799d-169">Egy GUID formátumú partnerazonosító, amely azonosítja a partnert.</span><span class="sxs-lookup"><span data-stu-id="d799d-169">A GUID formatted partner-id that identifies the partner.</span></span>                                                                   |
| <span data-ttu-id="d799d-170">sourcePartnerName (forráspartner neve)</span><span class="sxs-lookup"><span data-stu-id="d799d-170">sourcePartnerName</span></span>     | <span data-ttu-id="d799d-171">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-171">string</span></span>        | <span data-ttu-id="d799d-172">No</span><span class="sxs-lookup"><span data-stu-id="d799d-172">No</span></span>    | <span data-ttu-id="d799d-173">Választható.</span><span class="sxs-lookup"><span data-stu-id="d799d-173">Optional.</span></span> <span data-ttu-id="d799d-174">Az átadást kezdeményező partnerszervezet neve.</span><span class="sxs-lookup"><span data-stu-id="d799d-174">The name of the partner's organization who is initiating the transfer.</span></span>                                           |
| <span data-ttu-id="d799d-175">sourcePartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="d799d-175">sourcePartnerTenantId</span></span> | <span data-ttu-id="d799d-176">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-176">string</span></span>        | <span data-ttu-id="d799d-177">Igen</span><span class="sxs-lookup"><span data-stu-id="d799d-177">Yes</span></span>   | <span data-ttu-id="d799d-178">Egy GUID formátumú partnerazonosító, amely azonosítja az átadást kezdeményező partnert.</span><span class="sxs-lookup"><span data-stu-id="d799d-178">A GUID formatted partner-id that identifies the partner initiating the transfer.</span></span>                                           |
| <span data-ttu-id="d799d-179">targetPartnerName</span><span class="sxs-lookup"><span data-stu-id="d799d-179">targetPartnerName</span></span>     | <span data-ttu-id="d799d-180">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-180">string</span></span>        | <span data-ttu-id="d799d-181">No</span><span class="sxs-lookup"><span data-stu-id="d799d-181">No</span></span>    | <span data-ttu-id="d799d-182">Választható.</span><span class="sxs-lookup"><span data-stu-id="d799d-182">Optional.</span></span> <span data-ttu-id="d799d-183">Annak a partnernek a neve, amely számára az átvitel megcélzott.</span><span class="sxs-lookup"><span data-stu-id="d799d-183">The name of the partner's organization to whom the transfer is targeted.</span></span>                                         |
| <span data-ttu-id="d799d-184">targetPartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="d799d-184">targetPartnerTenantId</span></span> | <span data-ttu-id="d799d-185">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-185">string</span></span>        | <span data-ttu-id="d799d-186">Igen</span><span class="sxs-lookup"><span data-stu-id="d799d-186">Yes</span></span>   | <span data-ttu-id="d799d-187">Egy GUID formátumú partnerazonosító, amely azonosítja azt a partnert, akinek az átadást megcéloznia kell.</span><span class="sxs-lookup"><span data-stu-id="d799d-187">A GUID formatted partner-id that identifies the partner to whom the transfer is targeted.</span></span>                                  |
| <span data-ttu-id="d799d-188">lineItems (sorsorok)</span><span class="sxs-lookup"><span data-stu-id="d799d-188">lineItems</span></span>             | <span data-ttu-id="d799d-189">Objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="d799d-189">Array of objects</span></span> | <span data-ttu-id="d799d-190">Igen</span><span class="sxs-lookup"><span data-stu-id="d799d-190">Yes</span></span>| <span data-ttu-id="d799d-191">[TransferLineItem-erőforrások tömbje.](transfer-entity-resources.md#transferlineitem)</span><span class="sxs-lookup"><span data-stu-id="d799d-191">An Array of [TransferLineItem](transfer-entity-resources.md#transferlineitem) resources.</span></span>                                   |
| <span data-ttu-id="d799d-192">status</span><span class="sxs-lookup"><span data-stu-id="d799d-192">status</span></span>                | <span data-ttu-id="d799d-193">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-193">string</span></span>        | <span data-ttu-id="d799d-194">No</span><span class="sxs-lookup"><span data-stu-id="d799d-194">No</span></span>    | <span data-ttu-id="d799d-195">A transferEntity állapota.</span><span class="sxs-lookup"><span data-stu-id="d799d-195">The status of the transferEntity.</span></span> <span data-ttu-id="d799d-196">Lehetséges értékek: "Aktív" (törölhető/elküldve) és "Befejezve" (már befejeződött).</span><span class="sxs-lookup"><span data-stu-id="d799d-196">Possible values are "Active" (can be deleted/submitted) and "Completed" (has already been completed).</span></span> <span data-ttu-id="d799d-197">Alkalmazva a transferEntity sikeres létrehozásakor.</span><span class="sxs-lookup"><span data-stu-id="d799d-197">Applied upon successful creation of the transferEntity.</span></span>|

<span data-ttu-id="d799d-198">Ez a táblázat a kérés törzsében található [TransferLineItem](transfer-entity-resources.md#transferlineitem) tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="d799d-198">This table describes the [TransferLineItem](transfer-entity-resources.md#transferlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="d799d-199">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d799d-199">Property</span></span>       |            <span data-ttu-id="d799d-200">Típus</span><span class="sxs-lookup"><span data-stu-id="d799d-200">Type</span></span>             | <span data-ttu-id="d799d-201">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d799d-201">Required</span></span> | <span data-ttu-id="d799d-202">Leírás</span><span class="sxs-lookup"><span data-stu-id="d799d-202">Description</span></span>                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d799d-203">id</span><span class="sxs-lookup"><span data-stu-id="d799d-203">id</span></span>                   | <span data-ttu-id="d799d-204">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-204">string</span></span>                     | <span data-ttu-id="d799d-205">No</span><span class="sxs-lookup"><span data-stu-id="d799d-205">No</span></span>       | <span data-ttu-id="d799d-206">Egy átvitelisor-elem egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="d799d-206">A unique identifier for a transfer line item.</span></span> <span data-ttu-id="d799d-207">Alkalmazva a transferEntity sikeres létrehozásakor.</span><span class="sxs-lookup"><span data-stu-id="d799d-207">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="d799d-208">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="d799d-208">subscriptionId</span></span>       | <span data-ttu-id="d799d-209">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-209">string</span></span>                     | <span data-ttu-id="d799d-210">Igen</span><span class="sxs-lookup"><span data-stu-id="d799d-210">Yes</span></span>      | <span data-ttu-id="d799d-211">Az előfizetés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="d799d-211">The subscription identifier.</span></span>                                                                         |
| <span data-ttu-id="d799d-212">quantity</span><span class="sxs-lookup"><span data-stu-id="d799d-212">quantity</span></span>             | <span data-ttu-id="d799d-213">int</span><span class="sxs-lookup"><span data-stu-id="d799d-213">int</span></span>                        | <span data-ttu-id="d799d-214">Nem</span><span class="sxs-lookup"><span data-stu-id="d799d-214">No</span></span>       | <span data-ttu-id="d799d-215">A licencek vagy példányok száma.</span><span class="sxs-lookup"><span data-stu-id="d799d-215">The number of licenses or instances.</span></span>                                                                 |
| <span data-ttu-id="d799d-216">billingCycle</span><span class="sxs-lookup"><span data-stu-id="d799d-216">billingCycle</span></span>         | <span data-ttu-id="d799d-217">Objektum</span><span class="sxs-lookup"><span data-stu-id="d799d-217">Object</span></span>                     | <span data-ttu-id="d799d-218">Nem</span><span class="sxs-lookup"><span data-stu-id="d799d-218">No</span></span>       | <span data-ttu-id="d799d-219">Az aktuális időszakhoz beállított számlázási ciklus típusa.</span><span class="sxs-lookup"><span data-stu-id="d799d-219">The type of billing cycle set for the current period.</span></span>                                                |
| <span data-ttu-id="d799d-220">friendlyName (rövid név)</span><span class="sxs-lookup"><span data-stu-id="d799d-220">friendlyName</span></span>         | <span data-ttu-id="d799d-221">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-221">string</span></span>                     | <span data-ttu-id="d799d-222">No</span><span class="sxs-lookup"><span data-stu-id="d799d-222">No</span></span>       | <span data-ttu-id="d799d-223">Választható.</span><span class="sxs-lookup"><span data-stu-id="d799d-223">Optional.</span></span> <span data-ttu-id="d799d-224">A partner által definiált elem rövid neve, amely segít egyértelműsedni.</span><span class="sxs-lookup"><span data-stu-id="d799d-224">The friendly name for the item defined by the partner to help disambiguate.</span></span>                |
| <span data-ttu-id="d799d-225">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="d799d-225">partnerIdOnRecord</span></span>    | <span data-ttu-id="d799d-226">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-226">string</span></span>                     | <span data-ttu-id="d799d-227">No</span><span class="sxs-lookup"><span data-stu-id="d799d-227">No</span></span>       | <span data-ttu-id="d799d-228">PartnerAzonosító a rekordban (MPN-azonosító) a vásárláskor, amikor az átadást elfogadják.</span><span class="sxs-lookup"><span data-stu-id="d799d-228">PartnerId on Record (MPN ID) on the purchase that happens when the transfer is accepted.</span></span>              |
| <span data-ttu-id="d799d-229">offerId (ajánlatazonosító)</span><span class="sxs-lookup"><span data-stu-id="d799d-229">offerId</span></span>              | <span data-ttu-id="d799d-230">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-230">string</span></span>                     | <span data-ttu-id="d799d-231">No</span><span class="sxs-lookup"><span data-stu-id="d799d-231">No</span></span>       | <span data-ttu-id="d799d-232">Az ajánlat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="d799d-232">The offer identifier.</span></span>                                                                                |
| <span data-ttu-id="d799d-233">addonItems (bővítmények)</span><span class="sxs-lookup"><span data-stu-id="d799d-233">addonItems</span></span>           | <span data-ttu-id="d799d-234">**TransferLineItem-objektumok** listája</span><span class="sxs-lookup"><span data-stu-id="d799d-234">List of **TransferLineItem** objects</span></span> | <span data-ttu-id="d799d-235">Nem</span><span class="sxs-lookup"><span data-stu-id="d799d-235">No</span></span> | <span data-ttu-id="d799d-236">TransferEntity sorelemek gyűjteménye bővítményekhez, amelyek át lesznek adva az átvitt alap előfizetéssel együtt.</span><span class="sxs-lookup"><span data-stu-id="d799d-236">A collection of transferEntity line items for addons that will be transferred along with the base subscription that is being transferred.</span></span> <span data-ttu-id="d799d-237">Alkalmazva a transferEntity sikeres létrehozásakor.</span><span class="sxs-lookup"><span data-stu-id="d799d-237">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="d799d-238">transferError</span><span class="sxs-lookup"><span data-stu-id="d799d-238">transferError</span></span>        | <span data-ttu-id="d799d-239">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-239">string</span></span>                     | <span data-ttu-id="d799d-240">No</span><span class="sxs-lookup"><span data-stu-id="d799d-240">No</span></span>       | <span data-ttu-id="d799d-241">A transferEntity után lesz alkalmazva, ha hiba történik.</span><span class="sxs-lookup"><span data-stu-id="d799d-241">Applied after transferEntity is accepted if there is an error.</span></span>                                        |
| <span data-ttu-id="d799d-242">status</span><span class="sxs-lookup"><span data-stu-id="d799d-242">status</span></span>               | <span data-ttu-id="d799d-243">sztring</span><span class="sxs-lookup"><span data-stu-id="d799d-243">string</span></span>                     | <span data-ttu-id="d799d-244">No</span><span class="sxs-lookup"><span data-stu-id="d799d-244">No</span></span>       | <span data-ttu-id="d799d-245">A sortem állapota a transferEntity oszlopban.</span><span class="sxs-lookup"><span data-stu-id="d799d-245">The status of the lineitem in the transferEntity.</span></span>                                                    |

### <a name="request-example"></a><span data-ttu-id="d799d-246">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d799d-246">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="d799d-247">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d799d-247">REST response</span></span>

<span data-ttu-id="d799d-248">Ha a művelet sikeres, ez a metódus visszaadja a válasz törzsében a megadott [TransferEnity](transfer-entity-resources.md) erőforrást.</span><span class="sxs-lookup"><span data-stu-id="d799d-248">If successful, this method returns the populated [TransferEnity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d799d-249">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d799d-249">Response success and error codes</span></span>

<span data-ttu-id="d799d-250">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d799d-250">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d799d-251">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d799d-251">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d799d-252">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d799d-252">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d799d-253">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d799d-253">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
