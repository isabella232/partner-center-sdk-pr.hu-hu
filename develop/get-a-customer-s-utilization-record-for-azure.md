---
title: Ügyfél Azure-használati rekordjainak lekérése
description: Az Azure-kihasználtság API-val lekérheti az ügyfél Azure-előfizetésének kihasználtsági rekordjait egy adott időszakra vonatkozóan.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bcdeb51b04039fd05b923150c85119385c0537e0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768103"
---
# <a name="get-a-customers-utilization-records-for-azure"></a><span data-ttu-id="f3511-103">Ügyfél Azure-használati rekordjainak lekérése</span><span class="sxs-lookup"><span data-stu-id="f3511-103">Get a customer's utilization records for Azure</span></span>

<span data-ttu-id="f3511-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="f3511-104">**Applies to:**</span></span>

- <span data-ttu-id="f3511-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f3511-105">Partner Center</span></span>
- <span data-ttu-id="f3511-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f3511-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f3511-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f3511-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f3511-108">Az ügyfél Azure-előfizetésének kihasználtsági rekordjait az Azure-kihasználtság API használatával szerezheti be egy adott időszakra vonatkozóan.</span><span class="sxs-lookup"><span data-stu-id="f3511-108">You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3511-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f3511-109">Prerequisites</span></span>

- <span data-ttu-id="f3511-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="f3511-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f3511-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="f3511-111">This scenario supports authentication with both standalone app and App+User credentials.</span></span>

- <span data-ttu-id="f3511-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f3511-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f3511-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="f3511-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f3511-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="f3511-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f3511-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="f3511-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f3511-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="f3511-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f3511-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f3511-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f3511-118">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="f3511-118">A subscription identifier.</span></span>

<span data-ttu-id="f3511-119">Ez az API a napi és óránkénti nem értékelt felhasználást adja vissza egy tetszőleges időtartományra vonatkozóan.</span><span class="sxs-lookup"><span data-stu-id="f3511-119">This API returns daily and hourly unrated consumption for an arbitrary time span.</span></span> <span data-ttu-id="f3511-120">*Ez az API azonban nem támogatott az Azure-csomagokban*.</span><span class="sxs-lookup"><span data-stu-id="f3511-120">However, *this API isn't supported for Azure plans*.</span></span> <span data-ttu-id="f3511-121">Ha rendelkezik Azure-csomaggal, tekintse meg a [számlázás nem számlázott fogyasztási sorok beolvasása](get-invoice-unbilled-consumption-lineitems.md) és a számlázott [felhasználási sorok beolvasása](get-invoice-billed-consumption-lineitems.md) című cikket.</span><span class="sxs-lookup"><span data-stu-id="f3511-121">If you have an Azure plan, see the articles [Get invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead.</span></span> <span data-ttu-id="f3511-122">Ezek a cikkek azt írják le, hogyan lehet a névleges fogyasztást napi szinten, egységenként.</span><span class="sxs-lookup"><span data-stu-id="f3511-122">These articles describe how to get rated consumption at a daily level per meter per resource.</span></span> <span data-ttu-id="f3511-123">Ez a díjszabás megegyezik az Azure-kihasználtsági API által biztosított napi gabona-adatmennyiséggel.</span><span class="sxs-lookup"><span data-stu-id="f3511-123">This rate consumption is equivalent to the daily grain data provided by the Azure utilization API.</span></span> <span data-ttu-id="f3511-124">A számlázott használati adatok beolvasásához a számla azonosítóját kell használnia.</span><span class="sxs-lookup"><span data-stu-id="f3511-124">You'll need to use the invoice identifier to retrieve billed usage data.</span></span> <span data-ttu-id="f3511-125">Vagy a jelenlegi és az előző időszakok használatával lekérheti a nem számlázott használati becsléseket.</span><span class="sxs-lookup"><span data-stu-id="f3511-125">Or, you can use current and previous periods to get unbilled usage estimates.</span></span> <span data-ttu-id="f3511-126">*Az Azure-csomag előfizetési erőforrásai esetében jelenleg nem támogatott az óránkénti adatgabona és az önkényes dátumtartomány-szűrők* használata.</span><span class="sxs-lookup"><span data-stu-id="f3511-126">*Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.</span></span>

