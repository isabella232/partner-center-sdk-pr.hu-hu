---
title: Ügyfél végzettségének frissítése
description: Megtudhatja, hogyan frissítheti az ügyfél képzettségét aszinkron szűréssel vagy átvilágítással, beleértve a profilhoz társított címeket is.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 703585eeaba93b6d7a510a3174a78a28f22e1510
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711933"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="deac3-103">Ügyfél-képesítések aszinkron frissítése</span><span class="sxs-lookup"><span data-stu-id="deac3-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="deac3-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="deac3-104">**Applies To**</span></span>

- <span data-ttu-id="deac3-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="deac3-105">Partner Center</span></span>

<span data-ttu-id="deac3-106">Ismerje meg, hogyan frissítheti az ügyfeleket a partner Center API-kon keresztül aszinkron módon.</span><span class="sxs-lookup"><span data-stu-id="deac3-106">Learn how to update a customer's qualifications asynchronously via Partner Center APIs.</span></span> <span data-ttu-id="deac3-107">Ha szeretné megtudni, hogyan teheti meg ezt a szinkron módon, tekintse meg az [ügyfél minősítésének frissítése szinkron ellenőrzésen keresztül](update-customer-qualification-synchronous.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="deac3-107">To learn how to do this synchronously, see [Update a customer's qualification via synchronous validation](update-customer-qualification-synchronous.md).</span></span>

<span data-ttu-id="deac3-108">Egy partner aszinkron módon frissítheti az ügyfél képzettségét "Education" vagy "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="deac3-108">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="deac3-109">Más értékek, "None" és "nonprofit" nem állíthatók be.</span><span class="sxs-lookup"><span data-stu-id="deac3-109">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="deac3-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="deac3-110">Prerequisites</span></span>

- <span data-ttu-id="deac3-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="deac3-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="deac3-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="deac3-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="deac3-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="deac3-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="deac3-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="deac3-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="deac3-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="deac3-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="deac3-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="deac3-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="deac3-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="deac3-117">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="deac3-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="deac3-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="deac3-119">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="deac3-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="deac3-120">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="deac3-120">Request syntax</span></span>

| <span data-ttu-id="deac3-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="deac3-121">Method</span></span>  | <span data-ttu-id="deac3-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="deac3-122">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="deac3-123">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="deac3-123">**POST**</span></span> | <span data-ttu-id="deac3-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/Qualifications? kód = {VALIDATIONCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="deac3-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="deac3-125">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="deac3-125">URI parameter</span></span>

<span data-ttu-id="deac3-126">A minősítés frissítéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="deac3-126">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="deac3-127">Név</span><span class="sxs-lookup"><span data-stu-id="deac3-127">Name</span></span>                   | <span data-ttu-id="deac3-128">Típus</span><span class="sxs-lookup"><span data-stu-id="deac3-128">Type</span></span> | <span data-ttu-id="deac3-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="deac3-129">Required</span></span> | <span data-ttu-id="deac3-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="deac3-130">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="deac3-131">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="deac3-131">**customer-tenant-id**</span></span> | <span data-ttu-id="deac3-132">GUID</span><span class="sxs-lookup"><span data-stu-id="deac3-132">GUID</span></span> | <span data-ttu-id="deac3-133">Yes</span><span class="sxs-lookup"><span data-stu-id="deac3-133">Yes</span></span>      | <span data-ttu-id="deac3-134">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="deac3-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="deac3-135">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="deac3-135">**validationCode**</span></span>     | <span data-ttu-id="deac3-136">int</span><span class="sxs-lookup"><span data-stu-id="deac3-136">int</span></span>  | <span data-ttu-id="deac3-137">No</span><span class="sxs-lookup"><span data-stu-id="deac3-137">No</span></span>       | <span data-ttu-id="deac3-138">Csak a kormányzati közösségi felhőhöz szükséges.</span><span class="sxs-lookup"><span data-stu-id="deac3-138">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="deac3-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="deac3-139">Request headers</span></span>

<span data-ttu-id="deac3-140">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="deac3-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="deac3-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="deac3-141">Request body</span></span>

<span data-ttu-id="deac3-142">A [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enumerálás egész értékének értéke.</span><span class="sxs-lookup"><span data-stu-id="deac3-142">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="deac3-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="deac3-143">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="deac3-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="deac3-144">REST response</span></span>

<span data-ttu-id="deac3-145">Ha ez sikeres, ez a metódus egy minősítési objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="deac3-145">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="deac3-146">Alább látható egy példa arra, hogy a **post** hívása egy ügyfélen (a **none** korábbi minősítésével) az **oktatási** minősítéssel.</span><span class="sxs-lookup"><span data-stu-id="deac3-146">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="deac3-147">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="deac3-147">Response success and error codes</span></span>

<span data-ttu-id="deac3-148">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="deac3-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="deac3-149">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="deac3-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="deac3-150">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="deac3-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="deac3-151">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="deac3-151">Response example</span></span>

```http
HTTP/1.1 201 CREATED
Content-Length: 29
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualification": "Education",
    "vettingStatus": "InReview",
    "vettingCreateDate": "2020-12-04T20:54:24Z" // UTC
}
```

## <a name="related-articles"></a><span data-ttu-id="deac3-152">Kapcsolódó cikkek</span><span class="sxs-lookup"><span data-stu-id="deac3-152">Related articles</span></span>

- [<span data-ttu-id="deac3-153">Ügyfél képzettségének beszerzése</span><span class="sxs-lookup"><span data-stu-id="deac3-153">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="deac3-154">Egy partner ellenőrzési kódjainak lekérése</span><span class="sxs-lookup"><span data-stu-id="deac3-154">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)