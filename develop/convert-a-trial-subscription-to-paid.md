---
title: Próbaverziós előfizetés átalakítása fizetőssé
description: Ismerje meg, hogyan alakíthatja át a próbaverziós előfizetéseket a partner Center API-kkal a fizetős verzióra.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 59dcf6caf21d407b2fba4cc8438bc435fda9dc77
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768584"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a>Próbaverziós előfizetés átalakítása a partner Center API-k használatával

**A következőkre vonatkozik:**

- Partnerközpont

A próbaverziós előfizetés kifizetésre konvertálható.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Egy aktív próbaverziós előfizetés előfizetési azonosítója.

- Egy elérhető konverziós ajánlat.

## <a name="convert-a-trial-subscription-to-paid-through-code"></a>Próbaverziós előfizetés átalakítása kóddal való fizetésre

A próbaverziós előfizetés fizetős verzióra való átalakításához először be kell szereznie az elérhető próbaverziók gyűjteményét. Ezután ki kell választania a megvásárolni kívánt átalakítási ajánlatot.

Az átalakítási ajánlatok olyan mennyiséget határoznak meg, amely alapértelmezés szerint ugyanannyi licenccel rendelkezik, mint a próbaverziós előfizetés. Ezt a mennyiséget úgy módosíthatja, hogy a [**mennyiségi**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) tulajdonságot a megvásárolni kívánt licencek számára állítja be.

> [!NOTE]
> A megvásárolt licencek számától függetlenül a rendszer újra felhasználja a próbaverzió előfizetés-AZONOSÍTÓját a megvásárolt licencek esetében. Ennek eredményeképpen a próbaverzió eltűnik, és a vásárlás helyébe lép.

A próbaverziós előfizetés kód használatával történő átalakításához kövesse az alábbi lépéseket:

1. Szerezzen be egy felületet az elérhető előfizetési műveletekhez. Azonosítania kell az ügyfelet, és meg kell adnia a próbaverziós előfizetés előfizetés-azonosítóját.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. Szerezze be az elérhető átalakítási ajánlatok gyűjteményét. További információt és a módszerre vonatkozó kérés/válasz részleteit itt tekintheti meg: a [próbaverziós konvertálási ajánlatok listájának beolvasása](get-a-list-of-trial-conversion-offers.md).

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. Válasszon egy átalakítási ajánlatot. A következő kód kiválasztja a gyűjtemény első átalakítási ajánlatát.

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. Igény szerint megadhatja a megvásárolni kívánt licencek számát. Az alapértelmezett érték a próbaverziós előfizetésben található licencek száma.

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. A [**create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) metódus meghívásával konvertálja a próbaverziós előfizetést fizetettre.

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>C\#

Próbaverziós előfizetés átalakítása fizetős verzióra:

1. Az ügyfél azonosításához használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval.

2. Az előfizetések [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódus meghívása a próbaverziós előfizetés-azonosítóval az előfizetési műveletek eléréséhez. Egy helyi változóban mentheti az előfizetés-üzemeltetési felületre mutató hivatkozást.

3. Az [**átalakítások**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) [**tulajdonsággal**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) szerezzen be egy felületet az elérhető műveletekhez a konverziók között, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) metódust a rendelkezésre álló konverziós ajánlatok gyűjteményének lekéréséhez. Ki kell választania egyet. A következő példa a rendelkezésre álló első konverziót alapértelmezett értékre vált.

4. Használja az előfizetési műveletek felületét, amelyet egy helyi változóban és a [**konverziók**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) tulajdonságban mentett, hogy az elérhető műveletekhez csatolót szerezzen be a konverziók között.

5. A próbaverzió átalakításának megkísérlése érdekében adja át a kiválasztott átalakítási ajánlat objektumát a [**create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) metódusnak.

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

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/Conversions http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az ügyfél és a próbaverzió előfizetésének azonosításához használja a következő elérésiút-paramétereket.

| Név            | Típus   | Kötelező | Leírás                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| ügyfél-azonosító     | sztring | Igen      | Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.           |
| előfizetés-azonosító | sztring | Igen      | Egy GUID formátumú karakterlánc, amely azonosítja a próba-előfizetést. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

A kérelem törzsében szerepelnie kell egy feltöltött [konverziós](conversions-resources.md#conversion) erőforrásnak.

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

Ha ez sikeres, a válasz törzse [ConversionResult](conversions-resources.md#conversionresult) -erőforrást tartalmaz.

#### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).

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
