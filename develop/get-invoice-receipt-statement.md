---
title: Számla nyugtakivonatának lekérése
description: A számla-azonosító és a bevételezési azonosító használatával kérdezi le a számlázási bevételezési utasítást.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96cef11d6778de2d9bf28e466d88a39f9415727d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767683"
---
# <a name="get-invoice-receipt-statement"></a><span data-ttu-id="919b4-103">Számla nyugtakivonatának lekérése</span><span class="sxs-lookup"><span data-stu-id="919b4-103">Get invoice receipt statement</span></span>

<span data-ttu-id="919b4-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="919b4-104">**Applies To**</span></span>

- <span data-ttu-id="919b4-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="919b4-105">Partner Center</span></span>

<span data-ttu-id="919b4-106">A számla-azonosító és a bevételezési azonosító használatával kérdezi le a számlázási bevételezési utasítást.</span><span class="sxs-lookup"><span data-stu-id="919b4-106">Retrieves an invoice receipt statement using invoice ID and the receipt ID.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="919b4-107">Ez a funkció csak a tajvani adóbevallásokra vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="919b4-107">This feature is only applicable to Taiwan tax receipts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="919b4-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="919b4-108">Prerequisites</span></span>

- <span data-ttu-id="919b4-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="919b4-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="919b4-110">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="919b4-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="919b4-111">Egy érvényes számla-azonosító és egy megfelelő nyugta-azonosító.</span><span class="sxs-lookup"><span data-stu-id="919b4-111">A valid Invoice ID and a corresponding receipt ID.</span></span>

## <a name="c"></a><span data-ttu-id="919b4-112">C\#</span><span class="sxs-lookup"><span data-stu-id="919b4-112">C\#</span></span>

<span data-ttu-id="919b4-113">Ha azonosító alapján szeretné beolvasni a számla bevételezési utasítását, a partner Center SDK v 1.12.0 kezdődően, használja a **IPartner. számlák** gyűjteményt, és hívja meg a **ById ()** METÓDUSt a számla azonosítójának használatával, majd hívja meg a **beérkezési** gyűjteményt, hívja meg a **ById ()** , majd hívja meg a **Documents ()** és a **utasítás ()** metódust a számla</span><span class="sxs-lookup"><span data-stu-id="919b4-113">To get an invoice receipt statement by ID, starting with Partner Center SDK v1.12.0, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Receipts** collection and call **ById()** then call the **Documents()** and **Statement()** methods to access the invoice receipt statement.</span></span> <span data-ttu-id="919b4-114">Végül hívja meg a **Get ()** vagy a **GetAsync ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="919b4-114">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

<span data-ttu-id="919b4-115">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="919b4-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="919b4-116">**Projekt**: PartnerSDK. FeatureSample **osztály**: GetInvoiceReceiptStatement.cs</span><span class="sxs-lookup"><span data-stu-id="919b4-116">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceReceiptStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="919b4-117">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="919b4-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="919b4-118">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="919b4-118">Request syntax</span></span>

| <span data-ttu-id="919b4-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="919b4-119">Method</span></span>  | <span data-ttu-id="919b4-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="919b4-120">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="919b4-121">**GET**</span><span class="sxs-lookup"><span data-stu-id="919b4-121">**GET**</span></span> | <span data-ttu-id="919b4-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/receipts/{Receipt-ID}/Documents/Statement http/1.1</span><span class="sxs-lookup"><span data-stu-id="919b4-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="919b4-123">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="919b4-123">URI parameter</span></span>

<span data-ttu-id="919b4-124">Használja a következő lekérdezési paramétert a számla bevételezési utasításának beolvasásához.</span><span class="sxs-lookup"><span data-stu-id="919b4-124">Use the following query parameter to get the invoice receipt statement.</span></span>

| <span data-ttu-id="919b4-125">Név</span><span class="sxs-lookup"><span data-stu-id="919b4-125">Name</span></span>       | <span data-ttu-id="919b4-126">Típus</span><span class="sxs-lookup"><span data-stu-id="919b4-126">Type</span></span>   | <span data-ttu-id="919b4-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="919b4-127">Required</span></span> | <span data-ttu-id="919b4-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="919b4-128">Description</span></span>                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="919b4-129">számlázási azonosító</span><span class="sxs-lookup"><span data-stu-id="919b4-129">invoice-id</span></span> | <span data-ttu-id="919b4-130">sztring</span><span class="sxs-lookup"><span data-stu-id="919b4-130">string</span></span> | <span data-ttu-id="919b4-131">Igen</span><span class="sxs-lookup"><span data-stu-id="919b4-131">Yes</span></span>      | <span data-ttu-id="919b4-132">Az érték egy számlázási azonosító, amely lehetővé teszi, hogy a viszonteladó egy adott számla eredményét szűrje.</span><span class="sxs-lookup"><span data-stu-id="919b4-132">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |
| <span data-ttu-id="919b4-133">nyugta – azonosító</span><span class="sxs-lookup"><span data-stu-id="919b4-133">receipt-id</span></span> | <span data-ttu-id="919b4-134">sztring</span><span class="sxs-lookup"><span data-stu-id="919b4-134">string</span></span> | <span data-ttu-id="919b4-135">Igen</span><span class="sxs-lookup"><span data-stu-id="919b4-135">Yes</span></span>      | <span data-ttu-id="919b4-136">Az érték egy nyugtát azonosító, amely lehetővé teszi, hogy a viszonteladó szűrni lehessen egy adott számla nyugtáit.</span><span class="sxs-lookup"><span data-stu-id="919b4-136">The value is a receipt-id that allows the reseller to filter the receipts for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="919b4-137">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="919b4-137">Request headers</span></span>

<span data-ttu-id="919b4-138">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="919b4-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="919b4-139">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="919b4-139">Request body</span></span>

<span data-ttu-id="919b4-140">Nincs</span><span class="sxs-lookup"><span data-stu-id="919b4-140">None</span></span>

### <a name="request-example"></a><span data-ttu-id="919b4-141">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="919b4-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="919b4-142">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="919b4-142">REST response</span></span>

<span data-ttu-id="919b4-143">Ha ez sikeres, a metódus egy PDF-streamet ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="919b4-143">If successful, this method returns a pdf stream in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="919b4-144">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="919b4-144">Response success and error codes</span></span>

<span data-ttu-id="919b4-145">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="919b4-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="919b4-146">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="919b4-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="919b4-147">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="919b4-147">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="919b4-148">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="919b4-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 195556
Content-Type: application/pdf
MS-CorrelationId: a1d6ab41-5a30-4643-898b-b30d65d3a0a1
MS-RequestId: cc1ba6db-ab26-404a-9196-712b6395f518
Date: Tue, 05 Feb 2019 04:08:23 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[195556]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=E-Tax-8602768.pdf}
}
```
