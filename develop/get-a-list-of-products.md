---
title: Termékek listájának lekérése (ország alapján)
description: A Product erőforrással termékek gyűjteményét kaphatja meg az ügyfél országa szerint.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 1258727ecbe7c5cc332624577fa8a355e28e3717
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874210"
---
# <a name="get-a-list-of-products-by-country"></a><span data-ttu-id="9f415-103">Termékek listájának lekérése (ország alapján)</span><span class="sxs-lookup"><span data-stu-id="9f415-103">Get a list of products (by country)</span></span>

<span data-ttu-id="9f415-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9f415-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9f415-105">Az alábbi módszerekkel egy adott országban elérhető termékek gyűjteményét kaphatja meg.</span><span class="sxs-lookup"><span data-stu-id="9f415-105">You can use the following methods to get a collection of products available in a particular country.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f415-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="9f415-106">Prerequisites</span></span>

- <span data-ttu-id="9f415-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9f415-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9f415-108">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="9f415-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9f415-109">Egy ország.</span><span class="sxs-lookup"><span data-stu-id="9f415-109">A country.</span></span>

## <a name="c"></a><span data-ttu-id="9f415-110">C\#</span><span class="sxs-lookup"><span data-stu-id="9f415-110">C\#</span></span>

<span data-ttu-id="9f415-111">A termékek listájának lekért listája:</span><span class="sxs-lookup"><span data-stu-id="9f415-111">To get a list of products:</span></span>

1. <span data-ttu-id="9f415-112">Az **IAggregatePartner.Products gyűjtemény** használatával válassza ki az országot a **ByCountry() metódussal.**</span><span class="sxs-lookup"><span data-stu-id="9f415-112">Use your **IAggregatePartner.Products** collection to select the country by using the **ByCountry()** method.</span></span>

2. <span data-ttu-id="9f415-113">Válassza ki a katalógusnézetet a **ByTargetView() metódussal.**</span><span class="sxs-lookup"><span data-stu-id="9f415-113">Select the catalog view using the **ByTargetView()** method.</span></span>

3. <span data-ttu-id="9f415-114">(Nem kötelező) Válassza ki a foglalási hatókört a **ByReservationScope() metódussal.**</span><span class="sxs-lookup"><span data-stu-id="9f415-114">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

4. <span data-ttu-id="9f415-115">(Nem kötelező) Válassza ki a célszegmenst a **ByTargetSegment() metódussal.**</span><span class="sxs-lookup"><span data-stu-id="9f415-115">(Optional) Select the target segment using the **ByTargetSegment()** method.</span></span>

5. <span data-ttu-id="9f415-116">A **gyűjtemény visszaadáshoz hívja** meg a Get() vagy **a GetAsync()** metódust.</span><span class="sxs-lookup"><span data-stu-id="9f415-116">Call the **Get()** or **GetAsync()** method to return the collection.</span></span>

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

## <a name="java"></a><span data-ttu-id="9f415-117">Java</span><span class="sxs-lookup"><span data-stu-id="9f415-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="9f415-118">A termékek listájának lekért listája:</span><span class="sxs-lookup"><span data-stu-id="9f415-118">To get a list of products:</span></span>

1. <span data-ttu-id="9f415-119">Az **IAggregatePartner.getProducts** függvény használatával válassza ki az országot a **byCountry() függvény** használatával.</span><span class="sxs-lookup"><span data-stu-id="9f415-119">Use your **IAggregatePartner.getProducts** function to select the country by using the **byCountry()** function.</span></span>

2. <span data-ttu-id="9f415-120">Válassza ki a katalógusnézetet a **byTargetView() függvény** használatával.</span><span class="sxs-lookup"><span data-stu-id="9f415-120">Select the catalog view using the **byTargetView()** function.</span></span>
3. <span data-ttu-id="9f415-121">(Nem kötelező) Válassza ki a **célszegmenst a byTargetSegment() függvény** használatával.</span><span class="sxs-lookup"><span data-stu-id="9f415-121">(Optional) Select the target segment using the **byTargetSegment()** function.</span></span>

