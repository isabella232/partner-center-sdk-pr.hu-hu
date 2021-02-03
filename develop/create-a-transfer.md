---
title: Átvitel létrehozása
description: Előfizetések átvitelének létrehozása az ügyfelek számára.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5e70cc5b7ce4fcfa715f581a2151f0b8d1922b0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767760"
---
# <a name="create-a-transfer"></a><span data-ttu-id="abe3a-103">Átvitel létrehozása</span><span class="sxs-lookup"><span data-stu-id="abe3a-103">Create a transfer</span></span>

<span data-ttu-id="abe3a-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="abe3a-104">**Applies to:**</span></span>

- <span data-ttu-id="abe3a-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="abe3a-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abe3a-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="abe3a-106">Prerequisites</span></span>

- <span data-ttu-id="abe3a-107">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="abe3a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="abe3a-108">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="abe3a-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="abe3a-109">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="abe3a-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="abe3a-110">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="abe3a-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="abe3a-111">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="abe3a-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="abe3a-112">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="abe3a-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="abe3a-113">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="abe3a-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="abe3a-114">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="abe3a-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="abe3a-115">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="abe3a-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="abe3a-116">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="abe3a-116">Request syntax</span></span>

| <span data-ttu-id="abe3a-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="abe3a-117">Method</span></span>   | <span data-ttu-id="abe3a-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="abe3a-118">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="abe3a-119">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="abe3a-119">**POST**</span></span> | <span data-ttu-id="abe3a-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Transfers http/1.1</span><span class="sxs-lookup"><span data-stu-id="abe3a-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="abe3a-121">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="abe3a-121">URI parameter</span></span>

<span data-ttu-id="abe3a-122">Az ügyfél azonosításához használja a következő Path paramétert.</span><span class="sxs-lookup"><span data-stu-id="abe3a-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="abe3a-123">Név</span><span class="sxs-lookup"><span data-stu-id="abe3a-123">Name</span></span>            | <span data-ttu-id="abe3a-124">Típus</span><span class="sxs-lookup"><span data-stu-id="abe3a-124">Type</span></span>     | <span data-ttu-id="abe3a-125">Kötelező</span><span class="sxs-lookup"><span data-stu-id="abe3a-125">Required</span></span> | <span data-ttu-id="abe3a-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="abe3a-126">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="abe3a-127">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="abe3a-127">**customer-id**</span></span> | <span data-ttu-id="abe3a-128">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-128">string</span></span>   | <span data-ttu-id="abe3a-129">Igen</span><span class="sxs-lookup"><span data-stu-id="abe3a-129">Yes</span></span>      | <span data-ttu-id="abe3a-130">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="abe3a-130">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="abe3a-131">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="abe3a-131">Request headers</span></span>

<span data-ttu-id="abe3a-132">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="abe3a-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="abe3a-133">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="abe3a-133">Request body</span></span>

