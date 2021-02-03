---
title: Számla összegzéseinek lekérése
description: Az egyes pénznemekhez tartozó számla-összefoglaló erőforrások használatával megjelenítheti az ismétlődő és egyszeri költségek egyenlegét és teljes díját.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 82cd669117db72e1819d941f48f8ea69b2eddaec
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767684"
---
# <a name="get-invoice-summaries"></a><span data-ttu-id="c1608-103">Számla összegzéseinek lekérése</span><span class="sxs-lookup"><span data-stu-id="c1608-103">Get invoice summaries</span></span>

<span data-ttu-id="c1608-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="c1608-104">**Applies to:**</span></span>

- <span data-ttu-id="c1608-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="c1608-105">Partner Center</span></span>
- <span data-ttu-id="c1608-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="c1608-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="c1608-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="c1608-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c1608-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="c1608-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c1608-109">A **InvoiceSummaries** lekérheti a számla összegzését, amely az ismétlődő és egyszeri költségek egyenlegét és teljes díját mutatja.</span><span class="sxs-lookup"><span data-stu-id="c1608-109">You can use the **InvoiceSummaries** to retrieve an invoice summary which shows the balance and total charges of both recurring and one-time charges.</span></span> <span data-ttu-id="c1608-110">A **InvoiceSummaries** -erőforrás az egyes pénznemek típusaihoz tartozó számla összegzését tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="c1608-110">The **InvoiceSummaries** resource contains an invoice summary for each currency type.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1608-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c1608-111">Prerequisites</span></span>

- <span data-ttu-id="c1608-112">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="c1608-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c1608-113">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="c1608-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c1608-114">Érvényes fiókazonosító.</span><span class="sxs-lookup"><span data-stu-id="c1608-114">A valid invoice identifier.</span></span>

## <a name="c"></a><span data-ttu-id="c1608-115">C\#</span><span class="sxs-lookup"><span data-stu-id="c1608-115">C\#</span></span>

<span data-ttu-id="c1608-116">Egy olyan [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) -gyűjtemény beolvasása, amely [**InvoiceSummary**](invoice-resources.md#invoicesummary) tartalmaz az egyes pénznemek típusaihoz:</span><span class="sxs-lookup"><span data-stu-id="c1608-116">To retrieve an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) collection that contains an [**InvoiceSummary**](invoice-resources.md#invoicesummary) for each currency type:</span></span>

1. <span data-ttu-id="c1608-117">Az **összegzések** tulajdonság meghívásához használja a **IAggregatePartner. számlák** gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="c1608-117">Use your **IAggregatePartner.Invoices** collection to call the **Summaries** property.</span></span>

2. <span data-ttu-id="c1608-118">Hívja meg a **Get ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="c1608-118">Call the **Get()** method.</span></span>
3. <span data-ttu-id="c1608-119">Egy adott [**InvoiceSummary**](invoice-resources.md#invoicesummary)egyenlegének beszerzéséhez nyissa meg az adott tag **BalanceAmount** tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="c1608-119">To get the balance of an individual [**InvoiceSummary**](invoice-resources.md#invoicesummary), access the **BalanceAmount** property for that member of the collection.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

// Get the invoice summaries collection.
var invoiceSummaries = scopedPartnerOperations.Invoices.Summaries.Get();

// Display the balance on the first invoice summary in the collection.
Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummaries[0].BalanceAmount);
```

<span data-ttu-id="c1608-120">További információkért tekintse meg a következő példában szereplő kódot:</span><span class="sxs-lookup"><span data-stu-id="c1608-120">For more information, see the following example code:</span></span>

- <span data-ttu-id="c1608-121">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="c1608-121">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="c1608-122">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="c1608-122">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="c1608-123">Osztály: **GetInvoiceSummaries.cs**</span><span class="sxs-lookup"><span data-stu-id="c1608-123">Class: **GetInvoiceSummaries.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="c1608-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="c1608-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c1608-125">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="c1608-125">Request syntax</span></span>

| <span data-ttu-id="c1608-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="c1608-126">Method</span></span>  | <span data-ttu-id="c1608-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="c1608-127">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="c1608-128">**GET**</span><span class="sxs-lookup"><span data-stu-id="c1608-128">**GET**</span></span> | <span data-ttu-id="c1608-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/summaries http/1.1</span><span class="sxs-lookup"><span data-stu-id="c1608-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summaries HTTP/1.1</span></span>     |

#### <a name="uri-parameter"></a><span data-ttu-id="c1608-130">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="c1608-130">URI parameter</span></span>

<span data-ttu-id="c1608-131">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="c1608-131">None.</span></span>

### <a name="request-headers"></a><span data-ttu-id="c1608-132">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="c1608-132">Request headers</span></span>

<span data-ttu-id="c1608-133">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c1608-133">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c1608-134">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="c1608-134">Request body</span></span>

<span data-ttu-id="c1608-135">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="c1608-135">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c1608-136">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="c1608-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summaries HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="c1608-137">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="c1608-137">REST response</span></span>

<span data-ttu-id="c1608-138">Ha ez sikeres, ez a metódus egy [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) -erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="c1608-138">If successful, this method returns an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c1608-139">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="c1608-139">Response success and error codes</span></span>

<span data-ttu-id="c1608-140">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="c1608-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c1608-141">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="c1608-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c1608-142">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c1608-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c1608-143">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="c1608-143">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    "totalCount": 3,
    "items": [
        {
            "balanceAmount": 751094.39,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
            "lastPaymentDate": "2017-01-01T12:00:00Z",
            "lastPaymentAmount": 1000,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "Recurring",
                    "summary": {
                        "balanceAmount": 202955.87,
                        "currencyCode": "GBP",
                        "currencySymbol": "£",
                        "accountingDate": "2017-02-27T00:00:00Z",
                        "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
                        "lastPaymentDate": "2017-01-01T12:00:00Z",
                        "lastPaymentAmount": 1000,
                        "latestInvoiceDate": "0001-01-01T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                },
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 548138.52,
                        "currencyCode": "GBP",
                        "currencySymbol": "£",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        },
        {
            "balanceAmount": 1230.33,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2018-03-16T00:00:00",
            "lastPaymentDate": "0001-01-01T00:00:00",
            "lastPaymentAmount": 0,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 1230.33,
                        "currencyCode": "CHF",
                        "currencySymbol": "CHF",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        },
        {
            "balanceAmount": 1001.12,
            "currencyCode": "EUR",
            "currencySymbol": "€",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2018-03-16T00:00:00",
            "lastPaymentDate": "0001-01-01T00:00:00",
            "lastPaymentAmount": 0,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 1001.12,
                        "currencyCode": "EUR",
                        "currencySymbol": "€",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/summaries",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
