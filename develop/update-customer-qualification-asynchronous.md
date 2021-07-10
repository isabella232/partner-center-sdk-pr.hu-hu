---
title: Ügyfél végzettségének frissítése
description: Aszinkron módon frissíti az ügyfél minősítéseit, beleértve a profilhoz társított címet is.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: d7dd3593894ce91ddc7b96d604b80153d41d3a67
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572097"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="c9fa2-103">Ügyfél minősítésének aszinkron frissítése</span><span class="sxs-lookup"><span data-stu-id="c9fa2-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="c9fa2-104">Aszinkron módon frissíti az ügyfél minősítéseit.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-104">Updates a customer's qualifications asynchronously.</span></span>

<span data-ttu-id="c9fa2-105">A partnerek aszinkron módon frissítheti az ügyfelek minősítését " Education" vagy "GovernmentCocloud" minősítésre.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-105">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="c9fa2-106">Más értékek( "Nincs" és "Nonprofit" nem beállíthatók.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-106">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9fa2-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c9fa2-107">Prerequisites</span></span>

- <span data-ttu-id="c9fa2-108">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c9fa2-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c9fa2-109">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c9fa2-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c9fa2-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c9fa2-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="c9fa2-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c9fa2-112">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="c9fa2-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c9fa2-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="c9fa2-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c9fa2-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="c9fa2-114">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c9fa2-115">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c9fa2-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="c9fa2-116">C\#</span><span class="sxs-lookup"><span data-stu-id="c9fa2-116">C\#</span></span>

<span data-ttu-id="c9fa2-117">Ahhoz, hogy létrehoz egy ügyfél "Education" minősítését, először hozzon létre egy objektumot, amely a minősítési típust képviseli.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-117">To create a customer's qualification for "Education", first create an object representing the qualification type.</span></span> <span data-ttu-id="c9fa2-118">Ezután hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="c9fa2-119">Ezután a [**Minősítés tulajdonság**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) használatával lekér egy [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) felületet.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="c9fa2-120">Végül hívja meg `CreateQualifications()` a vagy a parancsot a `CreateQualificationsAsync()` minősítési típus objektummal bemeneti paraméterként.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-120">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object as an input parameter.</span></span>

