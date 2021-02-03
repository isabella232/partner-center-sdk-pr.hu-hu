---
title: Termékek listájának lekérése (ország alapján)
description: A Product (termék) erőforrás használatával a termékek gyűjteményét az ügyfél országa veheti igénybe.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ea239aa008a5b7c33740e9c4697c3795908415cd
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768172"
---
# <a name="get-a-list-of-products-by-country"></a><span data-ttu-id="f62ed-103">Termékek listájának lekérése (ország alapján)</span><span class="sxs-lookup"><span data-stu-id="f62ed-103">Get a list of products (by country)</span></span>

<span data-ttu-id="f62ed-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="f62ed-104">**Applies to:**</span></span>

- <span data-ttu-id="f62ed-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f62ed-105">Partner Center</span></span>
- <span data-ttu-id="f62ed-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="f62ed-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f62ed-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f62ed-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f62ed-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f62ed-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f62ed-109">A következő módszerekkel kérheti le egy adott országban elérhető termékek gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="f62ed-109">You can use the following methods to get a collection of products available in a particular country.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f62ed-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f62ed-110">Prerequisites</span></span>

- <span data-ttu-id="f62ed-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="f62ed-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f62ed-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="f62ed-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f62ed-113">Egy ország.</span><span class="sxs-lookup"><span data-stu-id="f62ed-113">A country.</span></span>

## <a name="c"></a><span data-ttu-id="f62ed-114">C\#</span><span class="sxs-lookup"><span data-stu-id="f62ed-114">C\#</span></span>

<span data-ttu-id="f62ed-115">A termékek listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="f62ed-115">To get a list of products:</span></span>

1. <span data-ttu-id="f62ed-116">A **IAggregatePartner. Products** gyűjtemény használatával válassza ki az országot a **ByCountry ()** metódus használatával.</span><span class="sxs-lookup"><span data-stu-id="f62ed-116">Use your **IAggregatePartner.Products** collection to select the country by using the **ByCountry()** method.</span></span>

2. <span data-ttu-id="f62ed-117">Válassza ki a katalógus nézetet a **ByTargetView ()** metódus használatával.</span><span class="sxs-lookup"><span data-stu-id="f62ed-117">Select the catalog view using the **ByTargetView()** method.</span></span>

3. <span data-ttu-id="f62ed-118">Választható Válassza ki a foglalási hatókört a **ByReservationScope ()** metódus használatával.</span><span class="sxs-lookup"><span data-stu-id="f62ed-118">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

4. <span data-ttu-id="f62ed-119">Választható A **ByTargetSegment ()** metódus használatával válassza ki a célként megadott szegmenst.</span><span class="sxs-lookup"><span data-stu-id="f62ed-119">(Optional) Select the target segment using the **ByTargetSegment()** method.</span></span>

5. <span data-ttu-id="f62ed-120">A gyűjtemény visszaadásához hívja meg a **Get ()** vagy a **GetAsync ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="f62ed-120">Call the **Get()** or **GetAsync()** method to return the collection.</span></span>

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a><span data-ttu-id="f62ed-121">Java</span><span class="sxs-lookup"><span data-stu-id="f62ed-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="f62ed-122">A termékek listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="f62ed-122">To get a list of products:</span></span>

1. <span data-ttu-id="f62ed-123">Használja az **IAggregatePartner. getProducts** függvényt az ország kiválasztásához a **byCountry ()** függvény használatával.</span><span class="sxs-lookup"><span data-stu-id="f62ed-123">Use your **IAggregatePartner.getProducts** function to select the country by using the **byCountry()** function.</span></span>

2. <span data-ttu-id="f62ed-124">Válassza ki a katalógus nézetet a **byTargetView ()** függvény használatával.</span><span class="sxs-lookup"><span data-stu-id="f62ed-124">Select the catalog view using the **byTargetView()** function.</span></span>
3. <span data-ttu-id="f62ed-125">Választható Válassza ki a cél szegmenst a **byTargetSegment ()** függvény használatával.</span><span class="sxs-lookup"><span data-stu-id="f62ed-125">(Optional) Select the target segment using the **byTargetSegment()** function.</span></span>

4. <span data-ttu-id="f62ed-126">A gyűjtemény visszaküldéséhez hívja meg a **Get ()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="f62ed-126">Call the **get()** function to return the collection.</span></span>

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a><span data-ttu-id="f62ed-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f62ed-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="f62ed-128">A termékek listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="f62ed-128">To get a list of products:</span></span>

