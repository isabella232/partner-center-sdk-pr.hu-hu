---
title: Egy ügyfél számlázási profiljának frissítése
description: Frissíti az ügyfél számlázási profilját, beleértve a profilhoz társított címeket is.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: adf4e3de9941fded632e0561624d91d854c5aa24
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768392"
---
# <a name="update-a-customers-billing-profile"></a><span data-ttu-id="02743-103">Egy ügyfél számlázási profiljának frissítése</span><span class="sxs-lookup"><span data-stu-id="02743-103">Update a customer's billing profile</span></span>

<span data-ttu-id="02743-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="02743-104">**Applies To**</span></span>

- <span data-ttu-id="02743-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="02743-105">Partner Center</span></span>
- <span data-ttu-id="02743-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="02743-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="02743-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="02743-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="02743-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="02743-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="02743-109">Frissíti az ügyfél számlázási profilját, beleértve a profilhoz társított címeket is.</span><span class="sxs-lookup"><span data-stu-id="02743-109">Updates a customer's billing profile, including the address associated with the profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02743-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="02743-110">Prerequisites</span></span>

- <span data-ttu-id="02743-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="02743-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="02743-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="02743-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="02743-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="02743-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="02743-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="02743-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="02743-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="02743-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="02743-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="02743-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="02743-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="02743-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="02743-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="02743-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="02743-119">C\#</span><span class="sxs-lookup"><span data-stu-id="02743-119">C\#</span></span>

<span data-ttu-id="02743-120">Az ügyfél számlázási profiljának frissítéséhez kérje le a számlázási profilt, és szükség szerint frissítse a tulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="02743-120">To update a customer's billing profile, retrieve the billing profile and update the properties as necessary.</span></span> <span data-ttu-id="02743-121">Ezután kérje le a [**IPartner. Customs**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, majd hívja meg a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="02743-121">Then, retrieve your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, and then call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="02743-122">Ezután hívja meg a [**profilok**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) tulajdonságot, majd a [**Számlázási**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="02743-122">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="02743-123">Ezt követően fejezze be a [**frissítés ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) vagy a [**UpdateAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) metódusok meghívásával.</span><span class="sxs-lookup"><span data-stu-id="02743-123">Then, finish by calling the [**Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();

// Apply changes to profile;

billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Update(billingProfile);
```

<span data-ttu-id="02743-124">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="02743-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="02743-125">**Projekt**: PartnerSDK. FeatureSamples **osztály**: UpdateCustomerBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="02743-125">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="02743-126">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="02743-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="02743-127">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="02743-127">Request syntax</span></span>

| <span data-ttu-id="02743-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="02743-128">Method</span></span>  | <span data-ttu-id="02743-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="02743-129">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="02743-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="02743-130">**PUT**</span></span> | <span data-ttu-id="02743-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Profiles/Billing http/1.1</span><span class="sxs-lookup"><span data-stu-id="02743-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="02743-132">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="02743-132">URI parameter</span></span>

<span data-ttu-id="02743-133">A számlázási profil frissítéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="02743-133">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="02743-134">Név</span><span class="sxs-lookup"><span data-stu-id="02743-134">Name</span></span>                   | <span data-ttu-id="02743-135">Típus</span><span class="sxs-lookup"><span data-stu-id="02743-135">Type</span></span>     | <span data-ttu-id="02743-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="02743-136">Required</span></span> | <span data-ttu-id="02743-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="02743-137">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="02743-138">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="02743-138">**customer-tenant-id**</span></span> | <span data-ttu-id="02743-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="02743-139">**guid**</span></span> | <span data-ttu-id="02743-140">Y</span><span class="sxs-lookup"><span data-stu-id="02743-140">Y</span></span>        | <span data-ttu-id="02743-141">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="02743-141">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="02743-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="02743-142">Request headers</span></span>

- <span data-ttu-id="02743-143">**IF-Match**: " &lt; ETAG &gt; " szükséges a Egyidejűség észleléséhez.</span><span class="sxs-lookup"><span data-stu-id="02743-143">**If-Match**: "&lt;ETag&gt;" is required for concurrency detection.</span></span>
<span data-ttu-id="02743-144">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="02743-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="02743-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="02743-145">Request body</span></span>

<span data-ttu-id="02743-146">A teljes erőforrás.</span><span class="sxs-lookup"><span data-stu-id="02743-146">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="02743-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="02743-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="02743-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="02743-148">REST response</span></span>

<span data-ttu-id="02743-149">Ha ez sikeres, ez a metódus a válasz törzsében a frissített [profil](profile-resources.md) erőforrás-tulajdonságokat adja vissza.</span><span class="sxs-lookup"><span data-stu-id="02743-149">If successful, this method returns updated [Profile](profile-resources.md) resource properties in the response body.</span></span> <span data-ttu-id="02743-150">Ehhez a híváshoz ETag szükséges a Egyidejűség észleléséhez.</span><span class="sxs-lookup"><span data-stu-id="02743-150">This call requires an ETag for concurrency detection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="02743-151">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="02743-151">Response success and error codes</span></span>

<span data-ttu-id="02743-152">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="02743-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="02743-153">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="02743-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="02743-154">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="02743-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="02743-155">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="02743-155">Response example</span></span>

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
