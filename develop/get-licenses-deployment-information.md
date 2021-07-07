---
title: Licencek üzembehelyezési adatainak lekérése
description: Telepítési információk lekérte Office Dynamics-licencekhez.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9eb0dc655affb2216b11635e58e00ed6464d6792
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445663"
---
# <a name="get-licenses-deployment-information"></a><span data-ttu-id="2e6a4-103">Licencek üzembehelyezési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="2e6a4-103">Get licenses deployment information</span></span>

<span data-ttu-id="2e6a4-104">Telepítési információk lekérte Office Dynamics-licencekhez.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-104">How to get deployment information for Office and Dynamics licenses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e6a4-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2e6a4-105">Prerequisites</span></span>

<span data-ttu-id="2e6a4-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2e6a4-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2e6a4-107">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="2e6a4-108">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="2e6a4-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2e6a4-109">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="2e6a4-109">Request syntax</span></span>

| <span data-ttu-id="2e6a4-110">Metódus</span><span class="sxs-lookup"><span data-stu-id="2e6a4-110">Method</span></span>  | <span data-ttu-id="2e6a4-111">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2e6a4-111">Request URI</span></span>                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e6a4-112">**Kap**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-112">**GET**</span></span> | <span data-ttu-id="2e6a4-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2e6a4-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2e6a4-114">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2e6a4-114">Request headers</span></span>

<span data-ttu-id="2e6a4-115">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2e6a4-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="2e6a4-116">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="2e6a4-116">URI parameters</span></span>

