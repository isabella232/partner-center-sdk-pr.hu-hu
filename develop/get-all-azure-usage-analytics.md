---
title: Az összes Azure-beli használatelemzési adat lekérése
description: Az Azure használatelemzési információinak lekért használata.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 7fe987c7dc50d55b26cd72d5aead52963eb1cfbe
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760215"
---
# <a name="get-all-azure-usage-analytics-information"></a><span data-ttu-id="ca588-103">Az összes Azure-beli használatelemzési adat lekérése</span><span class="sxs-lookup"><span data-stu-id="ca588-103">Get all Azure usage analytics information</span></span>

<span data-ttu-id="ca588-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ca588-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ca588-105">Az Azure használatelemzési információinak lekért használata az ügyfelek számára.</span><span class="sxs-lookup"><span data-stu-id="ca588-105">How to get all the Azure usage analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca588-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="ca588-106">Prerequisites</span></span>

- <span data-ttu-id="ca588-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ca588-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ca588-108">Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="ca588-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ca588-109">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="ca588-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ca588-110">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="ca588-110">Request syntax</span></span>

| <span data-ttu-id="ca588-111">Metódus</span><span class="sxs-lookup"><span data-stu-id="ca588-111">Method</span></span>  | <span data-ttu-id="ca588-112">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="ca588-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="ca588-113">**Kap**</span><span class="sxs-lookup"><span data-stu-id="ca588-113">**GET**</span></span> | <span data-ttu-id="ca588-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ca588-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="ca588-115">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="ca588-115">URI parameters</span></span>

