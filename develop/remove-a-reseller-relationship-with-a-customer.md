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
# <a name="remove-a-reseller-relationship-with-a-customer"></a><span data-ttu-id="b313a-103">Ügyféllel létesítendő viszonteladói kapcsolat eltávolítása</span><span class="sxs-lookup"><span data-stu-id="b313a-103">Remove a reseller relationship with a customer</span></span>

<span data-ttu-id="b313a-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="b313a-104">**Applies To**</span></span>

- <span data-ttu-id="b313a-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="b313a-105">Partner Center</span></span>

<span data-ttu-id="b313a-106">Távolítson el egy viszonteladói kapcsolatot egy ügyféllel, amelyhez már nincs tranzakció.</span><span class="sxs-lookup"><span data-stu-id="b313a-106">Remove a reseller relationship with a customer that you no longer have transactions with.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b313a-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b313a-107">Prerequisites</span></span>

- <span data-ttu-id="b313a-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="b313a-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b313a-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="b313a-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b313a-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b313a-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b313a-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="b313a-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b313a-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="b313a-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b313a-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="b313a-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b313a-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="b313a-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b313a-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b313a-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b313a-116">Az összes Azure-beli fenntartott VM-példányra vonatkozó rendelést meg kell szüntetni a viszonteladói kapcsolat eltávolítása előtt.</span><span class="sxs-lookup"><span data-stu-id="b313a-116">All Azure Reserved VM Instance orders must be canceled before a reseller relationship is removed.</span></span> <span data-ttu-id="b313a-117">Az Azure-támogatás meghívásával megszakíthatja az Azure-beli fenntartott VM-példányok megrendeléseit.</span><span class="sxs-lookup"><span data-stu-id="b313a-117">Call Azure support for canceling any open Azure Reserved VM Instance orders.</span></span>

## <a name="c"></a><span data-ttu-id="b313a-118">C\#</span><span class="sxs-lookup"><span data-stu-id="b313a-118">C\#</span></span>

<span data-ttu-id="b313a-119">Az ügyfél viszonteladói kapcsolatának eltávolításához először győződjön meg arról, hogy az ügyfélhez tartozó összes aktív Azure Reserved VM Instances meg lett szakítva.</span><span class="sxs-lookup"><span data-stu-id="b313a-119">To remove the reseller relationship for a customer, first ensure that any active Azure Reserved VM Instances for that customer are canceled.</span></span> <span data-ttu-id="b313a-120">Ezután győződjön meg arról, hogy az ügyfél összes aktív előfizetése fel van függesztve.</span><span class="sxs-lookup"><span data-stu-id="b313a-120">Next, ensure that all active subscriptions for that customer are suspended.</span></span> <span data-ttu-id="b313a-121">Ehhez meg kell határozni annak az ügyfélnek az AZONOSÍTÓját, akinek törölni szeretné a viszonteladói kapcsolatot.</span><span class="sxs-lookup"><span data-stu-id="b313a-121">To do so, determine the ID of the customer for whom you want to delete the reseller relationship.</span></span> <span data-ttu-id="b313a-122">A következő kódrészletben a rendszer kéri a felhasználótól, hogy adja meg az ügyfél-azonosítót.</span><span class="sxs-lookup"><span data-stu-id="b313a-122">In the following code example, the user is prompted to provide the customer identifier.</span></span>

