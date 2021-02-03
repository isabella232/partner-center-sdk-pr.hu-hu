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
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a><span data-ttu-id="07b55-103">Ügyfélfiók törlése az integrációs tesztkörnyezetből</span><span class="sxs-lookup"><span data-stu-id="07b55-103">Delete a customer account from the integration sandbox</span></span>

<span data-ttu-id="07b55-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="07b55-104">**Applies to:**</span></span>

- <span data-ttu-id="07b55-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="07b55-105">Partner Center</span></span>
- <span data-ttu-id="07b55-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="07b55-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="07b55-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="07b55-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="07b55-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="07b55-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="07b55-109">Ez a cikk ismerteti a partner és az ügyfél közötti kapcsolat bontását, és visszanyeri a kvótát az üzemi (tip) integrációs munkaterületre való teszteléshez.</span><span class="sxs-lookup"><span data-stu-id="07b55-109">This article explains, how to break the relationship between the partner and the customer account and regain the quota for Testing in Production (Tip) integration sandbox.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07b55-110">Ha töröl egy ügyfél-fiókot, az ügyfél-bérlőhöz társított összes erőforrás törlődni fog.</span><span class="sxs-lookup"><span data-stu-id="07b55-110">When you delete a customer account, all resources associated with that customer tenant will be purged.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07b55-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="07b55-111">Prerequisites</span></span>

- <span data-ttu-id="07b55-112">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="07b55-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="07b55-113">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="07b55-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="07b55-114">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="07b55-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="07b55-115">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="07b55-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="07b55-116">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="07b55-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="07b55-117">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="07b55-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="07b55-118">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="07b55-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="07b55-119">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="07b55-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="07b55-120">Az összes Azure Reserved Virtual Machine Instances-és szoftver-beszerzési rendelést meg kell szüntetni, mielőtt törölné egy ügyfelet a tip Integration sandbox-ból.</span><span class="sxs-lookup"><span data-stu-id="07b55-120">All Azure Reserved Virtual Machine Instances and software purchase orders must be cancelled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="c"></a><span data-ttu-id="07b55-121">C\#</span><span class="sxs-lookup"><span data-stu-id="07b55-121">C\#</span></span>

<span data-ttu-id="07b55-122">Ügyfél törlése a tipp-integrációs homokozóból:</span><span class="sxs-lookup"><span data-stu-id="07b55-122">To delete a customer from the Tip integration sandbox:</span></span>

