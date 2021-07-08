---
title: Ügyfél Azure-használati rekordjainak lekérése
description: Az Azure utilization API használatával lekérte egy ügyfél Azure-előfizetésének kihasználtsági rekordjait egy adott időszakra.
ms.date: 04/19/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7024bc65976a9b43a62b66c529d271519181ab23
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874924"
---
# <a name="get-a-customers-utilization-records-for-azure"></a><span data-ttu-id="08ace-103">Ügyfél Azure-használati rekordjainak lekérése</span><span class="sxs-lookup"><span data-stu-id="08ace-103">Get a customer's utilization records for Azure</span></span>

<span data-ttu-id="08ace-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="08ace-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="08ace-105">Az ügyfél Azure-előfizetésének kihasználtsági rekordjait egy adott időszakra az Azure utilization API-val kaphatja meg.</span><span class="sxs-lookup"><span data-stu-id="08ace-105">You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08ace-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="08ace-106">Prerequisites</span></span>

- <span data-ttu-id="08ace-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="08ace-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="08ace-108">Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="08ace-108">This scenario supports authentication with both standalone app and App+User credentials.</span></span>

- <span data-ttu-id="08ace-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="08ace-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="08ace-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="08ace-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="08ace-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="08ace-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="08ace-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="08ace-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="08ace-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="08ace-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="08ace-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="08ace-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="08ace-115">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="08ace-115">A subscription identifier.</span></span>

<span data-ttu-id="08ace-116">Ez az API egy tetszőleges időtartamra napi és óránkénti, nem időzített felhasználást ad vissza.</span><span class="sxs-lookup"><span data-stu-id="08ace-116">This API returns daily and hourly unrated consumption for an arbitrary time span.</span></span> <span data-ttu-id="08ace-117">Ez *az API azonban nem támogatott az Azure-csomagokhoz.*</span><span class="sxs-lookup"><span data-stu-id="08ace-117">However, *this API isn't supported for Azure plans*.</span></span> <span data-ttu-id="08ace-118">Ha már van Azure-csomagja, tekintse meg a számlázatlan használatú sorok cikkeit és a számlázott használatú sorok [cikkeit.](get-invoice-billed-consumption-lineitems.md) [](get-invoice-unbilled-consumption-lineitems.md)</span><span class="sxs-lookup"><span data-stu-id="08ace-118">If you have an Azure plan, see the articles [Get invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead.</span></span> <span data-ttu-id="08ace-119">Ezek a cikkek azt ismertetik, hogyan lehet mérőnként napi szinten lekért névleges fogyasztást erőforrásonként.</span><span class="sxs-lookup"><span data-stu-id="08ace-119">These articles describe how to get rated consumption at a daily level per meter per resource.</span></span> <span data-ttu-id="08ace-120">Ez a díjfelhasználás megegyezik az Azure utilization API által biztosított napi rendszerességgel kapcsolatos adatokkal.</span><span class="sxs-lookup"><span data-stu-id="08ace-120">This rate consumption is equivalent to the daily grain data provided by the Azure utilization API.</span></span> <span data-ttu-id="08ace-121">A számlázott használati adatok lekéréséhez a számlaazonosítót kell használnia.</span><span class="sxs-lookup"><span data-stu-id="08ace-121">You'll need to use the invoice identifier to retrieve billed usage data.</span></span> <span data-ttu-id="08ace-122">Az aktuális és az előző időszakokkal is lekérteheti a ki nemszámlázatlan használati becsléseket.</span><span class="sxs-lookup"><span data-stu-id="08ace-122">Or, you can use current and previous periods to get unbilled usage estimates.</span></span> <span data-ttu-id="08ace-123">Az óránkénti adat- és tetszőleges dátumtartomány-szűrők jelenleg nem támogatottak az *Azure-csomag előfizetési erőforrásaihoz.*</span><span class="sxs-lookup"><span data-stu-id="08ace-123">*Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.</span></span>

## <a name="azure-utilization-api"></a><span data-ttu-id="08ace-124">Azure-kihasználtsági API</span><span class="sxs-lookup"><span data-stu-id="08ace-124">Azure utilization API</span></span>

