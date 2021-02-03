---
title: Egy ügyfél vállalati profiljának lekérése
description: Lekéri egy ügyfél vállalati profilját.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: c26a86ecb96e5e7942ba179f8a3cc704abab7df5
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768123"
---
# <a name="get-a-customers-company-profile"></a><span data-ttu-id="60406-103">Egy ügyfél vállalati profiljának lekérése</span><span class="sxs-lookup"><span data-stu-id="60406-103">Get a customer's company profile</span></span>

<span data-ttu-id="60406-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="60406-104">**Applies To**</span></span>

- <span data-ttu-id="60406-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="60406-105">Partner Center</span></span>
- <span data-ttu-id="60406-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="60406-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="60406-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="60406-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="60406-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="60406-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="60406-109">Lekéri egy ügyfél vállalati profilját.</span><span class="sxs-lookup"><span data-stu-id="60406-109">Gets the company profile of a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60406-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="60406-110">Prerequisites</span></span>

- <span data-ttu-id="60406-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="60406-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="60406-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="60406-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="60406-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="60406-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="60406-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="60406-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="60406-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="60406-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="60406-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="60406-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="60406-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="60406-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="60406-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="60406-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="60406-119">C\#</span><span class="sxs-lookup"><span data-stu-id="60406-119">C\#</span></span>

<span data-ttu-id="60406-120">Az ügyfél vállalati profiljának lekéréséhez hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="60406-120">To get the company profile for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="60406-121">Ezután szerezze be az ügyfél [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) felületét a [**profilok**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) tulajdonságból a vállalati tulajdonság eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="60406-121">Then get the customer's [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) interface from the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, in order to access its Company property.</span></span> <span data-ttu-id="60406-122">Ezután szerezze be a [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) felületet a [**ICustomerProfileCollection. Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) tulajdonságból, és hívja meg a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="60406-122">Next, get the [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) interface from the [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) property, and call its [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

<span data-ttu-id="60406-123">**Minta**: [töltse le a partner Center SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681)-t.</span><span class="sxs-lookup"><span data-stu-id="60406-123">**Sample**: [Download the Partner Center SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span></span> <span data-ttu-id="60406-124">**Projekt**: PartnerSdk. FeatureSamples **osztály**: GetCustomerCompanyProfile.cs</span><span class="sxs-lookup"><span data-stu-id="60406-124">**Project**: PartnerSdk.FeatureSamples **Class**: GetCustomerCompanyProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="60406-125">Java</span><span class="sxs-lookup"><span data-stu-id="60406-125">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="60406-126">Az ügyfél vállalati profiljának lekéréséhez hívja meg a **IAggregatePartner. getCustomers (). byId** függvényt az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="60406-126">To get the company profile for a customer, call the **IAggregatePartner.getCustomers().byId** function with the customer identifier to identify the customer.</span></span> <span data-ttu-id="60406-127">Ezután szerezze be az ügyfél **ICustomerProfileCollection** felületét a [**getProfiles**] függvényből a vállalati tulajdonság eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="60406-127">Then get the customer's **ICustomerProfileCollection** interface from the [**getProfiles**] function, in order to access its Company property.</span></span> <span data-ttu-id="60406-128">Ezután szerezze be a **ICustomerReadonlyProfile** felületet a **ICustomerProfileCollection. getCompany** függvényből, és hívja meg a **Get** függvényt.</span><span class="sxs-lookup"><span data-stu-id="60406-128">Next, get the **ICustomerReadonlyProfile** interface from the **ICustomerProfileCollection.getCompany** function, and call the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <a name="rest-request"></a><span data-ttu-id="60406-129">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="60406-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="60406-130">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="60406-130">Request syntax</span></span>

| <span data-ttu-id="60406-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="60406-131">Method</span></span>  | <span data-ttu-id="60406-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="60406-132">Request URI</span></span>                                                             |
|---------|-------------------------------------------------------------------------|
| <span data-ttu-id="60406-133">**GET**</span><span class="sxs-lookup"><span data-stu-id="60406-133">**GET**</span></span> | <span data-ttu-id="60406-134">*{baseURL}*/v1/Customers/{Customer-Tenant-ID}/Profiles/Company http/1.1</span><span class="sxs-lookup"><span data-stu-id="60406-134">*{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="60406-135">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="60406-135">URI parameter</span></span>

<span data-ttu-id="60406-136">A vállalati profil beszerzéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="60406-136">Use the following query parameter to get the company profile.</span></span>

| <span data-ttu-id="60406-137">Név</span><span class="sxs-lookup"><span data-stu-id="60406-137">Name</span></span>                   | <span data-ttu-id="60406-138">Típus</span><span class="sxs-lookup"><span data-stu-id="60406-138">Type</span></span>     | <span data-ttu-id="60406-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="60406-139">Required</span></span> | <span data-ttu-id="60406-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="60406-140">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="60406-141">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="60406-141">**customer-tenant-id**</span></span> | <span data-ttu-id="60406-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="60406-142">**guid**</span></span> | <span data-ttu-id="60406-143">Y</span><span class="sxs-lookup"><span data-stu-id="60406-143">Y</span></span>        | <span data-ttu-id="60406-144">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="60406-144">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="60406-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="60406-145">Request headers</span></span>

<span data-ttu-id="60406-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="60406-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="60406-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="60406-147">Request body</span></span>

<span data-ttu-id="60406-148">Nincs</span><span class="sxs-lookup"><span data-stu-id="60406-148">None</span></span>

### <a name="request-example"></a><span data-ttu-id="60406-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="60406-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="60406-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="60406-150">REST response</span></span>

<span data-ttu-id="60406-151">Ha ez sikeres, a metódus a válasz törzsében adja vissza az adatokat.</span><span class="sxs-lookup"><span data-stu-id="60406-151">If successful, this method returns information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="60406-152">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="60406-152">Response success and error codes</span></span>

<span data-ttu-id="60406-153">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="60406-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="60406-154">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="60406-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="60406-155">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="60406-155">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="60406-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="60406-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 488
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CV: /e74N8OrkE29ycwZ.0
MS-ServerId: 101112202
Date: Wed, 04 Jan 2017 19:48:51 GMT

{
    "tenantId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "domain": "dtdemocspcustomer005.onmicrosoft.com",
    "companyName": "DT Demo CSP Customer 005",
    "address": {
        "country": "US",
        "region": "WA",
        "city": "Redmond ",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "phoneNumber": "4155551212"
    },
    "email": "daniel@hotmail.com.tw",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerCompanyProfile"
    }
}
```
