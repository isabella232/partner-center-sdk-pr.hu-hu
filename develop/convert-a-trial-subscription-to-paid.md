---
title: Próbaverziós előfizetés átalakítása fizetőssé
description: Ismerje meg, hogyan alakíthatja át a próbaverziós előfizetéseket a partner Center API-kkal a fizetős verzióra.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 59dcf6caf21d407b2fba4cc8438bc435fda9dc77
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768584"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a><span data-ttu-id="73c3b-103">Próbaverziós előfizetés átalakítása a partner Center API-k használatával</span><span class="sxs-lookup"><span data-stu-id="73c3b-103">Convert a trial subscription to paid using Partner Center APIs</span></span>

<span data-ttu-id="73c3b-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="73c3b-104">**Applies to:**</span></span>

- <span data-ttu-id="73c3b-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="73c3b-105">Partner Center</span></span>

<span data-ttu-id="73c3b-106">A próbaverziós előfizetés kifizetésre konvertálható.</span><span class="sxs-lookup"><span data-stu-id="73c3b-106">You can convert a trial subscription to paid.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73c3b-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="73c3b-107">Prerequisites</span></span>

- <span data-ttu-id="73c3b-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="73c3b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="73c3b-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="73c3b-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="73c3b-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="73c3b-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="73c3b-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="73c3b-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="73c3b-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="73c3b-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="73c3b-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="73c3b-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="73c3b-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="73c3b-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="73c3b-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="73c3b-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="73c3b-116">Egy aktív próbaverziós előfizetés előfizetési azonosítója.</span><span class="sxs-lookup"><span data-stu-id="73c3b-116">A subscription ID for an active trial subscription.</span></span>

- <span data-ttu-id="73c3b-117">Egy elérhető konverziós ajánlat.</span><span class="sxs-lookup"><span data-stu-id="73c3b-117">An available conversion offer.</span></span>

## <a name="convert-a-trial-subscription-to-paid-through-code"></a><span data-ttu-id="73c3b-118">Próbaverziós előfizetés átalakítása kóddal való fizetésre</span><span class="sxs-lookup"><span data-stu-id="73c3b-118">Convert a trial subscription to paid through code</span></span>

<span data-ttu-id="73c3b-119">A próbaverziós előfizetés fizetős verzióra való átalakításához először be kell szereznie az elérhető próbaverziók gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="73c3b-119">To convert a trial subscription to a paid one, you must first obtain a collection of the trial conversions available.</span></span> <span data-ttu-id="73c3b-120">Ezután ki kell választania a megvásárolni kívánt átalakítási ajánlatot.</span><span class="sxs-lookup"><span data-stu-id="73c3b-120">Then, you must choose the conversion offer that you want to purchase.</span></span>

<span data-ttu-id="73c3b-121">Az átalakítási ajánlatok olyan mennyiséget határoznak meg, amely alapértelmezés szerint ugyanannyi licenccel rendelkezik, mint a próbaverziós előfizetés.</span><span class="sxs-lookup"><span data-stu-id="73c3b-121">The conversion offers will specify a quantity that defaults to the same number of licenses as the trial subscription.</span></span> <span data-ttu-id="73c3b-122">Ezt a mennyiséget úgy módosíthatja, hogy a [**mennyiségi**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) tulajdonságot a megvásárolni kívánt licencek számára állítja be.</span><span class="sxs-lookup"><span data-stu-id="73c3b-122">You can change this quantity by setting the [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) property to the number of licenses that you want to purchase.</span></span>

> [!NOTE]
> <span data-ttu-id="73c3b-123">A megvásárolt licencek számától függetlenül a rendszer újra felhasználja a próbaverzió előfizetés-AZONOSÍTÓját a megvásárolt licencek esetében.</span><span class="sxs-lookup"><span data-stu-id="73c3b-123">Regardless of the number of licenses purchased, the subscription ID of the trial is reused for the purchased licenses.</span></span> <span data-ttu-id="73c3b-124">Ennek eredményeképpen a próbaverzió eltűnik, és a vásárlás helyébe lép.</span><span class="sxs-lookup"><span data-stu-id="73c3b-124">As a result, the trial in effect disappears and is replaced by the purchase.</span></span>

