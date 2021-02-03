---
title: Licencek használati adatainak lekérése
description: Licencek használati adatainak beszerzése az Office és a Dynamics munkaterhelési szintjén.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a144fd078a36289e4a2c70880817b1f0ca627e8a
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768160"
---
# <a name="get-licenses-usage-information"></a><span data-ttu-id="4a504-103">Licencek használati adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="4a504-103">Get licenses usage information</span></span>

<span data-ttu-id="4a504-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="4a504-104">**Applies To**</span></span>

- <span data-ttu-id="4a504-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="4a504-105">Partner Center</span></span>

<span data-ttu-id="4a504-106">Licencek használati adatainak beszerzése az Office és a Dynamics munkaterhelési szintjén.</span><span class="sxs-lookup"><span data-stu-id="4a504-106">How to get licenses usage information at the workload level for Office and Dynamics.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a504-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4a504-107">Prerequisites</span></span>

<span data-ttu-id="4a504-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="4a504-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4a504-109">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="4a504-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="4a504-110">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="4a504-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4a504-111">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4a504-111">Request syntax</span></span>

| <span data-ttu-id="4a504-112">Metódus</span><span class="sxs-lookup"><span data-stu-id="4a504-112">Method</span></span>  | <span data-ttu-id="4a504-113">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4a504-113">Request URI</span></span>                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="4a504-114">**GET**</span><span class="sxs-lookup"><span data-stu-id="4a504-114">**GET**</span></span> | <span data-ttu-id="4a504-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/Commercial/Usage/License/http/1.1</span><span class="sxs-lookup"><span data-stu-id="4a504-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4a504-116">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4a504-116">Request headers</span></span>

<span data-ttu-id="4a504-117">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4a504-117">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="4a504-118">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="4a504-118">URI parameters</span></span>

