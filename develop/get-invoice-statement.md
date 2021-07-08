---
title: Számlakivonat lekérése
description: Lekér egy számlakivonatot a számlaazonosítóval.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f0324916eb2efd9244530a53b1d7bb4abc0c8e6e
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549127"
---
# <a name="get-invoice-statement"></a><span data-ttu-id="2b35a-103">Számlakivonat lekérése</span><span class="sxs-lookup"><span data-stu-id="2b35a-103">Get invoice statement</span></span>

<span data-ttu-id="2b35a-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2b35a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b35a-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2b35a-105">Prerequisites</span></span>

- <span data-ttu-id="2b35a-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2b35a-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2b35a-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="2b35a-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2b35a-108">Egy érvényes számlaazonosító.</span><span class="sxs-lookup"><span data-stu-id="2b35a-108">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="2b35a-109">C\#</span><span class="sxs-lookup"><span data-stu-id="2b35a-109">C\#</span></span>

<span data-ttu-id="2b35a-110">A számlakivonat azonosító alapján való lehívásához használja **az IPartner.Invoices** gyűjteményt, és hívja meg a **ById()** metódust a számlaazonosítóval, majd hívja meg a **Documents()** és a **Statement() metódusokat** a számlakivonat eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="2b35a-110">To get an invoice statement by ID, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Documents()** and **Statement()** methods to access the invoice statement.</span></span> <span data-ttu-id="2b35a-111">Végül hívja meg a **Get() vagy** **a GetAsync() metódust.**</span><span class="sxs-lookup"><span data-stu-id="2b35a-111">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

<span data-ttu-id="2b35a-112">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="2b35a-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2b35a-113">**Project:** PartnerSDK.FeatureSample **osztály:** GetInvoiceStatement.cs</span><span class="sxs-lookup"><span data-stu-id="2b35a-113">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2b35a-114">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="2b35a-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2b35a-115">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="2b35a-115">Request syntax</span></span>

| <span data-ttu-id="2b35a-116">Metódus</span><span class="sxs-lookup"><span data-stu-id="2b35a-116">Method</span></span>  | <span data-ttu-id="2b35a-117">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2b35a-117">Request URI</span></span>                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2b35a-118">**Kap**</span><span class="sxs-lookup"><span data-stu-id="2b35a-118">**GET**</span></span> | <span data-ttu-id="2b35a-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{számlaazonosító}/documents/statement HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2b35a-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="2b35a-120">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="2b35a-120">URI parameter</span></span>

<span data-ttu-id="2b35a-121">Az alábbi lekérdezési paraméterrel lekérdezheti a számlakivonatot.</span><span class="sxs-lookup"><span data-stu-id="2b35a-121">Use the following query parameter to get the invoice statement.</span></span>

| <span data-ttu-id="2b35a-122">Név</span><span class="sxs-lookup"><span data-stu-id="2b35a-122">Name</span></span>       | <span data-ttu-id="2b35a-123">Típus</span><span class="sxs-lookup"><span data-stu-id="2b35a-123">Type</span></span>       | <span data-ttu-id="2b35a-124">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2b35a-124">Required</span></span> | <span data-ttu-id="2b35a-125">Leírás</span><span class="sxs-lookup"><span data-stu-id="2b35a-125">Description</span></span>                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2b35a-126">számlaazonosító</span><span class="sxs-lookup"><span data-stu-id="2b35a-126">invoice-id</span></span> | <span data-ttu-id="2b35a-127">sztring</span><span class="sxs-lookup"><span data-stu-id="2b35a-127">string</span></span>     | <span data-ttu-id="2b35a-128">Igen</span><span class="sxs-lookup"><span data-stu-id="2b35a-128">Yes</span></span>      | <span data-ttu-id="2b35a-129">Az érték egy számlaazonosító, amely lehetővé teszi a viszonteladó számára az eredmények szűrését egy adott számlára.</span><span class="sxs-lookup"><span data-stu-id="2b35a-129">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2b35a-130">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2b35a-130">Request headers</span></span>

<span data-ttu-id="2b35a-131">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2b35a-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2b35a-132">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2b35a-132">Request body</span></span>

<span data-ttu-id="2b35a-133">None</span><span class="sxs-lookup"><span data-stu-id="2b35a-133">None</span></span>

### <a name="request-example"></a><span data-ttu-id="2b35a-134">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="2b35a-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="2b35a-135">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2b35a-135">REST response</span></span>

<span data-ttu-id="2b35a-136">Ha a művelet sikeres, ez a metódus egy [InvoiceStatement erőforrást](invoice-resources.md#invoicestatement) ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="2b35a-136">If successful, this method returns an [InvoiceStatement](invoice-resources.md#invoicestatement) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2b35a-137">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2b35a-137">Response success and error codes</span></span>

<span data-ttu-id="2b35a-138">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="2b35a-138">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2b35a-139">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="2b35a-139">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2b35a-140">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2b35a-140">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2b35a-141">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2b35a-141">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[219753]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```