4. <span data-ttu-id="9f415-122">A **gyűjtemény visszaadáshoz hívja** meg a get() függvényt.</span><span class="sxs-lookup"><span data-stu-id="9f415-122">Call the **get()** function to return the collection.</span></span>

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a><span data-ttu-id="9f415-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f415-123">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="9f415-124">A termékek listájának lekért listája:</span><span class="sxs-lookup"><span data-stu-id="9f415-124">To get a list of products:</span></span>

1. <span data-ttu-id="9f415-125">Hajtsa végre [**a Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) parancsot.</span><span class="sxs-lookup"><span data-stu-id="9f415-125">Execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command.</span></span>

2. <span data-ttu-id="9f415-126">Válassza ki a katalógust a Catalog paraméter **megadásával.**</span><span class="sxs-lookup"><span data-stu-id="9f415-126">Select the catalog by specifying the **Catalog** parameter.</span></span>
3. <span data-ttu-id="9f415-127">(Nem kötelező) Válassza ki a célszegmenst a **Szegmens paraméter megadásával.**</span><span class="sxs-lookup"><span data-stu-id="9f415-127">(Optional) Select the target segment by specifying the **Segment** parameter.</span></span>

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a><span data-ttu-id="9f415-128">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="9f415-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9f415-129">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="9f415-129">Request syntax</span></span>

| <span data-ttu-id="9f415-130">Metódus</span><span class="sxs-lookup"><span data-stu-id="9f415-130">Method</span></span>  | <span data-ttu-id="9f415-131">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="9f415-131">Request URI</span></span>                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="9f415-132">**Kap**</span><span class="sxs-lookup"><span data-stu-id="9f415-132">**GET**</span></span> | <span data-ttu-id="9f415-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9f415-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="9f415-134">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="9f415-134">URI parameters</span></span>

<span data-ttu-id="9f415-135">Az alábbi elérési út és lekérdezési paraméterek használatával lekérdezheti a termékek listáját.</span><span class="sxs-lookup"><span data-stu-id="9f415-135">Use the following path and query parameters to get a list of products.</span></span>