## <a name="azure-utilization-api"></a><span data-ttu-id="f3511-127">Azure-kihasználtság API</span><span class="sxs-lookup"><span data-stu-id="f3511-127">Azure utilization API</span></span>

<span data-ttu-id="f3511-128">Ez az Azure-kihasználtsági API hozzáférést biztosít a kihasználtsági rekordokhoz egy olyan időszakra vonatkozóan, amely azt jelzi, hogy a kihasználtság mikor jelent meg a számlázási rendszeren.</span><span class="sxs-lookup"><span data-stu-id="f3511-128">This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system.</span></span> <span data-ttu-id="f3511-129">Hozzáférést biztosít az egyeztetési fájl létrehozásához és kiszámításához használt kihasználtsági adataihoz.</span><span class="sxs-lookup"><span data-stu-id="f3511-129">It provides access to the same utilization data that is used to create and calculate the reconciliation file.</span></span> <span data-ttu-id="f3511-130">Azonban nem ismeri a számlázási rendszerek egyeztetése fájl logikáját.</span><span class="sxs-lookup"><span data-stu-id="f3511-130">However, it does not have knowledge of billing system reconciliation file logic.</span></span> <span data-ttu-id="f3511-131">Nem várhatja el a fájl összefoglalási eredményeinek összeegyeztetését, hogy az adott API-ból beolvasott eredményt pontosan ugyanarra az időszakra kelljen megfeleltetni.</span><span class="sxs-lookup"><span data-stu-id="f3511-131">You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.</span></span>

<span data-ttu-id="f3511-132">A számlázási rendszer például ugyanazokat a kihasználtsági értékeket veszi figyelembe, és a késői szabályok alapján határozza meg, hogy mi történik az egyeztetési fájlban.</span><span class="sxs-lookup"><span data-stu-id="f3511-132">For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file.</span></span> <span data-ttu-id="f3511-133">A számlázási időszak bezárásakor a rendszer a számlázási időszak végéig tartó teljes használatot a megbékélési fájlba kerül.</span><span class="sxs-lookup"><span data-stu-id="f3511-133">When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file.</span></span> <span data-ttu-id="f3511-134">A számlázási időszak végét követő 24 órán belül jelentett időszakon belüli késői használatot a következő egyeztetési fájlban számoljuk el.</span><span class="sxs-lookup"><span data-stu-id="f3511-134">Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file.</span></span> <span data-ttu-id="f3511-135">A partner számlázásával kapcsolatos késői szabályokért lásd: az Azure- [előfizetéshez tartozó felhasználási információk beolvasása](/previous-versions/azure/reference/mt219001(v=azure.100)).</span><span class="sxs-lookup"><span data-stu-id="f3511-135">For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](/previous-versions/azure/reference/mt219001(v=azure.100)).</span></span>

<span data-ttu-id="f3511-136">Ez a REST API lapozható.</span><span class="sxs-lookup"><span data-stu-id="f3511-136">This REST API is paged.</span></span> <span data-ttu-id="f3511-137">Ha a válasz adattartalma nagyobb, mint egyetlen oldal, a következő hivatkozásra kell beolvasni a kihasználtsági rekordok következő oldalát.</span><span class="sxs-lookup"><span data-stu-id="f3511-137">If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.</span></span>

## <a name="c"></a><span data-ttu-id="f3511-138">C\#</span><span class="sxs-lookup"><span data-stu-id="f3511-138">C\#</span></span>

<span data-ttu-id="f3511-139">Az Azure-kihasználtsági rekordok beszerzése:</span><span class="sxs-lookup"><span data-stu-id="f3511-139">To obtain the Azure Utilization Records:</span></span>

1. <span data-ttu-id="f3511-140">Szerezze be az ügyfél-azonosítót és az előfizetés-azonosítót.</span><span class="sxs-lookup"><span data-stu-id="f3511-140">Get the customer ID and subscription ID.</span></span>

