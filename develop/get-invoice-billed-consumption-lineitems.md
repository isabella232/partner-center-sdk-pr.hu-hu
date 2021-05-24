---
title: Számlázott kereskedelmi használatú sorelemek lekért száma
description: Az adott számlához tartozó kereskedelmi használatú számlasorelem (lezárt napi minősített használati tétel) gyűjteményét a következő API Partnerközpont le.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1406938b16e5a363a73c36ef0338eb5fc4305279
ms.sourcegitcommit: 89aefbff6dbe740b6f27a888492ffc2e5f98b1e9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/24/2021
ms.locfileid: "110325445"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a><span data-ttu-id="7f3a2-103">Számlázott kereskedelmi használatú sorelemek lekért száma</span><span class="sxs-lookup"><span data-stu-id="7f3a2-103">Get invoice billed commercial consumption line items</span></span>

<span data-ttu-id="7f3a2-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-104">**Applies to:**</span></span>

- <span data-ttu-id="7f3a2-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="7f3a2-105">Partner Center</span></span>

<span data-ttu-id="7f3a2-106">Az alábbi módszerekkel lekért adatok egy adott számlához tartozó kereskedelmi használatú számlasorelemekre (más néven lezárt napi minősített használatisor-tételekre) vonatkozó részleteket.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-106">You can use the following methods to get a collection of details for commercial consumption invoice line items (also known as closed daily rated usage line items) for a specified invoice.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7f3a2-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="7f3a2-107">Prerequisites</span></span>

- <span data-ttu-id="7f3a2-108">A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7f3a2-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7f3a2-109">Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7f3a2-110">Egy számlaazonosító.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-110">An invoice identifier.</span></span> <span data-ttu-id="7f3a2-111">Ez azonosítja a számlát, amelynek lekéri a sorelemeket.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-111">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="7f3a2-112">C\#</span><span class="sxs-lookup"><span data-stu-id="7f3a2-112">C\#</span></span>

<span data-ttu-id="7f3a2-113">A megadott számla kereskedelmisor-elemeinek lekérése a számlaobjektumot kell lekérnie:</span><span class="sxs-lookup"><span data-stu-id="7f3a2-113">To get the commercial line items for the specified invoice, you must retrieve the invoice object:</span></span>

1. <span data-ttu-id="7f3a2-114">Hívja meg [**a ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) metódust a megadott számlához tartozó számlázási műveletek interfészének lehívása érdekében.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-114">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="7f3a2-115">A [**számlaobjektum lekérése**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódussal.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-115">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="7f3a2-116">A számlaobjektum a megadott számla összes adatát tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-116">The invoice object contains all of the information for the specified invoice.</span></span>

<span data-ttu-id="7f3a2-117">A **Szolgáltató** azonosítja a kiszámlázott részletes adatok forrását (például **egyszer).**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-117">The **Provider** identifies the source of the billed detail information (for example, **onetime**).</span></span> <span data-ttu-id="7f3a2-118">Az **InvoiceLineItemType** határozza meg a típust (például **UsageLineItem).**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-118">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="7f3a2-119">Az alábbi példakód egy **foreach ciklust használ** a sorelemek gyűjteményének feldolgozásához.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-119">The following example code uses a **foreach** loop to process the line items collection.</span></span> <span data-ttu-id="7f3a2-120">A rendszer minden **InvoiceLineItemType** típushoz külön sorelemek gyűjteményét olvassa be.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-120">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="7f3a2-121">Egy InvoiceDetail példánynak megfelelő sorelemek **gyűjteményének legyűjtéséhez:**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-121">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="7f3a2-122">Adja át a példány **BillingProvider** és **InvoiceLineItemType** tulajdonságát a [**By metódusnak.**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by)</span><span class="sxs-lookup"><span data-stu-id="7f3a2-122">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="7f3a2-123">A [**társított sorelemek lekérése**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódussal.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-123">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="7f3a2-124">Hozzon létre egy enumerátort, amely az alábbi példában látható módon lépked a gyűjteményen.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-124">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="7f3a2-125">Hasonló példát a következőben láthat:</span><span class="sxs-lookup"><span data-stu-id="7f3a2-125">For a similar example, see the following:</span></span>

- <span data-ttu-id="7f3a2-126">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="7f3a2-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="7f3a2-127">Projekt: **Partnerközpont SDK minták**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="7f3a2-128">Osztály: **GetBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-128">Class: **GetBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="7f3a2-129">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="7f3a2-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7f3a2-130">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="7f3a2-130">Request syntax</span></span>

