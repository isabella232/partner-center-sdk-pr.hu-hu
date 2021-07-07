---
title: Számlázatlan kereskedelmi használatú sorok elemeinek lekért száma
description: Egy adott számlához tartozó, nem számlázott kereskedelmi használatú tétel részleteinek gyűjteményét a következő API Partnerközpont le.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1b7dba3333aaec8df73f0e8147b0bbbc78b9b184
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446146"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a><span data-ttu-id="205f2-103">Számlázatlan kereskedelmi használatú sorok elemeinek lekért száma</span><span class="sxs-lookup"><span data-stu-id="205f2-103">Get invoice unbilled commercial consumption line items</span></span>

<span data-ttu-id="205f2-104">A ki nemszámlázatlan kereskedelmi használatú sortételek részleteinek gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="205f2-104">How to get a collection of unbilled commercial consumption line item details.</span></span>

<span data-ttu-id="205f2-105">A következő metódusok használatával programozott módon lekérte a ki nemszámlázatlan kereskedelmi használatú sorelemek (más néven nyitott használatisor-elemek) adatait.</span><span class="sxs-lookup"><span data-stu-id="205f2-105">You can use the following methods to get a collection of details unbilled commercial consumption line items (also known as open usage line items) programmatically.</span></span>

>[!NOTE]
><span data-ttu-id="205f2-106">A napi névleges használat általában 24 órát vesz igénybe, Partnerközpont api-n keresztül jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="205f2-106">Daily-rated usage normally takes 24 hours to appear in Partner Center or to be accessed through the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="205f2-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="205f2-107">Prerequisites</span></span>

- <span data-ttu-id="205f2-108">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="205f2-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="205f2-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="205f2-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="205f2-110">Egy számlaazonosító.</span><span class="sxs-lookup"><span data-stu-id="205f2-110">An invoice identifier.</span></span> <span data-ttu-id="205f2-111">Ez azonosítja a számlát, amelynek lekéri a sorelemeket.</span><span class="sxs-lookup"><span data-stu-id="205f2-111">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="205f2-112">C\#</span><span class="sxs-lookup"><span data-stu-id="205f2-112">C\#</span></span>

