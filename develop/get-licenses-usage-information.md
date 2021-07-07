---
title: Licencek használati adatainak lekérése
description: Licenchasználati információk lekérte a számítási feladatok szintjén a Office Dynamics szolgáltatáshoz.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea3658089ce7eb5c1ad7cc65c3db34f9b6353cdd
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445977"
---
# <a name="get-licenses-usage-information"></a><span data-ttu-id="5aeac-103">Licencek használati adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="5aeac-103">Get licenses usage information</span></span>

<span data-ttu-id="5aeac-104">Licenchasználati információk lekérte a számítási feladatok szintjén a Office Dynamics szolgáltatáshoz.</span><span class="sxs-lookup"><span data-stu-id="5aeac-104">How to get licenses usage information at the workload level for Office and Dynamics.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5aeac-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5aeac-105">Prerequisites</span></span>

<span data-ttu-id="5aeac-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5aeac-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5aeac-107">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="5aeac-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="5aeac-108">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="5aeac-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5aeac-109">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5aeac-109">Request syntax</span></span>

| <span data-ttu-id="5aeac-110">Metódus</span><span class="sxs-lookup"><span data-stu-id="5aeac-110">Method</span></span>  | <span data-ttu-id="5aeac-111">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5aeac-111">Request URI</span></span>                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="5aeac-112">**Kap**</span><span class="sxs-lookup"><span data-stu-id="5aeac-112">**GET**</span></span> | <span data-ttu-id="5aeac-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5aeac-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5aeac-114">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5aeac-114">Request headers</span></span>

<span data-ttu-id="5aeac-115">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5aeac-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="5aeac-116">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="5aeac-116">URI parameters</span></span>