<span data-ttu-id="7f3a2-131">Az első szintaxissal az adott számla összes sorelemének teljes listáját használhatja.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-131">Use the first syntax to return a full list of every line item for the given invoice.</span></span> <span data-ttu-id="7f3a2-132">Nagy számlák esetén használja a második szintaxist a megadott mérettel és a 0-alapú eltolással a sorelemek lapszámolt listájának visszaadására.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-132">For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> <span data-ttu-id="7f3a2-133">A harmadik szintaxissal lekérte a sorelemek következő oldalát a `seekOperation = "Next"` használatával.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-133">Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.</span></span>

| <span data-ttu-id="7f3a2-134">Metódus</span><span class="sxs-lookup"><span data-stu-id="7f3a2-134">Method</span></span>  | <span data-ttu-id="7f3a2-135">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="7f3a2-135">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7f3a2-136">**Kap**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-136">**GET**</span></span> | <span data-ttu-id="7f3a2-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7f3a2-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span></span>                              |
| <span data-ttu-id="7f3a2-138">**Kap**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-138">**GET**</span></span> | <span data-ttu-id="7f3a2-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7f3a2-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="7f3a2-140">**Kap**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-140">**GET**</span></span> | <span data-ttu-id="7f3a2-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="7f3a2-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span></span>                               |

#### <a name="uri-parameters"></a><span data-ttu-id="7f3a2-142">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="7f3a2-142">URI parameters</span></span>

<span data-ttu-id="7f3a2-143">A kérelem létrehozásakor használja a következő URI-t és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-143">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="7f3a2-144">Név</span><span class="sxs-lookup"><span data-stu-id="7f3a2-144">Name</span></span>                   | <span data-ttu-id="7f3a2-145">Típus</span><span class="sxs-lookup"><span data-stu-id="7f3a2-145">Type</span></span>   | <span data-ttu-id="7f3a2-146">Kötelező</span><span class="sxs-lookup"><span data-stu-id="7f3a2-146">Required</span></span> | <span data-ttu-id="7f3a2-147">Leírás</span><span class="sxs-lookup"><span data-stu-id="7f3a2-147">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="7f3a2-148">számlaazonosító</span><span class="sxs-lookup"><span data-stu-id="7f3a2-148">invoice-id</span></span>             | <span data-ttu-id="7f3a2-149">sztring</span><span class="sxs-lookup"><span data-stu-id="7f3a2-149">string</span></span> | <span data-ttu-id="7f3a2-150">Yes</span><span class="sxs-lookup"><span data-stu-id="7f3a2-150">Yes</span></span>      | <span data-ttu-id="7f3a2-151">A számlát azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-151">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="7f3a2-152">Szolgáltató</span><span class="sxs-lookup"><span data-stu-id="7f3a2-152">provider</span></span>               | <span data-ttu-id="7f3a2-153">sztring</span><span class="sxs-lookup"><span data-stu-id="7f3a2-153">string</span></span> | <span data-ttu-id="7f3a2-154">Yes</span><span class="sxs-lookup"><span data-stu-id="7f3a2-154">Yes</span></span>      | <span data-ttu-id="7f3a2-155">A szolgáltató: "OneTime".</span><span class="sxs-lookup"><span data-stu-id="7f3a2-155">The provider: "OneTime".</span></span>                                  |
| <span data-ttu-id="7f3a2-156">invoice-line-item-type</span><span class="sxs-lookup"><span data-stu-id="7f3a2-156">invoice-line-item-type</span></span> | <span data-ttu-id="7f3a2-157">sztring</span><span class="sxs-lookup"><span data-stu-id="7f3a2-157">string</span></span> | <span data-ttu-id="7f3a2-158">Yes</span><span class="sxs-lookup"><span data-stu-id="7f3a2-158">Yes</span></span>      | <span data-ttu-id="7f3a2-159">A számla részleteinek típusa: "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="7f3a2-159">The type of invoice detail: "UsageLineItems".</span></span> |
| <span data-ttu-id="7f3a2-160">currencyCode</span><span class="sxs-lookup"><span data-stu-id="7f3a2-160">currencyCode</span></span>           | <span data-ttu-id="7f3a2-161">sztring</span><span class="sxs-lookup"><span data-stu-id="7f3a2-161">string</span></span> | <span data-ttu-id="7f3a2-162">Yes</span><span class="sxs-lookup"><span data-stu-id="7f3a2-162">Yes</span></span>      | <span data-ttu-id="7f3a2-163">A számlázható sorelemek pénznemkódja.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-163">The currency code for the billed line items.</span></span>                    |
| <span data-ttu-id="7f3a2-164">period</span><span class="sxs-lookup"><span data-stu-id="7f3a2-164">period</span></span>                 | <span data-ttu-id="7f3a2-165">sztring</span><span class="sxs-lookup"><span data-stu-id="7f3a2-165">string</span></span> | <span data-ttu-id="7f3a2-166">Yes</span><span class="sxs-lookup"><span data-stu-id="7f3a2-166">Yes</span></span>      | <span data-ttu-id="7f3a2-167">A kiszámlázott felderítés időtartama.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-167">The period for billed recon.</span></span> <span data-ttu-id="7f3a2-168">példa: current, previous.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-168">example: current, previous.</span></span>        |
| <span data-ttu-id="7f3a2-169">size</span><span class="sxs-lookup"><span data-stu-id="7f3a2-169">size</span></span>                   | <span data-ttu-id="7f3a2-170">szám</span><span class="sxs-lookup"><span data-stu-id="7f3a2-170">number</span></span> | <span data-ttu-id="7f3a2-171">No</span><span class="sxs-lookup"><span data-stu-id="7f3a2-171">No</span></span>       | <span data-ttu-id="7f3a2-172">A visszaadott elemek maximális száma.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-172">The maximum number of items to return.</span></span> <span data-ttu-id="7f3a2-173">Az alapértelmezett méret 2000</span><span class="sxs-lookup"><span data-stu-id="7f3a2-173">Default size is 2000</span></span>       |
| <span data-ttu-id="7f3a2-174">seekOperation</span><span class="sxs-lookup"><span data-stu-id="7f3a2-174">seekOperation</span></span>          | <span data-ttu-id="7f3a2-175">sztring</span><span class="sxs-lookup"><span data-stu-id="7f3a2-175">string</span></span> | <span data-ttu-id="7f3a2-176">No</span><span class="sxs-lookup"><span data-stu-id="7f3a2-176">No</span></span>       | <span data-ttu-id="7f3a2-177">Állítsa be a seekOperation=Next elemet a felderítési sorelemek következő oldalának lekért értékhez.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-177">Set seekOperation=Next to get the next page of recon line items.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7f3a2-178">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="7f3a2-178">Request headers</span></span>