| <span data-ttu-id="2e6a4-117">Paraméter</span><span class="sxs-lookup"><span data-stu-id="2e6a4-117">Parameter</span></span>         | <span data-ttu-id="2e6a4-118">Típus</span><span class="sxs-lookup"><span data-stu-id="2e6a4-118">Type</span></span>     | <span data-ttu-id="2e6a4-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="2e6a4-119">Description</span></span> | <span data-ttu-id="2e6a4-120">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2e6a4-120">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="2e6a4-121">top</span><span class="sxs-lookup"><span data-stu-id="2e6a4-121">top</span></span>               | <span data-ttu-id="2e6a4-122">sztring</span><span class="sxs-lookup"><span data-stu-id="2e6a4-122">string</span></span>   | <span data-ttu-id="2e6a4-123">A kérésben visszaadni kívánt adatsorok száma.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-123">The number of rows of data to return in the request.</span></span> <span data-ttu-id="2e6a4-124">Ha nincs megadva, a maximális érték és az alapértelmezett érték 10000.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-124">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="2e6a4-125">Ha a lekérdezés több sort tartalmaz, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldal lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-125">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="2e6a4-126">Nem</span><span class="sxs-lookup"><span data-stu-id="2e6a4-126">No</span></span> |
| <span data-ttu-id="2e6a4-127">Ugrál</span><span class="sxs-lookup"><span data-stu-id="2e6a4-127">skip</span></span>              | <span data-ttu-id="2e6a4-128">int</span><span class="sxs-lookup"><span data-stu-id="2e6a4-128">int</span></span>      | <span data-ttu-id="2e6a4-129">A lekérdezésben kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-129">The number of rows to skip in the query.</span></span> <span data-ttu-id="2e6a4-130">Ezzel a paraméterrel nagy adatkészletek között lapokat laposszunk.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-130">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="2e6a4-131">Például a top=10000 és a skip=0 lekéri az első 10000 adatsort, a top=10000 és a skip=10000 a következő 10000 adatsort és így tovább.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-131">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="2e6a4-132">Nem</span><span class="sxs-lookup"><span data-stu-id="2e6a4-132">No</span></span> |
| <span data-ttu-id="2e6a4-133">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="2e6a4-133">filter</span></span>            | <span data-ttu-id="2e6a4-134">sztring</span><span class="sxs-lookup"><span data-stu-id="2e6a4-134">string</span></span>   | <span data-ttu-id="2e6a4-135">A *kérés* szűrőparamétere egy vagy több olyan utasításokat tartalmaz, amelyek szűrik a válasz sorait.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="2e6a4-136">Minden utasítás tartalmaz egy mezőt és egy értéket, amely az vagy operátorhoz van társítva, és az utasítások a vagy a használatával `eq` `ne` `and` `or` kombinálhatók.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-136">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="2e6a4-137">Íme néhány példa *szűrőparaméterre:*</span><span class="sxs-lookup"><span data-stu-id="2e6a4-137">Here are some example *filter* parameters:</span></span><br/><br/> <span data-ttu-id="2e6a4-138">*filter=serviceCode eq 'O365'*</span><span class="sxs-lookup"><span data-stu-id="2e6a4-138">*filter=serviceCode eq 'O365'*</span></span><br/> <span data-ttu-id="2e6a4-139">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span><span class="sxs-lookup"><span data-stu-id="2e6a4-139">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span></span><br/><br/> <span data-ttu-id="2e6a4-140">A következő mezőket adhatja meg:</span><span class="sxs-lookup"><span data-stu-id="2e6a4-140">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="2e6a4-141">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-141">**serviceCode**</span></span><br/><span data-ttu-id="2e6a4-142">**serviceName (szolgáltatásnév)**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-142">**serviceName**</span></span><br/><span data-ttu-id="2e6a4-143">**Csatorna**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-143">**channel**</span></span><br/><span data-ttu-id="2e6a4-144">**customerTenantId (customerTenantId)**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-144">**customerTenantId**</span></span><br/><span data-ttu-id="2e6a4-145">**customerName (ügyfél neve)**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-145">**customerName**</span></span><br/><span data-ttu-id="2e6a4-146">**Termelés**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-146">**productId**</span></span><br/><span data-ttu-id="2e6a4-147">**Productname**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-147">**productName**</span></span>  | <span data-ttu-id="2e6a4-148">Nem</span><span class="sxs-lookup"><span data-stu-id="2e6a4-148">No</span></span> |
| <span data-ttu-id="2e6a4-149">groupby (csoportosítás)</span><span class="sxs-lookup"><span data-stu-id="2e6a4-149">groupby</span></span>           | <span data-ttu-id="2e6a4-150">sztring</span><span class="sxs-lookup"><span data-stu-id="2e6a4-150">string</span></span>   | <span data-ttu-id="2e6a4-151">Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítőt.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-151">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="2e6a4-152">A következő mezőket adhatja meg:</span><span class="sxs-lookup"><span data-stu-id="2e6a4-152">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="2e6a4-153">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-153">**serviceCode**</span></span><br/><span data-ttu-id="2e6a4-154">**serviceName (szolgáltatásnév)**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-154">**serviceName**</span></span><br/><span data-ttu-id="2e6a4-155">**Csatorna**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-155">**channel**</span></span><br/><span data-ttu-id="2e6a4-156">**customerTenantId (customerTenantId)**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-156">**customerTenantId**</span></span><br/><span data-ttu-id="2e6a4-157">**customerName (ügyfél neve)**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-157">**customerName**</span></span><br/><span data-ttu-id="2e6a4-158">**Termelés**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-158">**productId**</span></span><br/><span data-ttu-id="2e6a4-159">**Productname**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-159">**productName**</span></span><br/><br/> <span data-ttu-id="2e6a4-160">A visszaadott adatsorok tartalmazzák a *groupby* paraméterben megadott mezőket és a következőket:</span><span class="sxs-lookup"><span data-stu-id="2e6a4-160">The returned data rows will contain the fields specified in the *groupby* parameter and the following:</span></span><br/><br/><span data-ttu-id="2e6a4-161">**licensesDeployed**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-161">**licensesDeployed**</span></span><br/><span data-ttu-id="2e6a4-162">**licensesSold**</span><span class="sxs-lookup"><span data-stu-id="2e6a4-162">**licensesSold**</span></span>  | <span data-ttu-id="2e6a4-163">Nem</span><span class="sxs-lookup"><span data-stu-id="2e6a4-163">No</span></span> |
| <span data-ttu-id="2e6a4-164">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="2e6a4-164">processedDateTime</span></span> | <span data-ttu-id="2e6a4-165">DateTime</span><span class="sxs-lookup"><span data-stu-id="2e6a4-165">DateTime</span></span> | <span data-ttu-id="2e6a4-166">Megadhatja a használati adatok feldolgozásának dátumát.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-166">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="2e6a4-167">Alapértelmezés szerint az adatok feldolgozásának legutóbbi dátuma</span><span class="sxs-lookup"><span data-stu-id="2e6a4-167">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="2e6a4-168">Nem</span><span class="sxs-lookup"><span data-stu-id="2e6a4-168">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="2e6a4-169">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="2e6a4-169">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="2e6a4-170">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2e6a4-170">REST response</span></span>

<span data-ttu-id="2e6a4-171">Sikeres művelet esetén a válasz törzse a következő mezőket tartalmazza, amelyek az üzembe helyezett licencekkel kapcsolatos adatokat tartalmazzák.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-171">If successful, the response body contains the following fields containing data about the licenses deployed.</span></span>

