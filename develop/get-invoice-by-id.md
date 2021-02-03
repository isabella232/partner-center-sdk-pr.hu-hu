---
title: Számla beolvasása azonosító alapján
description: Egy adott számla beolvasása a számla azonosítója alapján.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 17880265d06e8e5eaacc5470d83c49defd10ad51
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767687"
---
# <a name="get-invoice-by-id"></a><span data-ttu-id="8d79d-103">Számla beolvasása azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="8d79d-103">Get invoice by ID</span></span>

<span data-ttu-id="8d79d-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="8d79d-104">**Applies to:**</span></span>

- <span data-ttu-id="8d79d-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="8d79d-105">Partner Center</span></span>
- <span data-ttu-id="8d79d-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="8d79d-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8d79d-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="8d79d-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8d79d-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="8d79d-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8d79d-109">Egy adott számla beolvasása a számla azonosítója alapján.</span><span class="sxs-lookup"><span data-stu-id="8d79d-109">Retrieves a given invoice using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d79d-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8d79d-110">Prerequisites</span></span>

- <span data-ttu-id="8d79d-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="8d79d-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8d79d-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="8d79d-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="8d79d-113">Érvényes számla-azonosító.</span><span class="sxs-lookup"><span data-stu-id="8d79d-113">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="8d79d-114">C\#</span><span class="sxs-lookup"><span data-stu-id="8d79d-114">C\#</span></span>

<span data-ttu-id="8d79d-115">Számla beszerzése azonosító alapján:</span><span class="sxs-lookup"><span data-stu-id="8d79d-115">To get an invoice by ID:</span></span>

1. <span data-ttu-id="8d79d-116">Használja a **IPartner. számlákon** gyűjteményt, és hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="8d79d-116">Use your **IPartner.Invoices** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="8d79d-117">Hívja meg a **Get ()** vagy a **GetAsync ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="8d79d-117">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoice = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Get();
```

<span data-ttu-id="8d79d-118">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8d79d-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8d79d-119">**Projekt**: PartnerSDK. FeatureSample **osztály**: GetInvoice.cs</span><span class="sxs-lookup"><span data-stu-id="8d79d-119">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8d79d-120">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="8d79d-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8d79d-121">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="8d79d-121">Request syntax</span></span>

| <span data-ttu-id="8d79d-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="8d79d-122">Method</span></span>  | <span data-ttu-id="8d79d-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="8d79d-123">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="8d79d-124">**GET**</span><span class="sxs-lookup"><span data-stu-id="8d79d-124">**GET**</span></span> | <span data-ttu-id="8d79d-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="8d79d-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="8d79d-126">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="8d79d-126">URI parameter</span></span>

<span data-ttu-id="8d79d-127">A számla beszerzéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="8d79d-127">Use the following query parameter to get the invoice.</span></span>

| <span data-ttu-id="8d79d-128">Név</span><span class="sxs-lookup"><span data-stu-id="8d79d-128">Name</span></span>           | <span data-ttu-id="8d79d-129">Típus</span><span class="sxs-lookup"><span data-stu-id="8d79d-129">Type</span></span>       | <span data-ttu-id="8d79d-130">Kötelező</span><span class="sxs-lookup"><span data-stu-id="8d79d-130">Required</span></span> | <span data-ttu-id="8d79d-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="8d79d-131">Description</span></span>                                                                                        |
|----------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8d79d-132">**számlázási azonosító**</span><span class="sxs-lookup"><span data-stu-id="8d79d-132">**invoice-id**</span></span> | <span data-ttu-id="8d79d-133">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="8d79d-133">**string**</span></span> | <span data-ttu-id="8d79d-134">Igen</span><span class="sxs-lookup"><span data-stu-id="8d79d-134">Yes</span></span>      | <span data-ttu-id="8d79d-135">Az érték egy **Számlázási azonosító** , amely lehetővé teszi, hogy a viszonteladó egy adott számla eredményét szűrje.</span><span class="sxs-lookup"><span data-stu-id="8d79d-135">The value is an **invoice-id** that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8d79d-136">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="8d79d-136">Request headers</span></span>

<span data-ttu-id="8d79d-137">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8d79d-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8d79d-138">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="8d79d-138">Request body</span></span>

<span data-ttu-id="8d79d-139">Nincs</span><span class="sxs-lookup"><span data-stu-id="8d79d-139">None</span></span>

### <a name="request-example"></a><span data-ttu-id="8d79d-140">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8d79d-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="8d79d-141">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="8d79d-141">REST response</span></span>

<span data-ttu-id="8d79d-142">Ha ez sikeres, ez a metódus egy [Számlázási](invoice-resources.md#invoice) erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="8d79d-142">If successful, this method returns an [Invoice](invoice-resources.md#invoice) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8d79d-143">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="8d79d-143">Response success and error codes</span></span>

<span data-ttu-id="8d79d-144">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="8d79d-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8d79d-145">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="8d79d-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8d79d-146">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8d79d-146">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8d79d-147">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8d79d-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 676
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
Date: Thu, 24 Mar 2016 05:22:14 GMT

{
    "id": "G000024135",
    "invoiceDate": "2018-02-08T22:40:37.5897767Z",
    "billingPeriodStartDate": "2018-02-01T22:40:37.5897767Z",
    "billingPeriodEndDate": "2018-02-28T22:40:37.5897767Z",
    "totalCharges": 2076.63,
    "paidAmount": 0,
    "currencyCode": "USD",
    "currencySymbol": "$",
    "pdfDownloadLink": "/invoices/G000024135/documents/statement",
    "taxReceipts": [
        {
            "id": "123456",
            "taxReceiptPdfDownloadLink": "/invoices/G000024135/receipts/123456/documents/statement"
        }
    ],
    "invoiceDetails": [
        {
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024135/lineitems/OneTime/BillingLineItems",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceDetail"
            }
        }
    ],
    "documentType": "invoice",
    "invoiceType": "OneTime",
    "links": {
        "self": {
            "uri": "/invoices/OneTime-G000024135",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Invoice"
    }
}
```
