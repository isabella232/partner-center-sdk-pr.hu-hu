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
# <a name="get-a-record-of-partner-center-activity"></a>Partnerközpont-tevékenység rekordjának lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Ez a cikk azt ismerteti, hogyan lehet lekérni egy partnerfelhasználó vagy alkalmazás által egy adott időszakban végrehajtott műveletek rekordját.

Ezzel az API-val lekérhetők az előző 30 nap naplórekordjai az aktuális dátumból, vagy a kezdő és/vagy a záró dátum megadva megadott dátumtartományból. Vegye figyelembe azonban, hogy teljesítménybeli okokból a tevékenységnapló adatainak rendelkezésre állása az előző 90 napra van korlátozva. Az aktuális dátum előtti 90 napnál korábbi kezdési dátumú kérések hibás kérési kivételt (hibakód: 400) és egy megfelelő üzenetet kapnak.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

## <a name="c"></a>C\#

A műveletrekordok Partnerközpont először hozza létre a lekérni kívánt rekordok dátumtartományát. Az alábbi példakód csak kezdő dátumot használ, de záró dátumot is tartalmazhat. További információkért lásd a [**Query metódust.**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) Ezután hozza létre az alkalmazni kívánt szűrőtípushoz szükséges változókat, és rendelje hozzá a megfelelő értékeket. Ha például a vállalat nevesztring alsztring alapján szűr, hozzon létre egy változót, amely a karakterlánc alsztringet fogja tartani. Az ügyfél-azonosító alapján való szűréshez hozzon létre egy változót az azonosítóhoz.

A következő példában mintakód van megtéve a cégnév alsztring, ügyfél-azonosító vagy erőforrástípus alapján való szűréshez. Válasszon ki egyet, és jelölje meg megjegyzésként a többit. Minden esetben először példányosunk egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumot [](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) az alapértelmezett konstruktor használatával a szűrő létrehozásához. Meg kell adni egy sztringet, amely tartalmazza a kereshető mezőt, valamint az alkalmazandó megfelelő operátort, ahogy az ábrán látható. A szűréshez meg kell adnia a sztringet is.

Ezután az [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) tulajdonság használatával lekérdezheti a rekordműveleteket naplózható felületet, és a [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) vagy [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) metódust hívva végrehajtja a szűrőt, és lekérdezheti az eredmény első oldalát képviselő [**AuditRecord-gyűjteményt.**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) Adja át a metódusnak a kezdő dátumot, egy opcionális záró dátumot, amely itt nem használatos a példában, valamint egy [**IQuery-objektumot,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) amely egy entitáson való lekérdezést képvisel. Az IQuery objektum úgy jön létre, hogy a fent létrehozott szűrőt átküldi a [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery metódusának.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery)

Ha már megvan az elemek kezdeti oldala, az [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) metódussal hozzon létre egy enumerátort, amely a fennmaradó oldalakon való iteráláshoz használható.

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

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Mappa:** Naplózás

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1                                                                                                     |
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1                                                                                   |
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1 |
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1          |
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1      |

### <a name="uri-parameter"></a>URI-paraméter

A kérelem létrehozásakor használja a következő lekérdezési paramétereket.

| Név      | Típus   | Kötelező | Leírás                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| startDate (kezdőDátum) | dátum   | Nem       | A kezdődátum yyyy-mm-dd formátumban. Ha nincs megjelölve, az eredményhalmaz alapértelmezés szerint 30 nappal a kérés dátuma előtt lesz. Ez a paraméter nem kötelező szűrő megadása esetén.                                          |
| endDate (endDate)   | dátum   | Nem       | A záró dátum yyyy-mm-dd formátumban. Ez a paraméter nem kötelező szűrő megadása esetén. Ha a záró dátum nincs megadva vagy null értékűre van állítva, a kérés a maximális ablakot adja vissza, vagy a mai napot használja záró dátumként (amelyik kisebb). |
| filter (szűrő)    | sztring | No       | Az alkalmazandó szűrő. Ennek a paraméternek kódolt sztringnek kell lennie. Ez a paraméter nem kötelező, ha a kezdő dátum vagy a záró dátum meg van adva.                                                                                              |

### <a name="filter-syntax"></a>Szűrőszintaxis
A szűrőparamétert vesszővel tagolt kulcs-érték párok sorozataként kell összerakni. Minden kulcsot és értéket külön kell idézni, és kettősponttal kell elválasztani egymástól. A teljes szűrőt kódolni kell.

Egy nem kódolatlan példa a következő:

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

Az alábbi táblázat a szükséges kulcs-érték párokat ismerteti:

| Kulcs                 | Érték                             |
|:--------------------|:----------------------------------|
| Mező               | A szűrni való mező. A támogatott értékek a [kérelemszintaxisban találhatók.](get-a-record-of-partner-center-activity-by-user.md#rest-request)                                         |
| Érték               | A szűrési érték. A rendszer figyelmen kívül hagyja az érték kis- és nagyját. A kérelemszintaxisban látható módon a következő [értékparaméterek támogatottak:](get-a-record-of-partner-center-activity-by-user.md#rest-request)<br/><br/>                                                                *searchSubstring* – Cserélje le a helyére a vállalat nevét. A név egy részének megfelelő karakterláncot is megadhatja (például a megfelel a `bri` következőnek: `Fabrikam, Inc` ).<br/>**Példa:**`"Value":"bri"`<br/><br/>                                                                *customerId* – Cserélje le a helyére az ügyfél azonosítóját képviselő GUID formátumú sztringet.<br/>**Példa:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`<br/><br/>                                                                                        *resourceType* – Cserélje le a helyére azt az erőforrástípust, amelyhez lekéri a naplórekordokat (például előfizetés). Az elérhető erőforrástípusok a [ResourceType típusban vannak meghatározva.](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype)<br/>**Példa:**`"Value":"Subscription"`                                 |
| Operátor          | Az alkalmazandó operátor. A támogatott operátorok a [Kérelemszintaxisban találhatók.](get-a-record-of-partner-center-activity-by-user.md#rest-request)   |

### <a name="request-headers"></a>Kérésfejlécek

- További információ: [Parter Center REST-fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

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

## <a name="rest-response"></a>REST-válasz

Ha ez a módszer sikeres, a szűrőknek megfelelő tevékenységeket ad vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

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