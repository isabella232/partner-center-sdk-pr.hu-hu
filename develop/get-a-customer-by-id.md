---
title: Egy ügyfél lekérése azonosító alapján
description: Beolvas egy ügyfél-AZONOSÍTÓnak megfelelő ügyfél-erőforrást.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: dd4301dbb6f749b675fe624daf7f63751806f856
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768127"
---
# <a name="get-a-customer-by-id"></a><span data-ttu-id="f7237-103">Egy ügyfél lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="f7237-103">Get a customer by ID</span></span>

<span data-ttu-id="f7237-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="f7237-104">**Applies To**</span></span>

- <span data-ttu-id="f7237-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f7237-105">Partner Center</span></span>
- <span data-ttu-id="f7237-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="f7237-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f7237-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f7237-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f7237-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f7237-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f7237-109">Beolvas egy ügyfél-AZONOSÍTÓnak megfelelő **ügyfél** -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="f7237-109">Gets a **Customer** resource that corresponds to a customer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7237-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f7237-110">Prerequisites</span></span>

- <span data-ttu-id="f7237-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="f7237-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f7237-112">Ez a forgatókönyv támogatja az App + felhasználói hitelesítő adatokat vagy csak az alkalmazáson belüli hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="f7237-112">This scenario supports app+user credentials or app-only authentication.</span></span>

- <span data-ttu-id="f7237-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f7237-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f7237-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="f7237-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f7237-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="f7237-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f7237-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="f7237-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f7237-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="f7237-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f7237-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f7237-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="f7237-119">C\#</span><span class="sxs-lookup"><span data-stu-id="f7237-119">C\#</span></span>

