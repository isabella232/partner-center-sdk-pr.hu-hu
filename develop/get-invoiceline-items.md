---
title: Számla sorelemeinek lekérése
description: A partner Center API-k használatával lekérheti a számla sor (lezárt számlázási sor) részleteit a megadott számláról.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 50dac1bbc96776d395014dc7ee5a5990f0710484
ms.sourcegitcommit: a8ebfa97db9e43c6b5ff05bb37ecead6b3565721
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/13/2021
ms.locfileid: "100335812"
---
# <a name="get-invoice-line-items"></a><span data-ttu-id="14a25-103">Számla sorelemeinek lekérése</span><span class="sxs-lookup"><span data-stu-id="14a25-103">Get invoice line items</span></span>

<span data-ttu-id="14a25-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="14a25-104">**Applies to:**</span></span>

- <span data-ttu-id="14a25-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="14a25-105">Partner Center</span></span>
- <span data-ttu-id="14a25-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="14a25-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="14a25-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="14a25-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="14a25-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="14a25-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="14a25-109">A következő módszerekkel beolvashatja a számla sorok tételeinek (más néven lezárt számlázási sorok) gyűjteményének részleteit egy adott számlához.</span><span class="sxs-lookup"><span data-stu-id="14a25-109">You can use the following methods to get a collection details for of invoice line items (also known as closed billing line items) for a specified invoice.</span></span>

<span data-ttu-id="14a25-110">*A hibajavítások kivételével ez az API már nem frissül.*</span><span class="sxs-lookup"><span data-stu-id="14a25-110">*Except for bug fixes, this API is no longer being updated.*</span></span> <span data-ttu-id="14a25-111">Frissítse alkalmazásait, hogy a **piactér** helyett az **egykori** API-t hívja meg.</span><span class="sxs-lookup"><span data-stu-id="14a25-111">You should update your applications to call the **onetime** API instead of **marketplace**.</span></span> <span data-ttu-id="14a25-112">Az **egykori** API további funkciókat biztosít, és továbbra is frissülni fog.</span><span class="sxs-lookup"><span data-stu-id="14a25-112">The **onetime** API provides additional functionality, and will continue to be updated.</span></span>

<span data-ttu-id="14a25-113">Az **egyszeri** verziót kell használnia a **piactér** helyett az összes kereskedelmi fogyasztási sor elem lekérdezéséhez.</span><span class="sxs-lookup"><span data-stu-id="14a25-113">You should use **onetime** to query all commercial consumption line items instead of **marketplace**.</span></span> <span data-ttu-id="14a25-114">A hivatkozásokat a becsült hivatkozások hívásban is követheti.</span><span class="sxs-lookup"><span data-stu-id="14a25-114">Or, you can follow the links in the estimate links call.</span></span>

<span data-ttu-id="14a25-115">Ez az API az **Azure** és az **Office** Microsoft Azure (MS-AZR-0145P) előfizetések és az Office-ajánlatok **szolgáltatói** típusait is támogatja, így az API szolgáltatás visszafelé kompatibilis lesz.</span><span class="sxs-lookup"><span data-stu-id="14a25-115">This API also supports the **provider** types of **azure** and **office** for Microsoft Azure (MS-AZR-0145P) subscriptions and Office offers, which makes the API feature backward compatible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14a25-116">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="14a25-116">Prerequisites</span></span>

- <span data-ttu-id="14a25-117">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="14a25-117">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="14a25-118">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="14a25-118">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="14a25-119">Egy fiókazonosító.</span><span class="sxs-lookup"><span data-stu-id="14a25-119">An invoice identifier.</span></span> <span data-ttu-id="14a25-120">Ez azonosítja azt a számlát, amelynek a sorát be kell olvasni.</span><span class="sxs-lookup"><span data-stu-id="14a25-120">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="14a25-121">C\#</span><span class="sxs-lookup"><span data-stu-id="14a25-121">C\#</span></span>

<span data-ttu-id="14a25-122">A megadott számla vonali elemeinek beolvasása:</span><span class="sxs-lookup"><span data-stu-id="14a25-122">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="14a25-123">Hívja meg a [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) metódust, hogy lekérje a megadott számla műveleteinek számlázására szolgáló felületet.</span><span class="sxs-lookup"><span data-stu-id="14a25-123">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="14a25-124">Hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódust a számla objektum lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="14a25-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="14a25-125">A számla objektum a megadott számla összes adatát tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="14a25-125">The invoice object contains all of the information for the specified invoice.</span></span>
3. <span data-ttu-id="14a25-126">A számla objektum [**InvoiceDetails**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoice.invoicedetails) tulajdonságával hozzáférhet a [**InvoiceDetail**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail) objektumok egy gyűjteményéhez, amelyek mindegyike egy [**BillingProvider**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.billingprovider) és egy [**InvoiceLineItemType**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.invoicelineitemtype)tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="14a25-126">Use the invoice object's [**InvoiceDetails**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoice.invoicedetails) property to get access to a collection of [**InvoiceDetail**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail) objects, each of which contains a [**BillingProvider**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.billingprovider) and an [**InvoiceLineItemType**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.invoicelineitemtype).</span></span> <span data-ttu-id="14a25-127">A **BillingProvider** azonosítja a számla részletes adatainak forrását (például az **Office**, az **Azure**, az **egykori**), a **InvoiceLineItemType** pedig a típust (például **BillingLineItem**).</span><span class="sxs-lookup"><span data-stu-id="14a25-127">The **BillingProvider** identifies the source of the invoice detail information (such as **Office**, **Azure**, **OneTime**), and the **InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).</span></span>

