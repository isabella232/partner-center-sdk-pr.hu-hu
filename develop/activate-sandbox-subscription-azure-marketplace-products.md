---
title: Sandbox-előfizetés aktiválása kereskedelmi piactéri termékekhez
description: Megtudhatja, hogyan használhatja a C/# és a Partnerközpont REST API-kat a kereskedelmi piactéri termékekre vonatkozó sandbox-előfizetések aktiválásához.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b32c3e87462f58218771fc5da7da56ed177489cb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025700"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a><span data-ttu-id="e927c-103">Sandbox-előfizetés aktiválása kereskedelmi piactéri SaaS-termékekhez a számlázás engedélyezéséhez</span><span class="sxs-lookup"><span data-stu-id="e927c-103">Activate a sandbox subscription for commercial marketplace SaaS products to enable billing</span></span>

<span data-ttu-id="e927c-104">Előfizetés aktiválása kereskedelmi piactéri szolgáltatott szoftver (SaaS) termékekhez integrációs sandbox-fiókokból a számlázás engedélyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="e927c-104">How to activate a subscription for commercial marketplace Software as a Service (SaaS) products from integration sandbox accounts to enable billing.</span></span>

> [!NOTE]
> <span data-ttu-id="e927c-105">A kereskedelmi piactéri SaaS-termékek előfizetését csak integrációs sandbox-fiókokból lehet aktiválni.</span><span class="sxs-lookup"><span data-stu-id="e927c-105">It's only possible to activate a subscription for commercial marketplace SaaS products from integration sandbox accounts.</span></span> <span data-ttu-id="e927c-106">Ha éles üzemre vonatkozó előfizetéssel rendelkezik, a telepítési folyamat befejezéséhez meg kell látogatnia a közzétevő webhelyét.</span><span class="sxs-lookup"><span data-stu-id="e927c-106">If you have a production subscription, you must visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="e927c-107">Az előfizetés számlázása csak a beállítás befejezése után kezdődik meg.</span><span class="sxs-lookup"><span data-stu-id="e927c-107">Subscription billing will begin only after setup is complete.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e927c-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="e927c-108">Prerequisites</span></span>

- <span data-ttu-id="e927c-109">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e927c-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e927c-110">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="e927c-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e927c-111">Integrációs sandbox partnerfiók egy olyan ügyféllel, aki aktív előfizetéssel rendelkezik a kereskedelmi piactéri SaaS-termékekhez.</span><span class="sxs-lookup"><span data-stu-id="e927c-111">An integration sandbox partner account with a customer having an active subscription for commercial marketplace SaaS products.</span></span>

- <span data-ttu-id="e927c-112">A .NET SDK Partnerközpont t használó partnereknek az SDK 1.14.0-s vagy újabb verzióját kell használniuk a funkció eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="e927c-112">For partners using Partner Center .NET SDK, you must use SDK version 1.14.0 or higher to access this capability.</span></span>

## <a name="c"></a><span data-ttu-id="e927c-113">C\#</span><span class="sxs-lookup"><span data-stu-id="e927c-113">C\#</span></span>

<span data-ttu-id="e927c-114">A kereskedelmi piactéri SaaS-termékek előfizetésének aktiválásához kövesse az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="e927c-114">Use the following steps to activate a subscription for commercial marketplace SaaS products:</span></span>

1. <span data-ttu-id="e927c-115">Tegye elérhetővé az előfizetési műveletek felületét.</span><span class="sxs-lookup"><span data-stu-id="e927c-115">Make an interface to the subscription operations available.</span></span> <span data-ttu-id="e927c-116">Azonosítania kell az ügyfelet, és meg kell adnia a próba-előfizetés előfizetés-azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="e927c-116">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. <span data-ttu-id="e927c-117">Aktiválja az előfizetést az **Aktiválás művelettel.**</span><span class="sxs-lookup"><span data-stu-id="e927c-117">Activate the subscription using the **Activate** operation.</span></span>

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a><span data-ttu-id="e927c-118">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="e927c-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e927c-119">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="e927c-119">Request syntax</span></span>

| <span data-ttu-id="e927c-120">Metódus</span><span class="sxs-lookup"><span data-stu-id="e927c-120">Method</span></span>     | <span data-ttu-id="e927c-121">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="e927c-121">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="e927c-122">**Post**</span><span class="sxs-lookup"><span data-stu-id="e927c-122">**POST**</span></span> | <span data-ttu-id="e927c-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/activate HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e927c-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e927c-124">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="e927c-124">URI parameter</span></span>

| <span data-ttu-id="e927c-125">Név</span><span class="sxs-lookup"><span data-stu-id="e927c-125">Name</span></span>                   | <span data-ttu-id="e927c-126">Típus</span><span class="sxs-lookup"><span data-stu-id="e927c-126">Type</span></span>     | <span data-ttu-id="e927c-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e927c-127">Required</span></span> | <span data-ttu-id="e927c-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="e927c-128">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e927c-129">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="e927c-129">**customer-tenant-id**</span></span> | <span data-ttu-id="e927c-130">**guid**</span><span class="sxs-lookup"><span data-stu-id="e927c-130">**guid**</span></span> | <span data-ttu-id="e927c-131">Y</span><span class="sxs-lookup"><span data-stu-id="e927c-131">Y</span></span> | <span data-ttu-id="e927c-132">Az érték egy GUID-formátumú ügyfél bérlőazonosítója **(ügyfél-bérlő-azonosító),** amely lehetővé teszi az ügyfél megadását.</span><span class="sxs-lookup"><span data-stu-id="e927c-132">The value is a GUID-formatted customer tenant identifier (**customer-tenant-id**), which allows you to specify a customer.</span></span> |
| <span data-ttu-id="e927c-133">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="e927c-133">**subscription-id**</span></span> | <span data-ttu-id="e927c-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="e927c-134">**guid**</span></span> | <span data-ttu-id="e927c-135">Y</span><span class="sxs-lookup"><span data-stu-id="e927c-135">Y</span></span> | <span data-ttu-id="e927c-136">Az érték egy GUID-formátumú előfizetés-azonosító **(előfizetés-azonosító),** amely lehetővé teszi egy előfizetés megadását.</span><span class="sxs-lookup"><span data-stu-id="e927c-136">The value is a GUID-formatted subscription identifier (**subscription-id**), which allows you to specify a subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e927c-137">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="e927c-137">Request headers</span></span>

<span data-ttu-id="e927c-138">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e927c-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e927c-139">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="e927c-139">Request body</span></span>

<span data-ttu-id="e927c-140">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="e927c-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e927c-141">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="e927c-141">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a><span data-ttu-id="e927c-142">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="e927c-142">REST response</span></span>

<span data-ttu-id="e927c-143">Ez a metódus visszaadja **az előfizetés-azonosító és az** állapot **tulajdonságait.**</span><span class="sxs-lookup"><span data-stu-id="e927c-143">This method returns the **subscription-id** and **status** properties.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e927c-144">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="e927c-144">Response success and error codes</span></span>

<span data-ttu-id="e927c-145">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="e927c-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e927c-146">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="e927c-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e927c-147">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e927c-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e927c-148">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="e927c-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
