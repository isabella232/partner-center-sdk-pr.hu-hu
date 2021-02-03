---
title: Önkiszolgáló házirend frissítése
description: Önkiszolgáló házirend frissítése.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4d53ab8e5b8ef5b7be83360a3f43ec7791b2e3b4
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/08/2020
ms.locfileid: "97768668"
---
# <a name="update-a-selfservepolicy"></a><span data-ttu-id="8d24d-103">SelfServePolicy frissítése</span><span class="sxs-lookup"><span data-stu-id="8d24d-103">Update a SelfServePolicy</span></span>

<span data-ttu-id="8d24d-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="8d24d-104">**Applies to:**</span></span>

- <span data-ttu-id="8d24d-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="8d24d-105">Partner Center</span></span>

<span data-ttu-id="8d24d-106">Ez a témakör az önkiszolgáló szabályzatok frissítését ismerteti.</span><span class="sxs-lookup"><span data-stu-id="8d24d-106">This topic explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d24d-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8d24d-107">Prerequisites</span></span>

- <span data-ttu-id="8d24d-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="8d24d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8d24d-109">Ez a forgatókönyv támogatja az Application + felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="8d24d-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="8d24d-110">C\#</span><span class="sxs-lookup"><span data-stu-id="8d24d-110">C\#</span></span>

