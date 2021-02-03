---
title: Egy ügyfél felhasználói jelszavának alaphelyzetbe állítása
description: A jelszó alaphelyzetbe állítása nagyon hasonló ahhoz, hogy az ügyfél egy meglévő felhasználói fiókjában további adatokat frissítsen.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e0df93c2db55ec0fe49fc0e3089b7e11928f32bb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767791"
---
# <a name="reset-user-password-for-a-customer"></a><span data-ttu-id="9c175-103">Egy ügyfél felhasználói jelszavának alaphelyzetbe állítása</span><span class="sxs-lookup"><span data-stu-id="9c175-103">Reset user password for a customer</span></span>

<span data-ttu-id="9c175-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="9c175-104">**Applies To**</span></span>

- <span data-ttu-id="9c175-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="9c175-105">Partner Center</span></span>

<span data-ttu-id="9c175-106">A jelszó alaphelyzetbe állítása nagyon hasonló ahhoz, hogy az ügyfél egy meglévő felhasználói fiókjában további adatokat frissítsen.</span><span class="sxs-lookup"><span data-stu-id="9c175-106">Resetting a password is very similar to updating other details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c175-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="9c175-107">Prerequisites</span></span>

- <span data-ttu-id="9c175-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="9c175-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9c175-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="9c175-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9c175-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9c175-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9c175-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="9c175-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9c175-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="9c175-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9c175-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="9c175-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9c175-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="9c175-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9c175-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9c175-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9c175-116">C\#</span><span class="sxs-lookup"><span data-stu-id="9c175-116">C\#</span></span>

<span data-ttu-id="9c175-117">Egy adott ügyfél felhasználó jelszavának alaphelyzetbe állításához először kérje le a megadott ügyfél-azonosítót és a megcélozott felhasználót.</span><span class="sxs-lookup"><span data-stu-id="9c175-117">To reset a password for a specified customer user, first retrieve the specified customer ID and the targeted user.</span></span> <span data-ttu-id="9c175-118">Ezután hozzon létre egy új **CustomerUser** -objektumot, amely tartalmazza a meglévő ügyfél adatait, de egy új **PasswordProfile** objektummal.</span><span class="sxs-lookup"><span data-stu-id="9c175-118">Then, create a new **CustomerUser** object that contains the information for the existing customer, but with a new **PasswordProfile** object.</span></span> <span data-ttu-id="9c175-119">Ezután használja a **IAggregatePartner. Customers** gyűjteményt, és hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="9c175-119">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="9c175-120">Ezután hívja meg a **Users (felhasználók** ) tulajdonságot, a **ById ()** metódust, majd a **patch** metódust.</span><span class="sxs-lookup"><span data-stu-id="9c175-120">Then call the **Users** property, the **ById()** method, and then the **Patch** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// CustomerUser specifiedUser;

var selectedCustomer = partnerOperations.Customers.ById(selectedCustomerId).Get();
var userToUpdate = new CustomerUser()
   {
      PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "newPassword" },
      DisplayName = "Roger Federer",
      FirstName = "Roger",
      LastName = "Federer",
      UsageLocation = "US",
      UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
   };

// update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

<span data-ttu-id="9c175-121">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9c175-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9c175-122">**Projekt**: PartnerSDK. FeatureSamples **osztály**: CustomerUserUpdate.cs</span><span class="sxs-lookup"><span data-stu-id="9c175-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9c175-123">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="9c175-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9c175-124">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="9c175-124">Request syntax</span></span>

| <span data-ttu-id="9c175-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="9c175-125">Method</span></span>    | <span data-ttu-id="9c175-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="9c175-126">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="9c175-127">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="9c175-127">**PATCH**</span></span> | <span data-ttu-id="9c175-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users http/1.1</span><span class="sxs-lookup"><span data-stu-id="9c175-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9c175-129">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="9c175-129">URI parameter</span></span>

<span data-ttu-id="9c175-130">A megfelelő ügyfél azonosításához használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="9c175-130">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="9c175-131">Név</span><span class="sxs-lookup"><span data-stu-id="9c175-131">Name</span></span>                   | <span data-ttu-id="9c175-132">Típus</span><span class="sxs-lookup"><span data-stu-id="9c175-132">Type</span></span>     | <span data-ttu-id="9c175-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="9c175-133">Required</span></span> | <span data-ttu-id="9c175-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="9c175-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9c175-135">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="9c175-135">**customer-tenant-id**</span></span> | <span data-ttu-id="9c175-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="9c175-136">**guid**</span></span> | <span data-ttu-id="9c175-137">Y</span><span class="sxs-lookup"><span data-stu-id="9c175-137">Y</span></span>        | <span data-ttu-id="9c175-138">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="9c175-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="9c175-139">**felhasználói azonosító**</span><span class="sxs-lookup"><span data-stu-id="9c175-139">**user-id**</span></span>            | <span data-ttu-id="9c175-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="9c175-140">**guid**</span></span> | <span data-ttu-id="9c175-141">Y</span><span class="sxs-lookup"><span data-stu-id="9c175-141">Y</span></span>        | <span data-ttu-id="9c175-142">Az érték egy olyan GUID formátumú **felhasználói azonosító** , amely egyetlen felhasználói fiókhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="9c175-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="9c175-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="9c175-143">Request headers</span></span>

<span data-ttu-id="9c175-144">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9c175-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9c175-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="9c175-145">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="9c175-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="9c175-146">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
     "passwordProfile":{
        password: "Renew456*",
        forceChangePassword: true
      },

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="9c175-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="9c175-147">REST response</span></span>

<span data-ttu-id="9c175-148">Ha ez sikeres, ez a módszer a felhasználói adatokat adja vissza, valamint a frissített jelszavas információkat.</span><span class="sxs-lookup"><span data-stu-id="9c175-148">If successful, this method returns the user information, along with the updated password information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9c175-149">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="9c175-149">Response success and error codes</span></span>

<span data-ttu-id="9c175-150">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="9c175-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9c175-151">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="9c175-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9c175-152">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9c175-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9c175-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="9c175-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "AX",
  "id": "95794928-9abe-4548-8b43-50ffc20b9404",
  "userPrincipalName": "aaaa4@abcdefgh1234.ccsctp.net",
  "firstName": "aaaa4",
  "lastName": "aaaa4",
  "displayName": "aaaa4",
  "passwordProfile": {
    "forceChangePassword": false,
    "password": "Renew456*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/95794928-9abe-4548-8b43-50ffc20b9404",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```
