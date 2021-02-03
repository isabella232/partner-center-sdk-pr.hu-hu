---
title: Számlázott kereskedelmi fogyasztási sorok számlázásának beolvasása
description: A partner Center API-k használatával lekérheti a kereskedelmi fogyasztási számla sora (a napi lezárt használati sor) részleteit a megadott számlára vonatkozóan.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: a13b62903e44165ef9811ea7798fcea666d483dc
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768336"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a><span data-ttu-id="10094-103">Számlázott kereskedelmi fogyasztási sorok számlázásának beolvasása</span><span class="sxs-lookup"><span data-stu-id="10094-103">Get invoice billed commercial consumption line items</span></span>

<span data-ttu-id="10094-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="10094-104">**Applies to:**</span></span>

- <span data-ttu-id="10094-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="10094-105">Partner Center</span></span>

<span data-ttu-id="10094-106">A következő módszerekkel részletes információkat kaphat a kereskedelmi felhasználású számla sorokról (más néven bezárt napi használati sorokból) egy adott számlához.</span><span class="sxs-lookup"><span data-stu-id="10094-106">You can use the following methods to get a collection of details for commercial consumption invoice line items (also known as closed daily rated usage line items) for a specified invoice.</span></span>

<span data-ttu-id="10094-107">Ez az API a Microsoft Azure (MS-AZR-0145P) előfizetésekhez tartozó **Azure** -szolgáltatói típusokat is támogatja.</span><span class="sxs-lookup"><span data-stu-id="10094-107">This API also supports **azure** provider types for Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span> <span data-ttu-id="10094-108">Ez azt jelenti, hogy ez az API egy visszamenőlegesen kompatibilis szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="10094-108">This means this API is a backward-compatible feature.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10094-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="10094-109">Prerequisites</span></span>

- <span data-ttu-id="10094-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="10094-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="10094-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="10094-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="10094-112">Egy fiókazonosító.</span><span class="sxs-lookup"><span data-stu-id="10094-112">An invoice identifier.</span></span> <span data-ttu-id="10094-113">Ez azonosítja azt a számlát, amelynek a sorát be kell olvasni.</span><span class="sxs-lookup"><span data-stu-id="10094-113">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="10094-114">C\#</span><span class="sxs-lookup"><span data-stu-id="10094-114">C\#</span></span>

<span data-ttu-id="10094-115">A megadott számla kereskedelmi vonali elemeinek lekéréséhez le kell kérnie a számla objektumot:</span><span class="sxs-lookup"><span data-stu-id="10094-115">To get the commercial line items for the specified invoice, you must retrieve the invoice object:</span></span>

1. <span data-ttu-id="10094-116">Hívja meg a [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) metódust, hogy lekérje a megadott számla műveleteinek számlázására szolgáló felületet.</span><span class="sxs-lookup"><span data-stu-id="10094-116">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="10094-117">Hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódust a számla objektum lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="10094-117">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="10094-118">A számla objektum a megadott számla összes adatát tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="10094-118">The invoice object contains all of the information for the specified invoice.</span></span>

