---
title: Számlázott kereskedelmi fogyasztási sorok beolvasása
description: A partner Center API-k használatával beszerezhet egy adott számlára vonatkozó, nem számlázott kereskedelmi fogyasztási sor részleteit tartalmazó gyűjteményt.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8b6ca8d6ff7af53dd2a258ea20e6eaeb26421440
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274665"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a><span data-ttu-id="284ab-103">Számlázott kereskedelmi fogyasztási sorok beolvasása</span><span class="sxs-lookup"><span data-stu-id="284ab-103">Get invoice unbilled commercial consumption line items</span></span>

<span data-ttu-id="284ab-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="284ab-104">**Applies to:**</span></span>

- <span data-ttu-id="284ab-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="284ab-105">Partner Center</span></span>

<span data-ttu-id="284ab-106">A nem számlázott kereskedelmi fogyasztási sorokra vonatkozó részletek gyűjteményének beolvasása.</span><span class="sxs-lookup"><span data-stu-id="284ab-106">How to get a collection of unbilled commercial consumption line item details.</span></span>

<span data-ttu-id="284ab-107">A következő módszerekkel lekérheti a nem számlázott kereskedelmi fogyasztási sorok (más néven nyitott használati sorok) részletes gyűjteményét programozott módon.</span><span class="sxs-lookup"><span data-stu-id="284ab-107">You can use the following methods to get a collection of details unbilled commercial consumption line items (also known as open usage line items) programmatically.</span></span>

>[!NOTE]
><span data-ttu-id="284ab-108">A napi névleges használat általában 24 órát vesz igénybe a partner Centerben, vagy az API-n keresztül érhető el.</span><span class="sxs-lookup"><span data-stu-id="284ab-108">Daily-rated usage normally takes 24 hours to appear in Partner Center or to be accessed through the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="284ab-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="284ab-109">Prerequisites</span></span>

- <span data-ttu-id="284ab-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="284ab-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="284ab-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="284ab-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="284ab-112">Egy fiókazonosító.</span><span class="sxs-lookup"><span data-stu-id="284ab-112">An invoice identifier.</span></span> <span data-ttu-id="284ab-113">Ez azonosítja azt a számlát, amelynek a sorát be kell olvasni.</span><span class="sxs-lookup"><span data-stu-id="284ab-113">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="284ab-114">C\#</span><span class="sxs-lookup"><span data-stu-id="284ab-114">C\#</span></span>

