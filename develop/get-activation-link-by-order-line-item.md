---
title: Aktiválási hivatkozás lekérése megrendelési sorelem alapján
description: Lekért egy előfizetés-aktiválási hivatkozást rendeléssorelem alapján.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: aa02a5a5b4a281b96e32ee6d239cc440cf8af4ec
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760776"
---
# <a name="get-activation-link-by-order-line-item"></a><span data-ttu-id="030ea-103">Aktiválási hivatkozás lekérése megrendelési sorelem alapján</span><span class="sxs-lookup"><span data-stu-id="030ea-103">Get activation link by order line item</span></span>

<span data-ttu-id="030ea-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="030ea-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="030ea-105">Lekért egy kereskedelmi piactéri előfizetés aktiválási hivatkozását a rendelési sor tételszáma alapján.</span><span class="sxs-lookup"><span data-stu-id="030ea-105">Gets a commercial marketplace subscription activation link by the order line item number.</span></span>

<span data-ttu-id="030ea-106">Az Partnerközpont-irányítópulton ezt a műveletet úgy használhatja, hogy  kiválaszt egy adott előfizetést **az** Előfizetés alatt a főoldalon, vagy az  Előfizetések lapon az aktiválni kívánt előfizetés melletti Ugrás az **Publisher** webhelyre hivatkozást.</span><span class="sxs-lookup"><span data-stu-id="030ea-106">In the Partner Center dashboard, you can do this operation by selecting either a **Specific Subscription** under **Subscription** on the main page, or selecting the **Go to Publisher's site** link next to the subscription to activate on the **Subscriptions** page.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="030ea-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="030ea-107">Prerequisites</span></span>

- <span data-ttu-id="030ea-108">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="030ea-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="030ea-109">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="030ea-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="030ea-110">Kész rendelés az aktiválni szükséges termékkel.</span><span class="sxs-lookup"><span data-stu-id="030ea-110">Completed order with product that needs activation.</span></span>

## <a name="c"></a><span data-ttu-id="030ea-111">C\#</span><span class="sxs-lookup"><span data-stu-id="030ea-111">C\#</span></span>

<span data-ttu-id="030ea-112">Egy sorelem aktiválási hivatkozásának lehívásához használja az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a kiválasztott ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="030ea-112">To get a line item's activation link, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span> <span data-ttu-id="030ea-113">Ezután hívja meg [**az Orders tulajdonságot**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) és a [**ById() metódust**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) a megadott [**OrderId értékével.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id)</span><span class="sxs-lookup"><span data-stu-id="030ea-113">Then call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the [**ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method with your specified  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span></span> <span data-ttu-id="030ea-114">Ezután hívja meg a [**LineItems metódust**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) **a ById() metódussal** és a sortételszám azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="030ea-114">Then, call the [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById()** method with the line item number identifier.</span></span>  <span data-ttu-id="030ea-115">Végül hívja meg az **ActivationLinks() metódust.**</span><span class="sxs-lookup"><span data-stu-id="030ea-115">Finally, call the **ActivationLinks()** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a><span data-ttu-id="030ea-116">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="030ea-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="030ea-117">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="030ea-117">Request syntax</span></span>

| <span data-ttu-id="030ea-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="030ea-118">Method</span></span>  | <span data-ttu-id="030ea-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="030ea-119">Request URI</span></span>                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="030ea-120">**Kap**</span><span class="sxs-lookup"><span data-stu-id="030ea-120">**GET**</span></span> | <span data-ttu-id="030ea-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="030ea-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="030ea-122">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="030ea-122">Request headers</span></span>

<span data-ttu-id="030ea-123">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="030ea-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="030ea-124">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="030ea-124">Request body</span></span>

<span data-ttu-id="030ea-125">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="030ea-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="030ea-126">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="030ea-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="030ea-127">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="030ea-127">REST response</span></span>

<span data-ttu-id="030ea-128">Ha a művelet sikeres, ez a metódus ügyfélerőforrások [gyűjteményét](customer-resources.md#customer) adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="030ea-128">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="030ea-129">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="030ea-129">Response success and error codes</span></span>

<span data-ttu-id="030ea-130">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="030ea-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="030ea-131">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="030ea-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="030ea-132">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="030ea-132">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="030ea-133">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="030ea-133">Response example</span></span>

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