<span data-ttu-id="14a25-128">Az alábbi mintakód egy **foreach** hurkot használ a **InvoiceDetails** -gyűjtemény feldolgozásához.</span><span class="sxs-lookup"><span data-stu-id="14a25-128">The following example code uses a **foreach** loop to process the **InvoiceDetails** collection.</span></span> <span data-ttu-id="14a25-129">A rendszer minden egyes **InvoiceDetail** -példányhoz beolvassa a sorok egy külön gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="14a25-129">A separate collection of line items is retrieved for each **InvoiceDetail** instance.</span></span>

<span data-ttu-id="14a25-130">Egy **InvoiceDetail** -példánynak megfelelő sorok gyűjteményének beolvasása:</span><span class="sxs-lookup"><span data-stu-id="14a25-130">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="14a25-131">Adja át a példány **BillingProvider** és **InvoiceLineItemType** a [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) metódusnak.</span><span class="sxs-lookup"><span data-stu-id="14a25-131">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="14a25-132">A társított sorok beolvasásához hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="14a25-132">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="14a25-133">Hozzon létre egy enumerálást a gyűjtemény átjárásához az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="14a25-133">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;
// string invoiceId;

// Retrieve the invoice.
var invoiceOperations = partnerOperations.Invoices.ById(invoiceId);
var invoice = invoiceOperations.Get();

