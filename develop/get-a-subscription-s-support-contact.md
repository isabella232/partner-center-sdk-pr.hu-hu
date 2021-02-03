---
title: Egy előfizetés támogatási kapcsolattartójának lekérése
description: Előfizetés támogatási partnerének beszerzése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df3bce48902d95dc541c4a45e4e633569fc4406e
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768056"
---
# <a name="get-a-subscriptions-support-contact"></a><span data-ttu-id="946b1-103">Egy előfizetés támogatási kapcsolattartójának lekérése</span><span class="sxs-lookup"><span data-stu-id="946b1-103">Get a subscription's support contact</span></span>

<span data-ttu-id="946b1-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="946b1-104">**Applies To**</span></span>

- <span data-ttu-id="946b1-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="946b1-105">Partner Center</span></span>
- <span data-ttu-id="946b1-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="946b1-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="946b1-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="946b1-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="946b1-108">Előfizetés támogatási partnerének beszerzése.</span><span class="sxs-lookup"><span data-stu-id="946b1-108">How to get a subscription's support contact.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="946b1-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="946b1-109">Prerequisites</span></span>

- <span data-ttu-id="946b1-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="946b1-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="946b1-111">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="946b1-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="946b1-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="946b1-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="946b1-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="946b1-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="946b1-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="946b1-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="946b1-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="946b1-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="946b1-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="946b1-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="946b1-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="946b1-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="946b1-118">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="946b1-118">A subscription identifier.</span></span>

## <a name="c"></a><span data-ttu-id="946b1-119">C\#</span><span class="sxs-lookup"><span data-stu-id="946b1-119">C\#</span></span>

<span data-ttu-id="946b1-120">Az előfizetés támogatási kapcsolattartójának beszerzéséhez először a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust kell használnia az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="946b1-120">To get a subscription's support contact, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="946b1-121">Ezután kérjen meg egy illesztőfelületet az előfizetési műveletekhez az [**előfizetések. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódus meghívásával az előfizetés-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="946b1-121">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="946b1-122">Ezután a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) tulajdonsággal szerezzen be egy felületet a kapcsolattartási műveletek támogatásához, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) metódust a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) objektum lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="946b1-122">Next, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

<span data-ttu-id="946b1-123">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="946b1-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="946b1-124">**Projekt**: partner Center SDK Samples **osztály**: GetSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="946b1-124">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="946b1-125">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="946b1-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="946b1-126">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="946b1-126">Request syntax</span></span>

| <span data-ttu-id="946b1-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="946b1-127">Method</span></span>  | <span data-ttu-id="946b1-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="946b1-128">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="946b1-129">**GET**</span><span class="sxs-lookup"><span data-stu-id="946b1-129">**GET**</span></span> | <span data-ttu-id="946b1-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/supportcontact http/1.1</span><span class="sxs-lookup"><span data-stu-id="946b1-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="946b1-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="946b1-131">URI parameter</span></span>

<span data-ttu-id="946b1-132">A következő elérésiút-paraméterek használatával azonosíthatja az ügyfelet és az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="946b1-132">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="946b1-133">Név</span><span class="sxs-lookup"><span data-stu-id="946b1-133">Name</span></span>            | <span data-ttu-id="946b1-134">Típus</span><span class="sxs-lookup"><span data-stu-id="946b1-134">Type</span></span>   | <span data-ttu-id="946b1-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="946b1-135">Required</span></span> | <span data-ttu-id="946b1-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="946b1-136">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="946b1-137">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="946b1-137">customer-id</span></span>     | <span data-ttu-id="946b1-138">sztring</span><span class="sxs-lookup"><span data-stu-id="946b1-138">string</span></span> | <span data-ttu-id="946b1-139">Igen</span><span class="sxs-lookup"><span data-stu-id="946b1-139">Yes</span></span>      | <span data-ttu-id="946b1-140">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="946b1-140">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="946b1-141">előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="946b1-141">subscription-id</span></span> | <span data-ttu-id="946b1-142">sztring</span><span class="sxs-lookup"><span data-stu-id="946b1-142">string</span></span> | <span data-ttu-id="946b1-143">Igen</span><span class="sxs-lookup"><span data-stu-id="946b1-143">Yes</span></span>      | <span data-ttu-id="946b1-144">Egy GUID formátumú karakterlánc, amely azonosítja a próba-előfizetést.</span><span class="sxs-lookup"><span data-stu-id="946b1-144">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="946b1-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="946b1-145">Request headers</span></span>

<span data-ttu-id="946b1-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="946b1-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="946b1-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="946b1-147">Request body</span></span>

<span data-ttu-id="946b1-148">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="946b1-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="946b1-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="946b1-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="946b1-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="946b1-150">REST response</span></span>

<span data-ttu-id="946b1-151">Ha a művelet sikeres, a válasz törzse tartalmazza a [SupportContact](subscription-resources.md#supportcontact) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="946b1-151">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="946b1-152">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="946b1-152">Response success and error codes</span></span>

<span data-ttu-id="946b1-153">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="946b1-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="946b1-154">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="946b1-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="946b1-155">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="946b1-155">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="946b1-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="946b1-156">Response example</span></span>

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
