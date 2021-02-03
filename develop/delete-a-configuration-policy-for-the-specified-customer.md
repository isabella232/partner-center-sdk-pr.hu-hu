---
title: Konfigurációs szabályzat törlése a megadott ügyfélnél
description: Konfigurációs szabályzat törlése egy adott ügyfélre és házirend-azonosítóra vonatkozóan.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 586878367fc0873ef0fb1415799b2b7022954053
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768135"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="3575b-103">Konfigurációs szabályzat törlése a megadott ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="3575b-103">Delete a configuration policy for the specified customer</span></span>

<span data-ttu-id="3575b-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="3575b-104">**Applies to:**</span></span>

- <span data-ttu-id="3575b-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="3575b-105">Partner Center</span></span>
- <span data-ttu-id="3575b-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="3575b-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="3575b-107">Konfigurációs szabályzat törlése egy adott ügyfélre és házirend-azonosítóra vonatkozóan.</span><span class="sxs-lookup"><span data-stu-id="3575b-107">How to delete a configuration policy for a specified customer and policy identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3575b-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="3575b-108">Prerequisites</span></span>

- <span data-ttu-id="3575b-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="3575b-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3575b-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="3575b-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3575b-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3575b-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3575b-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="3575b-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3575b-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="3575b-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3575b-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="3575b-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3575b-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="3575b-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3575b-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3575b-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3575b-117">A házirend-azonosító.</span><span class="sxs-lookup"><span data-stu-id="3575b-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="3575b-118">C\#</span><span class="sxs-lookup"><span data-stu-id="3575b-118">C\#</span></span>

<span data-ttu-id="3575b-119">Egy adott ügyfélhez tartozó konfigurációs szabályzat törlése:</span><span class="sxs-lookup"><span data-stu-id="3575b-119">To delete a configuration policy for a specified customer:</span></span>

1. <span data-ttu-id="3575b-120">Hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérje le a felületet a műveletekre a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="3575b-120">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="3575b-121">Hívja meg a [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) metódust a házirend-azonosítóval, hogy lekérje az adott szabályzathoz tartozó konfigurációs házirend műveleteire vonatkozó felületet.</span><span class="sxs-lookup"><span data-stu-id="3575b-121">Call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span>

3. <span data-ttu-id="3575b-122">A konfigurációs szabályzat törléséhez hívja meg a [**delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) vagy a [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="3575b-122">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) method to delete the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

<span data-ttu-id="3575b-123">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3575b-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3575b-124">**Projekt**: partner Center SDK Samples **osztály**: DeleteConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="3575b-124">**Project**: Partner Center SDK Samples **Class**: DeleteConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="3575b-125">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="3575b-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3575b-126">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="3575b-126">Request syntax</span></span>

| <span data-ttu-id="3575b-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="3575b-127">Method</span></span>     | <span data-ttu-id="3575b-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="3575b-128">Request URI</span></span>                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3575b-129">**TÖRLÉSE**</span><span class="sxs-lookup"><span data-stu-id="3575b-129">**DELETE**</span></span> | <span data-ttu-id="3575b-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="3575b-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="3575b-131">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="3575b-131">URI parameters</span></span>

<span data-ttu-id="3575b-132">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="3575b-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="3575b-133">Név</span><span class="sxs-lookup"><span data-stu-id="3575b-133">Name</span></span>        | <span data-ttu-id="3575b-134">Típus</span><span class="sxs-lookup"><span data-stu-id="3575b-134">Type</span></span>   | <span data-ttu-id="3575b-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="3575b-135">Required</span></span> | <span data-ttu-id="3575b-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="3575b-136">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="3575b-137">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="3575b-137">customer-id</span></span> | <span data-ttu-id="3575b-138">sztring</span><span class="sxs-lookup"><span data-stu-id="3575b-138">string</span></span> | <span data-ttu-id="3575b-139">Igen</span><span class="sxs-lookup"><span data-stu-id="3575b-139">Yes</span></span>      | <span data-ttu-id="3575b-140">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="3575b-140">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="3575b-141">házirend-azonosító</span><span class="sxs-lookup"><span data-stu-id="3575b-141">policy-id</span></span>   | <span data-ttu-id="3575b-142">sztring</span><span class="sxs-lookup"><span data-stu-id="3575b-142">string</span></span> | <span data-ttu-id="3575b-143">Igen</span><span class="sxs-lookup"><span data-stu-id="3575b-143">Yes</span></span>      | <span data-ttu-id="3575b-144">Egy GUID-formázott karakterlánc, amely azonosítja a törölni kívánt szabályzatot.</span><span class="sxs-lookup"><span data-stu-id="3575b-144">A GUID-formatted string that identifies the policy to delete.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3575b-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="3575b-145">Request headers</span></span>

<span data-ttu-id="3575b-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3575b-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3575b-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="3575b-147">Request body</span></span>

<span data-ttu-id="3575b-148">Nincs</span><span class="sxs-lookup"><span data-stu-id="3575b-148">None</span></span>

### <a name="request-example"></a><span data-ttu-id="3575b-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="3575b-149">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="3575b-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="3575b-150">REST response</span></span>

<span data-ttu-id="3575b-151">Ha a művelet sikeres, a válasz egy 204-as tartalmat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="3575b-151">If successful, the response returns a 204 No Content status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3575b-152">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="3575b-152">Response success and error codes</span></span>

<span data-ttu-id="3575b-153">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="3575b-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3575b-154">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="3575b-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3575b-155">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="3575b-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3575b-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="3575b-156">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
