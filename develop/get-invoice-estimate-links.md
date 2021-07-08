---
title: Számlabecslés hivatkozásainak lekérése
description: A lekérdezés egyeztetési sorelemének részleteire mutató becslési hivatkozások gyűjteményét is lekérdezheti.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.assetid: ''
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 719becd3fac5605c4ad48ab86d483ba7903d65d8
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549144"
---
# <a name="get-invoice-estimate-links"></a><span data-ttu-id="42791-103">Számlabecslés hivatkozásainak lekérése</span><span class="sxs-lookup"><span data-stu-id="42791-103">Get invoice estimate links</span></span>

<span data-ttu-id="42791-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="42791-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="42791-105">A nem kiszámlázatlan egyeztetési sorelemek lekérdezési részleteinek lekérdezéséhez becslési hivatkozásokat is kaphat.</span><span class="sxs-lookup"><span data-stu-id="42791-105">You can get estimate links to help query details for unbilled reconciliation line items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42791-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="42791-106">Prerequisites</span></span>

- <span data-ttu-id="42791-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="42791-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="42791-108">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="42791-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="42791-109">Egy számlaazonosító.</span><span class="sxs-lookup"><span data-stu-id="42791-109">An invoice identifier.</span></span> <span data-ttu-id="42791-110">Ez azonosítja a számlát, amelynek lekéri a sorelemeket.</span><span class="sxs-lookup"><span data-stu-id="42791-110">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="42791-111">C\#</span><span class="sxs-lookup"><span data-stu-id="42791-111">C\#</span></span>

<span data-ttu-id="42791-112">Az alábbi példakód bemutatja, hogyan lehet lekérdezni a nem kiszámlázatlan sorelemek lekérdezésére mutató becslési hivatkozásokat egy adott pénznemre.</span><span class="sxs-lookup"><span data-stu-id="42791-112">The following example code shows how you can get the estimate links to query unbilled line items for a given currency.</span></span> <span data-ttu-id="42791-113">A válasz tartalmazza az egyes időtartamok (például az aktuális és az előző hónap) becslési hivatkozását.</span><span class="sxs-lookup"><span data-stu-id="42791-113">The response contains the estimate links for each period (for example, the current and previous month).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;

 // all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
 IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read estimate links for currencycode
var estimateLinks = scopedPartnerOperations.Invoices.Estimates.Links.ByCurrency(curencyCode).Get();
```

<span data-ttu-id="42791-114">Hasonló példát a következőben láthat:</span><span class="sxs-lookup"><span data-stu-id="42791-114">For a similar example, see the following:</span></span>

- <span data-ttu-id="42791-115">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="42791-115">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="42791-116">Project: **Partnerközpont SDK minták**</span><span class="sxs-lookup"><span data-stu-id="42791-116">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="42791-117">Osztály: **GetEstimatesLinks.cs**</span><span class="sxs-lookup"><span data-stu-id="42791-117">Class: **GetEstimatesLinks.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="42791-118">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="42791-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="42791-119">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="42791-119">Request syntax</span></span>

| <span data-ttu-id="42791-120">Metódus</span><span class="sxs-lookup"><span data-stu-id="42791-120">Method</span></span>  | <span data-ttu-id="42791-121">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="42791-121">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="42791-122">**Kap**</span><span class="sxs-lookup"><span data-stu-id="42791-122">**GET**</span></span> | <span data-ttu-id="42791-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/estimates/links?currencycode={currencycode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="42791-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/estimates/links?currencycode={currencycode} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="42791-124">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="42791-124">URI parameters</span></span>

<span data-ttu-id="42791-125">A kérelem létrehozásakor használja a következő URI-t és lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="42791-125">Use the following URI and query parameter when creating the request.</span></span>

| <span data-ttu-id="42791-126">Név</span><span class="sxs-lookup"><span data-stu-id="42791-126">Name</span></span>                   | <span data-ttu-id="42791-127">Típus</span><span class="sxs-lookup"><span data-stu-id="42791-127">Type</span></span>   | <span data-ttu-id="42791-128">Kötelező</span><span class="sxs-lookup"><span data-stu-id="42791-128">Required</span></span> | <span data-ttu-id="42791-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="42791-129">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="42791-130">currencyCode</span><span class="sxs-lookup"><span data-stu-id="42791-130">currencyCode</span></span>           | <span data-ttu-id="42791-131">sztring</span><span class="sxs-lookup"><span data-stu-id="42791-131">string</span></span> | <span data-ttu-id="42791-132">Igen</span><span class="sxs-lookup"><span data-stu-id="42791-132">Yes</span></span>      | <span data-ttu-id="42791-133">A ki nemszámlázatlan sorelemek pénznemkódja.</span><span class="sxs-lookup"><span data-stu-id="42791-133">The currency code for the unbilled line items.</span></span>                    |

### <a name="request-headers"></a><span data-ttu-id="42791-134">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="42791-134">Request headers</span></span>

<span data-ttu-id="42791-135">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="42791-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="42791-136">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="42791-136">Request body</span></span>

<span data-ttu-id="42791-137">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="42791-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="42791-138">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="42791-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/estimates/links?currencycode=usd HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="42791-139">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="42791-139">REST response</span></span>

<span data-ttu-id="42791-140">Ha ez sikeres, a válasz tartalmazza a nemszámlázatlan becslések lekérésének hivatkozását.</span><span class="sxs-lookup"><span data-stu-id="42791-140">If successful, the response contains the links to retrieve unbilled estimates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="42791-141">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="42791-141">Response success and error codes</span></span>

<span data-ttu-id="42791-142">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="42791-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="42791-143">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="42791-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="42791-144">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="42791-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="42791-145">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="42791-145">Response example</span></span>

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
