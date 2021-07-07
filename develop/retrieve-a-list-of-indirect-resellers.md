---
title: Közvetett viszonteladók listájának lekérése
description: A bejelentkezett partner közvetett viszonteladói listájának lekérése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 58f5c3378b5b941fdc9dafcf28f5efbc58c29c7c
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446564"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a><span data-ttu-id="8b8a9-103">Közvetett viszonteladók listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="8b8a9-103">Retrieve a list of indirect resellers</span></span>

<span data-ttu-id="8b8a9-104">A bejelentkezett partner közvetett viszonteladói listájának lekérése.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-104">How to retrieve a list of the signed-in partner's indirect resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b8a9-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8b8a9-105">Prerequisites</span></span>

- <span data-ttu-id="8b8a9-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8b8a9-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8b8a9-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-107">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="8b8a9-108">C\#</span><span class="sxs-lookup"><span data-stu-id="8b8a9-108">C\#</span></span>

<span data-ttu-id="8b8a9-109">Azon közvetett viszonteladók listájának lekéréséhez, akikkel a bejelentkezett partner kapcsolatban áll, először szerezze be a [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) tulajdonságból a kapcsolatgyűjtési műveletek felületét.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-109">To retrieve a list of indirect resellers with whom the signed-in partner has a relationship, first get an interface to relationship collection operations from the [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property.</span></span> <span data-ttu-id="8b8a9-110">Ezután hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) vagy [**Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) metódust, és adja át a [**PartnerRelationshipType enumerálás**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) egyik tagját a kapcsolattípus azonosításához.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-110">Then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) method, passing a member of the [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) enumeration to identify the relationship type.</span></span> <span data-ttu-id="8b8a9-111">A közvetett viszonteladók lekérése az IsIndirectCloudSolutionProviderOf parancs használatával oldható meg.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-111">To retrieve indirect resellers, you must use IsIndirectCloudSolutionProviderOf.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

<span data-ttu-id="8b8a9-112">**Minta:** [Konzoltesztelő](console-test-app.md)**alkalmazás Project:** Partnerközpont SDK Samples **Class:** GetIndirectResellers.cs</span><span class="sxs-lookup"><span data-stu-id="8b8a9-112">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8b8a9-113">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="8b8a9-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8b8a9-114">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="8b8a9-114">Request syntax</span></span>

| <span data-ttu-id="8b8a9-115">Metódus</span><span class="sxs-lookup"><span data-stu-id="8b8a9-115">Method</span></span>  | <span data-ttu-id="8b8a9-116">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="8b8a9-116">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8b8a9-117">**Kap**</span><span class="sxs-lookup"><span data-stu-id="8b8a9-117">**GET**</span></span> | <span data-ttu-id="8b8a9-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship \_ type=IsIndirectCloudSolutionProviderOf HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8b8a9-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship\_type=IsIndirectCloudSolutionProviderOf HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="8b8a9-119">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="8b8a9-119">URI parameter</span></span>

<span data-ttu-id="8b8a9-120">A kapcsolattípus azonosításához használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-120">Use the following query parameter to identify the relationship type.</span></span>

| <span data-ttu-id="8b8a9-121">Név</span><span class="sxs-lookup"><span data-stu-id="8b8a9-121">Name</span></span>               | <span data-ttu-id="8b8a9-122">Típus</span><span class="sxs-lookup"><span data-stu-id="8b8a9-122">Type</span></span>    | <span data-ttu-id="8b8a9-123">Kötelező</span><span class="sxs-lookup"><span data-stu-id="8b8a9-123">Required</span></span>  | <span data-ttu-id="8b8a9-124">Leírás</span><span class="sxs-lookup"><span data-stu-id="8b8a9-124">Description</span></span>                         |
|--------------------|---------|-----------|-------------------------------------|
| <span data-ttu-id="8b8a9-125">relationship_type</span><span class="sxs-lookup"><span data-stu-id="8b8a9-125">relationship_type</span></span>  | <span data-ttu-id="8b8a9-126">sztring</span><span class="sxs-lookup"><span data-stu-id="8b8a9-126">string</span></span>  | <span data-ttu-id="8b8a9-127">Igen</span><span class="sxs-lookup"><span data-stu-id="8b8a9-127">Yes</span></span>       | <span data-ttu-id="8b8a9-128">Az érték a [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype)típusban található egyik tagnév sztringes ábrázolása.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-128">The value is the string representation of one of the member names found in [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span></span><br/><br/> <span data-ttu-id="8b8a9-129">Ha a partner szolgáltatóként van bejelentkezve, és le szeretné kapni azon közvetett viszonteladók listáját, akikkel kapcsolatot létrehoztak, használja az IsIndirectCloudSolutionProviderOf használhatja.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-129">If the partner is signed in as a provider and you want to get a list of the indirect resellers with whom they have established a relationship, use IsIndirectCloudSolutionProviderOf.</span></span><br/><br/> <span data-ttu-id="8b8a9-130">Ha a partner viszonteladóként van bejelentkezve, és le szeretné kapni azon közvetett szolgáltatók listáját, akikkel kapcsolatot létrehozott, használja az IsIndirectResellerOf használhatja.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-130">If the partner is signed in as a reseller and you want to get a list of the indirect providers with whom they have established a relationship, use IsIndirectResellerOf.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="8b8a9-131">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="8b8a9-131">Request headers</span></span>

<span data-ttu-id="8b8a9-132">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8b8a9-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8b8a9-133">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="8b8a9-133">Request body</span></span>

<span data-ttu-id="8b8a9-134">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8b8a9-135">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8b8a9-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="8b8a9-136">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="8b8a9-136">REST response</span></span>

<span data-ttu-id="8b8a9-137">Ha a válasz törzse sikeres, a [partnerreláció](relationships-resources.md) erőforrásainak gyűjteményét tartalmazza a viszonteladók azonosításához.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-137">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8b8a9-138">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="8b8a9-138">Response success and error codes</span></span>

<span data-ttu-id="8b8a9-139">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8b8a9-140">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="8b8a9-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8b8a9-141">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8b8a9-141">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8b8a9-142">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8b8a9-142">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 298
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CV: b21Ll1miM0yFMPQQ.0
MS-ServerId: 030020643
Date: Wed, 05 Apr 2017 21:08:44 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847383",
            "location": "US",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }, {
            "id": "b01b1487-b36e-4e6d-9b5e-0b58974c4b28",
            "name": "ReleCloud",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847433",
            "location": "BR",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```