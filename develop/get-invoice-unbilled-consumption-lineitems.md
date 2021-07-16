---
title: Számlával nem számlázott kereskedelmi használatú sorok elemeinek lekért száma
description: A megadott számlához tartozó ki nem számlázott kereskedelmi használatú tétel részleteinek gyűjteményét a Partnerközpont le.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f7c74bedfd6412fc5954ed2ddc1388936e418fa3
ms.sourcegitcommit: 722992eea6f8ea366dc088e5dd1ee63c17d56f61
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/15/2021
ms.locfileid: "114224768"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a><span data-ttu-id="2cd40-103">Számlával nem számlázott kereskedelmi használatú sorok elemeinek lekért száma</span><span class="sxs-lookup"><span data-stu-id="2cd40-103">Get invoice unbilled commercial consumption line items</span></span>

<span data-ttu-id="2cd40-104">A ki nemszámlázatlan kereskedelmi használatú sortételek részleteinek gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="2cd40-104">How to get a collection of unbilled commercial consumption line item details.</span></span>

<span data-ttu-id="2cd40-105">A következő metódusokkal programozott módon lekért adatok gyűjteménye a ki nemszámlázatlan kereskedelmi használatú sorelemekről (más néven a nyitott használatisor-elemekről).</span><span class="sxs-lookup"><span data-stu-id="2cd40-105">You can use the following methods to get a collection of details unbilled commercial consumption line items (also known as open usage line items) programmatically.</span></span>

>[!NOTE]
><span data-ttu-id="2cd40-106">A napi névleges használat általában 24 órát vesz igénybe a Partnerközpont vagy az API-n keresztüli elérése.</span><span class="sxs-lookup"><span data-stu-id="2cd40-106">Daily-rated usage normally takes 24 hours to appear in Partner Center or to be accessed through the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2cd40-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2cd40-107">Prerequisites</span></span>

- <span data-ttu-id="2cd40-108">A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2cd40-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2cd40-109">Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="2cd40-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="2cd40-110">C\#</span><span class="sxs-lookup"><span data-stu-id="2cd40-110">C\#</span></span>

