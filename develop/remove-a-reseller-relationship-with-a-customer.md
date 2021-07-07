---
title: Ügyféllel létesítendő viszonteladói kapcsolat eltávolítása
description: Hogyan távolítható el egy viszonteladói kapcsolat egy olyan ügyféllel, akinél már nincsenek tranzakciók.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 45eca3564c3b9078e04d1f8155d08849a589d52f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446598"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a><span data-ttu-id="dd3ba-103">Ügyféllel létesítendő viszonteladói kapcsolat eltávolítása</span><span class="sxs-lookup"><span data-stu-id="dd3ba-103">Remove a reseller relationship with a customer</span></span>

<span data-ttu-id="dd3ba-104">Távolítsa el a viszonteladói kapcsolatot egy olyan ügyféllel, akinél már nincsenek tranzakciók.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-104">Remove a reseller relationship with a customer that you no longer have transactions with.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd3ba-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="dd3ba-105">Prerequisites</span></span>

- <span data-ttu-id="dd3ba-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="dd3ba-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dd3ba-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="dd3ba-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="dd3ba-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="dd3ba-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="dd3ba-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="dd3ba-110">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="dd3ba-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="dd3ba-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="dd3ba-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="dd3ba-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="dd3ba-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="dd3ba-113">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="dd3ba-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="dd3ba-114">A viszonteladói kapcsolat eltávolítása előtt minden Azure Reserved VM Instance-rendelést meg kell szakítani.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-114">All Azure Reserved VM Instance orders must be canceled before a reseller relationship is removed.</span></span> <span data-ttu-id="dd3ba-115">Hívja Azure-támogatás az azure-beli fenntartott virtuálisgép-példányok nyitott rendeléseit.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-115">Call Azure support for canceling any open Azure Reserved VM Instance orders.</span></span>

## <a name="c"></a><span data-ttu-id="dd3ba-116">C\#</span><span class="sxs-lookup"><span data-stu-id="dd3ba-116">C\#</span></span>

<span data-ttu-id="dd3ba-117">Az ügyfél viszonteladói kapcsolatának eltávolításához először győződjön meg arról, hogy az adott ügyfél Azure Reserved VM Instances összes aktív kapcsolata törölve lett.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-117">To remove the reseller relationship for a customer, first ensure that any active Azure Reserved VM Instances for that customer are canceled.</span></span> <span data-ttu-id="dd3ba-118">Ezután győződjön meg arról, hogy az ügyfél összes aktív előfizetése fel van függesztve.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-118">Next, ensure that all active subscriptions for that customer are suspended.</span></span> <span data-ttu-id="dd3ba-119">Ezt annak az ügyfélnek az azonosítójával kell meghatározni, aki számára törölni szeretné a viszonteladói kapcsolatot.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-119">To do so, determine the ID of the customer for whom you want to delete the reseller relationship.</span></span> <span data-ttu-id="dd3ba-120">A következő példakódban a rendszer felkéri a felhasználót, hogy adja meg az ügyfél azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-120">In the following code example, the user is prompted to provide the customer identifier.</span></span>