| <span data-ttu-id="5aeac-117">Paraméter</span><span class="sxs-lookup"><span data-stu-id="5aeac-117">Parameter</span></span>         | <span data-ttu-id="5aeac-118">Típus</span><span class="sxs-lookup"><span data-stu-id="5aeac-118">Type</span></span>     | <span data-ttu-id="5aeac-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="5aeac-119">Description</span></span> | <span data-ttu-id="5aeac-120">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5aeac-120">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="5aeac-121">top</span><span class="sxs-lookup"><span data-stu-id="5aeac-121">top</span></span>               | <span data-ttu-id="5aeac-122">sztring</span><span class="sxs-lookup"><span data-stu-id="5aeac-122">string</span></span>   | <span data-ttu-id="5aeac-123">A kérelemben visszaadni kívánt adatsorok száma.</span><span class="sxs-lookup"><span data-stu-id="5aeac-123">The number of rows of data to return in the request.</span></span> <span data-ttu-id="5aeac-124">Ha nincs megadva, a maximális érték és az alapértelmezett érték 10000.</span><span class="sxs-lookup"><span data-stu-id="5aeac-124">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="5aeac-125">Ha a lekérdezés több sort tartalmaz, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldal lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="5aeac-125">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="5aeac-126">Nem</span><span class="sxs-lookup"><span data-stu-id="5aeac-126">No</span></span> |
| <span data-ttu-id="5aeac-127">Ugrál</span><span class="sxs-lookup"><span data-stu-id="5aeac-127">skip</span></span>              | <span data-ttu-id="5aeac-128">int</span><span class="sxs-lookup"><span data-stu-id="5aeac-128">int</span></span>      | <span data-ttu-id="5aeac-129">A lekérdezésben kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="5aeac-129">The number of rows to skip in the query.</span></span> <span data-ttu-id="5aeac-130">Ezzel a paraméterrel nagy adatkészletek között lapokat laposszunk.</span><span class="sxs-lookup"><span data-stu-id="5aeac-130">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="5aeac-131">Például a top=10000 és a skip=0 lekéri az első 10000 adatsort, a top=10000 és a skip=10000 a következő 10000 adatsort és így tovább.</span><span class="sxs-lookup"><span data-stu-id="5aeac-131">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="5aeac-132">Nem</span><span class="sxs-lookup"><span data-stu-id="5aeac-132">No</span></span> |
| <span data-ttu-id="5aeac-133">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="5aeac-133">filter</span></span>            | <span data-ttu-id="5aeac-134">sztring</span><span class="sxs-lookup"><span data-stu-id="5aeac-134">string</span></span>   | <span data-ttu-id="5aeac-135">A *kérés* szűrőparamétere egy vagy több olyan utasításokat tartalmaz, amelyek szűrik a válasz sorait.</span><span class="sxs-lookup"><span data-stu-id="5aeac-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="5aeac-136">Minden utasítás tartalmaz egy mezőt és egy értéket, amely az vagy operátorhoz van társítva, és az utasítások kombinálhatók **`eq`** **`ne`** a vagy a **`and`** **`or`** használatával.</span><span class="sxs-lookup"><span data-stu-id="5aeac-136">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators, and statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="5aeac-137">Íme néhány példa *szűrőparaméterre:*</span><span class="sxs-lookup"><span data-stu-id="5aeac-137">Here are some example *filter* parameters:</span></span><br/><br/><span data-ttu-id="5aeac-138">*filter=workloadCode eq 'SFB'*</span><span class="sxs-lookup"><span data-stu-id="5aeac-138">*filter=workloadCode eq 'SFB'*</span></span><br/><br/><span data-ttu-id="5aeac-139">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span><span class="sxs-lookup"><span data-stu-id="5aeac-139">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span></span><br/><br/><span data-ttu-id="5aeac-140">A következő mezőket adhatja meg:</span><span class="sxs-lookup"><span data-stu-id="5aeac-140">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="5aeac-141">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="5aeac-141">**workloadCode**</span></span><br/><span data-ttu-id="5aeac-142">**workloadName (számítási feladat neve)**</span><span class="sxs-lookup"><span data-stu-id="5aeac-142">**workloadName**</span></span><br/><span data-ttu-id="5aeac-143">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="5aeac-143">**serviceCode**</span></span><br/><span data-ttu-id="5aeac-144">**serviceName (szolgáltatásnév)**</span><span class="sxs-lookup"><span data-stu-id="5aeac-144">**serviceName**</span></span><br/><span data-ttu-id="5aeac-145">**Csatorna**</span><span class="sxs-lookup"><span data-stu-id="5aeac-145">**channel**</span></span><br/><span data-ttu-id="5aeac-146">**customerTenantId (customerTenantId)**</span><span class="sxs-lookup"><span data-stu-id="5aeac-146">**customerTenantId**</span></span><br/><span data-ttu-id="5aeac-147">**customerName (ügyfél neve)**</span><span class="sxs-lookup"><span data-stu-id="5aeac-147">**customerName**</span></span><br/><span data-ttu-id="5aeac-148">**Termelés**</span><span class="sxs-lookup"><span data-stu-id="5aeac-148">**productId**</span></span><br/><span data-ttu-id="5aeac-149">**Productname**</span><span class="sxs-lookup"><span data-stu-id="5aeac-149">**productName**</span></span> | <span data-ttu-id="5aeac-150">Nem</span><span class="sxs-lookup"><span data-stu-id="5aeac-150">No</span></span> |
| <span data-ttu-id="5aeac-151">groupby</span><span class="sxs-lookup"><span data-stu-id="5aeac-151">groupby</span></span>           | <span data-ttu-id="5aeac-152">sztring</span><span class="sxs-lookup"><span data-stu-id="5aeac-152">string</span></span>   | <span data-ttu-id="5aeac-153">Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítőt.</span><span class="sxs-lookup"><span data-stu-id="5aeac-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="5aeac-154">A következő mezőket adhatja meg:</span><span class="sxs-lookup"><span data-stu-id="5aeac-154">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="5aeac-155">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="5aeac-155">**workloadCode**</span></span><br/><span data-ttu-id="5aeac-156">**workloadName (számítási feladat neve)**</span><span class="sxs-lookup"><span data-stu-id="5aeac-156">**workloadName**</span></span><br/><span data-ttu-id="5aeac-157">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="5aeac-157">**serviceCode**</span></span><br/><span data-ttu-id="5aeac-158">**serviceName (szolgáltatásnév)**</span><span class="sxs-lookup"><span data-stu-id="5aeac-158">**serviceName**</span></span><br/><span data-ttu-id="5aeac-159">**channelcustomerTenantId**</span><span class="sxs-lookup"><span data-stu-id="5aeac-159">**channelcustomerTenantId**</span></span><br/><span data-ttu-id="5aeac-160">**customerName (ügyfél neve)**</span><span class="sxs-lookup"><span data-stu-id="5aeac-160">**customerName**</span></span><br/><span data-ttu-id="5aeac-161">**Termelés**</span><span class="sxs-lookup"><span data-stu-id="5aeac-161">**productId**</span></span><br/><span data-ttu-id="5aeac-162">**Productname**</span><span class="sxs-lookup"><span data-stu-id="5aeac-162">**productName**</span></span><br/><br/><span data-ttu-id="5aeac-163">A visszaadott adatsorok tartalmazzák a *groupby* paraméterben megadott mezőket és a következőket:</span><span class="sxs-lookup"><span data-stu-id="5aeac-163">The returned data rows will contain the fields specified in the *groupby* parameter and the following:</span></span><br/><br/><span data-ttu-id="5aeac-164">**licensesActive**</span><span class="sxs-lookup"><span data-stu-id="5aeac-164">**licensesActive**</span></span><br/><span data-ttu-id="5aeac-165">**licensesQualified**</span><span class="sxs-lookup"><span data-stu-id="5aeac-165">**licensesQualified**</span></span> | <span data-ttu-id="5aeac-166">Nem</span><span class="sxs-lookup"><span data-stu-id="5aeac-166">No</span></span> |
| <span data-ttu-id="5aeac-167">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="5aeac-167">processedDateTime</span></span> | <span data-ttu-id="5aeac-168">DateTime</span><span class="sxs-lookup"><span data-stu-id="5aeac-168">DateTime</span></span> | <span data-ttu-id="5aeac-169">Megadhatja a használati adatok feldolgozásának dátumát.</span><span class="sxs-lookup"><span data-stu-id="5aeac-169">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="5aeac-170">Alapértelmezés szerint az adatok feldolgozásának legkésőbbi dátuma</span><span class="sxs-lookup"><span data-stu-id="5aeac-170">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="5aeac-171">Nem</span><span class="sxs-lookup"><span data-stu-id="5aeac-171">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="5aeac-172">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5aeac-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="5aeac-173">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5aeac-173">REST response</span></span>