|<span data-ttu-id="ca588-116">Paraméter</span><span class="sxs-lookup"><span data-stu-id="ca588-116">Parameter</span></span>        |<span data-ttu-id="ca588-117">Típus</span><span class="sxs-lookup"><span data-stu-id="ca588-117">Type</span></span>                        |<span data-ttu-id="ca588-118">Leírás</span><span class="sxs-lookup"><span data-stu-id="ca588-118">Description</span></span>               |
|:----------------|:---------------------------|:-------------------------|
|<span data-ttu-id="ca588-119">top</span><span class="sxs-lookup"><span data-stu-id="ca588-119">top</span></span>              | <span data-ttu-id="ca588-120">sztring</span><span class="sxs-lookup"><span data-stu-id="ca588-120">string</span></span>                     | <span data-ttu-id="ca588-121">A kérelemben visszaadni kívánt adatsorok száma.</span><span class="sxs-lookup"><span data-stu-id="ca588-121">The number of rows of data to return in the request.</span></span> <span data-ttu-id="ca588-122">Ha nincs megadva, a maximális érték és az alapértelmezett érték 10000.</span><span class="sxs-lookup"><span data-stu-id="ca588-122">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="ca588-123">Ha a lekérdezés több sort tartalmaz, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldal lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="ca588-123">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span>                        |
|<span data-ttu-id="ca588-124">Ugrál</span><span class="sxs-lookup"><span data-stu-id="ca588-124">skip</span></span>             | <span data-ttu-id="ca588-125">int</span><span class="sxs-lookup"><span data-stu-id="ca588-125">int</span></span>                        | <span data-ttu-id="ca588-126">A lekérdezésben kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="ca588-126">The number of rows to skip in the query.</span></span> <span data-ttu-id="ca588-127">Ezzel a paraméterrel nagy adatkészletek között lapokat laposszunk.</span><span class="sxs-lookup"><span data-stu-id="ca588-127">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="ca588-128">A például lekéri az első 10 000 adatsort, lekéri a következő `top=10000 and skip=0` `top=10000 and skip=10000` 10000 adatsort és így tovább.</span><span class="sxs-lookup"><span data-stu-id="ca588-128">For example, `top=10000 and skip=0` retrieves the first 10000 rows of data, `top=10000 and skip=10000` retrieves the next 10000 rows of data, and so on.</span></span>                       |
|<span data-ttu-id="ca588-129">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="ca588-129">filter</span></span>           | <span data-ttu-id="ca588-130">sztring</span><span class="sxs-lookup"><span data-stu-id="ca588-130">string</span></span>                     | <span data-ttu-id="ca588-131">A *kérés* szűrőparamétere egy vagy több olyan utasításokat tartalmaz, amelyek szűrik a válasz sorait.</span><span class="sxs-lookup"><span data-stu-id="ca588-131">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="ca588-132">Minden utasítás tartalmaz egy mezőt és egy értéket, amely az vagy operátorhoz van társítva, és az utasítások kombinálhatók `eq` `ne` a vagy a `and` `or` használatával.</span><span class="sxs-lookup"><span data-stu-id="ca588-132">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="ca588-133">A következő sztringeket adhatja meg:</span><span class="sxs-lookup"><span data-stu-id="ca588-133">You can specify the following strings:</span></span><br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="ca588-134">**Példa**</span><span class="sxs-lookup"><span data-stu-id="ca588-134">**Example:**</span></span><br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> <span data-ttu-id="ca588-135">**Példa**</span><span class="sxs-lookup"><span data-stu-id="ca588-135">**Example:**</span></span><br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|<span data-ttu-id="ca588-136">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="ca588-136">aggregationLevel</span></span> | <span data-ttu-id="ca588-137">sztring</span><span class="sxs-lookup"><span data-stu-id="ca588-137">string</span></span>                    | <span data-ttu-id="ca588-138">Megadja az összesített adatok lekérésének időtartományát.</span><span class="sxs-lookup"><span data-stu-id="ca588-138">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="ca588-139">A következő sztringek egyike lehet: `day` , `week` vagy `month` .</span><span class="sxs-lookup"><span data-stu-id="ca588-139">Can be one of the following strings: `day`, `week`, or `month`.</span></span> <span data-ttu-id="ca588-140">Ha nincs meghatározva, az alapértelmezett érték `day` a .</span><span class="sxs-lookup"><span data-stu-id="ca588-140">If unspecified, the default is `day`.</span></span><br/><br/>                                              <span data-ttu-id="ca588-141">A `aggregationLevel` paraméter nem támogatott a `groupby` nélkül.</span><span class="sxs-lookup"><span data-stu-id="ca588-141">The `aggregationLevel` parameter isn't supported without a `groupby`.</span></span> <span data-ttu-id="ca588-142">A `aggregationLevel` paraméter a összes, a-ban található dátummezőre vonatkozik. `groupby`</span><span class="sxs-lookup"><span data-stu-id="ca588-142">The `aggregationLevel` parameter applies to all date fields present in the `groupby`.</span></span>                                                      |
|<span data-ttu-id="ca588-143">orderby</span><span class="sxs-lookup"><span data-stu-id="ca588-143">orderby</span></span>          |<span data-ttu-id="ca588-144">sztring</span><span class="sxs-lookup"><span data-stu-id="ca588-144">string</span></span>                     | <span data-ttu-id="ca588-145">Az egyes telepítések eredményadatértékeit megrendelő utasítás.</span><span class="sxs-lookup"><span data-stu-id="ca588-145">A statement that orders the result data values for each install.</span></span> <span data-ttu-id="ca588-146">A szintaxis a következő: `...&orderby=field [order],field [order],...`.</span><span class="sxs-lookup"><span data-stu-id="ca588-146">The syntax is `...&orderby=field [order],field [order],...`.</span></span> <span data-ttu-id="ca588-147">A `field` paraméter a következő sztringek egyike lehet:</span><span class="sxs-lookup"><span data-stu-id="ca588-147">The `field` parameter can be one of the following strings:</span></span><br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> <span data-ttu-id="ca588-148">A *rendelési* paraméter megadása nem kötelező, és a értéke vagy lehet, ha növekvő vagy csökkenő sorrendet ad meg az `asc` egyes `desc` mezőkhöz.</span><span class="sxs-lookup"><span data-stu-id="ca588-148">The *order* parameter is optional and can be `asc` or `desc` to specify ascending or descending order for each field, respectively.</span></span> <span data-ttu-id="ca588-149">A mező alapértelmezett értéke: `asc`.</span><span class="sxs-lookup"><span data-stu-id="ca588-149">The default is `asc`.</span></span><br/><br/><span data-ttu-id="ca588-150">**Példa**</span><span class="sxs-lookup"><span data-stu-id="ca588-150">**Example:**</span></span><br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|<span data-ttu-id="ca588-151">groupby</span><span class="sxs-lookup"><span data-stu-id="ca588-151">groupby</span></span>          |<span data-ttu-id="ca588-152">sztring</span><span class="sxs-lookup"><span data-stu-id="ca588-152">string</span></span>                    | <span data-ttu-id="ca588-153">Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítőt.</span><span class="sxs-lookup"><span data-stu-id="ca588-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="ca588-154">A következő mezőket adhatja meg:</span><span class="sxs-lookup"><span data-stu-id="ca588-154">You can specify the following fields:</span></span><br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="ca588-155">A visszaadott adatsorok tartalmazzák a paraméterben és a Quantity mezőben `groupby` megadott *mezőket.*</span><span class="sxs-lookup"><span data-stu-id="ca588-155">The returned data rows will contain the fields specified in the `groupby`  parameter and the *Quantity*.</span></span><br/><br/><span data-ttu-id="ca588-156">A `groupby` paraméter a paraméterrel együtt `aggregationLevel` használható.</span><span class="sxs-lookup"><span data-stu-id="ca588-156">The `groupby` parameter can be used with the `aggregationLevel` parameter.</span></span><br/><br/><span data-ttu-id="ca588-157">**Példa**</span><span class="sxs-lookup"><span data-stu-id="ca588-157">**Example:**</span></span><br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a><span data-ttu-id="ca588-158">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="ca588-158">Request headers</span></span>

<span data-ttu-id="ca588-159">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ca588-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ca588-160">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="ca588-160">Request body</span></span>

<span data-ttu-id="ca588-161">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="ca588-161">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ca588-162">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ca588-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="ca588-163">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="ca588-163">REST response</span></span>

<span data-ttu-id="ca588-164">Ha ez sikeres, a válasz törzse azure-beli [használati erőforrások gyűjteményét](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="ca588-164">If successful, the response body contains a collection of [Azure usage](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ca588-165">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="ca588-165">Response success and error codes</span></span>

<span data-ttu-id="ca588-166">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="ca588-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ca588-167">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="ca588-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ca588-168">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ca588-168">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ca588-169">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ca588-169">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="ca588-170">Lásd még</span><span class="sxs-lookup"><span data-stu-id="ca588-170">See also</span></span>

- [<span data-ttu-id="ca588-171">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="ca588-171">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
