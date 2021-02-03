---
title: Az összes Azure-beli használatelemzési adat lekérése
description: Az összes Azure-használati elemzési információ beszerzése.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c281dcdeb93771a69a388ad64e1127b24156c809
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768168"
---
# <a name="get-all-azure-usage-analytics-information"></a><span data-ttu-id="adec3-103">Az összes Azure-beli használatelemzési adat lekérése</span><span class="sxs-lookup"><span data-stu-id="adec3-103">Get all Azure usage analytics information</span></span>

<span data-ttu-id="adec3-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="adec3-104">**Applies To**</span></span>

- <span data-ttu-id="adec3-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="adec3-105">Partner Center</span></span>
- <span data-ttu-id="adec3-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="adec3-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="adec3-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="adec3-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="adec3-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="adec3-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="adec3-109">Az Azure használati elemzési információinak beszerzése az ügyfelek számára.</span><span class="sxs-lookup"><span data-stu-id="adec3-109">How to get all the Azure usage analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adec3-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="adec3-110">Prerequisites</span></span>

- <span data-ttu-id="adec3-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="adec3-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="adec3-112">Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="adec3-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="adec3-113">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="adec3-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="adec3-114">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="adec3-114">Request syntax</span></span>

| <span data-ttu-id="adec3-115">Metódus</span><span class="sxs-lookup"><span data-stu-id="adec3-115">Method</span></span>  | <span data-ttu-id="adec3-116">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="adec3-116">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="adec3-117">**GET**</span><span class="sxs-lookup"><span data-stu-id="adec3-117">**GET**</span></span> | <span data-ttu-id="adec3-118">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Usage/Azure http/1.1</span><span class="sxs-lookup"><span data-stu-id="adec3-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="adec3-119">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="adec3-119">URI parameters</span></span>