<span data-ttu-id="b313a-123">Annak megállapításához, hogy az ügyfélhez tartozó összes Azure Reserved VM Instances meg kell-e szakítani, le kell kérnie a jogosultságok gyűjteményét a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódus meghívásával az ügyfél azonosítójának megadásával, és a [**jogosultságok**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, hogy lekérje a jogosultságok gyűjtési műveleteihez szükséges felületet.</span><span class="sxs-lookup"><span data-stu-id="b313a-123">To determine if any Azure Reserved VM Instances for the customer must be canceled, retrieve the collection of entitlements by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to entitlement collection operations.</span></span> <span data-ttu-id="b313a-124">A jogosultságok gyűjtésének lekéréséhez hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="b313a-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the entitlement collection.</span></span> <span data-ttu-id="b313a-125">Szűrje a gyűjteményt minden olyan jogosultsághoz, amely a [**EntitlementType. VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) [**EntitlementType**](entitlement-resources.md#entitlementtype) értékkel rendelkezik, és ha vannak ilyenek, a folytatás előtt a támogatás hívásával szakítsa meg őket.</span><span class="sxs-lookup"><span data-stu-id="b313a-125">Filter the collection for any entitlements with an [**EntitlementType**](entitlement-resources.md#entitlementtype) value of [**EntitlementType.VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) and if there are any, cancel them by calling support before proceeding.</span></span>

<span data-ttu-id="b313a-126">Ezután kérje le az ügyfél-előfizetések gyűjteményét úgy, hogy meghívja a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél megadásához, és az [**előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, amely az előfizetés-gyűjtési műveletekhez felületet kér le.</span><span class="sxs-lookup"><span data-stu-id="b313a-126">Then, retrieve a collection of the customer's subscriptions by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="b313a-127">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) metódust az ügyfél előfizetések gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="b313a-127">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the customer's subscriptions collection.</span></span> <span data-ttu-id="b313a-128">Az előfizetés bejárásával ellenőrizze, hogy az előfizetések egyike sem rendelkezik [**előfizetésekkel. status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) tulajdonság értéke [**SubscriptionStatus. Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="b313a-128">Traverse the subscription collection and ensure that none of the subscriptions have a [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property value of [**SubscriptionStatus.Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="b313a-129">Ha egy előfizetés még aktív, tekintse meg az [előfizetés felfüggesztése](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) című témakört, amelyből megtudhatja, hogyan felfüggesztheti.</span><span class="sxs-lookup"><span data-stu-id="b313a-129">If a subscription is still active, see [Suspend a subscription](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) for information on how to suspend it.</span></span>

<span data-ttu-id="b313a-130">Miután megerősítette, hogy az ügyfél összes aktív Azure Reserved VM Instancesa meg lett szakítva, és az összes aktív előfizetés fel van függesztve, eltávolíthatja az ügyfél viszonteladói kapcsolatát.</span><span class="sxs-lookup"><span data-stu-id="b313a-130">After confirming that all active Azure Reserved VM Instances for that customer are canceled and all active subscriptions are suspended, you can remove the reseller relationship for the customer.</span></span> <span data-ttu-id="b313a-131">Először hozzon létre egy új [Customer/DotNet/API/Microsoft. Store. partnercenter. models. Customs. Customer "objektumot a [Customer. RelationshipToPartner/DotNet/API/Microsoft. Store. partnercenter. models. customers. Customer. RelationshipToPartner) tulajdonsággal, amely a [**CustomerPartnerRelationship. None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship)értékre van beállítva.</span><span class="sxs-lookup"><span data-stu-id="b313a-131">First, create a new [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object with the [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) property set to [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span></span> <span data-ttu-id="b313a-132">Ezután hívja meg a [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosító használatával az ügyfél megadásához, és hívja meg a **patch** metódust, amely az új ügyfél objektumba kerül.</span><span class="sxs-lookup"><span data-stu-id="b313a-132">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and call the **Patch** method, passing in the new customer object.</span></span>

<span data-ttu-id="b313a-133">A kapcsolat újbóli létrehozásához ismételje meg a [viszonteladói kapcsolat/partner-központ/fejlesztés/kérelem-viszonteladói kapcsolat kérése) folyamatát.</span><span class="sxs-lookup"><span data-stu-id="b313a-133">To re-establish the relationship, repeat the process of [requesting a reseller relationship/partner-center/develop/request-reseller-relationship).</span></span>

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

<span data-ttu-id="b313a-134">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b313a-134">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b313a-135">**Projekt**: PartnerSDK. FeatureSample **osztály**: DeletePartnerCustomerRelationship.cs</span><span class="sxs-lookup"><span data-stu-id="b313a-135">**Project**: PartnerSDK.FeatureSample **Class**: DeletePartnerCustomerRelationship.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b313a-136">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="b313a-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b313a-137">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b313a-137">Request syntax</span></span>

| <span data-ttu-id="b313a-138">Metódus</span><span class="sxs-lookup"><span data-stu-id="b313a-138">Method</span></span>     | <span data-ttu-id="b313a-139">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b313a-139">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b313a-140">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="b313a-140">**PATCH**</span></span>  | <span data-ttu-id="b313a-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/http/1.1</span><span class="sxs-lookup"><span data-stu-id="b313a-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b313a-142">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="b313a-142">URI parameter</span></span>

<span data-ttu-id="b313a-143">Ez a táblázat a viszonteladói kapcsolat eltávolításához szükséges lekérdezési paramétereket sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="b313a-143">This table lists the required query parameters to remove a reseller relationship.</span></span>

| <span data-ttu-id="b313a-144">Név</span><span class="sxs-lookup"><span data-stu-id="b313a-144">Name</span></span>                   | <span data-ttu-id="b313a-145">Típus</span><span class="sxs-lookup"><span data-stu-id="b313a-145">Type</span></span>     | <span data-ttu-id="b313a-146">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b313a-146">Required</span></span> | <span data-ttu-id="b313a-147">Leírás</span><span class="sxs-lookup"><span data-stu-id="b313a-147">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="b313a-148">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="b313a-148">**customer-tenant-id**</span></span> | <span data-ttu-id="b313a-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="b313a-149">**guid**</span></span> | <span data-ttu-id="b313a-150">Y</span><span class="sxs-lookup"><span data-stu-id="b313a-150">Y</span></span>        | <span data-ttu-id="b313a-151">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító** , amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="b313a-151">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b313a-152">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b313a-152">Request headers</span></span>

<span data-ttu-id="b313a-153">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b313a-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b313a-154">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b313a-154">Request body</span></span>

<span data-ttu-id="b313a-155">A kérés törzsében meg kell adni egy **ügyfél** -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="b313a-155">A **Customer** resource is required in the request body.</span></span> <span data-ttu-id="b313a-156">Győződjön meg arról, hogy a **RelationshipToPartner** tulajdonság értéke NONE.</span><span class="sxs-lookup"><span data-stu-id="b313a-156">Ensure the **RelationshipToPartner** property has been set to none.</span></span>

### <a name="request-example"></a><span data-ttu-id="b313a-157">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b313a-157">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b313a-158">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b313a-158">REST response</span></span>

<span data-ttu-id="b313a-159">Ha ez sikeres, ez a metódus eltávolítja a viszonteladói kapcsolatot a megadott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="b313a-159">If successful, this method removes a reseller relationship for the specified customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b313a-160">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b313a-160">Response success and error codes</span></span>

<span data-ttu-id="b313a-161">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="b313a-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b313a-162">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="b313a-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b313a-163">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="b313a-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b313a-164">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b313a-164">Response example</span></span>

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
