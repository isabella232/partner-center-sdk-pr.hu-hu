---
title: Önkiszolgáló házirend létrehozása
description: Új önkiszolgáló házirend létrehozása
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd1579b2775ead57a440db0d6afb3bf22164c319
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/08/2020
ms.locfileid: "97768652"
---
# <a name="create-a-selfservepolicy"></a><span data-ttu-id="80f74-103">SelfServePolicy létrehozása</span><span class="sxs-lookup"><span data-stu-id="80f74-103">Create a SelfServePolicy</span></span>

<span data-ttu-id="80f74-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="80f74-104">**Applies to:**</span></span>

- <span data-ttu-id="80f74-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="80f74-105">Partner Center</span></span>

<span data-ttu-id="80f74-106">Ez a témakör bemutatja, hogyan hozhat létre új, önkiszolgáló házirendet.</span><span class="sxs-lookup"><span data-stu-id="80f74-106">This topic explains how to create a new self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80f74-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="80f74-107">Prerequisites</span></span>

- <span data-ttu-id="80f74-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="80f74-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="80f74-109">Ez a forgatókönyv támogatja az Application + felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="80f74-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="80f74-110">C\#</span><span class="sxs-lookup"><span data-stu-id="80f74-110">C\#</span></span>

<span data-ttu-id="80f74-111">Önkiszolgáló házirend létrehozása:</span><span class="sxs-lookup"><span data-stu-id="80f74-111">Create a self-serve policy:</span></span>

1. <span data-ttu-id="80f74-112">Hívja meg a [**IAggregatePartner. SelfServePolicies. Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) vagy a [**IAggregatePartner. SelfServePolicies. CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) metódust az önkiszolgáló házirend adataival.</span><span class="sxs-lookup"><span data-stu-id="80f74-112">Call the [**IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) or [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) method with the self-serve policy info.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string customerIdAsEntity;

