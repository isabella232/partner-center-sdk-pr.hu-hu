---
title: Számlakivonat lekérése
description: A számla AZONOSÍTÓjának lekérése a számlázási utasítás alapján.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 42e5201919eea5644da463dfe2584c8d55002083
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767884"
---
# <a name="get-invoice-statement"></a><span data-ttu-id="17253-103">Számlakivonat lekérése</span><span class="sxs-lookup"><span data-stu-id="17253-103">Get invoice statement</span></span>

<span data-ttu-id="17253-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="17253-104">**Applies To**</span></span>

- <span data-ttu-id="17253-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="17253-105">Partner Center</span></span>
- <span data-ttu-id="17253-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="17253-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="17253-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="17253-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="17253-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="17253-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="17253-109">A számla AZONOSÍTÓjának lekérése a számlázási utasítás alapján.</span><span class="sxs-lookup"><span data-stu-id="17253-109">Retrieves an invoice statement using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17253-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="17253-110">Prerequisites</span></span>

- <span data-ttu-id="17253-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="17253-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="17253-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="17253-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="17253-113">Érvényes számla-azonosító.</span><span class="sxs-lookup"><span data-stu-id="17253-113">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="17253-114">C\#</span><span class="sxs-lookup"><span data-stu-id="17253-114">C\#</span></span>

<span data-ttu-id="17253-115">Ha azonosító alapján szeretne számlát kapni, használja a **IPartner. számlákon** gyűjteményt, és hívja meg a **ById ()** METÓDUSt a számla azonosítójának használatával, majd hívja meg a **Documents ()** és a **utasítás ()** metódust a számla-utasítás eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="17253-115">To get an invoice statement by ID, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Documents()** and **Statement()** methods to access the invoice statement.</span></span> <span data-ttu-id="17253-116">Végül hívja meg a **Get ()** vagy a **GetAsync ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="17253-116">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

<span data-ttu-id="17253-117">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="17253-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="17253-118">**Projekt**: PartnerSDK. FeatureSample **osztály**: GetInvoiceStatement.cs</span><span class="sxs-lookup"><span data-stu-id="17253-118">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="17253-119">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="17253-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="17253-120">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="17253-120">Request syntax</span></span>

| <span data-ttu-id="17253-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="17253-121">Method</span></span>  | <span data-ttu-id="17253-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="17253-122">Request URI</span></span>                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| <span data-ttu-id="17253-123">**GET**</span><span class="sxs-lookup"><span data-stu-id="17253-123">**GET**</span></span> | <span data-ttu-id="17253-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/Documents/Statement http/1.1</span><span class="sxs-lookup"><span data-stu-id="17253-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="17253-125">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="17253-125">URI parameter</span></span>

<span data-ttu-id="17253-126">A számlakivonat beszerzéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="17253-126">Use the following query parameter to get the invoice statement.</span></span>

| <span data-ttu-id="17253-127">Név</span><span class="sxs-lookup"><span data-stu-id="17253-127">Name</span></span>       | <span data-ttu-id="17253-128">Típus</span><span class="sxs-lookup"><span data-stu-id="17253-128">Type</span></span>       | <span data-ttu-id="17253-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="17253-129">Required</span></span> | <span data-ttu-id="17253-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="17253-130">Description</span></span>                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="17253-131">számlázási azonosító</span><span class="sxs-lookup"><span data-stu-id="17253-131">invoice-id</span></span> | <span data-ttu-id="17253-132">sztring</span><span class="sxs-lookup"><span data-stu-id="17253-132">string</span></span>     | <span data-ttu-id="17253-133">Igen</span><span class="sxs-lookup"><span data-stu-id="17253-133">Yes</span></span>      | <span data-ttu-id="17253-134">Az érték egy számlázási azonosító, amely lehetővé teszi, hogy a viszonteladó egy adott számla eredményét szűrje.</span><span class="sxs-lookup"><span data-stu-id="17253-134">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="17253-135">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="17253-135">Request headers</span></span>

<span data-ttu-id="17253-136">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="17253-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="17253-137">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="17253-137">Request body</span></span>

<span data-ttu-id="17253-138">Nincs</span><span class="sxs-lookup"><span data-stu-id="17253-138">None</span></span>

### <a name="request-example"></a><span data-ttu-id="17253-139">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="17253-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="17253-140">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="17253-140">REST response</span></span>

<span data-ttu-id="17253-141">Ha ez sikeres, ez a metódus egy [InvoiceStatement](invoice-resources.md#invoicestatement) -erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="17253-141">If successful, this method returns an [InvoiceStatement](invoice-resources.md#invoicestatement) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="17253-142">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="17253-142">Response success and error codes</span></span>

<span data-ttu-id="17253-143">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="17253-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="17253-144">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="17253-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="17253-145">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="17253-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="17253-146">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="17253-146">Response example</span></span>

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