<span data-ttu-id="7f3a2-179">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7f3a2-179">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7f3a2-180">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="7f3a2-180">Request body</span></span>

<span data-ttu-id="7f3a2-181">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-181">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="7f3a2-182">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="7f3a2-182">REST response</span></span>

<span data-ttu-id="7f3a2-183">Ha ez sikeres, a válasz sorelem-részletek gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-183">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="7f3a2-184">A **ChargeType** sorelem esetében a **Purchase érték** az Új értékre van **leképezve.**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-184">For the line item **ChargeType**, the value **Purchase** is mapped to **New**.</span></span> <span data-ttu-id="7f3a2-185">A **Refund (Visszatérítés)** érték a Cancel (Lemondás) **értékre van leképezve.**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-185">The value **Refund** is mapped to **Cancel**.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7f3a2-186">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="7f3a2-186">Response success and error codes</span></span>

<span data-ttu-id="7f3a2-187">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7f3a2-188">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="7f3a2-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7f3a2-189">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7f3a2-189">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="rest-examples"></a><span data-ttu-id="7f3a2-190">REST-példák</span><span class="sxs-lookup"><span data-stu-id="7f3a2-190">REST examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="7f3a2-191">1. kérés-válasz példa</span><span class="sxs-lookup"><span data-stu-id="7f3a2-191">Request-response example 1</span></span>

<span data-ttu-id="7f3a2-192">A példa REST-kérés és -válasz részletei a következők:</span><span class="sxs-lookup"><span data-stu-id="7f3a2-192">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="7f3a2-193">**Szolgáltató:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-193">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="7f3a2-194">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-194">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="7f3a2-195">**Időszak:** **Előző**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-195">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="7f3a2-196">1. kérési példa</span><span class="sxs-lookup"><span data-stu-id="7f3a2-196">Request example 1</span></span>

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

#### <a name="response-example-1"></a><span data-ttu-id="7f3a2-197">1. válasz példa</span><span class="sxs-lookup"><span data-stu-id="7f3a2-197">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="7f3a2-198">2. kérés-válasz példa</span><span class="sxs-lookup"><span data-stu-id="7f3a2-198">Request-response example 2</span></span>

<span data-ttu-id="7f3a2-199">A példa REST-kérés és -válasz részletei a következők:</span><span class="sxs-lookup"><span data-stu-id="7f3a2-199">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="7f3a2-200">**Szolgáltató:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-200">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="7f3a2-201">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-201">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="7f3a2-202">**Időszak:** **Előző**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-202">**Period**: **Previous**</span></span>
- <span data-ttu-id="7f3a2-203">**SeekOperation:** **Tovább**</span><span class="sxs-lookup"><span data-stu-id="7f3a2-203">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="7f3a2-204">2. kérési példa</span><span class="sxs-lookup"><span data-stu-id="7f3a2-204">Request example 2</span></span>

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

## <a name="response-example-2"></a><span data-ttu-id="7f3a2-205">2. válasz példa</span><span class="sxs-lookup"><span data-stu-id="7f3a2-205">Response example 2</span></span>

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