<span data-ttu-id="5aeac-174">Sikeres művelet esetén a válasz törzse a következő mezőket tartalmazza, amelyek a licenchasználattal kapcsolatos adatokat tartalmazzák.</span><span class="sxs-lookup"><span data-stu-id="5aeac-174">If successful, the response body contains the following fields containing data about licenses usage.</span></span>

| <span data-ttu-id="5aeac-175">Mező</span><span class="sxs-lookup"><span data-stu-id="5aeac-175">Field</span></span>             | <span data-ttu-id="5aeac-176">Típus</span><span class="sxs-lookup"><span data-stu-id="5aeac-176">Type</span></span>     | <span data-ttu-id="5aeac-177">Leírás</span><span class="sxs-lookup"><span data-stu-id="5aeac-177">Description</span></span>                                   |
|-------------------|----------|-----------------------------------------------|
| <span data-ttu-id="5aeac-178">workloadCode</span><span class="sxs-lookup"><span data-stu-id="5aeac-178">workloadCode</span></span>      | <span data-ttu-id="5aeac-179">sztring</span><span class="sxs-lookup"><span data-stu-id="5aeac-179">string</span></span>   | <span data-ttu-id="5aeac-180">Számítási feladat kódja</span><span class="sxs-lookup"><span data-stu-id="5aeac-180">Workload code</span></span>                                 |
| <span data-ttu-id="5aeac-181">workloadName (számítási feladat neve)</span><span class="sxs-lookup"><span data-stu-id="5aeac-181">workloadName</span></span>      | <span data-ttu-id="5aeac-182">sztring</span><span class="sxs-lookup"><span data-stu-id="5aeac-182">string</span></span>   | <span data-ttu-id="5aeac-183">Számítási feladat neve</span><span class="sxs-lookup"><span data-stu-id="5aeac-183">Workload name</span></span>                                 |
| <span data-ttu-id="5aeac-184">serviceCode</span><span class="sxs-lookup"><span data-stu-id="5aeac-184">serviceCode</span></span>       | <span data-ttu-id="5aeac-185">sztring</span><span class="sxs-lookup"><span data-stu-id="5aeac-185">string</span></span>   | <span data-ttu-id="5aeac-186">Szolgáltatáskód</span><span class="sxs-lookup"><span data-stu-id="5aeac-186">Service code</span></span>                                  |
| <span data-ttu-id="5aeac-187">serviceName (szolgáltatásnév)</span><span class="sxs-lookup"><span data-stu-id="5aeac-187">serviceName</span></span>       | <span data-ttu-id="5aeac-188">sztring</span><span class="sxs-lookup"><span data-stu-id="5aeac-188">string</span></span>   | <span data-ttu-id="5aeac-189">Szolgáltatásnév</span><span class="sxs-lookup"><span data-stu-id="5aeac-189">Service name</span></span>                                  |
| <span data-ttu-id="5aeac-190">Csatorna</span><span class="sxs-lookup"><span data-stu-id="5aeac-190">channel</span></span>           | <span data-ttu-id="5aeac-191">sztring</span><span class="sxs-lookup"><span data-stu-id="5aeac-191">string</span></span>   | <span data-ttu-id="5aeac-192">Csatorna neve, viszonteladó</span><span class="sxs-lookup"><span data-stu-id="5aeac-192">Channel name, reseller</span></span>                        |
| <span data-ttu-id="5aeac-193">customerTenantId (customerTenantId)</span><span class="sxs-lookup"><span data-stu-id="5aeac-193">customerTenantId</span></span>  | <span data-ttu-id="5aeac-194">sztring</span><span class="sxs-lookup"><span data-stu-id="5aeac-194">string</span></span>   | <span data-ttu-id="5aeac-195">Az ügyfél egyedi azonosítója</span><span class="sxs-lookup"><span data-stu-id="5aeac-195">Unique identifier for the customer</span></span>            |
| <span data-ttu-id="5aeac-196">customerName (ügyfél neve)</span><span class="sxs-lookup"><span data-stu-id="5aeac-196">customerName</span></span>      | <span data-ttu-id="5aeac-197">sztring</span><span class="sxs-lookup"><span data-stu-id="5aeac-197">string</span></span>   | <span data-ttu-id="5aeac-198">Ügyfél neve</span><span class="sxs-lookup"><span data-stu-id="5aeac-198">Customer name</span></span>                                 |
| <span data-ttu-id="5aeac-199">productId</span><span class="sxs-lookup"><span data-stu-id="5aeac-199">productId</span></span>         | <span data-ttu-id="5aeac-200">sztring</span><span class="sxs-lookup"><span data-stu-id="5aeac-200">string</span></span>   | <span data-ttu-id="5aeac-201">A termék egyedi azonosítója</span><span class="sxs-lookup"><span data-stu-id="5aeac-201">Unique identifier for the product</span></span>             |
| <span data-ttu-id="5aeac-202">Productname</span><span class="sxs-lookup"><span data-stu-id="5aeac-202">productName</span></span>       | <span data-ttu-id="5aeac-203">sztring</span><span class="sxs-lookup"><span data-stu-id="5aeac-203">string</span></span>   | <span data-ttu-id="5aeac-204">Terméknév</span><span class="sxs-lookup"><span data-stu-id="5aeac-204">Product name</span></span>                                  |
| <span data-ttu-id="5aeac-205">licensesActive</span><span class="sxs-lookup"><span data-stu-id="5aeac-205">licensesActive</span></span>    | <span data-ttu-id="5aeac-206">hosszú</span><span class="sxs-lookup"><span data-stu-id="5aeac-206">long</span></span>     | <span data-ttu-id="5aeac-207">Aktív licencek száma számítási feladatonként</span><span class="sxs-lookup"><span data-stu-id="5aeac-207">Number of active licenses per workload</span></span>        |
| <span data-ttu-id="5aeac-208">licensesQualified</span><span class="sxs-lookup"><span data-stu-id="5aeac-208">licensesQualified</span></span> | <span data-ttu-id="5aeac-209">hosszú</span><span class="sxs-lookup"><span data-stu-id="5aeac-209">long</span></span>     | <span data-ttu-id="5aeac-210">A számítási feladat minősített licenceinek száma</span><span class="sxs-lookup"><span data-stu-id="5aeac-210">Number of qualified licenses for the workload</span></span> |
| <span data-ttu-id="5aeac-211">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="5aeac-211">processedDateTime</span></span> | <span data-ttu-id="5aeac-212">DateTime</span><span class="sxs-lookup"><span data-stu-id="5aeac-212">DateTime</span></span> | <span data-ttu-id="5aeac-213">Az adatok utolsó feldolgozásának dátuma</span><span class="sxs-lookup"><span data-stu-id="5aeac-213">Date when the data was last processed</span></span>         |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5aeac-214">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5aeac-214">Response success and error codes</span></span>

<span data-ttu-id="5aeac-215">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="5aeac-215">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5aeac-216">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="5aeac-216">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5aeac-217">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="5aeac-217">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5aeac-218">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5aeac-218">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 4
Date: Wed, 24 Oct 2018 22:37:18 GMT

{
"Value": [
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```
