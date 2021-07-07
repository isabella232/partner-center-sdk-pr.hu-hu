---
title: Egy ügyfél számlázási profiljának frissítése
description: Frissíti az ügyfél számlázási profilját, beleértve a profilhoz társított címet is.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 1605c3e8cb050717209cb482d2299e2a42b9b186
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530038"
---
# <a name="update-a-customers-billing-profile"></a><span data-ttu-id="e0d5a-103">Egy ügyfél számlázási profiljának frissítése</span><span class="sxs-lookup"><span data-stu-id="e0d5a-103">Update a customer's billing profile</span></span>

<span data-ttu-id="e0d5a-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e0d5a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e0d5a-105">Frissíti az ügyfél számlázási profilját, beleértve a profilhoz társított címet is.</span><span class="sxs-lookup"><span data-stu-id="e0d5a-105">Updates a customer's billing profile, including the address associated with the profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0d5a-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="e0d5a-106">Prerequisites</span></span>

- <span data-ttu-id="e0d5a-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e0d5a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e0d5a-108">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="e0d5a-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e0d5a-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e0d5a-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e0d5a-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="e0d5a-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e0d5a-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e0d5a-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e0d5a-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e0d5a-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e0d5a-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="e0d5a-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e0d5a-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e0d5a-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e0d5a-115">C\#</span><span class="sxs-lookup"><span data-stu-id="e0d5a-115">C\#</span></span>

<span data-ttu-id="e0d5a-116">Az ügyfél számlázási profiljának frissítéséhez olvassa be a számlázási profilt, és szükség szerint frissítse a tulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="e0d5a-116">To update a customer's billing profile, retrieve the billing profile and update the properties as necessary.</span></span> <span data-ttu-id="e0d5a-117">Ezután olvassa be az [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, majd hívja meg a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="e0d5a-117">Then, retrieve your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, and then call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="e0d5a-118">Ezután hívja meg [**a Profiles (Profilok)**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) tulajdonságot, majd a [**Billing (Számlázás)**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="e0d5a-118">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="e0d5a-119">Végül hívja meg az [**Update() vagy**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) [**az UpdateAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync)</span><span class="sxs-lookup"><span data-stu-id="e0d5a-119">Then, finish by calling the [**Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();

// Apply changes to profile;

billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Update(billingProfile);
```

<span data-ttu-id="e0d5a-120">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e0d5a-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e0d5a-121">**Project**: PartnerSDK.FeatureSamples **osztály:** UpdateCustomerBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="e0d5a-121">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e0d5a-122">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="e0d5a-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e0d5a-123">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="e0d5a-123">Request syntax</span></span>

| <span data-ttu-id="e0d5a-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="e0d5a-124">Method</span></span>  | <span data-ttu-id="e0d5a-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="e0d5a-125">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e0d5a-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="e0d5a-126">**PUT**</span></span> | <span data-ttu-id="e0d5a-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e0d5a-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e0d5a-128">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="e0d5a-128">URI parameter</span></span>

<span data-ttu-id="e0d5a-129">A számlázási profil frissítéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="e0d5a-129">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="e0d5a-130">Név</span><span class="sxs-lookup"><span data-stu-id="e0d5a-130">Name</span></span>                   | <span data-ttu-id="e0d5a-131">Típus</span><span class="sxs-lookup"><span data-stu-id="e0d5a-131">Type</span></span>     | <span data-ttu-id="e0d5a-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e0d5a-132">Required</span></span> | <span data-ttu-id="e0d5a-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="e0d5a-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e0d5a-134">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="e0d5a-134">**customer-tenant-id**</span></span> | <span data-ttu-id="e0d5a-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="e0d5a-135">**guid**</span></span> | <span data-ttu-id="e0d5a-136">Y</span><span class="sxs-lookup"><span data-stu-id="e0d5a-136">Y</span></span>        | <span data-ttu-id="e0d5a-137">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="e0d5a-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e0d5a-138">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="e0d5a-138">Request headers</span></span>

- <span data-ttu-id="e0d5a-139">**If-Match:**" &lt; &gt; ETag" szükséges az egyidejűség észleléséhez.</span><span class="sxs-lookup"><span data-stu-id="e0d5a-139">**If-Match**: "&lt;ETag&gt;" is required for concurrency detection.</span></span>
<span data-ttu-id="e0d5a-140">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e0d5a-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e0d5a-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="e0d5a-141">Request body</span></span>

<span data-ttu-id="e0d5a-142">A teljes erőforrás.</span><span class="sxs-lookup"><span data-stu-id="e0d5a-142">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="e0d5a-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="e0d5a-143">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ff85f13a-eb65-4b8e-9b67-05beb0565410
MS-CorrelationId: ff1b757d-cfaf-463a-b48b-0f96d05e95d7
Content-Type: application/json
Content-Length: 639
Expect: 100-continue

{
    "Id": "a58ceba5-60ac-48e4-a0bc-2a855811807a",
    "FirstName": "FirstName",
    "LastName": "LastName",
    "Email": "email@sample.com",
    "Culture": "en-US",
    "Language": "en",
    "CompanyName": "CompanyName",
    "DefaultAddress": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "One Microsoft Way",
        "AddressLine2": null,
        "PostalCode": "98052",
        "FirstName": "FirstName",
        "LastName": "LastName",
        "PhoneNumber": "4255555555"
    },
    "Links": {
        "Self": {
            "Uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "Method": "GET",
            "Headers": []
        }
    },
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "CustomerBillingProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="e0d5a-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="e0d5a-144">REST response</span></span>

<span data-ttu-id="e0d5a-145">Ha ez a metódus [](profile-resources.md) sikeres, a válasz törzsében frissített profilerőforrás-tulajdonságokat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="e0d5a-145">If successful, this method returns updated [Profile](profile-resources.md) resource properties in the response body.</span></span> <span data-ttu-id="e0d5a-146">A híváshoz szükség van egy ETagre az egyidejűség észleléséhez.</span><span class="sxs-lookup"><span data-stu-id="e0d5a-146">This call requires an ETag for concurrency detection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e0d5a-147">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="e0d5a-147">Response success and error codes</span></span>

<span data-ttu-id="e0d5a-148">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="e0d5a-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e0d5a-149">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="e0d5a-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e0d5a-150">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e0d5a-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e0d5a-151">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="e0d5a-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1210
Content-Type: application/json
MS-CorrelationId: ff1b757d-cfaf-463a-b48b-0f96d05e95d7
MS-RequestId: ff85f13a-eb65-4b8e-9b67-05beb0565410
Date: Mon, 23 Nov 2015 18:20:43 GMT

{
    "id": "a58ceba5-60ac-48e4-a0bc-2a855811807a",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "companyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "One Microsoft Way",
        "postalCode": "98052",
        "firstName": "FirstName",
        "lastName": "LastName",
        "phoneNumber": "4255555555"
    },
    "links": {
        "self": {
            "uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "<etag>",
        "objectType": "CustomerBillingProfile"
    }
}
```
