---
title: Számlák gyűjteményének lekérése
description: A partner számláinak gyűjteményének beolvasása.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: f56c3de8dd227f573921e5b969c2217c2f743a21
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768067"
---
# <a name="get-a-collection-of-invoices"></a><span data-ttu-id="2c2a7-103">Számlák gyűjteményének lekérése</span><span class="sxs-lookup"><span data-stu-id="2c2a7-103">Get a collection of invoices</span></span>

<span data-ttu-id="2c2a7-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="2c2a7-104">**Applies To**</span></span>

- <span data-ttu-id="2c2a7-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="2c2a7-105">Partner Center</span></span>
- <span data-ttu-id="2c2a7-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="2c2a7-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2c2a7-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="2c2a7-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2c2a7-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="2c2a7-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2c2a7-109">A partner számláinak gyűjteményének beolvasása.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-109">How to retrieve a collection of the partner's invoices.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c2a7-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2c2a7-110">Prerequisites</span></span>

- <span data-ttu-id="2c2a7-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2c2a7-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="2c2a7-113">C\#</span><span class="sxs-lookup"><span data-stu-id="2c2a7-113">C\#</span></span>

<span data-ttu-id="2c2a7-114">Az összes rendelkezésre álló számla gyűjteményének beszerzéséhez használja a [**számlák**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) tulajdonságot, hogy beolvassa a számlázási műveleteket, majd meghívja a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) metódust a gyűjtemény lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-114">To get a collection of all available invoices, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) method to retrieve the collection.</span></span>

<span data-ttu-id="2c2a7-115">A számlák lapozható gyűjteményének lekéréséhez először hívja meg a [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) metódust, és adja át az oldalméret számára egy [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) objektum létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-115">To get a paged collection of invoices, first call the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method and pass it the page size to create an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object.</span></span> <span data-ttu-id="2c2a7-116">Ezután a [**számlák**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) tulajdonsággal szerezzen be egy felületet a számlázási műveletekhez, majd továbbítsa a IQuery objektumot a [**lekérdezési**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) vagy [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) metódusnak a kérelem elküldéséhez és az első oldal beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-116">Next, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then pass the IQuery object to the [**Query**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) method to send the request and get the first page.</span></span>

<span data-ttu-id="2c2a7-117">Ezután a [**enumerálások**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) tulajdonsággal szerezzen be egy felületet a támogatott erőforrás-gyűjtési enumerálások gyűjteményéhez, majd hívja meg a [**számlákat. hozzon**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) létre egy enumerálást a számlák gyűjteményének átjárásához.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-117">Next, use the [**Enumerators**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) property to get an interface to the collection of supported resource collection enumerators, and then call [**Invoices.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) to create an enumerator for traversing the collection of invoices.</span></span> <span data-ttu-id="2c2a7-118">Végül a számbavételsel beolvashatja és használhatja a számlák egyes lapjait, ahogy az alábbi példában is látható.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-118">Finally, use the enumerator to retrieve and work with each page of invoices as shown in the following code example.</span></span> <span data-ttu-id="2c2a7-119">A [**következő**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) metódus minden hívása egy kérést küld a számlák következő lapjára az oldalméret alapján.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-119">Each call to the [**Next**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) method sends a request for the next page of invoices based on the page size.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;

// Is this an unpaged or paged request?
bool isUnpaged = (this.invoicePageSize <= 0);

// If the scenario is unpaged, get all the invoices, otherwise get the first page.
var invoicesPage = (isUnpaged)
                 ? partnerOperations.Invoices.Get()
                 : partnerOperations.Invoices.Query(QueryFactory.Instance.BuildIndexedQuery(this.invoicePageSize));

// Create an invoice enumerator for traversing the invoice pages.
var invoicesEnumerator = partnerOperations.Enumerators.Invoices.Create(invoicesPage);
int lineCounter = 1;

