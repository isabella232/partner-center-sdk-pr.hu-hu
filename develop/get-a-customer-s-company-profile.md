---
title: Egy ügyfél vállalati profiljának lekérése
description: Lekérte egy ügyfél céges profilját.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: a1c0c8401207f4b0bb33755a8eabc66de0ad9ff9
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874975"
---
# <a name="get-a-customers-company-profile"></a><span data-ttu-id="2b159-103">Egy ügyfél vállalati profiljának lekérése</span><span class="sxs-lookup"><span data-stu-id="2b159-103">Get a customer's company profile</span></span>

<span data-ttu-id="2b159-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2b159-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2b159-105">Lekérte egy ügyfél céges profilját.</span><span class="sxs-lookup"><span data-stu-id="2b159-105">Gets the company profile of a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b159-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2b159-106">Prerequisites</span></span>

- <span data-ttu-id="2b159-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2b159-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2b159-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="2b159-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2b159-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2b159-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2b159-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="2b159-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2b159-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="2b159-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2b159-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="2b159-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2b159-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="2b159-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2b159-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2b159-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2b159-115">C\#</span><span class="sxs-lookup"><span data-stu-id="2b159-115">C\#</span></span>

<span data-ttu-id="2b159-116">Az ügyfél céges profiljának lehíváshoz hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="2b159-116">To get the company profile for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="2b159-117">Ezután szerezze be az ügyfél [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) felületét a [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) (Profilok) tulajdonságból a Vállalati tulajdonság eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="2b159-117">Then get the customer's [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) interface from the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, in order to access its Company property.</span></span> <span data-ttu-id="2b159-118">Ezután szerezze be az [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) felületet az [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) tulajdonságból, és hívja meg a [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) vagy [**GetAsync() metódusokat.**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync)</span><span class="sxs-lookup"><span data-stu-id="2b159-118">Next, get the [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) interface from the [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) property, and call its [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

<span data-ttu-id="2b159-119">**Minta:** [Töltse le a Partnerközpont SDK.](https://go.microsoft.com/fwlink/p/?LinkId=746681)</span><span class="sxs-lookup"><span data-stu-id="2b159-119">**Sample**: [Download the Partner Center SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span></span> <span data-ttu-id="2b159-120">**Project:** PartnerSdk.FeatureSamples **osztály:** GetCustomerCompanyProfile.cs</span><span class="sxs-lookup"><span data-stu-id="2b159-120">**Project**: PartnerSdk.FeatureSamples **Class**: GetCustomerCompanyProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="2b159-121">Java</span><span class="sxs-lookup"><span data-stu-id="2b159-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="2b159-122">Az ügyfél céges profiljának lehíváshoz hívja meg az **IAggregatePartner.getCustomers().byId** függvényt az ügyfél azonosítóját az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="2b159-122">To get the company profile for a customer, call the **IAggregatePartner.getCustomers().byId** function with the customer identifier to identify the customer.</span></span> <span data-ttu-id="2b159-123">Ezután szerezze be az ügyfél **ICustomerProfileCollection** felületét a [**getProfiles**] függvényből a Vállalati tulajdonság eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="2b159-123">Then get the customer's **ICustomerProfileCollection** interface from the [**getProfiles**] function, in order to access its Company property.</span></span> <span data-ttu-id="2b159-124">Ezután szerezze be az **ICustomerReadonlyProfile** felületet az **ICustomerProfileCollection.getCompany függvényből,** és hívja meg a **get** függvényt.</span><span class="sxs-lookup"><span data-stu-id="2b159-124">Next, get the **ICustomerReadonlyProfile** interface from the **ICustomerProfileCollection.getCompany** function, and call the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <a name="rest-request"></a><span data-ttu-id="2b159-125">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="2b159-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2b159-126">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="2b159-126">Request syntax</span></span>

| <span data-ttu-id="2b159-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="2b159-127">Method</span></span>  | <span data-ttu-id="2b159-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2b159-128">Request URI</span></span>                                                             |
|---------|-------------------------------------------------------------------------|
| <span data-ttu-id="2b159-129">**Kap**</span><span class="sxs-lookup"><span data-stu-id="2b159-129">**GET**</span></span> | <span data-ttu-id="2b159-130">*{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2b159-130">*{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2b159-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="2b159-131">URI parameter</span></span>

<span data-ttu-id="2b159-132">A következő lekérdezési paraméterrel lekérdezheti a vállalati profilt.</span><span class="sxs-lookup"><span data-stu-id="2b159-132">Use the following query parameter to get the company profile.</span></span>

| <span data-ttu-id="2b159-133">Név</span><span class="sxs-lookup"><span data-stu-id="2b159-133">Name</span></span>                   | <span data-ttu-id="2b159-134">Típus</span><span class="sxs-lookup"><span data-stu-id="2b159-134">Type</span></span>     | <span data-ttu-id="2b159-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2b159-135">Required</span></span> | <span data-ttu-id="2b159-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="2b159-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2b159-137">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="2b159-137">**customer-tenant-id**</span></span> | <span data-ttu-id="2b159-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="2b159-138">**guid**</span></span> | <span data-ttu-id="2b159-139">Y</span><span class="sxs-lookup"><span data-stu-id="2b159-139">Y</span></span>        | <span data-ttu-id="2b159-140">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="2b159-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2b159-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2b159-141">Request headers</span></span>

<span data-ttu-id="2b159-142">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2b159-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2b159-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2b159-143">Request body</span></span>

<span data-ttu-id="2b159-144">None</span><span class="sxs-lookup"><span data-stu-id="2b159-144">None</span></span>

### <a name="request-example"></a><span data-ttu-id="2b159-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="2b159-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2b159-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2b159-146">REST response</span></span>

<span data-ttu-id="2b159-147">Ha ez a metódus sikeres, a válasz törzsében található információkat adja vissza.</span><span class="sxs-lookup"><span data-stu-id="2b159-147">If successful, this method returns information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2b159-148">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2b159-148">Response success and error codes</span></span>

<span data-ttu-id="2b159-149">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="2b159-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2b159-150">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="2b159-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2b159-151">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2b159-151">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2b159-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2b159-152">Response example</span></span>

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
