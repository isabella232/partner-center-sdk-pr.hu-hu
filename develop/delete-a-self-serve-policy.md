---
title: Önkiszolgáló szabályzat törlése
description: Önkiszolgáló házirend törlése.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3450145d6daf2ffca5e2886245e592406cb0886d
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/08/2020
ms.locfileid: "97768656"
---
# <a name="delete-a-selfservepolicy"></a><span data-ttu-id="dbe80-103">SelfServePolicy törlése</span><span class="sxs-lookup"><span data-stu-id="dbe80-103">Delete a SelfServePolicy</span></span>

<span data-ttu-id="dbe80-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="dbe80-104">**Applies to:**</span></span>

- <span data-ttu-id="dbe80-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="dbe80-105">Partner Center</span></span>

<span data-ttu-id="dbe80-106">Ez a témakör az önkiszolgáló szabályzatok frissítését ismerteti.</span><span class="sxs-lookup"><span data-stu-id="dbe80-106">This topic explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbe80-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="dbe80-107">Prerequisites</span></span>

- <span data-ttu-id="dbe80-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="dbe80-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dbe80-109">Ez a forgatókönyv támogatja az Application + felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="dbe80-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="dbe80-110">C\#</span><span class="sxs-lookup"><span data-stu-id="dbe80-110">C\#</span></span>

<span data-ttu-id="dbe80-111">Önkiszolgáló házirend törlése:</span><span class="sxs-lookup"><span data-stu-id="dbe80-111">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="dbe80-112">Hívja meg a [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metódust az entitás-azonosítóval, és kérje le a házirendek műveleteire szolgáló felületet.</span><span class="sxs-lookup"><span data-stu-id="dbe80-112">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="dbe80-113">Az önkiszolgáló házirend törléséhez hívja meg a [**delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) vagy a [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="dbe80-113">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) method to delete the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

<span data-ttu-id="dbe80-114">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="dbe80-114">For an example, see the following:</span></span>

- <span data-ttu-id="dbe80-115">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="dbe80-115">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="dbe80-116">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="dbe80-116">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="dbe80-117">Osztály: **DeleteSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="dbe80-117">Class: **DeleteSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="dbe80-118">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="dbe80-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dbe80-119">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="dbe80-119">Request syntax</span></span>

| <span data-ttu-id="dbe80-120">Metódus</span><span class="sxs-lookup"><span data-stu-id="dbe80-120">Method</span></span>  | <span data-ttu-id="dbe80-121">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="dbe80-121">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="dbe80-122">**TÖRLÉSE**</span><span class="sxs-lookup"><span data-stu-id="dbe80-122">**DELETE**</span></span> | <span data-ttu-id="dbe80-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="dbe80-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="dbe80-124">**URI-paraméter**</span><span class="sxs-lookup"><span data-stu-id="dbe80-124">**URI parameter**</span></span>

<span data-ttu-id="dbe80-125">A megadott termék beolvasásához használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="dbe80-125">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="dbe80-126">Név</span><span class="sxs-lookup"><span data-stu-id="dbe80-126">Name</span></span>                       | <span data-ttu-id="dbe80-127">Típus</span><span class="sxs-lookup"><span data-stu-id="dbe80-127">Type</span></span>         | <span data-ttu-id="dbe80-128">Kötelező</span><span class="sxs-lookup"><span data-stu-id="dbe80-128">Required</span></span> | <span data-ttu-id="dbe80-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="dbe80-129">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="dbe80-130">**SelfServePolicy-azonosító**</span><span class="sxs-lookup"><span data-stu-id="dbe80-130">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="dbe80-131">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="dbe80-131">**string**</span></span>   | <span data-ttu-id="dbe80-132">Igen</span><span class="sxs-lookup"><span data-stu-id="dbe80-132">Yes</span></span>      | <span data-ttu-id="dbe80-133">Az önkiszolgáló házirendet azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="dbe80-133">A string that identifies the self-serve policy.</span></span>                 |

### <a name="request-headers"></a><span data-ttu-id="dbe80-134">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="dbe80-134">Request headers</span></span>

- <span data-ttu-id="dbe80-135">A kérelem AZONOSÍTÓjának és korrelációs AZONOSÍTÓjának megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="dbe80-135">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="dbe80-136">További információért lásd a [partneri központ Rest-fejléceit](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="dbe80-136">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="dbe80-137">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="dbe80-137">Request body</span></span>

<span data-ttu-id="dbe80-138">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="dbe80-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="dbe80-139">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="dbe80-139">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 789
Connection: Keep-Alive

```

## <a name="rest-response"></a><span data-ttu-id="dbe80-140">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="dbe80-140">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dbe80-141">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="dbe80-141">Response success and error codes</span></span>

<span data-ttu-id="dbe80-142">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="dbe80-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dbe80-143">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="dbe80-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dbe80-144">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="dbe80-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dbe80-145">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="dbe80-145">Response example</span></span>

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
