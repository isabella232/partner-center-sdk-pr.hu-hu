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
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a><span data-ttu-id="d5f17-103">Ügyfélfiók törlése az integrációs tesztkörnyezetből</span><span class="sxs-lookup"><span data-stu-id="d5f17-103">Delete a customer account from the integration sandbox</span></span>

<span data-ttu-id="d5f17-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d5f17-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d5f17-105">Ez a cikk azt ismerteti, hogyan lehet megszakítani a partner és az ügyfélfiók közötti kapcsolatot, és vissza lehet szerezni a tesztelési kvótát éles környezetben (Tipp) az integrációs tesztkészletben.</span><span class="sxs-lookup"><span data-stu-id="d5f17-105">This article explains, how to break the relationship between the partner and the customer account and regain the quota for Testing in Production (Tip) integration sandbox.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5f17-106">Amikor töröl egy ügyfélfiókot, az adott ügyfélbérlőhöz társított összes erőforrás törölve lesz.</span><span class="sxs-lookup"><span data-stu-id="d5f17-106">When you delete a customer account, all resources associated with that customer tenant will be purged.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5f17-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d5f17-107">Prerequisites</span></span>

- <span data-ttu-id="d5f17-108">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d5f17-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d5f17-109">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="d5f17-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d5f17-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d5f17-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d5f17-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d5f17-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d5f17-112">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d5f17-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d5f17-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d5f17-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d5f17-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="d5f17-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d5f17-115">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d5f17-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d5f17-116">Minden Azure Reserved Virtual Machine Instances és szoftvervásárlási rendelést meg kell szakítani, mielőtt törölné az ügyfelet a Tipp integrációs védőfalból.</span><span class="sxs-lookup"><span data-stu-id="d5f17-116">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="c"></a><span data-ttu-id="d5f17-117">C\#</span><span class="sxs-lookup"><span data-stu-id="d5f17-117">C\#</span></span>

<span data-ttu-id="d5f17-118">Ügyfél törlése a Tipp integrációs védőfalból:</span><span class="sxs-lookup"><span data-stu-id="d5f17-118">To delete a customer from the Tip integration sandbox:</span></span>