<span data-ttu-id="73c3b-125">A próbaverziós előfizetés kód használatával történő átalakításához kövesse az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="73c3b-125">Use the following steps to convert a trial subscription through code:</span></span>

1. <span data-ttu-id="73c3b-126">Szerezzen be egy felületet az elérhető előfizetési műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="73c3b-126">Get an interface to the subscription operations available.</span></span> <span data-ttu-id="73c3b-127">Azonosítania kell az ügyfelet, és meg kell adnia a próbaverziós előfizetés előfizetés-azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="73c3b-127">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. <span data-ttu-id="73c3b-128">Szerezze be az elérhető átalakítási ajánlatok gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="73c3b-128">Get a collection of the available conversion offers.</span></span> <span data-ttu-id="73c3b-129">További információt és a módszerre vonatkozó kérés/válasz részleteit itt tekintheti meg: a [próbaverziós konvertálási ajánlatok listájának beolvasása](get-a-list-of-trial-conversion-offers.md).</span><span class="sxs-lookup"><span data-stu-id="73c3b-129">For more information and details on the request/response for this method, see [Get a list of trial conversion offers](get-a-list-of-trial-conversion-offers.md).</span></span>

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. <span data-ttu-id="73c3b-130">Válasszon egy átalakítási ajánlatot.</span><span class="sxs-lookup"><span data-stu-id="73c3b-130">Choose a conversion offer.</span></span> <span data-ttu-id="73c3b-131">A következő kód kiválasztja a gyűjtemény első átalakítási ajánlatát.</span><span class="sxs-lookup"><span data-stu-id="73c3b-131">The following code chooses the first conversion offer in the collection.</span></span>

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. <span data-ttu-id="73c3b-132">Igény szerint megadhatja a megvásárolni kívánt licencek számát.</span><span class="sxs-lookup"><span data-stu-id="73c3b-132">Optionally, specify the number of licenses to purchase.</span></span> <span data-ttu-id="73c3b-133">Az alapértelmezett érték a próbaverziós előfizetésben található licencek száma.</span><span class="sxs-lookup"><span data-stu-id="73c3b-133">The default is the number of licenses in the trial subscription.</span></span>

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. <span data-ttu-id="73c3b-134">A [**create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) metódus meghívásával konvertálja a próbaverziós előfizetést fizetettre.</span><span class="sxs-lookup"><span data-stu-id="73c3b-134">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to convert the trial subscription to paid.</span></span>

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a><span data-ttu-id="73c3b-135">C\#</span><span class="sxs-lookup"><span data-stu-id="73c3b-135">C\#</span></span>

<span data-ttu-id="73c3b-136">Próbaverziós előfizetés átalakítása fizetős verzióra:</span><span class="sxs-lookup"><span data-stu-id="73c3b-136">To convert a trial subscription to a paid one:</span></span>

1. <span data-ttu-id="73c3b-137">Az ügyfél azonosításához használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="73c3b-137">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="73c3b-138">Az előfizetések [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódus meghívása a próbaverziós előfizetés-azonosítóval az előfizetési műveletek eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="73c3b-138">Get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="73c3b-139">Egy helyi változóban mentheti az előfizetés-üzemeltetési felületre mutató hivatkozást.</span><span class="sxs-lookup"><span data-stu-id="73c3b-139">Save a reference to the subscription operations interface in a local variable.</span></span>

3. <span data-ttu-id="73c3b-140">Az [**átalakítások**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) [**tulajdonsággal**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) szerezzen be egy felületet az elérhető műveletekhez a konverziók között, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) metódust a rendelkezésre álló konverziós ajánlatok gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="73c3b-140">Use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span> <span data-ttu-id="73c3b-141">Ki kell választania egyet.</span><span class="sxs-lookup"><span data-stu-id="73c3b-141">You must choose one.</span></span> <span data-ttu-id="73c3b-142">A következő példa a rendelkezésre álló első konverziót alapértelmezett értékre vált.</span><span class="sxs-lookup"><span data-stu-id="73c3b-142">The following example defaults to the first conversion available.</span></span>

4. <span data-ttu-id="73c3b-143">Használja az előfizetési műveletek felületét, amelyet egy helyi változóban és a [**konverziók**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) tulajdonságban mentett, hogy az elérhető műveletekhez csatolót szerezzen be a konverziók között.</span><span class="sxs-lookup"><span data-stu-id="73c3b-143">Use the reference to the subscription operations interface that you saved in a local variable and the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions.</span></span>

