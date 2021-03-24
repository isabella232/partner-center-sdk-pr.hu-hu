---
title: Ügyfél végzettségének frissítése
description: Frissíti az ügyfél képzettségét aszinkron módon, beleértve a profilhoz társított címeket is.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 7606eeaac4df158ec0fad6ffd4e565bb250f448e
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030606"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="00559-103">Ügyfél-képesítések aszinkron frissítése</span><span class="sxs-lookup"><span data-stu-id="00559-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="00559-104">Aszinkron módon frissíti az ügyfél képzettségét.</span><span class="sxs-lookup"><span data-stu-id="00559-104">Updates a customer's qualifications asynchronously.</span></span>

<span data-ttu-id="00559-105">Egy partner aszinkron módon frissítheti az ügyfél képzettségét "Education" vagy "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="00559-105">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="00559-106">Más értékek, "None" és "nonprofit" nem állíthatók be.</span><span class="sxs-lookup"><span data-stu-id="00559-106">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00559-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="00559-107">Prerequisites</span></span>

- <span data-ttu-id="00559-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="00559-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="00559-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="00559-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="00559-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="00559-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="00559-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="00559-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="00559-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="00559-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="00559-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="00559-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="00559-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="00559-114">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="00559-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="00559-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="00559-116">C\#</span><span class="sxs-lookup"><span data-stu-id="00559-116">C\#</span></span>

<span data-ttu-id="00559-117">Először hozzon létre egy objektumot, amely a minősítés típusát jelöli.</span><span class="sxs-lookup"><span data-stu-id="00559-117">To create a customer's qualification for "Education", first create an object representing the qualification type.</span></span> <span data-ttu-id="00559-118">Ezután hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="00559-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="00559-119">Ezután használja a [**minősítés**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) tulajdonságot egy [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) felület lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="00559-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="00559-120">Végül hívja meg `CreateQualifications()` a vagy a `CreateQualificationsAsync()` minősítési típus objektumot bemeneti paraméterként.</span><span class="sxs-lookup"><span data-stu-id="00559-120">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object as an input parameter.</span></span>

