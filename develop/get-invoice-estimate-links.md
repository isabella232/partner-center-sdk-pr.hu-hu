---
title: Számlabecslés hivatkozásainak lekérése
description: A lekérdezési egyeztetési sor részleteire vonatkozó becsült hivatkozások gyűjteményét lekérheti.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.assetid: ''
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 10801cdb1f9d4f50a1f8fc86c2d0eaf8610ed68c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767887"
---
# <a name="get-invoice-estimate-links"></a><span data-ttu-id="562dc-103">Számlabecslés hivatkozásainak lekérése</span><span class="sxs-lookup"><span data-stu-id="562dc-103">Get invoice estimate links</span></span>

<span data-ttu-id="562dc-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="562dc-104">**Applies to:**</span></span>

- <span data-ttu-id="562dc-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="562dc-105">Partner Center</span></span>
- <span data-ttu-id="562dc-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="562dc-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="562dc-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="562dc-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="562dc-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="562dc-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="562dc-109">A becslési hivatkozásokra kattintva megtekintheti a nem számlázott egyeztetési sorok részleteinek lekérdezését.</span><span class="sxs-lookup"><span data-stu-id="562dc-109">You can get estimate links to help query details for unbilled reconciliation line items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="562dc-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="562dc-110">Prerequisites</span></span>

- <span data-ttu-id="562dc-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="562dc-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="562dc-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="562dc-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="562dc-113">Egy fiókazonosító.</span><span class="sxs-lookup"><span data-stu-id="562dc-113">An invoice identifier.</span></span> <span data-ttu-id="562dc-114">Ez azonosítja azt a számlát, amelynek a sorát be kell olvasni.</span><span class="sxs-lookup"><span data-stu-id="562dc-114">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="562dc-115">C\#</span><span class="sxs-lookup"><span data-stu-id="562dc-115">C\#</span></span>

<span data-ttu-id="562dc-116">Az alábbi mintakód bemutatja, hogyan kérheti le a becslési hivatkozásokat egy adott pénznemhez tartozó nem számlázott sorok lekérdezéséhez.</span><span class="sxs-lookup"><span data-stu-id="562dc-116">The following example code shows how you can get the estimate links to query unbilled line items for a given currency.</span></span> <span data-ttu-id="562dc-117">A válasz tartalmazza az egyes időszakok becsült hivatkozásait (például az aktuális és az előző hónapot).</span><span class="sxs-lookup"><span data-stu-id="562dc-117">The response contains the estimate links for each period (for example, the current and previous month).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;

 // all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
 IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read estimate links for currencycode
