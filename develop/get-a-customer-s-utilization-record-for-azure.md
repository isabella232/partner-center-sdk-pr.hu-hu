---
title: Ügyfél Azure-használati rekordjainak lekérése
description: Az Azure utilization API használatával lekérte egy ügyfél Azure-előfizetésének kihasználtsági rekordjait egy adott időszakra.
ms.date: 04/19/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23c8d18462081c6d6c95c1d969f269cbb3f8754b
ms.sourcegitcommit: abefe11421edc421491f14b257b2408b4f29b669
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/20/2021
ms.locfileid: "107745592"
---
# <a name="get-a-customers-utilization-records-for-azure"></a><span data-ttu-id="188e8-103">Ügyfél Azure-használati rekordjainak lekérése</span><span class="sxs-lookup"><span data-stu-id="188e8-103">Get a customer's utilization records for Azure</span></span>

<span data-ttu-id="188e8-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="188e8-104">**Applies to:**</span></span>

- <span data-ttu-id="188e8-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="188e8-105">Partner Center</span></span>
- <span data-ttu-id="188e8-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="188e8-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="188e8-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="188e8-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="188e8-108">Az ügyfél Azure-előfizetésének kihasználtsági rekordjait egy adott időszakra az Azure utilization API használatával kaphatja meg.</span><span class="sxs-lookup"><span data-stu-id="188e8-108">You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="188e8-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="188e8-109">Prerequisites</span></span>

- <span data-ttu-id="188e8-110">A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="188e8-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="188e8-111">Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="188e8-111">This scenario supports authentication with both standalone app and App+User credentials.</span></span>

- <span data-ttu-id="188e8-112">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="188e8-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="188e8-113">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="188e8-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="188e8-114">Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="188e8-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="188e8-115">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="188e8-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="188e8-116">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="188e8-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="188e8-117">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="188e8-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="188e8-118">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="188e8-118">A subscription identifier.</span></span>

<span data-ttu-id="188e8-119">Ez az API egy tetszőleges időtartamra napi és óránkénti, nem egységes használatot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="188e8-119">This API returns daily and hourly unrated consumption for an arbitrary time span.</span></span> <span data-ttu-id="188e8-120">Ez az API azonban nem támogatott az *Azure-csomagokhoz.*</span><span class="sxs-lookup"><span data-stu-id="188e8-120">However, *this API isn't supported for Azure plans*.</span></span> <span data-ttu-id="188e8-121">Ha már van [Azure-csomagja,](get-invoice-unbilled-consumption-lineitems.md) tekintse meg a számla [](get-invoice-billed-consumption-lineitems.md) nem számlázott használatú sorelemeket és a számlázott használatú sorok cikkeit.</span><span class="sxs-lookup"><span data-stu-id="188e8-121">If you have an Azure plan, see the articles [Get invoice un-billed consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead.</span></span> <span data-ttu-id="188e8-122">Ezek a cikkek azt ismertetik, hogyan lehet mérőnként napi szinten lekért névleges fogyasztást erőforrásonként.</span><span class="sxs-lookup"><span data-stu-id="188e8-122">These articles describe how to get rated consumption at a daily level per meter per resource.</span></span> <span data-ttu-id="188e8-123">Ez a díjfelhasználás megegyezik az Azure utilization API által biztosított napi rendszerességgel kapcsolatos adatokkal.</span><span class="sxs-lookup"><span data-stu-id="188e8-123">This rate consumption is equivalent to the daily grain data provided by the Azure utilization API.</span></span> <span data-ttu-id="188e8-124">A számlázott használati adatok lekéréséhez a számlaazonosítót kell használnia.</span><span class="sxs-lookup"><span data-stu-id="188e8-124">You'll need to use the invoice identifier to retrieve billed usage data.</span></span> <span data-ttu-id="188e8-125">Az aktuális és az előző időszakokkal is lekért használati becsléseket kaphat.</span><span class="sxs-lookup"><span data-stu-id="188e8-125">Or, you can use current and previous periods to get un-billed usage estimates.</span></span> <span data-ttu-id="188e8-126">Az óránkénti adat- és tetszőleges dátumtartomány-szűrők jelenleg nem támogatottak az *Azure-csomag előfizetési erőforrásaihoz.*</span><span class="sxs-lookup"><span data-stu-id="188e8-126">*Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.</span></span>

## <a name="azure-utilization-api"></a><span data-ttu-id="188e8-127">Azure-kihasználtsági API</span><span class="sxs-lookup"><span data-stu-id="188e8-127">Azure utilization API</span></span>

