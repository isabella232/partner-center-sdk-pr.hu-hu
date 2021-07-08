---
title: Egy ügyfél számlázási profiljának lekérése
description: Lekérte egy ügyfél számlázási profilját. Az Partnerközpont irányítópulton ezt a műveletet az ügyfél kiválasztásával hajthatja végre.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d22be53a5be4efcda76a568578468615495febb6
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760589"
---
# <a name="get-a-customers-billing-profile"></a><span data-ttu-id="40ccc-104">Egy ügyfél számlázási profiljának lekérése</span><span class="sxs-lookup"><span data-stu-id="40ccc-104">Get a customer's billing profile</span></span>

<span data-ttu-id="40ccc-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="40ccc-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="40ccc-106">Lekérte egy ügyfél számlázási profilját.</span><span class="sxs-lookup"><span data-stu-id="40ccc-106">Gets the billing profile of a customer.</span></span>

<span data-ttu-id="40ccc-107">A Partnerközpont a művelet végrehajtásához először ki kell [választania egy ügyfelet.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="40ccc-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="40ccc-108">Ezután a bal oldali oldalsávon az ügyfél neve alatt válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="40ccc-108">Then, under the customer's name in the left sidebar, select **Account**.</span></span> <span data-ttu-id="40ccc-109">A számlázási profil a Számlázási adatok fejléc alatt **található.**</span><span class="sxs-lookup"><span data-stu-id="40ccc-109">The billing profile can be found under the **Bill-to info** heading.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40ccc-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="40ccc-110">Prerequisites</span></span>

- <span data-ttu-id="40ccc-111">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="40ccc-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="40ccc-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="40ccc-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="40ccc-113">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="40ccc-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="40ccc-114">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="40ccc-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="40ccc-115">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="40ccc-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="40ccc-116">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="40ccc-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="40ccc-117">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="40ccc-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="40ccc-118">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="40ccc-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="40ccc-119">C\#</span><span class="sxs-lookup"><span data-stu-id="40ccc-119">C\#</span></span>

<span data-ttu-id="40ccc-120">Az ügyfél számlázási profiljának lehívásához használja [**az IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="40ccc-120">To get a customer's billing profile, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="40ccc-121">Ezután hívja meg [**a Profiles (Profilok)**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) tulajdonságot, majd a [**Billing (Számlázás)**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="40ccc-121">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="40ccc-122">Végül hívja meg a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync)</span><span class="sxs-lookup"><span data-stu-id="40ccc-122">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

<span data-ttu-id="40ccc-123">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="40ccc-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="40ccc-124">**Project:** PartnerSDK.FeatureSamples **osztály:** GetCustomerBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="40ccc-124">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="40ccc-125">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="40ccc-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="40ccc-126">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="40ccc-126">Request syntax</span></span>

| <span data-ttu-id="40ccc-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="40ccc-127">Method</span></span>  | <span data-ttu-id="40ccc-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="40ccc-128">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="40ccc-129">**Kap**</span><span class="sxs-lookup"><span data-stu-id="40ccc-129">**GET**</span></span> | <span data-ttu-id="40ccc-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="40ccc-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="40ccc-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="40ccc-131">URI parameter</span></span>

<span data-ttu-id="40ccc-132">A számlázási profil lekérdezhető a következő lekérdezési paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="40ccc-132">Use the following query parameter to get the billing profile.</span></span>

| <span data-ttu-id="40ccc-133">Név</span><span class="sxs-lookup"><span data-stu-id="40ccc-133">Name</span></span>                   | <span data-ttu-id="40ccc-134">Típus</span><span class="sxs-lookup"><span data-stu-id="40ccc-134">Type</span></span>     | <span data-ttu-id="40ccc-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="40ccc-135">Required</span></span> | <span data-ttu-id="40ccc-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="40ccc-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="40ccc-137">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="40ccc-137">**customer-tenant-id**</span></span> | <span data-ttu-id="40ccc-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="40ccc-138">**guid**</span></span> | <span data-ttu-id="40ccc-139">Y</span><span class="sxs-lookup"><span data-stu-id="40ccc-139">Y</span></span>        | <span data-ttu-id="40ccc-140">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="40ccc-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="40ccc-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="40ccc-141">Request headers</span></span>

<span data-ttu-id="40ccc-142">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="40ccc-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="40ccc-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="40ccc-143">Request body</span></span>

<span data-ttu-id="40ccc-144">None</span><span class="sxs-lookup"><span data-stu-id="40ccc-144">None</span></span>

### <a name="request-example"></a><span data-ttu-id="40ccc-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="40ccc-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a><span data-ttu-id="40ccc-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="40ccc-146">REST response</span></span>

<span data-ttu-id="40ccc-147">Ha ez a módszer sikeres, a válasz törzsében [profilerőforrások](profile-resources.md) gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="40ccc-147">If successful, this method returns a collection of [Profile](profile-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="40ccc-148">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="40ccc-148">Response success and error codes</span></span>

<span data-ttu-id="40ccc-149">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="40ccc-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="40ccc-150">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="40ccc-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="40ccc-151">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="40ccc-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="40ccc-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="40ccc-152">Response example</span></span>

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
