---
title: Számlázott kereskedelmi használatú sorok elemeinek lekért száma
description: A kereskedelmi használatú számlasorelem (lezárt napi minősített használati sor tétel) gyűjteményét egy adott számlához a következő API Partnerközpont le.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 285b6fbda774c9396dee8947550ed774d52bf901
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446224"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a><span data-ttu-id="7c6c6-103">Számlázott kereskedelmi használatú sorok elemeinek lekért száma</span><span class="sxs-lookup"><span data-stu-id="7c6c6-103">Get invoice billed commercial consumption line items</span></span>

<span data-ttu-id="7c6c6-104">A következő módszerekkel lekértheti a kereskedelmi felhasználású számlasorelemek (más néven a lezárt napi minősített használati sorelemek) részleteit egy adott számlához.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-104">You can use the following methods to get a collection of details for commercial consumption invoice line items (also known as closed daily rated usage line items) for a specified invoice.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7c6c6-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="7c6c6-105">Prerequisites</span></span>

- <span data-ttu-id="7c6c6-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7c6c6-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7c6c6-107">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7c6c6-108">Egy számlaazonosító.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-108">An invoice identifier.</span></span> <span data-ttu-id="7c6c6-109">Ez azonosítja a számlát, amelynek lekéri a sorelemeket.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-109">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="7c6c6-110">C\#</span><span class="sxs-lookup"><span data-stu-id="7c6c6-110">C\#</span></span>

<span data-ttu-id="7c6c6-111">A megadott számla kereskedelmisor-elemeinek lekérése a számlaobjektumot kell lekérnie:</span><span class="sxs-lookup"><span data-stu-id="7c6c6-111">To get the commercial line items for the specified invoice, you must retrieve the invoice object:</span></span>

1. <span data-ttu-id="7c6c6-112">Hívja meg [**a ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) metódust a megadott számlához tartozó számlázási műveletek interfészének lehívása érdekében.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-112">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="7c6c6-113">A [**számlaobjektum lekérése**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódussal.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-113">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="7c6c6-114">A számlaobjektum a megadott számla összes adatát tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-114">The invoice object contains all of the information for the specified invoice.</span></span>

