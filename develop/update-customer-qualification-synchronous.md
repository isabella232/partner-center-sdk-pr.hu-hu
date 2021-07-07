---
title: Ügyfél végzettségének frissítése
description: Megtudhatja, hogyan frissítheti az ügyfelek minősítését szinkron szűréssel vagy átvizsgálással, beleértve a profilhoz társított címet is.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 5047743afdef02033d9494e3d8c16c9ab96b3fe9
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446649"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="81288-103">Ügyfél minősítésének frissítése szinkron ellenőrzéssel</span><span class="sxs-lookup"><span data-stu-id="81288-103">Update a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="81288-104">Megtudhatja, hogyan frissítheti az ügyfelek minősítését szinkron módon az Partnerközpont API-kon keresztül.</span><span class="sxs-lookup"><span data-stu-id="81288-104">Learn how to update a customer's qualifications synchronously via Partner Center APIs.</span></span> <span data-ttu-id="81288-105">Ennek aszinkron módon történő érvényre hozásról lásd: Ügyfél minősítésének frissítése [aszinkron ellenőrzéssel.](update-customer-qualification-asynchronous.md)</span><span class="sxs-lookup"><span data-stu-id="81288-105">To learn how to do this asynchronously, see [Update a customer's qualification via asynchronous validation](update-customer-qualification-asynchronous.md).</span></span>

<span data-ttu-id="81288-106">A partnerek frissíthetik az ügyfelek "Education" vagy "GovernmentCocloud" minősítését.</span><span class="sxs-lookup"><span data-stu-id="81288-106">A partner can update a customer's qualification to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="81288-107">Más értékek( "Nincs" és "Nonprofit" nem beállíthatók.</span><span class="sxs-lookup"><span data-stu-id="81288-107">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81288-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="81288-108">Prerequisites</span></span>

- <span data-ttu-id="81288-109">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="81288-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="81288-110">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="81288-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="81288-111">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="81288-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="81288-112">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="81288-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="81288-113">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="81288-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="81288-114">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="81288-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="81288-115">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="81288-115">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="81288-116">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="81288-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="81288-117">C\#</span><span class="sxs-lookup"><span data-stu-id="81288-117">C\#</span></span>

<span data-ttu-id="81288-118">Ha frissítenie kell egy ügyfél "Education" minősítését, hívja meg **az [Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** hívást egy meglévő [**ügyfélen.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer)</span><span class="sxs-lookup"><span data-stu-id="81288-118">To update a customer's qualification to "Education", call **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** on an existing  [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span></span>

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

<span data-ttu-id="81288-119">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="81288-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="81288-120">**Project:** PartnerSDK.FeatureSamples **osztály:** CustomerQualificationOperations.cs</span><span class="sxs-lookup"><span data-stu-id="81288-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerQualificationOperations.cs</span></span>

<span data-ttu-id="81288-121">Ahhoz, hogy az ügyfél minősítés nélkül frissítve legyen a **GovernmentCocloud** minősítése egy meglévő ügyfélen, a partnernek tartalmaznia kell az ügyfél [**ValidationCode (Érvényesítési**](utility-resources.md#validationcode)kódja) kódját.</span><span class="sxs-lookup"><span data-stu-id="81288-121">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span>

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a><span data-ttu-id="81288-122">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="81288-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="81288-123">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="81288-123">Request syntax</span></span>

| <span data-ttu-id="81288-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="81288-124">Method</span></span>  | <span data-ttu-id="81288-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="81288-125">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="81288-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="81288-126">**PUT**</span></span> | <span data-ttu-id="81288-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="81288-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="81288-128">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="81288-128">URI parameter</span></span>

<span data-ttu-id="81288-129">A minősítés frissítéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="81288-129">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="81288-130">Név</span><span class="sxs-lookup"><span data-stu-id="81288-130">Name</span></span>                   | <span data-ttu-id="81288-131">Típus</span><span class="sxs-lookup"><span data-stu-id="81288-131">Type</span></span> | <span data-ttu-id="81288-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="81288-132">Required</span></span> | <span data-ttu-id="81288-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="81288-133">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="81288-134">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="81288-134">**customer-tenant-id**</span></span> | <span data-ttu-id="81288-135">GUID</span><span class="sxs-lookup"><span data-stu-id="81288-135">GUID</span></span> | <span data-ttu-id="81288-136">Igen</span><span class="sxs-lookup"><span data-stu-id="81288-136">Yes</span></span>      | <span data-ttu-id="81288-137">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="81288-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="81288-138">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="81288-138">**validationCode**</span></span>     | <span data-ttu-id="81288-139">int</span><span class="sxs-lookup"><span data-stu-id="81288-139">int</span></span>  | <span data-ttu-id="81288-140">Nem</span><span class="sxs-lookup"><span data-stu-id="81288-140">No</span></span>       | <span data-ttu-id="81288-141">Csak a Government Community Cloud.</span><span class="sxs-lookup"><span data-stu-id="81288-141">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="81288-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="81288-142">Request headers</span></span>

<span data-ttu-id="81288-143">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="81288-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="81288-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="81288-144">Request body</span></span>

<span data-ttu-id="81288-145">A [**CustomerQualification enum**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) egész értéke.</span><span class="sxs-lookup"><span data-stu-id="81288-145">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="81288-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="81288-146">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="81288-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="81288-147">REST response</span></span>

<span data-ttu-id="81288-148">Ha a művelet sikeres, ez a metódus visszaadja a [**frissített Minősítés tulajdonságot**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="81288-148">If successful, this method returns updated [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="81288-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="81288-149">Response success and error codes</span></span>

<span data-ttu-id="81288-150">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="81288-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="81288-151">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="81288-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="81288-152">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="81288-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="81288-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="81288-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a><span data-ttu-id="81288-154">Kapcsolódó cikkek</span><span class="sxs-lookup"><span data-stu-id="81288-154">Related articles</span></span>

- [<span data-ttu-id="81288-155">Egy ügyfél végzettségének lekérése</span><span class="sxs-lookup"><span data-stu-id="81288-155">Get a customer's qualification</span></span>](./get-customer-qualification-synchronous.md)
- [<span data-ttu-id="81288-156">Egy partner ellenőrzési kódjainak lekérése</span><span class="sxs-lookup"><span data-stu-id="81288-156">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
