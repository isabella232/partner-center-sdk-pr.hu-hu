---
title: Szoftvervásárlások lemondása
description: Önkiszolgáló lehetőség a szoftveres előfizetések és a végleges szoftverfrissítések megszakításához a partner Center API-kkal.
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 25fd10a171fa6ca01f3442d49145443f2382cc18
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768092"
---
# <a name="cancel-software-purchases"></a><span data-ttu-id="28d10-103">Szoftvervásárlások lemondása</span><span class="sxs-lookup"><span data-stu-id="28d10-103">Cancel software purchases</span></span>

<span data-ttu-id="28d10-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="28d10-104">**Applies to:**</span></span>

- <span data-ttu-id="28d10-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="28d10-105">Partner Center</span></span>

<span data-ttu-id="28d10-106">A partner Center API-kkal megszakíthatja a szoftver-előfizetéseket és az örökös szoftveres vásárlásokat (feltéve, hogy ezek a vásárlások a lemondási időszakon belül történnek).</span><span class="sxs-lookup"><span data-stu-id="28d10-106">You can use the Partner Center APIs to cancel software subscriptions and perpetual software purchases (as long as those purchases were made within the cancellation window from the purchase date).</span></span> <span data-ttu-id="28d10-107">Nem kell támogatási jegyet létrehoznia az ilyen lemondás elvégzéséhez, és a következő önkiszolgáló metódusokat használhatja helyette.</span><span class="sxs-lookup"><span data-stu-id="28d10-107">You don't need to create a support ticket to make such cancellations, and can use the following self-service methods instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28d10-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="28d10-108">Prerequisites</span></span>

- <span data-ttu-id="28d10-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="28d10-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="28d10-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="28d10-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="28d10-111">C\#</span><span class="sxs-lookup"><span data-stu-id="28d10-111">C\#</span></span>

<span data-ttu-id="28d10-112">A szoftver megrendelésének megszakítása</span><span class="sxs-lookup"><span data-stu-id="28d10-112">To cancel a software order,</span></span>