5. <span data-ttu-id="73c3b-144">A próbaverzió átalakításának megkísérlése érdekében adja át a kiválasztott átalakítási ajánlat objektumát a [**create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) metódusnak.</span><span class="sxs-lookup"><span data-stu-id="73c3b-144">Pass the selected conversion offer object to the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to attempt the trial conversion.</span></span>

### <a name="c-example"></a><span data-ttu-id="73c3b-145">C \# példa</span><span class="sxs-lookup"><span data-stu-id="73c3b-145">C\# example</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="73c3b-146">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="73c3b-146">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="73c3b-147">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="73c3b-147">Request syntax</span></span>

| <span data-ttu-id="73c3b-148">Metódus</span><span class="sxs-lookup"><span data-stu-id="73c3b-148">Method</span></span>   | <span data-ttu-id="73c3b-149">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="73c3b-149">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="73c3b-150">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="73c3b-150">**POST**</span></span> | <span data-ttu-id="73c3b-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/Conversions http/1.1</span><span class="sxs-lookup"><span data-stu-id="73c3b-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="73c3b-152">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="73c3b-152">URI parameter</span></span>

<span data-ttu-id="73c3b-153">Az ügyfél és a próbaverzió előfizetésének azonosításához használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="73c3b-153">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="73c3b-154">Név</span><span class="sxs-lookup"><span data-stu-id="73c3b-154">Name</span></span>            | <span data-ttu-id="73c3b-155">Típus</span><span class="sxs-lookup"><span data-stu-id="73c3b-155">Type</span></span>   | <span data-ttu-id="73c3b-156">Kötelező</span><span class="sxs-lookup"><span data-stu-id="73c3b-156">Required</span></span> | <span data-ttu-id="73c3b-157">Leírás</span><span class="sxs-lookup"><span data-stu-id="73c3b-157">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="73c3b-158">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="73c3b-158">customer-id</span></span>     | <span data-ttu-id="73c3b-159">sztring</span><span class="sxs-lookup"><span data-stu-id="73c3b-159">string</span></span> | <span data-ttu-id="73c3b-160">Igen</span><span class="sxs-lookup"><span data-stu-id="73c3b-160">Yes</span></span>      | <span data-ttu-id="73c3b-161">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="73c3b-161">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="73c3b-162">előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="73c3b-162">subscription-id</span></span> | <span data-ttu-id="73c3b-163">sztring</span><span class="sxs-lookup"><span data-stu-id="73c3b-163">string</span></span> | <span data-ttu-id="73c3b-164">Igen</span><span class="sxs-lookup"><span data-stu-id="73c3b-164">Yes</span></span>      | <span data-ttu-id="73c3b-165">Egy GUID formátumú karakterlánc, amely azonosítja a próba-előfizetést.</span><span class="sxs-lookup"><span data-stu-id="73c3b-165">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="73c3b-166">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="73c3b-166">Request headers</span></span>

<span data-ttu-id="73c3b-167">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="73c3b-167">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="73c3b-168">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="73c3b-168">Request body</span></span>

<span data-ttu-id="73c3b-169">A kérelem törzsében szerepelnie kell egy feltöltött [konverziós](conversions-resources.md#conversion) erőforrásnak.</span><span class="sxs-lookup"><span data-stu-id="73c3b-169">A populated [Conversion](conversions-resources.md#conversion) resource must be included in the request body.</span></span>

### <a name="request-example"></a><span data-ttu-id="73c3b-170">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="73c3b-170">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="73c3b-171">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="73c3b-171">REST response</span></span>

<span data-ttu-id="73c3b-172">Ha ez sikeres, a válasz törzse [ConversionResult](conversions-resources.md#conversionresult) -erőforrást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="73c3b-172">If successful, the response body contains a [ConversionResult](conversions-resources.md#conversionresult) resource.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="73c3b-173">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="73c3b-173">Response success and error codes</span></span>

<span data-ttu-id="73c3b-174">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="73c3b-174">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="73c3b-175">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="73c3b-175">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="73c3b-176">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="73c3b-176">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="73c3b-177">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="73c3b-177">Response example</span></span>

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