<span data-ttu-id="08ace-125">Ez az Azure-beli kihasználtsági API hozzáférést biztosít a kihasználtsági rekordokhoz egy olyan időszakra vonatkozóan, amely a kihasználtság számlázási rendszerben való jelentésének idejét jelöli.</span><span class="sxs-lookup"><span data-stu-id="08ace-125">This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system.</span></span> <span data-ttu-id="08ace-126">Hozzáférést biztosít ugyanazokhoz a kihasználtsági adatokhoz, amelyek az egyeztetési fájl létrehozásához és kiszámításához használatosak.</span><span class="sxs-lookup"><span data-stu-id="08ace-126">It provides access to the same utilization data that is used to create and calculate the reconciliation file.</span></span> <span data-ttu-id="08ace-127">Nem ismeri azonban a számlázási rendszer egyeztetési fájllogikát.</span><span class="sxs-lookup"><span data-stu-id="08ace-127">However, it does not have knowledge of billing system reconciliation file logic.</span></span> <span data-ttu-id="08ace-128">Nem számíthat arra, hogy az egyeztetési fájl összegző eredményei pontosan ugyanannak az időszaknak az API-ból lekért eredményre illeszkednek.</span><span class="sxs-lookup"><span data-stu-id="08ace-128">You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.</span></span>

<span data-ttu-id="08ace-129">A számlázási rendszer például ugyanezeket a kihasználtsági adatokat alkalmazza, és késési szabályokat alkalmaz annak megállapításához, hogy mit kell figyelembe venni az egyeztetési fájlban.</span><span class="sxs-lookup"><span data-stu-id="08ace-129">For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file.</span></span> <span data-ttu-id="08ace-130">Amikor egy számlázási időszak lezárul, az egyeztetési fájl tartalmazza a számlázási időszak végét elvégő nap végéig minden használatot.</span><span class="sxs-lookup"><span data-stu-id="08ace-130">When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file.</span></span> <span data-ttu-id="08ace-131">A számlázási időszakon belül a számlázási időszak vége után 24 órán belül jelentett minden kései használatot a következő egyeztetési fájlban kell figyelembe venni.</span><span class="sxs-lookup"><span data-stu-id="08ace-131">Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file.</span></span> <span data-ttu-id="08ace-132">A partner számlázásának késési szabályaiért lásd: Azure-előfizetés fogyasztási [adatainak lekért adatai.](/previous-versions/azure/reference/mt219001(v=azure.100))</span><span class="sxs-lookup"><span data-stu-id="08ace-132">For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](/previous-versions/azure/reference/mt219001(v=azure.100)).</span></span>

<span data-ttu-id="08ace-133">Ez REST API lapra van ásva.</span><span class="sxs-lookup"><span data-stu-id="08ace-133">This REST API is paged.</span></span> <span data-ttu-id="08ace-134">Ha a válasz hasznos adatai nagyobbak egyetlen lapnál, a következő hivatkozásra kattintva le kell töltenie a kihasználtsági rekordok következő lapját.</span><span class="sxs-lookup"><span data-stu-id="08ace-134">If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.</span></span>

### <a name="scenario-partner-a-has-transferred-billing-ownership-of-azure-legacy-subscription-145p-to-partner-b"></a><span data-ttu-id="08ace-135">Forgatókönyv: Az A partner átvitte az Azure Legacy Subscription (145P) számlázási tulajdonjogát a B partnernek</span><span class="sxs-lookup"><span data-stu-id="08ace-135">Scenario: Partner A has transferred billing ownership of Azure Legacy Subscription (145P) to Partner B</span></span>

<span data-ttu-id="08ace-136">Ha egy partner egy örökölt Azure-előfizetés számlázási tulajdonjogát átadja egy másik partnernek, amikor az új partner a Utilization API-t hívja meg az átvitt előfizetéshez, akkor az Azure-jogosultságazonosító helyett a Commerce-előfizetés azonosítóját (amely a saját Partnerközpont-fiókjában jelenik meg) kell használnia.</span><span class="sxs-lookup"><span data-stu-id="08ace-136">If a partner transfers billing ownership of an Azure legacy subscription to another partner, when new the new partner calls Utilization API for transferred subscription they have to use Commerce Subscription ID (which shows up in their Partner Center account) rather than the Azure Entitlement ID.</span></span> <span data-ttu-id="08ace-137">Az Azure-jogosultságazonosító csak akkor jelenik meg a B partnernél, ha rendszergazda (AOBO) nevében az ügyfél Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="08ace-137">Azure Entitlement ID appears for Partner B only when they are Admin on behalf of (AOBO) to Customer's Azure portal.</span></span> 

