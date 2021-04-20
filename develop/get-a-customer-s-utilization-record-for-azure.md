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
# <a name="get-a-customers-utilization-records-for-azure"></a>Ügyfél Azure-használati rekordjainak lekérése

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Az ügyfél Azure-előfizetésének kihasználtsági rekordjait egy adott időszakra az Azure utilization API használatával kaphatja meg.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

Ez az API egy tetszőleges időtartamra napi és óránkénti, nem egységes használatot ad vissza. Ez az API azonban nem támogatott az *Azure-csomagokhoz.* Ha már van [Azure-csomagja,](get-invoice-unbilled-consumption-lineitems.md) tekintse meg a számla [](get-invoice-billed-consumption-lineitems.md) nem számlázott használatú sorelemeket és a számlázott használatú sorok cikkeit. Ezek a cikkek azt ismertetik, hogyan lehet mérőnként napi szinten lekért névleges fogyasztást erőforrásonként. Ez a díjfelhasználás megegyezik az Azure utilization API által biztosított napi rendszerességgel kapcsolatos adatokkal. A számlázott használati adatok lekéréséhez a számlaazonosítót kell használnia. Az aktuális és az előző időszakokkal is lekért használati becsléseket kaphat. Az óránkénti adat- és tetszőleges dátumtartomány-szűrők jelenleg nem támogatottak az *Azure-csomag előfizetési erőforrásaihoz.*

## <a name="azure-utilization-api"></a>Azure-kihasználtsági API

Ez az Azure-beli kihasználtsági API hozzáférést biztosít a kihasználtsági rekordokhoz egy olyan időszakra vonatkozóan, amely azt jelzi, hogy mikor jelentték a kihasználtságot a számlázási rendszerben. Hozzáférést biztosít ugyanazokhoz a kihasználtsági adatokhoz, amelyek az egyeztetési fájl létrehozásához és kiszámításához használatosak. Nem ismeri azonban a számlázási rendszer egyeztetési fájllogikát. Az egyeztetési fájl összegzési eredményei várhatóan nem egyeznek meg az API-ból pontosan ugyanabban az időszakban lekért eredményekkel.

A számlázási rendszer például ugyanezeket a kihasználtsági adatokat alkalmazza, és késési szabályokat alkalmaz annak megállapításához, hogy mit kell figyelembe vennie egy egyeztetési fájlban. Ha egy számlázási időszak véget ér, az egyeztetési fájl tartalmazza a számlázási időszak végét elvégő teljes használatot. A számlázási időszakon belül a számlázási időszak vége után 24 órán belül jelentett minden kései használatot a következő egyeztetési fájlban kell figyelembe venni. A partner számlázásának késési szabályaiért lásd: [Azure-előfizetés fogyasztási adatainak lekérte.](/previous-versions/azure/reference/mt219001(v=azure.100))

Ez REST API lapra van ásva. Ha a válasz hasznos adatai nagyobbak egyetlen lapnál, a következő hivatkozásra kattintva le kell töltenie a kihasználtsági rekordok következő lapját.

### <a name="scenario--partner-a-has-transferred-billing-ownership-of-azure-legacy-subscription-145p-to-partner-b"></a>Forgatókönyv: Az A partner átvitte az Örökölt Azure-előfizetés (145P) számlázási tulajdonjogát a B partnernek

Ha egy partner egy örökölt Azure-előfizetés számlázási tulajdonjogát átadja egy másik partnernek, amikor az új partner a Utilization API-t hívja meg az átvitt előfizetéshez, akkor az Azure-jogosultságazonosító helyett a Kereskedelmi előfizetés azonosítóját (amely az Partnerközpont-fiókjában jelenik meg) kell használnia. Az Azure-jogosultságazonosító csak akkor jelenik meg a B partnernél, ha rendszergazda (AOBO) az ügyfél Azure Portal. 

Az átvitt előfizetés Utilization API-jának sikeres hívásához az új partnernek a Kereskedelmi előfizetés azonosítóját kell használnia.

## <a name="c"></a>C\#

Az Azure-beli kihasználtsági rekordok beszerzése:

1. Szerezze be az ügyfél-azonosítót és az előfizetés-azonosítót.

