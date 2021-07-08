---
title: A partner aktuális számlaegyenlegének lekérése
description: Lekéri a partner aktuális számlaegyenlegét. Egy ismétlődő és egyszeri díjakra vonatkozó számla egyenlegének és teljes díjának összegzése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a04ab63482ec9d06e2fe47d2b6ce1bc6a5fd5f27
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548498"
---
# <a name="get-the-partners-current-account-balance"></a><span data-ttu-id="6d808-104">A partner aktuális számlaegyenlegének lekérése</span><span class="sxs-lookup"><span data-stu-id="6d808-104">Get the partner's current account balance</span></span>

<span data-ttu-id="6d808-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6d808-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6d808-106">Lekéri a partner aktuális számlaegyenlegét.</span><span class="sxs-lookup"><span data-stu-id="6d808-106">Retrieves the partner's current account balance.</span></span> <span data-ttu-id="6d808-107">Egy ismétlődő és egyszeri díjakra vonatkozó számla egyenlegének és teljes díjának összegzése.</span><span class="sxs-lookup"><span data-stu-id="6d808-107">A summary of the balance and total charges of an invoice for both recurring and one-time charges.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d808-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6d808-108">Prerequisites</span></span>

- <span data-ttu-id="6d808-109">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6d808-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6d808-110">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="6d808-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="6d808-111">C\#</span><span class="sxs-lookup"><span data-stu-id="6d808-111">C\#</span></span>

<span data-ttu-id="6d808-112">A fiókegyenleg lekéréséhez használja az **IAggregatePartner.Invoices** gyűjteményt, majd hívja meg a **Summary tulajdonságot.**</span><span class="sxs-lookup"><span data-stu-id="6d808-112">To retrieve your account balance, use your **IAggregatePartner.Invoices** collection, and then call the **Summary** property.</span></span> <span data-ttu-id="6d808-113">Ezután hívja meg **a Get** függvényt, és végül hívja meg a **BalanceAmount tulajdonságot.**</span><span class="sxs-lookup"><span data-stu-id="6d808-113">Then call the **Get** function, and finally call the **BalanceAmount** property.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

var invoiceSummary = scopedPartnerOperations.Invoices.Summary.Get();

Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummary.BalanceAmount);
```

<span data-ttu-id="6d808-114">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="6d808-114">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6d808-115">**Project:** PartnerSDK.FeatureSample **osztály:** GetInvoiceSummary.cs</span><span class="sxs-lookup"><span data-stu-id="6d808-115">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceSummary.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6d808-116">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="6d808-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6d808-117">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="6d808-117">Request syntax</span></span>

| <span data-ttu-id="6d808-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="6d808-118">Method</span></span>  | <span data-ttu-id="6d808-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="6d808-119">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="6d808-120">**Kap**</span><span class="sxs-lookup"><span data-stu-id="6d808-120">**GET**</span></span> | <span data-ttu-id="6d808-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6d808-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1.1</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="6d808-122">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="6d808-122">Request headers</span></span>

<span data-ttu-id="6d808-123">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6d808-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6d808-124">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="6d808-124">Request body</span></span>

<span data-ttu-id="6d808-125">None</span><span class="sxs-lookup"><span data-stu-id="6d808-125">None</span></span>

### <a name="request-example"></a><span data-ttu-id="6d808-126">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="6d808-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="6d808-127">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="6d808-127">REST response</span></span>

<span data-ttu-id="6d808-128">Ha sikeres, ez a metódus egy [InvoiceSummary](invoice-resources.md#invoicesummary) erőforrást ad vissza a válaszban.</span><span class="sxs-lookup"><span data-stu-id="6d808-128">If successful, this method returns an [InvoiceSummary](invoice-resources.md#invoicesummary) resource in the response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6d808-129">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="6d808-129">Response success and error codes</span></span>

<span data-ttu-id="6d808-130">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="6d808-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6d808-131">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="6d808-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6d808-132">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6d808-132">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6d808-133">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="6d808-133">Response example</span></span>

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