<span data-ttu-id="2cd40-111">A megadott számlához tartozó sorelemek lekért száma:</span><span class="sxs-lookup"><span data-stu-id="2cd40-111">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="2cd40-112">Hívja meg [**a ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) metódust a megadott számlához tartozó számlázási műveletek interfészének lehívása érdekében.</span><span class="sxs-lookup"><span data-stu-id="2cd40-112">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="2cd40-113">A [**számlaobjektum lekérése**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódussal.</span><span class="sxs-lookup"><span data-stu-id="2cd40-113">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="2cd40-114">A **számlaobjektum** a megadott számla összes adatát tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="2cd40-114">The **invoice object** contains all of the information for the specified invoice.</span></span> <span data-ttu-id="2cd40-115">A **Provider** azonosítja a ki nemszámlázatlan részletes adatok forrását (például **OneTime).**</span><span class="sxs-lookup"><span data-stu-id="2cd40-115">The **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span> <span data-ttu-id="2cd40-116">Az **InvoiceLineItemType** határozza meg a típust (például **UsageLineItem).**</span><span class="sxs-lookup"><span data-stu-id="2cd40-116">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="2cd40-117">Az alábbi példakód egy **foreach ciklust használ** az **InvoiceLineItems gyűjtemény feldolgozásához.**</span><span class="sxs-lookup"><span data-stu-id="2cd40-117">The following example code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="2cd40-118">A rendszer minden **InvoiceLineItemType** típushoz külön sorelemek gyűjteményét olvassa be.</span><span class="sxs-lookup"><span data-stu-id="2cd40-118">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="2cd40-119">Egy InvoiceDetail példánynak megfelelő sorelemek **gyűjteményének legyűjtéséhez:**</span><span class="sxs-lookup"><span data-stu-id="2cd40-119">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="2cd40-120">Adja át a példány **BillingProvider** és **InvoiceLineItemType** tulajdonságát a [**By metódusnak.**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by)</span><span class="sxs-lookup"><span data-stu-id="2cd40-120">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="2cd40-121">A [**társított sorelemek lekérése**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódussal.</span><span class="sxs-lookup"><span data-stu-id="2cd40-121">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="2cd40-122">Hozzon létre egy enumerátort, amely az alábbi példában látható módon lépked át a gyűjteményen.</span><span class="sxs-lookup"><span data-stu-id="2cd40-122">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="2cd40-123">Hasonló példát a következőben láthat:</span><span class="sxs-lookup"><span data-stu-id="2cd40-123">For a similar example, see:</span></span>

- <span data-ttu-id="2cd40-124">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="2cd40-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="2cd40-125">Project: **Partnerközpont SDK minták**</span><span class="sxs-lookup"><span data-stu-id="2cd40-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="2cd40-126">Osztály: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="2cd40-126">Class: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="2cd40-127">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="2cd40-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2cd40-128">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="2cd40-128">Request syntax</span></span>

<span data-ttu-id="2cd40-129">A REST-kéréshez a következő szintaxisokat használhatja, az adott esettől függően.</span><span class="sxs-lookup"><span data-stu-id="2cd40-129">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="2cd40-130">További információért tekintse meg az egyes szintaxisok leírását.</span><span class="sxs-lookup"><span data-stu-id="2cd40-130">For more information, see the descriptions for each syntax.</span></span>

| <span data-ttu-id="2cd40-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="2cd40-131">Method</span></span>  | <span data-ttu-id="2cd40-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2cd40-132">Request URI</span></span>                                                                                                                                                                                              | <span data-ttu-id="2cd40-133">Szintaxishasználati eset leírása</span><span class="sxs-lookup"><span data-stu-id="2cd40-133">Description of syntax use case</span></span>                                                                                                     |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2cd40-134">**Kap**</span><span class="sxs-lookup"><span data-stu-id="2cd40-134">**GET**</span></span> | <span data-ttu-id="2cd40-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2cd40-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                       | <span data-ttu-id="2cd40-136">Ezzel a szintaxissal az adott számla összes sortételének teljes listáját használhatja.</span><span class="sxs-lookup"><span data-stu-id="2cd40-136">Use this syntax to return a full list of every line item for the given invoice.</span></span>                                                    |
| <span data-ttu-id="2cd40-137">**Kap**</span><span class="sxs-lookup"><span data-stu-id="2cd40-137">**GET**</span></span> | <span data-ttu-id="2cd40-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2cd40-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>           | <span data-ttu-id="2cd40-139">Ezt a szintaxist nagy számlákhoz használhatja.</span><span class="sxs-lookup"><span data-stu-id="2cd40-139">Use this syntax for large invoices.</span></span> <span data-ttu-id="2cd40-140">Használja ezt a szintaxist egy megadott mérettel és 0-alapú eltolással a sorelemek lapszámolt listájának visszaadására.</span><span class="sxs-lookup"><span data-stu-id="2cd40-140">Use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="2cd40-141">**Kap**</span><span class="sxs-lookup"><span data-stu-id="2cd40-141">**GET**</span></span> | <span data-ttu-id="2cd40-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="2cd40-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span> | <span data-ttu-id="2cd40-143">Ezzel a szintaxissal lekérte az egyeztetési sorelemek következő oldalát a `seekOperation = "Next"` használatával.</span><span class="sxs-lookup"><span data-stu-id="2cd40-143">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span>                                  |

#### <a name="uri-parameters"></a><span data-ttu-id="2cd40-144">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="2cd40-144">URI parameters</span></span>

<span data-ttu-id="2cd40-145">A kérelem létrehozásakor használja a következő URI-t és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="2cd40-145">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="2cd40-146">Név</span><span class="sxs-lookup"><span data-stu-id="2cd40-146">Name</span></span>                   | <span data-ttu-id="2cd40-147">Típus</span><span class="sxs-lookup"><span data-stu-id="2cd40-147">Type</span></span>   | <span data-ttu-id="2cd40-148">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2cd40-148">Required</span></span> | <span data-ttu-id="2cd40-149">Leírás</span><span class="sxs-lookup"><span data-stu-id="2cd40-149">Description</span></span>                                                                                                                                                                                                                                |
|------------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2cd40-150">Szolgáltató</span><span class="sxs-lookup"><span data-stu-id="2cd40-150">provider</span></span>               | <span data-ttu-id="2cd40-151">sztring</span><span class="sxs-lookup"><span data-stu-id="2cd40-151">string</span></span> | <span data-ttu-id="2cd40-152">Igen</span><span class="sxs-lookup"><span data-stu-id="2cd40-152">Yes</span></span>      | <span data-ttu-id="2cd40-153">A szolgáltató: "**OneTime**".</span><span class="sxs-lookup"><span data-stu-id="2cd40-153">The provider: "**OneTime**".</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="2cd40-154">invoice-line-item-type</span><span class="sxs-lookup"><span data-stu-id="2cd40-154">invoice-line-item-type</span></span> | <span data-ttu-id="2cd40-155">sztring</span><span class="sxs-lookup"><span data-stu-id="2cd40-155">string</span></span> | <span data-ttu-id="2cd40-156">Igen</span><span class="sxs-lookup"><span data-stu-id="2cd40-156">Yes</span></span>      | <span data-ttu-id="2cd40-157">A számla részleteinek típusa: "**UsageLineItems**", "**UsageLineItems**".</span><span class="sxs-lookup"><span data-stu-id="2cd40-157">The type of invoice detail: "**UsageLineItems**", "**UsageLineItems**".</span></span>                                                                                                                                                                    |
| <span data-ttu-id="2cd40-158">currencyCode</span><span class="sxs-lookup"><span data-stu-id="2cd40-158">currencyCode</span></span>           | <span data-ttu-id="2cd40-159">sztring</span><span class="sxs-lookup"><span data-stu-id="2cd40-159">string</span></span> | <span data-ttu-id="2cd40-160">Igen</span><span class="sxs-lookup"><span data-stu-id="2cd40-160">Yes</span></span>      | <span data-ttu-id="2cd40-161">A ki nemszámlázatlan sorelemek pénznemkódja.</span><span class="sxs-lookup"><span data-stu-id="2cd40-161">The currency code for the unbilled line items.</span></span>                                                                                                                                                                                             |
| <span data-ttu-id="2cd40-162">period</span><span class="sxs-lookup"><span data-stu-id="2cd40-162">period</span></span>                 | <span data-ttu-id="2cd40-163">sztring</span><span class="sxs-lookup"><span data-stu-id="2cd40-163">string</span></span> | <span data-ttu-id="2cd40-164">Igen</span><span class="sxs-lookup"><span data-stu-id="2cd40-164">Yes</span></span>      | <span data-ttu-id="2cd40-165">A ki nemszámlázatlan felderítés időtartama (például **aktuális,** **előző).**</span><span class="sxs-lookup"><span data-stu-id="2cd40-165">The period for unbilled recon (for example: **current**, **previous**).</span></span> <span data-ttu-id="2cd40-166">Tegyük fel, hogy januárban le kellkérdezni a számlázási ciklus (01/01/2020 – 01/31/2020) ki nem számlázatlan használati adatait, válassza az időszak **"Aktuális" lehetőséget,** egyébként pedig az **"Előző" lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="2cd40-166">Suppose you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) in January, choose period as **"Current,"** else **"Previous."**</span></span> |
| <span data-ttu-id="2cd40-167">size</span><span class="sxs-lookup"><span data-stu-id="2cd40-167">size</span></span>                   | <span data-ttu-id="2cd40-168">szám</span><span class="sxs-lookup"><span data-stu-id="2cd40-168">number</span></span> | <span data-ttu-id="2cd40-169">Nem</span><span class="sxs-lookup"><span data-stu-id="2cd40-169">No</span></span>       | <span data-ttu-id="2cd40-170">A visszaadott elemek maximális száma.</span><span class="sxs-lookup"><span data-stu-id="2cd40-170">The maximum number of items to return.</span></span> <span data-ttu-id="2cd40-171">Az alapértelmezett méret 2000.</span><span class="sxs-lookup"><span data-stu-id="2cd40-171">The default size is 2000.</span></span>                                                                                                                                                                           |
| <span data-ttu-id="2cd40-172">seekOperation</span><span class="sxs-lookup"><span data-stu-id="2cd40-172">seekOperation</span></span>          | <span data-ttu-id="2cd40-173">sztring</span><span class="sxs-lookup"><span data-stu-id="2cd40-173">string</span></span> | <span data-ttu-id="2cd40-174">No</span><span class="sxs-lookup"><span data-stu-id="2cd40-174">No</span></span>       | <span data-ttu-id="2cd40-175">Állítsa `seekOperation=Next` be az elemet az egyeztetési sorelemek következő oldalának le tételére.</span><span class="sxs-lookup"><span data-stu-id="2cd40-175">Set `seekOperation=Next` to get the next page of reconciliation line items.</span></span>                                                                                                                                                                |

### <a name="request-headers"></a><span data-ttu-id="2cd40-176">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2cd40-176">Request headers</span></span>

<span data-ttu-id="2cd40-177">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2cd40-177">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2cd40-178">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2cd40-178">Request body</span></span>

<span data-ttu-id="2cd40-179">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="2cd40-179">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="2cd40-180">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2cd40-180">REST response</span></span>

<span data-ttu-id="2cd40-181">Ha ez sikeres, a válasz sorelem-részletek gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="2cd40-181">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="2cd40-182">*A **ChargeType** sorelem esetében a Purchase  **(Vásárlás)** értéke New (Új) lesz, a **Refund** (Visszatérítés) pedig Cancel (Lemondás) **értékre van leképezve.***</span><span class="sxs-lookup"><span data-stu-id="2cd40-182">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2cd40-183">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2cd40-183">Response success and error codes</span></span>

<span data-ttu-id="2cd40-184">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="2cd40-184">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2cd40-185">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="2cd40-185">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2cd40-186">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2cd40-186">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="request-response-examples"></a><span data-ttu-id="2cd40-187">Kérés-válasz példák</span><span class="sxs-lookup"><span data-stu-id="2cd40-187">Request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="2cd40-188">1. kérés-válasz példa</span><span class="sxs-lookup"><span data-stu-id="2cd40-188">Request-response example 1</span></span>

<span data-ttu-id="2cd40-189">A következő részletek vonatkoznak erre a példára:</span><span class="sxs-lookup"><span data-stu-id="2cd40-189">The following details apply to this example:</span></span>

- <span data-ttu-id="2cd40-190">**Szolgáltató:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="2cd40-190">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="2cd40-191">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="2cd40-191">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="2cd40-192">**Időszak:** **Előző**</span><span class="sxs-lookup"><span data-stu-id="2cd40-192">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="2cd40-193">1. kérési példa</span><span class="sxs-lookup"><span data-stu-id="2cd40-193">Request example 1</span></span>

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

### <a name="response-example-1"></a><span data-ttu-id="2cd40-194">1. válasz példa</span><span class="sxs-lookup"><span data-stu-id="2cd40-194">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="2cd40-195">2. kérés-válasz példa</span><span class="sxs-lookup"><span data-stu-id="2cd40-195">Request-response example 2</span></span>

<span data-ttu-id="2cd40-196">A következő részletek vonatkoznak erre a példára:</span><span class="sxs-lookup"><span data-stu-id="2cd40-196">The following details apply to this example:</span></span>

- <span data-ttu-id="2cd40-197">**Szolgáltató:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="2cd40-197">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="2cd40-198">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="2cd40-198">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="2cd40-199">**Időszak:** **Előző**</span><span class="sxs-lookup"><span data-stu-id="2cd40-199">**Period**: **Previous**</span></span>
- <span data-ttu-id="2cd40-200">**SeekOperation:** **Tovább**</span><span class="sxs-lookup"><span data-stu-id="2cd40-200">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="2cd40-201">2. kérési példa</span><span class="sxs-lookup"><span data-stu-id="2cd40-201">Request example 2</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="2cd40-202">2. válasz példa</span><span class="sxs-lookup"><span data-stu-id="2cd40-202">Response example 2</span></span>

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
