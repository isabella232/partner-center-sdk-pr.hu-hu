---
title: Homokozó elvű előfizetés aktiválása kereskedelmi piactér-termékekhez
description: Ismerje meg, hogyan használható a C/# és a partner Center REST API-k a kereskedelmi Piactéri termékekhez készült homokozó-előfizetés aktiválásához.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a78b2c84368b29f1378f46971c4814929094e299
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768508"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a><span data-ttu-id="3d9d4-103">Homokozó-előfizetés aktiválása kereskedelmi Piactéri SaaS-termékekhez a számlázás engedélyezéséhez</span><span class="sxs-lookup"><span data-stu-id="3d9d4-103">Activate a sandbox subscription for commercial marketplace SaaS products to enable billing</span></span>

<span data-ttu-id="3d9d4-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="3d9d4-104">**Applies to:**</span></span>

- <span data-ttu-id="3d9d4-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="3d9d4-105">Partner Center</span></span>

<span data-ttu-id="3d9d4-106">Az előfizetések aktiválása a kereskedelmi piactéren szolgáltatott szoftverként (SaaS) származó termékekhez az integrációs sandbox-fiókoktól a számlázás engedélyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-106">How to activate a subscription for commercial marketplace Software as a Service (SaaS) products from integration sandbox accounts to enable billing.</span></span>

> [!NOTE]
> <span data-ttu-id="3d9d4-107">Csak a kereskedelmi piactéren elérhető SaaS-termékek előfizetését lehet aktiválni az integrációs homokozó fiókjaiból.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-107">It's only possible to activate a subscription for commercial marketplace SaaS products from integration sandbox accounts.</span></span> <span data-ttu-id="3d9d4-108">Ha éles előfizetéssel rendelkezik, a telepítési folyamat befejezéséhez fel kell keresnie a közzétevő helyét.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-108">If you have a production subscription, you must visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="3d9d4-109">Az előfizetés számlázása csak a telepítés befejeződése után kezdődik.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-109">Subscription billing will begin only after setup is complete.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d9d4-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="3d9d4-110">Prerequisites</span></span>

- <span data-ttu-id="3d9d4-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3d9d4-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3d9d4-113">Egy, a kereskedelmi piactér SaaS-termékekhez aktív előfizetéssel rendelkező ügyfél-integrációs munkapéldány-partneri fiók.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-113">An integration sandbox partner account with a customer having an active subscription for commercial marketplace SaaS products.</span></span>

- <span data-ttu-id="3d9d4-114">A partner Center .NET SDK-t használó partnereink számára a funkció eléréséhez az SDK 1.14.0 vagy újabb verzióját kell használnia.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-114">For partners using Partner Center .NET SDK, you must use SDK version 1.14.0 or higher to access this capability.</span></span>

## <a name="c"></a><span data-ttu-id="3d9d4-115">C\#</span><span class="sxs-lookup"><span data-stu-id="3d9d4-115">C\#</span></span>

<span data-ttu-id="3d9d4-116">Az alábbi lépéseket követve aktiválhatja az előfizetést a kereskedelmi Marketplace SaaS-termékekhez:</span><span class="sxs-lookup"><span data-stu-id="3d9d4-116">Use the following steps to activate a subscription for commercial marketplace SaaS products:</span></span>

1. <span data-ttu-id="3d9d4-117">Hozzon végre egy felületet az elérhető előfizetési műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-117">Make an interface to the subscription operations available.</span></span> <span data-ttu-id="3d9d4-118">Azonosítania kell az ügyfelet, és meg kell adnia a próbaverziós előfizetés előfizetés-azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-118">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. <span data-ttu-id="3d9d4-119">Aktiválja az előfizetést az **aktiválási** művelettel.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-119">Activate the subscription using the **Activate** operation.</span></span>

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a><span data-ttu-id="3d9d4-120">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="3d9d4-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3d9d4-121">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="3d9d4-121">Request syntax</span></span>

| <span data-ttu-id="3d9d4-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="3d9d4-122">Method</span></span>     | <span data-ttu-id="3d9d4-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="3d9d4-123">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="3d9d4-124">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="3d9d4-124">**POST**</span></span> | <span data-ttu-id="3d9d4-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/Activate http/1.1</span><span class="sxs-lookup"><span data-stu-id="3d9d4-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="3d9d4-126">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="3d9d4-126">URI parameter</span></span>

| <span data-ttu-id="3d9d4-127">Név</span><span class="sxs-lookup"><span data-stu-id="3d9d4-127">Name</span></span>                   | <span data-ttu-id="3d9d4-128">Típus</span><span class="sxs-lookup"><span data-stu-id="3d9d4-128">Type</span></span>     | <span data-ttu-id="3d9d4-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="3d9d4-129">Required</span></span> | <span data-ttu-id="3d9d4-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="3d9d4-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3d9d4-131">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="3d9d4-131">**customer-tenant-id**</span></span> | <span data-ttu-id="3d9d4-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="3d9d4-132">**guid**</span></span> | <span data-ttu-id="3d9d4-133">Y</span><span class="sxs-lookup"><span data-stu-id="3d9d4-133">Y</span></span> | <span data-ttu-id="3d9d4-134">Az érték egy GUID formátumú ügyfél-bérlői azonosító (**ügyfél-bérlő-azonosító**), amely lehetővé teszi az ügyfél megadását.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-134">The value is a GUID-formatted customer tenant identifier (**customer-tenant-id**), which allows you to specify a customer.</span></span> |
| <span data-ttu-id="3d9d4-135">**előfizetés-azonosító**</span><span class="sxs-lookup"><span data-stu-id="3d9d4-135">**subscription-id**</span></span> | <span data-ttu-id="3d9d4-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="3d9d4-136">**guid**</span></span> | <span data-ttu-id="3d9d4-137">Y</span><span class="sxs-lookup"><span data-stu-id="3d9d4-137">Y</span></span> | <span data-ttu-id="3d9d4-138">Az érték egy GUID-formátumú előfizetés-azonosító (**előfizetés-azonosító**), amely lehetővé teszi az előfizetés megadását.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-138">The value is a GUID-formatted subscription identifier (**subscription-id**), which allows you to specify a subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3d9d4-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="3d9d4-139">Request headers</span></span>

<span data-ttu-id="3d9d4-140">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3d9d4-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3d9d4-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="3d9d4-141">Request body</span></span>

<span data-ttu-id="3d9d4-142">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3d9d4-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="3d9d4-143">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a><span data-ttu-id="3d9d4-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="3d9d4-144">REST response</span></span>

<span data-ttu-id="3d9d4-145">Ez a metódus az **előfizetés-azonosító** és az **állapot** tulajdonságokat adja vissza.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-145">This method returns the **subscription-id** and **status** properties.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3d9d4-146">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="3d9d4-146">Response success and error codes</span></span>

<span data-ttu-id="3d9d4-147">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3d9d4-148">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3d9d4-149">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="3d9d4-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3d9d4-150">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="3d9d4-150">Response example</span></span>

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
