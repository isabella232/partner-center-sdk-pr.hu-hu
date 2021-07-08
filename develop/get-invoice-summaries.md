---
title: Számla összegzéseinek lekérése
description: A számlaösszegző erőforrást minden pénznemtípushoz használhatja az ismétlődő és egyszeri díjak egyenlegének és teljes díjának a megjelenítése érdekében.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: fb6ff839c56c7b0b77a9904abf05d95ca0500b00
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549110"
---
# <a name="get-invoice-summaries"></a><span data-ttu-id="17a92-103">Számla összegzéseinek lekérése</span><span class="sxs-lookup"><span data-stu-id="17a92-103">Get invoice summaries</span></span>

<span data-ttu-id="17a92-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="17a92-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="17a92-105">Az **InvoiceSummaries** segítségével lekérhet egy számlaösszegzést, amely az ismétlődő és egyszeri díjak egyenlegét és teljes díjait jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="17a92-105">You can use the **InvoiceSummaries** to retrieve an invoice summary that shows the balance and total charges of both recurring and one-time charges.</span></span> <span data-ttu-id="17a92-106">Az **InvoiceSummaries erőforrás** minden pénznemtípushoz tartalmaz egy számlaösszegzést.</span><span class="sxs-lookup"><span data-stu-id="17a92-106">The **InvoiceSummaries** resource contains an invoice summary for each currency type.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17a92-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="17a92-107">Prerequisites</span></span>

- <span data-ttu-id="17a92-108">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="17a92-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="17a92-109">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="17a92-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="17a92-110">Egy érvényes számlaazonosító.</span><span class="sxs-lookup"><span data-stu-id="17a92-110">A valid invoice identifier.</span></span>

## <a name="c"></a><span data-ttu-id="17a92-111">C\#</span><span class="sxs-lookup"><span data-stu-id="17a92-111">C\#</span></span>

<span data-ttu-id="17a92-112">Egy [**InvoiceSummaries gyűjtemény lekérése,**](invoice-resources.md#invoicesummaries) amely az egyes pénznemtípushoz tartozó [**InvoiceSummary**](invoice-resources.md#invoicesummary) adatokat tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="17a92-112">To retrieve an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) collection that contains an [**InvoiceSummary**](invoice-resources.md#invoicesummary) for each currency type:</span></span>

1. <span data-ttu-id="17a92-113">Használja az **IAggregatePartner.Invoices gyűjteményt** az **Summaries tulajdonság hívására.**</span><span class="sxs-lookup"><span data-stu-id="17a92-113">Use your **IAggregatePartner.Invoices** collection to call the **Summaries** property.</span></span>

2. <span data-ttu-id="17a92-114">Hívja meg a **Get() metódust.**</span><span class="sxs-lookup"><span data-stu-id="17a92-114">Call the **Get()** method.</span></span>
3. <span data-ttu-id="17a92-115">Egy önálló [**InvoiceSummary egyenlegének lekért összegéhez a**](invoice-resources.md#invoicesummary)gyűjtemény adott tagját kell elérnie a **BalanceAmount** tulajdonsághoz.</span><span class="sxs-lookup"><span data-stu-id="17a92-115">To get the balance of an individual [**InvoiceSummary**](invoice-resources.md#invoicesummary), access the **BalanceAmount** property for that member of the collection.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

// Get the invoice summaries collection.
var invoiceSummaries = scopedPartnerOperations.Invoices.Summaries.Get();

// Display the balance on the first invoice summary in the collection.
Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummaries[0].BalanceAmount);
```

<span data-ttu-id="17a92-116">További információért tekintse meg az alábbi példakódot:</span><span class="sxs-lookup"><span data-stu-id="17a92-116">For more information, see the following example code:</span></span>

- <span data-ttu-id="17a92-117">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="17a92-117">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="17a92-118">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="17a92-118">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="17a92-119">Osztály: **GetInvoiceSummaries.cs**</span><span class="sxs-lookup"><span data-stu-id="17a92-119">Class: **GetInvoiceSummaries.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="17a92-120">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="17a92-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="17a92-121">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="17a92-121">Request syntax</span></span>

| <span data-ttu-id="17a92-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="17a92-122">Method</span></span>  | <span data-ttu-id="17a92-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="17a92-123">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="17a92-124">**Kap**</span><span class="sxs-lookup"><span data-stu-id="17a92-124">**GET**</span></span> | <span data-ttu-id="17a92-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summaries HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="17a92-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summaries HTTP/1.1</span></span>     |

#### <a name="uri-parameter"></a><span data-ttu-id="17a92-126">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="17a92-126">URI parameter</span></span>

<span data-ttu-id="17a92-127">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="17a92-127">None.</span></span>

### <a name="request-headers"></a><span data-ttu-id="17a92-128">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="17a92-128">Request headers</span></span>

<span data-ttu-id="17a92-129">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="17a92-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="17a92-130">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="17a92-130">Request body</span></span>

<span data-ttu-id="17a92-131">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="17a92-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="17a92-132">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="17a92-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summaries HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="17a92-133">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="17a92-133">REST response</span></span>

<span data-ttu-id="17a92-134">Ha a művelet sikeres, ez a metódus egy [**InvoiceSummaries erőforrást**](invoice-resources.md#invoicesummaries) ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="17a92-134">If successful, this method returns an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="17a92-135">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="17a92-135">Response success and error codes</span></span>

<span data-ttu-id="17a92-136">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="17a92-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="17a92-137">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="17a92-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="17a92-138">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="17a92-138">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="17a92-139">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="17a92-139">Response example</span></span>

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