<span data-ttu-id="188e8-128">Ez az Azure-beli kihasználtsági API hozzáférést biztosít a kihasználtsági rekordokhoz egy olyan időszakra vonatkozóan, amely azt jelzi, hogy mikor jelentték a kihasználtságot a számlázási rendszerben.</span><span class="sxs-lookup"><span data-stu-id="188e8-128">This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system.</span></span> <span data-ttu-id="188e8-129">Hozzáférést biztosít ugyanazokhoz a kihasználtsági adatokhoz, amelyek az egyeztetési fájl létrehozásához és kiszámításához használatosak.</span><span class="sxs-lookup"><span data-stu-id="188e8-129">It provides access to the same utilization data that is used to create and calculate the reconciliation file.</span></span> <span data-ttu-id="188e8-130">Nem ismeri azonban a számlázási rendszer egyeztetési fájllogikát.</span><span class="sxs-lookup"><span data-stu-id="188e8-130">However, it does not have knowledge of billing system reconciliation file logic.</span></span> <span data-ttu-id="188e8-131">Az egyeztetési fájl összegzési eredményei várhatóan nem egyeznek meg az API-ból pontosan ugyanabban az időszakban lekért eredményekkel.</span><span class="sxs-lookup"><span data-stu-id="188e8-131">You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.</span></span>

<span data-ttu-id="188e8-132">A számlázási rendszer például ugyanezeket a kihasználtsági adatokat alkalmazza, és késési szabályokat alkalmaz annak megállapításához, hogy mit kell figyelembe vennie egy egyeztetési fájlban.</span><span class="sxs-lookup"><span data-stu-id="188e8-132">For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file.</span></span> <span data-ttu-id="188e8-133">Ha egy számlázási időszak véget ér, az egyeztetési fájl tartalmazza a számlázási időszak végét elvégő teljes használatot.</span><span class="sxs-lookup"><span data-stu-id="188e8-133">When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file.</span></span> <span data-ttu-id="188e8-134">A számlázási időszakon belül a számlázási időszak vége után 24 órán belül jelentett minden kései használatot a következő egyeztetési fájlban kell figyelembe venni.</span><span class="sxs-lookup"><span data-stu-id="188e8-134">Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file.</span></span> <span data-ttu-id="188e8-135">A partner számlázásának késési szabályaiért lásd: [Azure-előfizetés fogyasztási adatainak lekérte.](/previous-versions/azure/reference/mt219001(v=azure.100))</span><span class="sxs-lookup"><span data-stu-id="188e8-135">For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](/previous-versions/azure/reference/mt219001(v=azure.100)).</span></span>

<span data-ttu-id="188e8-136">Ez REST API lapra van ásva.</span><span class="sxs-lookup"><span data-stu-id="188e8-136">This REST API is paged.</span></span> <span data-ttu-id="188e8-137">Ha a válasz hasznos adatai nagyobbak egyetlen lapnál, a következő hivatkozásra kattintva le kell töltenie a kihasználtsági rekordok következő lapját.</span><span class="sxs-lookup"><span data-stu-id="188e8-137">If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.</span></span>

### <a name="scenario--partner-a-has-transferred-billing-ownership-of-azure-legacy-subscription-145p-to-partner-b"></a><span data-ttu-id="188e8-138">Forgatókönyv: Az A partner átvitte az Örökölt Azure-előfizetés (145P) számlázási tulajdonjogát a B partnernek</span><span class="sxs-lookup"><span data-stu-id="188e8-138">Scenario : Partner A has transferred billing ownership of Azure Legacy Subscription (145P) to Partner B</span></span>

<span data-ttu-id="188e8-139">Ha egy partner egy örökölt Azure-előfizetés számlázási tulajdonjogát átadja egy másik partnernek, amikor az új partner a Utilization API-t hívja meg az átvitt előfizetéshez, akkor az Azure-jogosultságazonosító helyett a Kereskedelmi előfizetés azonosítóját (amely az Partnerközpont-fiókjában jelenik meg) kell használnia.</span><span class="sxs-lookup"><span data-stu-id="188e8-139">If a partner transfers billing ownership of an Azure legacy subscription to another partner, when new the new partner calls Utilization API for transferred subscription they have to use Commerce Subscription ID (which shows up in their Partner Center account) rather than the Azure Entitlement ID.</span></span> <span data-ttu-id="188e8-140">Az Azure-jogosultságazonosító csak akkor jelenik meg a B partnernél, ha rendszergazda (AOBO) az ügyfél Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="188e8-140">Azure Entitlement ID appears for Partner B only when they are Admin on behalf of (AOBO) to Customer's Azure portal.</span></span> 