foreach (var invoiceDetail in invoice.InvoiceDetails)
{
    Console.WriteLine(string.Format("Getting invoice line item for product {0} and line item type {1}",
        invoiceDetail.BillingProvider,
        invoiceDetail.InvoiceLineItemType));

    // Is this an unpaged or paged request?
    bool isUnPaged = (this.invoicePageSize <= 0);

    // If the scenario is unpaged, get all the invoice line items, otherwise get the first page.
    var invoiceLineItemsCollection =
        (isUnPaged)
        ? invoiceOperations.By(invoiceDetail.BillingProvider, invoiceDetail.InvoiceLineItemType).Get()
        : invoiceOperations.By(invoiceDetail.BillingProvider, invoiceDetail.InvoiceLineItemType).Get(this.invoicePageSize, 0);

    // Create an enumerator for traversing the line items collection.
    var invoiceLineItemEnumerator =
        partnerOperations.Enumerators.InvoiceLineItems.Create(invoiceLineItemsCollection);

    while (invoiceLineItemEnumerator.HasValue)
    {
        // invoiceLineItemEnumerator.Current contains a collection
        // of line items.
        Console.WriteLine(String.Format("invoiceLineItemEnumerator.Current has {0} line items.",
            invoiceLineItemEnumerator.Current.TotalCount));
        //
        // Insert code here to work with the line items.
        //
        Console.WriteLine();
        Console.Write("Press any key to retrieve the next invoice line items page");
        Console.ReadKey();

        // Get the next list of invoice line items.
        invoiceLineItemEnumerator.Next();
    }
}
```

<span data-ttu-id="14a25-134">Ehhez hasonló példát a következő témakörben talál:</span><span class="sxs-lookup"><span data-stu-id="14a25-134">For a similar example, see the following:</span></span>

- <span data-ttu-id="14a25-135">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="14a25-135">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="14a25-136">Projekt: **partner Center SDK-minták**</span><span class="sxs-lookup"><span data-stu-id="14a25-136">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="14a25-137">Osztály: **GetInvoiceLineItems.cs**</span><span class="sxs-lookup"><span data-stu-id="14a25-137">Class: **GetInvoiceLineItems.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="14a25-138">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="14a25-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="14a25-139">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="14a25-139">Request syntax</span></span>

<span data-ttu-id="14a25-140">A kérést a számlázási szolgáltató megfelelő szintaxisával teheti meg a forgatókönyvben.</span><span class="sxs-lookup"><span data-stu-id="14a25-140">Make your request using the appropriate syntax for the billing provider in your scenario.</span></span>

#### <a name="office"></a><span data-ttu-id="14a25-141">Office</span><span class="sxs-lookup"><span data-stu-id="14a25-141">Office</span></span>

<span data-ttu-id="14a25-142">A következő szintaxis akkor érvényes, ha a számlázási szolgáltató **iroda**.</span><span class="sxs-lookup"><span data-stu-id="14a25-142">The following syntax applies when the billing provider is **Office**.</span></span>

| <span data-ttu-id="14a25-143">Metódus</span><span class="sxs-lookup"><span data-stu-id="14a25-143">Method</span></span>  | <span data-ttu-id="14a25-144">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="14a25-144">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="14a25-145">**GET**</span><span class="sxs-lookup"><span data-stu-id="14a25-145">**GET**</span></span> | <span data-ttu-id="14a25-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? szolgáltató = Office&invoicelineitemtype = billinglineitems&méret = {size} &eltolás = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="14a25-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=office&invoicelineitemtype=billinglineitems&size={size}&offset={offset} HTTP/1.1</span></span>                               |

#### <a name="microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="14a25-147">Microsoft Azure (MS-AZR-0145P) előfizetés</span><span class="sxs-lookup"><span data-stu-id="14a25-147">Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="14a25-148">A következő szintaxisok érvényesek, ha a számlázási szolgáltató Microsoft Azure (MS-AZR-0145P) előfizetéssel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="14a25-148">The following syntaxes apply when the billing provider has a Microsoft Azure (MS-AZR-0145P) subscription.</span></span>

| <span data-ttu-id="14a25-149">Metódus</span><span class="sxs-lookup"><span data-stu-id="14a25-149">Method</span></span>  | <span data-ttu-id="14a25-150">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="14a25-150">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="14a25-151">**GET**</span><span class="sxs-lookup"><span data-stu-id="14a25-151">**GET**</span></span> | <span data-ttu-id="14a25-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? Provider = Azure&invoicelineitemtype = billinglineitems&méret = {size} &eltolás = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="14a25-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=azure&invoicelineitemtype=billinglineitems&size={size}&offset={offset} HTTP/1.1</span></span>  |
| <span data-ttu-id="14a25-153">**GET**</span><span class="sxs-lookup"><span data-stu-id="14a25-153">**GET**</span></span> | <span data-ttu-id="14a25-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? Provider = Azure&invoicelineitemtype = usagelineitems&méret = {size} &eltolás = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="14a25-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=azure&invoicelineitemtype=usagelineitems&size={size}&offset={offset} HTTP/1.1</span></span>  |

##### <a name="onetime"></a><span data-ttu-id="14a25-155">Elvégezni</span><span class="sxs-lookup"><span data-stu-id="14a25-155">OneTime</span></span>

<span data-ttu-id="14a25-156">A következő szintaxisok akkor érvényesek, ha a számlázási szolgáltató az **egykori**.</span><span class="sxs-lookup"><span data-stu-id="14a25-156">The following syntaxes apply when the billing provider is **OneTime**.</span></span> <span data-ttu-id="14a25-157">Ez magában foglalja az Azure-foglalások, a szoftverek, az Azure-csomagok és a kereskedelmi piactér-termékek díját.</span><span class="sxs-lookup"><span data-stu-id="14a25-157">This includes charges for Azure reservations, software, Azure plans, and commercial marketplace products.</span></span>

| <span data-ttu-id="14a25-158">Metódus</span><span class="sxs-lookup"><span data-stu-id="14a25-158">Method</span></span>  | <span data-ttu-id="14a25-159">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="14a25-159">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="14a25-160">**GET**</span><span class="sxs-lookup"><span data-stu-id="14a25-160">**GET**</span></span> | <span data-ttu-id="14a25-161">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? Provider = egykori&invoicelineitemtype = billinglineitems&méret = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="14a25-161">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="14a25-162">**GET**</span><span class="sxs-lookup"><span data-stu-id="14a25-162">**GET**</span></span> | <span data-ttu-id="14a25-163">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems/onetime/billinglineitems&mérete = {size}? SeekOperation = tovább</span><span class="sxs-lookup"><span data-stu-id="14a25-163">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/onetime/billinglineitems&size={size}?seekOperation=Next</span></span>                           |

#### <a name="previous-syntaxes"></a><span data-ttu-id="14a25-164">Korábbi szintaxisok</span><span class="sxs-lookup"><span data-stu-id="14a25-164">Previous syntaxes</span></span>

<span data-ttu-id="14a25-165">Ha a következő szintaxist használja, ügyeljen arra, hogy a megfelelő szintaxist használja a használati esethez.</span><span class="sxs-lookup"><span data-stu-id="14a25-165">If you are using the following syntaxes, be sure to use the appropriate syntax for your use case.</span></span>

<span data-ttu-id="14a25-166">*A hibajavítások kivételével ez az API már nem frissül.*</span><span class="sxs-lookup"><span data-stu-id="14a25-166">*Except for bug fixes, this API is no longer being updated.*</span></span> <span data-ttu-id="14a25-167">Frissítse alkalmazásait, hogy a **piactér** helyett az **egykori** API-t hívja meg.</span><span class="sxs-lookup"><span data-stu-id="14a25-167">You should update your applications to call the **onetime** API instead of **marketplace**.</span></span> <span data-ttu-id="14a25-168">Az **egykori** API további funkciókat biztosít, és továbbra is frissülni fog.</span><span class="sxs-lookup"><span data-stu-id="14a25-168">The **onetime** API provides additional functionality, and will continue to be updated.</span></span>

<span data-ttu-id="14a25-169">Az **egyszeri** verziót kell használnia a **piactér** helyett az összes kereskedelmi fogyasztási sor elem lekérdezéséhez.</span><span class="sxs-lookup"><span data-stu-id="14a25-169">You should use **onetime** to query all commercial consumption line items instead of **marketplace**.</span></span> <span data-ttu-id="14a25-170">A hivatkozásokat a becsült hivatkozások hívásban is követheti.</span><span class="sxs-lookup"><span data-stu-id="14a25-170">Or, you can follow the links in the estimate links call.</span></span>

| <span data-ttu-id="14a25-171">Metódus</span><span class="sxs-lookup"><span data-stu-id="14a25-171">Method</span></span> | <span data-ttu-id="14a25-172">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="14a25-172">Request URI</span></span> | <span data-ttu-id="14a25-173">Szintaxis használati esetének leírása</span><span class="sxs-lookup"><span data-stu-id="14a25-173">Description of syntax use case</span></span> |
| ------ | ----------- | -------------------------------- |
| <span data-ttu-id="14a25-174">GET</span><span class="sxs-lookup"><span data-stu-id="14a25-174">GET</span></span> | <span data-ttu-id="14a25-175">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems/{Billing-Provider}/{Invoice-line-Item-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="14a25-175">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/{billing-provider}/{invoice-line-item-type} HTTP/1.1</span></span>                              | <span data-ttu-id="14a25-176">Ezzel a szintaxissal teljes listát adhat vissza az adott számlához tartozó összes sor tételről.</span><span class="sxs-lookup"><span data-stu-id="14a25-176">You can use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="14a25-177">GET</span><span class="sxs-lookup"><span data-stu-id="14a25-177">GET</span></span> | <span data-ttu-id="14a25-178">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems/{Billing-Provider}/{Invoice-line-Item-Type}? méret = {size} &eltolás = {ELTOLÁS} http/1.1</span><span class="sxs-lookup"><span data-stu-id="14a25-178">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/{billing-provider}/{invoice-line-item-type}?size={size}&offset={offset} HTTP/1.1</span></span>  | <span data-ttu-id="14a25-179">Nagyméretű számlák esetén ezt a szintaxist egy megadott mérettel és 0 alapú eltolással használhatja a sorok lapozható listájának visszaadásához.</span><span class="sxs-lookup"><span data-stu-id="14a25-179">For large invoices, you can use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="14a25-180">GET</span><span class="sxs-lookup"><span data-stu-id="14a25-180">GET</span></span> | <span data-ttu-id="14a25-181">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems/OneTime/{Invoice-line-Item-Type}? SeekOperation = Next</span><span class="sxs-lookup"><span data-stu-id="14a25-181">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/OneTime/{invoice-line-item-type}?seekOperation=Next</span></span>                               | <span data-ttu-id="14a25-182">Ezt a szintaxist használhatja egy olyan számla számlázására, amely egy **egyszeri** számlázási szolgáltatói értékkel rendelkezik, és a **következőre** állítja be a **seekOperation** , hogy beolvassa a számla sorok következő oldalát.</span><span class="sxs-lookup"><span data-stu-id="14a25-182">You can use this syntax for an invoice with a billing-provider value of **OneTime** and set **seekOperation** to **Next** to get the next page of invoice line items.</span></span> |

##### <a name="uri-parameters"></a><span data-ttu-id="14a25-183">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="14a25-183">URI parameters</span></span>

<span data-ttu-id="14a25-184">A kérelem létrehozásakor használja az alábbi URI-és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="14a25-184">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="14a25-185">Név</span><span class="sxs-lookup"><span data-stu-id="14a25-185">Name</span></span>                   | <span data-ttu-id="14a25-186">Típus</span><span class="sxs-lookup"><span data-stu-id="14a25-186">Type</span></span>   | <span data-ttu-id="14a25-187">Kötelező</span><span class="sxs-lookup"><span data-stu-id="14a25-187">Required</span></span> | <span data-ttu-id="14a25-188">Leírás</span><span class="sxs-lookup"><span data-stu-id="14a25-188">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="14a25-189">számlázási azonosító</span><span class="sxs-lookup"><span data-stu-id="14a25-189">invoice-id</span></span>             | <span data-ttu-id="14a25-190">sztring</span><span class="sxs-lookup"><span data-stu-id="14a25-190">string</span></span> | <span data-ttu-id="14a25-191">Yes</span><span class="sxs-lookup"><span data-stu-id="14a25-191">Yes</span></span>      | <span data-ttu-id="14a25-192">A számlát azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="14a25-192">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="14a25-193">számlázási szolgáltató</span><span class="sxs-lookup"><span data-stu-id="14a25-193">billing-provider</span></span>       | <span data-ttu-id="14a25-194">sztring</span><span class="sxs-lookup"><span data-stu-id="14a25-194">string</span></span> | <span data-ttu-id="14a25-195">Yes</span><span class="sxs-lookup"><span data-stu-id="14a25-195">Yes</span></span>      | <span data-ttu-id="14a25-196">A számlázási szolgáltató: "Office", "Azure", "egykori".</span><span class="sxs-lookup"><span data-stu-id="14a25-196">The billing provider: "Office", "Azure", "OneTime".</span></span> <span data-ttu-id="14a25-197">A korábbi verziókban külön adatmodellek vannak az Office & Azure-tranzakciók számára.</span><span class="sxs-lookup"><span data-stu-id="14a25-197">In the legacy, we have separate data models for Office & Azure transactions.</span></span> <span data-ttu-id="14a25-198">A Modernben azonban egyetlen adatmodellünk van minden termékben, amely az "egykori" értékkel van szűrve.</span><span class="sxs-lookup"><span data-stu-id="14a25-198">However, in the modern, we have one single data model across all products filtered through the "OneTime" value.</span></span>            |
| <span data-ttu-id="14a25-199">számla-sor-tétel típusa</span><span class="sxs-lookup"><span data-stu-id="14a25-199">invoice-line-item-type</span></span> | <span data-ttu-id="14a25-200">sztring</span><span class="sxs-lookup"><span data-stu-id="14a25-200">string</span></span> | <span data-ttu-id="14a25-201">Yes</span><span class="sxs-lookup"><span data-stu-id="14a25-201">Yes</span></span>      | <span data-ttu-id="14a25-202">A számla részleteinek típusa: "BillingLineItems", "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="14a25-202">The type of invoice detail: "BillingLineItems", "UsageLineItems".</span></span> |
| <span data-ttu-id="14a25-203">size</span><span class="sxs-lookup"><span data-stu-id="14a25-203">size</span></span>                   | <span data-ttu-id="14a25-204">szám</span><span class="sxs-lookup"><span data-stu-id="14a25-204">number</span></span> | <span data-ttu-id="14a25-205">No</span><span class="sxs-lookup"><span data-stu-id="14a25-205">No</span></span>       | <span data-ttu-id="14a25-206">A visszaadni kívánt elemek maximális száma.</span><span class="sxs-lookup"><span data-stu-id="14a25-206">The maximum number of items to return.</span></span> <span data-ttu-id="14a25-207">Alapértelmezett maximális méret = 2000</span><span class="sxs-lookup"><span data-stu-id="14a25-207">Default max size = 2000</span></span>    |
| <span data-ttu-id="14a25-208">offset</span><span class="sxs-lookup"><span data-stu-id="14a25-208">offset</span></span>                 | <span data-ttu-id="14a25-209">szám</span><span class="sxs-lookup"><span data-stu-id="14a25-209">number</span></span> | <span data-ttu-id="14a25-210">No</span><span class="sxs-lookup"><span data-stu-id="14a25-210">No</span></span>       | <span data-ttu-id="14a25-211">A visszaadni kívánt első sor nulla alapú indexe.</span><span class="sxs-lookup"><span data-stu-id="14a25-211">The zero-based index of the first line item to return.</span></span>            |
| <span data-ttu-id="14a25-212">seekOperation</span><span class="sxs-lookup"><span data-stu-id="14a25-212">seekOperation</span></span>          | <span data-ttu-id="14a25-213">sztring</span><span class="sxs-lookup"><span data-stu-id="14a25-213">string</span></span> | <span data-ttu-id="14a25-214">No</span><span class="sxs-lookup"><span data-stu-id="14a25-214">No</span></span>       | <span data-ttu-id="14a25-215">Ha a **számlázási szolgáltató** az **egykorinál** egyenlő, állítsa a **SeekOperation** egyenlő értékre a **következővel** , hogy beolvassa a számla sorok következő oldalát.</span><span class="sxs-lookup"><span data-stu-id="14a25-215">If **billing-provider** equals **OneTime**, set **seekOperation** equal to **Next** to get the next page of invoice line items.</span></span> |
| <span data-ttu-id="14a25-216">hasPartnerEarnedCredit</span><span class="sxs-lookup"><span data-stu-id="14a25-216">hasPartnerEarnedCredit</span></span> | <span data-ttu-id="14a25-217">logikai</span><span class="sxs-lookup"><span data-stu-id="14a25-217">bool</span></span> | <span data-ttu-id="14a25-218">No</span><span class="sxs-lookup"><span data-stu-id="14a25-218">No</span></span> | <span data-ttu-id="14a25-219">Az az érték, amely azt jelzi, hogy a rendszer visszaküldi-e a sorban lévő, partner által létrehozott jóváírást</span><span class="sxs-lookup"><span data-stu-id="14a25-219">The value indicating if to return the line items with partner earned credit applied.</span></span> <span data-ttu-id="14a25-220">Megjegyzés: ezt a paramétert csak akkor alkalmazza a rendszer, ha a számlázási szolgáltató típusa az egykori, a InvoiceLineItemType pedig UsageLineItems.</span><span class="sxs-lookup"><span data-stu-id="14a25-220">Note: this parameter will be only applied when billing provider type is OneTime and InvoiceLineItemType is UsageLineItems.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="14a25-221">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="14a25-221">Request headers</span></span>

<span data-ttu-id="14a25-222">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="14a25-222">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="14a25-223">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="14a25-223">Request body</span></span>

<span data-ttu-id="14a25-224">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="14a25-224">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="14a25-225">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="14a25-225">REST response</span></span>

<span data-ttu-id="14a25-226">Ha a művelet sikeres, a válasz tartalmazza a sor elem részleteinek gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="14a25-226">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="14a25-227">*A sor **ChargeType** a **megvásárolt** érték az **új** elemre van leképezve. Az érték- **visszatérítés** a **megszakításra** van leképezve.*</span><span class="sxs-lookup"><span data-stu-id="14a25-227">*For the line item **ChargeType**, the value **Purchase** is mapped to **New**. The value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="14a25-228">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="14a25-228">Response success and error codes</span></span>

<span data-ttu-id="14a25-229">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="14a25-229">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="14a25-230">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="14a25-230">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="14a25-231">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="14a25-231">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="rest-request-response-examples"></a><span data-ttu-id="14a25-232">REST-kérelem – válasz példák</span><span class="sxs-lookup"><span data-stu-id="14a25-232">REST request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="14a25-233">Kérelem – válasz 1. példa</span><span class="sxs-lookup"><span data-stu-id="14a25-233">Request-response example 1</span></span>

<span data-ttu-id="14a25-234">Ebben a példában a részletek a következők:</span><span class="sxs-lookup"><span data-stu-id="14a25-234">In this example, the details are as follows:</span></span>

- <span data-ttu-id="14a25-235">**BillingProvider**: **iroda**</span><span class="sxs-lookup"><span data-stu-id="14a25-235">**BillingProvider**: **Office**</span></span>
- <span data-ttu-id="14a25-236">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="14a25-236">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="14a25-237">1. példa kérés</span><span class="sxs-lookup"><span data-stu-id="14a25-237">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="14a25-238">1. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="14a25-238">Response example 1</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "74221236-D09C-4870-AC1D-33E155E9AEBE",
            "customerName": "TSTAGIN1CUST190",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "orderId": "567735045559164136",
            "subscriptionId": "4KIKawEAAAAAAAEA",
            "syndicationPartnerSubscriptionNumber": "1F58ACD7-FE51-4705-9567-D009C9ADA150",
            "offerId": "AAA5B3F0-0EE2-431B-A42F-3F18F3C6D540",
            "durableOfferId": "2F707C7C-2433-49A5-A437-9CA7CF40D3EB",
            "offerName": "EXCHANGE ONLINE (PLAN 2)",
            "domainName": "TStagin1Cust190.onmicrosoft.com",
            "billingCycleType": "MONTHLY",
            "subscriptionName": "EXCHANGE ONLINE (PLAN 2)",
            "subscriptionDescription": "EXCHANGE ONLINE (PLAN 2)",
            "subscriptionStartDate": "2017-05-12T00:00:00",
            "subscriptionEndDate": "2018-06-10T00:00:00",
            "chargeStartDate": "2017-05-12T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "chargeType": "New",
            "unitPrice": 0.0,
            "quantity": 3,
            "amount": 0.0,
            "totalOtherDiscount": 0.0,
            "subtotal": 0.0,
            "tax": 0.0,
            "totalForCustomer": 0.0,
            "currency": "USD",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "office",
            "attributes": {
                "objectType": "LicenseBasedLineItem"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "74221236-D09C-4870-AC1D-33E155E9AEBE",
            "customerName": "TSTAGIN1CUST190",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "orderId": "567735045564795186",
            "subscriptionId": "Ik4YawEAAAAAAAEA",
            "syndicationPartnerSubscriptionNumber": "D8A8F773-9D3E-4244-8797-3182075F09FA",
            "offerId": "618B53FE-9B99-428B-9745-F706AEAF3979",
            "durableOfferId": "69C67983-CF78-4102-83F6-3E5FD246864F",
            "offerName": "SHAREPOINT ONLINE (PLAN 2)",
            "domainName": "TStagin1Cust190.onmicrosoft.com",
            "billingCycleType": "MONTHLY",
            "subscriptionName": "SHAREPOINT ONLINE (PLAN 2)",
            "subscriptionDescription": "SHAREPOINT ONLINE (PLAN 2)",
            "subscriptionStartDate": "2017-05-13T00:00:00",
            "subscriptionEndDate": "2018-06-10T00:00:00",
            "chargeStartDate": "2017-05-13T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "chargeType": "New",
            "unitPrice": 0.0,
            "quantity": 1,
            "amount": 0.0,
            "totalOtherDiscount": 0.0,
            "subtotal": 0.0,
            "tax": 0.0,
            "totalForCustomer": 0.0,
            "currency": "USD",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "office",
            "attributes": {
                "objectType": "LicenseBasedLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a><span data-ttu-id="14a25-239">Kérelem – válasz 2. példa</span><span class="sxs-lookup"><span data-stu-id="14a25-239">Request-response example 2</span></span>

<span data-ttu-id="14a25-240">A következő példában a részletek a következők:</span><span class="sxs-lookup"><span data-stu-id="14a25-240">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="14a25-241">**BillingProvider**: **Azure**</span><span class="sxs-lookup"><span data-stu-id="14a25-241">**BillingProvider**: **Azure**</span></span>
- <span data-ttu-id="14a25-242">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="14a25-242">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="14a25-243">2. példa a kérelemre</span><span class="sxs-lookup"><span data-stu-id="14a25-243">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="14a25-244">2. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="14a25-244">Response example 2</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [
        {
            "detailLineItemId": 1,
            "sku": "7UD-00001",
            "includedQuantity": 0,
            "overageQuantity": 745,
            "listPrice": 0.085,
            "currency": "USD",
            "pretaxCharges": 63.33,
            "taxAmount": 6.34,
            "postTaxTotal": 69.67,
            "pretaxEffectiveRate": 0.08500671,
            "postTaxEffectiveRate": 0.09351677,
            "chargeType": "Assess usage fee for current cycle",
            "invoiceLineItemType": "billing_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_Big foot consulting",
            "partnerBillableAccountId": "1010578050",
            "customerId": "65726577-c208-40fd-9735-8c85ac000000",
            "domainName": "600test.onmicrosoft.com",
            "customerCompanyName": "601 tests",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "87f4b92f-a490-485e-ad34-5b70cb000000",
            "subscriptionName": "Microsoft Azure",
            "subscriptionDescription": "Microsoft Azure",
            "billingCycleType": "Monthly",
            "orderId": "568297985427000000",
            "serviceName": "Azure App Service",
            "serviceType": "Standard Plan",
            "resourceGuid": "505db374-df8a-44df-9d8c-13c14b61dee1",
            "resourceName": "S1",
            "region": "",
            "consumedQuantity": 745,
            "chargeStartDate": "2019-08-02T00:00:00",
            "chargeEndDate": "2019-09-01T00:00:00",
            "unit": "1 Hour",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "UsageBasedLineItem"
            }
        },
        {
            "detailLineItemId": 1,
            "sku": "7UD-00001",
            "includedQuantity": 0,
            "overageQuantity": 0.000882,
            "listPrice": 0.0383,
            "currency": "USD",
            "pretaxCharges": 0,
            "taxAmount": 0,
            "postTaxTotal": 0,
            "pretaxEffectiveRate": 0,
            "postTaxEffectiveRate": 0,
            "chargeType": "Assess usage fee for current cycle",
            "invoiceLineItemType": "billing_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E87E26A",
            "partnerName": "TEST_TEST_Big foot consulting",
            "partnerBillableAccountId": "1010578050",
            "customerId": "65726577-c208-40fd-9735-8c85ac9cac68",
            "domainName": "600test.onmicrosoft.com",
            "customerCompanyName": "601 tests",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "87f4b92f-a490-485e-ad34-5b70cb000000",
            "subscriptionName": "Microsoft Azure",
            "subscriptionDescription": "Microsoft Azure",
            "billingCycleType": "Monthly",
            "orderId": "568297985427000000",
            "serviceName": "Storage",
            "serviceType": "Standard Page Blob",
            "resourceGuid": "d23a5753-ff85-4ddf-af28-8cc5cf2d3882",
            "resourceName": "LRS Data Stored",
            "region": "",
            "consumedQuantity": 0.000882,
            "chargeStartDate": "2019-08-02T00:00:00",
            "chargeEndDate": "2019-09-01T00:00:00",
            "unit": "1 GB/Month",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "UsageBasedLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-3"></a><span data-ttu-id="14a25-245">Kérelem – válasz 3. példa</span><span class="sxs-lookup"><span data-stu-id="14a25-245">Request-response example 3</span></span>

<span data-ttu-id="14a25-246">A következő példában a részletek a következők:</span><span class="sxs-lookup"><span data-stu-id="14a25-246">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="14a25-247">**BillingProvider**: **Azure**</span><span class="sxs-lookup"><span data-stu-id="14a25-247">**BillingProvider**: **Azure**</span></span>
- <span data-ttu-id="14a25-248">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="14a25-248">**InvoiceLineItemType**: **UsageLineItems**</span></span>

#### <a name="request-example-3"></a><span data-ttu-id="14a25-249">3. példa a kérelemre</span><span class="sxs-lookup"><span data-stu-id="14a25-249">Request example 3</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-3"></a><span data-ttu-id="14a25-250">3. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="14a25-250">Response example 3</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [
        {
            "customerBillableAccount": "1439508127",
            "usageDate": "2019-08-05T00:00:00",
            "invoiceLineItemType": "usage_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_BIG FOOT CONSULTING",
            "partnerBillableAccountId": "1010578050",
            "customerId": "9E9B71BA-3442-458B-B519-E1CCF72FBB54",
            "domainName": "test600.onmicrosoft.com",
            "customerCompanyName": "600 TEST",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "F9BA6DA0-6DAC-4F88-B623-313C9B9C117A",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "568297985577171353",
            "serviceName": "STORAGE",
            "serviceType": "STANDARD PAGE BLOB",
            "resourceGuid": "9CC63CF8-6593-410A-B0E7-26A4EF71E8B3",
            "resourceName": "DISK DELETE OPERATIONS",
            "region": "",
            "consumedQuantity": 2.9616,
            "chargeStartDate": "2019-08-05T00:00:00",
            "chargeEndDate": "2019-09-04T00:00:00",
            "unit": "10K",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "DailyUsageLineItem"
            }
        },
        {
            "customerBillableAccount": "1307536861",
            "usageDate": "2019-08-10T00:00:00",
            "invoiceLineItemType": "usage_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_BIG FOOT CONSULTING",
            "partnerBillableAccountId": "1010578050",
            "customerId": "EB53B7BD-267E-440E-B3C0-8F0B40000000",
            "domainName": "brandontest.onmicrosoft.com",
            "customerCompanyName": "BRANDON'S TEST",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "62D22561-AB15-41E5-AD59-99025C000000",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "568297985605838583",
            "serviceName": "VIRTUAL MACHINES",
            "serviceType": "D/DS SERIES WINDOWS",
            "resourceGuid": "62C64B6C-4033-4E20-AB33-9E81271AC12A",
            "resourceName": "D1/DS1",
            "region": "US WEST",
            "consumedQuantity": 24,
            "chargeStartDate": "2019-08-05T00:00:00",
            "chargeEndDate": "2019-09-04T00:00:00",
            "unit": "1 HOUR",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "DailyUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-4"></a><span data-ttu-id="14a25-251">Kérelem – válasz 4. példa</span><span class="sxs-lookup"><span data-stu-id="14a25-251">Request-response example 4</span></span>

<span data-ttu-id="14a25-252">A következő példában a részletek a következők:</span><span class="sxs-lookup"><span data-stu-id="14a25-252">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="14a25-253">**BillingProvider**: **egykori**</span><span class="sxs-lookup"><span data-stu-id="14a25-253">**BillingProvider**: **OneTime**</span></span>
- <span data-ttu-id="14a25-254">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="14a25-254">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-4"></a><span data-ttu-id="14a25-255">4. példa kérése</span><span class="sxs-lookup"><span data-stu-id="14a25-255">Request example 4</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/G000024135/lineitems/OneTime/BillingLineItems?size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-4"></a><span data-ttu-id="14a25-256">4. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="14a25-256">Response example 4</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

 {
    "continuationToken": "d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7",
    "totalCount": 2,
    "items": [
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f000000",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38000000",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "QDOx5ZN3YR9uYhm4M1MGQJ_0nievUOrx1",
            "orderDate": "2018-02-08T22:31:42.9397946Z",
            "productId": "productid",
            "skuId": "skuid",
            "availabilityId": "availabilityid",
            "productName": "TEST PRODUCT",
            "skuName": "TEST SKU TITLE",
            "chargeType": "New",
            "unitPrice": 431.8,
            "effectiveUnitPrice": 496.07,
            "unitType": "Seats",
            "quantity": 1,
            "subtotal": 431.8,
            "taxTotal": 38.87,
            "totalForCustomer": 470.67,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232000000",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234278124b8",
            "priceAdjustmentDescription": "[\"100.0% Tier 1 Discount\"]",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0159369774,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "billingFrequency": "Monthly",
            "reservationOrderId": "883d475b-0000-2222-0000-8818752f1234",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f4badc2",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38cbb28e",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "QDOx5ZN3YR9uYhm4M1MGQJ_0nievUOrx1",
            "orderDate": "2018-02-08T22:31:42.9397946Z",
            "productId": "productid",
            "skuId": "skuid",
            "availabilityId": "availabilityid",
            "productName": "TEST PRODUCT",
            "skuName": "TEST SKU TITLE",
            "chargeType": "New",
            "unitPrice": 26.35,
            "effectiveUnitPrice": 496.07,
            "unitType": "1 Hour",
            "quantity": 1,
            "subtotal": 26.35,
            "taxTotal": 2.37,
            "totalForCustomer": 28.72,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232ea904a",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234578124b8",
            "priceAdjustmentDescription": "[\"100.0% Tier 1 Discount\"]",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0130687981,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2?seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7"
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-5"></a><span data-ttu-id="14a25-257">Kérelem – válasz 5. példa</span><span class="sxs-lookup"><span data-stu-id="14a25-257">Request-response example 5</span></span>

<span data-ttu-id="14a25-258">A következő példában egy folytatási tokent használó lapozás található.</span><span class="sxs-lookup"><span data-stu-id="14a25-258">In the following example, there is paging using a continuation token.</span></span> <span data-ttu-id="14a25-259">A részletek a következők:</span><span class="sxs-lookup"><span data-stu-id="14a25-259">The details are as follows:</span></span>

- <span data-ttu-id="14a25-260">**BillingProvider**: **egykori**</span><span class="sxs-lookup"><span data-stu-id="14a25-260">**BillingProvider**: **OneTime**</span></span>
- <span data-ttu-id="14a25-261">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="14a25-261">**InvoiceLineItemType**: **BillingLineItems**</span></span>
- <span data-ttu-id="14a25-262">**SeekOperation**: **következő**</span><span class="sxs-lookup"><span data-stu-id="14a25-262">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-5"></a><span data-ttu-id="14a25-263">5. példa kérés</span><span class="sxs-lookup"><span data-stu-id="14a25-263">Request example 5</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/G000024135/lineitems/OneTime/BillingLineItems?seekOperation=Next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-5"></a><span data-ttu-id="14a25-264">5. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="14a25-264">Response example 5</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 1,
    "items": [
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f000000",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38000000",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "NeqT31Kziwf8gkCXM9YQToWTqU-9Jbm81",
            "orderDate": "2018-02-08T22:31:47.1751688Z",
            "productId": "DZH318Z0BQ3P",
            "skuId": "001F",
            "availabilityId": "DZH318Z0DR0H",
            "productName": "Reserved VM Instance, Standard_D1, AP East, 3 years",
            "skuName": "D Series",
            "chargeType": "New",
            "unitPrice": 1447,
            "effectiveUnitPrice": 496.07,
            "unitType": "Seats",
            "quantity": 1,
            "subtotal": 1447,
            "taxTotal": 130.24,
            "totalForCustomer": 1577.24,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232000000",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234568124b8",
            "priceAdjustmentDescription": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0130687981,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "",
            "billingFrequency": "Monthly",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