|<span data-ttu-id="adec3-120">Paraméter</span><span class="sxs-lookup"><span data-stu-id="adec3-120">Parameter</span></span>        |<span data-ttu-id="adec3-121">Típus</span><span class="sxs-lookup"><span data-stu-id="adec3-121">Type</span></span>                        |<span data-ttu-id="adec3-122">Leírás</span><span class="sxs-lookup"><span data-stu-id="adec3-122">Description</span></span>               |
|:----------------|:---------------------------|:-------------------------|
|<span data-ttu-id="adec3-123">top</span><span class="sxs-lookup"><span data-stu-id="adec3-123">top</span></span>              | <span data-ttu-id="adec3-124">sztring</span><span class="sxs-lookup"><span data-stu-id="adec3-124">string</span></span>                     | <span data-ttu-id="adec3-125">A kérelemben visszaadni kívánt adatsorok száma.</span><span class="sxs-lookup"><span data-stu-id="adec3-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="adec3-126">A maximális érték és az alapértelmezett érték, ha nincs megadva, 10000.</span><span class="sxs-lookup"><span data-stu-id="adec3-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="adec3-127">Ha több sor van a lekérdezésben, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldalának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="adec3-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span>                        |
|<span data-ttu-id="adec3-128">kihagyása</span><span class="sxs-lookup"><span data-stu-id="adec3-128">skip</span></span>             | <span data-ttu-id="adec3-129">int</span><span class="sxs-lookup"><span data-stu-id="adec3-129">int</span></span>                        | <span data-ttu-id="adec3-130">A lekérdezésben kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="adec3-130">The number of rows to skip in the query.</span></span> <span data-ttu-id="adec3-131">Használja ezt a paramétert a nagy adathalmazokon keresztüli lapra.</span><span class="sxs-lookup"><span data-stu-id="adec3-131">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="adec3-132">Például `top=10000 and skip=0` lekéri az első 10000 sornyi adatsort, `top=10000 and skip=10000` lekérdezi a következő 10000 sort, és így tovább.</span><span class="sxs-lookup"><span data-stu-id="adec3-132">For example, `top=10000 and skip=0` retrieves the first 10000 rows of data, `top=10000 and skip=10000` retrieves the next 10000 rows of data, and so on.</span></span>                       |
|<span data-ttu-id="adec3-133">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="adec3-133">filter</span></span>           | <span data-ttu-id="adec3-134">sztring</span><span class="sxs-lookup"><span data-stu-id="adec3-134">string</span></span>                     | <span data-ttu-id="adec3-135">A kérelem *Filter* paraméterében egy vagy több olyan utasítás található, amely a válasz sorait szűri.</span><span class="sxs-lookup"><span data-stu-id="adec3-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="adec3-136">Minden utasítás tartalmaz egy mezőt és egy értéket, amely társítva van az `eq` vagy `ne` operátorhoz, és a utasítások kombinálhatók a vagy a használatával `and` `or` .</span><span class="sxs-lookup"><span data-stu-id="adec3-136">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="adec3-137">A következő karakterláncok megadására van lehetőség:</span><span class="sxs-lookup"><span data-stu-id="adec3-137">You can specify the following strings:</span></span><br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="adec3-138">**Példa**</span><span class="sxs-lookup"><span data-stu-id="adec3-138">**Example:**</span></span><br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> <span data-ttu-id="adec3-139">**Példa**</span><span class="sxs-lookup"><span data-stu-id="adec3-139">**Example:**</span></span><br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|<span data-ttu-id="adec3-140">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="adec3-140">aggregationLevel</span></span> | <span data-ttu-id="adec3-141">sztring</span><span class="sxs-lookup"><span data-stu-id="adec3-141">string</span></span>                    | <span data-ttu-id="adec3-142">Meghatározza azt az időtartományt, amely esetében az összesített adatokat le kell olvasni.</span><span class="sxs-lookup"><span data-stu-id="adec3-142">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="adec3-143">A következő karakterláncok egyike lehet: `day` , `week` , vagy `month` .</span><span class="sxs-lookup"><span data-stu-id="adec3-143">Can be one of the following strings: `day`, `week`, or `month`.</span></span> <span data-ttu-id="adec3-144">Ha nincs megadva, az alapértelmezett érték `day` .</span><span class="sxs-lookup"><span data-stu-id="adec3-144">If unspecified, the default is `day`.</span></span><br/><br/>                                              <span data-ttu-id="adec3-145">A paraméter nem támogatott a (z `aggregationLevel` `groupby` ) nélkül.</span><span class="sxs-lookup"><span data-stu-id="adec3-145">The `aggregationLevel` parameter isn't supported without a `groupby`.</span></span> <span data-ttu-id="adec3-146">A `aggregationLevel` paraméter a összes dátum mezőjére vonatkozik `groupby` .</span><span class="sxs-lookup"><span data-stu-id="adec3-146">The `aggregationLevel` parameter applies to all date fields present in the `groupby`.</span></span>                                                      |
|<span data-ttu-id="adec3-147">OrderBy</span><span class="sxs-lookup"><span data-stu-id="adec3-147">orderby</span></span>          |<span data-ttu-id="adec3-148">sztring</span><span class="sxs-lookup"><span data-stu-id="adec3-148">string</span></span>                     | <span data-ttu-id="adec3-149">Az egyes telepítésekhez tartozó eredmény adatértékeit megrendelő utasítás.</span><span class="sxs-lookup"><span data-stu-id="adec3-149">A statement that orders the result data values for each install.</span></span> <span data-ttu-id="adec3-150">A szintaxis a következő: `...&orderby=field [order],field [order],...`.</span><span class="sxs-lookup"><span data-stu-id="adec3-150">The syntax is `...&orderby=field [order],field [order],...`.</span></span> <span data-ttu-id="adec3-151">A `field` paraméter a következő karakterláncok egyike lehet:</span><span class="sxs-lookup"><span data-stu-id="adec3-151">The `field` parameter can be one of the following strings:</span></span><br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> <span data-ttu-id="adec3-152">A *Order* paraméter nem kötelező, és az `asc` `desc` egyes mezőknél növekvő vagy csökkenő sorrendet adhat meg.</span><span class="sxs-lookup"><span data-stu-id="adec3-152">The *order* parameter is optional and can be `asc` or `desc` to specify ascending or descending order for each field, respectively.</span></span> <span data-ttu-id="adec3-153">A mező alapértelmezett értéke: `asc`.</span><span class="sxs-lookup"><span data-stu-id="adec3-153">The default is `asc`.</span></span><br/><br/><span data-ttu-id="adec3-154">**Példa**</span><span class="sxs-lookup"><span data-stu-id="adec3-154">**Example:**</span></span><br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|<span data-ttu-id="adec3-155">groupby</span><span class="sxs-lookup"><span data-stu-id="adec3-155">groupby</span></span>          |<span data-ttu-id="adec3-156">sztring</span><span class="sxs-lookup"><span data-stu-id="adec3-156">string</span></span>                    | <span data-ttu-id="adec3-157">Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítést.</span><span class="sxs-lookup"><span data-stu-id="adec3-157">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="adec3-158">A következő mezőket adhatja meg:</span><span class="sxs-lookup"><span data-stu-id="adec3-158">You can specify the following fields:</span></span><br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="adec3-159">A visszaadott adatsorok tartalmazzák a paraméterben megadott mezőket `groupby`  és a *mennyiséget*.</span><span class="sxs-lookup"><span data-stu-id="adec3-159">The returned data rows will contain the fields specified in the `groupby`  parameter as well as the *Quantity*.</span></span><br/><br/><span data-ttu-id="adec3-160">A `groupby` paraméter használható a `aggregationLevel` paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="adec3-160">The `groupby` parameter can be used with the `aggregationLevel` parameter.</span></span><br/><br/><span data-ttu-id="adec3-161">**Példa**</span><span class="sxs-lookup"><span data-stu-id="adec3-161">**Example:**</span></span><br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a><span data-ttu-id="adec3-162">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="adec3-162">Request headers</span></span>

<span data-ttu-id="adec3-163">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="adec3-163">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="adec3-164">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="adec3-164">Request body</span></span>

<span data-ttu-id="adec3-165">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="adec3-165">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="adec3-166">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="adec3-166">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="adec3-167">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="adec3-167">REST response</span></span>

<span data-ttu-id="adec3-168">Ha ez sikeres, a válasz törzse az [Azure használati](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) erőforrásainak gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="adec3-168">If successful, the response body contains a collection of [Azure usage](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="adec3-169">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="adec3-169">Response success and error codes</span></span>

<span data-ttu-id="adec3-170">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="adec3-170">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="adec3-171">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="adec3-171">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="adec3-172">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="adec3-172">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="adec3-173">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="adec3-173">Response example</span></span>

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20
}
```

## <a name="see-also"></a><span data-ttu-id="adec3-174">Lásd még</span><span class="sxs-lookup"><span data-stu-id="adec3-174">See also</span></span>

- [<span data-ttu-id="adec3-175">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="adec3-175">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
