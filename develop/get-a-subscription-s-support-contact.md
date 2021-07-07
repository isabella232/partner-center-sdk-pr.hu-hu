---
title: Egy előfizetés támogatási kapcsolattartójának lekérése
description: Hogyan lehet lekérte az előfizetés támogatási kapcsolattartóját.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b6c98e5ed96f2ca4787e93504c9e094bd46ae783
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760759"
---
# <a name="get-a-subscriptions-support-contact"></a><span data-ttu-id="d8899-103">Egy előfizetés támogatási kapcsolattartójának lekérése</span><span class="sxs-lookup"><span data-stu-id="d8899-103">Get a subscription's support contact</span></span>

<span data-ttu-id="d8899-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d8899-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d8899-105">Hogyan lehet lekérte az előfizetés támogatási kapcsolattartóját.</span><span class="sxs-lookup"><span data-stu-id="d8899-105">How to get a subscription's support contact.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8899-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d8899-106">Prerequisites</span></span>

- <span data-ttu-id="d8899-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d8899-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d8899-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="d8899-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d8899-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d8899-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d8899-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d8899-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d8899-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d8899-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d8899-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d8899-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d8899-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="d8899-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d8899-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d8899-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d8899-115">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="d8899-115">A subscription identifier.</span></span>

## <a name="c"></a><span data-ttu-id="d8899-116">C\#</span><span class="sxs-lookup"><span data-stu-id="d8899-116">C\#</span></span>

<span data-ttu-id="d8899-117">Az előfizetés támogatási kapcsolattartójának leához először használja az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="d8899-117">To get a subscription's support contact, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="d8899-118">Ezután az előfizetési műveletek interfészének lehívásához hívja meg a [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust az előfizetés azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="d8899-118">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="d8899-119">Ezután a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) tulajdonság használatával szerezzen be egy kapcsolatot támogató felületet, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) metódust a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) objektum lekérésére.</span><span class="sxs-lookup"><span data-stu-id="d8899-119">Next, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

<span data-ttu-id="d8899-120">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d8899-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d8899-121">**Project**: Partnerközpont SDK **osztály:** GetSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="d8899-121">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d8899-122">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d8899-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d8899-123">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="d8899-123">Request syntax</span></span>

| <span data-ttu-id="d8899-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="d8899-124">Method</span></span>  | <span data-ttu-id="d8899-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d8899-125">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d8899-126">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d8899-126">**GET**</span></span> | <span data-ttu-id="d8899-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/supportcontact HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d8899-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d8899-128">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d8899-128">URI parameter</span></span>

<span data-ttu-id="d8899-129">Az ügyfél és az előfizetés azonosításához használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="d8899-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="d8899-130">Név</span><span class="sxs-lookup"><span data-stu-id="d8899-130">Name</span></span>            | <span data-ttu-id="d8899-131">Típus</span><span class="sxs-lookup"><span data-stu-id="d8899-131">Type</span></span>   | <span data-ttu-id="d8899-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d8899-132">Required</span></span> | <span data-ttu-id="d8899-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="d8899-133">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="d8899-134">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="d8899-134">customer-id</span></span>     | <span data-ttu-id="d8899-135">sztring</span><span class="sxs-lookup"><span data-stu-id="d8899-135">string</span></span> | <span data-ttu-id="d8899-136">Igen</span><span class="sxs-lookup"><span data-stu-id="d8899-136">Yes</span></span>      | <span data-ttu-id="d8899-137">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="d8899-137">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="d8899-138">subscription-id</span><span class="sxs-lookup"><span data-stu-id="d8899-138">subscription-id</span></span> | <span data-ttu-id="d8899-139">sztring</span><span class="sxs-lookup"><span data-stu-id="d8899-139">string</span></span> | <span data-ttu-id="d8899-140">Igen</span><span class="sxs-lookup"><span data-stu-id="d8899-140">Yes</span></span>      | <span data-ttu-id="d8899-141">A próba-előfizetést azonosító GUID formátumú sztring.</span><span class="sxs-lookup"><span data-stu-id="d8899-141">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d8899-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d8899-142">Request headers</span></span>

<span data-ttu-id="d8899-143">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d8899-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d8899-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d8899-144">Request body</span></span>

<span data-ttu-id="d8899-145">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d8899-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d8899-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d8899-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d8899-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d8899-147">REST response</span></span>

<span data-ttu-id="d8899-148">Ha a művelet sikeres, a válasz törzse tartalmazza a [SupportContact erőforrást.](subscription-resources.md#supportcontact)</span><span class="sxs-lookup"><span data-stu-id="d8899-148">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d8899-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d8899-149">Response success and error codes</span></span>

<span data-ttu-id="d8899-150">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d8899-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d8899-151">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d8899-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d8899-152">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d8899-152">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d8899-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d8899-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CV: bLbUhqy0+ESOX1v4.0
MS-ServerId: 201022015
Date: Tue, 20 Jun 2017 19:30:19 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
