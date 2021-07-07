---
title: Konfigurációs szabályzat törlése a megadott ügyfélnél
description: Adott ügyfél és szabályzatazonosító konfigurációs szabályzatának törlése.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2d6a7d392bd6af6850eb7716528e6745943bb7bb
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973026"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="4fc51-103">Konfigurációs szabályzat törlése a megadott ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="4fc51-103">Delete a configuration policy for the specified customer</span></span>

<span data-ttu-id="4fc51-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="4fc51-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="4fc51-105">Adott ügyfél és szabályzatazonosító konfigurációs szabályzatának törlése.</span><span class="sxs-lookup"><span data-stu-id="4fc51-105">How to delete a configuration policy for a specified customer and policy identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fc51-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4fc51-106">Prerequisites</span></span>

- <span data-ttu-id="4fc51-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4fc51-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4fc51-108">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="4fc51-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4fc51-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4fc51-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4fc51-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="4fc51-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4fc51-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4fc51-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4fc51-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4fc51-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4fc51-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="4fc51-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4fc51-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4fc51-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4fc51-115">A szabályzat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="4fc51-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="4fc51-116">C\#</span><span class="sxs-lookup"><span data-stu-id="4fc51-116">C\#</span></span>

<span data-ttu-id="4fc51-117">Adott ügyfél konfigurációs szabályzatának törlése:</span><span class="sxs-lookup"><span data-stu-id="4fc51-117">To delete a configuration policy for a specified customer:</span></span>

1. <span data-ttu-id="4fc51-118">Hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával, hogy lekérje a műveletek interfészét a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="4fc51-118">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="4fc51-119">Hívja meg [**a ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) metódust a szabályzat azonosítójával, hogy lekérje a megadott szabályzat konfigurációs házirend-műveleteinek felületét.</span><span class="sxs-lookup"><span data-stu-id="4fc51-119">Call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span>

3. <span data-ttu-id="4fc51-120">A konfigurációs [**szabályzat törléséhez**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) hívja meg a [**Delete vagy a DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="4fc51-120">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) method to delete the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

<span data-ttu-id="4fc51-121">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="4fc51-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4fc51-122">**Project**: Partnerközpont SDK **Osztály:** DeleteConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="4fc51-122">**Project**: Partner Center SDK Samples **Class**: DeleteConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4fc51-123">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="4fc51-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4fc51-124">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="4fc51-124">Request syntax</span></span>

| <span data-ttu-id="4fc51-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="4fc51-125">Method</span></span>     | <span data-ttu-id="4fc51-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4fc51-126">Request URI</span></span>                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4fc51-127">**Töröl**</span><span class="sxs-lookup"><span data-stu-id="4fc51-127">**DELETE**</span></span> | <span data-ttu-id="4fc51-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/policies/{policy-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4fc51-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="4fc51-129">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="4fc51-129">URI parameters</span></span>

<span data-ttu-id="4fc51-130">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="4fc51-130">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="4fc51-131">Név</span><span class="sxs-lookup"><span data-stu-id="4fc51-131">Name</span></span>        | <span data-ttu-id="4fc51-132">Típus</span><span class="sxs-lookup"><span data-stu-id="4fc51-132">Type</span></span>   | <span data-ttu-id="4fc51-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="4fc51-133">Required</span></span> | <span data-ttu-id="4fc51-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="4fc51-134">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="4fc51-135">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="4fc51-135">customer-id</span></span> | <span data-ttu-id="4fc51-136">sztring</span><span class="sxs-lookup"><span data-stu-id="4fc51-136">string</span></span> | <span data-ttu-id="4fc51-137">Igen</span><span class="sxs-lookup"><span data-stu-id="4fc51-137">Yes</span></span>      | <span data-ttu-id="4fc51-138">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="4fc51-138">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="4fc51-139">policy-id</span><span class="sxs-lookup"><span data-stu-id="4fc51-139">policy-id</span></span>   | <span data-ttu-id="4fc51-140">sztring</span><span class="sxs-lookup"><span data-stu-id="4fc51-140">string</span></span> | <span data-ttu-id="4fc51-141">Igen</span><span class="sxs-lookup"><span data-stu-id="4fc51-141">Yes</span></span>      | <span data-ttu-id="4fc51-142">Egy GUID-formátumú sztring, amely azonosítja a törölni kívánt szabályzatot.</span><span class="sxs-lookup"><span data-stu-id="4fc51-142">A GUID-formatted string that identifies the policy to delete.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4fc51-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4fc51-143">Request headers</span></span>

<span data-ttu-id="4fc51-144">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4fc51-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4fc51-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="4fc51-145">Request body</span></span>

<span data-ttu-id="4fc51-146">None</span><span class="sxs-lookup"><span data-stu-id="4fc51-146">None</span></span>

### <a name="request-example"></a><span data-ttu-id="4fc51-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4fc51-147">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="4fc51-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4fc51-148">REST response</span></span>

<span data-ttu-id="4fc51-149">Ha a válasz sikeres, a 204 No Content (Nincs tartalom) állapotkódot adja vissza.</span><span class="sxs-lookup"><span data-stu-id="4fc51-149">If successful, the response returns a 204 No Content status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4fc51-150">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4fc51-150">Response success and error codes</span></span>

<span data-ttu-id="4fc51-151">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="4fc51-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4fc51-152">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="4fc51-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4fc51-153">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="4fc51-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4fc51-154">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4fc51-154">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
