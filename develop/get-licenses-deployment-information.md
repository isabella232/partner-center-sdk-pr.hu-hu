---
title: Licencek üzembehelyezési adatainak lekérése
description: Az Office-és Dynamics-licencek telepítési adatainak beszerzése.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef0e5d73d34bc51e4cc58143db6c9fc49cb58fcb
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768164"
---
# <a name="get-licenses-deployment-information"></a><span data-ttu-id="68b6b-103">Licencek üzembehelyezési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="68b6b-103">Get licenses deployment information</span></span>

<span data-ttu-id="68b6b-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="68b6b-104">**Applies To**</span></span>

- <span data-ttu-id="68b6b-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="68b6b-105">Partner Center</span></span>

<span data-ttu-id="68b6b-106">Az Office-és Dynamics-licencek telepítési adatainak beszerzése.</span><span class="sxs-lookup"><span data-stu-id="68b6b-106">How to get deployment information for Office and Dynamics licenses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68b6b-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="68b6b-107">Prerequisites</span></span>

<span data-ttu-id="68b6b-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="68b6b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="68b6b-109">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="68b6b-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="68b6b-110">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="68b6b-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="68b6b-111">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="68b6b-111">Request syntax</span></span>

| <span data-ttu-id="68b6b-112">Metódus</span><span class="sxs-lookup"><span data-stu-id="68b6b-112">Method</span></span>  | <span data-ttu-id="68b6b-113">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="68b6b-113">Request URI</span></span>                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="68b6b-114">**GET**</span><span class="sxs-lookup"><span data-stu-id="68b6b-114">**GET**</span></span> | <span data-ttu-id="68b6b-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/Commercial/Deployment/License/http/1.1</span><span class="sxs-lookup"><span data-stu-id="68b6b-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="68b6b-116">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="68b6b-116">Request headers</span></span>

<span data-ttu-id="68b6b-117">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="68b6b-117">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="68b6b-118">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="68b6b-118">URI parameters</span></span>