<span data-ttu-id="abe3a-134">Ez a táblázat a kérelem törzsének [TransferEntity](transfer-entity-resources.md) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="abe3a-134">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="abe3a-135">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="abe3a-135">Property</span></span>              | <span data-ttu-id="abe3a-136">Típus</span><span class="sxs-lookup"><span data-stu-id="abe3a-136">Type</span></span>          | <span data-ttu-id="abe3a-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="abe3a-137">Required</span></span>  | <span data-ttu-id="abe3a-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="abe3a-138">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="abe3a-139">id</span><span class="sxs-lookup"><span data-stu-id="abe3a-139">id</span></span>                    | <span data-ttu-id="abe3a-140">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-140">string</span></span>        | <span data-ttu-id="abe3a-141">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-141">No</span></span>    | <span data-ttu-id="abe3a-142">A transferEntity sikeres létrehozásakor megadott transferEntity-azonosító.</span><span class="sxs-lookup"><span data-stu-id="abe3a-142">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="abe3a-143">createdTime</span><span class="sxs-lookup"><span data-stu-id="abe3a-143">createdTime</span></span>           | <span data-ttu-id="abe3a-144">DateTime</span><span class="sxs-lookup"><span data-stu-id="abe3a-144">DateTime</span></span>      | <span data-ttu-id="abe3a-145">Nem</span><span class="sxs-lookup"><span data-stu-id="abe3a-145">No</span></span>    | <span data-ttu-id="abe3a-146">A transferEntity létrehozásának dátuma dátum és idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="abe3a-146">The date the transferEntity was created, in date-time format.</span></span> <span data-ttu-id="abe3a-147">A transferEntity sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="abe3a-147">Applied upon successful creation of the transferEntity.</span></span>      |
| <span data-ttu-id="abe3a-148">lastModifiedTime</span><span class="sxs-lookup"><span data-stu-id="abe3a-148">lastModifiedTime</span></span>      | <span data-ttu-id="abe3a-149">DateTime</span><span class="sxs-lookup"><span data-stu-id="abe3a-149">DateTime</span></span>      | <span data-ttu-id="abe3a-150">Nem</span><span class="sxs-lookup"><span data-stu-id="abe3a-150">No</span></span>    | <span data-ttu-id="abe3a-151">A transferEntity utolsó frissítésének dátuma, dátum-idő formátumban.</span><span class="sxs-lookup"><span data-stu-id="abe3a-151">The date the transferEntity was last updated, in date-time format.</span></span> <span data-ttu-id="abe3a-152">A transferEntity sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="abe3a-152">Applied upon successful creation of the transferEntity.</span></span> |
| <span data-ttu-id="abe3a-153">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="abe3a-153">lastModifiedUser</span></span>      | <span data-ttu-id="abe3a-154">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-154">string</span></span>        | <span data-ttu-id="abe3a-155">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-155">No</span></span>    | <span data-ttu-id="abe3a-156">Az a felhasználó, aki utoljára frissítette a transferEntity.</span><span class="sxs-lookup"><span data-stu-id="abe3a-156">The user who last updated the transferEntity.</span></span> <span data-ttu-id="abe3a-157">A transferEntity sikeres létrehozásakor lett alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="abe3a-157">Applied upon successful creation of transferEntity.</span></span>                          |
| <span data-ttu-id="abe3a-158">Customername (</span><span class="sxs-lookup"><span data-stu-id="abe3a-158">customerName</span></span>          | <span data-ttu-id="abe3a-159">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-159">string</span></span>        | <span data-ttu-id="abe3a-160">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-160">No</span></span>    | <span data-ttu-id="abe3a-161">Választható.</span><span class="sxs-lookup"><span data-stu-id="abe3a-161">Optional.</span></span> <span data-ttu-id="abe3a-162">Annak az ügyfélnek a neve, amelynek előfizetéseit át kell vinni.</span><span class="sxs-lookup"><span data-stu-id="abe3a-162">The name of the customer whose subscriptions are being transferred.</span></span>                                              |
| <span data-ttu-id="abe3a-163">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="abe3a-163">customerTenantId</span></span>      | <span data-ttu-id="abe3a-164">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-164">string</span></span>        | <span data-ttu-id="abe3a-165">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-165">No</span></span>    | <span data-ttu-id="abe3a-166">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="abe3a-166">A GUID formatted customer-id that identifies the customer.</span></span> <span data-ttu-id="abe3a-167">A transferEntity sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="abe3a-167">Applied upon successful creation of the transferEntity.</span></span>         |
| <span data-ttu-id="abe3a-168">partnertenantid</span><span class="sxs-lookup"><span data-stu-id="abe3a-168">partnertenantid</span></span>       | <span data-ttu-id="abe3a-169">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-169">string</span></span>        | <span data-ttu-id="abe3a-170">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-170">No</span></span>    | <span data-ttu-id="abe3a-171">Egy GUID formátumú partner-azonosító, amely azonosítja a partnert.</span><span class="sxs-lookup"><span data-stu-id="abe3a-171">A GUID formatted partner-id that identifies the partner.</span></span>                                                                   |
| <span data-ttu-id="abe3a-172">sourcePartnerName</span><span class="sxs-lookup"><span data-stu-id="abe3a-172">sourcePartnerName</span></span>     | <span data-ttu-id="abe3a-173">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-173">string</span></span>        | <span data-ttu-id="abe3a-174">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-174">No</span></span>    | <span data-ttu-id="abe3a-175">Választható.</span><span class="sxs-lookup"><span data-stu-id="abe3a-175">Optional.</span></span> <span data-ttu-id="abe3a-176">A partner azon szervezetének neve, aki kezdeményezi az átvitelt.</span><span class="sxs-lookup"><span data-stu-id="abe3a-176">The name of the partner's organization who is initiating the transfer.</span></span>                                           |
| <span data-ttu-id="abe3a-177">sourcePartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="abe3a-177">sourcePartnerTenantId</span></span> | <span data-ttu-id="abe3a-178">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-178">string</span></span>        | <span data-ttu-id="abe3a-179">Igen</span><span class="sxs-lookup"><span data-stu-id="abe3a-179">Yes</span></span>   | <span data-ttu-id="abe3a-180">Egy GUID formátumú partner-azonosító, amely azonosítja az átvitelt kezdeményező partnert.</span><span class="sxs-lookup"><span data-stu-id="abe3a-180">A GUID formatted partner-id that identifies the partner initiating the transfer.</span></span>                                           |
| <span data-ttu-id="abe3a-181">targetPartnerName</span><span class="sxs-lookup"><span data-stu-id="abe3a-181">targetPartnerName</span></span>     | <span data-ttu-id="abe3a-182">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-182">string</span></span>        | <span data-ttu-id="abe3a-183">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-183">No</span></span>    | <span data-ttu-id="abe3a-184">Választható.</span><span class="sxs-lookup"><span data-stu-id="abe3a-184">Optional.</span></span> <span data-ttu-id="abe3a-185">A partner azon szervezetének neve, amelyhez az átvitel irányul.</span><span class="sxs-lookup"><span data-stu-id="abe3a-185">The name of the partner's organization to whom the transfer is targeted.</span></span>                                         |
| <span data-ttu-id="abe3a-186">targetPartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="abe3a-186">targetPartnerTenantId</span></span> | <span data-ttu-id="abe3a-187">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-187">string</span></span>        | <span data-ttu-id="abe3a-188">Igen</span><span class="sxs-lookup"><span data-stu-id="abe3a-188">Yes</span></span>   | <span data-ttu-id="abe3a-189">Egy GUID formátumú partner-azonosító, amely azonosítja azt a partnert, akire az átvitel irányul.</span><span class="sxs-lookup"><span data-stu-id="abe3a-189">A GUID formatted partner-id that identifies the partner to whom the transfer is targeted.</span></span>                                  |
| <span data-ttu-id="abe3a-190">Listaelemek</span><span class="sxs-lookup"><span data-stu-id="abe3a-190">lineItems</span></span>             | <span data-ttu-id="abe3a-191">Objektumok tömbje</span><span class="sxs-lookup"><span data-stu-id="abe3a-191">Array of objects</span></span> | <span data-ttu-id="abe3a-192">Igen</span><span class="sxs-lookup"><span data-stu-id="abe3a-192">Yes</span></span>| <span data-ttu-id="abe3a-193">[TransferLineItem](transfer-entity-resources.md#transferlineitem) -erőforrások tömbje.</span><span class="sxs-lookup"><span data-stu-id="abe3a-193">An Array of [TransferLineItem](transfer-entity-resources.md#transferlineitem) resources.</span></span>                                   |
| <span data-ttu-id="abe3a-194">status</span><span class="sxs-lookup"><span data-stu-id="abe3a-194">status</span></span>                | <span data-ttu-id="abe3a-195">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-195">string</span></span>        | <span data-ttu-id="abe3a-196">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-196">No</span></span>    | <span data-ttu-id="abe3a-197">A transferEntity állapota.</span><span class="sxs-lookup"><span data-stu-id="abe3a-197">The status of the transferEntity.</span></span> <span data-ttu-id="abe3a-198">A lehetséges értékek: "Active" (törölhető/elküldhető) és "befejezett" (már befejeződött).</span><span class="sxs-lookup"><span data-stu-id="abe3a-198">Possible values are "Active" (can be deleted/submitted) and "Completed" (has already been completed).</span></span> <span data-ttu-id="abe3a-199">A transferEntity sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="abe3a-199">Applied upon successful creation of the transferEntity.</span></span>|

<span data-ttu-id="abe3a-200">Ez a táblázat a kérelem törzsének [TransferLineItem](transfer-entity-resources.md#transferlineitem) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="abe3a-200">This table describes the [TransferLineItem](transfer-entity-resources.md#transferlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="abe3a-201">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="abe3a-201">Property</span></span>       |            <span data-ttu-id="abe3a-202">Típus</span><span class="sxs-lookup"><span data-stu-id="abe3a-202">Type</span></span>             | <span data-ttu-id="abe3a-203">Kötelező</span><span class="sxs-lookup"><span data-stu-id="abe3a-203">Required</span></span> | <span data-ttu-id="abe3a-204">Leírás</span><span class="sxs-lookup"><span data-stu-id="abe3a-204">Description</span></span>                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="abe3a-205">id</span><span class="sxs-lookup"><span data-stu-id="abe3a-205">id</span></span>                   | <span data-ttu-id="abe3a-206">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-206">string</span></span>                     | <span data-ttu-id="abe3a-207">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-207">No</span></span>       | <span data-ttu-id="abe3a-208">Egy adatátviteli sorhoz tartozó egyedi azonosító.</span><span class="sxs-lookup"><span data-stu-id="abe3a-208">A unique identifier for a transfer line item.</span></span> <span data-ttu-id="abe3a-209">A transferEntity sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="abe3a-209">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="abe3a-210">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="abe3a-210">subscriptionId</span></span>       | <span data-ttu-id="abe3a-211">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-211">string</span></span>                     | <span data-ttu-id="abe3a-212">Igen</span><span class="sxs-lookup"><span data-stu-id="abe3a-212">Yes</span></span>      | <span data-ttu-id="abe3a-213">Az előfizetés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="abe3a-213">The subscription identifier.</span></span>                                                                         |
| <span data-ttu-id="abe3a-214">quantity</span><span class="sxs-lookup"><span data-stu-id="abe3a-214">quantity</span></span>             | <span data-ttu-id="abe3a-215">int</span><span class="sxs-lookup"><span data-stu-id="abe3a-215">int</span></span>                        | <span data-ttu-id="abe3a-216">Nem</span><span class="sxs-lookup"><span data-stu-id="abe3a-216">No</span></span>       | <span data-ttu-id="abe3a-217">A licencek vagy példányok száma.</span><span class="sxs-lookup"><span data-stu-id="abe3a-217">The number of licenses or instances.</span></span>                                                                 |
| <span data-ttu-id="abe3a-218">billingCycle</span><span class="sxs-lookup"><span data-stu-id="abe3a-218">billingCycle</span></span>         | <span data-ttu-id="abe3a-219">Objektum</span><span class="sxs-lookup"><span data-stu-id="abe3a-219">Object</span></span>                     | <span data-ttu-id="abe3a-220">Nem</span><span class="sxs-lookup"><span data-stu-id="abe3a-220">No</span></span>       | <span data-ttu-id="abe3a-221">Az aktuális időszakban beállított számlázási ciklus típusa.</span><span class="sxs-lookup"><span data-stu-id="abe3a-221">The type of billing cycle set for the current period.</span></span>                                                |
| <span data-ttu-id="abe3a-222">friendlyName</span><span class="sxs-lookup"><span data-stu-id="abe3a-222">friendlyName</span></span>         | <span data-ttu-id="abe3a-223">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-223">string</span></span>                     | <span data-ttu-id="abe3a-224">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-224">No</span></span>       | <span data-ttu-id="abe3a-225">Választható.</span><span class="sxs-lookup"><span data-stu-id="abe3a-225">Optional.</span></span> <span data-ttu-id="abe3a-226">A partner által a egyértelműsítse segítségére meghatározott rövid név.</span><span class="sxs-lookup"><span data-stu-id="abe3a-226">The friendly name for the item defined by the partner to help disambiguate.</span></span>                |
| <span data-ttu-id="abe3a-227">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="abe3a-227">partnerIdOnRecord</span></span>    | <span data-ttu-id="abe3a-228">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-228">string</span></span>                     | <span data-ttu-id="abe3a-229">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-229">No</span></span>       | <span data-ttu-id="abe3a-230">A PartnerId on Record (MPNID) azon a vásárláson, amely az átvitel elfogadásakor történik.</span><span class="sxs-lookup"><span data-stu-id="abe3a-230">PartnerId on Record (MPNID) on the purchase that happens when the transfer is accepted.</span></span>              |
| <span data-ttu-id="abe3a-231">offerId</span><span class="sxs-lookup"><span data-stu-id="abe3a-231">offerId</span></span>              | <span data-ttu-id="abe3a-232">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-232">string</span></span>                     | <span data-ttu-id="abe3a-233">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-233">No</span></span>       | <span data-ttu-id="abe3a-234">Az ajánlat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="abe3a-234">The offer identifier.</span></span>                                                                                |
| <span data-ttu-id="abe3a-235">addonItems</span><span class="sxs-lookup"><span data-stu-id="abe3a-235">addonItems</span></span>           | <span data-ttu-id="abe3a-236">**TransferLineItem** -objektumok listája</span><span class="sxs-lookup"><span data-stu-id="abe3a-236">List of **TransferLineItem** objects</span></span> | <span data-ttu-id="abe3a-237">Nem</span><span class="sxs-lookup"><span data-stu-id="abe3a-237">No</span></span> | <span data-ttu-id="abe3a-238">Olyan transferEntity-elemek gyűjteménye, amelyek az átvitt alap előfizetéssel együtt lesznek átadva.</span><span class="sxs-lookup"><span data-stu-id="abe3a-238">A collection of transferEntity line items for addons that will be transferred along with the base subscription that is being transferred.</span></span> <span data-ttu-id="abe3a-239">A transferEntity sikeres létrehozása után alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="abe3a-239">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="abe3a-240">transferError</span><span class="sxs-lookup"><span data-stu-id="abe3a-240">transferError</span></span>        | <span data-ttu-id="abe3a-241">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-241">string</span></span>                     | <span data-ttu-id="abe3a-242">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-242">No</span></span>       | <span data-ttu-id="abe3a-243">A transferEntity elfogadását követően alkalmazva hiba esetén.</span><span class="sxs-lookup"><span data-stu-id="abe3a-243">Applied after transferEntity is accepted in case of an error.</span></span>                                        |
| <span data-ttu-id="abe3a-244">status</span><span class="sxs-lookup"><span data-stu-id="abe3a-244">status</span></span>               | <span data-ttu-id="abe3a-245">sztring</span><span class="sxs-lookup"><span data-stu-id="abe3a-245">string</span></span>                     | <span data-ttu-id="abe3a-246">No</span><span class="sxs-lookup"><span data-stu-id="abe3a-246">No</span></span>       | <span data-ttu-id="abe3a-247">A lineitem állapota a transferEntity.</span><span class="sxs-lookup"><span data-stu-id="abe3a-247">The status of the lineitem in the transferEntity.</span></span>                                                    |

### <a name="request-example"></a><span data-ttu-id="abe3a-248">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="abe3a-248">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="abe3a-249">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="abe3a-249">REST response</span></span>

<span data-ttu-id="abe3a-250">Ha ez sikeres, ez a metódus a válasz törzsében lévő [TransferEnity](transfer-entity-resources.md) -erőforrást adja vissza.</span><span class="sxs-lookup"><span data-stu-id="abe3a-250">If successful, this method returns the populated [TransferEnity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="abe3a-251">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="abe3a-251">Response success and error codes</span></span>

<span data-ttu-id="abe3a-252">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="abe3a-252">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="abe3a-253">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="abe3a-253">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="abe3a-254">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="abe3a-254">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="abe3a-255">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="abe3a-255">Response example</span></span>

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
