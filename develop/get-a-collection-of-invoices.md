---
title: Számlák gyűjteményének lekérése
description: A partner számlái gyűjteményének lekérése.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 7698d85df3341ae4cbff0377bd0a1bb47cd36740
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906435"
---
# <a name="get-a-collection-of-invoices"></a><span data-ttu-id="e3ff9-103">Számlák gyűjteményének lekérése</span><span class="sxs-lookup"><span data-stu-id="e3ff9-103">Get a collection of invoices</span></span>

<span data-ttu-id="e3ff9-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e3ff9-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e3ff9-105">A partner számlái gyűjteményének lekérése.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-105">How to retrieve a collection of the partner's invoices.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3ff9-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="e3ff9-106">Prerequisites</span></span>

- <span data-ttu-id="e3ff9-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e3ff9-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e3ff9-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="e3ff9-109">C\#</span><span class="sxs-lookup"><span data-stu-id="e3ff9-109">C\#</span></span>

<span data-ttu-id="e3ff9-110">Az összes elérhető számla gyűjteményének lekéréséhez használja az [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) tulajdonságot a számlázási műveletek interfészének lekéréséhez, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) metódust a gyűjtemény lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-110">To get a collection of all available invoices, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) method to retrieve the collection.</span></span>

<span data-ttu-id="e3ff9-111">A számlák lapozott gyűjteményének lehívásához először hívja meg a [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) metódust, és adja át neki az oldalméretet egy [**IQuery-objektum létrehozásához.**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery)</span><span class="sxs-lookup"><span data-stu-id="e3ff9-111">To get a paged collection of invoices, first call the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method and pass it the page size to create an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object.</span></span> <span data-ttu-id="e3ff9-112">Ezután az [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) tulajdonság használatával kérje le a számlaműveletek interfészét, majd adja át az IQuery objektumot a [**Query**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) vagy [**a QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) metódusnak a kérés elküldését és az első oldal lekérését.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-112">Next, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then pass the IQuery object to the [**Query**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) method to send the request and get the first page.</span></span>

<span data-ttu-id="e3ff9-113">Ezután az [**Enumerator (Enumerátorok)**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) tulajdonság használatával hozzon létre egy felületet a támogatott erőforrás-gyűjtemény-enumerátorok gyűjteményéhez, majd hívja meg az [**Invoices.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) hívását egy enumerátor létrehozásához a számlák gyűjteményének bejárása számára.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-113">Next, use the [**Enumerators**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) property to get an interface to the collection of supported resource collection enumerators, and then call [**Invoices.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) to create an enumerator for traversing the collection of invoices.</span></span> <span data-ttu-id="e3ff9-114">Végül az enumerátor használatával lekérheti a számlák minden oldalát, és használhatja őket az alábbi példakódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-114">Finally, use the enumerator to retrieve and work with each page of invoices as shown in the following code example.</span></span> <span data-ttu-id="e3ff9-115">A Next [**metódus**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) minden hívása a számlák következő oldalára vonatkozó kérést küld az oldal mérete alapján.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-115">Each call to the [**Next**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) method sends a request for the next page of invoices based on the page size.</span></span>

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

<span data-ttu-id="e3ff9-116">Egy kissé eltérő példáért lásd: **Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e3ff9-116">For a slightly different example, see **Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e3ff9-117">**Project**: Partnerközpont SDK **Osztály:** GetPagedInvoices.cs</span><span class="sxs-lookup"><span data-stu-id="e3ff9-117">**Project**: Partner Center SDK Samples **Class**: GetPagedInvoices.cs</span></span>

> [!NOTE] 
> <span data-ttu-id="e3ff9-118">Ugyanazt az API-t használjuk minden modern kereskedelmi vásárláshoz, valamint 145p és Office licenchez.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-118">The same API is used for all modern commercial purchases as well as 145p and Office licenses.</span></span> <span data-ttu-id="e3ff9-119">A méret és az eltolás csak az örökölt számlák esetén lesz figyelembe véve.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-119">Size and offset are only considered for legacy invoices.</span></span> <span data-ttu-id="e3ff9-120">Minden modern kereskedelmi vásárlás esetén a rendszer figyelmen kívül & eltolást.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-120">For all modern commercial purchases, pagesize & offset will be ignored.</span></span>