1. <span data-ttu-id="d5f17-119">Adja át Tipp-fiókja hitelesítő adatait a [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metódusnak, hogy [**IPartner-felületet**](/dotnet/api/microsoft.store.partnercenter.ipartner) kapjon a partneri műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="d5f17-119">Pass your Tip account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to partner operations.</span></span>

2. <span data-ttu-id="d5f17-120">A partner műveleti felületén lekéri a jogosultságok gyűjteményét:</span><span class="sxs-lookup"><span data-stu-id="d5f17-120">Use the partner operations interface to retrieve the collection of entitlements:</span></span>

    1. <span data-ttu-id="d5f17-121">Az ügyfél megadásához hívja meg a [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfélazonosítóval.</span><span class="sxs-lookup"><span data-stu-id="d5f17-121">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer.</span></span>

    2. <span data-ttu-id="d5f17-122">Hívja meg **a Jogosultságok tulajdonságot.**</span><span class="sxs-lookup"><span data-stu-id="d5f17-122">Call the **Entitlements** property.</span></span>

    3. <span data-ttu-id="d5f17-123">Hívja meg **a Get** vagy **GetAsync metódust** a jogosultsággyűjtemény [**lekéréséhez.**](entitlement-resources.md)</span><span class="sxs-lookup"><span data-stu-id="d5f17-123">Call the **Get** or **GetAsync** method to retrieve the [**Entitlement**](entitlement-resources.md) collection.</span></span>

3. <span data-ttu-id="d5f17-124">Győződjön meg arról, Azure Reserved Virtual Machine Instances ügyfél összes rendelése és szoftvervásárlási rendelése törölve lett.</span><span class="sxs-lookup"><span data-stu-id="d5f17-124">Make sure that all Azure Reserved Virtual Machine Instances and software purchase orders for that customer are canceled.</span></span> <span data-ttu-id="d5f17-125">A gyűjtemény [**minden egyes jogosultsága**](entitlement-resources.md) esetén:</span><span class="sxs-lookup"><span data-stu-id="d5f17-125">For each [**Entitlement**](entitlement-resources.md) in the collection:</span></span>

    1. <span data-ttu-id="d5f17-126">Használja a [**jogosultságot. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) le kell szereznie a megfelelő [](order-resources.md#order) rendelés helyi másolatát az ügyfél rendelésgyűjteményéből.</span><span class="sxs-lookup"><span data-stu-id="d5f17-126">Use the [**entitlement.ReferenceOrder.Id**](entitlement-resources.md#referenceorder) to get a local copy of the corresponding [Order](order-resources.md#order) from the customer's collection of orders.</span></span>

    2. <span data-ttu-id="d5f17-127">Állítsa az [**Order.Status**](order-resources.md#order) tulajdonságot "Megszakítva" állapotra.</span><span class="sxs-lookup"><span data-stu-id="d5f17-127">Set the [**Order.Status**](order-resources.md#order) property to "Cancelled".</span></span>

    3. <span data-ttu-id="d5f17-128">Frissítse a sorrendet a **Patch()** metódussal.</span><span class="sxs-lookup"><span data-stu-id="d5f17-128">Use the **Patch()** method to update the order.</span></span>

4. <span data-ttu-id="d5f17-129">Az összes rendelés visszavonása.</span><span class="sxs-lookup"><span data-stu-id="d5f17-129">Cancel all orders.</span></span> <span data-ttu-id="d5f17-130">A következő kódminta például egy ciklussal lekérdezi az egyes rendeléseket, amíg az állapota "Cancelled" (Megszakítva) nem lesz.</span><span class="sxs-lookup"><span data-stu-id="d5f17-130">For example, the following code sample uses a loop to poll each order until its status is "Cancelled".</span></span>

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

5. <span data-ttu-id="d5f17-131">Az ügyfél Delete metódusának hívásával győződjön meg arról, hogy minden rendelés vissza lett szakítva. </span><span class="sxs-lookup"><span data-stu-id="d5f17-131">Make sure all orders are canceled by calling the **Delete** method for the customer.</span></span>

<span data-ttu-id="d5f17-132">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d5f17-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d5f17-133">**Project**: Partnerközpont PartnerCenterSDK.FeaturesSamples **osztály:** DeleteCustomerFromTipAccount.cs</span><span class="sxs-lookup"><span data-stu-id="d5f17-133">**Project**: Partner Center PartnerCenterSDK.FeaturesSamples **Class**: DeleteCustomerFromTipAccount.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d5f17-134">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d5f17-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d5f17-135">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d5f17-135">Request syntax</span></span>

| <span data-ttu-id="d5f17-136">Metódus</span><span class="sxs-lookup"><span data-stu-id="d5f17-136">Method</span></span>     | <span data-ttu-id="d5f17-137">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d5f17-137">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="d5f17-138">DELETE</span><span class="sxs-lookup"><span data-stu-id="d5f17-138">DELETE</span></span>     | <span data-ttu-id="d5f17-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d5f17-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="d5f17-140">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d5f17-140">URI parameter</span></span>

<span data-ttu-id="d5f17-141">Az alábbi lekérdezési paraméterrel törölhet egy ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="d5f17-141">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="d5f17-142">Név</span><span class="sxs-lookup"><span data-stu-id="d5f17-142">Name</span></span>                   | <span data-ttu-id="d5f17-143">Típus</span><span class="sxs-lookup"><span data-stu-id="d5f17-143">Type</span></span>     | <span data-ttu-id="d5f17-144">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d5f17-144">Required</span></span> | <span data-ttu-id="d5f17-145">Leírás</span><span class="sxs-lookup"><span data-stu-id="d5f17-145">Description</span></span>                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="d5f17-146">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="d5f17-146">customer-tenant-id</span></span>     | <span data-ttu-id="d5f17-147">GUID</span><span class="sxs-lookup"><span data-stu-id="d5f17-147">GUID</span></span>     | <span data-ttu-id="d5f17-148">Y</span><span class="sxs-lookup"><span data-stu-id="d5f17-148">Y</span></span>        | <span data-ttu-id="d5f17-149">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="d5f17-149">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d5f17-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d5f17-150">Request headers</span></span>

<span data-ttu-id="d5f17-151">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d5f17-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d5f17-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d5f17-152">Request body</span></span>

<span data-ttu-id="d5f17-153">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d5f17-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d5f17-154">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d5f17-154">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="d5f17-155">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d5f17-155">REST response</span></span>

<span data-ttu-id="d5f17-156">Sikeres művelet esetén ez a metódus üres választ ad vissza.</span><span class="sxs-lookup"><span data-stu-id="d5f17-156">If successful, this method returns an empty response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d5f17-157">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d5f17-157">Response success and error codes</span></span>

<span data-ttu-id="d5f17-158">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d5f17-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d5f17-159">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d5f17-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d5f17-160">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d5f17-160">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d5f17-161">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d5f17-161">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
