---
title: Próbaverziós előfizetés átalakítása fizetőssé
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat a próba-előfizetés fizetős előfizetésre való átalakításához.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1876cfc796b683bfff00b7d137bcfe0b7162c78
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973859"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a><span data-ttu-id="d219f-103">Próba-előfizetés konvertálása fizetősre Partnerközpont API-k használatával</span><span class="sxs-lookup"><span data-stu-id="d219f-103">Convert a trial subscription to paid using Partner Center APIs</span></span>

<span data-ttu-id="d219f-104">A próba-előfizetéseket fizetősre konvertálhatja.</span><span class="sxs-lookup"><span data-stu-id="d219f-104">You can convert a trial subscription to paid.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d219f-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d219f-105">Prerequisites</span></span>

- <span data-ttu-id="d219f-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d219f-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d219f-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="d219f-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d219f-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d219f-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d219f-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d219f-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d219f-110">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d219f-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d219f-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d219f-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d219f-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="d219f-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d219f-113">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d219f-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d219f-114">Egy aktív próba-előfizetés előfizetés-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="d219f-114">A subscription ID for an active trial subscription.</span></span>

- <span data-ttu-id="d219f-115">Egy elérhető konverziós ajánlat.</span><span class="sxs-lookup"><span data-stu-id="d219f-115">An available conversion offer.</span></span>

## <a name="convert-a-trial-subscription-to-a-paid-subscription-through-code"></a><span data-ttu-id="d219f-116">Próbaverziós előfizetés konvertálása fizetős előfizetésre kóddal</span><span class="sxs-lookup"><span data-stu-id="d219f-116">Convert a trial subscription to a paid subscription through code</span></span>

<span data-ttu-id="d219f-117">A próba-előfizetés fizetősre való konvertálásához először be kell szereznie az elérhető próbaverziós konverziók gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="d219f-117">To convert a trial subscription to a paid one, you must first obtain a collection of the trial conversions available.</span></span> <span data-ttu-id="d219f-118">Ezután ki kell választania a megvásárolni kívánt átváltási ajánlatot.</span><span class="sxs-lookup"><span data-stu-id="d219f-118">Then, you must choose the conversion offer that you want to purchase.</span></span>

<span data-ttu-id="d219f-119">Az átváltási ajánlatok olyan mennyiséget határoznak meg, amely alapértelmezés szerint a próbaverziós előfizetéssel azonos számú licencre van beállítva.</span><span class="sxs-lookup"><span data-stu-id="d219f-119">The conversion offers will specify a quantity that defaults to the same number of licenses as the trial subscription.</span></span> <span data-ttu-id="d219f-120">Ezt a mennyiséget módosíthatja, ha a [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) tulajdonságot a megvásárolni kívánt licencek számára módosítja.</span><span class="sxs-lookup"><span data-stu-id="d219f-120">You can change this quantity by setting the [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) property to the number of licenses that you want to purchase.</span></span>

> [!NOTE]
> <span data-ttu-id="d219f-121">A megvásárolt licencek számától függetlenül a próbaidőszak előfizetés-azonosítója a megvásárolt licencekhez lesz újra felhasználva.</span><span class="sxs-lookup"><span data-stu-id="d219f-121">Regardless of the number of licenses purchased, the subscription ID of the trial is reused for the purchased licenses.</span></span> <span data-ttu-id="d219f-122">Ennek eredményeképpen a próbaverzió eltűnik, és a vásárlás váltja fel.</span><span class="sxs-lookup"><span data-stu-id="d219f-122">As a result, the trial in effect disappears and is replaced by the purchase.</span></span>

<span data-ttu-id="d219f-123">Próbaverziós előfizetés kódon keresztüli konvertálásához kövesse az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="d219f-123">Use the following steps to convert a trial subscription through code:</span></span>

