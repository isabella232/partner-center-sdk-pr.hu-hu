---
title: A partner aktuális számlaegyenlegének lekérése
description: Lekéri a partner aktuális fiókjának egyenlegét. Egy számla egyenlegének és teljes díjainak összefoglalása az ismétlődő és egyszeri költségekkel együtt.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 110da433faa6ff4d3d068c6d68a6f497f4a2721a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767904"
---
# <a name="get-the-partners-current-account-balance"></a><span data-ttu-id="4258c-104">A partner aktuális számlaegyenlegének lekérése</span><span class="sxs-lookup"><span data-stu-id="4258c-104">Get the partner's current account balance</span></span>

<span data-ttu-id="4258c-105">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="4258c-105">**Applies To**</span></span>

- <span data-ttu-id="4258c-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="4258c-106">Partner Center</span></span>
- <span data-ttu-id="4258c-107">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="4258c-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4258c-108">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="4258c-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4258c-109">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="4258c-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4258c-110">Lekéri a partner aktuális fiókjának egyenlegét.</span><span class="sxs-lookup"><span data-stu-id="4258c-110">Retrieves the partner's current account balance.</span></span> <span data-ttu-id="4258c-111">Egy számla egyenlegének és teljes díjainak összefoglalása az ismétlődő és egyszeri költségekkel együtt.</span><span class="sxs-lookup"><span data-stu-id="4258c-111">A summary of the balance and total charges of an invoice for both recurring and one-time charges.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4258c-112">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4258c-112">Prerequisites</span></span>

- <span data-ttu-id="4258c-113">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="4258c-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4258c-114">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="4258c-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="4258c-115">C\#</span><span class="sxs-lookup"><span data-stu-id="4258c-115">C\#</span></span>

<span data-ttu-id="4258c-116">A fiók egyenlegének lekéréséhez használja a **IAggregatePartner.** accounts gyűjteményt, majd hívja meg az **Summary (összefoglalás** ) tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="4258c-116">To retrieve your account balance, use your **IAggregatePartner.Invoices** collection, and then call the **Summary** property.</span></span> <span data-ttu-id="4258c-117">Ezután hívja meg a **Get** függvényt, és végül hívja meg a **BalanceAmount** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="4258c-117">Then call the **Get** function, and finally call the **BalanceAmount** property.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

var invoiceSummary = scopedPartnerOperations.Invoices.Summary.Get();

Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummary.BalanceAmount);
```

<span data-ttu-id="4258c-118">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="4258c-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4258c-119">**Projekt**: PartnerSDK. FeatureSample **osztály**: GetInvoiceSummary.cs</span><span class="sxs-lookup"><span data-stu-id="4258c-119">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceSummary.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4258c-120">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="4258c-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4258c-121">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4258c-121">Request syntax</span></span>

| <span data-ttu-id="4258c-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="4258c-122">Method</span></span>  | <span data-ttu-id="4258c-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4258c-123">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="4258c-124">**GET**</span><span class="sxs-lookup"><span data-stu-id="4258c-124">**GET**</span></span> | <span data-ttu-id="4258c-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/Summary http/1.1</span><span class="sxs-lookup"><span data-stu-id="4258c-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1.1</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="4258c-126">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4258c-126">Request headers</span></span>

<span data-ttu-id="4258c-127">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4258c-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4258c-128">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="4258c-128">Request body</span></span>

<span data-ttu-id="4258c-129">Nincs</span><span class="sxs-lookup"><span data-stu-id="4258c-129">None</span></span>

### <a name="request-example"></a><span data-ttu-id="4258c-130">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4258c-130">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="4258c-131">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4258c-131">REST response</span></span>

<span data-ttu-id="4258c-132">Ha ez sikeres, ez a metódus egy [InvoiceSummary](invoice-resources.md#invoicesummary) -erőforrást ad vissza a válaszban.</span><span class="sxs-lookup"><span data-stu-id="4258c-132">If successful, this method returns an [InvoiceSummary](invoice-resources.md#invoicesummary) resource in the response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4258c-133">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4258c-133">Response success and error codes</span></span>

<span data-ttu-id="4258c-134">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="4258c-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4258c-135">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="4258c-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4258c-136">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4258c-136">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4258c-137">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4258c-137">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    "balanceAmount": 751094.39,
    "currencyCode": "USD",
    "currencySymbol": "$",
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
                "currencyCode": "USD",
                "currencySymbol": "$",
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
                "currencyCode": "USD",
                "currencySymbol": "$",
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
```
