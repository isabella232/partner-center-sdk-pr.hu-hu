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
# <a name="get-a-customers-utilization-records-for-azure"></a>Ügyfél Azure-használati rekordjainak lekérése

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Az ügyfél Azure-előfizetésének kihasználtsági rekordjait az Azure-kihasználtság API használatával szerezheti be egy adott időszakra vonatkozóan.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

Ez az API a napi és óránkénti nem értékelt felhasználást adja vissza egy tetszőleges időtartományra vonatkozóan. *Ez az API azonban nem támogatott az Azure-csomagokban*. Ha rendelkezik Azure-csomaggal, tekintse meg a [számlázás nem számlázott fogyasztási sorok beolvasása](get-invoice-unbilled-consumption-lineitems.md) és a számlázott [felhasználási sorok beolvasása](get-invoice-billed-consumption-lineitems.md) című cikket. Ezek a cikkek azt írják le, hogyan lehet a névleges fogyasztást napi szinten, egységenként. Ez a díjszabás megegyezik az Azure-kihasználtsági API által biztosított napi gabona-adatmennyiséggel. A számlázott használati adatok beolvasásához a számla azonosítóját kell használnia. Vagy a jelenlegi és az előző időszakok használatával lekérheti a nem számlázott használati becsléseket. *Az Azure-csomag előfizetési erőforrásai esetében jelenleg nem támogatott az óránkénti adatgabona és az önkényes dátumtartomány-szűrők* használata.

## <a name="azure-utilization-api"></a>Azure-kihasználtság API

Ez az Azure-kihasználtsági API hozzáférést biztosít a kihasználtsági rekordokhoz egy olyan időszakra vonatkozóan, amely azt jelzi, hogy a kihasználtság mikor jelent meg a számlázási rendszeren. Hozzáférést biztosít az egyeztetési fájl létrehozásához és kiszámításához használt kihasználtsági adataihoz. Azonban nem ismeri a számlázási rendszerek egyeztetése fájl logikáját. Nem várhatja el a fájl összefoglalási eredményeinek összeegyeztetését, hogy az adott API-ból beolvasott eredményt pontosan ugyanarra az időszakra kelljen megfeleltetni.

A számlázási rendszer például ugyanazokat a kihasználtsági értékeket veszi figyelembe, és a késői szabályok alapján határozza meg, hogy mi történik az egyeztetési fájlban. A számlázási időszak bezárásakor a rendszer a számlázási időszak végéig tartó teljes használatot a megbékélési fájlba kerül. A számlázási időszak végét követő 24 órán belül jelentett időszakon belüli késői használatot a következő egyeztetési fájlban számoljuk el. A partner számlázásával kapcsolatos késői szabályokért lásd: az Azure- [előfizetéshez tartozó felhasználási információk beolvasása](/previous-versions/azure/reference/mt219001(v=azure.100)).

Ez a REST API lapozható. Ha a válasz adattartalma nagyobb, mint egyetlen oldal, a következő hivatkozásra kell beolvasni a kihasználtsági rekordok következő oldalát.

## <a name="c"></a>C\#

Az Azure-kihasználtsági rekordok beszerzése:

1. Szerezze be az ügyfél-azonosítót és az előfizetés-azonosítót.

2. Hívja meg a [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) metódust egy olyan [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) visszaadásához, amely tartalmazza a kihasználtsági rekordokat.

3. Szerezze be az Azure-kihasználtsági rekordok enumerálását a kihasználtsági lapok bejárásához. Erre a lépésre azért van szükség, mert az erőforrás-gyűjtemény lapozható.

- **Minta**: [konzol tesztelési alkalmazás](console-test-app.md)
- **Projekt**: partner Center SDK-minták
- **Osztály**: GetAzureSubscriptionUtilization.cs

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

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Az Azure-beli kihasználtsági rekordok beszerzéséhez először szüksége lesz egy ügyfél-azonosítóra és egy előfizetés-azonosítóra. Ezután meghívja a **IAzureUtilizationCollection. Query** függvényt egy olyan **ResourceCollection** visszaküldéséhez, amely tartalmazza a kihasználtsági rekordokat. Mivel az erőforrás-gyűjtemény lapozható, be kell szereznie egy Azure-kihasználtsági rekord enumerálását a kihasználtsági lapok átjárásához.

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

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Az Azure-beli kihasználtsági rekordok beszerzéséhez először szüksége lesz egy ügyfél-azonosítóra és egy előfizetés-azonosítóra. Ezután hívja meg a [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md). Ez a parancs a megadott időszakra vonatkozó összes rendelkezésre álló rekordot visszaadja.

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus | Kérés URI-ja |
|------- | ----------- |
| **GET** | *{baseURL}*/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/utilizations/Azure? kezdési \_ idő = {kezdő időpont} &befejezési \_ idő = {befejezési idő} &részletesség = {részletesség} &show \_ details = {True} |

#### <a name="uri-parameters"></a>URI-paraméterek

A kihasználtsági rekordok beszerzéséhez használja a következő elérési utat és a lekérdezési paramétereket.

| Név | Típus | Kötelező | Leírás |
| ---- | ---- | -------- | ----------- |
| ügyfél – bérlő – azonosító | sztring | Igen | Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet. |
| előfizetés-azonosító | sztring | Igen | Egy GUID-formázott karakterlánc, amely azonosítja az előfizetést. |
| start_time | karakterlánc UTC dátum-idő eltolási formátumban | Igen | Annak az időtartománynak a kezdete, amely akkor jelenik meg, amikor a rendszer a kihasználtságot a számlázási rendszeren mutatja be. |
| end_time | karakterlánc UTC dátum-idő eltolási formátumban | Igen | Annak az időtartománynak a vége, amely akkor jelenik meg, amikor a rendszer a kihasználtságot a számlázási rendszeren mutatja be. |
| granularitása | sztring | No | Meghatározza a használati összesítések részletességét. Az elérhető lehetőségek a következők: `daily` (alapértelmezett) és `hourly` .
| show_details | boolean | Nem | Megadja, hogy a példány-szintű használat részleteit kívánja-e lekérni. A mező alapértelmezett értéke: `true`. |
| size | szám | Nem | Egy API-hívás által visszaadott összesítések számát adja meg. Az alapértelmezett érték 1000. A max 1000. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincs

### <a name="request-example"></a>Példa kérésre

Az alábbi példában szereplő kérelem olyan eredményeket hoz létre, amelyek a 7/2-8/1-as időszakra vonatkozó, a megbékélési fájlhoz hasonlóan jelennek meg. Előfordulhat, hogy ezek az eredmények nem egyeznek pontosan (lásd a részleteket az [Azure kihasználtsági API](#azure-utilization-api) szakaszban).

Ez a példa a számlázási rendszeren jelentett kihasználtsági adatok visszaküldése 12 órakor (UTC) és 8/2 (UTC) 7/2.

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus az [Azure kihasználtsági rekord](azure-utilization-record-resources.md) erőforrásainak gyűjteményét adja vissza a válasz törzsében. Ha az Azure-beli kihasználtsági adatok még nem állnak készen egy függő rendszerbe, ez a metódus egy 204-as HTTP-állapotkódot ad vissza Retry-After fejléccel.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. Hálózati nyomkövetési eszközzel olvassa be a HTTP-állapotkódot, a [hibakód típusát](error-codes.md)és a további paramétereket.

### <a name="response-example"></a>Példa válaszra

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