1. <span data-ttu-id="07b55-123">Adja át a tip-fiókja hitelesítő adatait a [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metódusnak, hogy [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) felületet kapjon a partneri műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="07b55-123">Pass your Tip account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to partner operations.</span></span>

2. <span data-ttu-id="07b55-124">A jogosultságok gyűjteményének lekéréséhez használja a partner műveleti felületet:</span><span class="sxs-lookup"><span data-stu-id="07b55-124">Use the partner operations interface to retrieve the collection of entitlements:</span></span>

    1. <span data-ttu-id="07b55-125">Az ügyfél megadásához hívja meg a [**customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="07b55-125">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer.</span></span>

    2. <span data-ttu-id="07b55-126">Hívja meg a **jogosultságok** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="07b55-126">Call the **Entitlements** property.</span></span>

    3. <span data-ttu-id="07b55-127">A [**jogosultságok**](entitlement-resources.md) gyűjtésének lekéréséhez hívja meg a **Get** vagy a **GetAsync** metódust.</span><span class="sxs-lookup"><span data-stu-id="07b55-127">Call the **Get** or **GetAsync** method to retrieve the [**Entitlement**](entitlement-resources.md) collection.</span></span>

3. <span data-ttu-id="07b55-128">Győződjön meg arról, hogy az ügyfél összes Azure Reserved Virtual Machine Instances és szoftveres beszerzési rendelése meg lett szakítva.</span><span class="sxs-lookup"><span data-stu-id="07b55-128">Make sure that all Azure Reserved Virtual Machine Instances and software purchase orders for that customer are cancelled.</span></span> <span data-ttu-id="07b55-129">A gyűjtemény minden [**jogosultságához**](entitlement-resources.md) :</span><span class="sxs-lookup"><span data-stu-id="07b55-129">For each [**Entitlement**](entitlement-resources.md) in the collection:</span></span>

    1. <span data-ttu-id="07b55-130">Használja a [**jogosultságot. A ReferenceOrder.Id**](entitlement-resources.md#referenceorder) a megfelelő [rendelés](order-resources.md#order) helyi másolatát kapja meg az ügyfél rendeléseinek gyűjteményéből.</span><span class="sxs-lookup"><span data-stu-id="07b55-130">Use the [**entitlement.ReferenceOrder.Id**](entitlement-resources.md#referenceorder) to get a local copy of the corresponding [Order](order-resources.md#order) from the customer's collection of orders.</span></span>

    2. <span data-ttu-id="07b55-131">Állítsa a [**Order. status**](order-resources.md#order) tulajdonságot "megszakítva" értékre.</span><span class="sxs-lookup"><span data-stu-id="07b55-131">Set the [**Order.Status**](order-resources.md#order) property to "Cancelled".</span></span>

    3. <span data-ttu-id="07b55-132">A **javítás ()** metódus használatával frissítse a sorrendet.</span><span class="sxs-lookup"><span data-stu-id="07b55-132">Use the **Patch()** method to update the order.</span></span>

4. <span data-ttu-id="07b55-133">Az összes megrendelés megszakítása.</span><span class="sxs-lookup"><span data-stu-id="07b55-133">Cancel all orders.</span></span> <span data-ttu-id="07b55-134">Az alábbi mintakód például egy hurkot használ az egyes sorrendek lekérdezéséhez, amíg az állapota "megszakítva".</span><span class="sxs-lookup"><span data-stu-id="07b55-134">For example, the following code sample uses a loop to poll each order until its status is "Cancelled".</span></span>

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

5. <span data-ttu-id="07b55-135">Győződjön meg arról, hogy az összes megrendelést megszakította az ügyfél **törlési** metódusának meghívásával.</span><span class="sxs-lookup"><span data-stu-id="07b55-135">Make sure all orders are cancelled by calling the **Delete** method for the customer.</span></span>

<span data-ttu-id="07b55-136">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="07b55-136">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="07b55-137">**Projekt**: partner Center PartnerCenterSDK. FeaturesSamples **osztály**: DeleteCustomerFromTipAccount.cs</span><span class="sxs-lookup"><span data-stu-id="07b55-137">**Project**: Partner Center PartnerCenterSDK.FeaturesSamples **Class**: DeleteCustomerFromTipAccount.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="07b55-138">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="07b55-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="07b55-139">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="07b55-139">Request syntax</span></span>

| <span data-ttu-id="07b55-140">Metódus</span><span class="sxs-lookup"><span data-stu-id="07b55-140">Method</span></span>     | <span data-ttu-id="07b55-141">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="07b55-141">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="07b55-142">DELETE</span><span class="sxs-lookup"><span data-stu-id="07b55-142">DELETE</span></span>     | <span data-ttu-id="07b55-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="07b55-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="07b55-144">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="07b55-144">URI parameter</span></span>

<span data-ttu-id="07b55-145">Az ügyfél törléséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="07b55-145">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="07b55-146">Név</span><span class="sxs-lookup"><span data-stu-id="07b55-146">Name</span></span>                   | <span data-ttu-id="07b55-147">Típus</span><span class="sxs-lookup"><span data-stu-id="07b55-147">Type</span></span>     | <span data-ttu-id="07b55-148">Kötelező</span><span class="sxs-lookup"><span data-stu-id="07b55-148">Required</span></span> | <span data-ttu-id="07b55-149">Leírás</span><span class="sxs-lookup"><span data-stu-id="07b55-149">Description</span></span>                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="07b55-150">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="07b55-150">customer-tenant-id</span></span>     | <span data-ttu-id="07b55-151">GUID</span><span class="sxs-lookup"><span data-stu-id="07b55-151">GUID</span></span>     | <span data-ttu-id="07b55-152">Y</span><span class="sxs-lookup"><span data-stu-id="07b55-152">Y</span></span>        | <span data-ttu-id="07b55-153">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="07b55-153">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="07b55-154">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="07b55-154">Request headers</span></span>

<span data-ttu-id="07b55-155">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="07b55-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="07b55-156">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="07b55-156">Request body</span></span>

<span data-ttu-id="07b55-157">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="07b55-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="07b55-158">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="07b55-158">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="07b55-159">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="07b55-159">REST response</span></span>

<span data-ttu-id="07b55-160">Ha ez sikeres, a metódus üres választ ad vissza.</span><span class="sxs-lookup"><span data-stu-id="07b55-160">If successful, this method returns an empty response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="07b55-161">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="07b55-161">Response success and error codes</span></span>

<span data-ttu-id="07b55-162">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="07b55-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="07b55-163">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="07b55-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="07b55-164">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="07b55-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="07b55-165">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="07b55-165">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
