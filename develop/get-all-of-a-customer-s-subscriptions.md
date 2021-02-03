---
title: Egy ügyfél előfizetéseinek lekérése
description: Ügyfél-előfizetések gyűjteményének beszerzése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a037e4a81fccbff0a02b0bdf6d93478ee15fd50f
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768352"
---
# <a name="get-a-customers-subscriptions"></a><span data-ttu-id="7894e-103">Egy ügyfél előfizetéseinek lekérése</span><span class="sxs-lookup"><span data-stu-id="7894e-103">Get a customer's subscriptions</span></span>

<span data-ttu-id="7894e-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="7894e-104">**Applies To**</span></span>

- <span data-ttu-id="7894e-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="7894e-105">Partner Center</span></span>
- <span data-ttu-id="7894e-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="7894e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="7894e-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="7894e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7894e-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="7894e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7894e-109">Ügyfél-előfizetések gyűjteményének beszerzése.</span><span class="sxs-lookup"><span data-stu-id="7894e-109">How to get a collection of a customer's subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7894e-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="7894e-110">Prerequisites</span></span>

- <span data-ttu-id="7894e-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="7894e-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7894e-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="7894e-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7894e-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7894e-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7894e-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="7894e-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7894e-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="7894e-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7894e-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7894e-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7894e-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="7894e-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7894e-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7894e-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="7894e-119">C\#</span><span class="sxs-lookup"><span data-stu-id="7894e-119">C\#</span></span>

<span data-ttu-id="7894e-120">Az ügyfél-előfizetések listájának lekéréséhez először használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="7894e-120">To get a list of all of a customer's subscriptions, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to identify the customer.</span></span> <span data-ttu-id="7894e-121">Ezután az [**előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonsággal kérhet le egy felületet az előfizetés-gyűjtési műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="7894e-121">Then use the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="7894e-122">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) metódust az ügyfél előfizetések gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="7894e-122">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) methods to retrieve the customer's subscriptions collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerSubscriptions = partnerOperations.Customers.ById(customerId).Subscriptions.Get();
```

<span data-ttu-id="7894e-123">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7894e-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7894e-124">**Projekt**: partner Center SDK Samples **osztály**: GetSubscriptions.cs</span><span class="sxs-lookup"><span data-stu-id="7894e-124">**Project**: Partner Center SDK Samples **Class**: GetSubscriptions.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7894e-125">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="7894e-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7894e-126">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="7894e-126">Request syntax</span></span>

| <span data-ttu-id="7894e-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="7894e-127">Method</span></span>  | <span data-ttu-id="7894e-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="7894e-128">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7894e-129">**GET**</span><span class="sxs-lookup"><span data-stu-id="7894e-129">**GET**</span></span> | <span data-ttu-id="7894e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions http/1.1</span><span class="sxs-lookup"><span data-stu-id="7894e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7894e-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="7894e-131">URI parameter</span></span>

<span data-ttu-id="7894e-132">Ez a táblázat felsorolja az összes előfizetés lekéréséhez szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="7894e-132">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="7894e-133">Név</span><span class="sxs-lookup"><span data-stu-id="7894e-133">Name</span></span>               | <span data-ttu-id="7894e-134">Típus</span><span class="sxs-lookup"><span data-stu-id="7894e-134">Type</span></span>   | <span data-ttu-id="7894e-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="7894e-135">Required</span></span> | <span data-ttu-id="7894e-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="7894e-136">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="7894e-137">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="7894e-137">customer-tenant-id</span></span> | <span data-ttu-id="7894e-138">sztring</span><span class="sxs-lookup"><span data-stu-id="7894e-138">string</span></span> | <span data-ttu-id="7894e-139">Igen</span><span class="sxs-lookup"><span data-stu-id="7894e-139">Yes</span></span>      | <span data-ttu-id="7894e-140">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="7894e-140">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7894e-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="7894e-141">Request headers</span></span>

<span data-ttu-id="7894e-142">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7894e-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7894e-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="7894e-143">Request body</span></span>

<span data-ttu-id="7894e-144">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="7894e-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7894e-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="7894e-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="7894e-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="7894e-146">REST response</span></span>

<span data-ttu-id="7894e-147">Ha ez sikeres, ez a metódus az [előfizetési](subscription-resources.md) erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="7894e-147">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7894e-148">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="7894e-148">Response success and error codes</span></span>

<span data-ttu-id="7894e-149">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="7894e-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7894e-150">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="7894e-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7894e-151">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="7894e-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7894e-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="7894e-152">Response example</span></span>

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
