---
title: Számla nem számlázott egyeztetési sora beolvasása
description: A partner Center API-k használatával a megadott időszakra vonatkozó, nem számlázott egyeztetési sor részleteinek gyűjteményét szerezheti be.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: ff69798ddfd91fca817ec0d047bf407f326066c2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768443"
---
# <a name="get-invoices-unbilled-reconciliation-line-items"></a><span data-ttu-id="f2c50-103">Számla nem számlázott egyeztetési sora beolvasása</span><span class="sxs-lookup"><span data-stu-id="f2c50-103">Get invoice's unbilled reconciliation line items</span></span>

<span data-ttu-id="f2c50-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="f2c50-104">**Applies to:**</span></span>

- <span data-ttu-id="f2c50-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f2c50-105">Partner Center</span></span>
- <span data-ttu-id="f2c50-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="f2c50-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f2c50-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f2c50-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f2c50-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f2c50-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f2c50-109">A következő módszerekkel részletesen megtudhatja a nem számlázott számlasorok (más néven nyitott számlázási sorok) részleteit.</span><span class="sxs-lookup"><span data-stu-id="f2c50-109">You can use the following methods get a collection of details for unbilled invoice line items (also known as open billing line items).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2c50-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f2c50-110">Prerequisites</span></span>

- <span data-ttu-id="f2c50-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="f2c50-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f2c50-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="f2c50-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f2c50-113">Egy fiókazonosító.</span><span class="sxs-lookup"><span data-stu-id="f2c50-113">An invoice identifier.</span></span> <span data-ttu-id="f2c50-114">Ez azonosítja azt a számlát, amelynek a sorát be kell olvasni.</span><span class="sxs-lookup"><span data-stu-id="f2c50-114">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="f2c50-115">C\#</span><span class="sxs-lookup"><span data-stu-id="f2c50-115">C\#</span></span>

<span data-ttu-id="f2c50-116">A megadott számla vonali elemeinek lekéréséhez kérje le a számla objektumot:</span><span class="sxs-lookup"><span data-stu-id="f2c50-116">To get the line items for the specified invoice, retrieve the invoice object:</span></span>

1. <span data-ttu-id="f2c50-117">Hívja meg a [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) metódust, hogy lekérje a megadott számla műveleteinek számlázására szolgáló felületet.</span><span class="sxs-lookup"><span data-stu-id="f2c50-117">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="f2c50-118">Hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódust a számla objektum lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="f2c50-118">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="f2c50-119">A számla objektum a megadott számla összes adatát tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="f2c50-119">The invoice object contains all of the information for the specified invoice:</span></span>

- <span data-ttu-id="f2c50-120">A **szolgáltató** azonosítja a nem számlázott részletes információk forrását (például **egykori**).</span><span class="sxs-lookup"><span data-stu-id="f2c50-120">**Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span>

- <span data-ttu-id="f2c50-121">A **InvoiceLineItemType** meghatározza a típust (például **BillingLineItem**).</span><span class="sxs-lookup"><span data-stu-id="f2c50-121">**InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).</span></span>

<span data-ttu-id="f2c50-122">Egy **InvoiceDetail** -példánynak megfelelő sorok gyűjteményének beolvasása:</span><span class="sxs-lookup"><span data-stu-id="f2c50-122">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="f2c50-123">Adja át a példány BillingProvider és InvoiceLineItemType a [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) metódusnak.</span><span class="sxs-lookup"><span data-stu-id="f2c50-123">Pass the instance's BillingProvider and InvoiceLineItemType to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="f2c50-124">A társított sorok beolvasásához hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="f2c50-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>

3. <span data-ttu-id="f2c50-125">Hozzon létre egy enumerálást a gyűjtemény bejárásához.</span><span class="sxs-lookup"><span data-stu-id="f2c50-125">Create an enumerator to traverse the collection.</span></span> <span data-ttu-id="f2c50-126">Példaként tekintse meg a következő mintakód-kódot.</span><span class="sxs-lookup"><span data-stu-id="f2c50-126">For an example, see the following sample code.</span></span>