<span data-ttu-id="dd3ba-121">Annak megállapításához, hogy az ügyfél bármely Azure Reserved VM Instances-ját meg kell-e szakítani, a jogosultságok gyűjtésének lekéréséhez hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójának használatával, és a [**Jogosultságok**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot a jogosultsággyűjtési műveletek felületének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-121">To determine if any Azure Reserved VM Instances for the customer must be canceled, retrieve the collection of entitlements by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to entitlement collection operations.</span></span> <span data-ttu-id="dd3ba-122">A [**jogosultsággyűjtemény lekéréséhez**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) hívja meg a Get vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the entitlement collection.</span></span> <span data-ttu-id="dd3ba-123">Szűrje a gyűjteményt az esetleges jogosultságok esetében az [**EntitlementType.VirtualMachineReservedInstance értékre,**](entitlement-resources.md#entitlementtype) és ha vannak, a folytatás előtt hívja meg az ügyfélszolgálatot. [](entitlement-resources.md#entitlementtype)</span><span class="sxs-lookup"><span data-stu-id="dd3ba-123">Filter the collection for any entitlements with an [**EntitlementType**](entitlement-resources.md#entitlementtype) value of [**EntitlementType.VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) and if there are any, cancel them by calling support before proceeding.</span></span>

<span data-ttu-id="dd3ba-124">Ezután az ügyfél-előfizetések gyűjteményének lekéréséhez hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójának használatával az ügyfél megadásához, valamint az [**Előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot az előfizetés-gyűjtési műveletek interfészének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-124">Then, retrieve a collection of the customer's subscriptions by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="dd3ba-125">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) metódust az ügyfél előfizetési gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-125">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the customer's subscriptions collection.</span></span> <span data-ttu-id="dd3ba-126">Az előfizetés-gyűjtemény bejárásával győződjön meg arról, hogy egyik előfizetés sem rendelkezik [**SubscriptionStatus.Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) [**SubscriptionStatus.Status tulajdonságértékkel.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)</span><span class="sxs-lookup"><span data-stu-id="dd3ba-126">Traverse the subscription collection and ensure that none of the subscriptions have a [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property value of [**SubscriptionStatus.Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="dd3ba-127">Ha egy előfizetés még aktív, az előfizetés felfüggesztése részt [a](suspend-a-subscription.md) felfüggesztésével kapcsolatos információkért tekintse meg.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-127">If a subscription is still active, see [Suspend a subscription](suspend-a-subscription.md) for information on how to suspend it.</span></span>

<span data-ttu-id="dd3ba-128">Miután meggyőződött arról, Azure Reserved VM Instances ügyfél összes aktív előfizetése törölve lett, és az összes aktív előfizetés fel van függesztve, eltávolíthatja az ügyfél viszonteladói kapcsolatát.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-128">After confirming that all active Azure Reserved VM Instances for that customer are canceled and all active subscriptions are suspended, you can remove the reseller relationship for the customer.</span></span> <span data-ttu-id="dd3ba-129">Először hozzon létre egy új [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) objektumot a [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) tulajdonság [**CustomerPartnerRelationship.None beállításával.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship)</span><span class="sxs-lookup"><span data-stu-id="dd3ba-129">First, create a new [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object with the [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) property set to [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span></span> <span data-ttu-id="dd3ba-130">Ezután hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójának használatával az ügyfél megadásához, majd hívja meg a **Patch** metódust az új ügyfélobjektum átadásával.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-130">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and call the **Patch** method, passing in the new customer object.</span></span>

<span data-ttu-id="dd3ba-131">A kapcsolat ismételt létrehozására ismételje meg a ([viszonteladói kapcsolat/partnerközpont/develop/request-reseller-relationship) folyamatot.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-131">To re-establish the relationship, repeat the process of [requesting a reseller relationship/partner-center/develop/request-reseller-relationship).</span></span>

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

<span data-ttu-id="dd3ba-132">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="dd3ba-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="dd3ba-133">**Project**: PartnerSDK.FeatureSample **osztály:** DeletePartnerCustomerRelationship.cs</span><span class="sxs-lookup"><span data-stu-id="dd3ba-133">**Project**: PartnerSDK.FeatureSample **Class**: DeletePartnerCustomerRelationship.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="dd3ba-134">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="dd3ba-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dd3ba-135">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="dd3ba-135">Request syntax</span></span>

| <span data-ttu-id="dd3ba-136">Metódus</span><span class="sxs-lookup"><span data-stu-id="dd3ba-136">Method</span></span>     | <span data-ttu-id="dd3ba-137">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="dd3ba-137">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dd3ba-138">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="dd3ba-138">**PATCH**</span></span>  | <span data-ttu-id="dd3ba-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="dd3ba-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="dd3ba-140">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="dd3ba-140">URI parameter</span></span>

<span data-ttu-id="dd3ba-141">Ez a táblázat felsorolja a viszonteladói kapcsolatok eltávolításához szükséges lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-141">This table lists the required query parameters to remove a reseller relationship.</span></span>

| <span data-ttu-id="dd3ba-142">Név</span><span class="sxs-lookup"><span data-stu-id="dd3ba-142">Name</span></span>                   | <span data-ttu-id="dd3ba-143">Típus</span><span class="sxs-lookup"><span data-stu-id="dd3ba-143">Type</span></span>     | <span data-ttu-id="dd3ba-144">Kötelező</span><span class="sxs-lookup"><span data-stu-id="dd3ba-144">Required</span></span> | <span data-ttu-id="dd3ba-145">Leírás</span><span class="sxs-lookup"><span data-stu-id="dd3ba-145">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="dd3ba-146">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="dd3ba-146">**customer-tenant-id**</span></span> | <span data-ttu-id="dd3ba-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="dd3ba-147">**guid**</span></span> | <span data-ttu-id="dd3ba-148">Y</span><span class="sxs-lookup"><span data-stu-id="dd3ba-148">Y</span></span>        | <span data-ttu-id="dd3ba-149">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-149">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="dd3ba-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="dd3ba-150">Request headers</span></span>

<span data-ttu-id="dd3ba-151">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="dd3ba-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dd3ba-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="dd3ba-152">Request body</span></span>

<span data-ttu-id="dd3ba-153">A **kérelem** törzsében szükség van egy ügyfélerőforrásra.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-153">A **Customer** resource is required in the request body.</span></span> <span data-ttu-id="dd3ba-154">Ellenőrizze, hogy **a RelationshipToPartner** tulajdonság nincs-e beállítva.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-154">Ensure the **RelationshipToPartner** property has been set to none.</span></span>

### <a name="request-example"></a><span data-ttu-id="dd3ba-155">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="dd3ba-155">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="dd3ba-156">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="dd3ba-156">REST response</span></span>

<span data-ttu-id="dd3ba-157">Ha ez a módszer sikeres, eltávolítja a megadott ügyfél viszonteladói kapcsolatát.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-157">If successful, this method removes a reseller relationship for the specified customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dd3ba-158">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="dd3ba-158">Response success and error codes</span></span>

<span data-ttu-id="dd3ba-159">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dd3ba-160">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="dd3ba-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dd3ba-161">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="dd3ba-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dd3ba-162">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="dd3ba-162">Response example</span></span>

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