<span data-ttu-id="205f2-113">A megadott számlához tartozó sorelemek lekért száma:</span><span class="sxs-lookup"><span data-stu-id="205f2-113">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="205f2-114">Hívja meg [**a ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) metódust a megadott számlához tartozó számlázási műveletek interfészének lehívása érdekében.</span><span class="sxs-lookup"><span data-stu-id="205f2-114">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="205f2-115">A [**számlaobjektum lekérése**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódussal.</span><span class="sxs-lookup"><span data-stu-id="205f2-115">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="205f2-116">A **számlaobjektum** a megadott számla összes adatát tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="205f2-116">The **invoice object** contains all of the information for the specified invoice.</span></span> <span data-ttu-id="205f2-117">A **Provider** azonosítja a ki nemszámlázatlan részletes adatok forrását (például **OneTime).**</span><span class="sxs-lookup"><span data-stu-id="205f2-117">The **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span> <span data-ttu-id="205f2-118">Az **InvoiceLineItemType** megadja a típust (például **UsageLineItem).**</span><span class="sxs-lookup"><span data-stu-id="205f2-118">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="205f2-119">Az alábbi példakód egy **foreach ciklust** használ az **InvoiceLineItems gyűjtemény feldolgozásához.**</span><span class="sxs-lookup"><span data-stu-id="205f2-119">The following example code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="205f2-120">A rendszer külön sorelemek gyűjteményét olvassa be minden **InvoiceLineItemType típushoz.**</span><span class="sxs-lookup"><span data-stu-id="205f2-120">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="205f2-121">Az InvoiceDetail példánynak megfelelő sorelemek **gyűjteményének lekért** száma:</span><span class="sxs-lookup"><span data-stu-id="205f2-121">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="205f2-122">Adja át a példány **BillingProvider** és **InvoiceLineItemType** tulajdonságát a [**By metódusnak.**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by)</span><span class="sxs-lookup"><span data-stu-id="205f2-122">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="205f2-123">A [**társított sorelemek lekérése**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódussal.</span><span class="sxs-lookup"><span data-stu-id="205f2-123">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="205f2-124">Hozzon létre egy enumerátort, amely az alábbi példában látható módon lépked a gyűjteményen.</span><span class="sxs-lookup"><span data-stu-id="205f2-124">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine items count: " + seekBasedResourceCollection.Items.Count());

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
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="205f2-125">Hasonló példát a következőben láthat:</span><span class="sxs-lookup"><span data-stu-id="205f2-125">For a similar example, see:</span></span>

- <span data-ttu-id="205f2-126">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="205f2-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="205f2-127">Project: **Partnerközpont SDK minták**</span><span class="sxs-lookup"><span data-stu-id="205f2-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="205f2-128">Osztály: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="205f2-128">Class: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="205f2-129">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="205f2-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="205f2-130">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="205f2-130">Request syntax</span></span>

<span data-ttu-id="205f2-131">A REST-kéréshez a következő szintaxisokat használhatja a saját esetétől függően.</span><span class="sxs-lookup"><span data-stu-id="205f2-131">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="205f2-132">További információért tekintse meg az egyes szintaxisok leírását.</span><span class="sxs-lookup"><span data-stu-id="205f2-132">For more information, see the descriptions for each syntax.</span></span>

| <span data-ttu-id="205f2-133">Metódus</span><span class="sxs-lookup"><span data-stu-id="205f2-133">Method</span></span>  | <span data-ttu-id="205f2-134">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="205f2-134">Request URI</span></span>                                                                                                                                                                                              | <span data-ttu-id="205f2-135">Szintaxishasználati eset leírása</span><span class="sxs-lookup"><span data-stu-id="205f2-135">Description of syntax use case</span></span>                                                                                                     |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="205f2-136">**Kap**</span><span class="sxs-lookup"><span data-stu-id="205f2-136">**GET**</span></span> | <span data-ttu-id="205f2-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="205f2-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                       | <span data-ttu-id="205f2-138">Ezzel a szintaxissal az adott számla összes sorelemének teljes listáját használhatja.</span><span class="sxs-lookup"><span data-stu-id="205f2-138">Use this syntax to return a full list of every line item for the given invoice.</span></span>                                                    |
| <span data-ttu-id="205f2-139">**Kap**</span><span class="sxs-lookup"><span data-stu-id="205f2-139">**GET**</span></span> | <span data-ttu-id="205f2-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="205f2-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>           | <span data-ttu-id="205f2-141">Ezt a szintaxist nagy számlákhoz használja.</span><span class="sxs-lookup"><span data-stu-id="205f2-141">Use this syntax for large invoices.</span></span> <span data-ttu-id="205f2-142">Használja ezt a szintaxist a megadott mérettel és 0-alapú eltolással a sorelemek lapszámolt listájának visszaadására.</span><span class="sxs-lookup"><span data-stu-id="205f2-142">Use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="205f2-143">**Kap**</span><span class="sxs-lookup"><span data-stu-id="205f2-143">**GET**</span></span> | <span data-ttu-id="205f2-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="205f2-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span> | <span data-ttu-id="205f2-145">Ezzel a szintaxissal lekérte az egyeztetési sorelemek következő oldalát a `seekOperation = "Next"` használatával.</span><span class="sxs-lookup"><span data-stu-id="205f2-145">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span>                                  |

#### <a name="uri-parameters"></a><span data-ttu-id="205f2-146">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="205f2-146">URI parameters</span></span>

<span data-ttu-id="205f2-147">A kérelem létrehozásakor használja a következő URI-t és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="205f2-147">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="205f2-148">Név</span><span class="sxs-lookup"><span data-stu-id="205f2-148">Name</span></span>                   | <span data-ttu-id="205f2-149">Típus</span><span class="sxs-lookup"><span data-stu-id="205f2-149">Type</span></span>   | <span data-ttu-id="205f2-150">Kötelező</span><span class="sxs-lookup"><span data-stu-id="205f2-150">Required</span></span> | <span data-ttu-id="205f2-151">Leírás</span><span class="sxs-lookup"><span data-stu-id="205f2-151">Description</span></span>                                                                                                                                                                                                                                |
|------------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="205f2-152">Szolgáltató</span><span class="sxs-lookup"><span data-stu-id="205f2-152">provider</span></span>               | <span data-ttu-id="205f2-153">sztring</span><span class="sxs-lookup"><span data-stu-id="205f2-153">string</span></span> | <span data-ttu-id="205f2-154">Igen</span><span class="sxs-lookup"><span data-stu-id="205f2-154">Yes</span></span>      | <span data-ttu-id="205f2-155">A szolgáltató: "**OneTime**".</span><span class="sxs-lookup"><span data-stu-id="205f2-155">The provider: "**OneTime**".</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="205f2-156">invoice-line-item-type</span><span class="sxs-lookup"><span data-stu-id="205f2-156">invoice-line-item-type</span></span> | <span data-ttu-id="205f2-157">sztring</span><span class="sxs-lookup"><span data-stu-id="205f2-157">string</span></span> | <span data-ttu-id="205f2-158">Igen</span><span class="sxs-lookup"><span data-stu-id="205f2-158">Yes</span></span>      | <span data-ttu-id="205f2-159">A számla részleteinek típusa: "**UsageLineItems**", "**UsageLineItems**".</span><span class="sxs-lookup"><span data-stu-id="205f2-159">The type of invoice detail: "**UsageLineItems**", "**UsageLineItems**".</span></span>                                                                                                                                                                    |
| <span data-ttu-id="205f2-160">currencyCode</span><span class="sxs-lookup"><span data-stu-id="205f2-160">currencyCode</span></span>           | <span data-ttu-id="205f2-161">sztring</span><span class="sxs-lookup"><span data-stu-id="205f2-161">string</span></span> | <span data-ttu-id="205f2-162">Igen</span><span class="sxs-lookup"><span data-stu-id="205f2-162">Yes</span></span>      | <span data-ttu-id="205f2-163">A ki nemszámlázatlan sorelemek pénznemkódja.</span><span class="sxs-lookup"><span data-stu-id="205f2-163">The currency code for the unbilled line items.</span></span>                                                                                                                                                                                             |
| <span data-ttu-id="205f2-164">period</span><span class="sxs-lookup"><span data-stu-id="205f2-164">period</span></span>                 | <span data-ttu-id="205f2-165">sztring</span><span class="sxs-lookup"><span data-stu-id="205f2-165">string</span></span> | <span data-ttu-id="205f2-166">Igen</span><span class="sxs-lookup"><span data-stu-id="205f2-166">Yes</span></span>      | <span data-ttu-id="205f2-167">A nemszámlázatlan felderítés időtartama (például **aktuális,** **előző**).</span><span class="sxs-lookup"><span data-stu-id="205f2-167">The period for unbilled recon (for example: **current**, **previous**).</span></span> <span data-ttu-id="205f2-168">Tegyük fel, hogy januárban le kellkérdezni a számlázási ciklus ki nem számlázatlan használati adatait (2020.01.01. – 01.31.) 2020. januárban, válassza az **időszak "Aktuális" lehetőséget,** egyébként pedig az **"Előző" lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="205f2-168">Suppose you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) in January, choose period as **"Current,"** else **"Previous."**</span></span> |
| <span data-ttu-id="205f2-169">size</span><span class="sxs-lookup"><span data-stu-id="205f2-169">size</span></span>                   | <span data-ttu-id="205f2-170">szám</span><span class="sxs-lookup"><span data-stu-id="205f2-170">number</span></span> | <span data-ttu-id="205f2-171">Nem</span><span class="sxs-lookup"><span data-stu-id="205f2-171">No</span></span>       | <span data-ttu-id="205f2-172">A visszaadott elemek maximális száma.</span><span class="sxs-lookup"><span data-stu-id="205f2-172">The maximum number of items to return.</span></span> <span data-ttu-id="205f2-173">Az alapértelmezett méret 2000.</span><span class="sxs-lookup"><span data-stu-id="205f2-173">The default size is 2000.</span></span>                                                                                                                                                                           |
| <span data-ttu-id="205f2-174">seekOperation</span><span class="sxs-lookup"><span data-stu-id="205f2-174">seekOperation</span></span>          | <span data-ttu-id="205f2-175">sztring</span><span class="sxs-lookup"><span data-stu-id="205f2-175">string</span></span> | <span data-ttu-id="205f2-176">No</span><span class="sxs-lookup"><span data-stu-id="205f2-176">No</span></span>       | <span data-ttu-id="205f2-177">Állítsa `seekOperation=Next` be az elemet az egyeztetési sorelemek következő oldalának le tételére.</span><span class="sxs-lookup"><span data-stu-id="205f2-177">Set `seekOperation=Next` to get the next page of reconciliation line items.</span></span>                                                                                                                                                                |

### <a name="request-headers"></a><span data-ttu-id="205f2-178">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="205f2-178">Request headers</span></span>

<span data-ttu-id="205f2-179">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="205f2-179">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="205f2-180">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="205f2-180">Request body</span></span>

<span data-ttu-id="205f2-181">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="205f2-181">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="205f2-182">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="205f2-182">REST response</span></span>

<span data-ttu-id="205f2-183">Ha a művelet sikeres, a válasz sorelem-részletek gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="205f2-183">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="205f2-184">*A **ChargeType** sorelem esetében a **Purchase** (Vásárlás) értéke **New** (Új) értékre van leképezve, a **Refund** (Visszatérítés) értéke pedig Cancel (Lemondás) értékre **van leképezve.***</span><span class="sxs-lookup"><span data-stu-id="205f2-184">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="205f2-185">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="205f2-185">Response success and error codes</span></span>

<span data-ttu-id="205f2-186">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="205f2-186">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="205f2-187">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="205f2-187">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="205f2-188">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="205f2-188">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="request-response-examples"></a><span data-ttu-id="205f2-189">Példák kérés-válasz válaszra</span><span class="sxs-lookup"><span data-stu-id="205f2-189">Request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="205f2-190">1. kérés-válasz példa</span><span class="sxs-lookup"><span data-stu-id="205f2-190">Request-response example 1</span></span>

<span data-ttu-id="205f2-191">A következő részletek vonatkoznak erre a példára:</span><span class="sxs-lookup"><span data-stu-id="205f2-191">The following details apply to this example:</span></span>

- <span data-ttu-id="205f2-192">**Szolgáltató:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="205f2-192">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="205f2-193">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="205f2-193">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="205f2-194">**Időszak:** **Előző**</span><span class="sxs-lookup"><span data-stu-id="205f2-194">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="205f2-195">1. kérési példa</span><span class="sxs-lookup"><span data-stu-id="205f2-195">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

### <a name="response-example-1"></a><span data-ttu-id="205f2-196">1. válasz példa</span><span class="sxs-lookup"><span data-stu-id="205f2-196">Response example 1</span></span>

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
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-01T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "1234547f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 0,
            "creditType": "Credit Not Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
         },
         {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d12345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 1,
            "creditType": "Azure Credit Applied",
            "invoiceLineItemTypce": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
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

### <a name="request-response-example-2"></a><span data-ttu-id="205f2-197">2. kérés-válasz példa</span><span class="sxs-lookup"><span data-stu-id="205f2-197">Request-response example 2</span></span>

<span data-ttu-id="205f2-198">A következő részletek vonatkoznak erre a példára:</span><span class="sxs-lookup"><span data-stu-id="205f2-198">The following details apply to this example:</span></span>

- <span data-ttu-id="205f2-199">**Szolgáltató:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="205f2-199">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="205f2-200">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="205f2-200">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="205f2-201">**Időszak:** **Előző**</span><span class="sxs-lookup"><span data-stu-id="205f2-201">**Period**: **Previous**</span></span>
- <span data-ttu-id="205f2-202">**SeekOperation:** **Tovább**</span><span class="sxs-lookup"><span data-stu-id="205f2-202">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="205f2-203">2. kérési példa</span><span class="sxs-lookup"><span data-stu-id="205f2-203">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="205f2-204">2. válasz példa</span><span class="sxs-lookup"><span data-stu-id="205f2-204">Response example 2</span></span>

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
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0.15,
            "rateOfCredit": 0.15,
            "creditType": "Partner Earned Credit Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
