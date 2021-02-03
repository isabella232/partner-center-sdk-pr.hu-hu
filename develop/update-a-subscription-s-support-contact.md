---
title: Egy előfizetés támogatási kapcsolattartójának frissítése
description: Az előfizetés támogatási kapcsolattartójának frissítése a partner egyik hozzáadott értékének viszonteladója.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c8c6b658cfe6e14c75b0c06b177920ce3eb1b4ed
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768267"
---
# <a name="update-a-subscriptions-support-contact"></a><span data-ttu-id="b86d5-103">Egy előfizetés támogatási kapcsolattartójának frissítése</span><span class="sxs-lookup"><span data-stu-id="b86d5-103">Update a subscription's support contact</span></span>

<span data-ttu-id="b86d5-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="b86d5-104">**Applies To**</span></span>

- <span data-ttu-id="b86d5-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="b86d5-105">Partner Center</span></span>
- <span data-ttu-id="b86d5-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="b86d5-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b86d5-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="b86d5-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b86d5-108">Az előfizetés támogatási kapcsolattartójának frissítése a partner egyik hozzáadott értékének viszonteladója.</span><span class="sxs-lookup"><span data-stu-id="b86d5-108">How to update a subscription's support contact to one of the partner's value added resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b86d5-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b86d5-109">Prerequisites</span></span>

- <span data-ttu-id="b86d5-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="b86d5-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b86d5-111">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="b86d5-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b86d5-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b86d5-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b86d5-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="b86d5-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b86d5-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="b86d5-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b86d5-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="b86d5-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b86d5-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="b86d5-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b86d5-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b86d5-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b86d5-118">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="b86d5-118">A subscription identifier.</span></span>

- <span data-ttu-id="b86d5-119">Információ az új támogatási partnerről: bérlő azonosítója, Microsoft Partner Network azonosítója és neve.</span><span class="sxs-lookup"><span data-stu-id="b86d5-119">Information about the new support contact: tenant identifier, Microsoft Partner Network identifier, and name.</span></span> <span data-ttu-id="b86d5-120">A támogatási kapcsolattartónak a partner által hozzáadott értéknek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="b86d5-120">The support contact must be one of the partner's value added resellers.</span></span>

## <a name="c"></a><span data-ttu-id="b86d5-121">C\#</span><span class="sxs-lookup"><span data-stu-id="b86d5-121">C\#</span></span>

<span data-ttu-id="b86d5-122">Az előfizetés támogatási kapcsolattartójának frissítéséhez először hozzon létre egy [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) objektumot, és töltse fel az új értékekkel.</span><span class="sxs-lookup"><span data-stu-id="b86d5-122">To update a subscription's support contact, first instantiate and populate a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object with the new values.</span></span> <span data-ttu-id="b86d5-123">Ezután használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="b86d5-123">Then use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="b86d5-124">Ezután szerezzen be egy illesztőfelületet az előfizetési műveletekhez az [**előfizetések. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódus meghívásával az előfizetés-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="b86d5-124">Next, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="b86d5-125">Ezután a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) tulajdonsággal szerezzen be egy felületet a kapcsolattartási műveletek támogatásához.</span><span class="sxs-lookup"><span data-stu-id="b86d5-125">Then, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations.</span></span> <span data-ttu-id="b86d5-126">Végül hívja meg az [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) vagy a [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) metódust a feltöltött SupportContact objektummal a támogatási partner frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="b86d5-126">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) method with the populated SupportContact object to update the support contact.</span></span>

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

<span data-ttu-id="b86d5-127">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b86d5-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b86d5-128">**Projekt**: partner Center SDK Samples **osztály**: UpdateSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="b86d5-128">**Project**: Partner Center SDK Samples **Class**: UpdateSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b86d5-129">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="b86d5-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b86d5-130">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b86d5-130">Request syntax</span></span>

| <span data-ttu-id="b86d5-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="b86d5-131">Method</span></span>  | <span data-ttu-id="b86d5-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b86d5-132">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b86d5-133">**PUT**</span><span class="sxs-lookup"><span data-stu-id="b86d5-133">**PUT**</span></span> | <span data-ttu-id="b86d5-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/supportcontact http/1.1</span><span class="sxs-lookup"><span data-stu-id="b86d5-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b86d5-135">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="b86d5-135">URI parameter</span></span>

<span data-ttu-id="b86d5-136">A következő elérésiút-paraméterek használatával azonosíthatja az ügyfelet és az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="b86d5-136">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="b86d5-137">Név</span><span class="sxs-lookup"><span data-stu-id="b86d5-137">Name</span></span>            | <span data-ttu-id="b86d5-138">Típus</span><span class="sxs-lookup"><span data-stu-id="b86d5-138">Type</span></span>   | <span data-ttu-id="b86d5-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b86d5-139">Required</span></span> | <span data-ttu-id="b86d5-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="b86d5-140">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="b86d5-141">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="b86d5-141">customer-id</span></span>     | <span data-ttu-id="b86d5-142">sztring</span><span class="sxs-lookup"><span data-stu-id="b86d5-142">string</span></span> | <span data-ttu-id="b86d5-143">Igen</span><span class="sxs-lookup"><span data-stu-id="b86d5-143">Yes</span></span>      | <span data-ttu-id="b86d5-144">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="b86d5-144">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="b86d5-145">előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="b86d5-145">subscription-id</span></span> | <span data-ttu-id="b86d5-146">sztring</span><span class="sxs-lookup"><span data-stu-id="b86d5-146">string</span></span> | <span data-ttu-id="b86d5-147">Igen</span><span class="sxs-lookup"><span data-stu-id="b86d5-147">Yes</span></span>      | <span data-ttu-id="b86d5-148">Egy GUID formátumú karakterlánc, amely azonosítja a próba-előfizetést.</span><span class="sxs-lookup"><span data-stu-id="b86d5-148">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b86d5-149">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b86d5-149">Request headers</span></span>

<span data-ttu-id="b86d5-150">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b86d5-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b86d5-151">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b86d5-151">Request body</span></span>

<span data-ttu-id="b86d5-152">Tartalmaznia kell egy feltöltött [SupportContact](subscription-resources.md#supportcontact) -erőforrást a kérelem törzsében.</span><span class="sxs-lookup"><span data-stu-id="b86d5-152">You must include a populated [SupportContact](subscription-resources.md#supportcontact) resource in the request body.</span></span> <span data-ttu-id="b86d5-153">A támogatási kapcsolattartónak a partnerrel létesített kapcsolattal rendelkező meglévő viszonteladónak kell lennie.</span><span class="sxs-lookup"><span data-stu-id="b86d5-153">The support contact must be an existing reseller with a relationship to the partner.</span></span>

### <a name="request-example"></a><span data-ttu-id="b86d5-154">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b86d5-154">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b86d5-155">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b86d5-155">REST response</span></span>

<span data-ttu-id="b86d5-156">Ha a művelet sikeres, a válasz törzse tartalmazza a [SupportContact](subscription-resources.md#supportcontact) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="b86d5-156">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b86d5-157">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b86d5-157">Response success and error codes</span></span>

<span data-ttu-id="b86d5-158">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="b86d5-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b86d5-159">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="b86d5-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b86d5-160">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b86d5-160">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b86d5-161">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b86d5-161">Response example</span></span>

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
