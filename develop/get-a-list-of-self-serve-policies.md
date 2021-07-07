---
title: Önkiszolgáló szabályzatok listájának lekért listája
description: Az ügyfél önkiszolgáló szabályzatát képviselő erőforrások gyűjteményének lekért gyűjtése.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b18fde8a11d3ed3dd31e50fdba746dd6b0bf3f97
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025733"
---
# <a name="get-a-list-of-self-serve-policies"></a><span data-ttu-id="72ac3-103">Önkiszolgáló szabályzatok listájának lekért listája</span><span class="sxs-lookup"><span data-stu-id="72ac3-103">Get a list of self-serve policies</span></span>

<span data-ttu-id="72ac3-104">Lekért erőforrások gyűjteményét, amelyek egy entitás önkiszolgáló szabályzatát képviselik.</span><span class="sxs-lookup"><span data-stu-id="72ac3-104">Gets a collection of resources that represents self-serve policies for an entity.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72ac3-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="72ac3-105">Prerequisites</span></span>

- <span data-ttu-id="72ac3-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="72ac3-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="72ac3-107">Ez a forgatókönyv az Application+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="72ac3-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="72ac3-108">C\#</span><span class="sxs-lookup"><span data-stu-id="72ac3-108">C\#</span></span>

<span data-ttu-id="72ac3-109">Az összes önkiszolgáló szabályzat listájának lekért listája:</span><span class="sxs-lookup"><span data-stu-id="72ac3-109">To get a list of all self-serve policies:</span></span>

1. <span data-ttu-id="72ac3-110">Hívja meg az [**IAggregatePartner.SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) metódust az entitásazonosítóval, hogy lekérje a szabályzatok műveleteinek interfészét.</span><span class="sxs-lookup"><span data-stu-id="72ac3-110">Call the [**IAggregatePartner.SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// gets the self-serve policies
var SelfServePolicies = scopedPartnerOperations.SelfServePolicies.Get(customerIdAsEntity);
```

<span data-ttu-id="72ac3-111">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="72ac3-111">For an example, see the following:</span></span>

- <span data-ttu-id="72ac3-112">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="72ac3-112">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="72ac3-113">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="72ac3-113">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="72ac3-114">Osztály: **GetSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="72ac3-114">Class: **GetSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="72ac3-115">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="72ac3-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="72ac3-116">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="72ac3-116">Request syntax</span></span>

| <span data-ttu-id="72ac3-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="72ac3-117">Method</span></span>  | <span data-ttu-id="72ac3-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="72ac3-118">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="72ac3-119">**Kap**</span><span class="sxs-lookup"><span data-stu-id="72ac3-119">**GET**</span></span> | <span data-ttu-id="72ac3-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy?entity_id={entity_id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="72ac3-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy?entity_id={entity_id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="72ac3-121">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="72ac3-121">URI parameter</span></span>

<span data-ttu-id="72ac3-122">Az alábbi lekérdezési paraméterrel lekérdezheti az ügyfelek listáját.</span><span class="sxs-lookup"><span data-stu-id="72ac3-122">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="72ac3-123">Név</span><span class="sxs-lookup"><span data-stu-id="72ac3-123">Name</span></span>          | <span data-ttu-id="72ac3-124">Típus</span><span class="sxs-lookup"><span data-stu-id="72ac3-124">Type</span></span>       | <span data-ttu-id="72ac3-125">Kötelező</span><span class="sxs-lookup"><span data-stu-id="72ac3-125">Required</span></span> | <span data-ttu-id="72ac3-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="72ac3-126">Description</span></span>                                        |
|---------------|------------|----------|----------------------------------------------------|
| <span data-ttu-id="72ac3-127">**entity_id**</span><span class="sxs-lookup"><span data-stu-id="72ac3-127">**entity_id**</span></span> | <span data-ttu-id="72ac3-128">**sztring**</span><span class="sxs-lookup"><span data-stu-id="72ac3-128">**string**</span></span> | <span data-ttu-id="72ac3-129">Y</span><span class="sxs-lookup"><span data-stu-id="72ac3-129">Y</span></span>        | <span data-ttu-id="72ac3-130">A hozzáférést kérő entitásazonosító.</span><span class="sxs-lookup"><span data-stu-id="72ac3-130">The entity identifier requesting access for.</span></span> <span data-ttu-id="72ac3-131">Ez lesz az ügyfél bérlőazonosítója.</span><span class="sxs-lookup"><span data-stu-id="72ac3-131">This will be the customer's tenant ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="72ac3-132">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="72ac3-132">Request headers</span></span>

<span data-ttu-id="72ac3-133">További információ: [Fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="72ac3-133">For more information, see [Headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="72ac3-134">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="72ac3-134">Request body</span></span>

<span data-ttu-id="72ac3-135">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="72ac3-135">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="72ac3-136">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="72ac3-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy?entity_id=0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="72ac3-137">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="72ac3-137">REST response</span></span>

<span data-ttu-id="72ac3-138">Ha ez a módszer sikeres, a válasz törzsében [a SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) erőforrások gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="72ac3-138">If successful, this method returns a collection of [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="72ac3-139">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="72ac3-139">Response success and error codes</span></span>

<span data-ttu-id="72ac3-140">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="72ac3-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="72ac3-141">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="72ac3-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="72ac3-142">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="72ac3-142">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="72ac3-143">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="72ac3-143">Response example</span></span>

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