1. <span data-ttu-id="f62ed-129">Futtassa a [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) parancsot.</span><span class="sxs-lookup"><span data-stu-id="f62ed-129">Execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command.</span></span>

2. <span data-ttu-id="f62ed-130">Válassza ki a katalógust a **katalógus** paraméter megadásával.</span><span class="sxs-lookup"><span data-stu-id="f62ed-130">Select the catalog by specifying the **Catalog** parameter.</span></span>
3. <span data-ttu-id="f62ed-131">Választható Válassza ki a cél szegmenst a **szegmens** paraméter megadásával.</span><span class="sxs-lookup"><span data-stu-id="f62ed-131">(Optional) Select the target segment by specifying the **Segment** parameter.</span></span>

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a><span data-ttu-id="f62ed-132">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="f62ed-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f62ed-133">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f62ed-133">Request syntax</span></span>

| <span data-ttu-id="f62ed-134">Metódus</span><span class="sxs-lookup"><span data-stu-id="f62ed-134">Method</span></span>  | <span data-ttu-id="f62ed-135">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f62ed-135">Request URI</span></span>                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="f62ed-136">**GET**</span><span class="sxs-lookup"><span data-stu-id="f62ed-136">**GET**</span></span> | <span data-ttu-id="f62ed-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products? ország = {ország} &targetView = {targetView} &targetSegment = {TARGETSEGMENT} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f62ed-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="f62ed-138">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="f62ed-138">URI parameters</span></span>

<span data-ttu-id="f62ed-139">A termékek listájának megjelenítéséhez használja a következő elérési utat és a lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="f62ed-139">Use the following path and query parameters to get a list of products.</span></span>