<span data-ttu-id="188e8-141">Az átvitt előfizetés Utilization API-jának sikeres hívásához az új partnernek a Kereskedelmi előfizetés azonosítóját kell használnia.</span><span class="sxs-lookup"><span data-stu-id="188e8-141">To successfully call the Utilization API for the transferred subscription, the new partner needs to use the Commerce Subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="188e8-142">C\#</span><span class="sxs-lookup"><span data-stu-id="188e8-142">C\#</span></span>

<span data-ttu-id="188e8-143">Az Azure-beli kihasználtsági rekordok beszerzése:</span><span class="sxs-lookup"><span data-stu-id="188e8-143">To obtain the Azure Utilization Records:</span></span>

1. <span data-ttu-id="188e8-144">Szerezze be az ügyfél-azonosítót és az előfizetés-azonosítót.</span><span class="sxs-lookup"><span data-stu-id="188e8-144">Get the customer ID and subscription ID.</span></span>

2. <span data-ttu-id="188e8-145">Hívja meg az [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) metódust a kihasználtsági rekordokat tartalmazó [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) visszaadása érdekében.</span><span class="sxs-lookup"><span data-stu-id="188e8-145">Call the [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records.</span></span>

3. <span data-ttu-id="188e8-146">Szerezzen be egy Azure-beli kihasználtságirekord-enumerátort a kihasználtsági lapok bejárására.</span><span class="sxs-lookup"><span data-stu-id="188e8-146">Obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span> <span data-ttu-id="188e8-147">Erre a lépésre azért van szükség, mert az erőforrás-gyűjtemény lapszám van meglaposodva.</span><span class="sxs-lookup"><span data-stu-id="188e8-147">This step is required, because the resource collection is paged.</span></span>

- <span data-ttu-id="188e8-148">**Minta:** [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="188e8-148">**Sample**: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="188e8-149">**Projekt:** Partnerközpont SDK minták</span><span class="sxs-lookup"><span data-stu-id="188e8-149">**Project**: Partner Center SDK Samples</span></span>
- <span data-ttu-id="188e8-150">**Osztály:** GetAzureSubscriptionUtilization.cs</span><span class="sxs-lookup"><span data-stu-id="188e8-150">**Class**: GetAzureSubscriptionUtilization.cs</span></span>

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

## <a name="java"></a><span data-ttu-id="188e8-151">Java</span><span class="sxs-lookup"><span data-stu-id="188e8-151">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="188e8-152">Az Azure-beli kihasználtsági rekordok beszerzéséhez először egy ügyfél-azonosítóra és egy előfizetés-azonosítóra van szükség.</span><span class="sxs-lookup"><span data-stu-id="188e8-152">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="188e8-153">Ezután meg kell hívnia az **IAzureUtilizationCollection.query** függvényt, hogy visszaadja a kihasználtsági rekordokat tartalmazó **ResourceCollection** adatokat.</span><span class="sxs-lookup"><span data-stu-id="188e8-153">You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records.</span></span> <span data-ttu-id="188e8-154">Mivel az erőforrás-gyűjtemény lapozódva van, be kell szereznie egy Azure-beli kihasználtságirekord-enumerátort a kihasználtsági oldalakon való áthaladáshoz.</span><span class="sxs-lookup"><span data-stu-id="188e8-154">Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="188e8-155">PowerShell</span><span class="sxs-lookup"><span data-stu-id="188e8-155">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="188e8-156">Az Azure-beli kihasználtsági rekordok beszerzéséhez először egy ügyfél-azonosítóra és egy előfizetés-azonosítóra van szükség.</span><span class="sxs-lookup"><span data-stu-id="188e8-156">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="188e8-157">Ezután hívja meg a [**Get-PartnerCustomerSubscriptionUtilization függvényt.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md)</span><span class="sxs-lookup"><span data-stu-id="188e8-157">You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span></span> <span data-ttu-id="188e8-158">Ez a parancs a megadott időszakban elérhető összes rekordot visszaadja.</span><span class="sxs-lookup"><span data-stu-id="188e8-158">This command will return all records available for the specified period of time.</span></span>

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a><span data-ttu-id="188e8-159">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="188e8-159">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="188e8-160">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="188e8-160">Request syntax</span></span>

| <span data-ttu-id="188e8-161">Metódus</span><span class="sxs-lookup"><span data-stu-id="188e8-161">Method</span></span> | <span data-ttu-id="188e8-162">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="188e8-162">Request URI</span></span> |
|------- | ----------- |
| <span data-ttu-id="188e8-163">**Kap**</span><span class="sxs-lookup"><span data-stu-id="188e8-163">**GET**</span></span> | <span data-ttu-id="188e8-164">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/utilizations/azure?start \_ time={start-time}&\_ end-time={end-time}&granularity={granularity}&show \_ details={True}</span><span class="sxs-lookup"><span data-stu-id="188e8-164">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="188e8-165">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="188e8-165">URI parameters</span></span>

<span data-ttu-id="188e8-166">Az alábbi elérési út és lekérdezési paraméterek használatával lekérdezheti a kihasználtsági rekordokat.</span><span class="sxs-lookup"><span data-stu-id="188e8-166">Use the following path and query parameters to get the utilization records.</span></span>

| <span data-ttu-id="188e8-167">Név</span><span class="sxs-lookup"><span data-stu-id="188e8-167">Name</span></span> | <span data-ttu-id="188e8-168">Típus</span><span class="sxs-lookup"><span data-stu-id="188e8-168">Type</span></span> | <span data-ttu-id="188e8-169">Kötelező</span><span class="sxs-lookup"><span data-stu-id="188e8-169">Required</span></span> | <span data-ttu-id="188e8-170">Leírás</span><span class="sxs-lookup"><span data-stu-id="188e8-170">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="188e8-171">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="188e8-171">customer-tenant-id</span></span> | <span data-ttu-id="188e8-172">sztring</span><span class="sxs-lookup"><span data-stu-id="188e8-172">string</span></span> | <span data-ttu-id="188e8-173">Yes</span><span class="sxs-lookup"><span data-stu-id="188e8-173">Yes</span></span> | <span data-ttu-id="188e8-174">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="188e8-174">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="188e8-175">subscription-id</span><span class="sxs-lookup"><span data-stu-id="188e8-175">subscription-id</span></span> | <span data-ttu-id="188e8-176">sztring</span><span class="sxs-lookup"><span data-stu-id="188e8-176">string</span></span> | <span data-ttu-id="188e8-177">Yes</span><span class="sxs-lookup"><span data-stu-id="188e8-177">Yes</span></span> | <span data-ttu-id="188e8-178">Egy GUID-formátumú sztring, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="188e8-178">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="188e8-179">start_time</span><span class="sxs-lookup"><span data-stu-id="188e8-179">start_time</span></span> | <span data-ttu-id="188e8-180">sztring UTC dátum-idő eltolási formátumban</span><span class="sxs-lookup"><span data-stu-id="188e8-180">string in UTC date-time offset format</span></span> | <span data-ttu-id="188e8-181">Yes</span><span class="sxs-lookup"><span data-stu-id="188e8-181">Yes</span></span> | <span data-ttu-id="188e8-182">Annak az időtartománynak a kezdete, amely a kihasználtság számlázási rendszerben való jelentésének idejét jelöli.</span><span class="sxs-lookup"><span data-stu-id="188e8-182">The start of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="188e8-183">end_time</span><span class="sxs-lookup"><span data-stu-id="188e8-183">end_time</span></span> | <span data-ttu-id="188e8-184">sztring UTC dátum-idő eltolási formátumban</span><span class="sxs-lookup"><span data-stu-id="188e8-184">string in UTC date-time offset format</span></span> | <span data-ttu-id="188e8-185">Yes</span><span class="sxs-lookup"><span data-stu-id="188e8-185">Yes</span></span> | <span data-ttu-id="188e8-186">Annak az időtartománynak a vége, amely a kihasználtság számlázási rendszerben való jelentésének idejét jelöli.</span><span class="sxs-lookup"><span data-stu-id="188e8-186">The end of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="188e8-187">Finomsága</span><span class="sxs-lookup"><span data-stu-id="188e8-187">granularity</span></span> | <span data-ttu-id="188e8-188">sztring</span><span class="sxs-lookup"><span data-stu-id="188e8-188">string</span></span> | <span data-ttu-id="188e8-189">No</span><span class="sxs-lookup"><span data-stu-id="188e8-189">No</span></span> | <span data-ttu-id="188e8-190">Meghatározza a használati aggregációk részletességét.</span><span class="sxs-lookup"><span data-stu-id="188e8-190">Defines the granularity of usage aggregations.</span></span> <span data-ttu-id="188e8-191">Az elérhető lehetőségek: `daily` (alapértelmezett) és `hourly` .</span><span class="sxs-lookup"><span data-stu-id="188e8-191">Available options are: `daily` (default) and `hourly`.</span></span>
| <span data-ttu-id="188e8-192">show_details</span><span class="sxs-lookup"><span data-stu-id="188e8-192">show_details</span></span> | <span data-ttu-id="188e8-193">boolean</span><span class="sxs-lookup"><span data-stu-id="188e8-193">boolean</span></span> | <span data-ttu-id="188e8-194">No</span><span class="sxs-lookup"><span data-stu-id="188e8-194">No</span></span> | <span data-ttu-id="188e8-195">Megadja, hogy a rendszer le tudja-e szerezni a példányszintű használati adatokat.</span><span class="sxs-lookup"><span data-stu-id="188e8-195">Specifies whether to get the instance-level usage details.</span></span> <span data-ttu-id="188e8-196">A mező alapértelmezett értéke: `true`.</span><span class="sxs-lookup"><span data-stu-id="188e8-196">The default is `true`.</span></span> |
| <span data-ttu-id="188e8-197">size</span><span class="sxs-lookup"><span data-stu-id="188e8-197">size</span></span> | <span data-ttu-id="188e8-198">szám</span><span class="sxs-lookup"><span data-stu-id="188e8-198">number</span></span> | <span data-ttu-id="188e8-199">No</span><span class="sxs-lookup"><span data-stu-id="188e8-199">No</span></span> | <span data-ttu-id="188e8-200">Az egyetlen API-hívás által visszaadott aggregációk számát adja meg.</span><span class="sxs-lookup"><span data-stu-id="188e8-200">Specifies the number of aggregations returned by a single API call.</span></span> <span data-ttu-id="188e8-201">Az alapértelmezett érték 1000.</span><span class="sxs-lookup"><span data-stu-id="188e8-201">The default is 1000.</span></span> <span data-ttu-id="188e8-202">A maximális érték 1000.</span><span class="sxs-lookup"><span data-stu-id="188e8-202">The max is 1000.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="188e8-203">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="188e8-203">Request headers</span></span>

<span data-ttu-id="188e8-204">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="188e8-204">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="188e8-205">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="188e8-205">Request body</span></span>

<span data-ttu-id="188e8-206">Nincsenek</span><span class="sxs-lookup"><span data-stu-id="188e8-206">None</span></span>

### <a name="request-example"></a><span data-ttu-id="188e8-207">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="188e8-207">Request example</span></span>

<span data-ttu-id="188e8-208">A következő példakérés a 7/2–8/1 időszakban az egyeztetési fájlhoz hasonló eredményeket ad vissza.</span><span class="sxs-lookup"><span data-stu-id="188e8-208">The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1.</span></span> <span data-ttu-id="188e8-209">Előfordulhat, hogy ezek az eredmények nem egyeznek meg pontosan (a részletekért lásd az [Azure utilization API szakaszt).](#azure-utilization-api)</span><span class="sxs-lookup"><span data-stu-id="188e8-209">These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).</span></span>

<span data-ttu-id="188e8-210">Ez a példakérés a számlázási rendszerben jelentett kihasználtsági adatokat adja vissza 7/2 időpontban (UTC) 12:00-kor (UTC) és 8/2 időpontban(UTC) 12:00-kor.</span><span class="sxs-lookup"><span data-stu-id="188e8-210">This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="188e8-211">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="188e8-211">REST response</span></span>

<span data-ttu-id="188e8-212">Ha a művelet sikeres, ez a metódus az [Azure-beli kihasználtsági](azure-utilization-record-resources.md) rekord erőforrásainak gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="188e8-212">If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body.</span></span> <span data-ttu-id="188e8-213">Ha az Azure-kihasználtsági adatok még nem állnak készen egy függő rendszerben, ez a metódus egy 204-es HTTP-állapotkódot ad vissza egy Retry-After fejléccel.</span><span class="sxs-lookup"><span data-stu-id="188e8-213">If the Azure utilization data isn't yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="188e8-214">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="188e8-214">Response success and error codes</span></span>

<span data-ttu-id="188e8-215">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="188e8-215">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="188e8-216">Egy hálózati nyomkövetési eszközzel olvassa be a HTTP-állapotkódot, a [hibakód típusát](error-codes.md)és a további paramétereket.</span><span class="sxs-lookup"><span data-stu-id="188e8-216">Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="188e8-217">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="188e8-217">Response example</span></span>

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
