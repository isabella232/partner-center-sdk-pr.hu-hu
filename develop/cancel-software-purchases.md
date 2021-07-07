---
title: Szoftvervásárlások lemondása
description: Önkiszolgáló lehetőség a szoftver-előfizetések és a folyamatos szoftvervásárlások lemondására Partnerközpont API-k használatával.
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 877702ac930919ff72c6cc45a3c0e8ecc7e1b5f4
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974233"
---
# <a name="cancel-software-purchases"></a><span data-ttu-id="b8de5-103">Szoftvervásárlások lemondása</span><span class="sxs-lookup"><span data-stu-id="b8de5-103">Cancel software purchases</span></span>

<span data-ttu-id="b8de5-104">A Partnerközpont API-k használatával megszüntetheti a szoftver-előfizetéseket és a folyamatos szoftvervásárlásokat (felhasználhatja azokat a vásárlásokat a vásárlás dátumtól számított lemondási időszakban).</span><span class="sxs-lookup"><span data-stu-id="b8de5-104">You can use the Partner Center APIs to cancel software subscriptions and perpetual software purchases (as long as those purchases were made within the cancellation window from the purchase date).</span></span> <span data-ttu-id="b8de5-105">Ilyen lemondáshoz nem kell támogatási jegyet létrehoznia, és ehelyett a következő önkiszolgáló módszereket használhatja.</span><span class="sxs-lookup"><span data-stu-id="b8de5-105">You don't need to create a support ticket to make such cancellations, and can use the following self-service methods instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8de5-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b8de5-106">Prerequisites</span></span>

- <span data-ttu-id="b8de5-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b8de5-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b8de5-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="b8de5-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="b8de5-109">C\#</span><span class="sxs-lookup"><span data-stu-id="b8de5-109">C\#</span></span>

<span data-ttu-id="b8de5-110">Szoftverrendelés lemondása:</span><span class="sxs-lookup"><span data-stu-id="b8de5-110">To cancel a software order,</span></span>