| <span data-ttu-id="f62ed-140">Név</span><span class="sxs-lookup"><span data-stu-id="f62ed-140">Name</span></span>                   | <span data-ttu-id="f62ed-141">Típus</span><span class="sxs-lookup"><span data-stu-id="f62ed-141">Type</span></span>     | <span data-ttu-id="f62ed-142">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f62ed-142">Required</span></span> | <span data-ttu-id="f62ed-143">Leírás</span><span class="sxs-lookup"><span data-stu-id="f62ed-143">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="f62ed-144">ország</span><span class="sxs-lookup"><span data-stu-id="f62ed-144">country</span></span>                | <span data-ttu-id="f62ed-145">sztring</span><span class="sxs-lookup"><span data-stu-id="f62ed-145">string</span></span>   | <span data-ttu-id="f62ed-146">Igen</span><span class="sxs-lookup"><span data-stu-id="f62ed-146">Yes</span></span>      | <span data-ttu-id="f62ed-147">Az ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="f62ed-147">The country/region ID.</span></span>                                                  |
| <span data-ttu-id="f62ed-148">targetView</span><span class="sxs-lookup"><span data-stu-id="f62ed-148">targetView</span></span>             | <span data-ttu-id="f62ed-149">sztring</span><span class="sxs-lookup"><span data-stu-id="f62ed-149">string</span></span>   | <span data-ttu-id="f62ed-150">Igen</span><span class="sxs-lookup"><span data-stu-id="f62ed-150">Yes</span></span>      | <span data-ttu-id="f62ed-151">Meghatározza a katalógus céljának nézetét.</span><span class="sxs-lookup"><span data-stu-id="f62ed-151">Identifies the target view of the catalog.</span></span> <span data-ttu-id="f62ed-152">A támogatott értékek a következők:</span><span class="sxs-lookup"><span data-stu-id="f62ed-152">The supported values are:</span></span> <br/><br/><span data-ttu-id="f62ed-153">**Azure**, amely tartalmazza az összes Azure-elemet</span><span class="sxs-lookup"><span data-stu-id="f62ed-153">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="f62ed-154">**AzureReservations**, amely tartalmazza az összes Azure foglalási elemet</span><span class="sxs-lookup"><span data-stu-id="f62ed-154">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="f62ed-155">**AzureReservationsVM**, amely tartalmazza az összes virtuális gép (VM) foglalási elemét</span><span class="sxs-lookup"><span data-stu-id="f62ed-155">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="f62ed-156">**AzureReservationsSQL**, amely az összes SQL-foglalási elemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="f62ed-156">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="f62ed-157">**AzureReservationsCosmosDb**, amely tartalmazza az összes Cosmos-adatbázis foglalási elemét.</span><span class="sxs-lookup"><span data-stu-id="f62ed-157">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="f62ed-158">**MicrosoftAzure**, amely Microsoft Azure előfizetések (**MS-AZR-0145P**) és az Azure-csomagok elemeit tartalmazza</span><span class="sxs-lookup"><span data-stu-id="f62ed-158">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="f62ed-159">**OnlineServices**, amely tartalmazza az összes online szolgáltatási elemet (beleértve a kereskedelmi piactér termékeit is)</span><span class="sxs-lookup"><span data-stu-id="f62ed-159">**OnlineServices**, which includes all online service items (including commercial marketplace products)</span></span><br/><br/><span data-ttu-id="f62ed-160">**Szoftver**, amely tartalmazza az összes szoftver elemet</span><span class="sxs-lookup"><span data-stu-id="f62ed-160">**Software**, which includes all software items</span></span><br/><br/><span data-ttu-id="f62ed-161">**SoftwareSUSELinux**, amely tartalmazza az összes szoftver SUSE Linux-elemet</span><span class="sxs-lookup"><span data-stu-id="f62ed-161">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="f62ed-162">**SoftwarePerpetual**, amely tartalmazza az összes örökös szoftver elemet.</span><span class="sxs-lookup"><span data-stu-id="f62ed-162">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="f62ed-163">**SoftwareSubscriptions**, amely tartalmazza az összes szoftver-előfizetési elemet</span><span class="sxs-lookup"><span data-stu-id="f62ed-163">**SoftwareSubscriptions**, which includes all software subscription items</span></span>    |
| <span data-ttu-id="f62ed-164">targetSegment</span><span class="sxs-lookup"><span data-stu-id="f62ed-164">targetSegment</span></span>          | <span data-ttu-id="f62ed-165">sztring</span><span class="sxs-lookup"><span data-stu-id="f62ed-165">string</span></span>   | <span data-ttu-id="f62ed-166">No</span><span class="sxs-lookup"><span data-stu-id="f62ed-166">No</span></span>       | <span data-ttu-id="f62ed-167">A célként megadott szegmenst azonosítja.</span><span class="sxs-lookup"><span data-stu-id="f62ed-167">Identifies the target segment.</span></span> <span data-ttu-id="f62ed-168">A különböző célközönségek nézete.</span><span class="sxs-lookup"><span data-stu-id="f62ed-168">The view for different target audiences.</span></span> <span data-ttu-id="f62ed-169">A támogatott értékek a következők:</span><span class="sxs-lookup"><span data-stu-id="f62ed-169">The supported values are:</span></span> <br/><br/><span data-ttu-id="f62ed-170">**kereskedelmi**</span><span class="sxs-lookup"><span data-stu-id="f62ed-170">**commercial**</span></span><br/><span data-ttu-id="f62ed-171">**oktatás**</span><span class="sxs-lookup"><span data-stu-id="f62ed-171">**education**</span></span><br/><span data-ttu-id="f62ed-172">**kormány**</span><span class="sxs-lookup"><span data-stu-id="f62ed-172">**government**</span></span><br/><span data-ttu-id="f62ed-173">**nonprofit**</span><span class="sxs-lookup"><span data-stu-id="f62ed-173">**nonprofit**</span></span>  |
| <span data-ttu-id="f62ed-174">reservationScope</span><span class="sxs-lookup"><span data-stu-id="f62ed-174">reservationScope</span></span> | <span data-ttu-id="f62ed-175">sztring</span><span class="sxs-lookup"><span data-stu-id="f62ed-175">string</span></span>   | <span data-ttu-id="f62ed-176">No</span><span class="sxs-lookup"><span data-stu-id="f62ed-176">No</span></span> | <span data-ttu-id="f62ed-177">A Azure Reservations termékek listájának lekérdezésekor az `reservationScope=AzurePlan` Azure-csomagokra érvényes termékek listájának lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="f62ed-177">When querying for a list of products for Azure Reservations, specify `reservationScope=AzurePlan` to get a list of products that are applicable to Azure plans.</span></span> <span data-ttu-id="f62ed-178">Zárja be ezt a paramétert, hogy lekérje a Microsoft Azure (**MS-AZR-0145P**) előfizetésekre vonatkozó termékek listáját az Azure-foglalásokhoz.</span><span class="sxs-lookup"><span data-stu-id="f62ed-178">Exclude this parameter to get a list of products for Azure reservations, which are applicable to Microsoft Azure (**MS-AZR-0145P**) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="f62ed-179">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f62ed-179">Request headers</span></span>