| <span data-ttu-id="9f415-136">Név</span><span class="sxs-lookup"><span data-stu-id="9f415-136">Name</span></span>                   | <span data-ttu-id="9f415-137">Típus</span><span class="sxs-lookup"><span data-stu-id="9f415-137">Type</span></span>     | <span data-ttu-id="9f415-138">Kötelező</span><span class="sxs-lookup"><span data-stu-id="9f415-138">Required</span></span> | <span data-ttu-id="9f415-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="9f415-139">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="9f415-140">ország</span><span class="sxs-lookup"><span data-stu-id="9f415-140">country</span></span>                | <span data-ttu-id="9f415-141">sztring</span><span class="sxs-lookup"><span data-stu-id="9f415-141">string</span></span>   | <span data-ttu-id="9f415-142">Igen</span><span class="sxs-lookup"><span data-stu-id="9f415-142">Yes</span></span>      | <span data-ttu-id="9f415-143">Az ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="9f415-143">The country/region ID.</span></span>                                                  |
| <span data-ttu-id="9f415-144">targetView</span><span class="sxs-lookup"><span data-stu-id="9f415-144">targetView</span></span>             | <span data-ttu-id="9f415-145">sztring</span><span class="sxs-lookup"><span data-stu-id="9f415-145">string</span></span>   | <span data-ttu-id="9f415-146">Igen</span><span class="sxs-lookup"><span data-stu-id="9f415-146">Yes</span></span>      | <span data-ttu-id="9f415-147">A katalógus célnézetét azonosítja.</span><span class="sxs-lookup"><span data-stu-id="9f415-147">Identifies the target view of the catalog.</span></span> <span data-ttu-id="9f415-148">A támogatott értékek a következőek:</span><span class="sxs-lookup"><span data-stu-id="9f415-148">The supported values are:</span></span> <br/><br/><span data-ttu-id="9f415-149">**Azure**, amely az összes Azure-elemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="9f415-149">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="9f415-150">**AzureReservations**, amely az összes Azure-foglalási elemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="9f415-150">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="9f415-151">**AzureReservationsVM,** amely az összes virtuálisgép-foglalási elemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="9f415-151">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="9f415-152">**AzureReservationsSQL,** amely az összes SQL tartalmazza</span><span class="sxs-lookup"><span data-stu-id="9f415-152">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="9f415-153">**AzureReservationsCosmosDb**, amely az összes Cosmos-adatbázis foglalási elemét tartalmazza</span><span class="sxs-lookup"><span data-stu-id="9f415-153">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="9f415-154">**MicrosoftAzure**, amely Microsoft Azure **(MS-AZR-0145P)** és Azure-csomagokhoz tartalmaz elemeket</span><span class="sxs-lookup"><span data-stu-id="9f415-154">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="9f415-155">**OnlineServices**, amely az összes online szolgáltatási elemet tartalmazza (a kereskedelmi piactéren elérhető termékeket is beleértve)</span><span class="sxs-lookup"><span data-stu-id="9f415-155">**OnlineServices**, which includes all online service items (including commercial marketplace products)</span></span><br/><br/><span data-ttu-id="9f415-156">**Szoftver,** amely az összes szoftverelemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="9f415-156">**Software**, which includes all software items</span></span><br/><br/><span data-ttu-id="9f415-157">**SoftwareSUSELinux**, amely az összes szoftveres SUSE Linux-elemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="9f415-157">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="9f415-158">**SzoftverPerpetual**, amely az összes folyamatos szoftverelemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="9f415-158">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="9f415-159">**SoftwareSubscriptions**, amely az összes szoftver-előfizetési elemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="9f415-159">**SoftwareSubscriptions**, which includes all software subscription items</span></span>    |
| <span data-ttu-id="9f415-160">targetSegment</span><span class="sxs-lookup"><span data-stu-id="9f415-160">targetSegment</span></span>          | <span data-ttu-id="9f415-161">sztring</span><span class="sxs-lookup"><span data-stu-id="9f415-161">string</span></span>   | <span data-ttu-id="9f415-162">No</span><span class="sxs-lookup"><span data-stu-id="9f415-162">No</span></span>       | <span data-ttu-id="9f415-163">Azonosítja a célszegmenst.</span><span class="sxs-lookup"><span data-stu-id="9f415-163">Identifies the target segment.</span></span> <span data-ttu-id="9f415-164">A különböző célközönségek nézete.</span><span class="sxs-lookup"><span data-stu-id="9f415-164">The view for different target audiences.</span></span> <span data-ttu-id="9f415-165">A támogatott értékek a következőek:</span><span class="sxs-lookup"><span data-stu-id="9f415-165">The supported values are:</span></span> <br/><br/><span data-ttu-id="9f415-166">**Kereskedelmi**</span><span class="sxs-lookup"><span data-stu-id="9f415-166">**commercial**</span></span><br/><span data-ttu-id="9f415-167">**Oktatás**</span><span class="sxs-lookup"><span data-stu-id="9f415-167">**education**</span></span><br/><span data-ttu-id="9f415-168">**Kormány**</span><span class="sxs-lookup"><span data-stu-id="9f415-168">**government**</span></span><br/><span data-ttu-id="9f415-169">**Nonprofit**</span><span class="sxs-lookup"><span data-stu-id="9f415-169">**nonprofit**</span></span>  |
| <span data-ttu-id="9f415-170">reservationScope</span><span class="sxs-lookup"><span data-stu-id="9f415-170">reservationScope</span></span> | <span data-ttu-id="9f415-171">sztring</span><span class="sxs-lookup"><span data-stu-id="9f415-171">string</span></span>   | <span data-ttu-id="9f415-172">No</span><span class="sxs-lookup"><span data-stu-id="9f415-172">No</span></span> | <span data-ttu-id="9f415-173">Az Azure Reservationshez használható termékek listájának lekérdezésekor adja meg a következőt: , hogy lekérdezi az Azure-csomagokra vonatkozó `reservationScope=AzurePlan` termékek listáját.</span><span class="sxs-lookup"><span data-stu-id="9f415-173">When querying for a list of products for Azure Reservations, specify `reservationScope=AzurePlan` to get a list of products that are applicable to Azure plans.</span></span> <span data-ttu-id="9f415-174">Zárja ki ezt a paramétert, hogy lekérte a termékek listáját az Azure Reservationshez, amelyek Microsoft Azure (**MS-AZR-0145P**) előfizetésre vonatkoznak.</span><span class="sxs-lookup"><span data-stu-id="9f415-174">Exclude this parameter to get a list of products for Azure reservations, which are applicable to Microsoft Azure (**MS-AZR-0145P**) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="9f415-175">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="9f415-175">Request headers</span></span>

