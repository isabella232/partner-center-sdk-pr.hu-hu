---
title: Számla lekérte azonosító alapján
description: Lekér egy adott számlát a számlaazonosítóval.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c888786a6b6ca941629bb7aac95227021c37a7fc
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549161"
---
# <a name="get-invoice-by-id"></a><span data-ttu-id="95941-103">Számla lekérte azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="95941-103">Get invoice by ID</span></span>

<span data-ttu-id="95941-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="95941-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="95941-105">Lekér egy adott számlát a számlaazonosítóval.</span><span class="sxs-lookup"><span data-stu-id="95941-105">Retrieves a given invoice using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95941-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="95941-106">Prerequisites</span></span>

- <span data-ttu-id="95941-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="95941-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="95941-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="95941-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="95941-109">Egy érvényes számlaazonosító.</span><span class="sxs-lookup"><span data-stu-id="95941-109">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="95941-110">C\#</span><span class="sxs-lookup"><span data-stu-id="95941-110">C\#</span></span>

<span data-ttu-id="95941-111">Számla lekért száma azonosító alapján:</span><span class="sxs-lookup"><span data-stu-id="95941-111">To get an invoice by ID:</span></span>

1. <span data-ttu-id="95941-112">Használja az **IPartner.Invoices gyűjteményt,** és hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="95941-112">Use your **IPartner.Invoices** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="95941-113">Hívja meg **a Get() vagy** **a GetAsync() metódust.**</span><span class="sxs-lookup"><span data-stu-id="95941-113">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoice = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Get();
```

<span data-ttu-id="95941-114">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="95941-114">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="95941-115">**Project:** PartnerSDK.FeatureSample **osztály:** GetInvoice.cs</span><span class="sxs-lookup"><span data-stu-id="95941-115">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="95941-116">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="95941-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="95941-117">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="95941-117">Request syntax</span></span>

| <span data-ttu-id="95941-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="95941-118">Method</span></span>  | <span data-ttu-id="95941-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="95941-119">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="95941-120">**Kap**</span><span class="sxs-lookup"><span data-stu-id="95941-120">**GET**</span></span> | <span data-ttu-id="95941-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{számlaazonosító} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="95941-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="95941-122">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="95941-122">URI parameter</span></span>

<span data-ttu-id="95941-123">A számla lekérdezhető a következő lekérdezési paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="95941-123">Use the following query parameter to get the invoice.</span></span>

| <span data-ttu-id="95941-124">Név</span><span class="sxs-lookup"><span data-stu-id="95941-124">Name</span></span>           | <span data-ttu-id="95941-125">Típus</span><span class="sxs-lookup"><span data-stu-id="95941-125">Type</span></span>       | <span data-ttu-id="95941-126">Kötelező</span><span class="sxs-lookup"><span data-stu-id="95941-126">Required</span></span> | <span data-ttu-id="95941-127">Leírás</span><span class="sxs-lookup"><span data-stu-id="95941-127">Description</span></span>                                                                                        |
|----------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="95941-128">**számlaazonosító**</span><span class="sxs-lookup"><span data-stu-id="95941-128">**invoice-id**</span></span> | <span data-ttu-id="95941-129">**sztring**</span><span class="sxs-lookup"><span data-stu-id="95941-129">**string**</span></span> | <span data-ttu-id="95941-130">Igen</span><span class="sxs-lookup"><span data-stu-id="95941-130">Yes</span></span>      | <span data-ttu-id="95941-131">Az érték egy **számlaazonosító,** amely lehetővé teszi, hogy a viszonteladó szűrje egy adott számla eredményeit.</span><span class="sxs-lookup"><span data-stu-id="95941-131">The value is an **invoice-id** that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="95941-132">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="95941-132">Request headers</span></span>

<span data-ttu-id="95941-133">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="95941-133">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="95941-134">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="95941-134">Request body</span></span>

<span data-ttu-id="95941-135">None</span><span class="sxs-lookup"><span data-stu-id="95941-135">None</span></span>

### <a name="request-example"></a><span data-ttu-id="95941-136">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="95941-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="95941-137">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="95941-137">REST response</span></span>

<span data-ttu-id="95941-138">Ha a művelet sikeres, ez a metódus egy [invoice erőforrást](invoice-resources.md#invoice) ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="95941-138">If successful, this method returns an [Invoice](invoice-resources.md#invoice) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="95941-139">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="95941-139">Response success and error codes</span></span>

<span data-ttu-id="95941-140">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="95941-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="95941-141">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="95941-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="95941-142">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="95941-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="95941-143">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="95941-143">Response example</span></span>

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
