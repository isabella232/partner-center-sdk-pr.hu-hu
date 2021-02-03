---
title: Előfizetés átváltása
description: Egy ügyfél előfizetésének frissítése egy adott cél előfizetésre.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b757eee8bc65c16b5c65221a4c14b6c0fd6369e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767832"
---
# <a name="transition-a-subscription"></a><span data-ttu-id="a1d0b-103">Előfizetés átváltása</span><span class="sxs-lookup"><span data-stu-id="a1d0b-103">Transition a subscription</span></span>

<span data-ttu-id="a1d0b-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="a1d0b-104">**Applies To**</span></span>

- <span data-ttu-id="a1d0b-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="a1d0b-105">Partner Center</span></span>
- <span data-ttu-id="a1d0b-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="a1d0b-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a1d0b-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="a1d0b-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a1d0b-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="a1d0b-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a1d0b-109">Egy ügyfél előfizetésének frissítése egy adott cél előfizetésre.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-109">Upgrades a customer's subscription to a specified target subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1d0b-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="a1d0b-110">Prerequisites</span></span>

- <span data-ttu-id="a1d0b-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a1d0b-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a1d0b-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a1d0b-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a1d0b-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="a1d0b-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a1d0b-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a1d0b-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a1d0b-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a1d0b-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a1d0b-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a1d0b-119">Két előfizetési azonosító, egyet a kezdeti előfizetéshez, egyet pedig a cél előfizetéshez.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-119">Two subscription IDs, one for the initial subscription and one for the target subscription.</span></span>

## <a name="c"></a><span data-ttu-id="a1d0b-120">C\#</span><span class="sxs-lookup"><span data-stu-id="a1d0b-120">C\#</span></span>

