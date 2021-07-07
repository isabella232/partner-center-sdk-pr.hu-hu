---
title: Ügyfélfiók törlése az integrációs tesztkörnyezetből
description: Ügyfélfiók törlése a Tesztelés éles környezetben (Tipp) integrációs tesztkészletből.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9d9e44ac9c40bd4e3c7e1a9e04253f853dfd96c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973128"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a>Ügyfélfiók törlése az integrációs tesztkörnyezetből

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Ez a cikk azt ismerteti, hogyan lehet megszakítani a partner és az ügyfélfiók közötti kapcsolatot, és vissza lehet szerezni a tesztelési kvótát éles környezetben (Tipp) az integrációs tesztkészletben.

> [!IMPORTANT]
> Amikor töröl egy ügyfélfiókot, az adott ügyfélbérlőhöz társított összes erőforrás törölve lesz.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Minden Azure Reserved Virtual Machine Instances és szoftvervásárlási rendelést meg kell szakítani, mielőtt törölné az ügyfelet a Tipp integrációs védőfalból.

## <a name="c"></a>C\#

Ügyfél törlése a Tipp integrációs védőfalból:

1. Adja át Tipp-fiókja hitelesítő adatait a [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metódusnak, hogy [**IPartner-felületet**](/dotnet/api/microsoft.store.partnercenter.ipartner) kapjon a partneri műveletekhez.

2. A partner műveleti felületén lekéri a jogosultságok gyűjteményét:

    1. Az ügyfél megadásához hívja meg a [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfélazonosítóval.

    2. Hívja meg **a Jogosultságok tulajdonságot.**

    3. Hívja meg **a Get** vagy **GetAsync metódust** a jogosultsággyűjtemény [**lekéréséhez.**](entitlement-resources.md)

3. Győződjön meg arról, Azure Reserved Virtual Machine Instances ügyfél összes rendelése és szoftvervásárlási rendelése törölve lett. A gyűjtemény [**minden egyes jogosultsága**](entitlement-resources.md) esetén:

    1. Használja a [**jogosultságot. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) le kell szereznie a megfelelő [](order-resources.md#order) rendelés helyi másolatát az ügyfél rendelésgyűjteményéből.

    2. Állítsa az [**Order.Status**](order-resources.md#order) tulajdonságot "Megszakítva" állapotra.

    3. Frissítse a sorrendet a **Patch()** metódussal.

4. Az összes rendelés visszavonása. A következő kódminta például egy ciklussal lekérdezi az egyes rendeléseket, amíg az állapota "Cancelled" (Megszakítva) nem lesz.

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be canceled.
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
        // Check if all the orders were canceled.
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

5. Az ügyfél Delete metódusának hívásával győződjön meg arról, hogy minden rendelés vissza lett szakítva. 

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont PartnerCenterSDK.FeaturesSamples **osztály:** DeleteCustomerFromTipAccount.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus     | Kérés URI-ja                                                                            |
|------------|----------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

Az alábbi lekérdezési paraméterrel törölhet egy ügyfelet.

| Név                   | Típus     | Kötelező | Leírás                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| ügyfél-bérlő-azonosító     | GUID     | Y        | Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Sikeres művelet esetén ez a metódus üres választ ad vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