<span data-ttu-id="f62ed-180">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f62ed-180">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f62ed-181">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f62ed-181">Request body</span></span>

<span data-ttu-id="f62ed-182">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="f62ed-182">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="f62ed-183">Példák kérése</span><span class="sxs-lookup"><span data-stu-id="f62ed-183">Request examples</span></span>

#### <a name="products-by-country"></a><span data-ttu-id="f62ed-184">Termékek országonként</span><span class="sxs-lookup"><span data-stu-id="f62ed-184">Products by country</span></span>

<span data-ttu-id="f62ed-185">Ezt a példát követve beolvashatja a termékek ország szerinti listáját Microsoft Azure (MS-AZR-0145P) előfizetések és az Azure-csomagok alapján.</span><span class="sxs-lookup"><span data-stu-id="f62ed-185">Follow this example to get a list of products by country for Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a><span data-ttu-id="f62ed-186">Azure VM-foglalások (Azure-csomag)</span><span class="sxs-lookup"><span data-stu-id="f62ed-186">Azure VM reservations (Azure plan)</span></span>

<span data-ttu-id="f62ed-187">Ezt a példát követve az Azure-csomagokra érvényes Azure-beli virtuális gépekhez tartozó termékek országonkénti listáját kaphatja meg.</span><span class="sxs-lookup"><span data-stu-id="f62ed-187">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="f62ed-188">Azure-beli virtuális gépek foglalása Microsoft Azure (MS-AZR-0145P) előfizetésekhez</span><span class="sxs-lookup"><span data-stu-id="f62ed-188">Azure VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="f62ed-189">Ezt a példát követve megtekintheti az ország által a Microsoft Azure (MS-AZR-0145P) előfizetésekre alkalmazható Azure-beli virtuálisgép-foglalások listáját.</span><span class="sxs-lookup"><span data-stu-id="f62ed-189">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="f62ed-190">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f62ed-190">REST response</span></span>

<span data-ttu-id="f62ed-191">Ha ez sikeres, a válasz törzse tartalmazza a [**termék**](product-resources.md#product) erőforrásainak gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="f62ed-191">If successful, the response body contains a collection of [**Product**](product-resources.md#product) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f62ed-192">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f62ed-192">Response success and error codes</span></span>

<span data-ttu-id="f62ed-193">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="f62ed-193">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f62ed-194">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="f62ed-194">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f62ed-195">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f62ed-195">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="f62ed-196">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="f62ed-196">This method returns the following error codes:</span></span>

| <span data-ttu-id="f62ed-197">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="f62ed-197">HTTP Status Code</span></span>     | <span data-ttu-id="f62ed-198">Hibakód</span><span class="sxs-lookup"><span data-stu-id="f62ed-198">Error code</span></span>   | <span data-ttu-id="f62ed-199">Leírás</span><span class="sxs-lookup"><span data-stu-id="f62ed-199">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f62ed-200">403</span><span class="sxs-lookup"><span data-stu-id="f62ed-200">403</span></span>                  | <span data-ttu-id="f62ed-201">400030</span><span class="sxs-lookup"><span data-stu-id="f62ed-201">400030</span></span>       | <span data-ttu-id="f62ed-202">A kért targetSegment való hozzáférés nem engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="f62ed-202">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="f62ed-203">403</span><span class="sxs-lookup"><span data-stu-id="f62ed-203">403</span></span>                  | <span data-ttu-id="f62ed-204">400036</span><span class="sxs-lookup"><span data-stu-id="f62ed-204">400036</span></span>       | <span data-ttu-id="f62ed-205">A kért targetView való hozzáférés nem engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="f62ed-205">Access to the requested targetView is not allowed.</span></span>                                                        |

### <a name="response-example"></a><span data-ttu-id="f62ed-206">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f62ed-206">Response example</span></span>

```http
{
    "totalCount": 19,
    "items": [
        {
            "id": "DZH318Z0BQ3Q",
            "title": "Virtual Machines DSv2 Series",
            "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
            "productType": {
                "id": "Azure",
                "displayName": "Azure",
                "subType": {
                "id": "VirtualMachines",
                "displayName": "VirtualMachines"
                }
            },
            "isMicrosoftProduct": true,
            "publisherName": "Microsoft",
            "links": {
                "skus": {
                    "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