## <a name="rest-request"></a><span data-ttu-id="e3ff9-121">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="e3ff9-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e3ff9-122">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="e3ff9-122">Request syntax</span></span>

| <span data-ttu-id="e3ff9-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="e3ff9-123">Method</span></span>  | <span data-ttu-id="e3ff9-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="e3ff9-124">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="e3ff9-125">**Kap**</span><span class="sxs-lookup"><span data-stu-id="e3ff9-125">**GET**</span></span> | <span data-ttu-id="e3ff9-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e3ff9-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1</span></span>  |

### <a name="uri-parameters"></a><span data-ttu-id="e3ff9-127">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="e3ff9-127">URI parameters</span></span>

<span data-ttu-id="e3ff9-128">A kérelem létrehozásakor használja a következő lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-128">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="e3ff9-129">Név</span><span class="sxs-lookup"><span data-stu-id="e3ff9-129">Name</span></span>   | <span data-ttu-id="e3ff9-130">Típus</span><span class="sxs-lookup"><span data-stu-id="e3ff9-130">Type</span></span> | <span data-ttu-id="e3ff9-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e3ff9-131">Required</span></span> | <span data-ttu-id="e3ff9-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="e3ff9-132">Description</span></span>                                                                            |
|--------|------|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="e3ff9-133">size</span><span class="sxs-lookup"><span data-stu-id="e3ff9-133">size</span></span>   | <span data-ttu-id="e3ff9-134">int</span><span class="sxs-lookup"><span data-stu-id="e3ff9-134">int</span></span>  | <span data-ttu-id="e3ff9-135">Nem</span><span class="sxs-lookup"><span data-stu-id="e3ff9-135">No</span></span>       | <span data-ttu-id="e3ff9-136">A válaszban visszaadni szükséges számlaerőforrások száma.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-136">The number of invoice resources to return in the response.</span></span> <span data-ttu-id="e3ff9-137">Ezt a paramétert nem kötelező megadni.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-137">This parameter is optional.</span></span> |
| <span data-ttu-id="e3ff9-138">offset</span><span class="sxs-lookup"><span data-stu-id="e3ff9-138">offset</span></span> | <span data-ttu-id="e3ff9-139">int</span><span class="sxs-lookup"><span data-stu-id="e3ff9-139">int</span></span>  | <span data-ttu-id="e3ff9-140">Nem</span><span class="sxs-lookup"><span data-stu-id="e3ff9-140">No</span></span>       | <span data-ttu-id="e3ff9-141">Az első vissza nem tér számlának nulla alapú indexe.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-141">The zero-based index of the first invoice to return.</span></span>                                   |

### <a name="request-headers"></a><span data-ttu-id="e3ff9-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="e3ff9-142">Request headers</span></span>

<span data-ttu-id="e3ff9-143">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e3ff9-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e3ff9-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="e3ff9-144">Request body</span></span>

<span data-ttu-id="e3ff9-145">None</span><span class="sxs-lookup"><span data-stu-id="e3ff9-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="e3ff9-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="e3ff9-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="e3ff9-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="e3ff9-147">REST response</span></span>

<span data-ttu-id="e3ff9-148">Ha a művelet sikeres, a válasz törzse tartalmazza a [számlaerőforrások gyűjteményét.](invoice-resources.md#invoice)</span><span class="sxs-lookup"><span data-stu-id="e3ff9-148">If successful, the response body contains the collection of [Invoice](invoice-resources.md#invoice) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e3ff9-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="e3ff9-149">Response success and error codes</span></span>

<span data-ttu-id="e3ff9-150">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e3ff9-151">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="e3ff9-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e3ff9-152">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e3ff9-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e3ff9-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="e3ff9-153">Response example</span></span>

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