``` csharp
var qualificationType = { Qualification = "education" };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

<span data-ttu-id="00559-121">**Példa**: [konzolos minta alkalmazás](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="00559-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="00559-122">**Projekt**: SdkSamples **osztály**: CreateCustomerQualification. cs</span><span class="sxs-lookup"><span data-stu-id="00559-122">**Project**: SdkSamples **Class**: CreateCustomerQualification.cs</span></span>

<span data-ttu-id="00559-123">Ha szeretné frissíteni az ügyfél minősítését, hogy **GovernmentCommunityCloud** egy meglévő ügyfélen a minősítés nélkül, akkor a partnernek is az ügyfél [**ValidationCode**](utility-resources.md#validationcode)kell tartoznia.</span><span class="sxs-lookup"><span data-stu-id="00559-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is also required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span> <span data-ttu-id="00559-124">Először hozzon létre egy objektumot, amely a minősítés típusát jelképezi.</span><span class="sxs-lookup"><span data-stu-id="00559-124">First, create an object representing the qualification type.</span></span> <span data-ttu-id="00559-125">Ezután hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="00559-125">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="00559-126">Ezután használja a [**minősítés**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) tulajdonságot egy [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) felület lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="00559-126">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="00559-127">Végül hívja meg `CreateQualifications()` `CreateQualificationsAsync()` a minősítési típus objektumot és az érvényesítési kódot bemeneti paraméterként.</span><span class="sxs-lookup"><span data-stu-id="00559-127">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object and the validation code as input parameters.</span></span>

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

<span data-ttu-id="00559-128">**Példa**: [konzolos minta alkalmazás](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="00559-128">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="00559-129">**Projekt**: SdkSamples **osztály**: CreateCustomerQualificationWithGCC. cs</span><span class="sxs-lookup"><span data-stu-id="00559-129">**Project**: SdkSamples **Class**: CreateCustomerQualificationWithGCC.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="00559-130">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="00559-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="00559-131">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="00559-131">Request syntax</span></span>

| <span data-ttu-id="00559-132">Metódus</span><span class="sxs-lookup"><span data-stu-id="00559-132">Method</span></span>  | <span data-ttu-id="00559-133">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="00559-133">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="00559-134">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="00559-134">**POST**</span></span> | <span data-ttu-id="00559-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/Qualifications? kód = {VALIDATIONCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="00559-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="00559-136">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="00559-136">URI parameter</span></span>

<span data-ttu-id="00559-137">A minősítés frissítéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="00559-137">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="00559-138">Név</span><span class="sxs-lookup"><span data-stu-id="00559-138">Name</span></span>                   | <span data-ttu-id="00559-139">Típus</span><span class="sxs-lookup"><span data-stu-id="00559-139">Type</span></span> | <span data-ttu-id="00559-140">Kötelező</span><span class="sxs-lookup"><span data-stu-id="00559-140">Required</span></span> | <span data-ttu-id="00559-141">Leírás</span><span class="sxs-lookup"><span data-stu-id="00559-141">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="00559-142">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="00559-142">**customer-tenant-id**</span></span> | <span data-ttu-id="00559-143">GUID</span><span class="sxs-lookup"><span data-stu-id="00559-143">GUID</span></span> | <span data-ttu-id="00559-144">Igen</span><span class="sxs-lookup"><span data-stu-id="00559-144">Yes</span></span>      | <span data-ttu-id="00559-145">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="00559-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="00559-146">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="00559-146">**validationCode**</span></span>     | <span data-ttu-id="00559-147">int</span><span class="sxs-lookup"><span data-stu-id="00559-147">int</span></span>  | <span data-ttu-id="00559-148">Nem</span><span class="sxs-lookup"><span data-stu-id="00559-148">No</span></span>       | <span data-ttu-id="00559-149">Csak a kormányzati közösségi felhőhöz szükséges.</span><span class="sxs-lookup"><span data-stu-id="00559-149">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="00559-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="00559-150">Request headers</span></span>

<span data-ttu-id="00559-151">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="00559-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="00559-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="00559-152">Request body</span></span>

<span data-ttu-id="00559-153">Ez a tábla a kérelem törzsének minősítési objektumát ismerteti.</span><span class="sxs-lookup"><span data-stu-id="00559-153">This table describes the qualification object in the request body.</span></span>

<span data-ttu-id="00559-154">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="00559-154">Property</span></span> | <span data-ttu-id="00559-155">Típus</span><span class="sxs-lookup"><span data-stu-id="00559-155">Type</span></span> | <span data-ttu-id="00559-156">Kötelező</span><span class="sxs-lookup"><span data-stu-id="00559-156">Required</span></span> | <span data-ttu-id="00559-157">Leírás</span><span class="sxs-lookup"><span data-stu-id="00559-157">Description</span></span>
-------- | ---- | -------- | -----------
<span data-ttu-id="00559-158">Minősítés</span><span class="sxs-lookup"><span data-stu-id="00559-158">Qualification</span></span> | <span data-ttu-id="00559-159">sztring</span><span class="sxs-lookup"><span data-stu-id="00559-159">string</span></span> | <span data-ttu-id="00559-160">Igen</span><span class="sxs-lookup"><span data-stu-id="00559-160">Yes</span></span> | <span data-ttu-id="00559-161">A [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) Enum karakterláncának értéke.</span><span class="sxs-lookup"><span data-stu-id="00559-161">The string value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="00559-162">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="00559-162">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="00559-163">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="00559-163">REST response</span></span>

<span data-ttu-id="00559-164">Ha ez sikeres, ez a metódus egy minősítési objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="00559-164">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="00559-165">Alább látható egy példa arra, hogy a **post** hívása egy ügyfélen (a **none** korábbi minősítésével) az **oktatási** minősítéssel.</span><span class="sxs-lookup"><span data-stu-id="00559-165">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="00559-166">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="00559-166">Response success and error codes</span></span>

<span data-ttu-id="00559-167">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="00559-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="00559-168">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="00559-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="00559-169">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="00559-169">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="00559-170">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="00559-170">Response example</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="00559-171">Kapcsolódó cikkek</span><span class="sxs-lookup"><span data-stu-id="00559-171">Related articles</span></span>

- [<span data-ttu-id="00559-172">Ügyfél képzettségének beszerzése</span><span class="sxs-lookup"><span data-stu-id="00559-172">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="00559-173">Egy partner ellenőrzési kódjainak lekérése</span><span class="sxs-lookup"><span data-stu-id="00559-173">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
