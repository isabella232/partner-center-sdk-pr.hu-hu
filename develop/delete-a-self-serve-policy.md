---
title: Önkiszolgáló szabályzat törlése
description: Önkiszolgáló szabályzat törlése.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 063cf98d4c78e82622e486427baeb1a5721715e5
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973094"
---
# <a name="delete-a-selfservepolicy"></a><span data-ttu-id="74754-103">SelfServePolicy törlése</span><span class="sxs-lookup"><span data-stu-id="74754-103">Delete a SelfServePolicy</span></span>

<span data-ttu-id="74754-104">Ez a cikk az önkiszolgáló szabályzatok frissítését ismerteti.</span><span class="sxs-lookup"><span data-stu-id="74754-104">This article explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74754-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="74754-105">Prerequisites</span></span>

- <span data-ttu-id="74754-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="74754-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="74754-107">Ez a forgatókönyv támogatja az Application+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="74754-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="74754-108">C\#</span><span class="sxs-lookup"><span data-stu-id="74754-108">C\#</span></span>

<span data-ttu-id="74754-109">Önkiszolgáló szabályzat törlése:</span><span class="sxs-lookup"><span data-stu-id="74754-109">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="74754-110">Hívja meg az [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metódust az entitásazonosítóval, hogy lekérje a szabályzatok műveleteinek interfészét.</span><span class="sxs-lookup"><span data-stu-id="74754-110">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="74754-111">Az [**önkiszolgáló**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) szabályzat törléséhez hívja meg a Delete vagy [**a DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="74754-111">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) method to delete the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

<span data-ttu-id="74754-112">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="74754-112">For an example, see the following:</span></span>

- <span data-ttu-id="74754-113">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="74754-113">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="74754-114">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="74754-114">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="74754-115">Osztály: **DeleteSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="74754-115">Class: **DeleteSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="74754-116">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="74754-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="74754-117">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="74754-117">Request syntax</span></span>

| <span data-ttu-id="74754-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="74754-118">Method</span></span>  | <span data-ttu-id="74754-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="74754-119">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="74754-120">**Töröl**</span><span class="sxs-lookup"><span data-stu-id="74754-120">**DELETE**</span></span> | <span data-ttu-id="74754-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="74754-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="74754-122">**URI-paraméter**</span><span class="sxs-lookup"><span data-stu-id="74754-122">**URI parameter**</span></span>

<span data-ttu-id="74754-123">Az alábbi elérésiút-paraméterek használatával szerezze be a megadott terméket.</span><span class="sxs-lookup"><span data-stu-id="74754-123">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="74754-124">Név</span><span class="sxs-lookup"><span data-stu-id="74754-124">Name</span></span>                       | <span data-ttu-id="74754-125">Típus</span><span class="sxs-lookup"><span data-stu-id="74754-125">Type</span></span>         | <span data-ttu-id="74754-126">Kötelező</span><span class="sxs-lookup"><span data-stu-id="74754-126">Required</span></span> | <span data-ttu-id="74754-127">Leírás</span><span class="sxs-lookup"><span data-stu-id="74754-127">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="74754-128">**SelfServePolicy-id**</span><span class="sxs-lookup"><span data-stu-id="74754-128">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="74754-129">**sztring**</span><span class="sxs-lookup"><span data-stu-id="74754-129">**string**</span></span>   | <span data-ttu-id="74754-130">Igen</span><span class="sxs-lookup"><span data-stu-id="74754-130">Yes</span></span>      | <span data-ttu-id="74754-131">Az önkiszolgáló szabályzatot azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="74754-131">A string that identifies the self-serve policy.</span></span>                 |

### <a name="request-headers"></a><span data-ttu-id="74754-132">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="74754-132">Request headers</span></span>

- <span data-ttu-id="74754-133">Szükség van egy kérésazonosítóra és egy korrelációs azonosítóra.</span><span class="sxs-lookup"><span data-stu-id="74754-133">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="74754-134">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="74754-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="74754-135">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="74754-135">Request body</span></span>

<span data-ttu-id="74754-136">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="74754-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="74754-137">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="74754-137">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="74754-138">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="74754-138">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="74754-139">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="74754-139">Response success and error codes</span></span>

<span data-ttu-id="74754-140">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="74754-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="74754-141">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="74754-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="74754-142">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="74754-142">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="74754-143">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="74754-143">Response example</span></span>

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
