---
title: Egy ügyfél számlázási profiljának lekérése
description: Lekéri az ügyfél számlázási profilját. A partner Center irányítópultján ezt a műveletet a felhasználó kiválasztásával végezheti el.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 6c837c1c220e334df82e75eb680b6012862c9686
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768363"
---
# <a name="get-a-customers-billing-profile"></a><span data-ttu-id="b3034-103">Egy ügyfél számlázási profiljának lekérése</span><span class="sxs-lookup"><span data-stu-id="b3034-103">Get a customer's billing profile</span></span>

<span data-ttu-id="b3034-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="b3034-104">**Applies To**</span></span>

- <span data-ttu-id="b3034-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="b3034-105">Partner Center</span></span>
- <span data-ttu-id="b3034-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="b3034-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b3034-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="b3034-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b3034-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="b3034-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b3034-109">Lekéri az ügyfél számlázási profilját.</span><span class="sxs-lookup"><span data-stu-id="b3034-109">Gets the billing profile of a customer.</span></span>

<span data-ttu-id="b3034-110">A partner Center irányítópultján ezt a műveletet a [felhasználó kiválasztásával](get-a-customer-by-name.md)végezheti el.</span><span class="sxs-lookup"><span data-stu-id="b3034-110">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="b3034-111">Ezután az ügyfél neve alatt a bal oldali oldalsávon válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="b3034-111">Then, under the customer's name in the left sidebar, select **Account**.</span></span> <span data-ttu-id="b3034-112">A számlázási profil a **Számlázási adatok** fejléc alatt található.</span><span class="sxs-lookup"><span data-stu-id="b3034-112">The billing profile can be found under the **Bill-to info** heading.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3034-113">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b3034-113">Prerequisites</span></span>

- <span data-ttu-id="b3034-114">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="b3034-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b3034-115">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="b3034-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b3034-116">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b3034-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b3034-117">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="b3034-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b3034-118">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="b3034-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b3034-119">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="b3034-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b3034-120">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="b3034-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b3034-121">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b3034-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b3034-122">C\#</span><span class="sxs-lookup"><span data-stu-id="b3034-122">C\#</span></span>

<span data-ttu-id="b3034-123">Az ügyfél számlázási profiljának beszerzéséhez használja a [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="b3034-123">To get a customer's billing profile, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="b3034-124">Ezután hívja meg a [**profilok**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) tulajdonságot, majd a [**Számlázási**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="b3034-124">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="b3034-125">Végül hívja meg a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="b3034-125">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

<span data-ttu-id="b3034-126">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b3034-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b3034-127">**Projekt**: PartnerSDK. FeatureSamples **osztály**: GetCustomerBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="b3034-127">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b3034-128">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="b3034-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b3034-129">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b3034-129">Request syntax</span></span>

| <span data-ttu-id="b3034-130">Metódus</span><span class="sxs-lookup"><span data-stu-id="b3034-130">Method</span></span>  | <span data-ttu-id="b3034-131">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b3034-131">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b3034-132">**GET**</span><span class="sxs-lookup"><span data-stu-id="b3034-132">**GET**</span></span> | <span data-ttu-id="b3034-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Profiles/Billing http/1.1</span><span class="sxs-lookup"><span data-stu-id="b3034-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b3034-134">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="b3034-134">URI parameter</span></span>

<span data-ttu-id="b3034-135">A számlázási profil beszerzéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="b3034-135">Use the following query parameter to get the billing profile.</span></span>

| <span data-ttu-id="b3034-136">Név</span><span class="sxs-lookup"><span data-stu-id="b3034-136">Name</span></span>                   | <span data-ttu-id="b3034-137">Típus</span><span class="sxs-lookup"><span data-stu-id="b3034-137">Type</span></span>     | <span data-ttu-id="b3034-138">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b3034-138">Required</span></span> | <span data-ttu-id="b3034-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="b3034-139">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b3034-140">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="b3034-140">**customer-tenant-id**</span></span> | <span data-ttu-id="b3034-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="b3034-141">**guid**</span></span> | <span data-ttu-id="b3034-142">Y</span><span class="sxs-lookup"><span data-stu-id="b3034-142">Y</span></span>        | <span data-ttu-id="b3034-143">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="b3034-143">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b3034-144">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b3034-144">Request headers</span></span>

<span data-ttu-id="b3034-145">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b3034-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b3034-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b3034-146">Request body</span></span>

<span data-ttu-id="b3034-147">Nincs</span><span class="sxs-lookup"><span data-stu-id="b3034-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="b3034-148">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b3034-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a><span data-ttu-id="b3034-149">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b3034-149">REST response</span></span>

<span data-ttu-id="b3034-150">Ha a művelet sikeres, ez a metódus a válasz törzsében a [profil](profile-resources.md) erőforrásainak gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="b3034-150">If successful, this method returns a collection of [Profile](profile-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b3034-151">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b3034-151">Response success and error codes</span></span>

<span data-ttu-id="b3034-152">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="b3034-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b3034-153">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="b3034-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b3034-154">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b3034-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b3034-155">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b3034-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1206
Content-Type: application/json
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
Date: Mon, 23 Nov 2015 18:13:43 GMT

{
    "id": "<billing-profile-id>",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "CompanyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
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
