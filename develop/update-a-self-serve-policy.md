---
title: Önkiszolgáló szabályzat frissítése
description: Önkiszolgáló szabályzat frissítése.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d94382e73fd2a79751fe5f8f8414df2befde584f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445255"
---
# <a name="update-a-selfservepolicy"></a><span data-ttu-id="74cc7-103">SelfServePolicy frissítése</span><span class="sxs-lookup"><span data-stu-id="74cc7-103">Update a SelfServePolicy</span></span>

<span data-ttu-id="74cc7-104">Ez a cikk az önkiszolgáló szabályzatok frissítését ismerteti.</span><span class="sxs-lookup"><span data-stu-id="74cc7-104">This article explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74cc7-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="74cc7-105">Prerequisites</span></span>

- <span data-ttu-id="74cc7-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="74cc7-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="74cc7-107">Ez a forgatókönyv támogatja az Application+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="74cc7-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="74cc7-108">C\#</span><span class="sxs-lookup"><span data-stu-id="74cc7-108">C\#</span></span>

<span data-ttu-id="74cc7-109">Önkiszolgáló szabályzat törlése:</span><span class="sxs-lookup"><span data-stu-id="74cc7-109">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="74cc7-110">Hívja meg az [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metódust az entitásazonosítóval, hogy lekérje a szabályzatok műveleteinek interfészét.</span><span class="sxs-lookup"><span data-stu-id="74cc7-110">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="74cc7-111">Az önkiszolgáló szabályzat frissítéséhez hívja meg a [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) vagy [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="74cc7-111">Call the [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) or [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) method to update the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a><span data-ttu-id="74cc7-112">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="74cc7-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="74cc7-113">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="74cc7-113">Request syntax</span></span>

| <span data-ttu-id="74cc7-114">Metódus</span><span class="sxs-lookup"><span data-stu-id="74cc7-114">Method</span></span>   | <span data-ttu-id="74cc7-115">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="74cc7-115">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="74cc7-116">**PUT**</span><span class="sxs-lookup"><span data-stu-id="74cc7-116">**PUT**</span></span> | <span data-ttu-id="74cc7-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="74cc7-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="74cc7-118">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="74cc7-118">Request headers</span></span>

- <span data-ttu-id="74cc7-119">Szükség van egy kérelem- és korrelációs azonosítóra.</span><span class="sxs-lookup"><span data-stu-id="74cc7-119">A request identifier and correlation identifier are required.</span></span>
- <span data-ttu-id="74cc7-120">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="74cc7-120">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="74cc7-121">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="74cc7-121">Request body</span></span>

<span data-ttu-id="74cc7-122">Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="74cc7-122">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="74cc7-123">Név</span><span class="sxs-lookup"><span data-stu-id="74cc7-123">Name</span></span>                              | <span data-ttu-id="74cc7-124">Típus</span><span class="sxs-lookup"><span data-stu-id="74cc7-124">Type</span></span>   | <span data-ttu-id="74cc7-125">Leírás</span><span class="sxs-lookup"><span data-stu-id="74cc7-125">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="74cc7-126">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="74cc7-126">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="74cc7-127">object</span><span class="sxs-lookup"><span data-stu-id="74cc7-127">object</span></span> | <span data-ttu-id="74cc7-128">Az önkiszolgáló szabályzat adatai.</span><span class="sxs-lookup"><span data-stu-id="74cc7-128">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="74cc7-129">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="74cc7-129">SelfServePolicy</span></span>

<span data-ttu-id="74cc7-130">Ez a táblázat az új önkiszolgáló szabályzat létrehozásához szükséges [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) erőforrás minimálisan szükséges mezőit ismerteti.</span><span class="sxs-lookup"><span data-stu-id="74cc7-130">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="74cc7-131">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="74cc7-131">Property</span></span>              | <span data-ttu-id="74cc7-132">Típus</span><span class="sxs-lookup"><span data-stu-id="74cc7-132">Type</span></span>             | <span data-ttu-id="74cc7-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="74cc7-133">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="74cc7-134">id</span><span class="sxs-lookup"><span data-stu-id="74cc7-134">id</span></span>                    | <span data-ttu-id="74cc7-135">sztring</span><span class="sxs-lookup"><span data-stu-id="74cc7-135">string</span></span>           | <span data-ttu-id="74cc7-136">Önkiszolgáló szabályzatazonosító, amely az önkiszolgáló szabályzat sikeres létrehozása után lesz megadva.</span><span class="sxs-lookup"><span data-stu-id="74cc7-136">A self-serve policy identifier that is supplied upon successful creation of the self-serve policy.</span></span>     |
| <span data-ttu-id="74cc7-137">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="74cc7-137">SelfServeEntity</span></span>       | <span data-ttu-id="74cc7-138">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="74cc7-138">SelfServeEntity</span></span>  | <span data-ttu-id="74cc7-139">Az önkiszolgáló entitás, amely hozzáférést kap.</span><span class="sxs-lookup"><span data-stu-id="74cc7-139">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="74cc7-140">Grantor</span><span class="sxs-lookup"><span data-stu-id="74cc7-140">Grantor</span></span>               | <span data-ttu-id="74cc7-141">Grantor</span><span class="sxs-lookup"><span data-stu-id="74cc7-141">Grantor</span></span>          | <span data-ttu-id="74cc7-142">A hozzáférést megadó megadó.</span><span class="sxs-lookup"><span data-stu-id="74cc7-142">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="74cc7-143">Engedélyek</span><span class="sxs-lookup"><span data-stu-id="74cc7-143">Permissions</span></span>           | <span data-ttu-id="74cc7-144">Engedélytömb</span><span class="sxs-lookup"><span data-stu-id="74cc7-144">Array of Permission</span></span>| <span data-ttu-id="74cc7-145">[Engedélyerőforrások tömbje.](self-serve-policy-resources.md#permission)</span><span class="sxs-lookup"><span data-stu-id="74cc7-145">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                      |
| <span data-ttu-id="74cc7-146">Etag</span><span class="sxs-lookup"><span data-stu-id="74cc7-146">Etag</span></span>                  | <span data-ttu-id="74cc7-147">sztring</span><span class="sxs-lookup"><span data-stu-id="74cc7-147">string</span></span>           | <span data-ttu-id="74cc7-148">Az Etag.</span><span class="sxs-lookup"><span data-stu-id="74cc7-148">The Etag.</span></span>                                                                                               |


### <a name="request-example"></a><span data-ttu-id="74cc7-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="74cc7-149">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="74cc7-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="74cc7-150">REST response</span></span>

<span data-ttu-id="74cc7-151">Sikeres művelet esetén ez az API egy [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) erőforrást ad vissza a frissített önkiszolgáló szabályzathoz.</span><span class="sxs-lookup"><span data-stu-id="74cc7-151">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the updated self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="74cc7-152">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="74cc7-152">Response success and error codes</span></span>

<span data-ttu-id="74cc7-153">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="74cc7-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="74cc7-154">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="74cc7-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="74cc7-155">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="74cc7-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="74cc7-156">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="74cc7-156">This method returns the following error codes:</span></span>

| <span data-ttu-id="74cc7-157">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="74cc7-157">HTTP Status Code</span></span>     | <span data-ttu-id="74cc7-158">Hibakód</span><span class="sxs-lookup"><span data-stu-id="74cc7-158">Error code</span></span>   | <span data-ttu-id="74cc7-159">Leírás</span><span class="sxs-lookup"><span data-stu-id="74cc7-159">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="74cc7-160">404</span><span class="sxs-lookup"><span data-stu-id="74cc7-160">404</span></span>                  | <span data-ttu-id="74cc7-161">600039</span><span class="sxs-lookup"><span data-stu-id="74cc7-161">600039</span></span>       | <span data-ttu-id="74cc7-162">Az önkiszolgáló szabályzat nem található</span><span class="sxs-lookup"><span data-stu-id="74cc7-162">Self-serve policy was not found</span></span>                                            |
| <span data-ttu-id="74cc7-163">404</span><span class="sxs-lookup"><span data-stu-id="74cc7-163">404</span></span>                  | <span data-ttu-id="74cc7-164">600040</span><span class="sxs-lookup"><span data-stu-id="74cc7-164">600040</span></span>       | <span data-ttu-id="74cc7-165">Az önkiszolgáló szabályzatazonosító helytelen</span><span class="sxs-lookup"><span data-stu-id="74cc7-165">Self-serve policy identifier is incorrect</span></span>                                  |


### <a name="response-example"></a><span data-ttu-id="74cc7-166">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="74cc7-166">Response example</span></span>

```http
HTTP/1.1 200 Ok
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"1ec98034-a249-46f4-b9dd-9cd464fb5e47\"",
        "objectType": "SelfServePolicy"
    }
}
```
