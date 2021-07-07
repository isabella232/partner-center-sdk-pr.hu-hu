---
title: Kapcsolatkérés URL-címének lekérése
description: Kapcsolatkérési URL-cím lekérése, hogy elküldhető legyen egy ügyfélnek.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 07804b36dfe0892cf8b531e0731188260c014f49
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547450"
---
# <a name="retrieve-a-relationship-request-url"></a><span data-ttu-id="2b83e-103">Kapcsolatkérés URL-címének lekérése</span><span class="sxs-lookup"><span data-stu-id="2b83e-103">Retrieve a relationship request URL</span></span>

<span data-ttu-id="2b83e-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="2b83e-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="2b83e-105">Kapcsolatkérési URL-cím lekérése, hogy elküldhető legyen egy ügyfélnek.</span><span class="sxs-lookup"><span data-stu-id="2b83e-105">How to retrieve a relationship request URL to send to a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b83e-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2b83e-106">Prerequisites</span></span>

- <span data-ttu-id="2b83e-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2b83e-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2b83e-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="2b83e-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="2b83e-109">C\#</span><span class="sxs-lookup"><span data-stu-id="2b83e-109">C\#</span></span>

<span data-ttu-id="2b83e-110">Kapcsolatkérés URL-címének lekéréséhez először használja az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) adatokat a partner ügyfélműveletei felületének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="2b83e-110">To retrieve a relationship request URL, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="2b83e-111">Ezután a [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) tulajdonság használatával lekért felület az ügyfélkapcsolati kérések műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="2b83e-111">Next, use the [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) property to get an interface to customer relationship request operations.</span></span> <span data-ttu-id="2b83e-112">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) vagy [**GetAsync metódust**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) az URL-cím lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="2b83e-112">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) method to retrieve the URL.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

<span data-ttu-id="2b83e-113">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="2b83e-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2b83e-114">**Project**: Partnerközpont SDK **Osztály:** GetCustomerRelationshipRequest.cs</span><span class="sxs-lookup"><span data-stu-id="2b83e-114">**Project**: Partner Center SDK Samples **Class**: GetCustomerRelationshipRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2b83e-115">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="2b83e-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2b83e-116">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="2b83e-116">Request syntax</span></span>

| <span data-ttu-id="2b83e-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="2b83e-117">Method</span></span>  | <span data-ttu-id="2b83e-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2b83e-118">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="2b83e-119">**Kap**</span><span class="sxs-lookup"><span data-stu-id="2b83e-119">**GET**</span></span> | <span data-ttu-id="2b83e-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2b83e-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2b83e-121">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2b83e-121">Request headers</span></span>

<span data-ttu-id="2b83e-122">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2b83e-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2b83e-123">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2b83e-123">Request body</span></span>

<span data-ttu-id="2b83e-124">None</span><span class="sxs-lookup"><span data-stu-id="2b83e-124">None</span></span>

### <a name="request-example"></a><span data-ttu-id="2b83e-125">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="2b83e-125">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2b83e-126">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2b83e-126">REST response</span></span>

<span data-ttu-id="2b83e-127">Ha sikeres, a válasz tartalmazza a [RelationshipRequest objektumot.](relationships-resources.md#relationshiprequest)</span><span class="sxs-lookup"><span data-stu-id="2b83e-127">If successful, the response contains the [RelationshipRequest](relationships-resources.md#relationshiprequest) object.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2b83e-128">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2b83e-128">Response success and error codes</span></span>

<span data-ttu-id="2b83e-129">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="2b83e-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2b83e-130">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="2b83e-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2b83e-131">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2b83e-131">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2b83e-132">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2b83e-132">Response example</span></span>

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
