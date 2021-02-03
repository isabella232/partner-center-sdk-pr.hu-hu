---
title: Partnerközpont-tevékenység rekordjának lekérése
description: Műveletek rekordjának lekérése egy partner felhasználó vagy alkalmazás által egy adott időszakban.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2f37eae8bb96c1c1e7008e8c566b085e25d8807d
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768228"
---
# <a name="get-a-record-of-partner-center-activity"></a><span data-ttu-id="d39b1-103">Partnerközpont-tevékenység rekordjának lekérése</span><span class="sxs-lookup"><span data-stu-id="d39b1-103">Get a record of Partner Center activity</span></span>

<span data-ttu-id="d39b1-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="d39b1-104">**Applies To**</span></span>

- <span data-ttu-id="d39b1-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="d39b1-105">Partner Center</span></span>
- <span data-ttu-id="d39b1-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="d39b1-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d39b1-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="d39b1-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d39b1-108">Ez a cikk azt ismerteti, hogyan kérhető le olyan műveletek rekordja, amelyeket egy adott időtartamon belül egy partner felhasználó vagy alkalmazás hajtott végre.</span><span class="sxs-lookup"><span data-stu-id="d39b1-108">This article describes how to retrieve a record of operations that was performed by a partner user or application over a period of time.</span></span>

<span data-ttu-id="d39b1-109">Ezzel az API-val lekérheti az előző 30 nap naplózási rekordjait az aktuális dátumból, illetve a Kezdődátum és/vagy a befejezési dátummal megadott dátumtartományt.</span><span class="sxs-lookup"><span data-stu-id="d39b1-109">Use this API to retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="d39b1-110">Vegye figyelembe azonban, hogy a teljesítmény miatt a tevékenység naplójának adatelérhetősége az előző 90 napra korlátozódik.</span><span class="sxs-lookup"><span data-stu-id="d39b1-110">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="d39b1-111">Az aktuális dátum előtt 90 nappal nagyobb kezdési dátummal rendelkező kérések esetén a rendszer rossz kérési kivételt (hibakód: 400) és megfelelő üzenetet kap.</span><span class="sxs-lookup"><span data-stu-id="d39b1-111">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d39b1-112">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d39b1-112">Prerequisites</span></span>

- <span data-ttu-id="d39b1-113">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="d39b1-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d39b1-114">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="d39b1-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d39b1-115">C\#</span><span class="sxs-lookup"><span data-stu-id="d39b1-115">C\#</span></span>

<span data-ttu-id="d39b1-116">A partner Center-műveletek rekordjának lekéréséhez először hozza létre a lekérdezni kívánt rekordok dátumtartományt.</span><span class="sxs-lookup"><span data-stu-id="d39b1-116">To retrieve a record of Partner Center operations, first establish the date range for the records you want to retrieve.</span></span> <span data-ttu-id="d39b1-117">A következő példa csak kezdő dátumot használ, de a befejezési dátumot is megadhatja.</span><span class="sxs-lookup"><span data-stu-id="d39b1-117">The following code example only uses a start date, but you can also include an end date.</span></span> <span data-ttu-id="d39b1-118">További információ: [**lekérdezési**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) módszer.</span><span class="sxs-lookup"><span data-stu-id="d39b1-118">For more information, see the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) method.</span></span> <span data-ttu-id="d39b1-119">Ezután hozza létre a szükséges változókat az alkalmazni kívánt szűrő típusához, és rendelje hozzá a megfelelő értékeket.</span><span class="sxs-lookup"><span data-stu-id="d39b1-119">Next, create the variables you need for the type of filter you want to apply, and assign the appropriate values.</span></span> <span data-ttu-id="d39b1-120">Ha például a vállalat neve alsztring alapján szeretne szűrni, hozzon létre egy változót az alsztring tárolásához.</span><span class="sxs-lookup"><span data-stu-id="d39b1-120">For example, to filter by company name substring, create a variable to hold the substring.</span></span> <span data-ttu-id="d39b1-121">Az ügyfél-azonosító alapján történő szűréshez hozzon létre egy változót az azonosító tárolásához.</span><span class="sxs-lookup"><span data-stu-id="d39b1-121">To filter by customer ID, create a variable to hold the ID.</span></span>