1. <span data-ttu-id="28d10-113">Adja át a fiók hitelesítő adatait a [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metódusnak, hogy [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) felületet kapjon a partneri műveletek elvégzéséhez.</span><span class="sxs-lookup"><span data-stu-id="28d10-113">Pass your account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

2. <span data-ttu-id="28d10-114">Válassza ki a megszüntetni kívánt [sorrendet](order-resources.md#order) .</span><span class="sxs-lookup"><span data-stu-id="28d10-114">Select a particular [Order](order-resources.md#order) you wish to cancel.</span></span> <span data-ttu-id="28d10-115">Hívja meg a [**customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, majd a Orders **. ById ()** függvényt a megrendelés azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="28d10-115">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier, followed by **Orders.ById()** with order identifier.</span></span>

3. <span data-ttu-id="28d10-116">A megrendelés lekéréséhez hívja meg a **Get** vagy a **GetAsync** metódust.</span><span class="sxs-lookup"><span data-stu-id="28d10-116">Call the **Get** or **GetAsync** method to retrieve the order.</span></span>

4. <span data-ttu-id="28d10-117">Állítsa a [**Order. status**](order-resources.md#order) tulajdonságot a következőre: `cancelled` .</span><span class="sxs-lookup"><span data-stu-id="28d10-117">Set the [**Order.Status**](order-resources.md#order) property to `cancelled`.</span></span>

5. <span data-ttu-id="28d10-118">Választható Ha bizonyos sortöréseket szeretne megadni, állítsa a [**sorrendet. listaelemek**](order-resources.md#order) a megszakítani kívánt sorok listájára.</span><span class="sxs-lookup"><span data-stu-id="28d10-118">(Optional) If you want to specify certain line items for cancellation, set the [**Order.LineItems**](order-resources.md#order) to list of line items that you want to cancel.</span></span>

6. <span data-ttu-id="28d10-119">A **javítás ()** metódus használatával frissítse a sorrendet.</span><span class="sxs-lookup"><span data-stu-id="28d10-119">Use the **Patch()** method to update the order.</span></span>

``` csharp
// IPartnerCredentials accountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner accountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(accountCredentials);

// Cancel order
var order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order.LineItems = new List<OrderLineItem> {
    order.LineItems.First()
};
order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a><span data-ttu-id="28d10-120">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="28d10-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="28d10-121">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="28d10-121">Request syntax</span></span>

| <span data-ttu-id="28d10-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="28d10-122">Method</span></span>     | <span data-ttu-id="28d10-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="28d10-123">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="28d10-124">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="28d10-124">**PATCH**</span></span> | <span data-ttu-id="28d10-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="28d10-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="28d10-126">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="28d10-126">URI parameters</span></span>

<span data-ttu-id="28d10-127">Az ügyfél törléséhez használja a következő lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="28d10-127">Use the following query parameters to delete a customer.</span></span>

| <span data-ttu-id="28d10-128">Név</span><span class="sxs-lookup"><span data-stu-id="28d10-128">Name</span></span>                   | <span data-ttu-id="28d10-129">Típus</span><span class="sxs-lookup"><span data-stu-id="28d10-129">Type</span></span>     | <span data-ttu-id="28d10-130">Kötelező</span><span class="sxs-lookup"><span data-stu-id="28d10-130">Required</span></span> | <span data-ttu-id="28d10-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="28d10-131">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="28d10-132">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="28d10-132">**customer-tenant-id**</span></span> | <span data-ttu-id="28d10-133">**guid**</span><span class="sxs-lookup"><span data-stu-id="28d10-133">**guid**</span></span> | <span data-ttu-id="28d10-134">Y</span><span class="sxs-lookup"><span data-stu-id="28d10-134">Y</span></span>        | <span data-ttu-id="28d10-135">Az érték egy GUID formátumú ügyfél-bérlői azonosító, amely lehetővé teszi a viszonteladónak a viszonteladóhoz tartozó adott ügyfél eredményének szűrését.</span><span class="sxs-lookup"><span data-stu-id="28d10-135">The value is a GUID formatted customer tenant identifier that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="28d10-136">**megrendelés azonosítója**</span><span class="sxs-lookup"><span data-stu-id="28d10-136">**order-id**</span></span> | <span data-ttu-id="28d10-137">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="28d10-137">**string**</span></span> | <span data-ttu-id="28d10-138">Y</span><span class="sxs-lookup"><span data-stu-id="28d10-138">Y</span></span>        | <span data-ttu-id="28d10-139">Az érték egy olyan karakterlánc, amely a megszakítani kívánt megrendelés azonosítóját jelöli.</span><span class="sxs-lookup"><span data-stu-id="28d10-139">The value is a string that denotes the identifier of the order that you want to cancel.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="28d10-140">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="28d10-140">Request headers</span></span>

<span data-ttu-id="28d10-141">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="28d10-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="28d10-142">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="28d10-142">Request body</span></span>

```http
{
    “id”: “2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

### <a name="request-example"></a><span data-ttu-id="28d10-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="28d10-143">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="28d10-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="28d10-144">REST response</span></span>

<span data-ttu-id="28d10-145">Ha ez sikeres, a metódus visszaadja a megszakított sorok sorrendjét.</span><span class="sxs-lookup"><span data-stu-id="28d10-145">If successful, this method returns the order with canceled line items.</span></span>

<span data-ttu-id="28d10-146">A megrendelés állapota **megszakítva** , ha a sorrendben lévő összes sort megszakították **, vagy ha** a sorrend nem az összes sort megszakítja.</span><span class="sxs-lookup"><span data-stu-id="28d10-146">The order status will be marked as either **cancelled** if all the line items in the order are cancelled, or **completed** if not all line items in the order are canceled.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="28d10-147">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="28d10-147">Response success and error codes</span></span>

<span data-ttu-id="28d10-148">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="28d10-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="28d10-149">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="28d10-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="28d10-150">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="28d10-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="28d10-151">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="28d10-151">Response example</span></span>

<span data-ttu-id="28d10-152">Az alábbi példában látható válaszban láthatja, hogy az ajánlat-azonosítóval rendelkező sor mennyisége **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** nulla (0) lesz.</span><span class="sxs-lookup"><span data-stu-id="28d10-152">In the following example response, you can see that the quantity of line item with the offer identifier **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** has become zero (0).</span></span> <span data-ttu-id="28d10-153">Ez a módosítás azt jelenti, hogy a törlésre megjelölt sort a rendszer sikeresen megszakította.</span><span class="sxs-lookup"><span data-stu-id="28d10-153">This change means that the line item that was marked for cancellation has been canceled successfully.</span></span> <span data-ttu-id="28d10-154">A példában szereplő egyéb sorok nem lettek megszakítva, ami azt jelenti, hogy a teljes megrendelés állapota **befejezettként** lesz megjelölve, nem **szakítva** meg.</span><span class="sxs-lookup"><span data-stu-id="28d10-154">The example order contains other line items that weren't canceled, which means that the status of the overall order will be marked as **completed**, not **cancelled**.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "alternateId": "c403d91b21d2",
    "referenceCustomerId": "45411344-b09d-47e7-9653-542006bf9766",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "SQL Server Enterprise - 2 Core License Pack - 3 year",
            "quantity": 0,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0FKZV?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003/availabilities/DG7GMGF0DWMS?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "DG7GMGF0DVT7:000C:DG7GMGF0FVZM",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "Windows Server CAL - 1 Device CAL - 3 year",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DVT7?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C/availabilities/DG7GMGF0FVZM?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-12-12T17:33:56.1306495Z",
    "status": "completed",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {
        "marketplaceCountry": "US",
        "deviceFamily": "UniversalStore-PartnerCenter",
        "name": "Partner Center API"
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
