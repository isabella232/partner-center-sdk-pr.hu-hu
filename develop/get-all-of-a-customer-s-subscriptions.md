---
title: Egy ügyfél előfizetéseinek lekérése
description: Ügyfél-előfizetések gyűjteményének begyűjtése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 01ac9e5169258d0ac263d5bbe8cff567c76f98ed
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760623"
---
# <a name="get-a-customers-subscriptions"></a><span data-ttu-id="59629-103">Egy ügyfél előfizetéseinek lekérése</span><span class="sxs-lookup"><span data-stu-id="59629-103">Get a customer's subscriptions</span></span>

<span data-ttu-id="59629-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="59629-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="59629-105">Ügyfél-előfizetések gyűjteményének begyűjtése.</span><span class="sxs-lookup"><span data-stu-id="59629-105">How to get a collection of a customer's subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59629-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="59629-106">Prerequisites</span></span>

- <span data-ttu-id="59629-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="59629-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="59629-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="59629-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="59629-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="59629-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="59629-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="59629-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="59629-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="59629-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="59629-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="59629-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="59629-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="59629-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="59629-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="59629-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="59629-115">C\#</span><span class="sxs-lookup"><span data-stu-id="59629-115">C\#</span></span>

<span data-ttu-id="59629-116">Az ügyfél összes előfizetésének listájáért először használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="59629-116">To get a list of all of a customer's subscriptions, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to identify the customer.</span></span> <span data-ttu-id="59629-117">Ezután az [**Előfizetések tulajdonság**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) használatával lekéri az előfizetés-gyűjtési műveletek felületét.</span><span class="sxs-lookup"><span data-stu-id="59629-117">Then use the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="59629-118">Végül hívja meg [**a Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) vagy [**GetAsync metódusokat**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) az ügyfél előfizetés-gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="59629-118">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) methods to retrieve the customer's subscriptions collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerSubscriptions = partnerOperations.Customers.ById(customerId).Subscriptions.Get();
```

<span data-ttu-id="59629-119">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="59629-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="59629-120">**Project:** Partnerközpont SDK Samples **Osztály:** GetSubscriptions.cs</span><span class="sxs-lookup"><span data-stu-id="59629-120">**Project**: Partner Center SDK Samples **Class**: GetSubscriptions.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="59629-121">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="59629-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="59629-122">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="59629-122">Request syntax</span></span>

| <span data-ttu-id="59629-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="59629-123">Method</span></span>  | <span data-ttu-id="59629-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="59629-124">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="59629-125">**Kap**</span><span class="sxs-lookup"><span data-stu-id="59629-125">**GET**</span></span> | <span data-ttu-id="59629-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="59629-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="59629-127">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="59629-127">URI parameter</span></span>

<span data-ttu-id="59629-128">Ez a táblázat felsorolja az összes előfizetés lekérdezhető lekérdezési paraméterét.</span><span class="sxs-lookup"><span data-stu-id="59629-128">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="59629-129">Név</span><span class="sxs-lookup"><span data-stu-id="59629-129">Name</span></span>               | <span data-ttu-id="59629-130">Típus</span><span class="sxs-lookup"><span data-stu-id="59629-130">Type</span></span>   | <span data-ttu-id="59629-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="59629-131">Required</span></span> | <span data-ttu-id="59629-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="59629-132">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="59629-133">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="59629-133">customer-tenant-id</span></span> | <span data-ttu-id="59629-134">sztring</span><span class="sxs-lookup"><span data-stu-id="59629-134">string</span></span> | <span data-ttu-id="59629-135">Igen</span><span class="sxs-lookup"><span data-stu-id="59629-135">Yes</span></span>      | <span data-ttu-id="59629-136">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="59629-136">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="59629-137">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="59629-137">Request headers</span></span>

<span data-ttu-id="59629-138">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="59629-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="59629-139">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="59629-139">Request body</span></span>

<span data-ttu-id="59629-140">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="59629-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="59629-141">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="59629-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="59629-142">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="59629-142">REST response</span></span>

<span data-ttu-id="59629-143">Ha a művelet sikeres, ez a metódus [előfizetési](subscription-resources.md) erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="59629-143">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="59629-144">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="59629-144">Response success and error codes</span></span>

<span data-ttu-id="59629-145">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="59629-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="59629-146">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="59629-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="59629-147">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="59629-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="59629-148">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="59629-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
Date: Wed, 25 Nov 2015 05:43:06 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "a356ac8c-e310-44f4-bf85-C7f29044af99",
        "friendlyName": "nickname",
        "quantity": 1,
        "unitType": "none",
        "creationDate": "2015-11-25T06: 41: 12Z",
        "effectiveStartDate": "2015-11-24T08: 00: 00Z",
        "commitmentEndDate": "2016-12-12T08: 00: 00Z",
        "status": "active",
        "autoRenewEnabled": false,
        "billingType": "none",
        "contractType": "subscription",
        "links": {
            "offer": {
                "uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        },
        "orderId": "6183db3d-6318-4e52-877e-25806e4971be",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Subscription"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