<span data-ttu-id="7c6c6-115">A **Szolgáltató** azonosítja a számlázott részletes adatok forrását (például **egyszer).**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-115">The **Provider** identifies the source of the billed detail information (for example, **onetime**).</span></span> <span data-ttu-id="7c6c6-116">Az **InvoiceLineItemType** megadja a típust (például **UsageLineItem).**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-116">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="7c6c6-117">Az alábbi példakód egy **foreach ciklust használ** a sorelemek gyűjteményének feldolgozásához.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-117">The following example code uses a **foreach** loop to process the line items collection.</span></span> <span data-ttu-id="7c6c6-118">A rendszer külön sorelemek gyűjteményét olvassa be minden **InvoiceLineItemType típushoz.**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-118">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="7c6c6-119">Az InvoiceDetail példánynak megfelelő sorelemek **gyűjteményének lekért** száma:</span><span class="sxs-lookup"><span data-stu-id="7c6c6-119">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="7c6c6-120">Adja át a példány **BillingProvider** és **InvoiceLineItemType** tulajdonságát a [**By metódusnak.**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by)</span><span class="sxs-lookup"><span data-stu-id="7c6c6-120">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="7c6c6-121">A [**társított sorelemek lekérése**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódussal.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-121">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="7c6c6-122">Hozzon létre egy enumerátort, amely az alábbi példában látható módon lépked a gyűjteményen.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-122">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="7c6c6-123">Hasonló példát a következőben láthat:</span><span class="sxs-lookup"><span data-stu-id="7c6c6-123">For a similar example, see the following:</span></span>

- <span data-ttu-id="7c6c6-124">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="7c6c6-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="7c6c6-125">Project: **Partnerközpont SDK minták**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="7c6c6-126">Osztály: **GetBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-126">Class: **GetBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="7c6c6-127">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="7c6c6-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7c6c6-128">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="7c6c6-128">Request syntax</span></span>

<span data-ttu-id="7c6c6-129">Az első szintaxissal az adott számla összes sorelemének teljes listáját használhatja.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-129">Use the first syntax to return a full list of every line item for the given invoice.</span></span> <span data-ttu-id="7c6c6-130">Nagy számlák esetén használja a második szintaxist a megadott mérettel és a 0-alapú eltolással a sorelemek lapszámolt listájának visszaadására.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-130">For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> <span data-ttu-id="7c6c6-131">A harmadik szintaxissal lekérte a sorelemek következő oldalát a `seekOperation = "Next"` használatával.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-131">Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.</span></span>

| <span data-ttu-id="7c6c6-132">Metódus</span><span class="sxs-lookup"><span data-stu-id="7c6c6-132">Method</span></span>  | <span data-ttu-id="7c6c6-133">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="7c6c6-133">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7c6c6-134">**Kap**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-134">**GET**</span></span> | <span data-ttu-id="7c6c6-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7c6c6-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span></span>                              |
| <span data-ttu-id="7c6c6-136">**Kap**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-136">**GET**</span></span> | <span data-ttu-id="7c6c6-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7c6c6-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="7c6c6-138">**Kap**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-138">**GET**</span></span> | <span data-ttu-id="7c6c6-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="7c6c6-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span></span>                               |

#### <a name="uri-parameters"></a><span data-ttu-id="7c6c6-140">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="7c6c6-140">URI parameters</span></span>

<span data-ttu-id="7c6c6-141">A kérelem létrehozásakor használja a következő URI-t és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-141">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="7c6c6-142">Név</span><span class="sxs-lookup"><span data-stu-id="7c6c6-142">Name</span></span>                   | <span data-ttu-id="7c6c6-143">Típus</span><span class="sxs-lookup"><span data-stu-id="7c6c6-143">Type</span></span>   | <span data-ttu-id="7c6c6-144">Kötelező</span><span class="sxs-lookup"><span data-stu-id="7c6c6-144">Required</span></span> | <span data-ttu-id="7c6c6-145">Leírás</span><span class="sxs-lookup"><span data-stu-id="7c6c6-145">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="7c6c6-146">számlaazonosító</span><span class="sxs-lookup"><span data-stu-id="7c6c6-146">invoice-id</span></span>             | <span data-ttu-id="7c6c6-147">sztring</span><span class="sxs-lookup"><span data-stu-id="7c6c6-147">string</span></span> | <span data-ttu-id="7c6c6-148">Igen</span><span class="sxs-lookup"><span data-stu-id="7c6c6-148">Yes</span></span>      | <span data-ttu-id="7c6c6-149">A számlát azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-149">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="7c6c6-150">Szolgáltató</span><span class="sxs-lookup"><span data-stu-id="7c6c6-150">provider</span></span>               | <span data-ttu-id="7c6c6-151">sztring</span><span class="sxs-lookup"><span data-stu-id="7c6c6-151">string</span></span> | <span data-ttu-id="7c6c6-152">Igen</span><span class="sxs-lookup"><span data-stu-id="7c6c6-152">Yes</span></span>      | <span data-ttu-id="7c6c6-153">A szolgáltató: "OneTime".</span><span class="sxs-lookup"><span data-stu-id="7c6c6-153">The provider: "OneTime".</span></span>                                  |
| <span data-ttu-id="7c6c6-154">invoice-line-item-type</span><span class="sxs-lookup"><span data-stu-id="7c6c6-154">invoice-line-item-type</span></span> | <span data-ttu-id="7c6c6-155">sztring</span><span class="sxs-lookup"><span data-stu-id="7c6c6-155">string</span></span> | <span data-ttu-id="7c6c6-156">Igen</span><span class="sxs-lookup"><span data-stu-id="7c6c6-156">Yes</span></span>      | <span data-ttu-id="7c6c6-157">A számla részleteinek típusa: "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="7c6c6-157">The type of invoice detail: "UsageLineItems".</span></span> |
| <span data-ttu-id="7c6c6-158">currencyCode</span><span class="sxs-lookup"><span data-stu-id="7c6c6-158">currencyCode</span></span>           | <span data-ttu-id="7c6c6-159">sztring</span><span class="sxs-lookup"><span data-stu-id="7c6c6-159">string</span></span> | <span data-ttu-id="7c6c6-160">Igen</span><span class="sxs-lookup"><span data-stu-id="7c6c6-160">Yes</span></span>      | <span data-ttu-id="7c6c6-161">A számlázott sorelemek pénznemkódja.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-161">The currency code for the billed line items.</span></span>                    |
| <span data-ttu-id="7c6c6-162">period</span><span class="sxs-lookup"><span data-stu-id="7c6c6-162">period</span></span>                 | <span data-ttu-id="7c6c6-163">sztring</span><span class="sxs-lookup"><span data-stu-id="7c6c6-163">string</span></span> | <span data-ttu-id="7c6c6-164">Igen</span><span class="sxs-lookup"><span data-stu-id="7c6c6-164">Yes</span></span>      | <span data-ttu-id="7c6c6-165">A számlázható recon időszaka.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-165">The period for billed recon.</span></span> <span data-ttu-id="7c6c6-166">például: current, previous.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-166">example: current, previous.</span></span>        |
| <span data-ttu-id="7c6c6-167">size</span><span class="sxs-lookup"><span data-stu-id="7c6c6-167">size</span></span>                   | <span data-ttu-id="7c6c6-168">szám</span><span class="sxs-lookup"><span data-stu-id="7c6c6-168">number</span></span> | <span data-ttu-id="7c6c6-169">Nem</span><span class="sxs-lookup"><span data-stu-id="7c6c6-169">No</span></span>       | <span data-ttu-id="7c6c6-170">A visszaadott elemek maximális száma.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-170">The maximum number of items to return.</span></span> <span data-ttu-id="7c6c6-171">Az alapértelmezett méret 2000</span><span class="sxs-lookup"><span data-stu-id="7c6c6-171">Default size is 2000</span></span>       |
| <span data-ttu-id="7c6c6-172">seekOperation</span><span class="sxs-lookup"><span data-stu-id="7c6c6-172">seekOperation</span></span>          | <span data-ttu-id="7c6c6-173">sztring</span><span class="sxs-lookup"><span data-stu-id="7c6c6-173">string</span></span> | <span data-ttu-id="7c6c6-174">No</span><span class="sxs-lookup"><span data-stu-id="7c6c6-174">No</span></span>       | <span data-ttu-id="7c6c6-175">Állítsa be a seekOperation=Next elemet a felderítési sorelemek következő oldalának le tételhez.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-175">Set seekOperation=Next to get the next page of recon line items.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7c6c6-176">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="7c6c6-176">Request headers</span></span>

<span data-ttu-id="7c6c6-177">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7c6c6-177">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7c6c6-178">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="7c6c6-178">Request body</span></span>

<span data-ttu-id="7c6c6-179">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-179">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="7c6c6-180">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="7c6c6-180">REST response</span></span>

<span data-ttu-id="7c6c6-181">Ha a művelet sikeres, a válasz sorelem-részletek gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-181">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="7c6c6-182">A **ChargeType** sorelem esetében a **Purchase** értéke New (Új) értékre **van leképezve.**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-182">For the line item **ChargeType**, the value **Purchase** is mapped to **New**.</span></span> <span data-ttu-id="7c6c6-183">A Refund **(Visszatérítés)** érték a Cancel (Lemondás) **értékre van leképezve.**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-183">The value **Refund** is mapped to **Cancel**.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7c6c6-184">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="7c6c6-184">Response success and error codes</span></span>

<span data-ttu-id="7c6c6-185">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-185">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7c6c6-186">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="7c6c6-186">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7c6c6-187">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7c6c6-187">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="rest-examples"></a><span data-ttu-id="7c6c6-188">REST-példák</span><span class="sxs-lookup"><span data-stu-id="7c6c6-188">REST examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="7c6c6-189">1. kérés-válasz példa</span><span class="sxs-lookup"><span data-stu-id="7c6c6-189">Request-response example 1</span></span>

<span data-ttu-id="7c6c6-190">A példa REST-kérés és -válasz részletei a következők:</span><span class="sxs-lookup"><span data-stu-id="7c6c6-190">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="7c6c6-191">**Szolgáltató:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-191">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="7c6c6-192">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-192">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="7c6c6-193">**Időszak:** **Előző**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-193">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="7c6c6-194">1. kérési példa</span><span class="sxs-lookup"><span data-stu-id="7c6c6-194">Request example 1</span></span>

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

#### <a name="response-example-1"></a><span data-ttu-id="7c6c6-195">1. válasz példa</span><span class="sxs-lookup"><span data-stu-id="7c6c6-195">Response example 1</span></span>

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
            "creditType": "Credit Not Applied",
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
            "rateOfCredit": 1,
            "creditType": "Azure Credit Applied",
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

### <a name="request-response-example-2"></a><span data-ttu-id="7c6c6-196">2. kérés-válasz példa</span><span class="sxs-lookup"><span data-stu-id="7c6c6-196">Request-response example 2</span></span>

<span data-ttu-id="7c6c6-197">A példa REST-kérés és -válasz részletei a következők:</span><span class="sxs-lookup"><span data-stu-id="7c6c6-197">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="7c6c6-198">**Szolgáltató:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-198">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="7c6c6-199">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-199">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="7c6c6-200">**Időszak:** **Előző**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-200">**Period**: **Previous**</span></span>
- <span data-ttu-id="7c6c6-201">**SeekOperation:** **Tovább**</span><span class="sxs-lookup"><span data-stu-id="7c6c6-201">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="7c6c6-202">2. kérési példa</span><span class="sxs-lookup"><span data-stu-id="7c6c6-202">Request example 2</span></span>

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

## <a name="response-example-2"></a><span data-ttu-id="7c6c6-203">2. válasz példa</span><span class="sxs-lookup"><span data-stu-id="7c6c6-203">Response example 2</span></span>

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
            "rateOfCredit": 0.15,
            "creditType": "Partner Earned Credit Applied",
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