1. <span data-ttu-id="b8de5-111">Adja át a fiók hitelesítő adatait a [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metódusnak egy [**IPartner-felület**](/dotnet/api/microsoft.store.partnercenter.ipartner) lekért létrehozásához a partnerműveleteket lekért fiókhoz.</span><span class="sxs-lookup"><span data-stu-id="b8de5-111">Pass your account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

2. <span data-ttu-id="b8de5-112">Válassza ki azt a [megrendelést,](order-resources.md#order) amelyről le szeretné mondani a rendelést.</span><span class="sxs-lookup"><span data-stu-id="b8de5-112">Select a particular [Order](order-resources.md#order) you wish to cancel.</span></span> <span data-ttu-id="b8de5-113">Hívja meg [**a Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóját, majd az **Orders.ById()** metódust a rendelésazonosítóval.</span><span class="sxs-lookup"><span data-stu-id="b8de5-113">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier, followed by **Orders.ById()** with order identifier.</span></span>

3. <span data-ttu-id="b8de5-114">A **rendelés lekérése** érdekében hívja meg a Get vagy **a GetAsync** metódust.</span><span class="sxs-lookup"><span data-stu-id="b8de5-114">Call the **Get** or **GetAsync** method to retrieve the order.</span></span>

4. <span data-ttu-id="b8de5-115">Állítsa az [**Order.Status**](order-resources.md#order) tulajdonságot a `cancelled` következőre: .</span><span class="sxs-lookup"><span data-stu-id="b8de5-115">Set the [**Order.Status**](order-resources.md#order) property to `cancelled`.</span></span>

5. <span data-ttu-id="b8de5-116">(Nem kötelező) Ha meg szeretne adni bizonyos sorelemeket a megszakításhoz, állítsa az [**Order.LineItems**](order-resources.md#order) elemet a megszakítani kívánt sorelemek listájára.</span><span class="sxs-lookup"><span data-stu-id="b8de5-116">(Optional) If you want to specify certain line items for cancellation, set the [**Order.LineItems**](order-resources.md#order) to list of line items that you want to cancel.</span></span>

6. <span data-ttu-id="b8de5-117">Frissítse a sorrendet a **Patch()** metódussal.</span><span class="sxs-lookup"><span data-stu-id="b8de5-117">Use the **Patch()** method to update the order.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="b8de5-118">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="b8de5-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b8de5-119">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b8de5-119">Request syntax</span></span>

| <span data-ttu-id="b8de5-120">Metódus</span><span class="sxs-lookup"><span data-stu-id="b8de5-120">Method</span></span>     | <span data-ttu-id="b8de5-121">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b8de5-121">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="b8de5-122">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="b8de5-122">**PATCH**</span></span> | <span data-ttu-id="b8de5-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{rendelésazonosító} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b8de5-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="b8de5-124">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="b8de5-124">URI parameters</span></span>

<span data-ttu-id="b8de5-125">Az ügyfél törléséhez használja az alábbi lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="b8de5-125">Use the following query parameters to delete a customer.</span></span>

| <span data-ttu-id="b8de5-126">Név</span><span class="sxs-lookup"><span data-stu-id="b8de5-126">Name</span></span>                   | <span data-ttu-id="b8de5-127">Típus</span><span class="sxs-lookup"><span data-stu-id="b8de5-127">Type</span></span>     | <span data-ttu-id="b8de5-128">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b8de5-128">Required</span></span> | <span data-ttu-id="b8de5-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="b8de5-129">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b8de5-130">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="b8de5-130">**customer-tenant-id**</span></span> | <span data-ttu-id="b8de5-131">**guid**</span><span class="sxs-lookup"><span data-stu-id="b8de5-131">**guid**</span></span> | <span data-ttu-id="b8de5-132">Y</span><span class="sxs-lookup"><span data-stu-id="b8de5-132">Y</span></span>        | <span data-ttu-id="b8de5-133">Az érték egy GUID formátumú ügyfélbérlő-azonosító, amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="b8de5-133">The value is a GUID formatted customer tenant identifier that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="b8de5-134">**order-id (rendelésazonosító)**</span><span class="sxs-lookup"><span data-stu-id="b8de5-134">**order-id**</span></span> | <span data-ttu-id="b8de5-135">**sztring**</span><span class="sxs-lookup"><span data-stu-id="b8de5-135">**string**</span></span> | <span data-ttu-id="b8de5-136">Y</span><span class="sxs-lookup"><span data-stu-id="b8de5-136">Y</span></span>        | <span data-ttu-id="b8de5-137">Az érték egy sztring, amely a megszakítani kívánt rendelés azonosítóját jelöli.</span><span class="sxs-lookup"><span data-stu-id="b8de5-137">The value is a string that denotes the identifier of the order that you want to cancel.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b8de5-138">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b8de5-138">Request headers</span></span>

<span data-ttu-id="b8de5-139">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b8de5-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b8de5-140">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b8de5-140">Request body</span></span>

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

### <a name="request-example"></a><span data-ttu-id="b8de5-141">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b8de5-141">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b8de5-142">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b8de5-142">REST response</span></span>

<span data-ttu-id="b8de5-143">Ha sikeres, ez a metódus megszakított sorelemeket ad vissza a rendeléshez.</span><span class="sxs-lookup"><span data-stu-id="b8de5-143">If successful, this method returns the order with canceled line items.</span></span>

<span data-ttu-id="b8de5-144">A rendelés állapota vagy  megszakítva állapotúként lesz megjelölve, ha a  rendelésben lévő összes sorelemet visszavonják, vagy akkor fejeződnek be, ha nem minden sorelemet törölnek.</span><span class="sxs-lookup"><span data-stu-id="b8de5-144">The order status will be marked as either **cancelled** if all the line items in the order are canceled, or **completed** if not all line items in the order are canceled.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b8de5-145">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b8de5-145">Response success and error codes</span></span>

<span data-ttu-id="b8de5-146">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="b8de5-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b8de5-147">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="b8de5-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b8de5-148">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b8de5-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b8de5-149">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b8de5-149">Response example</span></span>

<span data-ttu-id="b8de5-150">A következő példaválaszban láthatja, hogy az ajánlatazonosítóval együtt a sorelem mennyisége **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** nullára (0) vált.</span><span class="sxs-lookup"><span data-stu-id="b8de5-150">In the following example response, you can see that the quantity of line item with the offer identifier **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** has become zero (0).</span></span> <span data-ttu-id="b8de5-151">Ez a módosítás azt jelenti, hogy a megszakításra megjelölt sorelem sikeresen törölve lett.</span><span class="sxs-lookup"><span data-stu-id="b8de5-151">This change means that the line item that was marked for cancellation has been canceled successfully.</span></span> <span data-ttu-id="b8de5-152">A példasorrend más sorelemeket is tartalmaz, amelyeket nem töröltek, ami azt jelenti, hogy a teljes rendelés állapota befejezettként lesz megjelölve, nem **megszakítva.**</span><span class="sxs-lookup"><span data-stu-id="b8de5-152">The example order contains other line items that weren't canceled, which means that the status of the overall order will be marked as **completed**, not **cancelled**.</span></span>

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