<span data-ttu-id="284ab-115">A megadott számla vonali elemeinek beolvasása:</span><span class="sxs-lookup"><span data-stu-id="284ab-115">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="284ab-116">Hívja meg a [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) metódust, hogy lekérje a megadott számla műveleteinek számlázására szolgáló felületet.</span><span class="sxs-lookup"><span data-stu-id="284ab-116">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="284ab-117">Hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódust a számla objektum lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="284ab-117">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="284ab-118">A **számla objektum** a megadott számla összes adatát tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="284ab-118">The **invoice object** contains all of the information for the specified invoice.</span></span> <span data-ttu-id="284ab-119">A **szolgáltató** azonosítja a nem számlázott részletes információk forrását (például **egykori**).</span><span class="sxs-lookup"><span data-stu-id="284ab-119">The **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span> <span data-ttu-id="284ab-120">A **InvoiceLineItemType** meghatározza a típust (például **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="284ab-120">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="284ab-121">Az alábbi mintakód egy **foreach** hurkot használ a **InvoiceLineItems** -gyűjtemény feldolgozásához.</span><span class="sxs-lookup"><span data-stu-id="284ab-121">The following example code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="284ab-122">Az egyes **InvoiceLineItemType** tartozó sorok külön gyűjteménye lesz beolvasva.</span><span class="sxs-lookup"><span data-stu-id="284ab-122">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="284ab-123">Egy **InvoiceDetail** -példánynak megfelelő sorok gyűjteményének beolvasása:</span><span class="sxs-lookup"><span data-stu-id="284ab-123">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="284ab-124">Adja át a példány **BillingProvider** és **InvoiceLineItemType** a [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) metódusnak.</span><span class="sxs-lookup"><span data-stu-id="284ab-124">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="284ab-125">A társított sorok beolvasásához hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="284ab-125">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="284ab-126">Hozzon létre egy enumerálást a gyűjtemény átjárásához az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="284ab-126">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="284ab-127">Ehhez hasonló példát a következő témakörben talál:</span><span class="sxs-lookup"><span data-stu-id="284ab-127">For a similar example, see:</span></span>

- <span data-ttu-id="284ab-128">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="284ab-128">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="284ab-129">Projekt: **partner Center SDK-minták**</span><span class="sxs-lookup"><span data-stu-id="284ab-129">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="284ab-130">Osztály: **GetUnBilledConsumptionReconLineItemsPaging. cs**</span><span class="sxs-lookup"><span data-stu-id="284ab-130">Class: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="284ab-131">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="284ab-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="284ab-132">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="284ab-132">Request syntax</span></span>

<span data-ttu-id="284ab-133">A REST-kérelemhez a használati esettől függően a következő szintaxist használhatja.</span><span class="sxs-lookup"><span data-stu-id="284ab-133">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="284ab-134">További információkért tekintse meg az egyes szintaxisok leírását.</span><span class="sxs-lookup"><span data-stu-id="284ab-134">For more information, see the descriptions for each syntax.</span></span>

| <span data-ttu-id="284ab-135">Metódus</span><span class="sxs-lookup"><span data-stu-id="284ab-135">Method</span></span>  | <span data-ttu-id="284ab-136">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="284ab-136">Request URI</span></span>                                                                                                                                                                                              | <span data-ttu-id="284ab-137">Szintaxis használati esetének leírása</span><span class="sxs-lookup"><span data-stu-id="284ab-137">Description of syntax use case</span></span>                                                                                                     |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="284ab-138">**GET**</span><span class="sxs-lookup"><span data-stu-id="284ab-138">**GET**</span></span> | <span data-ttu-id="284ab-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/UNBILLED/lineitems? Provider = egykori&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &időszak = {period} http/1.1</span><span class="sxs-lookup"><span data-stu-id="284ab-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                       | <span data-ttu-id="284ab-140">Ezzel a szintaxissal teljes listát adhat vissza az adott számlához tartozó összes sor tételről.</span><span class="sxs-lookup"><span data-stu-id="284ab-140">Use this syntax to return a full list of every line item for the given invoice.</span></span>                                                    |
| <span data-ttu-id="284ab-141">**GET**</span><span class="sxs-lookup"><span data-stu-id="284ab-141">**GET**</span></span> | <span data-ttu-id="284ab-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/UNBILLED/lineitems? Provider = egykori&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &időszak = {period} &mérete = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="284ab-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>           | <span data-ttu-id="284ab-143">Használja ezt a szintaxist nagyméretű számlákhoz.</span><span class="sxs-lookup"><span data-stu-id="284ab-143">Use this syntax for large invoices.</span></span> <span data-ttu-id="284ab-144">Ezt a szintaxist egy megadott mérettel és 0-alapú eltolással használhatja a sorok lapozható listájának visszaadásához.</span><span class="sxs-lookup"><span data-stu-id="284ab-144">Use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="284ab-145">**GET**</span><span class="sxs-lookup"><span data-stu-id="284ab-145">**GET**</span></span> | <span data-ttu-id="284ab-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/UNBILLED/lineitems? Provider = egykori&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &időszak = {period} &mérete = {size} &SeekOperation = tovább</span><span class="sxs-lookup"><span data-stu-id="284ab-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span> | <span data-ttu-id="284ab-147">Ezzel a szintaxissal beolvashatja az egyeztetési sorok következő oldalát a használatával `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="284ab-147">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span>                                  |

#### <a name="uri-parameters"></a><span data-ttu-id="284ab-148">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="284ab-148">URI parameters</span></span>

<span data-ttu-id="284ab-149">A kérelem létrehozásakor használja az alábbi URI-és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="284ab-149">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="284ab-150">Név</span><span class="sxs-lookup"><span data-stu-id="284ab-150">Name</span></span>                   | <span data-ttu-id="284ab-151">Típus</span><span class="sxs-lookup"><span data-stu-id="284ab-151">Type</span></span>   | <span data-ttu-id="284ab-152">Kötelező</span><span class="sxs-lookup"><span data-stu-id="284ab-152">Required</span></span> | <span data-ttu-id="284ab-153">Leírás</span><span class="sxs-lookup"><span data-stu-id="284ab-153">Description</span></span>                                                                                                                                                                                                                                |
|------------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="284ab-154">Szolgáltató</span><span class="sxs-lookup"><span data-stu-id="284ab-154">provider</span></span>               | <span data-ttu-id="284ab-155">sztring</span><span class="sxs-lookup"><span data-stu-id="284ab-155">string</span></span> | <span data-ttu-id="284ab-156">Igen</span><span class="sxs-lookup"><span data-stu-id="284ab-156">Yes</span></span>      | <span data-ttu-id="284ab-157">A szolgáltató: "**egykori**".</span><span class="sxs-lookup"><span data-stu-id="284ab-157">The provider: "**OneTime**".</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="284ab-158">számla-sor-tétel típusa</span><span class="sxs-lookup"><span data-stu-id="284ab-158">invoice-line-item-type</span></span> | <span data-ttu-id="284ab-159">sztring</span><span class="sxs-lookup"><span data-stu-id="284ab-159">string</span></span> | <span data-ttu-id="284ab-160">Igen</span><span class="sxs-lookup"><span data-stu-id="284ab-160">Yes</span></span>      | <span data-ttu-id="284ab-161">A számla részleteinek típusa: "**UsageLineItems**", "**UsageLineItems**".</span><span class="sxs-lookup"><span data-stu-id="284ab-161">The type of invoice detail: "**UsageLineItems**", "**UsageLineItems**".</span></span>                                                                                                                                                                    |
| <span data-ttu-id="284ab-162">currencyCode</span><span class="sxs-lookup"><span data-stu-id="284ab-162">currencyCode</span></span>           | <span data-ttu-id="284ab-163">sztring</span><span class="sxs-lookup"><span data-stu-id="284ab-163">string</span></span> | <span data-ttu-id="284ab-164">Igen</span><span class="sxs-lookup"><span data-stu-id="284ab-164">Yes</span></span>      | <span data-ttu-id="284ab-165">A nem számlázott sorok pénznemkódja.</span><span class="sxs-lookup"><span data-stu-id="284ab-165">The currency code for the unbilled line items.</span></span>                                                                                                                                                                                             |
| <span data-ttu-id="284ab-166">period</span><span class="sxs-lookup"><span data-stu-id="284ab-166">period</span></span>                 | <span data-ttu-id="284ab-167">sztring</span><span class="sxs-lookup"><span data-stu-id="284ab-167">string</span></span> | <span data-ttu-id="284ab-168">Igen</span><span class="sxs-lookup"><span data-stu-id="284ab-168">Yes</span></span>      | <span data-ttu-id="284ab-169">A nem számlázott felderítés időtartama (például: **current**, **Previous**).</span><span class="sxs-lookup"><span data-stu-id="284ab-169">The period for unbilled recon (for example: **current**, **previous**).</span></span> <span data-ttu-id="284ab-170">Tegyük fel, hogy a számlázási ciklus (01/01/2020 – 01/31/2020) nem számlázott használati adatait kell lekérdezni januárban, válassza a **"jelenlegi",** "else **" (előző) lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="284ab-170">Suppose you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) in January, choose period as **"Current,"** else **"Previous."**</span></span> |
| <span data-ttu-id="284ab-171">size</span><span class="sxs-lookup"><span data-stu-id="284ab-171">size</span></span>                   | <span data-ttu-id="284ab-172">szám</span><span class="sxs-lookup"><span data-stu-id="284ab-172">number</span></span> | <span data-ttu-id="284ab-173">Nem</span><span class="sxs-lookup"><span data-stu-id="284ab-173">No</span></span>       | <span data-ttu-id="284ab-174">A visszaadni kívánt elemek maximális száma.</span><span class="sxs-lookup"><span data-stu-id="284ab-174">The maximum number of items to return.</span></span> <span data-ttu-id="284ab-175">Az alapértelmezett méret 2000.</span><span class="sxs-lookup"><span data-stu-id="284ab-175">The default size is 2000.</span></span>                                                                                                                                                                           |
| <span data-ttu-id="284ab-176">seekOperation</span><span class="sxs-lookup"><span data-stu-id="284ab-176">seekOperation</span></span>          | <span data-ttu-id="284ab-177">sztring</span><span class="sxs-lookup"><span data-stu-id="284ab-177">string</span></span> | <span data-ttu-id="284ab-178">No</span><span class="sxs-lookup"><span data-stu-id="284ab-178">No</span></span>       | <span data-ttu-id="284ab-179">Állítsa be `seekOperation=Next` az egyeztetési sorok következő oldalának beolvasásához.</span><span class="sxs-lookup"><span data-stu-id="284ab-179">Set `seekOperation=Next` to get the next page of reconciliation line items.</span></span>                                                                                                                                                                |

### <a name="request-headers"></a><span data-ttu-id="284ab-180">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="284ab-180">Request headers</span></span>

<span data-ttu-id="284ab-181">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="284ab-181">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="284ab-182">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="284ab-182">Request body</span></span>

<span data-ttu-id="284ab-183">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="284ab-183">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="284ab-184">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="284ab-184">REST response</span></span>

<span data-ttu-id="284ab-185">Ha a művelet sikeres, a válasz tartalmazza a sor elem részleteinek gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="284ab-185">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="284ab-186">*A sor **ChargeType** az érték **megvásárlása** **újra** van leképezve, és az érték- **visszatérítés** a **megszakításra** van leképezve.*</span><span class="sxs-lookup"><span data-stu-id="284ab-186">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="284ab-187">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="284ab-187">Response success and error codes</span></span>

<span data-ttu-id="284ab-188">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="284ab-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="284ab-189">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="284ab-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="284ab-190">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="284ab-190">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="request-response-examples"></a><span data-ttu-id="284ab-191">Kérelem – válasz példák</span><span class="sxs-lookup"><span data-stu-id="284ab-191">Request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="284ab-192">Kérelem – válasz 1. példa</span><span class="sxs-lookup"><span data-stu-id="284ab-192">Request-response example 1</span></span>

<span data-ttu-id="284ab-193">A következő részletek a példára vonatkoznak:</span><span class="sxs-lookup"><span data-stu-id="284ab-193">The following details apply to this example:</span></span>

- <span data-ttu-id="284ab-194">**Szolgáltató**: **egykori**</span><span class="sxs-lookup"><span data-stu-id="284ab-194">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="284ab-195">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="284ab-195">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="284ab-196">**Időszak**: **előző**</span><span class="sxs-lookup"><span data-stu-id="284ab-196">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="284ab-197">1. példa kérés</span><span class="sxs-lookup"><span data-stu-id="284ab-197">Request example 1</span></span>

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

### <a name="response-example-1"></a><span data-ttu-id="284ab-198">1. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="284ab-198">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="284ab-199">Kérelem – válasz 2. példa</span><span class="sxs-lookup"><span data-stu-id="284ab-199">Request-response example 2</span></span>

<span data-ttu-id="284ab-200">A következő részletek a példára vonatkoznak:</span><span class="sxs-lookup"><span data-stu-id="284ab-200">The following details apply to this example:</span></span>

- <span data-ttu-id="284ab-201">**Szolgáltató**: **egykori**</span><span class="sxs-lookup"><span data-stu-id="284ab-201">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="284ab-202">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="284ab-202">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="284ab-203">**Időszak**: **előző**</span><span class="sxs-lookup"><span data-stu-id="284ab-203">**Period**: **Previous**</span></span>
- <span data-ttu-id="284ab-204">**SeekOperation**: **következő**</span><span class="sxs-lookup"><span data-stu-id="284ab-204">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="284ab-205">2. példa a kérelemre</span><span class="sxs-lookup"><span data-stu-id="284ab-205">Request example 2</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="284ab-206">2. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="284ab-206">Response example 2</span></span>

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
