---
title: Egy előfizetés támogatási kapcsolattartójának frissítése
description: Hogyan frissítheti egy előfizetés támogatási kapcsolattartóját a partner egyik hozzáadott értékkel bővült viszonteladóira.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c89f91fc9e89384a7be1237c08d7a9a1cfe3164
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530361"
---
# <a name="update-a-subscriptions-support-contact"></a><span data-ttu-id="ce906-103">Egy előfizetés támogatási kapcsolattartójának frissítése</span><span class="sxs-lookup"><span data-stu-id="ce906-103">Update a subscription's support contact</span></span>

<span data-ttu-id="ce906-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ce906-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ce906-105">Hogyan frissítheti egy előfizetés támogatási kapcsolattartóját a partner egyik hozzáadott értékkel bővült viszonteladóira.</span><span class="sxs-lookup"><span data-stu-id="ce906-105">How to update a subscription's support contact to one of the partner's value added resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce906-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="ce906-106">Prerequisites</span></span>

- <span data-ttu-id="ce906-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ce906-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ce906-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="ce906-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ce906-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ce906-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ce906-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="ce906-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ce906-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="ce906-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ce906-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="ce906-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ce906-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="ce906-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ce906-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ce906-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ce906-115">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="ce906-115">A subscription identifier.</span></span>

- <span data-ttu-id="ce906-116">Az új támogatási kapcsolattartóval kapcsolatos információk: bérlőazonosító, Microsoft Partner Network azonosító és név.</span><span class="sxs-lookup"><span data-stu-id="ce906-116">Information about the new support contact: tenant identifier, Microsoft Partner Network identifier, and name.</span></span> <span data-ttu-id="ce906-117">A támogatási kapcsolattartónak a partner értékével hozzáadott viszonteladók egyikének kell lennie.</span><span class="sxs-lookup"><span data-stu-id="ce906-117">The support contact must be one of the partner's value added resellers.</span></span>

## <a name="c"></a><span data-ttu-id="ce906-118">C\#</span><span class="sxs-lookup"><span data-stu-id="ce906-118">C\#</span></span>

<span data-ttu-id="ce906-119">Az előfizetés támogatási kapcsolattartóját úgy frissítheti, hogy először példányosul, majd feltölti a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) objektumot az új értékekkel.</span><span class="sxs-lookup"><span data-stu-id="ce906-119">To update a subscription's support contact, first instantiate and populate a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object with the new values.</span></span> <span data-ttu-id="ce906-120">Ezután használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="ce906-120">Then use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="ce906-121">Ezután szerezze be az előfizetési műveletek interfészét a [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódus az előfizetés azonosítójával való hívásával.</span><span class="sxs-lookup"><span data-stu-id="ce906-121">Next, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="ce906-122">Ezután a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) tulajdonság használatával szerezzen be egy felületet, amely támogatja a kapcsolattartási műveleteket.</span><span class="sxs-lookup"><span data-stu-id="ce906-122">Then, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations.</span></span> <span data-ttu-id="ce906-123">Végül hívja meg az [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) vagy [**az UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) metódust a kitöltve a SupportContact objektummal a támogatási kapcsolattartó frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="ce906-123">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) method with the populated SupportContact object to update the support contact.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Instantiate a SupportContact object and populate it with the new support contact information.
var supportContact = new SupportContact()
{
    Name = "Support contact's name",
    SupportTenantId = "Support contact's tenant ID",
    SupportMpnId = "Support contact's MPN ID"
};