<span data-ttu-id="9f415-176">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9f415-176">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9f415-177">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="9f415-177">Request body</span></span>

<span data-ttu-id="9f415-178">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="9f415-178">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="9f415-179">Példák kérésre</span><span class="sxs-lookup"><span data-stu-id="9f415-179">Request examples</span></span>

#### <a name="products-by-country"></a><span data-ttu-id="9f415-180">Termékek ország szerint</span><span class="sxs-lookup"><span data-stu-id="9f415-180">Products by country</span></span>

<span data-ttu-id="9f415-181">Ebben a példában országonként lekért termékek listáját Microsoft Azure (MS-AZR-0145P) előfizetések és Azure-csomagok esetében.</span><span class="sxs-lookup"><span data-stu-id="9f415-181">Follow this example to get a list of products by country for Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a><span data-ttu-id="9f415-182">Azure-beli virtuális gépek foglalása (Azure-csomag)</span><span class="sxs-lookup"><span data-stu-id="9f415-182">Azure VM reservations (Azure plan)</span></span>

<span data-ttu-id="9f415-183">Kövesse ezt a példát az Azure-csomagokra vonatkozó Azure-beli virtuálisgép-foglalások termékek országonkénti listájának lekért listájáért.</span><span class="sxs-lookup"><span data-stu-id="9f415-183">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="9f415-184">Azure-beli virtuális gépek foglalása Microsoft Azure (MS-AZR-0145P) előfizetéshez</span><span class="sxs-lookup"><span data-stu-id="9f415-184">Azure VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="9f415-185">Az alábbi példa alapján országonként lekért termékek listája az azure-beli virtuális gépek foglalásához, amelyek Microsoft Azure (MS-AZR-0145P) előfizetésre vonatkoznak.</span><span class="sxs-lookup"><span data-stu-id="9f415-185">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="9f415-186">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="9f415-186">REST response</span></span>

<span data-ttu-id="9f415-187">Ha ez sikeres, a válasz törzse termékerőforrások [**gyűjteményét**](product-resources.md#product) tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="9f415-187">If successful, the response body contains a collection of [**Product**](product-resources.md#product) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9f415-188">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="9f415-188">Response success and error codes</span></span>

<span data-ttu-id="9f415-189">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="9f415-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9f415-190">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="9f415-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9f415-191">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9f415-191">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="9f415-192">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="9f415-192">This method returns the following error codes:</span></span>

| <span data-ttu-id="9f415-193">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="9f415-193">HTTP Status Code</span></span>     | <span data-ttu-id="9f415-194">Hibakód</span><span class="sxs-lookup"><span data-stu-id="9f415-194">Error code</span></span>   | <span data-ttu-id="9f415-195">Leírás</span><span class="sxs-lookup"><span data-stu-id="9f415-195">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9f415-196">403</span><span class="sxs-lookup"><span data-stu-id="9f415-196">403</span></span>                  | <span data-ttu-id="9f415-197">400030</span><span class="sxs-lookup"><span data-stu-id="9f415-197">400030</span></span>       | <span data-ttu-id="9f415-198">A kért targetSegment szolgáltatáshoz való hozzáférés nem engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="9f415-198">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="9f415-199">403</span><span class="sxs-lookup"><span data-stu-id="9f415-199">403</span></span>                  | <span data-ttu-id="9f415-200">400036</span><span class="sxs-lookup"><span data-stu-id="9f415-200">400036</span></span>       | <span data-ttu-id="9f415-201">A kért targetView-hoz való hozzáférés nem engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="9f415-201">Access to the requested targetView is not allowed.</span></span>                                                        |

### <a name="response-example"></a><span data-ttu-id="9f415-202">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="9f415-202">Response example</span></span>

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