var selfServePolicy = new SelfServePolicy
{
    SelfServeEntity = new SelfServeEntity
    {
        SelfServeEntityType = "customer",
        TenantID = customerIdAsEntity,
    },
    Grantor = new Grantor
    {
        GrantorType = "billToPartner",
        TenantID = partnerIdAsGrantor,
    },
    Permissions = new Permission[]
    {
        new Permission
        {
        Action = "Purchase",
        Resource = "AzureReservedInstances",
        },
    },
};

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// creates the self-serve policy
SelfServePolicy createdSelfServePolicy = scopedPartnerOperations.selfServePolicies.Create(selfServePolicy);
```

<span data-ttu-id="80f74-113">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="80f74-113">For an example, see the following:</span></span>

- <span data-ttu-id="80f74-114">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="80f74-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="80f74-115">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="80f74-115">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="80f74-116">Osztály: **CreateSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="80f74-116">Class: **CreateSelfServePolicies.cs**</span></span>


## <a name="rest-request"></a><span data-ttu-id="80f74-117">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="80f74-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="80f74-118">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="80f74-118">Request syntax</span></span>

| <span data-ttu-id="80f74-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="80f74-119">Method</span></span>   | <span data-ttu-id="80f74-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="80f74-120">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="80f74-121">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="80f74-121">**POST**</span></span> | <span data-ttu-id="80f74-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy http/1.1</span><span class="sxs-lookup"><span data-stu-id="80f74-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="80f74-123">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="80f74-123">Request headers</span></span>

- <span data-ttu-id="80f74-124">A kérelem AZONOSÍTÓjának és korrelációs AZONOSÍTÓjának megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="80f74-124">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="80f74-125">További információért lásd a [partneri központ Rest-fejléceit](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="80f74-125">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="80f74-126">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="80f74-126">Request body</span></span>

<span data-ttu-id="80f74-127">Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="80f74-127">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="80f74-128">Név</span><span class="sxs-lookup"><span data-stu-id="80f74-128">Name</span></span>                              | <span data-ttu-id="80f74-129">Típus</span><span class="sxs-lookup"><span data-stu-id="80f74-129">Type</span></span>   | <span data-ttu-id="80f74-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="80f74-130">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="80f74-131">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="80f74-131">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="80f74-132">object</span><span class="sxs-lookup"><span data-stu-id="80f74-132">object</span></span> | <span data-ttu-id="80f74-133">Az önkiszolgáló házirend adatai.</span><span class="sxs-lookup"><span data-stu-id="80f74-133">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="80f74-134">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="80f74-134">SelfServePolicy</span></span>

<span data-ttu-id="80f74-135">Ez a táblázat ismerteti az új önkiszolgáló házirend létrehozásához szükséges [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -erőforrás minimálisan szükséges mezőit.</span><span class="sxs-lookup"><span data-stu-id="80f74-135">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="80f74-136">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="80f74-136">Property</span></span>              | <span data-ttu-id="80f74-137">Típus</span><span class="sxs-lookup"><span data-stu-id="80f74-137">Type</span></span>             | <span data-ttu-id="80f74-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="80f74-138">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="80f74-139">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="80f74-139">SelfServeEntity</span></span>       | <span data-ttu-id="80f74-140">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="80f74-140">SelfServeEntity</span></span>  | <span data-ttu-id="80f74-141">Az önkiszolgáló entitás, amely hozzáférést kap.</span><span class="sxs-lookup"><span data-stu-id="80f74-141">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="80f74-142">Megadó fél</span><span class="sxs-lookup"><span data-stu-id="80f74-142">Grantor</span></span>               | <span data-ttu-id="80f74-143">Megadó fél</span><span class="sxs-lookup"><span data-stu-id="80f74-143">Grantor</span></span>          | <span data-ttu-id="80f74-144">A hozzáférést biztosító biztosító.</span><span class="sxs-lookup"><span data-stu-id="80f74-144">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="80f74-145">Engedélyek</span><span class="sxs-lookup"><span data-stu-id="80f74-145">Permissions</span></span>           | <span data-ttu-id="80f74-146">Engedély tömbje</span><span class="sxs-lookup"><span data-stu-id="80f74-146">Array of Permission</span></span>| <span data-ttu-id="80f74-147">[Engedélyezési](self-serve-policy-resources.md#permission) erőforrások tömbje.</span><span class="sxs-lookup"><span data-stu-id="80f74-147">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                                     |


### <a name="request-example"></a><span data-ttu-id="80f74-148">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="80f74-148">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
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
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="80f74-149">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="80f74-149">REST response</span></span>

<span data-ttu-id="80f74-150">Ha ez sikeres, ez az API egy [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -erőforrást ad vissza az új önkiszolgáló házirendhez.</span><span class="sxs-lookup"><span data-stu-id="80f74-150">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the new self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="80f74-151">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="80f74-151">Response success and error codes</span></span>

<span data-ttu-id="80f74-152">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="80f74-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="80f74-153">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="80f74-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="80f74-154">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="80f74-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="80f74-155">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="80f74-155">This method returns the following error codes:</span></span>

| <span data-ttu-id="80f74-156">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="80f74-156">HTTP Status Code</span></span>     | <span data-ttu-id="80f74-157">Hibakód</span><span class="sxs-lookup"><span data-stu-id="80f74-157">Error code</span></span>   | <span data-ttu-id="80f74-158">Leírás</span><span class="sxs-lookup"><span data-stu-id="80f74-158">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="80f74-159">409</span><span class="sxs-lookup"><span data-stu-id="80f74-159">409</span></span>                  | <span data-ttu-id="80f74-160">600041</span><span class="sxs-lookup"><span data-stu-id="80f74-160">600041</span></span>       | <span data-ttu-id="80f74-161">Az önkiszolgáló házirend már létezik.</span><span class="sxs-lookup"><span data-stu-id="80f74-161">Self-serve policy already exists.</span></span>                                                     |


### <a name="response-example"></a><span data-ttu-id="80f74-162">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="80f74-162">Response example</span></span>

```http
HTTP/1.1 201 Created
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
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```