// Update the support contact with a new object that has valid VAR values.
var updatedSupportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).SupportContact.Update(supportContact);
```

<span data-ttu-id="ce906-124">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ce906-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ce906-125">**Project:** Partnerközpont SDK **Osztály:** UpdateSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="ce906-125">**Project**: Partner Center SDK Samples **Class**: UpdateSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ce906-126">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="ce906-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ce906-127">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="ce906-127">Request syntax</span></span>

| <span data-ttu-id="ce906-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="ce906-128">Method</span></span>  | <span data-ttu-id="ce906-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="ce906-129">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ce906-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="ce906-130">**PUT**</span></span> | <span data-ttu-id="ce906-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/supportcontact HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ce906-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ce906-132">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="ce906-132">URI parameter</span></span>

<span data-ttu-id="ce906-133">Az ügyfél és az előfizetés azonosításához használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="ce906-133">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="ce906-134">Név</span><span class="sxs-lookup"><span data-stu-id="ce906-134">Name</span></span>            | <span data-ttu-id="ce906-135">Típus</span><span class="sxs-lookup"><span data-stu-id="ce906-135">Type</span></span>   | <span data-ttu-id="ce906-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="ce906-136">Required</span></span> | <span data-ttu-id="ce906-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="ce906-137">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="ce906-138">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="ce906-138">customer-id</span></span>     | <span data-ttu-id="ce906-139">sztring</span><span class="sxs-lookup"><span data-stu-id="ce906-139">string</span></span> | <span data-ttu-id="ce906-140">Igen</span><span class="sxs-lookup"><span data-stu-id="ce906-140">Yes</span></span>      | <span data-ttu-id="ce906-141">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="ce906-141">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="ce906-142">subscription-id (előfizetés-azonosító)</span><span class="sxs-lookup"><span data-stu-id="ce906-142">subscription-id</span></span> | <span data-ttu-id="ce906-143">sztring</span><span class="sxs-lookup"><span data-stu-id="ce906-143">string</span></span> | <span data-ttu-id="ce906-144">Igen</span><span class="sxs-lookup"><span data-stu-id="ce906-144">Yes</span></span>      | <span data-ttu-id="ce906-145">A próba-előfizetést azonosító GUID formátumú sztring.</span><span class="sxs-lookup"><span data-stu-id="ce906-145">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ce906-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="ce906-146">Request headers</span></span>

<span data-ttu-id="ce906-147">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ce906-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ce906-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="ce906-148">Request body</span></span>

<span data-ttu-id="ce906-149">A kérés törzsében meg kell lennie egy [feltöltve a SupportContact](subscription-resources.md#supportcontact) erőforrásnak.</span><span class="sxs-lookup"><span data-stu-id="ce906-149">You must include a populated [SupportContact](subscription-resources.md#supportcontact) resource in the request body.</span></span> <span data-ttu-id="ce906-150">A támogatási kapcsolattartónak egy meglévő viszonteladónak kell lennie, aki kapcsolatban áll a partnerrel.</span><span class="sxs-lookup"><span data-stu-id="ce906-150">The support contact must be an existing reseller with a relationship to the partner.</span></span>

### <a name="request-example"></a><span data-ttu-id="ce906-151">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ce906-151">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b72d732a-eed7-4a60-82d1-1b2e6cba0ed2
MS-CorrelationId: 84eff9e1-6a8c-42aa-8678-c00b0d3fb26f
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 320
Expect: 100-continue

{
    "SupportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "SupportMpnId": "4391507",
    "Name": "Trey Research",
    "Links": {
        "Self": {
            "Uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "Method": "Get",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "SupportContact"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="ce906-152">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="ce906-152">REST response</span></span>

<span data-ttu-id="ce906-153">Ha a művelet sikeres, a válasz törzse tartalmazza a [SupportContact erőforrást.](subscription-resources.md#supportcontact)</span><span class="sxs-lookup"><span data-stu-id="ce906-153">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ce906-154">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="ce906-154">Response success and error codes</span></span>

<span data-ttu-id="ce906-155">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="ce906-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ce906-156">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="ce906-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ce906-157">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ce906-157">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ce906-158">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ce906-158">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b0cd9bcc-742e-4c76-9e34-a96d3bdc7673
MS-RequestId: 7591ca22-d4e3-409d-bfa6-09806eaff4f3
MS-CV: W8Tzj6NGckKHcq+E.0
MS-ServerId: 030020344
Date: Wed, 21 Jun 2017 01:01:17 GMT

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