<span data-ttu-id="f7237-120">Az ügyfél azonosító alapján történő beszerzéséhez használja a [**IAggregatePartner. Customs**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, hívja meg a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust, majd hívja meg a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="f7237-120">To get a customer by ID, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, then call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

Customer customerInfo = partnerOperations.Customers.ById(customerIdToRetrieve).Get();
```

<span data-ttu-id="f7237-121">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f7237-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f7237-122">**Projekt**: PartnerSDK. FeatureSamples **osztály**: CustomerInformation.cs</span><span class="sxs-lookup"><span data-stu-id="f7237-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerInformation.cs</span></span>

## <a name="java"></a><span data-ttu-id="f7237-123">Java</span><span class="sxs-lookup"><span data-stu-id="f7237-123">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="f7237-124">Az ügyfél azonosító alapján történő beszerzéséhez használja a **IAggregatePartner. getCustomers** függvényt, hívja meg a **byId ()** függvényt, majd hívja meg a **Get ()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="f7237-124">To get a customer by ID, use your **IAggregatePartner.getCustomers** function, call the **byId()** function, then call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerIdToRetrieve;

Customer customerInfo = partnerOperations.getCustomers().byId(customerIdToRetrieve).get();
```

## <a name="powershell"></a><span data-ttu-id="f7237-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7237-125">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="f7237-126">Az ügyfél azonosító alapján történő beszerzéséhez hajtsa végre a [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) parancsot, és határozza meg a **Vevőkód** paramétert.</span><span class="sxs-lookup"><span data-stu-id="f7237-126">To get a customer by ID, execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command and specify the **CustomerId** parameter.</span></span>

```powershell
Get-PartnerCustomer -CustomerId '2ca7de6c-c05c-46b5-b689-32e53573a97a'
```

## <a name="rest-request"></a><span data-ttu-id="f7237-127">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="f7237-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f7237-128">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f7237-128">Request syntax</span></span>

| <span data-ttu-id="f7237-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="f7237-129">Method</span></span>  | <span data-ttu-id="f7237-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f7237-130">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="f7237-131">**GET**</span><span class="sxs-lookup"><span data-stu-id="f7237-131">**GET**</span></span> | <span data-ttu-id="f7237-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f7237-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f7237-133">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="f7237-133">URI parameter</span></span>

<span data-ttu-id="f7237-134">Használja az alábbi lekérdezési paramétert egy adott ügyfélhez.</span><span class="sxs-lookup"><span data-stu-id="f7237-134">Use the following query parameter to a specific customer.</span></span>

| <span data-ttu-id="f7237-135">Név</span><span class="sxs-lookup"><span data-stu-id="f7237-135">Name</span></span>                   | <span data-ttu-id="f7237-136">Típus</span><span class="sxs-lookup"><span data-stu-id="f7237-136">Type</span></span>     | <span data-ttu-id="f7237-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f7237-137">Required</span></span> | <span data-ttu-id="f7237-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="f7237-138">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f7237-139">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="f7237-139">**customer-tenant-id**</span></span> | <span data-ttu-id="f7237-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="f7237-140">**guid**</span></span> | <span data-ttu-id="f7237-141">Y</span><span class="sxs-lookup"><span data-stu-id="f7237-141">Y</span></span>        | <span data-ttu-id="f7237-142">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="f7237-142">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f7237-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f7237-143">Request headers</span></span>

<span data-ttu-id="f7237-144">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f7237-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f7237-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f7237-145">Request body</span></span>

<span data-ttu-id="f7237-146">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="f7237-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f7237-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f7237-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b
```

## <a name="rest-response"></a><span data-ttu-id="f7237-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f7237-148">REST response</span></span>

<span data-ttu-id="f7237-149">Ha ez sikeres, ez a metódus egy [ügyfél](customer-resources.md#customer) -erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="f7237-149">If successful, this method returns a [Customer](customer-resources.md#customer) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f7237-150">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f7237-150">Response success and error codes</span></span>

<span data-ttu-id="f7237-151">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="f7237-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f7237-152">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="f7237-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f7237-153">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f7237-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f7237-154">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f7237-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1530
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b

{
  "id": "eebd1b55-5360-4438-a11d-5c06918c3014",
  "commerceId": "99e6a635-48e7-424d-9059-c9db944e3c54",
  "companyProfile": {
    "tenantId": "eebd1b55-5360-4438-a11d-5c06918c3014",
    "domain": "abcdefgh1234.ccsctp.net",
    "companyName": "1kl as kjk",
    "address": {
      "country": "US",
      "region": "wa",
      "city": "redmond",
      "addressLine1": "1 ms way",
      "postalCode": "98052",
      "phoneNumber": "1234567890"
    },
    "email": "a@a.com",
    "links": {
      "self": {
        "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/profiles/company",
        "method": "GET",
        "headers": []
      }
    },
    "attributes": {
      "objectType": "CustomerCompanyProfile"
    }
  },
  "billingProfile": {
    "id": "eeada110-69d6-4cc9-b093-75feb7ca9d3f",
    "firstName": "d0d89d776d03471c819bf772191ed728",
    "lastName": "kjkAJJAAAAAAAAAAAAAAAAAAAA",
    "email": "a@a.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "1kl as kjkAAAAAAAAAAAAAAAJJJJJJJJJJJAAAAAJJJJJJJJJJJAAJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJAJJJJJAJJAAAAJAJJAAAAAAAAAAAAAAAAAAAA",
    "defaultAddress": {
      "country": "US",
      "city": "redmond",
      "state": "WA",
      "addressLine1": "1 ms way",
      "postalCode": "98052",
      "firstName": "1kl as",
      "lastName": "kjk",
      "phoneNumber": "1234567890"
    },
    "links": {
      "self": {
        "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/profiles/billing",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "etag": "-4242348048554929329",
      "objectType": "CustomerBillingProfile"
    }
  },
  "relationshipToPartner": "reseller",
  "allowDelegatedAccess": true,
  "customDomains": [
    "abcdefgh1234.ccsctp.net"
  ],
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Customer"
  }
}
```