<span data-ttu-id="d39b1-122">A következő példában a rendszer minta kódot biztosít a vállalat neve alsztring, az ügyfél azonosítója vagy az erőforrástípus alapján történő szűréshez.</span><span class="sxs-lookup"><span data-stu-id="d39b1-122">In the following example, sample code is provided to filter by a company name substring, customer ID, or resource type.</span></span> <span data-ttu-id="d39b1-123">Válassza ki az egyiket, és véleményezze a többiet.</span><span class="sxs-lookup"><span data-stu-id="d39b1-123">Choose one and comment out the others.</span></span> <span data-ttu-id="d39b1-124">Minden esetben először hozzon létre egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumot az alapértelmezett [**konstruktor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) használatával a szűrő létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="d39b1-124">In each case, you first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object using its default [**constructor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) to create the filter.</span></span> <span data-ttu-id="d39b1-125">Meg kell adnia egy karakterláncot, amely a keresendő mezőt tartalmazza, és a megfelelő operátort kell alkalmaznia, ahogy az látható.</span><span class="sxs-lookup"><span data-stu-id="d39b1-125">You'll need to pass a string that contains the field to search, and the appropriate operator to apply, as shown.</span></span> <span data-ttu-id="d39b1-126">Meg kell adnia a szűréshez használandó karakterláncot is.</span><span class="sxs-lookup"><span data-stu-id="d39b1-126">You also must provide the string to filter by.</span></span>

<span data-ttu-id="d39b1-127">Ezután a [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) tulajdonsággal szerezzen be egy felületet a rekordok naplózásához, és hívja meg a [**lekérdezés**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) vagy a [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) metódust a szűrő végrehajtásához és az eredmény első oldalát ábrázoló [**AuditRecord**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="d39b1-127">Next, use the [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) property to get an interface to audit record operations, and call the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) method to execute the filter and get the collection of [**AuditRecord's**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) that represent the first page of the result.</span></span> <span data-ttu-id="d39b1-128">Adja át a metódust a kezdő dátumnak, az itt látható példában nem használt nem kötelező befejezési dátumnak, valamint egy entitásra vonatkozó lekérdezést jelölő [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) objektumnak.</span><span class="sxs-lookup"><span data-stu-id="d39b1-128">Pass the method the start date, an optional end date not used in the example here, and an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object that represents a query on an entity.</span></span> <span data-ttu-id="d39b1-129">A IQuery objektum létrehozása a fent létrehozott szűrőnek a [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódusba való átadásával történik.</span><span class="sxs-lookup"><span data-stu-id="d39b1-129">The IQuery object is created by passing the filter created above to the [**QueryFactory's**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method.</span></span>

<span data-ttu-id="d39b1-130">Miután megtörtént az elemek kezdeti lapja, használja a [**enumerálások. AuditRecords. Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) metódust egy olyan enumerálás létrehozásához, amelyet a többi oldalon való iterációhoz használhat.</span><span class="sxs-lookup"><span data-stu-id="d39b1-130">Once you have the initial page of items, use the [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) method to create an enumerator that you can use to iterate through the remaining pages.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var startDate = new DateTime(DateTime.Now.Year, DateTime.Now.Month, 01);

// First perform the query, then get the enumerator. Choose one of the following and comment out the other two.

// To retrieve audit records by company name substring (for example "bri" matches "Fabrikam, Inc.").
var searchSubstring="bri";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CompanyName.ToString(), FieldFilterOperation.Substring, searchSubstring);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by customer ID.
var customerId="0c39d6d5-c70d-4c55-bc02-f620844f3fd1";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CustomerId.ToString(), FieldFilterOperation.Equals, customerId);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by resource type.
int resourceTypeInt = 3; // Subscription Resource.
string searchField = Enum.GetName(typeof(ResourceType), resourceTypeInt);
var filter = new SimpleFieldFilter(AuditRecordSearchField.ResourceType.ToString(), FieldFilterOperation.Equals, searchField);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

var auditRecordEnumerator = partnerOperations.Enumerators.AuditRecords.Create(auditRecordsPage);

