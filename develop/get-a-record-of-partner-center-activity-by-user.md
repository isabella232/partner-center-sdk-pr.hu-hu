---
title: Partnerközpont-tevékenység rekordjának lekérése
description: Műveletrekord lekérése egy partnerfelhasználó vagy alkalmazás által egy adott időszakra vonatkozóan.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aec933d4b681d99080619505792bde56bdd25580
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873971"
---
# <a name="get-a-record-of-partner-center-activity"></a><span data-ttu-id="d8c98-103">Partnerközpont-tevékenység rekordjának lekérése</span><span class="sxs-lookup"><span data-stu-id="d8c98-103">Get a record of Partner Center activity</span></span>

<span data-ttu-id="d8c98-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d8c98-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d8c98-105">Ez a cikk azt ismerteti, hogyan lehet lekérni egy partnerfelhasználó vagy alkalmazás által egy adott időszakban végrehajtott műveletek rekordját.</span><span class="sxs-lookup"><span data-stu-id="d8c98-105">This article describes how to retrieve a record of operations that was performed by a partner user or application over a period of time.</span></span>

<span data-ttu-id="d8c98-106">Ezzel az API-val lekérhetők az előző 30 nap naplórekordjai az aktuális dátumból, vagy a kezdő és/vagy a záró dátum megadva megadott dátumtartományból.</span><span class="sxs-lookup"><span data-stu-id="d8c98-106">Use this API to retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="d8c98-107">Vegye figyelembe azonban, hogy teljesítménybeli okokból a tevékenységnapló adatainak rendelkezésre állása az előző 90 napra van korlátozva.</span><span class="sxs-lookup"><span data-stu-id="d8c98-107">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="d8c98-108">Az aktuális dátum előtti 90 napnál korábbi kezdési dátumú kérések hibás kérési kivételt (hibakód: 400) és egy megfelelő üzenetet kapnak.</span><span class="sxs-lookup"><span data-stu-id="d8c98-108">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8c98-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d8c98-109">Prerequisites</span></span>

- <span data-ttu-id="d8c98-110">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d8c98-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d8c98-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="d8c98-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d8c98-112">C\#</span><span class="sxs-lookup"><span data-stu-id="d8c98-112">C\#</span></span>

<span data-ttu-id="d8c98-113">A műveletrekordok Partnerközpont először hozza létre a lekérni kívánt rekordok dátumtartományát.</span><span class="sxs-lookup"><span data-stu-id="d8c98-113">To retrieve a record of Partner Center operations, first establish the date range for the records you want to retrieve.</span></span> <span data-ttu-id="d8c98-114">Az alábbi példakód csak kezdő dátumot használ, de záró dátumot is tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="d8c98-114">The following code example only uses a start date, but you can also include an end date.</span></span> <span data-ttu-id="d8c98-115">További információkért lásd a [**Query metódust.**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query)</span><span class="sxs-lookup"><span data-stu-id="d8c98-115">For more information, see the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) method.</span></span> <span data-ttu-id="d8c98-116">Ezután hozza létre az alkalmazni kívánt szűrőtípushoz szükséges változókat, és rendelje hozzá a megfelelő értékeket.</span><span class="sxs-lookup"><span data-stu-id="d8c98-116">Next, create the variables you need for the type of filter you want to apply, and assign the appropriate values.</span></span> <span data-ttu-id="d8c98-117">Ha például a vállalat nevesztring alsztring alapján szűr, hozzon létre egy változót, amely a karakterlánc alsztringet fogja tartani.</span><span class="sxs-lookup"><span data-stu-id="d8c98-117">For example, to filter by company name substring, create a variable to hold the substring.</span></span> <span data-ttu-id="d8c98-118">Az ügyfél-azonosító alapján való szűréshez hozzon létre egy változót az azonosítóhoz.</span><span class="sxs-lookup"><span data-stu-id="d8c98-118">To filter by customer ID, create a variable to hold the ID.</span></span>

