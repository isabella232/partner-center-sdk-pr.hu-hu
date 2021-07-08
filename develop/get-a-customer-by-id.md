---
title: Egy ügyfél lekérése azonosító alapján
description: Lekért egy ügyfél-erőforrást, amely megfelel egy ügyfél-azonosítónak.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 196d653c789c4b4e1327f0c6e5d2531a18681a71
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874992"
---
# <a name="get-a-customer-by-id"></a><span data-ttu-id="d04a7-103">Egy ügyfél lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="d04a7-103">Get a customer by ID</span></span>

<span data-ttu-id="d04a7-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d04a7-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d04a7-105">Lekért egy ügyfél-erőforrást, amely megfelel egy ügyfél-azonosítónak. </span><span class="sxs-lookup"><span data-stu-id="d04a7-105">Gets a **Customer** resource that corresponds to a customer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d04a7-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d04a7-106">Prerequisites</span></span>

- <span data-ttu-id="d04a7-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d04a7-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d04a7-108">Ez a forgatókönyv támogatja az alkalmazás+felhasználói hitelesítő adatokat vagy a csak az alkalmazásra vonatkozó hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="d04a7-108">This scenario supports app+user credentials or app-only authentication.</span></span>

- <span data-ttu-id="d04a7-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d04a7-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d04a7-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d04a7-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d04a7-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d04a7-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d04a7-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d04a7-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d04a7-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="d04a7-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d04a7-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d04a7-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="d04a7-115">C\#</span><span class="sxs-lookup"><span data-stu-id="d04a7-115">C\#</span></span>

<span data-ttu-id="d04a7-116">Ha azonosító alapján szeretnék lehívni az ügyfelet, használja az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, hívja meg a [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust, majd hívja meg a [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) vagy [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync)</span><span class="sxs-lookup"><span data-stu-id="d04a7-116">To get a customer by ID, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, then call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

Customer customerInfo = partnerOperations.Customers.ById(customerIdToRetrieve).Get();
```

<span data-ttu-id="d04a7-117">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d04a7-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d04a7-118">**Project:** PartnerSDK.FeatureSamples **osztály:** CustomerInformation.cs</span><span class="sxs-lookup"><span data-stu-id="d04a7-118">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerInformation.cs</span></span>

## <a name="java"></a><span data-ttu-id="d04a7-119">Java</span><span class="sxs-lookup"><span data-stu-id="d04a7-119">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="d04a7-120">Az ügyfél azonosító alapján való lehíváshoz használja az **IAggregatePartner.getCustomers** függvényt, hívja meg a **byId()** függvényt, majd hívja meg a **get()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="d04a7-120">To get a customer by ID, use your **IAggregatePartner.getCustomers** function, call the **byId()** function, then call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerIdToRetrieve;

Customer customerInfo = partnerOperations.getCustomers().byId(customerIdToRetrieve).get();
```

## <a name="powershell"></a><span data-ttu-id="d04a7-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d04a7-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="d04a7-122">Ha azonosító alapján kell lekérte az ügyfelet, hajtsa végre a [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) parancsot, és adja meg a **CustomerId paramétert.**</span><span class="sxs-lookup"><span data-stu-id="d04a7-122">To get a customer by ID, execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command and specify the **CustomerId** parameter.</span></span>

```powershell
Get-PartnerCustomer -CustomerId '2ca7de6c-c05c-46b5-b689-32e53573a97a'
```

## <a name="rest-request"></a><span data-ttu-id="d04a7-123">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d04a7-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d04a7-124">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="d04a7-124">Request syntax</span></span>

| <span data-ttu-id="d04a7-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="d04a7-125">Method</span></span>  | <span data-ttu-id="d04a7-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d04a7-126">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="d04a7-127">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d04a7-127">**GET**</span></span> | <span data-ttu-id="d04a7-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d04a7-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d04a7-129">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d04a7-129">URI parameter</span></span>

<span data-ttu-id="d04a7-130">Használja az alábbi lekérdezési paramétert egy adott ügyfélhez.</span><span class="sxs-lookup"><span data-stu-id="d04a7-130">Use the following query parameter to a specific customer.</span></span>

| <span data-ttu-id="d04a7-131">Név</span><span class="sxs-lookup"><span data-stu-id="d04a7-131">Name</span></span>                   | <span data-ttu-id="d04a7-132">Típus</span><span class="sxs-lookup"><span data-stu-id="d04a7-132">Type</span></span>     | <span data-ttu-id="d04a7-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d04a7-133">Required</span></span> | <span data-ttu-id="d04a7-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="d04a7-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d04a7-135">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="d04a7-135">**customer-tenant-id**</span></span> | <span data-ttu-id="d04a7-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="d04a7-136">**guid**</span></span> | <span data-ttu-id="d04a7-137">Y</span><span class="sxs-lookup"><span data-stu-id="d04a7-137">Y</span></span>        | <span data-ttu-id="d04a7-138">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="d04a7-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d04a7-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d04a7-139">Request headers</span></span>

<span data-ttu-id="d04a7-140">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d04a7-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d04a7-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d04a7-141">Request body</span></span>

<span data-ttu-id="d04a7-142">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d04a7-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d04a7-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d04a7-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b
```

## <a name="rest-response"></a><span data-ttu-id="d04a7-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d04a7-144">REST response</span></span>

<span data-ttu-id="d04a7-145">Ha sikeres, ez a metódus egy [Customer erőforrást](customer-resources.md#customer) ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="d04a7-145">If successful, this method returns a [Customer](customer-resources.md#customer) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d04a7-146">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d04a7-146">Response success and error codes</span></span>

<span data-ttu-id="d04a7-147">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d04a7-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d04a7-148">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d04a7-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d04a7-149">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d04a7-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d04a7-150">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d04a7-150">Response example</span></span>

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