while (invoicesEnumerator.HasValue)
{
    // Print the current invoice results page.
    var invoices = invoicesEnumerator.Current.Items;

    foreach (var i in invoices)
    {
        Console.WriteLine(String.Format("{0,3}. {1}  {2}  {3,16:C2}",
            lineCounter++,
            i.Id,
            i.InvoiceDate.ToString("yyyy&#39;-&#39;MM&#39;-&#39;dd&#39;T&#39;HH&#39;:&#39;mm&#39;:&#39;ss&#39;Z&#39;"),
            i.TotalCharges));
    }

    Console.WriteLine();
    Console.Write("Press any key to retrieve the next invoices page");
    Console.ReadKey();

    // Get the next page of invoices.
    invoicesEnumerator.Next();
}
```

<span data-ttu-id="2c2a7-120">Egy kicsit más példához lásd: **minta**: [konzol tesztelése alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2c2a7-120">For a slightly different example, see **Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2c2a7-121">**Projekt**: partner Center SDK Samples **osztály**: GetPagedInvoices.cs</span><span class="sxs-lookup"><span data-stu-id="2c2a7-121">**Project**: Partner Center SDK Samples **Class**: GetPagedInvoices.cs</span></span>

> [!NOTE] 
> <span data-ttu-id="2c2a7-122">Ugyanezt az API-t használja az összes modern kereskedelmi vásárláshoz, valamint a 145p és az Office-licencekhez.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-122">The same API is used for all modern commercial purchases as well as 145p and Office licenses.</span></span> <span data-ttu-id="2c2a7-123">A méretet és az eltolást csak a régi számlákra számítjuk.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-123">Size and offset are only considered for legacy invoices.</span></span> <span data-ttu-id="2c2a7-124">Az összes modern kereskedelmi vásárlás esetén a pageSize & eltolása figyelmen kívül lesz hagyva.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-124">For all modern commercial purchases, pagesize & offset will be ignored.</span></span>

## <a name="rest-request"></a><span data-ttu-id="2c2a7-125">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="2c2a7-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2c2a7-126">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="2c2a7-126">Request syntax</span></span>

| <span data-ttu-id="2c2a7-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="2c2a7-127">Method</span></span>  | <span data-ttu-id="2c2a7-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2c2a7-128">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="2c2a7-129">**GET**</span><span class="sxs-lookup"><span data-stu-id="2c2a7-129">**GET**</span></span> | <span data-ttu-id="2c2a7-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices? méret = {size} &eltolás = {ELTOLÁS} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2c2a7-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1</span></span>  |

### <a name="uri-parameters"></a><span data-ttu-id="2c2a7-131">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="2c2a7-131">URI parameters</span></span>

<span data-ttu-id="2c2a7-132">A kérelem létrehozásakor használja a következő lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-132">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="2c2a7-133">Név</span><span class="sxs-lookup"><span data-stu-id="2c2a7-133">Name</span></span>   | <span data-ttu-id="2c2a7-134">Típus</span><span class="sxs-lookup"><span data-stu-id="2c2a7-134">Type</span></span> | <span data-ttu-id="2c2a7-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2c2a7-135">Required</span></span> | <span data-ttu-id="2c2a7-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="2c2a7-136">Description</span></span>                                                                            |
|--------|------|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="2c2a7-137">size</span><span class="sxs-lookup"><span data-stu-id="2c2a7-137">size</span></span>   | <span data-ttu-id="2c2a7-138">int</span><span class="sxs-lookup"><span data-stu-id="2c2a7-138">int</span></span>  | <span data-ttu-id="2c2a7-139">Nem</span><span class="sxs-lookup"><span data-stu-id="2c2a7-139">No</span></span>       | <span data-ttu-id="2c2a7-140">A válaszban visszaadni kívánt számlázási erőforrások száma.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-140">The number of invoice resources to return in the response.</span></span> <span data-ttu-id="2c2a7-141">Ezt a paramétert nem kötelező megadni.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-141">This parameter is optional.</span></span> |
| <span data-ttu-id="2c2a7-142">offset</span><span class="sxs-lookup"><span data-stu-id="2c2a7-142">offset</span></span> | <span data-ttu-id="2c2a7-143">int</span><span class="sxs-lookup"><span data-stu-id="2c2a7-143">int</span></span>  | <span data-ttu-id="2c2a7-144">Nem</span><span class="sxs-lookup"><span data-stu-id="2c2a7-144">No</span></span>       | <span data-ttu-id="2c2a7-145">A visszaadni kívánt első számla nulla alapú indexe.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-145">The zero-based index of the first invoice to return.</span></span>                                   |

### <a name="request-headers"></a><span data-ttu-id="2c2a7-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2c2a7-146">Request headers</span></span>

<span data-ttu-id="2c2a7-147">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2c2a7-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2c2a7-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2c2a7-148">Request body</span></span>

<span data-ttu-id="2c2a7-149">Nincs</span><span class="sxs-lookup"><span data-stu-id="2c2a7-149">None</span></span>

### <a name="request-example"></a><span data-ttu-id="2c2a7-150">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="2c2a7-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices?size=200&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="2c2a7-151">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2c2a7-151">REST response</span></span>

<span data-ttu-id="2c2a7-152">Ha ez sikeres, a válasz törzse tartalmazza a [Számlázási](invoice-resources.md#invoice) erőforrások gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-152">If successful, the response body contains the collection of [Invoice](invoice-resources.md#invoice) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2c2a7-153">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2c2a7-153">Response success and error codes</span></span>

<span data-ttu-id="2c2a7-154">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2c2a7-155">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2c2a7-156">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="2c2a7-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2c2a7-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2c2a7-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT
{
    "totalCount": 2,
    "items": [
        {
            "id": "D02005YFHI",
            "invoiceDate": "2017-01-21T00:00:00Z",
            "totalCharges": 24606.35,
            "paidAmount": 1000,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "pdfDownloadLink": "/invoices/D02005YFHI/documents/statement",
            "taxReceipts": [
                {
                    "id": "123456",
                    "taxReceiptPdfDownloadLink": "/invoices/D02005YFHI/receipts/123456/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "office",
                    "links": {
                        "self": {
                            "uri": "/invoices/Recurring-D02005YFHI/lineitems/Office/BillingLineItems",
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
            "invoiceType": "Recurring",
            "links": {
                "self": {
                    "uri": "/invoices/Recurring-D02005YFHI",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        },
        {
            "id": "G000024130",
            "invoiceDate": "2018-02-08T01:22:47.603895Z",
            "totalCharges": 586366,
            "paidAmount": 0,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "pdfDownloadLink": "/invoices/G000024130/documents/statement",
            "taxReceipts": [
                {
                    "id": "234567",
                    "taxReceiptPdfDownloadLink": "/invoices/G000024130/receipts/234567/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "one_time",
                    "links": {
                        "self": {
                            "uri": "/invoices/OneTime-G000024130/lineitems/OneTime/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "amendments": [
                {
                    "id": "G000024131",
                    "invoiceDate": "2018-02-08T18:44:37.5381456Z",
                    "totalCharges": 107661.12,
                    "paidAmount": 0,
                    "currencyCode": "CHF",
                    "currencySymbol": "CHF",
                    "invoiceDetails": [
                        {
                            "invoiceLineItemType": "billing_line_items",
                            "billingProvider": "one_time",
                            "attributes": {
                                "objectType": "InvoiceDetail"
                            }
                        }
                    ],
                    "documentType": "adjustment_note",
                    "amendsOf": "G000024130",
                    "invoiceType": "OneTime",
                    "attributes": {
                        "objectType": "Invoice"
                    }
                }
            ],
            "documentType": "void_note",
            "invoiceType": "OneTime",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024130",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices?size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices?size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