2. Hívja meg az [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) metódust a kihasználtsági rekordokat tartalmazó [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) visszaadása érdekében.

3. Szerezzen be egy Azure-beli kihasználtságirekord-enumerátort a kihasználtsági lapok bejárására. Erre a lépésre azért van szükség, mert az erőforrás-gyűjtemény lapszám van meglaposodva.

- **Minta:** [Konzoltesztalkalmazás](console-test-app.md)
- **Projekt:** Partnerközpont SDK minták
- **Osztály:** GetAzureSubscriptionUtilization.cs

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

Az Azure-beli kihasználtsági rekordok beszerzéséhez először egy ügyfél-azonosítóra és egy előfizetés-azonosítóra van szükség. Ezután meg kell hívnia az **IAzureUtilizationCollection.query** függvényt, hogy visszaadja a kihasználtsági rekordokat tartalmazó **ResourceCollection** adatokat. Mivel az erőforrás-gyűjtemény lapozódva van, be kell szereznie egy Azure-beli kihasználtságirekord-enumerátort a kihasználtsági oldalakon való áthaladáshoz.

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

Az Azure-beli kihasználtsági rekordok beszerzéséhez először egy ügyfél-azonosítóra és egy előfizetés-azonosítóra van szükség. Ezután hívja meg a [**Get-PartnerCustomerSubscriptionUtilization függvényt.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md) Ez a parancs a megadott időszakban elérhető összes rekordot visszaadja.

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus | Kérés URI-ja |
|------- | ----------- |
| **Kap** | *{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/utilizations/azure?start \_ time={start-time}&\_ end-time={end-time}&granularity={granularity}&show \_ details={True} |

#### <a name="uri-parameters"></a>URI-paraméterek

Az alábbi elérési út és lekérdezési paraméterek használatával lekérdezheti a kihasználtsági rekordokat.

| Név | Típus | Kötelező | Leírás |
| ---- | ---- | -------- | ----------- |
| ügyfél-bérlő-azonosító | sztring | Yes | Egy GUID formátumú sztring, amely azonosítja az ügyfelet. |
| subscription-id | sztring | Yes | Egy GUID-formátumú sztring, amely azonosítja az előfizetést. |
| start_time | sztring UTC dátum-idő eltolási formátumban | Yes | Annak az időtartománynak a kezdete, amely a kihasználtság számlázási rendszerben való jelentésének idejét jelöli. |
| end_time | sztring UTC dátum-idő eltolási formátumban | Yes | Annak az időtartománynak a vége, amely a kihasználtság számlázási rendszerben való jelentésének idejét jelöli. |
| Finomsága | sztring | No | Meghatározza a használati aggregációk részletességét. Az elérhető lehetőségek: `daily` (alapértelmezett) és `hourly` .
| show_details | boolean | No | Megadja, hogy a rendszer le tudja-e szerezni a példányszintű használati adatokat. A mező alapértelmezett értéke: `true`. |
| size | szám | No | Az egyetlen API-hívás által visszaadott aggregációk számát adja meg. Az alapértelmezett érték 1000. A maximális érték 1000. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek

### <a name="request-example"></a>Példa kérésre

A következő példakérés a 7/2–8/1 időszakban az egyeztetési fájlhoz hasonló eredményeket ad vissza. Előfordulhat, hogy ezek az eredmények nem egyeznek meg pontosan (a részletekért lásd az [Azure utilization API szakaszt).](#azure-utilization-api)

Ez a példakérés a számlázási rendszerben jelentett kihasználtsági adatokat adja vissza 7/2 időpontban (UTC) 12:00-kor (UTC) és 8/2 időpontban(UTC) 12:00-kor.

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

Ha a művelet sikeres, ez a metódus az [Azure-beli kihasználtsági](azure-utilization-record-resources.md) rekord erőforrásainak gyűjteményét adja vissza a válasz törzsében. Ha az Azure-kihasználtsági adatok még nem állnak készen egy függő rendszerben, ez a metódus egy 204-es HTTP-állapotkódot ad vissza egy Retry-After fejléccel.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Egy hálózati nyomkövetési eszközzel olvassa be a HTTP-állapotkódot, a [hibakód típusát](error-codes.md)és a további paramétereket.

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