int pageNumber = 1;
while (auditRecordEnumerator.HasValue)
{
    // Work with the current page.
    foreach (var c in auditRecordEnumerator.Current.Items)
    {
        // Display some info, such as operation type, operation date, and operation status.
        Console.WriteLine(string.Format("{0} {1} {2}.", c.OperationType, c.OperationDate, c.OperationStatus));
    }

    // Get the next page of audit records.
    auditRecordEnumerator.Next();
}
```

<span data-ttu-id="d39b1-131">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d39b1-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d39b1-132">**Projekt**: a partner Center SDK Samples **mappája**: naplózás</span><span class="sxs-lookup"><span data-stu-id="d39b1-132">**Project**: Partner Center SDK Samples **Folder**: Auditing</span></span>

## <a name="rest-request"></a><span data-ttu-id="d39b1-133">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="d39b1-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d39b1-134">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d39b1-134">Request syntax</span></span>

| <span data-ttu-id="d39b1-135">Metódus</span><span class="sxs-lookup"><span data-stu-id="d39b1-135">Method</span></span>  | <span data-ttu-id="d39b1-136">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d39b1-136">Request URI</span></span>                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d39b1-137">**GET**</span><span class="sxs-lookup"><span data-stu-id="d39b1-137">**GET**</span></span> | <span data-ttu-id="d39b1-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {STARTDATE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d39b1-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span></span>                                                                                                     |
| <span data-ttu-id="d39b1-139">**GET**</span><span class="sxs-lookup"><span data-stu-id="d39b1-139">**GET**</span></span> | <span data-ttu-id="d39b1-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &endDate = {ENDDATE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d39b1-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span></span>                                                                                   |
| <span data-ttu-id="d39b1-141">**GET**</span><span class="sxs-lookup"><span data-stu-id="d39b1-141">**GET**</span></span> | <span data-ttu-id="d39b1-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &endDate = {endDate} &Filter = {"mező": "cégnév", "érték": "{searchSubstring}", "operátor": "alkarakterlánc"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d39b1-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span></span> |
| <span data-ttu-id="d39b1-143">**GET**</span><span class="sxs-lookup"><span data-stu-id="d39b1-143">**GET**</span></span> | <span data-ttu-id="d39b1-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &endDate = {endDate} &Filter = {"mező": "Vevőkód", "value": "{Vevőkód}", "operátor": "Equals"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d39b1-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span></span>          |
| <span data-ttu-id="d39b1-145">**GET**</span><span class="sxs-lookup"><span data-stu-id="d39b1-145">**GET**</span></span> | <span data-ttu-id="d39b1-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &endDate = {endDate} &Filter = {"mező": "resourcetype", "value": "{resourcetype}", "operátor": "Equals"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d39b1-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="d39b1-147">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d39b1-147">URI parameter</span></span>

<span data-ttu-id="d39b1-148">A kérelem létrehozásakor használja a következő lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="d39b1-148">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="d39b1-149">Név</span><span class="sxs-lookup"><span data-stu-id="d39b1-149">Name</span></span>      | <span data-ttu-id="d39b1-150">Típus</span><span class="sxs-lookup"><span data-stu-id="d39b1-150">Type</span></span>   | <span data-ttu-id="d39b1-151">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d39b1-151">Required</span></span> | <span data-ttu-id="d39b1-152">Leírás</span><span class="sxs-lookup"><span data-stu-id="d39b1-152">Description</span></span>                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d39b1-153">startDate</span><span class="sxs-lookup"><span data-stu-id="d39b1-153">startDate</span></span> | <span data-ttu-id="d39b1-154">dátum</span><span class="sxs-lookup"><span data-stu-id="d39b1-154">date</span></span>   | <span data-ttu-id="d39b1-155">Nem</span><span class="sxs-lookup"><span data-stu-id="d39b1-155">No</span></span>       | <span data-ttu-id="d39b1-156">A kezdő dátum éééé-hh-nn formátumban.</span><span class="sxs-lookup"><span data-stu-id="d39b1-156">The start date in yyyy-mm-dd format.</span></span> <span data-ttu-id="d39b1-157">Ha nincs megadva, az eredményhalmaz alapértelmezett értéke a kérelem dátuma előtt 30 nappal lesz.</span><span class="sxs-lookup"><span data-stu-id="d39b1-157">If none is provided, the result set will default to 30 days prior to the request date.</span></span> <span data-ttu-id="d39b1-158">Ez a paraméter nem kötelező, ha szűrő van megadva.</span><span class="sxs-lookup"><span data-stu-id="d39b1-158">This parameter is optional when a filter is supplied.</span></span>                                          |
| <span data-ttu-id="d39b1-159">endDate</span><span class="sxs-lookup"><span data-stu-id="d39b1-159">endDate</span></span>   | <span data-ttu-id="d39b1-160">dátum</span><span class="sxs-lookup"><span data-stu-id="d39b1-160">date</span></span>   | <span data-ttu-id="d39b1-161">Nem</span><span class="sxs-lookup"><span data-stu-id="d39b1-161">No</span></span>       | <span data-ttu-id="d39b1-162">A befejezési dátum éééé-hh-nn formátumban.</span><span class="sxs-lookup"><span data-stu-id="d39b1-162">The end date in yyyy-mm-dd format.</span></span> <span data-ttu-id="d39b1-163">Ez a paraméter nem kötelező, ha szűrő van megadva.</span><span class="sxs-lookup"><span data-stu-id="d39b1-163">This parameter is optional when a filter is supplied.</span></span> <span data-ttu-id="d39b1-164">Ha a befejezési dátum ki van hagyva, vagy NULL értékre van állítva, a kérelem a maximális ablakot adja vissza, vagy a mai napon a befejezési dátumot használja, attól függően, hogy melyik a kisebb.</span><span class="sxs-lookup"><span data-stu-id="d39b1-164">When the end date is omitted or set to null, the request returns the max window or uses today as the end date, whichever is less.</span></span> |
| <span data-ttu-id="d39b1-165">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="d39b1-165">filter</span></span>    | <span data-ttu-id="d39b1-166">sztring</span><span class="sxs-lookup"><span data-stu-id="d39b1-166">string</span></span> | <span data-ttu-id="d39b1-167">No</span><span class="sxs-lookup"><span data-stu-id="d39b1-167">No</span></span>       | <span data-ttu-id="d39b1-168">Az alkalmazni kívánt szűrő.</span><span class="sxs-lookup"><span data-stu-id="d39b1-168">The filter to apply.</span></span> <span data-ttu-id="d39b1-169">A paraméternek kódolt sztringnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="d39b1-169">This parameter must be an encoded string.</span></span> <span data-ttu-id="d39b1-170">Ez a paraméter nem kötelező, ha meg van adva a kezdő dátum vagy a befejezési dátum.</span><span class="sxs-lookup"><span data-stu-id="d39b1-170">This parameter is optional when the start date or end date are supplied.</span></span>                                                                                              |

### <a name="filter-syntax"></a><span data-ttu-id="d39b1-171">Szűrési szintaxis</span><span class="sxs-lookup"><span data-stu-id="d39b1-171">Filter syntax</span></span>
<span data-ttu-id="d39b1-172">A Filter paramétert vesszővel elválasztott, kulcs-érték párokból álló sorozatként kell összeállítani.</span><span class="sxs-lookup"><span data-stu-id="d39b1-172">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="d39b1-173">Minden kulcsot és értéket külön kell megadni, és kettősponttal kell elválasztani őket.</span><span class="sxs-lookup"><span data-stu-id="d39b1-173">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="d39b1-174">A teljes szűrőt kódolni kell.</span><span class="sxs-lookup"><span data-stu-id="d39b1-174">The entire filter must be encoded.</span></span>

<span data-ttu-id="d39b1-175">A kódolás nélküli példa a következőképpen néz ki:</span><span class="sxs-lookup"><span data-stu-id="d39b1-175">An unencoded example looks like this:</span></span>

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

<span data-ttu-id="d39b1-176">A következő táblázat a szükséges kulcs-érték párokat ismerteti:</span><span class="sxs-lookup"><span data-stu-id="d39b1-176">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="d39b1-177">Kulcs</span><span class="sxs-lookup"><span data-stu-id="d39b1-177">Key</span></span>                 | <span data-ttu-id="d39b1-178">Érték</span><span class="sxs-lookup"><span data-stu-id="d39b1-178">Value</span></span>                             |
|:--------------------|:----------------------------------|
| <span data-ttu-id="d39b1-179">Mező</span><span class="sxs-lookup"><span data-stu-id="d39b1-179">Field</span></span>               | <span data-ttu-id="d39b1-180">A szűrni kívánt mező.</span><span class="sxs-lookup"><span data-stu-id="d39b1-180">The field to filter.</span></span> <span data-ttu-id="d39b1-181">A támogatott értékek a [kérelem szintaxisában](get-a-record-of-partner-center-activity-by-user.md#rest-request)találhatók.</span><span class="sxs-lookup"><span data-stu-id="d39b1-181">The supported values can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>                                         |
| <span data-ttu-id="d39b1-182">Érték</span><span class="sxs-lookup"><span data-stu-id="d39b1-182">Value</span></span>               | <span data-ttu-id="d39b1-183">A szűréshez használandó érték.</span><span class="sxs-lookup"><span data-stu-id="d39b1-183">The value to filter by.</span></span> <span data-ttu-id="d39b1-184">A rendszer figyelmen kívül hagyja az érték esetét.</span><span class="sxs-lookup"><span data-stu-id="d39b1-184">The case of the value is ignored.</span></span> <span data-ttu-id="d39b1-185">A következő érték-paraméterek támogatottak a [kérelem szintaxisában](get-a-record-of-partner-center-activity-by-user.md#rest-request)látható módon:</span><span class="sxs-lookup"><span data-stu-id="d39b1-185">The following value parameters are supported as shown in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span></span><br/><br/>                                                                <span data-ttu-id="d39b1-186">*searchSubstring* – cserélje le a nevet a vállalat nevével.</span><span class="sxs-lookup"><span data-stu-id="d39b1-186">*searchSubstring* - Replace with the name of the company.</span></span> <span data-ttu-id="d39b1-187">Megadhat egy olyan alkarakterláncot, amely megfelel a vállalat nevének (például: `bri` egyezés `Fabrikam, Inc` ).</span><span class="sxs-lookup"><span data-stu-id="d39b1-187">You can enter a substring to match part of the company name (for example, `bri` will match `Fabrikam, Inc`).</span></span><br/><span data-ttu-id="d39b1-188">**Példa:**`"Value":"bri"`</span><span class="sxs-lookup"><span data-stu-id="d39b1-188">**Example:** `"Value":"bri"`</span></span><br/><br/>                                                                <span data-ttu-id="d39b1-189">*Vevőkód* – cserélje le egy GUID formátumú karakterláncot, amely az ügyfél azonosítóját jelöli.</span><span class="sxs-lookup"><span data-stu-id="d39b1-189">*customerId* - Replace with a GUID formatted string that represents the customer identifier.</span></span><br/><span data-ttu-id="d39b1-190">**Példa:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span><span class="sxs-lookup"><span data-stu-id="d39b1-190">**Example:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span></span><br/><br/>                                                                                        <span data-ttu-id="d39b1-191">*resourceType* – cserélje le annak az erőforrásnak a típusára, amelyre a naplózási rekordokat (például az előfizetést) be kell olvasni.</span><span class="sxs-lookup"><span data-stu-id="d39b1-191">*resourceType* - Replace with the type of resource for which to retrieve audit records (for example, Subscription).</span></span> <span data-ttu-id="d39b1-192">Az elérhető erőforrástípusok a [resourcetype](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype)-ben vannak meghatározva.</span><span class="sxs-lookup"><span data-stu-id="d39b1-192">The available resource types are defined in [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span></span><br/><span data-ttu-id="d39b1-193">**Példa:**`"Value":"Subscription"`</span><span class="sxs-lookup"><span data-stu-id="d39b1-193">**Example:** `"Value":"Subscription"`</span></span>                                 |
| <span data-ttu-id="d39b1-194">Operátor</span><span class="sxs-lookup"><span data-stu-id="d39b1-194">Operator</span></span>          | <span data-ttu-id="d39b1-195">Az alkalmazni kívánt operátor.</span><span class="sxs-lookup"><span data-stu-id="d39b1-195">The operator to apply.</span></span> <span data-ttu-id="d39b1-196">A támogatott operátorok a [kérelem szintaxisában](get-a-record-of-partner-center-activity-by-user.md#rest-request)találhatók.</span><span class="sxs-lookup"><span data-stu-id="d39b1-196">The supported operators can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="d39b1-197">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d39b1-197">Request headers</span></span>

- <span data-ttu-id="d39b1-198">További információért lásd a [parti központ Rest-fejléceit](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="d39b1-198">See [Parter Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="d39b1-199">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d39b1-199">Request body</span></span>

<span data-ttu-id="d39b1-200">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d39b1-200">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d39b1-201">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d39b1-201">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=6/1/2017%2012:00:00%20AM&filter=%7B%22Field%22:%22CustomerId%22,%22Value%22:%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22,%22Operator%22:%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="d39b1-202">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d39b1-202">REST response</span></span>

<span data-ttu-id="d39b1-203">Ha a művelet sikeres, ez a metódus a szűrőknek megfelelő tevékenységek egy halmazát adja vissza.</span><span class="sxs-lookup"><span data-stu-id="d39b1-203">If successful, this method returns a set of activities that meet the filters.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d39b1-204">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d39b1-204">Response success and error codes</span></span>

<span data-ttu-id="d39b1-205">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="d39b1-205">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d39b1-206">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="d39b1-206">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d39b1-207">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="d39b1-207">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d39b1-208">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d39b1-208">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CV: 4xDKynq/zE2im0wj.0
MS-ServerId: 030011719
Date: Tue, 27 Jun 2017 22:19:46 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "resourceType": "order",
            "resourceNewValue": "{\"Id\":\"d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"ReferenceCustomerId\":\"0c39d6d5-c70d-4c55-bc02-f620844f3fd1\",\"BillingCycle\":\"none\",\"LineItems\":[{\"LineItemNumber\":0,\"OfferId\":\"C0BD2E08-11AC-4836-BDC7-3712E744922F\",\"SubscriptionId\":\"488745B5-2086-4912-802C-6ABB9F7C3638\",\"ParentSubscriptionId\":null,\"FriendlyName\":\"Office 365 Business Premium Trial\",\"Quantity\":25,\"PartnerIdOnRecord\":null,\"Links\":{\"Subscription\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638\",\"Method\":\"GET\",\"Headers\":[]}}}],\"CreationDate\":\"2017-06-15T15:56:04.077-07:00\",\"Links\":{\"Self\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/orders/d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"Method\":\"GET\",\"Headers\":[]}},\"Attributes\":{\"Etag\":\"eyJpZCI6ImQ1MWEwNTJlLTA0M2MtNGEyYS1hYTM3LTJiYjkzOGNlZjZjMSIsInZlcnNpb24iOjF9\",\"ObjectType\":\"Order\"}}",
            "operationType": "create_order",
            "operationDate": "2017-06-15T22:56:05.0589308Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "OrderId",
                    "value": "d51a052e-043c-4a2a-aa37-2bb938cef6c1"
                }, {
                    "key": "BillingCycle",
                    "value": "None"
                }, {
                    "key": "OfferId-0",
                    "value": "C0BD2E08-11AC-4836-BDC7-3712E744922F"
                }, {
                    "key": "SubscriptionId-0",
                    "value": "488745B5-2086-4912-802C-6ABB9F7C3638"
                }, {
                    "key": "SubscriptionName-0",
                    "value": "Office 365 Business Premium Trial"
                }, {
                    "key": "Quantity-0",
                    "value": "25"
                }, {
                    "key": "PartnerOnRecord-0",
                    "value": null
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "applicationId": "Partner Center Native App",
            "resourceType": "license",
            "resourceNewValue": "{\"LicensesToAssign\":[{\"ExcludedPlans\":null,\"SkuId\":\"efccb6f7-5641-4e0e-bd10-b4976e1bf68e\"}],\"LicensesToRemove\":null,\"LicenseWarnings\":[],\"Attributes\":{\"ObjectType\":\"LicenseUpdate\"}}",
            "operationType": "update_customer_user_licenses",
            "operationDate": "2017-06-01T20:09:07.0450483Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "CustomerUserId",
                    "value": "482e2152-4b49-48ec-b715-823365ce3d4c"
                }, {
                    "key": "AddedLicenseSkuId",
                    "value": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e"
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/auditrecords?startDate=2017-06-01&size=500&filter=%7B%22Field%22%3A%22CustomerId%22%2C%22Value%22%3A%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```