<span data-ttu-id="d8c98-119">A következő példában mintakód van megtéve a cégnév alsztring, ügyfél-azonosító vagy erőforrástípus alapján való szűréshez.</span><span class="sxs-lookup"><span data-stu-id="d8c98-119">In the following example, sample code is provided to filter by a company name substring, customer ID, or resource type.</span></span> <span data-ttu-id="d8c98-120">Válasszon ki egyet, és jelölje meg megjegyzésként a többit.</span><span class="sxs-lookup"><span data-stu-id="d8c98-120">Choose one and comment out the others.</span></span> <span data-ttu-id="d8c98-121">Minden esetben először példányosunk egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumot [](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) az alapértelmezett konstruktor használatával a szűrő létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="d8c98-121">In each case, you first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object using its default [**constructor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) to create the filter.</span></span> <span data-ttu-id="d8c98-122">Meg kell adni egy sztringet, amely tartalmazza a kereshető mezőt, valamint az alkalmazandó megfelelő operátort, ahogy az ábrán látható.</span><span class="sxs-lookup"><span data-stu-id="d8c98-122">You'll need to pass a string that contains the field to search, and the appropriate operator to apply, as shown.</span></span> <span data-ttu-id="d8c98-123">A szűréshez meg kell adnia a sztringet is.</span><span class="sxs-lookup"><span data-stu-id="d8c98-123">You also must provide the string to filter by.</span></span>