<span data-ttu-id="a1d0b-121">Az ügyfél előfizetésének frissítéséhez először [szerezze be a customer's-előfizetést](get-a-subscription-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="a1d0b-121">To upgrade a customer's subscription, first [get that's customer's subscription](get-a-subscription-by-id.md).</span></span> <span data-ttu-id="a1d0b-122">Ezután szerezze be az előfizetéshez tartozó frissítések listáját úgy, hogy meghívja a **verziófrissítések** tulajdonságot, majd a **Get ()** vagy a **GetAsync ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-122">Then, obtain a list of upgrades for that subscription by calling the **Upgrades** property followed by the **Get()** or **GetAsync()** methods.</span></span> <span data-ttu-id="a1d0b-123">Válasszon egy cél frissítést a frissítések listájáról, majd hívja meg a kezdeti előfizetés **verziófrissítések** tulajdonságát, majd a **create ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-123">Choose a target upgrade from that list of upgrades, and then call the **Upgrades** property of the initial subscription, followed by the **Create()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionIdForUpgrade;
// Upgrade targetOffer;

UpgradeResult upgradeResult = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionIdForUpgrade).Upgrades.Create(targetOffer);
```

<span data-ttu-id="a1d0b-124">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a1d0b-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a1d0b-125">**Projekt**: PartnerSDK. FeatureSamples **osztály**: UpgradeSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="a1d0b-125">**Project**: PartnerSDK.FeatureSamples **Class**: UpgradeSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a1d0b-126">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="a1d0b-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a1d0b-127">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="a1d0b-127">Request syntax</span></span>

| <span data-ttu-id="a1d0b-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="a1d0b-128">Method</span></span>   | <span data-ttu-id="a1d0b-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="a1d0b-129">Request URI</span></span>                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a1d0b-130">**GET**</span><span class="sxs-lookup"><span data-stu-id="a1d0b-130">**GET**</span></span>  | <span data-ttu-id="a1d0b-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription}/Upgrades http/1.1</span><span class="sxs-lookup"><span data-stu-id="a1d0b-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1</span></span> |
| <span data-ttu-id="a1d0b-132">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="a1d0b-132">**POST**</span></span> | <span data-ttu-id="a1d0b-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Target}/Upgrades http/1.1</span><span class="sxs-lookup"><span data-stu-id="a1d0b-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1</span></span>       |

### <a name="uri-parameter"></a><span data-ttu-id="a1d0b-134">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="a1d0b-134">URI parameter</span></span>

<span data-ttu-id="a1d0b-135">Az előfizetés átváltásához használja az alábbi lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-135">Use the following query parameter to transition the subscription.</span></span>

| <span data-ttu-id="a1d0b-136">Név</span><span class="sxs-lookup"><span data-stu-id="a1d0b-136">Name</span></span>                    | <span data-ttu-id="a1d0b-137">Típus</span><span class="sxs-lookup"><span data-stu-id="a1d0b-137">Type</span></span>     | <span data-ttu-id="a1d0b-138">Kötelező</span><span class="sxs-lookup"><span data-stu-id="a1d0b-138">Required</span></span> | <span data-ttu-id="a1d0b-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="a1d0b-139">Description</span></span>                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| <span data-ttu-id="a1d0b-140">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="a1d0b-140">**customer-tenant-id**</span></span>  | <span data-ttu-id="a1d0b-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="a1d0b-141">**guid**</span></span> | <span data-ttu-id="a1d0b-142">Y</span><span class="sxs-lookup"><span data-stu-id="a1d0b-142">Y</span></span>        | <span data-ttu-id="a1d0b-143">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-143">A GUID corresponding to the customer.</span></span>             |
| <span data-ttu-id="a1d0b-144">**azonosító – előfizetés**</span><span class="sxs-lookup"><span data-stu-id="a1d0b-144">**id-for-subscription**</span></span> | <span data-ttu-id="a1d0b-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="a1d0b-145">**guid**</span></span> | <span data-ttu-id="a1d0b-146">Y</span><span class="sxs-lookup"><span data-stu-id="a1d0b-146">Y</span></span>        | <span data-ttu-id="a1d0b-147">A kezdeti előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-147">A GUID corresponding to the initial subscription.</span></span> |
| <span data-ttu-id="a1d0b-148">**azonosító – cél**</span><span class="sxs-lookup"><span data-stu-id="a1d0b-148">**id-for-target**</span></span>       | <span data-ttu-id="a1d0b-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="a1d0b-149">**guid**</span></span> | <span data-ttu-id="a1d0b-150">Y</span><span class="sxs-lookup"><span data-stu-id="a1d0b-150">Y</span></span>        | <span data-ttu-id="a1d0b-151">A célként megadott előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-151">A GUID corresponding to the target subscription.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="a1d0b-152">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="a1d0b-152">Request headers</span></span>

<span data-ttu-id="a1d0b-153">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a1d0b-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a1d0b-154">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="a1d0b-154">Request body</span></span>

<span data-ttu-id="a1d0b-155">Nincs</span><span class="sxs-lookup"><span data-stu-id="a1d0b-155">None</span></span>

### <a name="request-example"></a><span data-ttu-id="a1d0b-156">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="a1d0b-156">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

POST https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 750fd5ea-904b-4c3e-b476-60d0feacab0d
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
Content-Type: application/json
Content-Length: 1098
Expect: 100-continue

{
    "TargetOffer":{
        "Id":"796B6B5F-613C-4E24-A17C-EBA730D49C02",
        "Name":"Office 365 Enterprise E3",
        "Description":"The best plan for businesses that need full productivity, communication and collaboration tools with the familiar Office suite, including Office Online.",
        "MinimumQuantity":1,
        "MaximumQuantity":10000000,
        "Rank":61,
        "Uri":"/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/796B6B5F-613C-4E24-A17C-EBA730D49C02",
        "Locale":"en-us",
        "Country":"US",
        "Category":{
            "Id":"Enterprise_Key",
            "Name":"Enterprise",
            "Rank":20,
            "Locale":"en-us",
            "Country":"US",
            "Attributes":{
                "ObjectType":"OfferCategory"
            }
        },
        "PrerequisiteOffers":[],
        "IsAddOn":false,
        "IsAvailableForPurchase":true,
        "Billing":"license",
        "IsAutoRenewable":true,
        "Product":{
            "Id":"6fd2c87f-b296-42f0-b197-1e91e994b900",
            "Name":"Office 365 Enterprise E3",
            "Unit":"Licenses"
        },
        "UnitType":"Licenses",
        "Links":{
            "LearnMore":{
                "Uri":"http://g.microsoftonline.com/0BXPS00en/1015",
                "Method":"GET",
                "Headers":[]
            }
        }
        "Attributes":{
            "ObjectType":"Offer"
        }
    },
    "UpgradeType":1,
    "IsEligible":true,
    "Quantity":1,
    "UpgradeErrors":[],
    "Attributes":{
        "ObjectType":"Upgrade"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="a1d0b-157">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="a1d0b-157">REST response</span></span>

<span data-ttu-id="a1d0b-158">Ha ez sikeres, ez a metódus a válasz törzsében a **frissítési** eredmény erőforrását adja vissza.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-158">If successful, this method returns an **Upgrade** result resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a1d0b-159">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="a1d0b-159">Response success and error codes</span></span>

<span data-ttu-id="a1d0b-160">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a1d0b-161">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="a1d0b-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a1d0b-162">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a1d0b-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a1d0b-163">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="a1d0b-163">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 29 Jan 2016 20:42:26 GMT

{
    "totalCount": 1,
    "items": [{
        "targetOffer": {
            "id": "91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "name": "Office 365 Enterprise E1",
            "description": "For businesses that need communication and collaboration tools and the ability to read and do lightweight editing of documents with Office Online.",
            "minimumQuantity": 1,
            "maximumQuantity": 10000000,
            "rank": 48,
            "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "locale": "en-us",
            "country": "US",
            "category": {
                "id": "Enterprise_Key",
                "name": "Enterprise",
                "rank": 20,
                "locale": "en-us",
                "country": "US",
                "attributes": {
                    "objectType": "OfferCategory"
                }
            },
            "prerequisiteOffers": [],
            "isAddOn": false,
            "isAvailableForPurchase": true,
            "billing": "license",
            "isAutoRenewable": true,
            "isInternal": false,
            "conversionTargetOffers": [],
            "partnerQualifications": ["none"],
            "product": {
                "id": "18181a46-0d4e-45cd-891e-60aabd171b4e",
                "name": "Office 365 Enterprise E1",
                "unit": "Licenses"
            },
            "unitType": "Licenses",
            "links": {
                "learnMore": {
                    "uri": "http://g.microsoftonline.com/0BXPS00en/1013",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/offers/91FD106F-4B2C-4938-95AC-F54F74E9A239?country=US",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Offer"
            }
        },
        "upgradeType": "upgrade_only",
        "isEligible": false,
        "quantity": 1,
        "upgradeErrors": [{
            "code": 2,
            "description": "Subscription cannot be upgraded because the source subscription state is not active.  Additional Details contains the current source subscription state.",
            "attributes": {
                "objectType": "UpgradeError"
            }
        }],
        "attributes": {
            "objectType": "Upgrade"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}

HTTP/1.1 200 OK
Content-Length: 448
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 750fd5ea-904b-4c3e-b476-60d0feacab0d
MS-CV: RnK86LBbDkWP/w2R.0
MS-ServerId: 102031201
Date: Fri, 29 Jan 2016 20:44:21 GMT

{
    "sourceSubscriptionId":"896a2862-67e2-4f3d-bb3f-c50c42b5fad8",
    "targetSubscriptionId":"2add8a55-454a-4ae5-a4c9-5107dc6e9768",
    "upgradeType":1,
    "upgradeErrors":[],
    "licenseErrors":[],
    "attributes":{
        "objectType":"UpgradeResult"
    }
}
```
