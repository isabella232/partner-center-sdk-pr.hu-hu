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
# <a name="get-a-record-of-partner-center-activity"></a>Partnerközpont-tevékenység rekordjának lekérése

**A következőkre vonatkozik**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ez a cikk azt ismerteti, hogyan kérhető le olyan műveletek rekordja, amelyeket egy adott időtartamon belül egy partner felhasználó vagy alkalmazás hajtott végre.

Ezzel az API-val lekérheti az előző 30 nap naplózási rekordjait az aktuális dátumból, illetve a Kezdődátum és/vagy a befejezési dátummal megadott dátumtartományt. Vegye figyelembe azonban, hogy a teljesítmény miatt a tevékenység naplójának adatelérhetősége az előző 90 napra korlátozódik. Az aktuális dátum előtt 90 nappal nagyobb kezdési dátummal rendelkező kérések esetén a rendszer rossz kérési kivételt (hibakód: 400) és megfelelő üzenetet kap.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

## <a name="c"></a>C\#

A partner Center-műveletek rekordjának lekéréséhez először hozza létre a lekérdezni kívánt rekordok dátumtartományt. A következő példa csak kezdő dátumot használ, de a befejezési dátumot is megadhatja. További információ: [**lekérdezési**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) módszer. Ezután hozza létre a szükséges változókat az alkalmazni kívánt szűrő típusához, és rendelje hozzá a megfelelő értékeket. Ha például a vállalat neve alsztring alapján szeretne szűrni, hozzon létre egy változót az alsztring tárolásához. Az ügyfél-azonosító alapján történő szűréshez hozzon létre egy változót az azonosító tárolásához.

A következő példában a rendszer minta kódot biztosít a vállalat neve alsztring, az ügyfél azonosítója vagy az erőforrástípus alapján történő szűréshez. Válassza ki az egyiket, és véleményezze a többiet. Minden esetben először hozzon létre egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumot az alapértelmezett [**konstruktor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) használatával a szűrő létrehozásához. Meg kell adnia egy karakterláncot, amely a keresendő mezőt tartalmazza, és a megfelelő operátort kell alkalmaznia, ahogy az látható. Meg kell adnia a szűréshez használandó karakterláncot is.

Ezután a [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) tulajdonsággal szerezzen be egy felületet a rekordok naplózásához, és hívja meg a [**lekérdezés**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) vagy a [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) metódust a szűrő végrehajtásához és az eredmény első oldalát ábrázoló [**AuditRecord**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) gyűjteményének lekéréséhez. Adja át a metódust a kezdő dátumnak, az itt látható példában nem használt nem kötelező befejezési dátumnak, valamint egy entitásra vonatkozó lekérdezést jelölő [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) objektumnak. A IQuery objektum létrehozása a fent létrehozott szűrőnek a [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódusba való átadásával történik.

Miután megtörtént az elemek kezdeti lapja, használja a [**enumerálások. AuditRecords. Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) metódust egy olyan enumerálás létrehozásához, amelyet a többi oldalon való iterációhoz használhat.

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

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: a partner Center SDK Samples **mappája**: naplózás

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {STARTDATE} http/1.1                                                                                                     |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &endDate = {ENDDATE} http/1.1                                                                                   |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &endDate = {endDate} &Filter = {"mező": "cégnév", "érték": "{searchSubstring}", "operátor": "alkarakterlánc"} http/1.1 |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &endDate = {endDate} &Filter = {"mező": "Vevőkód", "value": "{Vevőkód}", "operátor": "Equals"} http/1.1          |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords? StartDate = {startDate} &endDate = {endDate} &Filter = {"mező": "resourcetype", "value": "{resourcetype}", "operátor": "Equals"} http/1.1      |

### <a name="uri-parameter"></a>URI-paraméter

A kérelem létrehozásakor használja a következő lekérdezési paramétereket.

| Név      | Típus   | Kötelező | Leírás                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| startDate | dátum   | Nem       | A kezdő dátum éééé-hh-nn formátumban. Ha nincs megadva, az eredményhalmaz alapértelmezett értéke a kérelem dátuma előtt 30 nappal lesz. Ez a paraméter nem kötelező, ha szűrő van megadva.                                          |
| endDate   | dátum   | Nem       | A befejezési dátum éééé-hh-nn formátumban. Ez a paraméter nem kötelező, ha szűrő van megadva. Ha a befejezési dátum ki van hagyva, vagy NULL értékre van állítva, a kérelem a maximális ablakot adja vissza, vagy a mai napon a befejezési dátumot használja, attól függően, hogy melyik a kisebb. |
| filter (szűrő)    | sztring | No       | Az alkalmazni kívánt szűrő. A paraméternek kódolt sztringnek kell lennie. Ez a paraméter nem kötelező, ha meg van adva a kezdő dátum vagy a befejezési dátum.                                                                                              |

### <a name="filter-syntax"></a>Szűrési szintaxis
A Filter paramétert vesszővel elválasztott, kulcs-érték párokból álló sorozatként kell összeállítani. Minden kulcsot és értéket külön kell megadni, és kettősponttal kell elválasztani őket. A teljes szűrőt kódolni kell.

A kódolás nélküli példa a következőképpen néz ki:

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

A következő táblázat a szükséges kulcs-érték párokat ismerteti:

| Kulcs                 | Érték                             |
|:--------------------|:----------------------------------|
| Mező               | A szűrni kívánt mező. A támogatott értékek a [kérelem szintaxisában](get-a-record-of-partner-center-activity-by-user.md#rest-request)találhatók.                                         |
| Érték               | A szűréshez használandó érték. A rendszer figyelmen kívül hagyja az érték esetét. A következő érték-paraméterek támogatottak a [kérelem szintaxisában](get-a-record-of-partner-center-activity-by-user.md#rest-request)látható módon:<br/><br/>                                                                *searchSubstring* – cserélje le a nevet a vállalat nevével. Megadhat egy olyan alkarakterláncot, amely megfelel a vállalat nevének (például: `bri` egyezés `Fabrikam, Inc` ).<br/>**Példa:**`"Value":"bri"`<br/><br/>                                                                *Vevőkód* – cserélje le egy GUID formátumú karakterláncot, amely az ügyfél azonosítóját jelöli.<br/>**Példa:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`<br/><br/>                                                                                        *resourceType* – cserélje le annak az erőforrásnak a típusára, amelyre a naplózási rekordokat (például az előfizetést) be kell olvasni. Az elérhető erőforrástípusok a [resourcetype](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype)-ben vannak meghatározva.<br/>**Példa:**`"Value":"Subscription"`                                 |
| Operátor          | Az alkalmazni kívánt operátor. A támogatott operátorok a [kérelem szintaxisában](get-a-record-of-partner-center-activity-by-user.md#rest-request)találhatók.   |

### <a name="request-headers"></a>Kérésfejlécek

- További információért lásd a [parti központ Rest-fejléceit](headers.md) .

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

Ha a művelet sikeres, ez a metódus a szűrőknek megfelelő tevékenységek egy halmazát adja vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

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