| <span data-ttu-id="4a504-119">Paraméter</span><span class="sxs-lookup"><span data-stu-id="4a504-119">Parameter</span></span>         | <span data-ttu-id="4a504-120">Típus</span><span class="sxs-lookup"><span data-stu-id="4a504-120">Type</span></span>     | <span data-ttu-id="4a504-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="4a504-121">Description</span></span> | <span data-ttu-id="4a504-122">Kötelező</span><span class="sxs-lookup"><span data-stu-id="4a504-122">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="4a504-123">top</span><span class="sxs-lookup"><span data-stu-id="4a504-123">top</span></span>               | <span data-ttu-id="4a504-124">sztring</span><span class="sxs-lookup"><span data-stu-id="4a504-124">string</span></span>   | <span data-ttu-id="4a504-125">A kérelemben visszaadni kívánt adatsorok száma.</span><span class="sxs-lookup"><span data-stu-id="4a504-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="4a504-126">A maximális érték és az alapértelmezett érték, ha nincs megadva, 10000.</span><span class="sxs-lookup"><span data-stu-id="4a504-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="4a504-127">Ha több sor van a lekérdezésben, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldalának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="4a504-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="4a504-128">Nem</span><span class="sxs-lookup"><span data-stu-id="4a504-128">No</span></span> |
| <span data-ttu-id="4a504-129">kihagyása</span><span class="sxs-lookup"><span data-stu-id="4a504-129">skip</span></span>              | <span data-ttu-id="4a504-130">int</span><span class="sxs-lookup"><span data-stu-id="4a504-130">int</span></span>      | <span data-ttu-id="4a504-131">A lekérdezésben kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="4a504-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="4a504-132">Használja ezt a paramétert a nagy adathalmazokon keresztüli lapra.</span><span class="sxs-lookup"><span data-stu-id="4a504-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="4a504-133">Például a Top = 10000 és a skip = 0 lekérdezi az első 10000 adatsort, a Top = 10000 és a skip = 10000 lekéri a következő 10000 sort, és így tovább.</span><span class="sxs-lookup"><span data-stu-id="4a504-133">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="4a504-134">Nem</span><span class="sxs-lookup"><span data-stu-id="4a504-134">No</span></span> |
| <span data-ttu-id="4a504-135">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="4a504-135">filter</span></span>            | <span data-ttu-id="4a504-136">sztring</span><span class="sxs-lookup"><span data-stu-id="4a504-136">string</span></span>   | <span data-ttu-id="4a504-137">A kérelem *Filter* paraméterében egy vagy több olyan utasítás található, amely a válasz sorait szűri.</span><span class="sxs-lookup"><span data-stu-id="4a504-137">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="4a504-138">Minden utasítás tartalmaz egy mezőt és egy értéket, amely társítva van az **`eq`** vagy **`ne`** operátorhoz, és a utasítások kombinálhatók a vagy a használatával **`and`** **`or`** .</span><span class="sxs-lookup"><span data-stu-id="4a504-138">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators, and statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="4a504-139">Íme néhány példa a *szűrési* paraméterekre:</span><span class="sxs-lookup"><span data-stu-id="4a504-139">Here are some example *filter* parameters:</span></span><br/><br/><span data-ttu-id="4a504-140">*Filter = workloadCode EQ "SFB"*</span><span class="sxs-lookup"><span data-stu-id="4a504-140">*filter=workloadCode eq 'SFB'*</span></span><br/><br/><span data-ttu-id="4a504-141">*Filter = workloadCode EQ "SFB"* vagy (*Channel EQ "viszonteladó"*)</span><span class="sxs-lookup"><span data-stu-id="4a504-141">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span></span><br/><br/><span data-ttu-id="4a504-142">A következő mezőket adhatja meg:</span><span class="sxs-lookup"><span data-stu-id="4a504-142">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="4a504-143">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="4a504-143">**workloadCode**</span></span><br/><span data-ttu-id="4a504-144">**workloadName**</span><span class="sxs-lookup"><span data-stu-id="4a504-144">**workloadName**</span></span><br/><span data-ttu-id="4a504-145">**Meg**</span><span class="sxs-lookup"><span data-stu-id="4a504-145">**serviceCode**</span></span><br/><span data-ttu-id="4a504-146">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="4a504-146">**serviceName**</span></span><br/><span data-ttu-id="4a504-147">**csatorna**</span><span class="sxs-lookup"><span data-stu-id="4a504-147">**channel**</span></span><br/><span data-ttu-id="4a504-148">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="4a504-148">**customerTenantId**</span></span><br/><span data-ttu-id="4a504-149">**Customername (**</span><span class="sxs-lookup"><span data-stu-id="4a504-149">**customerName**</span></span><br/><span data-ttu-id="4a504-150">**productId**</span><span class="sxs-lookup"><span data-stu-id="4a504-150">**productId**</span></span><br/><span data-ttu-id="4a504-151">**productName**</span><span class="sxs-lookup"><span data-stu-id="4a504-151">**productName**</span></span> | <span data-ttu-id="4a504-152">Nem</span><span class="sxs-lookup"><span data-stu-id="4a504-152">No</span></span> |
| <span data-ttu-id="4a504-153">groupby</span><span class="sxs-lookup"><span data-stu-id="4a504-153">groupby</span></span>           | <span data-ttu-id="4a504-154">sztring</span><span class="sxs-lookup"><span data-stu-id="4a504-154">string</span></span>   | <span data-ttu-id="4a504-155">Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítést.</span><span class="sxs-lookup"><span data-stu-id="4a504-155">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="4a504-156">A következő mezőket adhatja meg:</span><span class="sxs-lookup"><span data-stu-id="4a504-156">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="4a504-157">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="4a504-157">**workloadCode**</span></span><br/><span data-ttu-id="4a504-158">**workloadName**</span><span class="sxs-lookup"><span data-stu-id="4a504-158">**workloadName**</span></span><br/><span data-ttu-id="4a504-159">**Meg**</span><span class="sxs-lookup"><span data-stu-id="4a504-159">**serviceCode**</span></span><br/><span data-ttu-id="4a504-160">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="4a504-160">**serviceName**</span></span><br/><span data-ttu-id="4a504-161">**channelcustomerTenantId**</span><span class="sxs-lookup"><span data-stu-id="4a504-161">**channelcustomerTenantId**</span></span><br/><span data-ttu-id="4a504-162">**Customername (**</span><span class="sxs-lookup"><span data-stu-id="4a504-162">**customerName**</span></span><br/><span data-ttu-id="4a504-163">**productId**</span><span class="sxs-lookup"><span data-stu-id="4a504-163">**productId**</span></span><br/><span data-ttu-id="4a504-164">**productName**</span><span class="sxs-lookup"><span data-stu-id="4a504-164">**productName**</span></span><br/><br/><span data-ttu-id="4a504-165">A visszaadott adatsorok tartalmazzák a *groupby* paraméterben megadott mezőket, valamint a következőket:</span><span class="sxs-lookup"><span data-stu-id="4a504-165">The returned data rows will contain the fields specified in the *groupby* parameter as well as the following:</span></span><br/><br/><span data-ttu-id="4a504-166">**licensesActive**</span><span class="sxs-lookup"><span data-stu-id="4a504-166">**licensesActive**</span></span><br/><span data-ttu-id="4a504-167">**licensesQualified**</span><span class="sxs-lookup"><span data-stu-id="4a504-167">**licensesQualified**</span></span> | <span data-ttu-id="4a504-168">Nem</span><span class="sxs-lookup"><span data-stu-id="4a504-168">No</span></span> |
| <span data-ttu-id="4a504-169">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="4a504-169">processedDateTime</span></span> | <span data-ttu-id="4a504-170">DateTime</span><span class="sxs-lookup"><span data-stu-id="4a504-170">DateTime</span></span> | <span data-ttu-id="4a504-171">Megadhatja azt a dátumot, amelyből a használati adatokat feldolgozták.</span><span class="sxs-lookup"><span data-stu-id="4a504-171">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="4a504-172">Alapértelmezett érték az adatok feldolgozásának legkésőbbi dátuma</span><span class="sxs-lookup"><span data-stu-id="4a504-172">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="4a504-173">Nem</span><span class="sxs-lookup"><span data-stu-id="4a504-173">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="4a504-174">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4a504-174">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="4a504-175">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4a504-175">REST response</span></span>

<span data-ttu-id="4a504-176">Ha a művelet sikeres, a válasz törzse a következő mezőket tartalmazza, amelyek tartalmazzák a licencek használatáról szóló adatokat.</span><span class="sxs-lookup"><span data-stu-id="4a504-176">If successful, the response body contains the following fields containing data about licenses usage.</span></span>

| <span data-ttu-id="4a504-177">Mező</span><span class="sxs-lookup"><span data-stu-id="4a504-177">Field</span></span>             | <span data-ttu-id="4a504-178">Típus</span><span class="sxs-lookup"><span data-stu-id="4a504-178">Type</span></span>     | <span data-ttu-id="4a504-179">Leírás</span><span class="sxs-lookup"><span data-stu-id="4a504-179">Description</span></span>                                   |
|-------------------|----------|-----------------------------------------------|
| <span data-ttu-id="4a504-180">workloadCode</span><span class="sxs-lookup"><span data-stu-id="4a504-180">workloadCode</span></span>      | <span data-ttu-id="4a504-181">sztring</span><span class="sxs-lookup"><span data-stu-id="4a504-181">string</span></span>   | <span data-ttu-id="4a504-182">Munkaterhelés kódja</span><span class="sxs-lookup"><span data-stu-id="4a504-182">Workload code</span></span>                                 |
| <span data-ttu-id="4a504-183">workloadName</span><span class="sxs-lookup"><span data-stu-id="4a504-183">workloadName</span></span>      | <span data-ttu-id="4a504-184">sztring</span><span class="sxs-lookup"><span data-stu-id="4a504-184">string</span></span>   | <span data-ttu-id="4a504-185">Munkaterhelés neve</span><span class="sxs-lookup"><span data-stu-id="4a504-185">Workload name</span></span>                                 |
| <span data-ttu-id="4a504-186">Meg</span><span class="sxs-lookup"><span data-stu-id="4a504-186">serviceCode</span></span>       | <span data-ttu-id="4a504-187">sztring</span><span class="sxs-lookup"><span data-stu-id="4a504-187">string</span></span>   | <span data-ttu-id="4a504-188">Szolgáltatási kód</span><span class="sxs-lookup"><span data-stu-id="4a504-188">Service code</span></span>                                  |
| <span data-ttu-id="4a504-189">serviceName</span><span class="sxs-lookup"><span data-stu-id="4a504-189">serviceName</span></span>       | <span data-ttu-id="4a504-190">sztring</span><span class="sxs-lookup"><span data-stu-id="4a504-190">string</span></span>   | <span data-ttu-id="4a504-191">Szolgáltatásnév</span><span class="sxs-lookup"><span data-stu-id="4a504-191">Service name</span></span>                                  |
| <span data-ttu-id="4a504-192">csatorna</span><span class="sxs-lookup"><span data-stu-id="4a504-192">channel</span></span>           | <span data-ttu-id="4a504-193">sztring</span><span class="sxs-lookup"><span data-stu-id="4a504-193">string</span></span>   | <span data-ttu-id="4a504-194">Csatorna neve, viszonteladó</span><span class="sxs-lookup"><span data-stu-id="4a504-194">Channel name, reseller</span></span>                        |
| <span data-ttu-id="4a504-195">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="4a504-195">customerTenantId</span></span>  | <span data-ttu-id="4a504-196">sztring</span><span class="sxs-lookup"><span data-stu-id="4a504-196">string</span></span>   | <span data-ttu-id="4a504-197">Az ügyfél egyedi azonosítója</span><span class="sxs-lookup"><span data-stu-id="4a504-197">Unique identifier for the customer</span></span>            |
| <span data-ttu-id="4a504-198">Customername (</span><span class="sxs-lookup"><span data-stu-id="4a504-198">customerName</span></span>      | <span data-ttu-id="4a504-199">sztring</span><span class="sxs-lookup"><span data-stu-id="4a504-199">string</span></span>   | <span data-ttu-id="4a504-200">Ügyfél neve</span><span class="sxs-lookup"><span data-stu-id="4a504-200">Customer name</span></span>                                 |
| <span data-ttu-id="4a504-201">productId</span><span class="sxs-lookup"><span data-stu-id="4a504-201">productId</span></span>         | <span data-ttu-id="4a504-202">sztring</span><span class="sxs-lookup"><span data-stu-id="4a504-202">string</span></span>   | <span data-ttu-id="4a504-203">A termék egyedi azonosítója</span><span class="sxs-lookup"><span data-stu-id="4a504-203">Unique identifier for the product</span></span>             |
| <span data-ttu-id="4a504-204">productName</span><span class="sxs-lookup"><span data-stu-id="4a504-204">productName</span></span>       | <span data-ttu-id="4a504-205">sztring</span><span class="sxs-lookup"><span data-stu-id="4a504-205">string</span></span>   | <span data-ttu-id="4a504-206">Terméknév</span><span class="sxs-lookup"><span data-stu-id="4a504-206">Product name</span></span>                                  |
| <span data-ttu-id="4a504-207">licensesActive</span><span class="sxs-lookup"><span data-stu-id="4a504-207">licensesActive</span></span>    | <span data-ttu-id="4a504-208">hosszú</span><span class="sxs-lookup"><span data-stu-id="4a504-208">long</span></span>     | <span data-ttu-id="4a504-209">Aktív licencek száma munkaterhelés szerint</span><span class="sxs-lookup"><span data-stu-id="4a504-209">Number of active licenses per workload</span></span>        |
| <span data-ttu-id="4a504-210">licensesQualified</span><span class="sxs-lookup"><span data-stu-id="4a504-210">licensesQualified</span></span> | <span data-ttu-id="4a504-211">hosszú</span><span class="sxs-lookup"><span data-stu-id="4a504-211">long</span></span>     | <span data-ttu-id="4a504-212">A munkaterheléshez tartozó minősített licencek száma</span><span class="sxs-lookup"><span data-stu-id="4a504-212">Number of qualified licenses for the workload</span></span> |
| <span data-ttu-id="4a504-213">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="4a504-213">processedDateTime</span></span> | <span data-ttu-id="4a504-214">DateTime</span><span class="sxs-lookup"><span data-stu-id="4a504-214">DateTime</span></span> | <span data-ttu-id="4a504-215">Az adatok legutóbbi feldolgozásának dátuma</span><span class="sxs-lookup"><span data-stu-id="4a504-215">Date when the data was last processed</span></span>         |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4a504-216">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4a504-216">Response success and error codes</span></span>

<span data-ttu-id="4a504-217">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="4a504-217">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4a504-218">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="4a504-218">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4a504-219">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="4a504-219">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4a504-220">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4a504-220">Response example</span></span>

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
