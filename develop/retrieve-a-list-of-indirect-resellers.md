---
title: Közvetett viszonteladók listájának lekérése
description: A bejelentkezett partner közvetett viszonteladói listájának beolvasása.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e53237b97fa26d3a987f0ee7de491084b596af4a
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768399"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a><span data-ttu-id="52bc9-103">Közvetett viszonteladók listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="52bc9-103">Retrieve a list of indirect resellers</span></span>

<span data-ttu-id="52bc9-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="52bc9-104">**Applies To**</span></span>

- <span data-ttu-id="52bc9-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="52bc9-105">Partner Center</span></span>

<span data-ttu-id="52bc9-106">A bejelentkezett partner közvetett viszonteladói listájának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="52bc9-106">How to retrieve a list of the signed-in partner's indirect resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52bc9-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="52bc9-107">Prerequisites</span></span>

- <span data-ttu-id="52bc9-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="52bc9-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="52bc9-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="52bc9-109">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="52bc9-110">C\#</span><span class="sxs-lookup"><span data-stu-id="52bc9-110">C\#</span></span>

<span data-ttu-id="52bc9-111">Azon közvetett viszonteladók listájának lekéréséhez, akikkel a bejelentkezett partnernek van kapcsolata, először szerezzen be egy felületet a kapcsolat gyűjtési műveleteihez a [**partnerOperations. kapcsolatok**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="52bc9-111">To retrieve a list of indirect resellers with whom the signed-in partner has a relationship, first get an interface to relationship collection operations from the [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property.</span></span> <span data-ttu-id="52bc9-112">Ezután hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) vagy a [**Get \_ aszinkron**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) metódust, amely a [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) enumerálás egy tagját továbbítja a kapcsolat típusának azonosításához.</span><span class="sxs-lookup"><span data-stu-id="52bc9-112">Then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) method, passing a member of the [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) enumeration to identify the relationship type.</span></span> <span data-ttu-id="52bc9-113">A közvetett viszonteladók beolvasásához a IsIndirectCloudSolutionProviderOf-t kell használnia.</span><span class="sxs-lookup"><span data-stu-id="52bc9-113">To retrieve indirect resellers, you must use IsIndirectCloudSolutionProviderOf.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

<span data-ttu-id="52bc9-114">**Minta**: [Console test app](console-test-app.md)**Project**: a partner Center SDK Samples **osztálya**: GetIndirectResellers.cs</span><span class="sxs-lookup"><span data-stu-id="52bc9-114">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="52bc9-115">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="52bc9-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="52bc9-116">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="52bc9-116">Request syntax</span></span>

| <span data-ttu-id="52bc9-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="52bc9-117">Method</span></span>  | <span data-ttu-id="52bc9-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="52bc9-118">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="52bc9-119">**GET**</span><span class="sxs-lookup"><span data-stu-id="52bc9-119">**GET**</span></span> | <span data-ttu-id="52bc9-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/Relationships? kapcsolat \_ típusa = IsIndirectCloudSolutionProviderOf http/1.1</span><span class="sxs-lookup"><span data-stu-id="52bc9-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship\_type=IsIndirectCloudSolutionProviderOf HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="52bc9-121">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="52bc9-121">URI parameter</span></span>

<span data-ttu-id="52bc9-122">A kapcsolat típusának azonosításához használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="52bc9-122">Use the following query parameter to identify the relationship type.</span></span>

| <span data-ttu-id="52bc9-123">Név</span><span class="sxs-lookup"><span data-stu-id="52bc9-123">Name</span></span>               | <span data-ttu-id="52bc9-124">Típus</span><span class="sxs-lookup"><span data-stu-id="52bc9-124">Type</span></span>    | <span data-ttu-id="52bc9-125">Kötelező</span><span class="sxs-lookup"><span data-stu-id="52bc9-125">Required</span></span>  | <span data-ttu-id="52bc9-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="52bc9-126">Description</span></span>                         |
|--------------------|---------|-----------|-------------------------------------|
| <span data-ttu-id="52bc9-127">relationship_type</span><span class="sxs-lookup"><span data-stu-id="52bc9-127">relationship_type</span></span>  | <span data-ttu-id="52bc9-128">sztring</span><span class="sxs-lookup"><span data-stu-id="52bc9-128">string</span></span>  | <span data-ttu-id="52bc9-129">Igen</span><span class="sxs-lookup"><span data-stu-id="52bc9-129">Yes</span></span>       | <span data-ttu-id="52bc9-130">Az érték a [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype)található egyik tag nevének karakterláncos ábrázolása.</span><span class="sxs-lookup"><span data-stu-id="52bc9-130">The value is the string representation of one of the member names found in [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span></span><br/><br/> <span data-ttu-id="52bc9-131">Ha a partner be van jelentkezve szolgáltatóként, és szeretné lekérni azon közvetett viszonteladók listáját, akikkel kapcsolatot létesítettek, használja a IsIndirectCloudSolutionProviderOf.</span><span class="sxs-lookup"><span data-stu-id="52bc9-131">If the partner is signed in as a provider and you want to get a list of the indirect resellers with whom they have established a relationship, use IsIndirectCloudSolutionProviderOf.</span></span><br/><br/> <span data-ttu-id="52bc9-132">Ha a partnert viszonteladóként jelentkezett be, és szeretné lekérni azon közvetett szolgáltatók listáját, akikkel kapcsolatot létesítettek, használja a IsIndirectResellerOf-t.</span><span class="sxs-lookup"><span data-stu-id="52bc9-132">If the partner is signed in as a reseller and you want to get a list of the indirect providers with whom they have established a relationship, use IsIndirectResellerOf.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="52bc9-133">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="52bc9-133">Request headers</span></span>

<span data-ttu-id="52bc9-134">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="52bc9-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="52bc9-135">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="52bc9-135">Request body</span></span>

<span data-ttu-id="52bc9-136">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="52bc9-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="52bc9-137">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="52bc9-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="52bc9-138">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="52bc9-138">REST response</span></span>

<span data-ttu-id="52bc9-139">Ha ez sikeres, a válasz törzse [PartnerRelationship](relationships-resources.md) -erőforrások gyűjteményét tartalmazza a viszonteladók azonosításához.</span><span class="sxs-lookup"><span data-stu-id="52bc9-139">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="52bc9-140">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="52bc9-140">Response success and error codes</span></span>

<span data-ttu-id="52bc9-141">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="52bc9-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="52bc9-142">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="52bc9-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="52bc9-143">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="52bc9-143">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="52bc9-144">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="52bc9-144">Response example</span></span>

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