---
title: Önkiszolgáló szabályzatok listájának beolvasása
description: Az ügyfél önkiszolgáló házirendjeit képviselő erőforrások gyűjteményének beszerzése.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ff3116b8757e28e03615930ebd19bc75f34e2efe
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/08/2020
ms.locfileid: "97768664"
---
# <a name="get-a-list-of-self-serve-policies"></a><span data-ttu-id="74a32-103">Önkiszolgáló szabályzatok listájának beolvasása</span><span class="sxs-lookup"><span data-stu-id="74a32-103">Get a list of self-serve policies</span></span>

<span data-ttu-id="74a32-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="74a32-104">**Applies to:**</span></span>

- <span data-ttu-id="74a32-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="74a32-105">Partner Center</span></span>

<span data-ttu-id="74a32-106">Ez a cikk azt ismerteti, hogyan szerezhet be olyan erőforrás-gyűjteményt, amely az entitások önkiszolgáló házirendjeit jelképezi.</span><span class="sxs-lookup"><span data-stu-id="74a32-106">This article describes how to get a collection of resources that represents self-serve policies for an entity.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74a32-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="74a32-107">Prerequisites</span></span>

- <span data-ttu-id="74a32-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="74a32-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="74a32-109">Ez a forgatókönyv támogatja az Application + felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="74a32-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="74a32-110">C\#</span><span class="sxs-lookup"><span data-stu-id="74a32-110">C\#</span></span>

<span data-ttu-id="74a32-111">Az összes önkiszolgáló házirend listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="74a32-111">To get a list of all self-serve policies:</span></span>

1. <span data-ttu-id="74a32-112">Hívja meg a [**IAggregatePartner. SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) metódust az entitás-azonosítóval, és kérje le a szabályzatok műveleteihez szükséges felületet.</span><span class="sxs-lookup"><span data-stu-id="74a32-112">Call the [**IAggregatePartner.SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// gets the self-serve policies
var SelfServePolicies = scopedPartnerOperations.SelfServePolicies.Get(customerIdAsEntity);
```

<span data-ttu-id="74a32-113">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="74a32-113">For an example, see the following:</span></span>

- <span data-ttu-id="74a32-114">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="74a32-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="74a32-115">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="74a32-115">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="74a32-116">Osztály: **GetSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="74a32-116">Class: **GetSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="74a32-117">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="74a32-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="74a32-118">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="74a32-118">Request syntax</span></span>

| <span data-ttu-id="74a32-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="74a32-119">Method</span></span>  | <span data-ttu-id="74a32-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="74a32-120">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="74a32-121">**GET**</span><span class="sxs-lookup"><span data-stu-id="74a32-121">**GET**</span></span> | <span data-ttu-id="74a32-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy? entity_id = {ENTITY_ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="74a32-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy?entity_id={entity_id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="74a32-123">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="74a32-123">URI parameter</span></span>

<span data-ttu-id="74a32-124">Használja az alábbi lekérdezési paramétert az ügyfelek listájának lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="74a32-124">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="74a32-125">Név</span><span class="sxs-lookup"><span data-stu-id="74a32-125">Name</span></span>          | <span data-ttu-id="74a32-126">Típus</span><span class="sxs-lookup"><span data-stu-id="74a32-126">Type</span></span>       | <span data-ttu-id="74a32-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="74a32-127">Required</span></span> | <span data-ttu-id="74a32-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="74a32-128">Description</span></span>                                        |
|---------------|------------|----------|----------------------------------------------------|
| <span data-ttu-id="74a32-129">**entity_id**</span><span class="sxs-lookup"><span data-stu-id="74a32-129">**entity_id**</span></span> | <span data-ttu-id="74a32-130">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="74a32-130">**string**</span></span> | <span data-ttu-id="74a32-131">Y</span><span class="sxs-lookup"><span data-stu-id="74a32-131">Y</span></span>        | <span data-ttu-id="74a32-132">A számára hozzáférést kérő entitás azonosítója.</span><span class="sxs-lookup"><span data-stu-id="74a32-132">The entity identifier requesting access for.</span></span> <span data-ttu-id="74a32-133">Ez lesz az ügyfél bérlői azonosítója.</span><span class="sxs-lookup"><span data-stu-id="74a32-133">This will be the customer's tenant ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="74a32-134">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="74a32-134">Request headers</span></span>

<span data-ttu-id="74a32-135">További információ: [fejlécek](headers.md).</span><span class="sxs-lookup"><span data-stu-id="74a32-135">For more information, see [Headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="74a32-136">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="74a32-136">Request body</span></span>

<span data-ttu-id="74a32-137">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="74a32-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="74a32-138">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="74a32-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy?entity_id=0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="74a32-139">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="74a32-139">REST response</span></span>

<span data-ttu-id="74a32-140">Ha ez sikeres, ez a metódus [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="74a32-140">If successful, this method returns a collection of [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="74a32-141">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="74a32-141">Response success and error codes</span></span>

<span data-ttu-id="74a32-142">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="74a32-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="74a32-143">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="74a32-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="74a32-144">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="74a32-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="74a32-145">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="74a32-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 1,
    "items": [{
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
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
