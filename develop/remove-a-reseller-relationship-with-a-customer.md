---
title: Ügyféllel létesítendő viszonteladói kapcsolat eltávolítása
description: Hogyan távolítható el egy viszonteladói kapcsolat egy olyan ügyféllel, akinél már nincsenek tranzakciók.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: bcfba544bd1647ba0f3eb360d5ace14c7223b38837cb858198cf95c4e82dd594
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997073"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>Ügyféllel létesítendő viszonteladói kapcsolat eltávolítása

Távolítsa el a viszonteladói kapcsolatot egy olyan ügyféllel, akinél már nincsenek tranzakciók.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- A viszonteladói kapcsolat eltávolítása előtt minden Azure Reserved VM Instance-rendelést meg kell szakítani. Hívja Azure-támogatás az azure-beli fenntartott virtuálisgép-példányok nyitott rendeléseit.

## <a name="c"></a>C\#

Az ügyfél viszonteladói kapcsolatának eltávolításához először győződjön meg arról, hogy az adott ügyfélhez Azure Reserved VM Instances összes aktív kapcsolat törlődik. Ezután győződjön meg arról, hogy az ügyfél összes aktív előfizetése fel van függesztve. Ez annak az ügyfélnek az azonosítóját határozza meg, aki számára törölni szeretné a viszonteladói kapcsolatot. Az alábbi példakódban a rendszer felkéri a felhasználót, hogy adja meg az ügyfél azonosítóját.

Annak megállapításához, hogy az ügyfél bármely Azure Reserved VM Instances-ját meg kell-e szakítani, a jogosultságok gyűjtésének lekéréséhez hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójának használatával az ügyfél azonosítójának megadásával, valamint a [**Jogosultságok**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot a jogosultsággyűjtési műveletek felületének lekéréséhez. A [**jogosultsággyűjtemény lekéréséhez**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) hívja meg a Get vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) metódust. Szűrje a gyűjteményt minden jogosultságra az [**EntitlementType.VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) [**entitlementType**](entitlement-resources.md#entitlementtype) értékével, és ha van ilyen, a folytatás előtt hívja meg az ügyfélszolgálatot.

Ezután az ügyfél előfizetési gyűjteményének lekéréséhez hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójának használatával az ügyfél megadásához, valamint az [**Előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot az előfizetés-gyűjtési műveletek interfészének lekéréséhez. Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) metódust az ügyfél előfizetés-gyűjteményének lekéréséhez. Az előfizetés-gyűjtemény bejárásával győződjön meg arról, hogy egyik előfizetés sem rendelkezik [**SubscriptionStatus.Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) [**SubscriptionStatus.Status tulajdonságértékkel.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus) Ha egy előfizetés még aktív, a felfüggesztésével kapcsolatos információkért [lásd:](suspend-a-subscription.md) Előfizetés felfüggesztése.

Miután meggyőződött arról, hogy Azure Reserved VM Instances ügyfél összes aktív előfizetése törölve lett, és az összes aktív előfizetés fel van függesztve, eltávolíthatja az ügyfél viszonteladói kapcsolatát. Először hozzon létre egy új [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) objektumot a [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) tulajdonság [**customerPartnerRelationship.None beállításával.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship) Ezután az ügyfél azonosítójának használatával hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust, és hívja meg a **Patch** metódust az új ügyfélobjektum átadásával.

A kapcsolat ismételt létrehozása érdekében ismételje meg [viszonteladói kapcsolat kérése/partnerközpont/develop/request-reseller-relationship).

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

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: PartnerSDK.FeatureSample **osztály:** DeletePartnerCustomerRelationship.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus     | Kérés URI-ja                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **Javítás**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja a viszonteladói kapcsolatok eltávolításához szükséges lekérdezési paramétereket.

| Név                   | Típus     | Kötelező | Leírás                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

A **kérelem** törzsében szükség van egy Ügyfélerőforrásra. Győződjön meg arról, hogy a **RelationshipToPartner** tulajdonság nincsre van beállítva.

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

Ha ez a módszer sikeres, eltávolítja a megadott ügyfél viszonteladói kapcsolatát.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