var estimateLinks = scopedPartnerOperations.Invoices.Estimates.Links.ByCurrency(curencyCode).Get();
```

<span data-ttu-id="562dc-118">Ehhez hasonló példát a következő témakörben talál:</span><span class="sxs-lookup"><span data-stu-id="562dc-118">For a similar example, see the following:</span></span>

- <span data-ttu-id="562dc-119">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="562dc-119">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="562dc-120">Projekt: **partner Center SDK-minták**</span><span class="sxs-lookup"><span data-stu-id="562dc-120">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="562dc-121">Osztály: **GetEstimatesLinks.cs**</span><span class="sxs-lookup"><span data-stu-id="562dc-121">Class: **GetEstimatesLinks.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="562dc-122">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="562dc-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="562dc-123">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="562dc-123">Request syntax</span></span>

| <span data-ttu-id="562dc-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="562dc-124">Method</span></span>  | <span data-ttu-id="562dc-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="562dc-125">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="562dc-126">**GET**</span><span class="sxs-lookup"><span data-stu-id="562dc-126">**GET**</span></span> | <span data-ttu-id="562dc-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/Estimates/Links? CurrencyCode = {CURRENCYCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="562dc-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/estimates/links?currencycode={currencycode} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="562dc-128">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="562dc-128">URI parameters</span></span>

<span data-ttu-id="562dc-129">A kérelem létrehozásakor használja a következő URI és lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="562dc-129">Use the following URI and query parameter when creating the request.</span></span>

| <span data-ttu-id="562dc-130">Név</span><span class="sxs-lookup"><span data-stu-id="562dc-130">Name</span></span>                   | <span data-ttu-id="562dc-131">Típus</span><span class="sxs-lookup"><span data-stu-id="562dc-131">Type</span></span>   | <span data-ttu-id="562dc-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="562dc-132">Required</span></span> | <span data-ttu-id="562dc-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="562dc-133">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="562dc-134">currencyCode</span><span class="sxs-lookup"><span data-stu-id="562dc-134">currencyCode</span></span>           | <span data-ttu-id="562dc-135">sztring</span><span class="sxs-lookup"><span data-stu-id="562dc-135">string</span></span> | <span data-ttu-id="562dc-136">Igen</span><span class="sxs-lookup"><span data-stu-id="562dc-136">Yes</span></span>      | <span data-ttu-id="562dc-137">A nem számlázott sorok pénznemkódja.</span><span class="sxs-lookup"><span data-stu-id="562dc-137">The currency code for the unbilled line items.</span></span>                    |

### <a name="request-headers"></a><span data-ttu-id="562dc-138">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="562dc-138">Request headers</span></span>

<span data-ttu-id="562dc-139">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="562dc-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="562dc-140">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="562dc-140">Request body</span></span>

<span data-ttu-id="562dc-141">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="562dc-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="562dc-142">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="562dc-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/estimates/links?currencycode=usd HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="562dc-143">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="562dc-143">REST response</span></span>

<span data-ttu-id="562dc-144">Ha a művelet sikeres, a válasz tartalmazza a nem számlázott becslések beolvasására vonatkozó hivatkozásokat.</span><span class="sxs-lookup"><span data-stu-id="562dc-144">If successful, the response contains the links to retrieve unbilled estimates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="562dc-145">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="562dc-145">Response success and error codes</span></span>

<span data-ttu-id="562dc-146">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="562dc-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="562dc-147">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="562dc-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="562dc-148">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="562dc-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="562dc-149">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="562dc-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 80EAA055-B5D3-4D88-BFE8-924A3F706462
MS-RequestId: 1b18689e-3fe3-4fdb-d09e-39d13941390b
X-Locale: en-US
X-SourceFiles: =?UTF-8?B?RDpcU291cmNlc1xSUEUuUGFydG5lci5TZXJ2aWNlLkJpbGxpbmdTZXJ2aWNlXHYxLjFcV2ViQXBpc1xCaWxsaW5nU2VydmljZS5WMi5XZWJcdjFcaW52b2ljZXNcZXN0aW1hdGVzXGxpbmtz?=
X-Powered-By: ASP.NET
Date: Thu, 14 Mar 2019 18:15:06 GMT
Content-Length: 1857

{
  "totalCount": 4,
  "items": [
    {
      "type": "daily_rated_usage",
      "title": "Daily rated usage unbilled",
      "description": "This invoice line items includes unbilled consumption based data only.",
      "period": "Current",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=Marketplace&invoicelineitemtype=UsageLineItems&currencycode=USD&period=current&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "daily_rated_usage",
      "title": "Daily rated usage unbilled",
      "description": "This invoice line items includes unbilled consumption based data only.",
      "period": "Previous",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=Marketplace&invoicelineitemtype=UsageLineItems&currencycode=USD&period=previous&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "non_consumption",
      "title": "Unbilled reconciliation line items",
      "description": "This includes reconciliation line items for unbilled data only.",
      "period": "Current",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=USD&period=current&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "non_consumption",
      "title": "Unbilled reconciliation line items",
      "description": "This includes reconciliation line items for unbilled data only.",
      "period": "Previous",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=USD&period=previous&size=2000",
        "method": "GET",
        "headers": []
      }
    }
  ],
  "attributes": {
    "objectType": "Collection"
 }
}
```
