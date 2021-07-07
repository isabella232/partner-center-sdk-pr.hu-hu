---
title: Számla nyugtakivonatának lekérése
description: Lekér egy számlakivonatot a számlaazonosító és a nyugtaazonosító használatával.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac4c8f0b881409dcad3560eefb82d4bb5e877a
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446129"
---
# <a name="get-invoice-receipt-statement"></a><span data-ttu-id="f043a-103">Számla nyugtakivonatának lekérése</span><span class="sxs-lookup"><span data-stu-id="f043a-103">Get invoice receipt statement</span></span>

<span data-ttu-id="f043a-104">Lekér egy számlakivonatot a számlaazonosító és a nyugtaazonosító használatával.</span><span class="sxs-lookup"><span data-stu-id="f043a-104">Retrieves an invoice receipt statement using invoice ID and the receipt ID.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f043a-105">Ez a funkció csak a Tajvani adóbevallások esetében érvényes.</span><span class="sxs-lookup"><span data-stu-id="f043a-105">This feature is only applicable to Taiwan tax receipts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f043a-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f043a-106">Prerequisites</span></span>

- <span data-ttu-id="f043a-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f043a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f043a-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="f043a-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f043a-109">Egy érvényes számlaazonosító és egy megfelelő nyugtaazonosító.</span><span class="sxs-lookup"><span data-stu-id="f043a-109">A valid Invoice ID and a corresponding receipt ID.</span></span>

## <a name="c"></a><span data-ttu-id="f043a-110">C\#</span><span class="sxs-lookup"><span data-stu-id="f043a-110">C\#</span></span>

<span data-ttu-id="f043a-111">A számla visszaigazolási kimutatásának azonosító alapján való lehívásához az Partnerközpont SDK v1.12.0-val kezdve használja az **IPartner.Invoices** gyűjteményt, és hívja meg a **ById()** metódust a számlaazonosítóval, majd hívja meg a **ById()** metódust, majd hívja meg a **Documents()** és a **Statement() metódusokat** a számlakivonat eléréséhez. </span><span class="sxs-lookup"><span data-stu-id="f043a-111">To get an invoice receipt statement by ID, starting with Partner Center SDK v1.12.0, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Receipts** collection and call **ById()** then call the **Documents()** and **Statement()** methods to access the invoice receipt statement.</span></span> <span data-ttu-id="f043a-112">Végül hívja meg a **Get() vagy** **a GetAsync() metódust.**</span><span class="sxs-lookup"><span data-stu-id="f043a-112">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

<span data-ttu-id="f043a-113">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f043a-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f043a-114">**Project**: PartnerSDK.FeatureSample **osztály:** GetInvoiceReceiptStatement.cs</span><span class="sxs-lookup"><span data-stu-id="f043a-114">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceReceiptStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f043a-115">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="f043a-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f043a-116">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f043a-116">Request syntax</span></span>

| <span data-ttu-id="f043a-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="f043a-117">Method</span></span>  | <span data-ttu-id="f043a-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f043a-118">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f043a-119">**Kap**</span><span class="sxs-lookup"><span data-stu-id="f043a-119">**GET**</span></span> | <span data-ttu-id="f043a-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{számlaazonosító}/receipts/{nyugtaazonosító}/documents/statement HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f043a-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f043a-121">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="f043a-121">URI parameter</span></span>

<span data-ttu-id="f043a-122">Az alábbi lekérdezési paraméterrel lekérdezheti a számlakivonatot.</span><span class="sxs-lookup"><span data-stu-id="f043a-122">Use the following query parameter to get the invoice receipt statement.</span></span>

| <span data-ttu-id="f043a-123">Név</span><span class="sxs-lookup"><span data-stu-id="f043a-123">Name</span></span>       | <span data-ttu-id="f043a-124">Típus</span><span class="sxs-lookup"><span data-stu-id="f043a-124">Type</span></span>   | <span data-ttu-id="f043a-125">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f043a-125">Required</span></span> | <span data-ttu-id="f043a-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="f043a-126">Description</span></span>                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f043a-127">számlaazonosító</span><span class="sxs-lookup"><span data-stu-id="f043a-127">invoice-id</span></span> | <span data-ttu-id="f043a-128">sztring</span><span class="sxs-lookup"><span data-stu-id="f043a-128">string</span></span> | <span data-ttu-id="f043a-129">Igen</span><span class="sxs-lookup"><span data-stu-id="f043a-129">Yes</span></span>      | <span data-ttu-id="f043a-130">Az érték egy számlaazonosító, amely lehetővé teszi, hogy a viszonteladó szűrje egy adott számla eredményeit.</span><span class="sxs-lookup"><span data-stu-id="f043a-130">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |
| <span data-ttu-id="f043a-131">nyugta-azonosító</span><span class="sxs-lookup"><span data-stu-id="f043a-131">receipt-id</span></span> | <span data-ttu-id="f043a-132">sztring</span><span class="sxs-lookup"><span data-stu-id="f043a-132">string</span></span> | <span data-ttu-id="f043a-133">Igen</span><span class="sxs-lookup"><span data-stu-id="f043a-133">Yes</span></span>      | <span data-ttu-id="f043a-134">Az érték egy nyugtaazonosító, amely lehetővé teszi, hogy a viszonteladó szűrje egy adott számla nyugtáit.</span><span class="sxs-lookup"><span data-stu-id="f043a-134">The value is a receipt-id that allows the reseller to filter the receipts for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f043a-135">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f043a-135">Request headers</span></span>

<span data-ttu-id="f043a-136">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f043a-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f043a-137">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f043a-137">Request body</span></span>

<span data-ttu-id="f043a-138">None</span><span class="sxs-lookup"><span data-stu-id="f043a-138">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f043a-139">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f043a-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="f043a-140">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f043a-140">REST response</span></span>

<span data-ttu-id="f043a-141">Ha a művelet sikeres, ez a metódus egy PDF-streamet ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="f043a-141">If successful, this method returns a pdf stream in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f043a-142">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f043a-142">Response success and error codes</span></span>

<span data-ttu-id="f043a-143">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="f043a-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f043a-144">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="f043a-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f043a-145">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f043a-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f043a-146">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f043a-146">Response example</span></span>

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