<span data-ttu-id="d8c98-124">Ezután az [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) tulajdonság használatával lekérdezheti a rekordműveleteket naplózható felületet, és a [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) vagy [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) metódust hívva végrehajtja a szűrőt, és lekérdezheti az eredmény első oldalát képviselő [**AuditRecord-gyűjteményt.**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord)</span><span class="sxs-lookup"><span data-stu-id="d8c98-124">Next, use the [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) property to get an interface to audit record operations, and call the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) method to execute the filter and get the collection of [**AuditRecord's**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) that represent the first page of the result.</span></span> <span data-ttu-id="d8c98-125">Adja át a metódusnak a kezdő dátumot, egy opcionális záró dátumot, amely itt nem használatos a példában, valamint egy [**IQuery-objektumot,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) amely egy entitáson való lekérdezést képvisel.</span><span class="sxs-lookup"><span data-stu-id="d8c98-125">Pass the method the start date, an optional end date not used in the example here, and an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object that represents a query on an entity.</span></span> <span data-ttu-id="d8c98-126">Az IQuery objektum úgy jön létre, hogy a fent létrehozott szűrőt átküldi a [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery metódusának.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery)</span><span class="sxs-lookup"><span data-stu-id="d8c98-126">The IQuery object is created by passing the filter created above to the [**QueryFactory's**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method.</span></span>

<span data-ttu-id="d8c98-127">Ha már megvan az elemek kezdeti oldala, az [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) metódussal hozzon létre egy enumerátort, amely a fennmaradó oldalakon való iteráláshoz használható.</span><span class="sxs-lookup"><span data-stu-id="d8c98-127">Once you have the initial page of items, use the [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) method to create an enumerator that you can use to iterate through the remaining pages.</span></span>

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

<span data-ttu-id="d8c98-128">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d8c98-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d8c98-129">**Project**: Partnerközpont SDK **Mappa:** Naplózás</span><span class="sxs-lookup"><span data-stu-id="d8c98-129">**Project**: Partner Center SDK Samples **Folder**: Auditing</span></span>

## <a name="rest-request"></a><span data-ttu-id="d8c98-130">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d8c98-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d8c98-131">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d8c98-131">Request syntax</span></span>

| <span data-ttu-id="d8c98-132">Metódus</span><span class="sxs-lookup"><span data-stu-id="d8c98-132">Method</span></span>  | <span data-ttu-id="d8c98-133">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d8c98-133">Request URI</span></span>                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d8c98-134">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d8c98-134">**GET**</span></span> | <span data-ttu-id="d8c98-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d8c98-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span></span>                                                                                                     |
| <span data-ttu-id="d8c98-136">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d8c98-136">**GET**</span></span> | <span data-ttu-id="d8c98-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d8c98-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span></span>                                                                                   |
| <span data-ttu-id="d8c98-138">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d8c98-138">**GET**</span></span> | <span data-ttu-id="d8c98-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d8c98-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span></span> |
| <span data-ttu-id="d8c98-140">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d8c98-140">**GET**</span></span> | <span data-ttu-id="d8c98-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d8c98-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span></span>          |
| <span data-ttu-id="d8c98-142">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d8c98-142">**GET**</span></span> | <span data-ttu-id="d8c98-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d8c98-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="d8c98-144">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d8c98-144">URI parameter</span></span>

<span data-ttu-id="d8c98-145">A kérelem létrehozásakor használja a következő lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="d8c98-145">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="d8c98-146">Név</span><span class="sxs-lookup"><span data-stu-id="d8c98-146">Name</span></span>      | <span data-ttu-id="d8c98-147">Típus</span><span class="sxs-lookup"><span data-stu-id="d8c98-147">Type</span></span>   | <span data-ttu-id="d8c98-148">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d8c98-148">Required</span></span> | <span data-ttu-id="d8c98-149">Leírás</span><span class="sxs-lookup"><span data-stu-id="d8c98-149">Description</span></span>                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d8c98-150">startDate (kezdőDátum)</span><span class="sxs-lookup"><span data-stu-id="d8c98-150">startDate</span></span> | <span data-ttu-id="d8c98-151">dátum</span><span class="sxs-lookup"><span data-stu-id="d8c98-151">date</span></span>   | <span data-ttu-id="d8c98-152">Nem</span><span class="sxs-lookup"><span data-stu-id="d8c98-152">No</span></span>       | <span data-ttu-id="d8c98-153">A kezdődátum yyyy-mm-dd formátumban.</span><span class="sxs-lookup"><span data-stu-id="d8c98-153">The start date in yyyy-mm-dd format.</span></span> <span data-ttu-id="d8c98-154">Ha nincs megjelölve, az eredményhalmaz alapértelmezés szerint 30 nappal a kérés dátuma előtt lesz.</span><span class="sxs-lookup"><span data-stu-id="d8c98-154">If none is provided, the result set will default to 30 days prior to the request date.</span></span> <span data-ttu-id="d8c98-155">Ez a paraméter nem kötelező szűrő megadása esetén.</span><span class="sxs-lookup"><span data-stu-id="d8c98-155">This parameter is optional when a filter is supplied.</span></span>                                          |
| <span data-ttu-id="d8c98-156">endDate (endDate)</span><span class="sxs-lookup"><span data-stu-id="d8c98-156">endDate</span></span>   | <span data-ttu-id="d8c98-157">dátum</span><span class="sxs-lookup"><span data-stu-id="d8c98-157">date</span></span>   | <span data-ttu-id="d8c98-158">Nem</span><span class="sxs-lookup"><span data-stu-id="d8c98-158">No</span></span>       | <span data-ttu-id="d8c98-159">A záró dátum yyyy-mm-dd formátumban.</span><span class="sxs-lookup"><span data-stu-id="d8c98-159">The end date in yyyy-mm-dd format.</span></span> <span data-ttu-id="d8c98-160">Ez a paraméter nem kötelező szűrő megadása esetén.</span><span class="sxs-lookup"><span data-stu-id="d8c98-160">This parameter is optional when a filter is supplied.</span></span> <span data-ttu-id="d8c98-161">Ha a záró dátum nincs megadva vagy null értékűre van állítva, a kérés a maximális ablakot adja vissza, vagy a mai napot használja záró dátumként (amelyik kisebb).</span><span class="sxs-lookup"><span data-stu-id="d8c98-161">When the end date is omitted or set to null, the request returns the max window or uses today as the end date, whichever is less.</span></span> |
| <span data-ttu-id="d8c98-162">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="d8c98-162">filter</span></span>    | <span data-ttu-id="d8c98-163">sztring</span><span class="sxs-lookup"><span data-stu-id="d8c98-163">string</span></span> | <span data-ttu-id="d8c98-164">No</span><span class="sxs-lookup"><span data-stu-id="d8c98-164">No</span></span>       | <span data-ttu-id="d8c98-165">Az alkalmazandó szűrő.</span><span class="sxs-lookup"><span data-stu-id="d8c98-165">The filter to apply.</span></span> <span data-ttu-id="d8c98-166">Ennek a paraméternek kódolt sztringnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="d8c98-166">This parameter must be an encoded string.</span></span> <span data-ttu-id="d8c98-167">Ez a paraméter nem kötelező, ha a kezdő dátum vagy a záró dátum meg van adva.</span><span class="sxs-lookup"><span data-stu-id="d8c98-167">This parameter is optional when the start date or end date are supplied.</span></span>                                                                                              |

### <a name="filter-syntax"></a><span data-ttu-id="d8c98-168">Szűrőszintaxis</span><span class="sxs-lookup"><span data-stu-id="d8c98-168">Filter syntax</span></span>
<span data-ttu-id="d8c98-169">A szűrőparamétert vesszővel tagolt kulcs-érték párok sorozataként kell összerakni.</span><span class="sxs-lookup"><span data-stu-id="d8c98-169">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="d8c98-170">Minden kulcsot és értéket külön kell idézni, és kettősponttal kell elválasztani egymástól.</span><span class="sxs-lookup"><span data-stu-id="d8c98-170">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="d8c98-171">A teljes szűrőt kódolni kell.</span><span class="sxs-lookup"><span data-stu-id="d8c98-171">The entire filter must be encoded.</span></span>

<span data-ttu-id="d8c98-172">Egy nem kódolatlan példa a következő:</span><span class="sxs-lookup"><span data-stu-id="d8c98-172">An unencoded example looks like this:</span></span>

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

<span data-ttu-id="d8c98-173">Az alábbi táblázat a szükséges kulcs-érték párokat ismerteti:</span><span class="sxs-lookup"><span data-stu-id="d8c98-173">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="d8c98-174">Kulcs</span><span class="sxs-lookup"><span data-stu-id="d8c98-174">Key</span></span>                 | <span data-ttu-id="d8c98-175">Érték</span><span class="sxs-lookup"><span data-stu-id="d8c98-175">Value</span></span>                             |
|:--------------------|:----------------------------------|
| <span data-ttu-id="d8c98-176">Mező</span><span class="sxs-lookup"><span data-stu-id="d8c98-176">Field</span></span>               | <span data-ttu-id="d8c98-177">A szűrni való mező.</span><span class="sxs-lookup"><span data-stu-id="d8c98-177">The field to filter.</span></span> <span data-ttu-id="d8c98-178">A támogatott értékek a [kérelemszintaxisban találhatók.](get-a-record-of-partner-center-activity-by-user.md#rest-request)</span><span class="sxs-lookup"><span data-stu-id="d8c98-178">The supported values can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>                                         |
| <span data-ttu-id="d8c98-179">Érték</span><span class="sxs-lookup"><span data-stu-id="d8c98-179">Value</span></span>               | <span data-ttu-id="d8c98-180">A szűrési érték.</span><span class="sxs-lookup"><span data-stu-id="d8c98-180">The value to filter by.</span></span> <span data-ttu-id="d8c98-181">A rendszer figyelmen kívül hagyja az érték kis- és nagyját.</span><span class="sxs-lookup"><span data-stu-id="d8c98-181">The case of the value is ignored.</span></span> <span data-ttu-id="d8c98-182">A kérelemszintaxisban látható módon a következő [értékparaméterek támogatottak:](get-a-record-of-partner-center-activity-by-user.md#rest-request)</span><span class="sxs-lookup"><span data-stu-id="d8c98-182">The following value parameters are supported as shown in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span></span><br/><br/>                                                                <span data-ttu-id="d8c98-183">*searchSubstring* – Cserélje le a helyére a vállalat nevét.</span><span class="sxs-lookup"><span data-stu-id="d8c98-183">*searchSubstring* - Replace with the name of the company.</span></span> <span data-ttu-id="d8c98-184">A név egy részének megfelelő karakterláncot is megadhatja (például a megfelel a `bri` következőnek: `Fabrikam, Inc` ).</span><span class="sxs-lookup"><span data-stu-id="d8c98-184">You can enter a substring to match part of the company name (for example, `bri` will match `Fabrikam, Inc`).</span></span><br/><span data-ttu-id="d8c98-185">**Példa:**`"Value":"bri"`</span><span class="sxs-lookup"><span data-stu-id="d8c98-185">**Example:** `"Value":"bri"`</span></span><br/><br/>                                                                <span data-ttu-id="d8c98-186">*customerId* – Cserélje le a helyére az ügyfél azonosítóját képviselő GUID formátumú sztringet.</span><span class="sxs-lookup"><span data-stu-id="d8c98-186">*customerId* - Replace with a GUID formatted string that represents the customer identifier.</span></span><br/><span data-ttu-id="d8c98-187">**Példa:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span><span class="sxs-lookup"><span data-stu-id="d8c98-187">**Example:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span></span><br/><br/>                                                                                        <span data-ttu-id="d8c98-188">*resourceType* – Cserélje le a helyére azt az erőforrástípust, amelyhez lekéri a naplórekordokat (például előfizetés).</span><span class="sxs-lookup"><span data-stu-id="d8c98-188">*resourceType* - Replace with the type of resource for which to retrieve audit records (for example, Subscription).</span></span> <span data-ttu-id="d8c98-189">Az elérhető erőforrástípusok a [ResourceType típusban vannak meghatározva.](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype)</span><span class="sxs-lookup"><span data-stu-id="d8c98-189">The available resource types are defined in [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span></span><br/><span data-ttu-id="d8c98-190">**Példa:**`"Value":"Subscription"`</span><span class="sxs-lookup"><span data-stu-id="d8c98-190">**Example:** `"Value":"Subscription"`</span></span>                                 |
| <span data-ttu-id="d8c98-191">Operátor</span><span class="sxs-lookup"><span data-stu-id="d8c98-191">Operator</span></span>          | <span data-ttu-id="d8c98-192">Az alkalmazandó operátor.</span><span class="sxs-lookup"><span data-stu-id="d8c98-192">The operator to apply.</span></span> <span data-ttu-id="d8c98-193">A támogatott operátorok a [Kérelemszintaxisban találhatók.](get-a-record-of-partner-center-activity-by-user.md#rest-request)</span><span class="sxs-lookup"><span data-stu-id="d8c98-193">The supported operators can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="d8c98-194">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d8c98-194">Request headers</span></span>

- <span data-ttu-id="d8c98-195">További információ: [Parter Center REST-fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d8c98-195">For more information, see [Parter Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d8c98-196">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d8c98-196">Request body</span></span>

<span data-ttu-id="d8c98-197">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d8c98-197">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d8c98-198">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d8c98-198">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="d8c98-199">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d8c98-199">REST response</span></span>

<span data-ttu-id="d8c98-200">Ha ez a módszer sikeres, a szűrőknek megfelelő tevékenységeket ad vissza.</span><span class="sxs-lookup"><span data-stu-id="d8c98-200">If successful, this method returns a set of activities that meet the filters.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d8c98-201">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d8c98-201">Response success and error codes</span></span>

<span data-ttu-id="d8c98-202">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d8c98-202">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d8c98-203">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d8c98-203">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d8c98-204">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d8c98-204">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d8c98-205">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d8c98-205">Response example</span></span>

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