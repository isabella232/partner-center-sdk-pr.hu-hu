---
title: Ügyféllel létesítendő viszonteladói kapcsolat eltávolítása
description: Viszonteladói kapcsolat eltávolítása olyan ügyféllel, amelyhez már nincs tranzakció.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 084797997e57c63b5c447379bb08ecb88ebd0cc4
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768276"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>Ügyféllel létesítendő viszonteladói kapcsolat eltávolítása

**A következőkre vonatkozik**

- Partnerközpont

Távolítson el egy viszonteladói kapcsolatot egy ügyféllel, amelyhez már nincs tranzakció.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Az összes Azure-beli fenntartott VM-példányra vonatkozó rendelést meg kell szüntetni a viszonteladói kapcsolat eltávolítása előtt. Az Azure-támogatás meghívásával megszakíthatja az Azure-beli fenntartott VM-példányok megrendeléseit.

## <a name="c"></a>C\#

Az ügyfél viszonteladói kapcsolatának eltávolításához először győződjön meg arról, hogy az ügyfélhez tartozó összes aktív Azure Reserved VM Instances meg lett szakítva. Ezután győződjön meg arról, hogy az ügyfél összes aktív előfizetése fel van függesztve. Ehhez meg kell határozni annak az ügyfélnek az AZONOSÍTÓját, akinek törölni szeretné a viszonteladói kapcsolatot. A következő kódrészletben a rendszer kéri a felhasználótól, hogy adja meg az ügyfél-azonosítót.

Annak megállapításához, hogy az ügyfélhez tartozó összes Azure Reserved VM Instances meg kell-e szakítani, le kell kérnie a jogosultságok gyűjteményét a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódus meghívásával az ügyfél azonosítójának megadásával, és a [**jogosultságok**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, hogy lekérje a jogosultságok gyűjtési műveleteihez szükséges felületet. A jogosultságok gyűjtésének lekéréséhez hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) metódust. Szűrje a gyűjteményt minden olyan jogosultsághoz, amely a [**EntitlementType. VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) [**EntitlementType**](entitlement-resources.md#entitlementtype) értékkel rendelkezik, és ha vannak ilyenek, a folytatás előtt a támogatás hívásával szakítsa meg őket.

Ezután kérje le az ügyfél-előfizetések gyűjteményét úgy, hogy meghívja a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél megadásához, és az [**előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, amely az előfizetés-gyűjtési műveletekhez felületet kér le. Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) metódust az ügyfél előfizetések gyűjteményének lekéréséhez. Az előfizetés bejárásával ellenőrizze, hogy az előfizetések egyike sem rendelkezik [**előfizetésekkel. status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) tulajdonság értéke [**SubscriptionStatus. Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus). Ha egy előfizetés még aktív, tekintse meg az [előfizetés felfüggesztése](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) című témakört, amelyből megtudhatja, hogyan felfüggesztheti.

Miután megerősítette, hogy az ügyfél összes aktív Azure Reserved VM Instancesa meg lett szakítva, és az összes aktív előfizetés fel van függesztve, eltávolíthatja az ügyfél viszonteladói kapcsolatát. Először hozzon létre egy új [Customer/DotNet/API/Microsoft. Store. partnercenter. models. Customs. Customer "objektumot a [Customer. RelationshipToPartner/DotNet/API/Microsoft. Store. partnercenter. models. customers. Customer. RelationshipToPartner) tulajdonsággal, amely a [**CustomerPartnerRelationship. None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship)értékre van beállítva. Ezután hívja meg a [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosító használatával az ügyfél megadásához, és hívja meg a **patch** metódust, amely az új ügyfél objektumba kerül.

A kapcsolat újbóli létrehozásához ismételje meg a [viszonteladói kapcsolat/partner-központ/fejlesztés/kérelem-viszonteladói kapcsolat kérése) folyamatát.

``` csharp
// IAggregatePartner partnerOperations;

// Prompt the user the enter the customer ID.
var customerIdToDeleteRelationshipOf = this.Context.ConsoleHelper.ReadNonEmptyString("Please enter the ID of the customer you want to delete the relationship with", "The customer ID can't be empty");

// Determine if there are any active Azure Reserved VM Instances for this customer.
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Entitlements.Get();

If (entitlements.Items.Where(x => x.EntitlementType == EntitlementType.VirtualMachineReservedInstance).Any())
{
    this.Context.ConsoleHelper.Warning("Please cancel Azure Reserved Virtual Machine Instance orders through support and try again. Aborting the delete customer relationship operation");
               return;
}

// Verify that there are no active subscriptions.
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Subscriptions.Get();
IList<Subscription> subscriptions = new List<Subscription>(customerSubscriptions.Items);

foreach (Subscription customerSubscription in subscriptions)
{
    if (customerSubscription.Status == SubscriptionStatus.Active)
    {
        this.Context.ConsoleHelper.Warning(String.Format("Subscription with ID :{0}  OfferName: {1} cannot be in active state, ", customerSubscription.Id, customerSubscription.OfferName));
        this.Context.ConsoleHelper.Warning("Please Suspend all the Subscriptions and try again. Aborting the delete customer relationship operation");
               return;
    }
}

// Delete the customer's relationship to the partner.
Customer customer = new Customer();
customer.RelationshipToPartner = CustomerPartnerRelationship.None;
customer = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Patch(customer);

if (customer.RelationshipToPartner == CustomerPartnerRelationship.None)
{
    this.Context.ConsoleHelper.Success("Customer Partner Relationship successfully deleted");
}
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: PartnerSDK. FeatureSample **osztály**: DeletePartnerCustomerRelationship.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus     | Kérés URI-ja                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **JAVÍTÁS**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat a viszonteladói kapcsolat eltávolításához szükséges lekérdezési paramétereket sorolja fel.

| Név                   | Típus     | Kötelező | Leírás                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **ügyfél – bérlő – azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlő-azonosító** , amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

A kérés törzsében meg kell adni egy **ügyfél** -erőforrást. Győződjön meg arról, hogy a **RelationshipToPartner** tulajdonság értéke NONE.

### <a name="request-example"></a>Példa kérésre

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Content-Length: 74
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
MS-RequestId: 9fef8b23-6e3e-45d2-8678-e9fe89c35af5
Date: Fri, 12 Jan 2018 00:31:55 GMT

{
    "relationshipToPartner":"none",
    "attributes":{
        "objectType":"Customer"
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus eltávolítja a viszonteladói kapcsolatot a megadott ügyfél számára.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
MS-RequestId: 7988dde4-b516-472c-b226-6d53fb18f04e
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
X-Locale: en-US
Content-Type: application/json
Content-Length: 242
Expect: 100-continue

{
    "Id":null,
    "CommerceId":null,
    "CompanyProfile":null,
    "BillingProfile":null,
    "RelationshipToPartner":"none",
    "AllowDelegatedAccess":null,
    "UserCredentials":null,
    "CustomDomains":null,
    "AssociatedPartnerId":null,
    "Attributes":{
        "ObjectType":"Customer"
    }
}
```