2. <span data-ttu-id="f3511-141">Hívja meg a [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) metódust egy olyan [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) visszaadásához, amely tartalmazza a kihasználtsági rekordokat.</span><span class="sxs-lookup"><span data-stu-id="f3511-141">Call the [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records.</span></span>

3. <span data-ttu-id="f3511-142">Szerezze be az Azure-kihasználtsági rekordok enumerálását a kihasználtsági lapok bejárásához.</span><span class="sxs-lookup"><span data-stu-id="f3511-142">Obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span> <span data-ttu-id="f3511-143">Erre a lépésre azért van szükség, mert az erőforrás-gyűjtemény lapozható.</span><span class="sxs-lookup"><span data-stu-id="f3511-143">This step is required, because the resource collection is paged.</span></span>

- <span data-ttu-id="f3511-144">**Minta**: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f3511-144">**Sample**: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="f3511-145">**Projekt**: partner Center SDK-minták</span><span class="sxs-lookup"><span data-stu-id="f3511-145">**Project**: Partner Center SDK Samples</span></span>
- <span data-ttu-id="f3511-146">**Osztály**: GetAzureSubscriptionUtilization.cs</span><span class="sxs-lookup"><span data-stu-id="f3511-146">**Class**: GetAzureSubscriptionUtilization.cs</span></span>

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

## <a name="java"></a><span data-ttu-id="f3511-147">Java</span><span class="sxs-lookup"><span data-stu-id="f3511-147">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="f3511-148">Az Azure-beli kihasználtsági rekordok beszerzéséhez először szüksége lesz egy ügyfél-azonosítóra és egy előfizetés-azonosítóra.</span><span class="sxs-lookup"><span data-stu-id="f3511-148">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="f3511-149">Ezután meghívja a **IAzureUtilizationCollection. Query** függvényt egy olyan **ResourceCollection** visszaküldéséhez, amely tartalmazza a kihasználtsági rekordokat.</span><span class="sxs-lookup"><span data-stu-id="f3511-149">You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records.</span></span> <span data-ttu-id="f3511-150">Mivel az erőforrás-gyűjtemény lapozható, be kell szereznie egy Azure-kihasználtsági rekord enumerálását a kihasználtsági lapok átjárásához.</span><span class="sxs-lookup"><span data-stu-id="f3511-150">Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="f3511-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3511-151">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="f3511-152">Az Azure-beli kihasználtsági rekordok beszerzéséhez először szüksége lesz egy ügyfél-azonosítóra és egy előfizetés-azonosítóra.</span><span class="sxs-lookup"><span data-stu-id="f3511-152">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="f3511-153">Ezután hívja meg a [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span><span class="sxs-lookup"><span data-stu-id="f3511-153">You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span></span> <span data-ttu-id="f3511-154">Ez a parancs a megadott időszakra vonatkozó összes rendelkezésre álló rekordot visszaadja.</span><span class="sxs-lookup"><span data-stu-id="f3511-154">This command will return all records available for the specified period of time.</span></span>

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a><span data-ttu-id="f3511-155">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="f3511-155">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f3511-156">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f3511-156">Request syntax</span></span>

| <span data-ttu-id="f3511-157">Metódus</span><span class="sxs-lookup"><span data-stu-id="f3511-157">Method</span></span> | <span data-ttu-id="f3511-158">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f3511-158">Request URI</span></span> |
|------- | ----------- |
| <span data-ttu-id="f3511-159">**GET**</span><span class="sxs-lookup"><span data-stu-id="f3511-159">**GET**</span></span> | <span data-ttu-id="f3511-160">*{baseURL}*/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/utilizations/Azure? kezdési \_ idő = {kezdő időpont} &befejezési \_ idő = {befejezési idő} &részletesség = {részletesség} &show \_ details = {True}</span><span class="sxs-lookup"><span data-stu-id="f3511-160">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="f3511-161">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="f3511-161">URI parameters</span></span>

<span data-ttu-id="f3511-162">A kihasználtsági rekordok beszerzéséhez használja a következő elérési utat és a lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="f3511-162">Use the following path and query parameters to get the utilization records.</span></span>

| <span data-ttu-id="f3511-163">Név</span><span class="sxs-lookup"><span data-stu-id="f3511-163">Name</span></span> | <span data-ttu-id="f3511-164">Típus</span><span class="sxs-lookup"><span data-stu-id="f3511-164">Type</span></span> | <span data-ttu-id="f3511-165">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f3511-165">Required</span></span> | <span data-ttu-id="f3511-166">Leírás</span><span class="sxs-lookup"><span data-stu-id="f3511-166">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="f3511-167">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="f3511-167">customer-tenant-id</span></span> | <span data-ttu-id="f3511-168">sztring</span><span class="sxs-lookup"><span data-stu-id="f3511-168">string</span></span> | <span data-ttu-id="f3511-169">Igen</span><span class="sxs-lookup"><span data-stu-id="f3511-169">Yes</span></span> | <span data-ttu-id="f3511-170">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="f3511-170">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="f3511-171">előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="f3511-171">subscription-id</span></span> | <span data-ttu-id="f3511-172">sztring</span><span class="sxs-lookup"><span data-stu-id="f3511-172">string</span></span> | <span data-ttu-id="f3511-173">Igen</span><span class="sxs-lookup"><span data-stu-id="f3511-173">Yes</span></span> | <span data-ttu-id="f3511-174">Egy GUID-formázott karakterlánc, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="f3511-174">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="f3511-175">start_time</span><span class="sxs-lookup"><span data-stu-id="f3511-175">start_time</span></span> | <span data-ttu-id="f3511-176">karakterlánc UTC dátum-idő eltolási formátumban</span><span class="sxs-lookup"><span data-stu-id="f3511-176">string in UTC date-time offset format</span></span> | <span data-ttu-id="f3511-177">Igen</span><span class="sxs-lookup"><span data-stu-id="f3511-177">Yes</span></span> | <span data-ttu-id="f3511-178">Annak az időtartománynak a kezdete, amely akkor jelenik meg, amikor a rendszer a kihasználtságot a számlázási rendszeren mutatja be.</span><span class="sxs-lookup"><span data-stu-id="f3511-178">The start of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="f3511-179">end_time</span><span class="sxs-lookup"><span data-stu-id="f3511-179">end_time</span></span> | <span data-ttu-id="f3511-180">karakterlánc UTC dátum-idő eltolási formátumban</span><span class="sxs-lookup"><span data-stu-id="f3511-180">string in UTC date-time offset format</span></span> | <span data-ttu-id="f3511-181">Igen</span><span class="sxs-lookup"><span data-stu-id="f3511-181">Yes</span></span> | <span data-ttu-id="f3511-182">Annak az időtartománynak a vége, amely akkor jelenik meg, amikor a rendszer a kihasználtságot a számlázási rendszeren mutatja be.</span><span class="sxs-lookup"><span data-stu-id="f3511-182">The end of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="f3511-183">granularitása</span><span class="sxs-lookup"><span data-stu-id="f3511-183">granularity</span></span> | <span data-ttu-id="f3511-184">sztring</span><span class="sxs-lookup"><span data-stu-id="f3511-184">string</span></span> | <span data-ttu-id="f3511-185">No</span><span class="sxs-lookup"><span data-stu-id="f3511-185">No</span></span> | <span data-ttu-id="f3511-186">Meghatározza a használati összesítések részletességét.</span><span class="sxs-lookup"><span data-stu-id="f3511-186">Defines the granularity of usage aggregations.</span></span> <span data-ttu-id="f3511-187">Az elérhető lehetőségek a következők: `daily` (alapértelmezett) és `hourly` .</span><span class="sxs-lookup"><span data-stu-id="f3511-187">Available options are: `daily` (default) and `hourly`.</span></span>
| <span data-ttu-id="f3511-188">show_details</span><span class="sxs-lookup"><span data-stu-id="f3511-188">show_details</span></span> | <span data-ttu-id="f3511-189">boolean</span><span class="sxs-lookup"><span data-stu-id="f3511-189">boolean</span></span> | <span data-ttu-id="f3511-190">Nem</span><span class="sxs-lookup"><span data-stu-id="f3511-190">No</span></span> | <span data-ttu-id="f3511-191">Megadja, hogy a példány-szintű használat részleteit kívánja-e lekérni.</span><span class="sxs-lookup"><span data-stu-id="f3511-191">Specifies whether to get the instance-level usage details.</span></span> <span data-ttu-id="f3511-192">A mező alapértelmezett értéke: `true`.</span><span class="sxs-lookup"><span data-stu-id="f3511-192">The default is `true`.</span></span> |
| <span data-ttu-id="f3511-193">size</span><span class="sxs-lookup"><span data-stu-id="f3511-193">size</span></span> | <span data-ttu-id="f3511-194">szám</span><span class="sxs-lookup"><span data-stu-id="f3511-194">number</span></span> | <span data-ttu-id="f3511-195">Nem</span><span class="sxs-lookup"><span data-stu-id="f3511-195">No</span></span> | <span data-ttu-id="f3511-196">Egy API-hívás által visszaadott összesítések számát adja meg.</span><span class="sxs-lookup"><span data-stu-id="f3511-196">Specifies the number of aggregations returned by a single API call.</span></span> <span data-ttu-id="f3511-197">Az alapértelmezett érték 1000.</span><span class="sxs-lookup"><span data-stu-id="f3511-197">The default is 1000.</span></span> <span data-ttu-id="f3511-198">A max 1000.</span><span class="sxs-lookup"><span data-stu-id="f3511-198">The max is 1000.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f3511-199">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f3511-199">Request headers</span></span>

<span data-ttu-id="f3511-200">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f3511-200">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f3511-201">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f3511-201">Request body</span></span>

<span data-ttu-id="f3511-202">Nincs</span><span class="sxs-lookup"><span data-stu-id="f3511-202">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f3511-203">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f3511-203">Request example</span></span>

<span data-ttu-id="f3511-204">Az alábbi példában szereplő kérelem olyan eredményeket hoz létre, amelyek a 7/2-8/1-as időszakra vonatkozó, a megbékélési fájlhoz hasonlóan jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="f3511-204">The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1.</span></span> <span data-ttu-id="f3511-205">Előfordulhat, hogy ezek az eredmények nem egyeznek pontosan (lásd a részleteket az [Azure kihasználtsági API](#azure-utilization-api) szakaszban).</span><span class="sxs-lookup"><span data-stu-id="f3511-205">These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).</span></span>

<span data-ttu-id="f3511-206">Ez a példa a számlázási rendszeren jelentett kihasználtsági adatok visszaküldése 12 órakor (UTC) és 8/2 (UTC) 7/2.</span><span class="sxs-lookup"><span data-stu-id="f3511-206">This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f3511-207">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f3511-207">REST response</span></span>

<span data-ttu-id="f3511-208">Ha ez sikeres, ez a metódus az [Azure kihasználtsági rekord](azure-utilization-record-resources.md) erőforrásainak gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="f3511-208">If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body.</span></span> <span data-ttu-id="f3511-209">Ha az Azure-beli kihasználtsági adatok még nem állnak készen egy függő rendszerbe, ez a metódus egy 204-as HTTP-állapotkódot ad vissza Retry-After fejléccel.</span><span class="sxs-lookup"><span data-stu-id="f3511-209">If the Azure utilization data isn't yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f3511-210">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f3511-210">Response success and error codes</span></span>

<span data-ttu-id="f3511-211">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="f3511-211">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f3511-212">Hálózati nyomkövetési eszközzel olvassa be a HTTP-állapotkódot, a [hibakód típusát](error-codes.md)és a további paramétereket.</span><span class="sxs-lookup"><span data-stu-id="f3511-212">Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="f3511-213">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f3511-213">Response example</span></span>

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