<span data-ttu-id="f2c50-127">A következő mintakód egy **foreach** hurok használatával dolgozza fel a **InvoiceLineItems** -gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="f2c50-127">The following sample code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="f2c50-128">Az egyes **InvoiceLineItemType** tartozó sorok külön gyűjteménye lesz beolvasva.</span><span class="sxs-lookup"><span data-stu-id="f2c50-128">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string currencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type OneTimeInvoiceLineItem
        if (item is OneTimeInvoiceLineItem)
        {
            Type t = typeof(OneTimeInvoiceLineItem);
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
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="f2c50-129">Ehhez hasonló példát a következő témakörben talál:</span><span class="sxs-lookup"><span data-stu-id="f2c50-129">For a similar example, see:</span></span>

- <span data-ttu-id="f2c50-130">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f2c50-130">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="f2c50-131">Projekt: **partner Center SDK-minták**</span><span class="sxs-lookup"><span data-stu-id="f2c50-131">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="f2c50-132">Osztály: **GetUnBilledReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="f2c50-132">Class: **GetUnBilledReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="f2c50-133">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="f2c50-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f2c50-134">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f2c50-134">Request syntax</span></span>

<span data-ttu-id="f2c50-135">A REST-kérelemhez a használati esettől függően a következő szintaxist használhatja.</span><span class="sxs-lookup"><span data-stu-id="f2c50-135">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="f2c50-136">További információkért tekintse meg az egyes szintaxisok leírását.</span><span class="sxs-lookup"><span data-stu-id="f2c50-136">For more information, see the descriptions for each syntax.</span></span>

 | <span data-ttu-id="f2c50-137">Metódus</span><span class="sxs-lookup"><span data-stu-id="f2c50-137">Method</span></span>  | <span data-ttu-id="f2c50-138">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f2c50-138">Request URI</span></span>            | <span data-ttu-id="f2c50-139">Szintaxis használati esetének leírása</span><span class="sxs-lookup"><span data-stu-id="f2c50-139">Description of syntax use case</span></span>                                                                                |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f2c50-140">**GET**</span><span class="sxs-lookup"><span data-stu-id="f2c50-140">**GET**</span></span> | <span data-ttu-id="f2c50-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? Provider = egykori&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &időszak = {period} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f2c50-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                              | <span data-ttu-id="f2c50-142">Ezzel a szintaxissal teljes listát adhat vissza az adott számlához tartozó összes sor tételről.</span><span class="sxs-lookup"><span data-stu-id="f2c50-142">Use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="f2c50-143">**GET**</span><span class="sxs-lookup"><span data-stu-id="f2c50-143">**GET**</span></span> | <span data-ttu-id="f2c50-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? Provider = egykori&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &időszak = {period} &mérete = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f2c50-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>  | <span data-ttu-id="f2c50-145">Nagyméretű számlák esetén használja ezt a szintaxist egy megadott mérettel és 0 alapú eltolással a sorok lapozható listájának visszaadásához.</span><span class="sxs-lookup"><span data-stu-id="f2c50-145">For large invoices, use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="f2c50-146">**GET**</span><span class="sxs-lookup"><span data-stu-id="f2c50-146">**GET**</span></span> | <span data-ttu-id="f2c50-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? Provider = egykori&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &időszak = {period} &mérete = {size} &SeekOperation = tovább</span><span class="sxs-lookup"><span data-stu-id="f2c50-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span>                               | <span data-ttu-id="f2c50-148">Ezzel a szintaxissal beolvashatja az egyeztetési sorok következő oldalát a használatával `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="f2c50-148">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="f2c50-149">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="f2c50-149">URI parameters</span></span>

<span data-ttu-id="f2c50-150">A kérelem létrehozásakor használja az alábbi URI-és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="f2c50-150">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="f2c50-151">Név</span><span class="sxs-lookup"><span data-stu-id="f2c50-151">Name</span></span>                   | <span data-ttu-id="f2c50-152">Típus</span><span class="sxs-lookup"><span data-stu-id="f2c50-152">Type</span></span>   | <span data-ttu-id="f2c50-153">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f2c50-153">Required</span></span> | <span data-ttu-id="f2c50-154">Leírás</span><span class="sxs-lookup"><span data-stu-id="f2c50-154">Description</span></span>                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| <span data-ttu-id="f2c50-155">számlázási azonosító</span><span class="sxs-lookup"><span data-stu-id="f2c50-155">invoice-id</span></span>             | <span data-ttu-id="f2c50-156">sztring</span><span class="sxs-lookup"><span data-stu-id="f2c50-156">string</span></span> | <span data-ttu-id="f2c50-157">Igen</span><span class="sxs-lookup"><span data-stu-id="f2c50-157">Yes</span></span>      | <span data-ttu-id="f2c50-158">A számlát azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="f2c50-158">A string that identifies the invoice.</span></span> <span data-ttu-id="f2c50-159">A nem számlázott becslések lekéréséhez használja a "nem számlázott" lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="f2c50-159">Use 'unbilled' to get unbilled estimates.</span></span> |
| <span data-ttu-id="f2c50-160">Szolgáltató</span><span class="sxs-lookup"><span data-stu-id="f2c50-160">provider</span></span>               | <span data-ttu-id="f2c50-161">sztring</span><span class="sxs-lookup"><span data-stu-id="f2c50-161">string</span></span> | <span data-ttu-id="f2c50-162">Igen</span><span class="sxs-lookup"><span data-stu-id="f2c50-162">Yes</span></span>      | <span data-ttu-id="f2c50-163">A szolgáltató: "egykori".</span><span class="sxs-lookup"><span data-stu-id="f2c50-163">The provider: "OneTime".</span></span>                                                |
| <span data-ttu-id="f2c50-164">számla-sor-tétel típusa</span><span class="sxs-lookup"><span data-stu-id="f2c50-164">invoice-line-item-type</span></span> | <span data-ttu-id="f2c50-165">sztring</span><span class="sxs-lookup"><span data-stu-id="f2c50-165">string</span></span> | <span data-ttu-id="f2c50-166">Igen</span><span class="sxs-lookup"><span data-stu-id="f2c50-166">Yes</span></span>      | <span data-ttu-id="f2c50-167">A számla részleteinek típusa: "BillingLineItems".</span><span class="sxs-lookup"><span data-stu-id="f2c50-167">The type of invoice detail: "BillingLineItems".</span></span>               |
| <span data-ttu-id="f2c50-168">hasPartnerEarnedCredit</span><span class="sxs-lookup"><span data-stu-id="f2c50-168">hasPartnerEarnedCredit</span></span> | <span data-ttu-id="f2c50-169">logikai</span><span class="sxs-lookup"><span data-stu-id="f2c50-169">bool</span></span>   | <span data-ttu-id="f2c50-170">Nem</span><span class="sxs-lookup"><span data-stu-id="f2c50-170">No</span></span>       | <span data-ttu-id="f2c50-171">Az az érték, amely azt jelzi, hogy a rendszer visszaküldi-e a sorban lévő, partner által létrehozott jóváírást</span><span class="sxs-lookup"><span data-stu-id="f2c50-171">The value indicating if to return the line items with partner earned credit applied.</span></span> <span data-ttu-id="f2c50-172">Megjegyzés: ezt a paramétert csak akkor alkalmazza a rendszer, ha a szolgáltató típusa az egykori, a InvoiceLineItemType pedig UsageLineItems.</span><span class="sxs-lookup"><span data-stu-id="f2c50-172">Note: this parameter will be only applied when provider type is OneTime and InvoiceLineItemType is UsageLineItems.</span></span>
| <span data-ttu-id="f2c50-173">currencyCode</span><span class="sxs-lookup"><span data-stu-id="f2c50-173">currencyCode</span></span>           | <span data-ttu-id="f2c50-174">sztring</span><span class="sxs-lookup"><span data-stu-id="f2c50-174">string</span></span> | <span data-ttu-id="f2c50-175">Igen</span><span class="sxs-lookup"><span data-stu-id="f2c50-175">Yes</span></span>      | <span data-ttu-id="f2c50-176">A nem számlázott sorok pénznemkódja.</span><span class="sxs-lookup"><span data-stu-id="f2c50-176">The currency code for the unbilled line items.</span></span>                                  |
| <span data-ttu-id="f2c50-177">period</span><span class="sxs-lookup"><span data-stu-id="f2c50-177">period</span></span>                 | <span data-ttu-id="f2c50-178">sztring</span><span class="sxs-lookup"><span data-stu-id="f2c50-178">string</span></span> | <span data-ttu-id="f2c50-179">Igen</span><span class="sxs-lookup"><span data-stu-id="f2c50-179">Yes</span></span>      | <span data-ttu-id="f2c50-180">A nem számlázott felderítés időtartama.</span><span class="sxs-lookup"><span data-stu-id="f2c50-180">The period for unbilled recon.</span></span> <span data-ttu-id="f2c50-181">Példa: current, Previous.</span><span class="sxs-lookup"><span data-stu-id="f2c50-181">example: current, previous.</span></span>                      |
| <span data-ttu-id="f2c50-182">size</span><span class="sxs-lookup"><span data-stu-id="f2c50-182">size</span></span>                   | <span data-ttu-id="f2c50-183">szám</span><span class="sxs-lookup"><span data-stu-id="f2c50-183">number</span></span> | <span data-ttu-id="f2c50-184">Nem</span><span class="sxs-lookup"><span data-stu-id="f2c50-184">No</span></span>       | <span data-ttu-id="f2c50-185">A visszaadni kívánt elemek maximális száma.</span><span class="sxs-lookup"><span data-stu-id="f2c50-185">The maximum number of items to return.</span></span> <span data-ttu-id="f2c50-186">Az alapértelmezett méret 2000</span><span class="sxs-lookup"><span data-stu-id="f2c50-186">Default size is 2000</span></span>                     |
| <span data-ttu-id="f2c50-187">seekOperation</span><span class="sxs-lookup"><span data-stu-id="f2c50-187">seekOperation</span></span>          | <span data-ttu-id="f2c50-188">sztring</span><span class="sxs-lookup"><span data-stu-id="f2c50-188">string</span></span> | <span data-ttu-id="f2c50-189">No</span><span class="sxs-lookup"><span data-stu-id="f2c50-189">No</span></span>       | <span data-ttu-id="f2c50-190">Állítsa be a seekOperation = Next (Beolvasás) elemet a felderítési sorok következő oldalának beolvasásához.</span><span class="sxs-lookup"><span data-stu-id="f2c50-190">Set seekOperation=Next to get the next page of recon line items.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="f2c50-191">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f2c50-191">Request headers</span></span>

<span data-ttu-id="f2c50-192">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f2c50-192">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f2c50-193">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f2c50-193">Request body</span></span>

<span data-ttu-id="f2c50-194">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="f2c50-194">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="f2c50-195">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f2c50-195">REST response</span></span>

<span data-ttu-id="f2c50-196">Ha a művelet sikeres, a válasz tartalmazza a sor elem részleteinek gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="f2c50-196">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="f2c50-197">*A sor **ChargeType** az érték **megvásárlása** **újra** van leképezve, és az érték- **visszatérítés** a **megszakításra** van leképezve.*</span><span class="sxs-lookup"><span data-stu-id="f2c50-197">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f2c50-198">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f2c50-198">Response success and error codes</span></span>

<span data-ttu-id="f2c50-199">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="f2c50-199">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f2c50-200">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="f2c50-200">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f2c50-201">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="f2c50-201">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="request-response-examples"></a><span data-ttu-id="f2c50-202">Kérelem – válasz példák</span><span class="sxs-lookup"><span data-stu-id="f2c50-202">Request-response examples</span></span>

#### <a name="request-response-example-1"></a><span data-ttu-id="f2c50-203">Kérelem – válasz 1. példa</span><span class="sxs-lookup"><span data-stu-id="f2c50-203">Request-response example 1</span></span>

<span data-ttu-id="f2c50-204">A következő részletek a példára vonatkoznak:</span><span class="sxs-lookup"><span data-stu-id="f2c50-204">The following details apply to this example:</span></span>

- <span data-ttu-id="f2c50-205">Szolgáltató: **egykori**</span><span class="sxs-lookup"><span data-stu-id="f2c50-205">Provider: **OneTime**</span></span>
- <span data-ttu-id="f2c50-206">InvoiceLineItemType: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="f2c50-206">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="f2c50-207">Időszak: **előző**</span><span class="sxs-lookup"><span data-stu-id="f2c50-207">Period: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="f2c50-208">1. példa kérés</span><span class="sxs-lookup"><span data-stu-id="f2c50-208">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="f2c50-209">1. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="f2c50-209">Response example 1</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "HJVtMZMkgQ2miuCiNv0RSr51zQDans0m1",
            "orderDate": "2019-02-04T17:59:52.9460102Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0002",
            "availabilityId": "DZH318Z0BP8B",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Medium Plan",
            "chargeType": "New",
            "unitPrice": 820,
            "effectiveUnitPrice": 820,
            "unitType": "",
            "quantity": 1,
            "subtotal": 820,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-9cf0-4a1f-9514-7fcc7fe9d1fe",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 3.1618,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "883d475b-0000-1234-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": "883d475b-0000-2222-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
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

### <a name="request-response-example-2"></a><span data-ttu-id="f2c50-210">Kérelem – válasz 2. példa</span><span class="sxs-lookup"><span data-stu-id="f2c50-210">Request-response example 2</span></span>

<span data-ttu-id="f2c50-211">A következő részletek a példára vonatkoznak:</span><span class="sxs-lookup"><span data-stu-id="f2c50-211">The following details apply to this example:</span></span>

- <span data-ttu-id="f2c50-212">Szolgáltató: **egykori**</span><span class="sxs-lookup"><span data-stu-id="f2c50-212">Provider: **OneTime**</span></span>
- <span data-ttu-id="f2c50-213">InvoiceLineItemType: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="f2c50-213">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="f2c50-214">Időszak: **előző**</span><span class="sxs-lookup"><span data-stu-id="f2c50-214">Period: **Previous**</span></span>
- <span data-ttu-id="f2c50-215">SeekOperation: **következő**</span><span class="sxs-lookup"><span data-stu-id="f2c50-215">SeekOperation: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="f2c50-216">2. példa a kérelemre</span><span class="sxs-lookup"><span data-stu-id="f2c50-216">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=billinglineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="f2c50-217">2. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="f2c50-217">Response example 2</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": ""
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

#### <a name="request-example-3"></a><span data-ttu-id="f2c50-218">3. példa a kérelemre</span><span class="sxs-lookup"><span data-stu-id="f2c50-218">Request example 3</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=OneTime&invoiceLineItemType=UsageLineItems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-3"></a><span data-ttu-id="f2c50-219">3. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="f2c50-219">Response example 3</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "PartnerName": "testPartner",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "invoiceNumber": "T11ETHHDDD",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "publisherId": "21223810",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "subscriptionDescription": "sub description",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "UsageDate": "2019-02-07T09:22:34.6455294-08:00",
            "MeterType": "type",
            "MeterCategory": "category",
            "MeterId": "21312312312-fdsfsd",
            "MeterSubCategory": "subcategory",
            "MeterName": "meter name",
            "MeterRegion": "meter region",
            "UnitOfMeasure": "11",
            "skuName": "Test WaaS - Large Plan",
            "publisherName": "Test Networks, Inc.",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "discountDetails": "",
            "providerSource": "All",
            "RateOfPartnerEarnedCredit": 0.15,
            "IsPartnerEarnedCreditApplied": true,
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