1. <span data-ttu-id="d219f-124">Szerezze be az elérhető előfizetési műveletek felületét.</span><span class="sxs-lookup"><span data-stu-id="d219f-124">Get an interface to the subscription operations available.</span></span> <span data-ttu-id="d219f-125">Azonosítania kell az ügyfelet, és meg kell adnia a próba-előfizetés előfizetés-azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="d219f-125">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. <span data-ttu-id="d219f-126">Szerezze be az elérhető konverziós ajánlatok gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="d219f-126">Get a collection of the available conversion offers.</span></span> <span data-ttu-id="d219f-127">A metódus kérésével/válaszával kapcsolatos további információkért lásd: Próbaverziós konverziós [ajánlatok listájának lekérése.](get-a-list-of-trial-conversion-offers.md)</span><span class="sxs-lookup"><span data-stu-id="d219f-127">For more information and details on the request/response for this method, see [Get a list of trial conversion offers](get-a-list-of-trial-conversion-offers.md).</span></span>

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. <span data-ttu-id="d219f-128">Válasszon egy konverziós ajánlatot.</span><span class="sxs-lookup"><span data-stu-id="d219f-128">Choose a conversion offer.</span></span> <span data-ttu-id="d219f-129">A következő kód a gyűjtemény első konverziós ajánlatát választja ki.</span><span class="sxs-lookup"><span data-stu-id="d219f-129">The following code chooses the first conversion offer in the collection.</span></span>

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. <span data-ttu-id="d219f-130">Megadhatja a megvásárolni kívánt licencek számát is.</span><span class="sxs-lookup"><span data-stu-id="d219f-130">Optionally, specify the number of licenses to purchase.</span></span> <span data-ttu-id="d219f-131">Az alapértelmezett érték a próbaverziós előfizetésben elérhető licencek száma.</span><span class="sxs-lookup"><span data-stu-id="d219f-131">The default is the number of licenses in the trial subscription.</span></span>

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. <span data-ttu-id="d219f-132">A [**próba-előfizetés**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) fizetősre konvertálásához hívja meg a Create vagy [**a CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="d219f-132">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to convert the trial subscription to paid.</span></span>

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a><span data-ttu-id="d219f-133">C\#</span><span class="sxs-lookup"><span data-stu-id="d219f-133">C\#</span></span>

<span data-ttu-id="d219f-134">Próbaverziós előfizetés fizetősre konvertálása:</span><span class="sxs-lookup"><span data-stu-id="d219f-134">To convert a trial subscription to a paid one:</span></span>

1. <span data-ttu-id="d219f-135">Az ügyfél azonosításához használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="d219f-135">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="d219f-136">Az előfizetési műveletek interfészének lehívásához hívja meg a [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust a próba-előfizetés azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="d219f-136">Get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="d219f-137">Mentse az előfizetési műveleti felület hivatkozását egy helyi változóban.</span><span class="sxs-lookup"><span data-stu-id="d219f-137">Save a reference to the subscription operations interface in a local variable.</span></span>

3. <span data-ttu-id="d219f-138">A [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) tulajdonság használatával szerezzen be egy felületet az elérhető konverziós műveletekhez, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) metódust az elérhető konverziós ajánlatok [**gyűjteményének lekéréséhez.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion)</span><span class="sxs-lookup"><span data-stu-id="d219f-138">Use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span> <span data-ttu-id="d219f-139">Ki kell választania egyet.</span><span class="sxs-lookup"><span data-stu-id="d219f-139">You must choose one.</span></span> <span data-ttu-id="d219f-140">Az alábbi példa alapértelmezés szerint az első elérhető konverziót használja.</span><span class="sxs-lookup"><span data-stu-id="d219f-140">The following example defaults to the first conversion available.</span></span>

4. <span data-ttu-id="d219f-141">A helyi változóba mentett előfizetési műveleti felületre és a [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) tulajdonságra való hivatkozással szerezzen be egy interfészt az átalakításkor elérhető műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="d219f-141">Use the reference to the subscription operations interface that you saved in a local variable and the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions.</span></span>

5. <span data-ttu-id="d219f-142">A próbakonverzió megkísérlése érdekében adja át a kiválasztott konverziós ajánlat objektumát a [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) vagy [**a CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) metódusnak.</span><span class="sxs-lookup"><span data-stu-id="d219f-142">Pass the selected conversion offer object to the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to attempt the trial conversion.</span></span>

### <a name="c-example"></a><span data-ttu-id="d219f-143">C \# példa</span><span class="sxs-lookup"><span data-stu-id="d219f-143">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get subscription operations for the trial subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the available conversions.
var conversions = subscriptionOperations.Conversions.Get();

// If there are no conversions available, we&#39;re done.
// Otherwise, convert the trial to the first available conversion offer.
if (conversions.TotalCount <= 0)
{
    System.Console.WriteLine("This subscription has no conversions");
}
else
{
    // Default to the first conversion.
    var selectedConversion = conversions.Items.ToList()[0];

    // Convert the trial and return the result.
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
}
```

## <a name="rest-request"></a><span data-ttu-id="d219f-144">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d219f-144">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d219f-145">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d219f-145">Request syntax</span></span>

| <span data-ttu-id="d219f-146">Metódus</span><span class="sxs-lookup"><span data-stu-id="d219f-146">Method</span></span>   | <span data-ttu-id="d219f-147">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d219f-147">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d219f-148">**Post**</span><span class="sxs-lookup"><span data-stu-id="d219f-148">**POST**</span></span> | <span data-ttu-id="d219f-149">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/konverziós HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d219f-149">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d219f-150">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d219f-150">URI parameter</span></span>

<span data-ttu-id="d219f-151">Az alábbi elérésiút-paraméterekkel azonosíthatja az ügyfelet és a próbaverziós előfizetést.</span><span class="sxs-lookup"><span data-stu-id="d219f-151">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="d219f-152">Név</span><span class="sxs-lookup"><span data-stu-id="d219f-152">Name</span></span>            | <span data-ttu-id="d219f-153">Típus</span><span class="sxs-lookup"><span data-stu-id="d219f-153">Type</span></span>   | <span data-ttu-id="d219f-154">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d219f-154">Required</span></span> | <span data-ttu-id="d219f-155">Leírás</span><span class="sxs-lookup"><span data-stu-id="d219f-155">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="d219f-156">ügyfélazonosító</span><span class="sxs-lookup"><span data-stu-id="d219f-156">customer-id</span></span>     | <span data-ttu-id="d219f-157">sztring</span><span class="sxs-lookup"><span data-stu-id="d219f-157">string</span></span> | <span data-ttu-id="d219f-158">Igen</span><span class="sxs-lookup"><span data-stu-id="d219f-158">Yes</span></span>      | <span data-ttu-id="d219f-159">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="d219f-159">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="d219f-160">subscription-id</span><span class="sxs-lookup"><span data-stu-id="d219f-160">subscription-id</span></span> | <span data-ttu-id="d219f-161">sztring</span><span class="sxs-lookup"><span data-stu-id="d219f-161">string</span></span> | <span data-ttu-id="d219f-162">Igen</span><span class="sxs-lookup"><span data-stu-id="d219f-162">Yes</span></span>      | <span data-ttu-id="d219f-163">A próba-előfizetést azonosító GUID formátumú sztring.</span><span class="sxs-lookup"><span data-stu-id="d219f-163">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d219f-164">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d219f-164">Request headers</span></span>

<span data-ttu-id="d219f-165">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d219f-165">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d219f-166">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d219f-166">Request body</span></span>

<span data-ttu-id="d219f-167">A kérelem [törzsében](conversions-resources.md#conversion) szerepelnie kell egy feltöltéses konverziós erőforrásnak.</span><span class="sxs-lookup"><span data-stu-id="d219f-167">A populated [Conversion](conversions-resources.md#conversion) resource must be included in the request body.</span></span>

### <a name="request-example"></a><span data-ttu-id="d219f-168">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d219f-168">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 234
Expect: 100-continue

{
    "OfferId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "TargetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "OrderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
    "Quantity": 25,
    "BillingCycle": "monthly",
    "Attributes": {
        "ObjectType": "Conversion"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="d219f-169">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d219f-169">REST response</span></span>

<span data-ttu-id="d219f-170">Ha a művelet sikeres, a válasz törzse tartalmaz egy [ConversionResult erőforrást.](conversions-resources.md#conversionresult)</span><span class="sxs-lookup"><span data-stu-id="d219f-170">If successful, the response body contains a [ConversionResult](conversions-resources.md#conversionresult) resource.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="d219f-171">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d219f-171">Response success and error codes</span></span>

<span data-ttu-id="d219f-172">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d219f-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d219f-173">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d219f-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d219f-174">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d219f-174">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="d219f-175">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d219f-175">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 211
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CV: kW4GzmhvHEqCq1ls.0
MS-ServerId: 030020643
Date: Thu, 15 Jun 2017 23:10:40 GMT

 {
    "subscriptionId": "488745B5-2086-4912-802C-6ABB9F7C3638",
    "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "attributes": {
        "objectType": "ConversionResult"
    }
}
```
