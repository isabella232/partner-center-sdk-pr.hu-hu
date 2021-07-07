---
title: Próbaverziós előfizetés átalakítása fizetőssé
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat a próba-előfizetés fizetős előfizetésre való átalakításához.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1876cfc796b683bfff00b7d137bcfe0b7162c78
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973859"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a>Próba-előfizetés konvertálása fizetősre Partnerközpont API-k használatával

A próba-előfizetéseket fizetősre konvertálhatja.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Egy aktív próba-előfizetés előfizetés-azonosítója.

- Egy elérhető konverziós ajánlat.

## <a name="convert-a-trial-subscription-to-a-paid-subscription-through-code"></a>Próbaverziós előfizetés konvertálása fizetős előfizetésre kóddal

A próba-előfizetés fizetősre való konvertálásához először be kell szereznie az elérhető próbaverziós konverziók gyűjteményét. Ezután ki kell választania a megvásárolni kívánt átváltási ajánlatot.

Az átváltási ajánlatok olyan mennyiséget határoznak meg, amely alapértelmezés szerint a próbaverziós előfizetéssel azonos számú licencre van beállítva. Ezt a mennyiséget módosíthatja, ha a [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) tulajdonságot a megvásárolni kívánt licencek számára módosítja.

> [!NOTE]
> A megvásárolt licencek számától függetlenül a próbaidőszak előfizetés-azonosítója a megvásárolt licencekhez lesz újra felhasználva. Ennek eredményeképpen a próbaverzió eltűnik, és a vásárlás váltja fel.

Próbaverziós előfizetés kódon keresztüli konvertálásához kövesse az alábbi lépéseket:

1. Szerezze be az elérhető előfizetési műveletek felületét. Azonosítania kell az ügyfelet, és meg kell adnia a próba-előfizetés előfizetés-azonosítóját.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. Szerezze be az elérhető konverziós ajánlatok gyűjteményét. A metódus kérésével/válaszával kapcsolatos további információkért lásd: Próbaverziós konverziós [ajánlatok listájának lekérése.](get-a-list-of-trial-conversion-offers.md)

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. Válasszon egy konverziós ajánlatot. A következő kód a gyűjtemény első konverziós ajánlatát választja ki.

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. Megadhatja a megvásárolni kívánt licencek számát is. Az alapértelmezett érték a próbaverziós előfizetésben elérhető licencek száma.

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. A [**próba-előfizetés**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) fizetősre konvertálásához hívja meg a Create vagy [**a CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) metódust.

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>C\#

Próbaverziós előfizetés fizetősre konvertálása:

1. Az ügyfél azonosításához használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával.

2. Az előfizetési műveletek interfészének lehívásához hívja meg a [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust a próba-előfizetés azonosítójával. Mentse az előfizetési műveleti felület hivatkozását egy helyi változóban.

3. A [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) tulajdonság használatával szerezzen be egy felületet az elérhető konverziós műveletekhez, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) metódust az elérhető konverziós ajánlatok [**gyűjteményének lekéréséhez.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) Ki kell választania egyet. Az alábbi példa alapértelmezés szerint az első elérhető konverziót használja.

4. A helyi változóba mentett előfizetési műveleti felületre és a [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) tulajdonságra való hivatkozással szerezzen be egy interfészt az átalakításkor elérhető műveletekhez.

5. A próbakonverzió megkísérlése érdekében adja át a kiválasztott konverziós ajánlat objektumát a [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) vagy [**a CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) metódusnak.

### <a name="c-example"></a>C \# példa

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get subscription operations for the trial subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the available conversions.
var conversions = subscriptionOperations.Conversions.Get();

// If there are no conversions available, we&#39;re done.
// Otherwise, convert the trial to the first available conversion offer.
if (conversions.TotalCount <= 0)
{
    System.Console.WriteLine("This subscription has no conversions");
}
else
{
    // Default to the first conversion.
    var selectedConversion = conversions.Items.ToList()[0];

    // Convert the trial and return the result.
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
}
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus   | Kérés URI-ja                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/konverziós HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az alábbi elérésiút-paraméterekkel azonosíthatja az ügyfelet és a próbaverziós előfizetést.

| Név            | Típus   | Kötelező | Leírás                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| ügyfélazonosító     | sztring | Igen      | Egy GUID formátumú sztring, amely azonosítja az ügyfelet.           |
| subscription-id | sztring | Igen      | A próba-előfizetést azonosító GUID formátumú sztring. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

A kérelem [törzsében](conversions-resources.md#conversion) szerepelnie kell egy feltöltéses konverziós erőforrásnak.

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 234
Expect: 100-continue

{
    "OfferId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "TargetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "OrderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
    "Quantity": 25,
    "BillingCycle": "monthly",
    "Attributes": {
        "ObjectType": "Conversion"
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse tartalmaz egy [ConversionResult erőforrást.](conversions-resources.md#conversionresult)

#### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

#### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 211
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CV: kW4GzmhvHEqCq1ls.0
MS-ServerId: 030020643
Date: Thu, 15 Jun 2017 23:10:40 GMT

 {
    "subscriptionId": "488745B5-2086-4912-802C-6ABB9F7C3638",
    "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "attributes": {
        "objectType": "ConversionResult"
    }
}
```
