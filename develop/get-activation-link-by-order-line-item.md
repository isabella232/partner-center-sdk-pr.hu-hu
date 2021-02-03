---
title: Aktiválási hivatkozás lekérése megrendelési sorelem alapján
description: Lekérdezi az előfizetés aktiválási hivatkozását Order Line elem alapján.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c0e84888870571cf6bd21306f527863f2aa7ee85
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768052"
---
# <a name="get-activation-link-by-order-line-item"></a><span data-ttu-id="dbfa6-103">Aktiválási hivatkozás lekérése megrendelési sorelem alapján</span><span class="sxs-lookup"><span data-stu-id="dbfa6-103">Get activation link by order line item</span></span>

<span data-ttu-id="dbfa6-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="dbfa6-104">**Applies To**</span></span>

- <span data-ttu-id="dbfa6-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="dbfa6-105">Partner Center</span></span>
- <span data-ttu-id="dbfa6-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="dbfa6-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="dbfa6-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="dbfa6-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="dbfa6-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="dbfa6-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="dbfa6-109">A kereskedelmi piactér-előfizetés aktiválási hivatkozásának beolvasása a sorszám alapján.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-109">Gets a commercial marketplace subscription activation link by the order line item number.</span></span>

<span data-ttu-id="dbfa6-110">A partner Center irányítópultján ehhez a művelethez válasszon ki egy **adott előfizetést** a főoldalon, vagy válassza az **előfizetés elem** melletti **Ugrás a közzétevőhöz webhelyre** hivatkozást az **előfizetések** lapon az aktiváláshoz.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-110">In the Partner Center dashboard, you can do this operation by selecting either a **Specific Subscription** under **Subscription** on the main page, or selecting the **Go to Publisher's site** link next to the subscription to activate on the **Subscriptions** page.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbfa6-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="dbfa6-111">Prerequisites</span></span>

- <span data-ttu-id="dbfa6-112">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dbfa6-113">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="dbfa6-114">Befejeződött a megrendelés az aktiválást igénylő termékkel.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-114">Completed order with product that needs activation.</span></span>

## <a name="c"></a><span data-ttu-id="dbfa6-115">C\#</span><span class="sxs-lookup"><span data-stu-id="dbfa6-115">C\#</span></span>

<span data-ttu-id="dbfa6-116">Egy sor aktiválási hivatkozásának beszerzéséhez használja a [**IAggregatePartner. Customs**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a kiválasztott ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-116">To get a line item's activation link, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span> <span data-ttu-id="dbfa6-117">Ezután hívja meg a [**megrendelések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) tulajdonságot és a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) metódust a megadott  [**Rendeléskód**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id)értékkel.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-117">Then call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the [**ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method with your specified  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span></span> <span data-ttu-id="dbfa6-118">Ezt követően hívja meg a [**listaelemek**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) a **ById ()** metódussal a sor cikkszám-azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-118">Then, call the [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById()** method with the line item number identifier.</span></span>  <span data-ttu-id="dbfa6-119">Végül hívja meg a **ActivationLinks ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-119">Finally, call the **ActivationLinks()** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a><span data-ttu-id="dbfa6-120">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="dbfa6-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dbfa6-121">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="dbfa6-121">Request syntax</span></span>

| <span data-ttu-id="dbfa6-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="dbfa6-122">Method</span></span>  | <span data-ttu-id="dbfa6-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="dbfa6-123">Request URI</span></span>                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dbfa6-124">**GET**</span><span class="sxs-lookup"><span data-stu-id="dbfa6-124">**GET**</span></span> | <span data-ttu-id="dbfa6-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customerId}/Orders/{orderId}/lineitems/{lineItemNumber}/activationlinks http/1.1</span><span class="sxs-lookup"><span data-stu-id="dbfa6-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="dbfa6-126">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="dbfa6-126">Request headers</span></span>

<span data-ttu-id="dbfa6-127">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="dbfa6-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dbfa6-128">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="dbfa6-128">Request body</span></span>

<span data-ttu-id="dbfa6-129">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-129">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="dbfa6-130">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="dbfa6-130">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="dbfa6-131">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="dbfa6-131">REST response</span></span>

<span data-ttu-id="dbfa6-132">Ha ez sikeres, ez a metódus a válasz törzsében lévő [ügyfél](customer-resources.md#customer) -erőforrások gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-132">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dbfa6-133">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="dbfa6-133">Response success and error codes</span></span>

<span data-ttu-id="dbfa6-134">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dbfa6-135">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="dbfa6-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dbfa6-136">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dbfa6-136">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dbfa6-137">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="dbfa6-137">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 809
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT
{
  "totalCount": 1,
  "items": [
    {
      "lineItemNumber": 0,
      "link": {
        "uri": "<link populated here>",
        "method": "GET",
        "headers": [

        ]
      }
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```