<span data-ttu-id="8d24d-111">Önkiszolgáló házirend törlése:</span><span class="sxs-lookup"><span data-stu-id="8d24d-111">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="8d24d-112">Hívja meg a [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metódust az entitás-azonosítóval, és kérje le a házirendek műveleteire szolgáló felületet.</span><span class="sxs-lookup"><span data-stu-id="8d24d-112">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="8d24d-113">A saját kiszolgálási szabályzat frissítéséhez hívja meg a [**put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) vagy a [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="8d24d-113">Call the [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) or [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) method to update the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a><span data-ttu-id="8d24d-114">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="8d24d-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8d24d-115">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="8d24d-115">Request syntax</span></span>

| <span data-ttu-id="8d24d-116">Metódus</span><span class="sxs-lookup"><span data-stu-id="8d24d-116">Method</span></span>   | <span data-ttu-id="8d24d-117">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="8d24d-117">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="8d24d-118">**PUT**</span><span class="sxs-lookup"><span data-stu-id="8d24d-118">**PUT**</span></span> | <span data-ttu-id="8d24d-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy http/1.1</span><span class="sxs-lookup"><span data-stu-id="8d24d-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8d24d-120">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="8d24d-120">Request headers</span></span>

- <span data-ttu-id="8d24d-121">A kérelem azonosítójának és korrelációs azonosítójának megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="8d24d-121">A request identifier and correlation identifier are required.</span></span>
- <span data-ttu-id="8d24d-122">További információért lásd a [partneri központ Rest-fejléceit](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="8d24d-122">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="8d24d-123">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="8d24d-123">Request body</span></span>

<span data-ttu-id="8d24d-124">Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="8d24d-124">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="8d24d-125">Név</span><span class="sxs-lookup"><span data-stu-id="8d24d-125">Name</span></span>                              | <span data-ttu-id="8d24d-126">Típus</span><span class="sxs-lookup"><span data-stu-id="8d24d-126">Type</span></span>   | <span data-ttu-id="8d24d-127">Leírás</span><span class="sxs-lookup"><span data-stu-id="8d24d-127">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="8d24d-128">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="8d24d-128">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="8d24d-129">object</span><span class="sxs-lookup"><span data-stu-id="8d24d-129">object</span></span> | <span data-ttu-id="8d24d-130">Az önkiszolgáló házirend adatai.</span><span class="sxs-lookup"><span data-stu-id="8d24d-130">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="8d24d-131">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="8d24d-131">SelfServePolicy</span></span>

<span data-ttu-id="8d24d-132">Ez a táblázat ismerteti az új önkiszolgáló házirend létrehozásához szükséges [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -erőforrás minimálisan szükséges mezőit.</span><span class="sxs-lookup"><span data-stu-id="8d24d-132">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="8d24d-133">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="8d24d-133">Property</span></span>              | <span data-ttu-id="8d24d-134">Típus</span><span class="sxs-lookup"><span data-stu-id="8d24d-134">Type</span></span>             | <span data-ttu-id="8d24d-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="8d24d-135">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8d24d-136">id</span><span class="sxs-lookup"><span data-stu-id="8d24d-136">id</span></span>                    | <span data-ttu-id="8d24d-137">sztring</span><span class="sxs-lookup"><span data-stu-id="8d24d-137">string</span></span>           | <span data-ttu-id="8d24d-138">Önkiszolgáló házirend-azonosító, amelyet az önkiszolgáló házirend sikeres létrehozásakor kell megadni.</span><span class="sxs-lookup"><span data-stu-id="8d24d-138">A self-serve policy identifier that is supplied upon successful creation of the self-serve policy.</span></span>     |
| <span data-ttu-id="8d24d-139">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="8d24d-139">SelfServeEntity</span></span>       | <span data-ttu-id="8d24d-140">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="8d24d-140">SelfServeEntity</span></span>  | <span data-ttu-id="8d24d-141">Az önkiszolgáló entitás, amely hozzáférést kap.</span><span class="sxs-lookup"><span data-stu-id="8d24d-141">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="8d24d-142">Megadó fél</span><span class="sxs-lookup"><span data-stu-id="8d24d-142">Grantor</span></span>               | <span data-ttu-id="8d24d-143">Megadó fél</span><span class="sxs-lookup"><span data-stu-id="8d24d-143">Grantor</span></span>          | <span data-ttu-id="8d24d-144">A hozzáférést biztosító biztosító.</span><span class="sxs-lookup"><span data-stu-id="8d24d-144">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="8d24d-145">Engedélyek</span><span class="sxs-lookup"><span data-stu-id="8d24d-145">Permissions</span></span>           | <span data-ttu-id="8d24d-146">Engedély tömbje</span><span class="sxs-lookup"><span data-stu-id="8d24d-146">Array of Permission</span></span>| <span data-ttu-id="8d24d-147">[Engedélyezési](self-serve-policy-resources.md#permission) erőforrások tömbje.</span><span class="sxs-lookup"><span data-stu-id="8d24d-147">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                      |
| <span data-ttu-id="8d24d-148">ETAG</span><span class="sxs-lookup"><span data-stu-id="8d24d-148">Etag</span></span>                  | <span data-ttu-id="8d24d-149">sztring</span><span class="sxs-lookup"><span data-stu-id="8d24d-149">string</span></span>           | <span data-ttu-id="8d24d-150">A ETAG.</span><span class="sxs-lookup"><span data-stu-id="8d24d-150">The Etag.</span></span>                                                                                               |


### <a name="request-example"></a><span data-ttu-id="8d24d-151">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8d24d-151">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="8d24d-152">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="8d24d-152">REST response</span></span>

<span data-ttu-id="8d24d-153">Ha ez sikeres, ez az API egy [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -erőforrást ad vissza a frissített önkiszolgáló házirendhez.</span><span class="sxs-lookup"><span data-stu-id="8d24d-153">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the updated self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8d24d-154">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="8d24d-154">Response success and error codes</span></span>

<span data-ttu-id="8d24d-155">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="8d24d-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8d24d-156">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="8d24d-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8d24d-157">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="8d24d-157">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="8d24d-158">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="8d24d-158">This method returns the following error codes:</span></span>

| <span data-ttu-id="8d24d-159">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="8d24d-159">HTTP Status Code</span></span>     | <span data-ttu-id="8d24d-160">Hibakód</span><span class="sxs-lookup"><span data-stu-id="8d24d-160">Error code</span></span>   | <span data-ttu-id="8d24d-161">Leírás</span><span class="sxs-lookup"><span data-stu-id="8d24d-161">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="8d24d-162">404</span><span class="sxs-lookup"><span data-stu-id="8d24d-162">404</span></span>                  | <span data-ttu-id="8d24d-163">600039</span><span class="sxs-lookup"><span data-stu-id="8d24d-163">600039</span></span>       | <span data-ttu-id="8d24d-164">Az önkiszolgáló házirend nem található</span><span class="sxs-lookup"><span data-stu-id="8d24d-164">Self-serve policy was not found</span></span>                                            |
| <span data-ttu-id="8d24d-165">404</span><span class="sxs-lookup"><span data-stu-id="8d24d-165">404</span></span>                  | <span data-ttu-id="8d24d-166">600040</span><span class="sxs-lookup"><span data-stu-id="8d24d-166">600040</span></span>       | <span data-ttu-id="8d24d-167">Az önkiszolgáló házirend-azonosító helytelen</span><span class="sxs-lookup"><span data-stu-id="8d24d-167">Self-serve policy identifier is incorrect</span></span>                                  |


### <a name="response-example"></a><span data-ttu-id="8d24d-168">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8d24d-168">Response example</span></span>

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
