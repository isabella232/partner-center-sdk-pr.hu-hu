---
title: Kapcsolatkérés URL-címének lekérése
description: A kapcsolati kérelem URL-címének lekérése az ügyfélnek küldendő kapcsolati kéréshez.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5f899734b774ff460e005e20df8658275b2ce9d5
ms.sourcegitcommit: d4e652e3b73c6137704d43d4a472cc5aa5549f11
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/09/2020
ms.locfileid: "97768680"
---
# <a name="retrieve-a-relationship-request-url"></a><span data-ttu-id="373f6-103">Kapcsolatkérés URL-címének lekérése</span><span class="sxs-lookup"><span data-stu-id="373f6-103">Retrieve a relationship request URL</span></span>

<span data-ttu-id="373f6-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="373f6-104">**Applies To**</span></span>

- <span data-ttu-id="373f6-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="373f6-105">Partner Center</span></span>
- <span data-ttu-id="373f6-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="373f6-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="373f6-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="373f6-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="373f6-108">A kapcsolati kérelem URL-címének lekérése az ügyfélnek küldendő kapcsolati kéréshez.</span><span class="sxs-lookup"><span data-stu-id="373f6-108">How to retrieve a relationship request URL to send to a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="373f6-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="373f6-109">Prerequisites</span></span>

- <span data-ttu-id="373f6-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="373f6-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="373f6-111">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="373f6-111">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="373f6-112">C\#</span><span class="sxs-lookup"><span data-stu-id="373f6-112">C\#</span></span>

<span data-ttu-id="373f6-113">A kapcsolati kérelem URL-címének lekéréséhez először használja a [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) felületet a partner ügyfél-műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="373f6-113">To retrieve a relationship request URL, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="373f6-114">Ezután a [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) tulajdonsággal szerezzen be egy felületet az ügyfélkapcsolati kérelmek műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="373f6-114">Next, use the [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) property to get an interface to customer relationship request operations.</span></span> <span data-ttu-id="373f6-115">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) metódust az URL-cím lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="373f6-115">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) method to retrieve the URL.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

<span data-ttu-id="373f6-116">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="373f6-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="373f6-117">**Projekt**: partner Center SDK Samples **osztály**: GetCustomerRelationshipRequest.cs</span><span class="sxs-lookup"><span data-stu-id="373f6-117">**Project**: Partner Center SDK Samples **Class**: GetCustomerRelationshipRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="373f6-118">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="373f6-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="373f6-119">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="373f6-119">Request syntax</span></span>

| <span data-ttu-id="373f6-120">Metódus</span><span class="sxs-lookup"><span data-stu-id="373f6-120">Method</span></span>  | <span data-ttu-id="373f6-121">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="373f6-121">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="373f6-122">**GET**</span><span class="sxs-lookup"><span data-stu-id="373f6-122">**GET**</span></span> | <span data-ttu-id="373f6-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/relationshiprequests http/1.1</span><span class="sxs-lookup"><span data-stu-id="373f6-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="373f6-124">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="373f6-124">Request headers</span></span>

<span data-ttu-id="373f6-125">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="373f6-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="373f6-126">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="373f6-126">Request body</span></span>

<span data-ttu-id="373f6-127">Nincs</span><span class="sxs-lookup"><span data-stu-id="373f6-127">None</span></span>

### <a name="request-example"></a><span data-ttu-id="373f6-128">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="373f6-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/relationshiprequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="373f6-129">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="373f6-129">REST response</span></span>

<span data-ttu-id="373f6-130">Ha a művelet sikeres, a válasz tartalmazza a [RelationshipRequest](relationships-resources.md#relationshiprequest) objektumot.</span><span class="sxs-lookup"><span data-stu-id="373f6-130">If successful, the response contains the [RelationshipRequest](relationships-resources.md#relationshiprequest) object.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="373f6-131">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="373f6-131">Response success and error codes</span></span>

<span data-ttu-id="373f6-132">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="373f6-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="373f6-133">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="373f6-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="373f6-134">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="373f6-134">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="373f6-135">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="373f6-135">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 196
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CV: jbYZRWjU3E262f8o.0
MS-ServerId: 030020643
Date: Fri, 19 May 2017 22:32:07 GMT

{
    "url": "https://admin.microsoft.com/Adminportal/Home?invType=ResellerRelationship&partnerId=3b33e682-00c3-41ee-9dd2-a548adf56438&msppId=0&DAP=false#/BillingAccounts/partner-invitation",
    "attributes": {
        "objectType": "RelationshipRequest"
    }
}
```
