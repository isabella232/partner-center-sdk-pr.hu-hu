---
title: Ügyfélfiók törlése az integrációs tesztkörnyezetből
description: Felhasználói fiók törlése a tesztelés éles környezetben (tip) integrációs munkaterületen.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e3a1642c0202c174ddd4f65a6aeda2752def9176
ms.sourcegitcommit: b1ff781b67b1d322820bbcac2c583229201a8c07
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2020
ms.locfileid: "97768156"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a>Ügyfélfiók törlése az integrációs tesztkörnyezetből

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ez a cikk ismerteti a partner és az ügyfél közötti kapcsolat bontását, és visszanyeri a kvótát az üzemi (tip) integrációs munkaterületre való teszteléshez.

> [!IMPORTANT]
> Ha töröl egy ügyfél-fiókot, az ügyfél-bérlőhöz társított összes erőforrás törlődni fog.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Az összes Azure Reserved Virtual Machine Instances-és szoftver-beszerzési rendelést meg kell szüntetni, mielőtt törölné egy ügyfelet a tip Integration sandbox-ból.

## <a name="c"></a>C\#

Ügyfél törlése a tipp-integrációs homokozóból:

1. Adja át a tip-fiókja hitelesítő adatait a [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metódusnak, hogy [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) felületet kapjon a partneri műveletekhez.

2. A jogosultságok gyűjteményének lekéréséhez használja a partner műveleti felületet:

    1. Az ügyfél megadásához hívja meg a [**customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval.

    2. Hívja meg a **jogosultságok** tulajdonságot.

    3. A [**jogosultságok**](entitlement-resources.md) gyűjtésének lekéréséhez hívja meg a **Get** vagy a **GetAsync** metódust.

3. Győződjön meg arról, hogy az ügyfél összes Azure Reserved Virtual Machine Instances és szoftveres beszerzési rendelése meg lett szakítva. A gyűjtemény minden [**jogosultságához**](entitlement-resources.md) :

    1. Használja a [**jogosultságot. A ReferenceOrder.Id**](entitlement-resources.md#referenceorder) a megfelelő [rendelés](order-resources.md#order) helyi másolatát kapja meg az ügyfél rendeléseinek gyűjteményéből.

    2. Állítsa a [**Order. status**](order-resources.md#order) tulajdonságot "megszakítva" értékre.

    3. A **javítás ()** metódus használatával frissítse a sorrendet.

4. Az összes megrendelés megszakítása. Az alábbi mintakód például egy hurkot használ az egyes sorrendek lekérdezéséhez, amíg az állapota "megszakítva".

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be cancelled.
    ResourceCollection<Entitlement> entitlements = tipAccountPartnerOperations.Customers.ById(customerTenantId).Entitlements.Get();

    // Cancel all orders
    foreach (var entitlement in entitlements)
    {
        var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
        order.Status = "Cancelled";
        order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(order.Id).Patch(order);
    }

    // Keep polling until the status of all orders is "Cancelled".
    bool proceed = true;
    do
    {
        // Check if all the orders were cancelled.
        foreach (var entitlement in entitlements)
        {
            var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
            if (!order.Status.Equals("Cancelled", StringComparison.OrdinalIgnoreCase))
            {
                proceed = false;
            }
        }

        // Wait for a few seconds.
        Thread.Sleep(5000);
    }
    while (proceed == false);

    tipAccountPartnerOperations.Customers.ById(customerTenantId).Delete();
    ```

5. Győződjön meg arról, hogy az összes megrendelést megszakította az ügyfél **törlési** metódusának meghívásával.

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center PartnerCenterSDK. FeaturesSamples **osztály**: DeleteCustomerFromTipAccount.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus     | Kérés URI-ja                                                                            |
|------------|----------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID} http/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

Az ügyfél törléséhez használja a következő lekérdezési paramétert.

| Név                   | Típus     | Kötelező | Leírás                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| ügyfél – bérlő – azonosító     | GUID     | Y        | Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a metódus üres választ ad vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