``` csharp
var qualificationToCreate = "education";    // can also be "StateOwnedEntity" or "GovernmentCommunityCloud". See GCC example below.
var qualificationType = { Qualification = qualificationToCreate };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

<span data-ttu-id="c9fa2-121">**Minta:** [Konzol mintaalkalmazás.](https://github.com/microsoft/Partner-Center-DotNet-Samples)</span><span class="sxs-lookup"><span data-stu-id="c9fa2-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="c9fa2-122">**Project:** SdkSamples **osztály:** CreateCustomerQualification.cs</span><span class="sxs-lookup"><span data-stu-id="c9fa2-122">**Project**: SdkSamples **Class**: CreateCustomerQualification.cs</span></span>

<span data-ttu-id="c9fa2-123">Ahhoz, hogy egy ügyfél minősítés nélkül is frissítve legyen a **GovernmentCocloud** minősítése egy meglévő ügyfélen, a partnernek tartalmaznia kell az ügyfél [**ValidationCode (Érvényesítési**](utility-resources.md#validationcode)kódja) kódját is.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is also required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span> <span data-ttu-id="c9fa2-124">Először hozzon létre egy objektumot, amely a minősítési típust képviseli.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-124">First, create an object representing the qualification type.</span></span> <span data-ttu-id="c9fa2-125">Ezután hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-125">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="c9fa2-126">Ezután a [**Minősítés tulajdonság**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) használatával lekér egy [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) felületet.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-126">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="c9fa2-127">Végül hívja meg a vagy a `CreateQualifications()` parancsot `CreateQualificationsAsync()` a minősítési típus objektummal és az érvényesítési kóddal bemeneti paraméterként.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-127">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object and the validation code as input parameters.</span></span>

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

<span data-ttu-id="c9fa2-128">**Minta:** [Konzol mintaalkalmazás.](https://github.com/microsoft/Partner-Center-DotNet-Samples)</span><span class="sxs-lookup"><span data-stu-id="c9fa2-128">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="c9fa2-129">**Project:** SdkSamples **osztály:** CreateCustomerQualificationWithGCC.cs</span><span class="sxs-lookup"><span data-stu-id="c9fa2-129">**Project**: SdkSamples **Class**: CreateCustomerQualificationWithGCC.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c9fa2-130">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="c9fa2-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c9fa2-131">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="c9fa2-131">Request syntax</span></span>

| <span data-ttu-id="c9fa2-132">Metódus</span><span class="sxs-lookup"><span data-stu-id="c9fa2-132">Method</span></span>  | <span data-ttu-id="c9fa2-133">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="c9fa2-133">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c9fa2-134">**Post**</span><span class="sxs-lookup"><span data-stu-id="c9fa2-134">**POST**</span></span> | <span data-ttu-id="c9fa2-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c9fa2-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="c9fa2-136">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="c9fa2-136">URI parameter</span></span>

<span data-ttu-id="c9fa2-137">A minősítés frissítéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-137">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="c9fa2-138">Név</span><span class="sxs-lookup"><span data-stu-id="c9fa2-138">Name</span></span>                   | <span data-ttu-id="c9fa2-139">Típus</span><span class="sxs-lookup"><span data-stu-id="c9fa2-139">Type</span></span> | <span data-ttu-id="c9fa2-140">Kötelező</span><span class="sxs-lookup"><span data-stu-id="c9fa2-140">Required</span></span> | <span data-ttu-id="c9fa2-141">Leírás</span><span class="sxs-lookup"><span data-stu-id="c9fa2-141">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c9fa2-142">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="c9fa2-142">**customer-tenant-id**</span></span> | <span data-ttu-id="c9fa2-143">GUID</span><span class="sxs-lookup"><span data-stu-id="c9fa2-143">GUID</span></span> | <span data-ttu-id="c9fa2-144">Yes</span><span class="sxs-lookup"><span data-stu-id="c9fa2-144">Yes</span></span>      | <span data-ttu-id="c9fa2-145">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="c9fa2-146">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="c9fa2-146">**validationCode**</span></span>     | <span data-ttu-id="c9fa2-147">int</span><span class="sxs-lookup"><span data-stu-id="c9fa2-147">int</span></span>  | <span data-ttu-id="c9fa2-148">No</span><span class="sxs-lookup"><span data-stu-id="c9fa2-148">No</span></span>       | <span data-ttu-id="c9fa2-149">Csak az ilyen Government Community Cloud.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-149">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="c9fa2-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="c9fa2-150">Request headers</span></span>

<span data-ttu-id="c9fa2-151">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c9fa2-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c9fa2-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="c9fa2-152">Request body</span></span>

<span data-ttu-id="c9fa2-153">Ez a táblázat a kérelem törzsében található minősítési objektumot ismerteti.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-153">This table describes the qualification object in the request body.</span></span>

<span data-ttu-id="c9fa2-154">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="c9fa2-154">Property</span></span> | <span data-ttu-id="c9fa2-155">Típus</span><span class="sxs-lookup"><span data-stu-id="c9fa2-155">Type</span></span> | <span data-ttu-id="c9fa2-156">Kötelező</span><span class="sxs-lookup"><span data-stu-id="c9fa2-156">Required</span></span> | <span data-ttu-id="c9fa2-157">Leírás</span><span class="sxs-lookup"><span data-stu-id="c9fa2-157">Description</span></span>
-------- | ---- | -------- | -----------
<span data-ttu-id="c9fa2-158">Minősítés</span><span class="sxs-lookup"><span data-stu-id="c9fa2-158">Qualification</span></span> | <span data-ttu-id="c9fa2-159">sztring</span><span class="sxs-lookup"><span data-stu-id="c9fa2-159">string</span></span> | <span data-ttu-id="c9fa2-160">Yes</span><span class="sxs-lookup"><span data-stu-id="c9fa2-160">Yes</span></span> | <span data-ttu-id="c9fa2-161">A [**CustomerQualification enum sztringértéke.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)</span><span class="sxs-lookup"><span data-stu-id="c9fa2-161">The string value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="c9fa2-162">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="c9fa2-162">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

{
    "Qualification": "Education"
}

```

## <a name="rest-response"></a><span data-ttu-id="c9fa2-163">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="c9fa2-163">REST response</span></span>

<span data-ttu-id="c9fa2-164">Ha sikeres, ez a metódus egy minősítési objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-164">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="c9fa2-165">Az alábbiakban egy  példát mutatunk be egy olyan ügyfél POST-hívására (korábbi minősítéssel: **Nincs),** amely rendelkezik **Oktatási minősítéssel.**</span><span class="sxs-lookup"><span data-stu-id="c9fa2-165">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c9fa2-166">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="c9fa2-166">Response success and error codes</span></span>

<span data-ttu-id="c9fa2-167">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c9fa2-168">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="c9fa2-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c9fa2-169">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c9fa2-169">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c9fa2-170">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="c9fa2-170">Response example</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="c9fa2-171">Kapcsolódó cikkek</span><span class="sxs-lookup"><span data-stu-id="c9fa2-171">Related articles</span></span>

- [<span data-ttu-id="c9fa2-172">Ügyfél minősítésének lekértsége</span><span class="sxs-lookup"><span data-stu-id="c9fa2-172">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="c9fa2-173">Egy partner ellenőrzési kódjainak lekérése</span><span class="sxs-lookup"><span data-stu-id="c9fa2-173">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