<span data-ttu-id="08ace-138">Az átvitt előfizetés Utilization API-jának sikeres hívásához az új partnernek a Kereskedelmi előfizetés azonosítóját kell használnia.</span><span class="sxs-lookup"><span data-stu-id="08ace-138">To successfully call the Utilization API for the transferred subscription, the new partner needs to use the Commerce Subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="08ace-139">C\#</span><span class="sxs-lookup"><span data-stu-id="08ace-139">C\#</span></span>

<span data-ttu-id="08ace-140">Az Azure-beli kihasználtsági rekordok beszerzése:</span><span class="sxs-lookup"><span data-stu-id="08ace-140">To obtain the Azure Utilization Records:</span></span>

1. <span data-ttu-id="08ace-141">Szerezze be az ügyfél-azonosítót és az előfizetés-azonosítót.</span><span class="sxs-lookup"><span data-stu-id="08ace-141">Get the customer ID and subscription ID.</span></span>

2. <span data-ttu-id="08ace-142">Hívja meg az [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) metódust a kihasználtsági rekordokat tartalmazó [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) visszaadása érdekében.</span><span class="sxs-lookup"><span data-stu-id="08ace-142">Call the [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records.</span></span>

3. <span data-ttu-id="08ace-143">Szerezzen be egy Azure-beli kihasználtságirekord-enumerátort a kihasználtsági lapok bejárására.</span><span class="sxs-lookup"><span data-stu-id="08ace-143">Obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span> <span data-ttu-id="08ace-144">Erre a lépésre azért van szükség, mert az erőforrás-gyűjtemény lapként van meglaposodva.</span><span class="sxs-lookup"><span data-stu-id="08ace-144">This step is required, because the resource collection is paged.</span></span>

- <span data-ttu-id="08ace-145">**Minta:** [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="08ace-145">**Sample**: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="08ace-146">**Project:** Partnerközpont SDK minták</span><span class="sxs-lookup"><span data-stu-id="08ace-146">**Project**: Partner Center SDK Samples</span></span>
- <span data-ttu-id="08ace-147">**Osztály:** GetAzureSubscriptionUtilization.cs</span><span class="sxs-lookup"><span data-stu-id="08ace-147">**Class**: GetAzureSubscriptionUtilization.cs</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a><span data-ttu-id="08ace-148">Java</span><span class="sxs-lookup"><span data-stu-id="08ace-148">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="08ace-149">Az Azure-beli kihasználtsági rekordok beszerzéséhez először egy ügyfél-azonosítóra és egy előfizetés-azonosítóra van szükség.</span><span class="sxs-lookup"><span data-stu-id="08ace-149">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="08ace-150">Ezután meg kell hívnia az **IAzureUtilizationCollection.query** függvényt, hogy visszaadja a kihasználtsági rekordokat tartalmazó **ResourceCollection** adatokat.</span><span class="sxs-lookup"><span data-stu-id="08ace-150">You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records.</span></span> <span data-ttu-id="08ace-151">Mivel az erőforrás-gyűjtemény lapozódva van, be kell szereznie egy Azure-beli kihasználtságirekord-enumerátort a kihasználtsági oldalakon való áthaladáshoz.</span><span class="sxs-lookup"><span data-stu-id="08ace-151">Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a><span data-ttu-id="08ace-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08ace-152">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="08ace-153">Az Azure-beli kihasználtsági rekordok beszerzéséhez először egy ügyfél-azonosítóra és egy előfizetés-azonosítóra van szükség.</span><span class="sxs-lookup"><span data-stu-id="08ace-153">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="08ace-154">Ezután hívja meg a [**Get-PartnerCustomerSubscriptionUtilization függvényt.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md)</span><span class="sxs-lookup"><span data-stu-id="08ace-154">You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span></span> <span data-ttu-id="08ace-155">Ez a parancs a megadott időszakban elérhető összes rekordot visszaadja.</span><span class="sxs-lookup"><span data-stu-id="08ace-155">This command will return all records available for the specified period of time.</span></span>

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a><span data-ttu-id="08ace-156">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="08ace-156">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="08ace-157">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="08ace-157">Request syntax</span></span>

| <span data-ttu-id="08ace-158">Metódus</span><span class="sxs-lookup"><span data-stu-id="08ace-158">Method</span></span> | <span data-ttu-id="08ace-159">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="08ace-159">Request URI</span></span> |
|------- | ----------- |
| <span data-ttu-id="08ace-160">**Kap**</span><span class="sxs-lookup"><span data-stu-id="08ace-160">**GET**</span></span> | <span data-ttu-id="08ace-161">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/utilizations/azure?start \_ time={start-time}&\_ end-time={end-time}&granularity={granularity}&show \_ details={True}</span><span class="sxs-lookup"><span data-stu-id="08ace-161">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="08ace-162">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="08ace-162">URI parameters</span></span>

<span data-ttu-id="08ace-163">Az alábbi elérési út és lekérdezési paraméterek használatával lekérdezheti a kihasználtsági rekordokat.</span><span class="sxs-lookup"><span data-stu-id="08ace-163">Use the following path and query parameters to get the utilization records.</span></span>

| <span data-ttu-id="08ace-164">Név</span><span class="sxs-lookup"><span data-stu-id="08ace-164">Name</span></span> | <span data-ttu-id="08ace-165">Típus</span><span class="sxs-lookup"><span data-stu-id="08ace-165">Type</span></span> | <span data-ttu-id="08ace-166">Kötelező</span><span class="sxs-lookup"><span data-stu-id="08ace-166">Required</span></span> | <span data-ttu-id="08ace-167">Leírás</span><span class="sxs-lookup"><span data-stu-id="08ace-167">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="08ace-168">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="08ace-168">customer-tenant-id</span></span> | <span data-ttu-id="08ace-169">sztring</span><span class="sxs-lookup"><span data-stu-id="08ace-169">string</span></span> | <span data-ttu-id="08ace-170">Igen</span><span class="sxs-lookup"><span data-stu-id="08ace-170">Yes</span></span> | <span data-ttu-id="08ace-171">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="08ace-171">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="08ace-172">subscription-id (előfizetés-azonosító)</span><span class="sxs-lookup"><span data-stu-id="08ace-172">subscription-id</span></span> | <span data-ttu-id="08ace-173">sztring</span><span class="sxs-lookup"><span data-stu-id="08ace-173">string</span></span> | <span data-ttu-id="08ace-174">Igen</span><span class="sxs-lookup"><span data-stu-id="08ace-174">Yes</span></span> | <span data-ttu-id="08ace-175">Egy GUID-formátumú sztring, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="08ace-175">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="08ace-176">start_time</span><span class="sxs-lookup"><span data-stu-id="08ace-176">start_time</span></span> | <span data-ttu-id="08ace-177">sztring (UTC) dátum-idő eltolási formátumban</span><span class="sxs-lookup"><span data-stu-id="08ace-177">string in UTC date-time offset format</span></span> | <span data-ttu-id="08ace-178">Igen</span><span class="sxs-lookup"><span data-stu-id="08ace-178">Yes</span></span> | <span data-ttu-id="08ace-179">Annak az időtartománynak a kezdete, amely a kihasználtság számlázási rendszerben való jelentésének idejét jelöli.</span><span class="sxs-lookup"><span data-stu-id="08ace-179">The start of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="08ace-180">end_time</span><span class="sxs-lookup"><span data-stu-id="08ace-180">end_time</span></span> | <span data-ttu-id="08ace-181">sztring (UTC) dátum-idő eltolási formátumban</span><span class="sxs-lookup"><span data-stu-id="08ace-181">string in UTC date-time offset format</span></span> | <span data-ttu-id="08ace-182">Igen</span><span class="sxs-lookup"><span data-stu-id="08ace-182">Yes</span></span> | <span data-ttu-id="08ace-183">Annak az időtartománynak a vége, amely a kihasználtság számlázási rendszerben való jelentésének idejét jelöli.</span><span class="sxs-lookup"><span data-stu-id="08ace-183">The end of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="08ace-184">Finomsága</span><span class="sxs-lookup"><span data-stu-id="08ace-184">granularity</span></span> | <span data-ttu-id="08ace-185">sztring</span><span class="sxs-lookup"><span data-stu-id="08ace-185">string</span></span> | <span data-ttu-id="08ace-186">No</span><span class="sxs-lookup"><span data-stu-id="08ace-186">No</span></span> | <span data-ttu-id="08ace-187">A használati aggregációk részletességét határozza meg.</span><span class="sxs-lookup"><span data-stu-id="08ace-187">Defines the granularity of usage aggregations.</span></span> <span data-ttu-id="08ace-188">Az elérhető lehetőségek: `daily` (alapértelmezett) és `hourly` .</span><span class="sxs-lookup"><span data-stu-id="08ace-188">Available options are: `daily` (default) and `hourly`.</span></span>
| <span data-ttu-id="08ace-189">show_details</span><span class="sxs-lookup"><span data-stu-id="08ace-189">show_details</span></span> | <span data-ttu-id="08ace-190">boolean</span><span class="sxs-lookup"><span data-stu-id="08ace-190">boolean</span></span> | <span data-ttu-id="08ace-191">Nem</span><span class="sxs-lookup"><span data-stu-id="08ace-191">No</span></span> | <span data-ttu-id="08ace-192">Megadja, hogy a rendszer le tudja-e szerezni a példányszintű használati adatokat.</span><span class="sxs-lookup"><span data-stu-id="08ace-192">Specifies whether to get the instance-level usage details.</span></span> <span data-ttu-id="08ace-193">A mező alapértelmezett értéke: `true`.</span><span class="sxs-lookup"><span data-stu-id="08ace-193">The default is `true`.</span></span> |
| <span data-ttu-id="08ace-194">size</span><span class="sxs-lookup"><span data-stu-id="08ace-194">size</span></span> | <span data-ttu-id="08ace-195">szám</span><span class="sxs-lookup"><span data-stu-id="08ace-195">number</span></span> | <span data-ttu-id="08ace-196">Nem</span><span class="sxs-lookup"><span data-stu-id="08ace-196">No</span></span> | <span data-ttu-id="08ace-197">Az egyetlen API-hívás által visszaadott aggregációk számát adja meg.</span><span class="sxs-lookup"><span data-stu-id="08ace-197">Specifies the number of aggregations returned by a single API call.</span></span> <span data-ttu-id="08ace-198">Az alapértelmezett érték 1000.</span><span class="sxs-lookup"><span data-stu-id="08ace-198">The default is 1000.</span></span> <span data-ttu-id="08ace-199">A maximális érték 1000.</span><span class="sxs-lookup"><span data-stu-id="08ace-199">The max is 1000.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="08ace-200">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="08ace-200">Request headers</span></span>

<span data-ttu-id="08ace-201">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="08ace-201">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="08ace-202">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="08ace-202">Request body</span></span>

<span data-ttu-id="08ace-203">None</span><span class="sxs-lookup"><span data-stu-id="08ace-203">None</span></span>

### <a name="request-example"></a><span data-ttu-id="08ace-204">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="08ace-204">Request example</span></span>

<span data-ttu-id="08ace-205">A következő példakérés a 7/2–8/1 időszakban az egyeztetési fájlhoz hasonló eredményeket ad vissza.</span><span class="sxs-lookup"><span data-stu-id="08ace-205">The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1.</span></span> <span data-ttu-id="08ace-206">Előfordulhat, hogy ezek az eredmények nem egyeznek meg pontosan (a részletekért lásd az [Azure utilization API szakaszt).](#azure-utilization-api)</span><span class="sxs-lookup"><span data-stu-id="08ace-206">These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).</span></span>

<span data-ttu-id="08ace-207">Ez a példakérés a számlázási rendszerben jelentett kihasználtsági adatokat adja vissza 7/2 időpontban (UTC) 12:00-kor (UTC) és 8/2 időpontban(UTC) 12:00-kor.</span><span class="sxs-lookup"><span data-stu-id="08ace-207">This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="08ace-208">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="08ace-208">REST response</span></span>

<span data-ttu-id="08ace-209">Ha a művelet sikeres, ez a metódus az [Azure-beli kihasználtsági](azure-utilization-record-resources.md) rekord erőforrásainak gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="08ace-209">If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body.</span></span> <span data-ttu-id="08ace-210">Ha az Azure-kihasználtsági adatok még nem állnak készen egy függő rendszerben, ez a metódus egy 204-es HTTP-állapotkódot ad vissza egy Retry-After fejléccel.</span><span class="sxs-lookup"><span data-stu-id="08ace-210">If the Azure utilization data isn't yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="08ace-211">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="08ace-211">Response success and error codes</span></span>

<span data-ttu-id="08ace-212">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="08ace-212">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="08ace-213">Egy hálózati nyomkövetési eszközzel olvassa be a HTTP-állapotkódot, a [hibakód típusát](error-codes.md)és a további paramétereket.</span><span class="sxs-lookup"><span data-stu-id="08ace-213">Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="08ace-214">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="08ace-214">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
