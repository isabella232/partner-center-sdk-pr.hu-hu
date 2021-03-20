---
title: Ügyfél végzettségének frissítése
description: Megtudhatja, hogyan frissítheti az ügyfél képzettségét szinkron szűréssel vagy átvilágítással, beleértve a profilhoz társított címeket is.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: c202d95beab771241a9665243be5f08ab6f82fd5
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711967"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="2e357-103">Ügyfél minősítésének frissítése szinkron ellenőrzés útján</span><span class="sxs-lookup"><span data-stu-id="2e357-103">Update a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="2e357-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="2e357-104">**Applies To**</span></span>

- <span data-ttu-id="2e357-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="2e357-105">Partner Center</span></span>

<span data-ttu-id="2e357-106">Ismerje meg, hogyan frissítheti az ügyfeleket a partner Center API-kkal párhuzamosan.</span><span class="sxs-lookup"><span data-stu-id="2e357-106">Learn how to update a customer's qualifications synchronously via Partner Center APIs.</span></span> <span data-ttu-id="2e357-107">Ennek aszinkron módon történő végrehajtásával kapcsolatban lásd: [az ügyfél minősítésének frissítése aszinkron ellenőrzés útján](update-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="2e357-107">To learn how to do this asynchronously, see [Update a customer's qualification via asynchronous validation](update-customer-qualification-asynchronous.md).</span></span>

<span data-ttu-id="2e357-108">Egy partner frissítheti az ügyfél minősítését, hogy "Education" vagy "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="2e357-108">A partner can update a customer's qualification to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="2e357-109">Más értékek, "None" és "nonprofit" nem állíthatók be.</span><span class="sxs-lookup"><span data-stu-id="2e357-109">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e357-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2e357-110">Prerequisites</span></span>

- <span data-ttu-id="2e357-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="2e357-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2e357-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="2e357-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2e357-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2e357-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2e357-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="2e357-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2e357-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="2e357-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2e357-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="2e357-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2e357-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="2e357-117">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2e357-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2e357-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2e357-119">C\#</span><span class="sxs-lookup"><span data-stu-id="2e357-119">C\#</span></span>

<span data-ttu-id="2e357-120">Ha frissíteni szeretné az ügyfél képzettségét az "oktatás" értékre, hívja meg a **[Update/DotNet/API/Microsoft. Store. partnercenter. minősítés. icustomerqualification. Update)** egy meglévő  [**ügyfélen**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span><span class="sxs-lookup"><span data-stu-id="2e357-120">To update a customer's qualification to "Education", call **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** on an existing  [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span></span>

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

<span data-ttu-id="2e357-121">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2e357-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2e357-122">**Projekt**: PartnerSDK. FeatureSamples **osztály**: CustomerQualificationOperations. cs</span><span class="sxs-lookup"><span data-stu-id="2e357-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerQualificationOperations.cs</span></span>

<span data-ttu-id="2e357-123">Az ügyfél minősítésének frissítése egy meglévő ügyfél **GovernmentCommunityCloud** minősítés nélkül.</span><span class="sxs-lookup"><span data-stu-id="2e357-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification.</span></span>  <span data-ttu-id="2e357-124">Emellett a partnernek is meg kell adnia az ügyfél [**ValidationCode**](utility-resources.md#validationcode).</span><span class="sxs-lookup"><span data-stu-id="2e357-124">The partner is also are required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span>

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a><span data-ttu-id="2e357-125">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="2e357-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2e357-126">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="2e357-126">Request syntax</span></span>

| <span data-ttu-id="2e357-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="2e357-127">Method</span></span>  | <span data-ttu-id="2e357-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2e357-128">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e357-129">**PUT**</span><span class="sxs-lookup"><span data-stu-id="2e357-129">**PUT**</span></span> | <span data-ttu-id="2e357-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/Qualification? kód = {VALIDATIONCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2e357-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2e357-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="2e357-131">URI parameter</span></span>

<span data-ttu-id="2e357-132">A minősítés frissítéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="2e357-132">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="2e357-133">Név</span><span class="sxs-lookup"><span data-stu-id="2e357-133">Name</span></span>                   | <span data-ttu-id="2e357-134">Típus</span><span class="sxs-lookup"><span data-stu-id="2e357-134">Type</span></span> | <span data-ttu-id="2e357-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2e357-135">Required</span></span> | <span data-ttu-id="2e357-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="2e357-136">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e357-137">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="2e357-137">**customer-tenant-id**</span></span> | <span data-ttu-id="2e357-138">GUID</span><span class="sxs-lookup"><span data-stu-id="2e357-138">GUID</span></span> | <span data-ttu-id="2e357-139">Yes</span><span class="sxs-lookup"><span data-stu-id="2e357-139">Yes</span></span>      | <span data-ttu-id="2e357-140">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="2e357-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="2e357-141">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="2e357-141">**validationCode**</span></span>     | <span data-ttu-id="2e357-142">int</span><span class="sxs-lookup"><span data-stu-id="2e357-142">int</span></span>  | <span data-ttu-id="2e357-143">No</span><span class="sxs-lookup"><span data-stu-id="2e357-143">No</span></span>       | <span data-ttu-id="2e357-144">Csak a kormányzati közösségi felhőhöz szükséges.</span><span class="sxs-lookup"><span data-stu-id="2e357-144">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="2e357-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2e357-145">Request headers</span></span>

<span data-ttu-id="2e357-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2e357-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2e357-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2e357-147">Request body</span></span>

<span data-ttu-id="2e357-148">A [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enumerálás egész értékének értéke.</span><span class="sxs-lookup"><span data-stu-id="2e357-148">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="2e357-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="2e357-149">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="2e357-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2e357-150">REST response</span></span>

<span data-ttu-id="2e357-151">Ha ez sikeres, ez a metódus visszaadja a frissített [**minősítési**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) tulajdonságot a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="2e357-151">If successful, this method returns updated [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2e357-152">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2e357-152">Response success and error codes</span></span>

<span data-ttu-id="2e357-153">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="2e357-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2e357-154">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="2e357-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2e357-155">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2e357-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2e357-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2e357-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a><span data-ttu-id="2e357-157">Kapcsolódó cikkek</span><span class="sxs-lookup"><span data-stu-id="2e357-157">Related articles</span></span>

- [<span data-ttu-id="2e357-158">Egy ügyfél végzettségének lekérése</span><span class="sxs-lookup"><span data-stu-id="2e357-158">Get a customer's qualification</span></span>](./get-customer-qualification-synchronous.md)
- [<span data-ttu-id="2e357-159">Egy partner ellenőrzési kódjainak lekérése</span><span class="sxs-lookup"><span data-stu-id="2e357-159">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)