| <span data-ttu-id="68b6b-119">Paraméter</span><span class="sxs-lookup"><span data-stu-id="68b6b-119">Parameter</span></span>         | <span data-ttu-id="68b6b-120">Típus</span><span class="sxs-lookup"><span data-stu-id="68b6b-120">Type</span></span>     | <span data-ttu-id="68b6b-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="68b6b-121">Description</span></span> | <span data-ttu-id="68b6b-122">Kötelező</span><span class="sxs-lookup"><span data-stu-id="68b6b-122">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="68b6b-123">top</span><span class="sxs-lookup"><span data-stu-id="68b6b-123">top</span></span>               | <span data-ttu-id="68b6b-124">sztring</span><span class="sxs-lookup"><span data-stu-id="68b6b-124">string</span></span>   | <span data-ttu-id="68b6b-125">A kérelemben visszaadni kívánt adatsorok száma.</span><span class="sxs-lookup"><span data-stu-id="68b6b-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="68b6b-126">A maximális érték és az alapértelmezett érték, ha nincs megadva, 10000.</span><span class="sxs-lookup"><span data-stu-id="68b6b-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="68b6b-127">Ha több sor van a lekérdezésben, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldalának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="68b6b-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="68b6b-128">Nem</span><span class="sxs-lookup"><span data-stu-id="68b6b-128">No</span></span> |
| <span data-ttu-id="68b6b-129">kihagyása</span><span class="sxs-lookup"><span data-stu-id="68b6b-129">skip</span></span>              | <span data-ttu-id="68b6b-130">int</span><span class="sxs-lookup"><span data-stu-id="68b6b-130">int</span></span>      | <span data-ttu-id="68b6b-131">A lekérdezésben kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="68b6b-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="68b6b-132">Használja ezt a paramétert a nagy adathalmazokon keresztüli lapra.</span><span class="sxs-lookup"><span data-stu-id="68b6b-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="68b6b-133">Például a Top = 10000 és a skip = 0 lekérdezi az első 10000 adatsort, a Top = 10000 és a skip = 10000 lekéri a következő 10000 sort, és így tovább.</span><span class="sxs-lookup"><span data-stu-id="68b6b-133">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="68b6b-134">Nem</span><span class="sxs-lookup"><span data-stu-id="68b6b-134">No</span></span> |
| <span data-ttu-id="68b6b-135">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="68b6b-135">filter</span></span>            | <span data-ttu-id="68b6b-136">sztring</span><span class="sxs-lookup"><span data-stu-id="68b6b-136">string</span></span>   | <span data-ttu-id="68b6b-137">A kérelem *Filter* paraméterében egy vagy több olyan utasítás található, amely a válasz sorait szűri.</span><span class="sxs-lookup"><span data-stu-id="68b6b-137">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="68b6b-138">Minden utasítás tartalmaz egy mezőt és egy értéket, amely társítva van az `eq` vagy `ne` operátorhoz, és a utasítások kombinálhatók a vagy a használatával `and` `or` .</span><span class="sxs-lookup"><span data-stu-id="68b6b-138">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="68b6b-139">Íme néhány példa a *szűrési* paraméterekre:</span><span class="sxs-lookup"><span data-stu-id="68b6b-139">Here are some example *filter* parameters:</span></span><br/><br/> <span data-ttu-id="68b6b-140">*Filter = meg EQ "O365"*</span><span class="sxs-lookup"><span data-stu-id="68b6b-140">*filter=serviceCode eq 'O365'*</span></span><br/> <span data-ttu-id="68b6b-141">*Filter = meg EQ "O365"* vagy (*Channel EQ "viszonteladó"*)</span><span class="sxs-lookup"><span data-stu-id="68b6b-141">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span></span><br/><br/> <span data-ttu-id="68b6b-142">A következő mezőket adhatja meg:</span><span class="sxs-lookup"><span data-stu-id="68b6b-142">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="68b6b-143">**Meg**</span><span class="sxs-lookup"><span data-stu-id="68b6b-143">**serviceCode**</span></span><br/><span data-ttu-id="68b6b-144">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="68b6b-144">**serviceName**</span></span><br/><span data-ttu-id="68b6b-145">**csatorna**</span><span class="sxs-lookup"><span data-stu-id="68b6b-145">**channel**</span></span><br/><span data-ttu-id="68b6b-146">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="68b6b-146">**customerTenantId**</span></span><br/><span data-ttu-id="68b6b-147">**Customername (**</span><span class="sxs-lookup"><span data-stu-id="68b6b-147">**customerName**</span></span><br/><span data-ttu-id="68b6b-148">**productId**</span><span class="sxs-lookup"><span data-stu-id="68b6b-148">**productId**</span></span><br/><span data-ttu-id="68b6b-149">**productName**</span><span class="sxs-lookup"><span data-stu-id="68b6b-149">**productName**</span></span>  | <span data-ttu-id="68b6b-150">Nem</span><span class="sxs-lookup"><span data-stu-id="68b6b-150">No</span></span> |
| <span data-ttu-id="68b6b-151">groupby</span><span class="sxs-lookup"><span data-stu-id="68b6b-151">groupby</span></span>           | <span data-ttu-id="68b6b-152">sztring</span><span class="sxs-lookup"><span data-stu-id="68b6b-152">string</span></span>   | <span data-ttu-id="68b6b-153">Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítést.</span><span class="sxs-lookup"><span data-stu-id="68b6b-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="68b6b-154">A következő mezőket adhatja meg:</span><span class="sxs-lookup"><span data-stu-id="68b6b-154">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="68b6b-155">**Meg**</span><span class="sxs-lookup"><span data-stu-id="68b6b-155">**serviceCode**</span></span><br/><span data-ttu-id="68b6b-156">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="68b6b-156">**serviceName**</span></span><br/><span data-ttu-id="68b6b-157">**csatorna**</span><span class="sxs-lookup"><span data-stu-id="68b6b-157">**channel**</span></span><br/><span data-ttu-id="68b6b-158">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="68b6b-158">**customerTenantId**</span></span><br/><span data-ttu-id="68b6b-159">**Customername (**</span><span class="sxs-lookup"><span data-stu-id="68b6b-159">**customerName**</span></span><br/><span data-ttu-id="68b6b-160">**productId**</span><span class="sxs-lookup"><span data-stu-id="68b6b-160">**productId**</span></span><br/><span data-ttu-id="68b6b-161">**productName**</span><span class="sxs-lookup"><span data-stu-id="68b6b-161">**productName**</span></span><br/><br/> <span data-ttu-id="68b6b-162">A visszaadott adatsorok tartalmazzák a *groupby* paraméterben megadott mezőket, valamint a következőket:</span><span class="sxs-lookup"><span data-stu-id="68b6b-162">The returned data rows will contain the fields specified in the *groupby* parameter as well as the following:</span></span><br/><br/><span data-ttu-id="68b6b-163">**licensesDeployed**</span><span class="sxs-lookup"><span data-stu-id="68b6b-163">**licensesDeployed**</span></span><br/><span data-ttu-id="68b6b-164">**licensesSold**</span><span class="sxs-lookup"><span data-stu-id="68b6b-164">**licensesSold**</span></span>  | <span data-ttu-id="68b6b-165">Nem</span><span class="sxs-lookup"><span data-stu-id="68b6b-165">No</span></span> |
| <span data-ttu-id="68b6b-166">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="68b6b-166">processedDateTime</span></span> | <span data-ttu-id="68b6b-167">DateTime</span><span class="sxs-lookup"><span data-stu-id="68b6b-167">DateTime</span></span> | <span data-ttu-id="68b6b-168">Megadhatja azt a dátumot, amelyből a használati adatokat feldolgozták.</span><span class="sxs-lookup"><span data-stu-id="68b6b-168">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="68b6b-169">Alapértelmezett érték az adatok feldolgozásának legkésőbbi dátuma</span><span class="sxs-lookup"><span data-stu-id="68b6b-169">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="68b6b-170">Nem</span><span class="sxs-lookup"><span data-stu-id="68b6b-170">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="68b6b-171">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="68b6b-171">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="68b6b-172">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="68b6b-172">REST response</span></span>

<span data-ttu-id="68b6b-173">Ha a művelet sikeres, a válasz törzse a következő mezőket tartalmazza, amelyek a telepített licencekre vonatkozó információkat tartalmaznak.</span><span class="sxs-lookup"><span data-stu-id="68b6b-173">If successful, the response body contains the following fields containing data about the licenses deployed.</span></span>

| <span data-ttu-id="68b6b-174">Mező</span><span class="sxs-lookup"><span data-stu-id="68b6b-174">Field</span></span>             | <span data-ttu-id="68b6b-175">Típus</span><span class="sxs-lookup"><span data-stu-id="68b6b-175">Type</span></span>     | <span data-ttu-id="68b6b-176">Leírás</span><span class="sxs-lookup"><span data-stu-id="68b6b-176">Description</span></span>                           |
|-------------------|----------|---------------------------------------|
| <span data-ttu-id="68b6b-177">Meg</span><span class="sxs-lookup"><span data-stu-id="68b6b-177">serviceCode</span></span>       | <span data-ttu-id="68b6b-178">sztring</span><span class="sxs-lookup"><span data-stu-id="68b6b-178">string</span></span>   | <span data-ttu-id="68b6b-179">Szolgáltatási kód</span><span class="sxs-lookup"><span data-stu-id="68b6b-179">Service code</span></span>                          |
| <span data-ttu-id="68b6b-180">serviceName</span><span class="sxs-lookup"><span data-stu-id="68b6b-180">serviceName</span></span>       | <span data-ttu-id="68b6b-181">sztring</span><span class="sxs-lookup"><span data-stu-id="68b6b-181">string</span></span>   | <span data-ttu-id="68b6b-182">Szolgáltatásnév</span><span class="sxs-lookup"><span data-stu-id="68b6b-182">Service name</span></span>                          |
| <span data-ttu-id="68b6b-183">csatorna</span><span class="sxs-lookup"><span data-stu-id="68b6b-183">channel</span></span>           | <span data-ttu-id="68b6b-184">sztring</span><span class="sxs-lookup"><span data-stu-id="68b6b-184">string</span></span>   | <span data-ttu-id="68b6b-185">Csatorna neve, viszonteladó</span><span class="sxs-lookup"><span data-stu-id="68b6b-185">Channel name, reseller</span></span>                |
| <span data-ttu-id="68b6b-186">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="68b6b-186">customerTenantId</span></span>  | <span data-ttu-id="68b6b-187">sztring</span><span class="sxs-lookup"><span data-stu-id="68b6b-187">string</span></span>   | <span data-ttu-id="68b6b-188">Az ügyfél egyedi azonosítója</span><span class="sxs-lookup"><span data-stu-id="68b6b-188">Unique identifier for the customer</span></span>    |
| <span data-ttu-id="68b6b-189">Customername (</span><span class="sxs-lookup"><span data-stu-id="68b6b-189">customerName</span></span>      | <span data-ttu-id="68b6b-190">sztring</span><span class="sxs-lookup"><span data-stu-id="68b6b-190">string</span></span>   | <span data-ttu-id="68b6b-191">Ügyfél neve</span><span class="sxs-lookup"><span data-stu-id="68b6b-191">Customer name</span></span>                         |
| <span data-ttu-id="68b6b-192">productId</span><span class="sxs-lookup"><span data-stu-id="68b6b-192">productId</span></span>         | <span data-ttu-id="68b6b-193">sztring</span><span class="sxs-lookup"><span data-stu-id="68b6b-193">string</span></span>   | <span data-ttu-id="68b6b-194">A termék egyedi azonosítója</span><span class="sxs-lookup"><span data-stu-id="68b6b-194">Unique identifier for the product</span></span>     |
| <span data-ttu-id="68b6b-195">productName</span><span class="sxs-lookup"><span data-stu-id="68b6b-195">productName</span></span>       | <span data-ttu-id="68b6b-196">sztring</span><span class="sxs-lookup"><span data-stu-id="68b6b-196">string</span></span>   | <span data-ttu-id="68b6b-197">Terméknév</span><span class="sxs-lookup"><span data-stu-id="68b6b-197">Product name</span></span>                          |
| <span data-ttu-id="68b6b-198">licensesDeployed</span><span class="sxs-lookup"><span data-stu-id="68b6b-198">licensesDeployed</span></span>  | <span data-ttu-id="68b6b-199">hosszú</span><span class="sxs-lookup"><span data-stu-id="68b6b-199">long</span></span>     | <span data-ttu-id="68b6b-200">Telepített licencek száma</span><span class="sxs-lookup"><span data-stu-id="68b6b-200">Number of licenses deployed</span></span>           |
| <span data-ttu-id="68b6b-201">licensesSold</span><span class="sxs-lookup"><span data-stu-id="68b6b-201">licensesSold</span></span>      | <span data-ttu-id="68b6b-202">hosszú</span><span class="sxs-lookup"><span data-stu-id="68b6b-202">long</span></span>     | <span data-ttu-id="68b6b-203">Eladott licencek száma</span><span class="sxs-lookup"><span data-stu-id="68b6b-203">Number of licenses sold</span></span>               |
| <span data-ttu-id="68b6b-204">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="68b6b-204">processedDateTime</span></span> | <span data-ttu-id="68b6b-205">DateTime</span><span class="sxs-lookup"><span data-stu-id="68b6b-205">DateTime</span></span> | <span data-ttu-id="68b6b-206">Az adatok legutóbbi feldolgozásának dátuma</span><span class="sxs-lookup"><span data-stu-id="68b6b-206">Date when the data was last processed</span></span> |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="68b6b-207">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="68b6b-207">Response success and error codes</span></span>

<span data-ttu-id="68b6b-208">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="68b6b-208">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="68b6b-209">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="68b6b-209">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="68b6b-210">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="68b6b-210">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="68b6b-211">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="68b6b-211">Response example</span></span>

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
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```
