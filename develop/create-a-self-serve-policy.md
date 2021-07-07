---
title: Önkiszolgáló szabályzat létrehozása
description: Új önkiszolgáló szabályzat létrehozása.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14f46e22fbd294c765b745204cf62474250cbfbd
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973688"
---
# <a name="create-a-selfservepolicy"></a><span data-ttu-id="32596-103">SelfServePolicy létrehozása</span><span class="sxs-lookup"><span data-stu-id="32596-103">Create a SelfServePolicy</span></span>

<span data-ttu-id="32596-104">Ez a cikk bemutatja, hogyan hozhat létre új önkiszolgáló szabályzatot.</span><span class="sxs-lookup"><span data-stu-id="32596-104">This article explains how to create a new self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32596-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="32596-105">Prerequisites</span></span>

- <span data-ttu-id="32596-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="32596-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="32596-107">Ez a forgatókönyv támogatja az Application+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="32596-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="32596-108">C\#</span><span class="sxs-lookup"><span data-stu-id="32596-108">C\#</span></span>

<span data-ttu-id="32596-109">Önkiszolgáló szabályzat létrehozása:</span><span class="sxs-lookup"><span data-stu-id="32596-109">Create a self-serve policy:</span></span>

1. <span data-ttu-id="32596-110">Hívja meg az [**IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) vagy [**az IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) metódust az önkiszolgáló szabályzat adataival.</span><span class="sxs-lookup"><span data-stu-id="32596-110">Call the [**IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) or [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) method with the self-serve policy info.</span></span>

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

<span data-ttu-id="32596-111">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="32596-111">For an example, see the following:</span></span>

- <span data-ttu-id="32596-112">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="32596-112">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="32596-113">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="32596-113">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="32596-114">Osztály: **CreateSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="32596-114">Class: **CreateSelfServePolicies.cs**</span></span>


## <a name="rest-request"></a><span data-ttu-id="32596-115">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="32596-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="32596-116">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="32596-116">Request syntax</span></span>

| <span data-ttu-id="32596-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="32596-117">Method</span></span>   | <span data-ttu-id="32596-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="32596-118">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="32596-119">**Post**</span><span class="sxs-lookup"><span data-stu-id="32596-119">**POST**</span></span> | <span data-ttu-id="32596-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="32596-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="32596-121">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="32596-121">Request headers</span></span>

- <span data-ttu-id="32596-122">Szükség van egy kérésazonosítóra és egy korrelációs azonosítóra.</span><span class="sxs-lookup"><span data-stu-id="32596-122">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="32596-123">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="32596-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="32596-124">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="32596-124">Request body</span></span>

<span data-ttu-id="32596-125">Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="32596-125">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="32596-126">Név</span><span class="sxs-lookup"><span data-stu-id="32596-126">Name</span></span>                              | <span data-ttu-id="32596-127">Típus</span><span class="sxs-lookup"><span data-stu-id="32596-127">Type</span></span>   | <span data-ttu-id="32596-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="32596-128">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="32596-129">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="32596-129">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="32596-130">object</span><span class="sxs-lookup"><span data-stu-id="32596-130">object</span></span> | <span data-ttu-id="32596-131">Az önkiszolgáló szabályzat adatai.</span><span class="sxs-lookup"><span data-stu-id="32596-131">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="32596-132">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="32596-132">SelfServePolicy</span></span>

<span data-ttu-id="32596-133">Ez a táblázat az új önkiszolgáló szabályzat létrehozásához szükséges [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) erőforrás minimálisan szükséges mezőit ismerteti.</span><span class="sxs-lookup"><span data-stu-id="32596-133">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="32596-134">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="32596-134">Property</span></span>              | <span data-ttu-id="32596-135">Típus</span><span class="sxs-lookup"><span data-stu-id="32596-135">Type</span></span>             | <span data-ttu-id="32596-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="32596-136">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="32596-137">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="32596-137">SelfServeEntity</span></span>       | <span data-ttu-id="32596-138">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="32596-138">SelfServeEntity</span></span>  | <span data-ttu-id="32596-139">Az önkiszolgáló entitás, amely hozzáférést kap.</span><span class="sxs-lookup"><span data-stu-id="32596-139">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="32596-140">Grantor</span><span class="sxs-lookup"><span data-stu-id="32596-140">Grantor</span></span>               | <span data-ttu-id="32596-141">Grantor</span><span class="sxs-lookup"><span data-stu-id="32596-141">Grantor</span></span>          | <span data-ttu-id="32596-142">A hozzáférést megadó megadó.</span><span class="sxs-lookup"><span data-stu-id="32596-142">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="32596-143">Engedélyek</span><span class="sxs-lookup"><span data-stu-id="32596-143">Permissions</span></span>           | <span data-ttu-id="32596-144">Engedélytömb</span><span class="sxs-lookup"><span data-stu-id="32596-144">Array of Permission</span></span>| <span data-ttu-id="32596-145">[Engedélyerőforrások tömbje.](self-serve-policy-resources.md#permission)</span><span class="sxs-lookup"><span data-stu-id="32596-145">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                                     |


### <a name="request-example"></a><span data-ttu-id="32596-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="32596-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="32596-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="32596-147">REST response</span></span>

<span data-ttu-id="32596-148">Ha ez az API sikeres, egy [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) erőforrást ad vissza az új önkiszolgáló szabályzathoz.</span><span class="sxs-lookup"><span data-stu-id="32596-148">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the new self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="32596-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="32596-149">Response success and error codes</span></span>

<span data-ttu-id="32596-150">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="32596-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="32596-151">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="32596-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="32596-152">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="32596-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="32596-153">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="32596-153">This method returns the following error codes:</span></span>

| <span data-ttu-id="32596-154">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="32596-154">HTTP Status Code</span></span>     | <span data-ttu-id="32596-155">Hibakód</span><span class="sxs-lookup"><span data-stu-id="32596-155">Error code</span></span>   | <span data-ttu-id="32596-156">Leírás</span><span class="sxs-lookup"><span data-stu-id="32596-156">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="32596-157">409</span><span class="sxs-lookup"><span data-stu-id="32596-157">409</span></span>                  | <span data-ttu-id="32596-158">600041</span><span class="sxs-lookup"><span data-stu-id="32596-158">600041</span></span>       | <span data-ttu-id="32596-159">Az önkiszolgáló szabályzat már létezik.</span><span class="sxs-lookup"><span data-stu-id="32596-159">Self-serve policy already exists.</span></span>                                                     |


### <a name="response-example"></a><span data-ttu-id="32596-160">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="32596-160">Response example</span></span>

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
