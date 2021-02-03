---
title: Megrendelés megszakítása az integrációs munkaterületről
description: Megtudhatja, hogyan vonhatja vissza a különböző típusú előfizetési rendeléseket a partner Center API-kkal az integrációs homokozó fiókjaiból.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 363bf209e27d5223259c8c533710a3b35bbef1e6
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768596"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a><span data-ttu-id="6b511-103">Megrendelés megszakítása az integrációs munkaterületről a partner Center API-k használatával</span><span class="sxs-lookup"><span data-stu-id="6b511-103">Cancel an order from the integration sandbox using Partner Center APIs</span></span>

<span data-ttu-id="6b511-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="6b511-104">**Applies to:**</span></span>

- <span data-ttu-id="6b511-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="6b511-105">Partner Center</span></span>
- <span data-ttu-id="6b511-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="6b511-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="6b511-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="6b511-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="6b511-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="6b511-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6b511-109">Ez a cikk azt ismerteti, hogyan lehet a partner Center API-kkal különböző típusú előfizetési rendeléseket lemondani az Integration sandbox-fiókokból.</span><span class="sxs-lookup"><span data-stu-id="6b511-109">This article describes how to use Partner Center APIs to cancel different types of subscription orders from integration sandbox accounts.</span></span> <span data-ttu-id="6b511-110">Az ilyen megrendelések tartalmazhatnak fenntartott példányokat, szoftvereket és kereskedelmi Piactéri szoftvereket (SaaS) előfizetési rendeléseket.</span><span class="sxs-lookup"><span data-stu-id="6b511-110">Such orders can include reserved instances, software, and commercial marketplace Software as a Service (SaaS) subscription orders.</span></span>

>[!NOTE]
><span data-ttu-id="6b511-111">Felhívjuk a figyelmét arra, hogy a fenntartott példányok vagy a kereskedelmi Piactéri SaaS-előfizetési megrendelések törlése csak az integrációs munkaterületről lehetséges.</span><span class="sxs-lookup"><span data-stu-id="6b511-111">Please be aware that the cancellations of reserved instance, or commercial marketplace SaaS subscription orders are only possible from integration sandbox accounts.</span></span>  

<span data-ttu-id="6b511-112">Ha az API-n keresztül szeretné lemondani a szoftver éles sorrendjét, használja a [Cancel-Software-](cancel-software-purchases.md)Buys parancsot.</span><span class="sxs-lookup"><span data-stu-id="6b511-112">To cancel production orders of software through API, use [cancel-software-purchases](cancel-software-purchases.md).</span></span>
<span data-ttu-id="6b511-113">Az irányítópulton keresztül is megszakíthatja a szoftver éles rendeléseit a [vásárlás megszakításával](/partner-center/csp-software-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="6b511-113">You can also cancel production orders of software through dashboard using [cancel a purchase](/partner-center/csp-software-subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b511-114">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6b511-114">Prerequisites</span></span>

- <span data-ttu-id="6b511-115">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="6b511-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6b511-116">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="6b511-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6b511-117">Egy integrációs sandbox-partner fiók egy aktív fenntartott példány/szoftver/harmadik féltől származó SaaS-előfizetési rendeléssel rendelkező ügyféllel.</span><span class="sxs-lookup"><span data-stu-id="6b511-117">An integration sandbox partner account with a customer having active reserved instance / software / third-party SaaS subscription orders.</span></span>

## <a name="c"></a><span data-ttu-id="6b511-118">C\#</span><span class="sxs-lookup"><span data-stu-id="6b511-118">C\#</span></span>

<span data-ttu-id="6b511-119">Ha meg szeretné szüntetni a rendelést az integrációs munkaterületről, adja át a fiók hitelesítő adatait a [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metódusnak, hogy lekérje a partneri műveletek elvégzéséhez szükséges [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) felületet.</span><span class="sxs-lookup"><span data-stu-id="6b511-119">To cancel an order from the integration sandbox, pass your account credentials to the [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

<span data-ttu-id="6b511-120">Egy adott [megrendelés](order-resources.md#order)kiválasztásához használja a partner műveleti és Call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és adja meg az ügyfelet, majd a **`Orders.ById()`** megrendelés azonosítójának megadásával adja meg a sorrendet, végül **`Get`** vagy **`GetAsync`** a lekérési módszert.</span><span class="sxs-lookup"><span data-stu-id="6b511-120">To select a particular [Order](order-resources.md#order), use the partner operations and call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, followed by **`Orders.ById()`** with order identifier to specify the order and finally **`Get`** or **`GetAsync`** method to retrieve it.</span></span>

<span data-ttu-id="6b511-121">Állítsa be a tulajdonságot a értékre, [**`Order.Status`**](order-resources.md#order) `cancelled` és használja a **`Patch()`** metódust a sorrend frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="6b511-121">Set the [**`Order.Status`**](order-resources.md#order) property to `cancelled` and use the **`Patch()`** method to update the order.</span></span>

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a><span data-ttu-id="6b511-122">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="6b511-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6b511-123">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="6b511-123">Request syntax</span></span>

| <span data-ttu-id="6b511-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="6b511-124">Method</span></span>     | <span data-ttu-id="6b511-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="6b511-125">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="6b511-126">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="6b511-126">**PATCH**</span></span> | <span data-ttu-id="6b511-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="6b511-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6b511-128">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="6b511-128">URI parameter</span></span>

<span data-ttu-id="6b511-129">Az ügyfél törléséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="6b511-129">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="6b511-130">Név</span><span class="sxs-lookup"><span data-stu-id="6b511-130">Name</span></span>                   | <span data-ttu-id="6b511-131">Típus</span><span class="sxs-lookup"><span data-stu-id="6b511-131">Type</span></span>     | <span data-ttu-id="6b511-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="6b511-132">Required</span></span> | <span data-ttu-id="6b511-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="6b511-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6b511-134">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="6b511-134">**customer-tenant-id**</span></span> | <span data-ttu-id="6b511-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="6b511-135">**guid**</span></span> | <span data-ttu-id="6b511-136">Y</span><span class="sxs-lookup"><span data-stu-id="6b511-136">Y</span></span>        | <span data-ttu-id="6b511-137">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="6b511-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="6b511-138">**megrendelés azonosítója**</span><span class="sxs-lookup"><span data-stu-id="6b511-138">**order-id**</span></span> | <span data-ttu-id="6b511-139">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="6b511-139">**string**</span></span> | <span data-ttu-id="6b511-140">Y</span><span class="sxs-lookup"><span data-stu-id="6b511-140">Y</span></span>        | <span data-ttu-id="6b511-141">Az érték a megszakítani kívánt sorrendi azonosítókat jelölő karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="6b511-141">The value is a string denoting the order IDs that need to be canceled.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6b511-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="6b511-142">Request headers</span></span>

<span data-ttu-id="6b511-143">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6b511-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6b511-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="6b511-144">Request body</span></span>

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a><span data-ttu-id="6b511-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="6b511-145">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a><span data-ttu-id="6b511-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="6b511-146">REST response</span></span>

<span data-ttu-id="6b511-147">Ha ez sikeres, a metódus visszaadja a megszakított sorrendet.</span><span class="sxs-lookup"><span data-stu-id="6b511-147">If successful, this method returns the canceled order.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6b511-148">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="6b511-148">Response success and error codes</span></span>

<span data-ttu-id="6b511-149">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="6b511-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6b511-150">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="6b511-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6b511-151">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="6b511-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6b511-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="6b511-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