| <span data-ttu-id="2e6a4-172">Mező</span><span class="sxs-lookup"><span data-stu-id="2e6a4-172">Field</span></span>             | <span data-ttu-id="2e6a4-173">Típus</span><span class="sxs-lookup"><span data-stu-id="2e6a4-173">Type</span></span>     | <span data-ttu-id="2e6a4-174">Leírás</span><span class="sxs-lookup"><span data-stu-id="2e6a4-174">Description</span></span>                           |
|-------------------|----------|---------------------------------------|
| <span data-ttu-id="2e6a4-175">serviceCode</span><span class="sxs-lookup"><span data-stu-id="2e6a4-175">serviceCode</span></span>       | <span data-ttu-id="2e6a4-176">sztring</span><span class="sxs-lookup"><span data-stu-id="2e6a4-176">string</span></span>   | <span data-ttu-id="2e6a4-177">Szolgáltatáskód</span><span class="sxs-lookup"><span data-stu-id="2e6a4-177">Service code</span></span>                          |
| <span data-ttu-id="2e6a4-178">serviceName (szolgáltatásnév)</span><span class="sxs-lookup"><span data-stu-id="2e6a4-178">serviceName</span></span>       | <span data-ttu-id="2e6a4-179">sztring</span><span class="sxs-lookup"><span data-stu-id="2e6a4-179">string</span></span>   | <span data-ttu-id="2e6a4-180">Szolgáltatásnév</span><span class="sxs-lookup"><span data-stu-id="2e6a4-180">Service name</span></span>                          |
| <span data-ttu-id="2e6a4-181">Csatorna</span><span class="sxs-lookup"><span data-stu-id="2e6a4-181">channel</span></span>           | <span data-ttu-id="2e6a4-182">sztring</span><span class="sxs-lookup"><span data-stu-id="2e6a4-182">string</span></span>   | <span data-ttu-id="2e6a4-183">Csatorna neve, viszonteladó</span><span class="sxs-lookup"><span data-stu-id="2e6a4-183">Channel name, reseller</span></span>                |
| <span data-ttu-id="2e6a4-184">customerTenantId (customerTenantId)</span><span class="sxs-lookup"><span data-stu-id="2e6a4-184">customerTenantId</span></span>  | <span data-ttu-id="2e6a4-185">sztring</span><span class="sxs-lookup"><span data-stu-id="2e6a4-185">string</span></span>   | <span data-ttu-id="2e6a4-186">Az ügyfél egyedi azonosítója</span><span class="sxs-lookup"><span data-stu-id="2e6a4-186">Unique identifier for the customer</span></span>    |
| <span data-ttu-id="2e6a4-187">customerName (ügyfél neve)</span><span class="sxs-lookup"><span data-stu-id="2e6a4-187">customerName</span></span>      | <span data-ttu-id="2e6a4-188">sztring</span><span class="sxs-lookup"><span data-stu-id="2e6a4-188">string</span></span>   | <span data-ttu-id="2e6a4-189">Ügyfél neve</span><span class="sxs-lookup"><span data-stu-id="2e6a4-189">Customer name</span></span>                         |
| <span data-ttu-id="2e6a4-190">productId</span><span class="sxs-lookup"><span data-stu-id="2e6a4-190">productId</span></span>         | <span data-ttu-id="2e6a4-191">sztring</span><span class="sxs-lookup"><span data-stu-id="2e6a4-191">string</span></span>   | <span data-ttu-id="2e6a4-192">A termék egyedi azonosítója</span><span class="sxs-lookup"><span data-stu-id="2e6a4-192">Unique identifier for the product</span></span>     |
| <span data-ttu-id="2e6a4-193">Productname</span><span class="sxs-lookup"><span data-stu-id="2e6a4-193">productName</span></span>       | <span data-ttu-id="2e6a4-194">sztring</span><span class="sxs-lookup"><span data-stu-id="2e6a4-194">string</span></span>   | <span data-ttu-id="2e6a4-195">Terméknév</span><span class="sxs-lookup"><span data-stu-id="2e6a4-195">Product name</span></span>                          |
| <span data-ttu-id="2e6a4-196">licensesDeployed</span><span class="sxs-lookup"><span data-stu-id="2e6a4-196">licensesDeployed</span></span>  | <span data-ttu-id="2e6a4-197">hosszú</span><span class="sxs-lookup"><span data-stu-id="2e6a4-197">long</span></span>     | <span data-ttu-id="2e6a4-198">Telepített licencek száma</span><span class="sxs-lookup"><span data-stu-id="2e6a4-198">Number of licenses deployed</span></span>           |
| <span data-ttu-id="2e6a4-199">licensesSold</span><span class="sxs-lookup"><span data-stu-id="2e6a4-199">licensesSold</span></span>      | <span data-ttu-id="2e6a4-200">hosszú</span><span class="sxs-lookup"><span data-stu-id="2e6a4-200">long</span></span>     | <span data-ttu-id="2e6a4-201">Eladott licencek száma</span><span class="sxs-lookup"><span data-stu-id="2e6a4-201">Number of licenses sold</span></span>               |
| <span data-ttu-id="2e6a4-202">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="2e6a4-202">processedDateTime</span></span> | <span data-ttu-id="2e6a4-203">DateTime</span><span class="sxs-lookup"><span data-stu-id="2e6a4-203">DateTime</span></span> | <span data-ttu-id="2e6a4-204">Az adatok utolsó feldolgozásának dátuma</span><span class="sxs-lookup"><span data-stu-id="2e6a4-204">Date when the data was last processed</span></span> |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2e6a4-205">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2e6a4-205">Response success and error codes</span></span>

<span data-ttu-id="2e6a4-206">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-206">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2e6a4-207">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="2e6a4-207">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2e6a4-208">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2e6a4-208">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2e6a4-209">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2e6a4-209">Response example</span></span>

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