<span data-ttu-id="10094-119">A **szolgáltató** azonosítja a számlázott részletes információk forrását (például: **egykori**).</span><span class="sxs-lookup"><span data-stu-id="10094-119">The **Provider** identifies the source of the billed detail information (for example, **onetime**).</span></span> <span data-ttu-id="10094-120">A **InvoiceLineItemType** meghatározza a típust (például **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="10094-120">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="10094-121">A következő példa egy **foreach** hurok használatával dolgozza fel a line Items gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="10094-121">The following example code uses a **foreach** loop to process the line items collection.</span></span> <span data-ttu-id="10094-122">Az egyes **InvoiceLineItemType** tartozó sorok külön gyűjteménye lesz beolvasva.</span><span class="sxs-lookup"><span data-stu-id="10094-122">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="10094-123">Egy **InvoiceDetail** -példánynak megfelelő sorok gyűjteményének beolvasása:</span><span class="sxs-lookup"><span data-stu-id="10094-123">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="10094-124">Adja át a példány **BillingProvider** és **InvoiceLineItemType** a [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) metódusnak.</span><span class="sxs-lookup"><span data-stu-id="10094-124">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="10094-125">A társított sorok beolvasásához hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="10094-125">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="10094-126">Hozzon létre egy enumerálást a gyűjtemény átjárásához az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="10094-126">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string invoiceId;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type DailyRatedUsageLineItem
        if (item is DailyRatedUsageLineItem)
        {
            Type t = typeof(DailyRatedUsageLineItem);
            PropertyInfo[] properties = t.GetProperties();

            foreach (PropertyInfo property in properties)
            {
                // Insert code here to work with the line item properties
            }
        }
        itemNumber++;
    });

    Console.Out.WriteLine("\tPress any key to fetch next data. Press the Escape (Esc) key to quit: \n");
    keyInfo = Console.ReadKey();

    if (keyInfo.Key == ConsoleKey.Escape)
    {
        break;
    }

    fetchNext = !string.IsNullOrWhiteSpace(seekBasedResourceCollection.ContinuationToken);

    if (fetchNext)
    {
        if (seekBasedResourceCollection.Links.Next.Headers != null && seekBasedResourceCollection.Links.Next.Headers.Any())
        {
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="10094-127">Ehhez hasonló példát a következő témakörben talál:</span><span class="sxs-lookup"><span data-stu-id="10094-127">For a similar example, see the following:</span></span>

- <span data-ttu-id="10094-128">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="10094-128">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="10094-129">Projekt: **partner Center SDK-minták**</span><span class="sxs-lookup"><span data-stu-id="10094-129">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="10094-130">Osztály: **GetBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="10094-130">Class: **GetBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="10094-131">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="10094-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="10094-132">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="10094-132">Request syntax</span></span>

<span data-ttu-id="10094-133">Az első szintaxissal adja vissza az adott számla összes sorát tartalmazó teljes listát.</span><span class="sxs-lookup"><span data-stu-id="10094-133">Use the first syntax to return a full list of every line item for the given invoice.</span></span> <span data-ttu-id="10094-134">Nagyméretű számlák esetén a második szintaxist a megadott mérettel és 0 alapú eltolással adja vissza a sorok lapozható listájának visszaadásához.</span><span class="sxs-lookup"><span data-stu-id="10094-134">For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> <span data-ttu-id="10094-135">A harmadik szintaxissal szerezheti be a felderítési sorok következő lapját a használatával: `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="10094-135">Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.</span></span>

| <span data-ttu-id="10094-136">Metódus</span><span class="sxs-lookup"><span data-stu-id="10094-136">Method</span></span>  | <span data-ttu-id="10094-137">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="10094-137">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="10094-138">**GET**</span><span class="sxs-lookup"><span data-stu-id="10094-138">**GET**</span></span> | <span data-ttu-id="10094-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? Provider = egykori&invoicelineitemtype = usagelineitems&CurrencyCode = {CURRENCYCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="10094-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span></span>                              |
| <span data-ttu-id="10094-140">**GET**</span><span class="sxs-lookup"><span data-stu-id="10094-140">**GET**</span></span> | <span data-ttu-id="10094-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? Provider = egykori&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &mérete = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="10094-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="10094-142">**GET**</span><span class="sxs-lookup"><span data-stu-id="10094-142">**GET**</span></span> | <span data-ttu-id="10094-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? Provider = egykori&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &méret = {size} &SeekOperation = Next</span><span class="sxs-lookup"><span data-stu-id="10094-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span></span>                               |

#### <a name="uri-parameters"></a><span data-ttu-id="10094-144">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="10094-144">URI parameters</span></span>

<span data-ttu-id="10094-145">A kérelem létrehozásakor használja az alábbi URI-és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="10094-145">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="10094-146">Név</span><span class="sxs-lookup"><span data-stu-id="10094-146">Name</span></span>                   | <span data-ttu-id="10094-147">Típus</span><span class="sxs-lookup"><span data-stu-id="10094-147">Type</span></span>   | <span data-ttu-id="10094-148">Kötelező</span><span class="sxs-lookup"><span data-stu-id="10094-148">Required</span></span> | <span data-ttu-id="10094-149">Leírás</span><span class="sxs-lookup"><span data-stu-id="10094-149">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="10094-150">számlázási azonosító</span><span class="sxs-lookup"><span data-stu-id="10094-150">invoice-id</span></span>             | <span data-ttu-id="10094-151">sztring</span><span class="sxs-lookup"><span data-stu-id="10094-151">string</span></span> | <span data-ttu-id="10094-152">Igen</span><span class="sxs-lookup"><span data-stu-id="10094-152">Yes</span></span>      | <span data-ttu-id="10094-153">A számlát azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="10094-153">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="10094-154">Szolgáltató</span><span class="sxs-lookup"><span data-stu-id="10094-154">provider</span></span>               | <span data-ttu-id="10094-155">sztring</span><span class="sxs-lookup"><span data-stu-id="10094-155">string</span></span> | <span data-ttu-id="10094-156">Igen</span><span class="sxs-lookup"><span data-stu-id="10094-156">Yes</span></span>      | <span data-ttu-id="10094-157">A szolgáltató: "egykori".</span><span class="sxs-lookup"><span data-stu-id="10094-157">The provider: "OneTime".</span></span>                                  |
| <span data-ttu-id="10094-158">számla-sor-tétel típusa</span><span class="sxs-lookup"><span data-stu-id="10094-158">invoice-line-item-type</span></span> | <span data-ttu-id="10094-159">sztring</span><span class="sxs-lookup"><span data-stu-id="10094-159">string</span></span> | <span data-ttu-id="10094-160">Igen</span><span class="sxs-lookup"><span data-stu-id="10094-160">Yes</span></span>      | <span data-ttu-id="10094-161">A számla részleteinek típusa: "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="10094-161">The type of invoice detail: "UsageLineItems".</span></span> |
| <span data-ttu-id="10094-162">currencyCode</span><span class="sxs-lookup"><span data-stu-id="10094-162">currencyCode</span></span>           | <span data-ttu-id="10094-163">sztring</span><span class="sxs-lookup"><span data-stu-id="10094-163">string</span></span> | <span data-ttu-id="10094-164">Igen</span><span class="sxs-lookup"><span data-stu-id="10094-164">Yes</span></span>      | <span data-ttu-id="10094-165">A számlázott sorok pénznemkódja.</span><span class="sxs-lookup"><span data-stu-id="10094-165">The currency code for the billed line items.</span></span>                    |
| <span data-ttu-id="10094-166">period</span><span class="sxs-lookup"><span data-stu-id="10094-166">period</span></span>                 | <span data-ttu-id="10094-167">sztring</span><span class="sxs-lookup"><span data-stu-id="10094-167">string</span></span> | <span data-ttu-id="10094-168">Igen</span><span class="sxs-lookup"><span data-stu-id="10094-168">Yes</span></span>      | <span data-ttu-id="10094-169">A számlázott felderítés időszaka.</span><span class="sxs-lookup"><span data-stu-id="10094-169">The period for billed recon.</span></span> <span data-ttu-id="10094-170">Példa: current, Previous.</span><span class="sxs-lookup"><span data-stu-id="10094-170">example: current, previous.</span></span>        |
| <span data-ttu-id="10094-171">size</span><span class="sxs-lookup"><span data-stu-id="10094-171">size</span></span>                   | <span data-ttu-id="10094-172">szám</span><span class="sxs-lookup"><span data-stu-id="10094-172">number</span></span> | <span data-ttu-id="10094-173">Nem</span><span class="sxs-lookup"><span data-stu-id="10094-173">No</span></span>       | <span data-ttu-id="10094-174">A visszaadni kívánt elemek maximális száma.</span><span class="sxs-lookup"><span data-stu-id="10094-174">The maximum number of items to return.</span></span> <span data-ttu-id="10094-175">Az alapértelmezett méret 2000</span><span class="sxs-lookup"><span data-stu-id="10094-175">Default size is 2000</span></span>       |
| <span data-ttu-id="10094-176">seekOperation</span><span class="sxs-lookup"><span data-stu-id="10094-176">seekOperation</span></span>          | <span data-ttu-id="10094-177">sztring</span><span class="sxs-lookup"><span data-stu-id="10094-177">string</span></span> | <span data-ttu-id="10094-178">No</span><span class="sxs-lookup"><span data-stu-id="10094-178">No</span></span>       | <span data-ttu-id="10094-179">Állítsa be a seekOperation = Next (Beolvasás) elemet a felderítési sorok következő oldalának beolvasásához.</span><span class="sxs-lookup"><span data-stu-id="10094-179">Set seekOperation=Next to get the next page of recon line items.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="10094-180">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="10094-180">Request headers</span></span>

<span data-ttu-id="10094-181">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="10094-181">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="10094-182">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="10094-182">Request body</span></span>

<span data-ttu-id="10094-183">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="10094-183">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="10094-184">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="10094-184">REST response</span></span>

<span data-ttu-id="10094-185">Ha a művelet sikeres, a válasz tartalmazza a sor elem részleteinek gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="10094-185">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="10094-186">A sor **ChargeType** a **megvásárolt** érték az **új** elemre van leképezve.</span><span class="sxs-lookup"><span data-stu-id="10094-186">For the line item **ChargeType**, the value **Purchase** is mapped to **New**.</span></span> <span data-ttu-id="10094-187">Az érték- **visszatérítés** a **megszakításra** van leképezve.</span><span class="sxs-lookup"><span data-stu-id="10094-187">The value **Refund** is mapped to **Cancel**.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="10094-188">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="10094-188">Response success and error codes</span></span>

<span data-ttu-id="10094-189">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="10094-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="10094-190">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="10094-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="10094-191">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="10094-191">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="rest-examples"></a><span data-ttu-id="10094-192">REST-példák</span><span class="sxs-lookup"><span data-stu-id="10094-192">REST examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="10094-193">Kérelem – válasz 1. példa</span><span class="sxs-lookup"><span data-stu-id="10094-193">Request-response example 1</span></span>

<span data-ttu-id="10094-194">A példában szereplő REST-kérelem és-válasz részletei a következők:</span><span class="sxs-lookup"><span data-stu-id="10094-194">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="10094-195">**Szolgáltató**: **egykori**</span><span class="sxs-lookup"><span data-stu-id="10094-195">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="10094-196">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="10094-196">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="10094-197">**Időszak**: **előző**</span><span class="sxs-lookup"><span data-stu-id="10094-197">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="10094-198">1. példa kérés</span><span class="sxs-lookup"><span data-stu-id="10094-198">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="10094-199">1. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="10094-199">Response example 1</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 2,
    "items": [
        {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        },
        {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Ubuntu 16.04 (WebHost)",
            "productName": "Test Test on Linux",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Linux",
            "meterName": "Test Test on Linux - Test Test on Ubuntu 16.04 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TESTRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/testUbuntuTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209951014286867,
            "quantity": 23.350007,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.490235765325545,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.490235765325545,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1999968000511991808131,
            "rateOfPartnerEarnedCredit": 0,
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "AQAAAA=="
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a><span data-ttu-id="10094-200">Kérelem – válasz 2. példa</span><span class="sxs-lookup"><span data-stu-id="10094-200">Request-response example 2</span></span>

<span data-ttu-id="10094-201">A példában szereplő REST-kérelem és-válasz részletei a következők:</span><span class="sxs-lookup"><span data-stu-id="10094-201">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="10094-202">**Szolgáltató**: **egykori**</span><span class="sxs-lookup"><span data-stu-id="10094-202">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="10094-203">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="10094-203">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="10094-204">**Időszak**: **előző**</span><span class="sxs-lookup"><span data-stu-id="10094-204">**Period**: **Previous**</span></span>
- <span data-ttu-id="10094-205">**SeekOperation**: **következő**</span><span class="sxs-lookup"><span data-stu-id="10094-205">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="10094-206">2. példa a kérelemre</span><span class="sxs-lookup"><span data-stu-id="10094-206">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="response-example-2"></a><span data-ttu-id="10094-207">2. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="10094-207">Response example 2</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 1,
    "items": [
          {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1835431430074643112595,
            "rateOfPartnerEarnedCredit": 0.15,

            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
