---
title: Előfizetés átváltása
description: Frissíti egy ügyfél előfizetését egy megadott cél-előfizetésre.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 01455315825cad026830268b6bbd55509e964bb5
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530232"
---
# <a name="transition-a-subscription"></a><span data-ttu-id="be3f0-103">Előfizetés átváltása</span><span class="sxs-lookup"><span data-stu-id="be3f0-103">Transition a subscription</span></span>

<span data-ttu-id="be3f0-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="be3f0-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="be3f0-105">Frissíti egy ügyfél előfizetését egy megadott cél-előfizetésre.</span><span class="sxs-lookup"><span data-stu-id="be3f0-105">Upgrades a customer's subscription to a specified target subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be3f0-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="be3f0-106">Prerequisites</span></span>

- <span data-ttu-id="be3f0-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="be3f0-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="be3f0-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="be3f0-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="be3f0-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="be3f0-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="be3f0-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="be3f0-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="be3f0-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="be3f0-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="be3f0-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="be3f0-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="be3f0-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="be3f0-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="be3f0-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="be3f0-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="be3f0-115">Két előfizetés- és egy a kezdeti előfizetéshez, egy pedig a cél-előfizetéshez.</span><span class="sxs-lookup"><span data-stu-id="be3f0-115">Two subscription IDs, one for the initial subscription and one for the target subscription.</span></span>

## <a name="c"></a><span data-ttu-id="be3f0-116">C\#</span><span class="sxs-lookup"><span data-stu-id="be3f0-116">C\#</span></span>

<span data-ttu-id="be3f0-117">Az ügyfél előfizetésének frissítéséhez először szerezze be az [ügyfél előfizetését.](get-a-subscription-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="be3f0-117">To upgrade a customer's subscription, first [get that's customer's subscription](get-a-subscription-by-id.md).</span></span> <span data-ttu-id="be3f0-118">Ezután szerezze be az előfizetés frissítésének listáját az **Upgrades tulajdonság,** majd a **Get()** vagy **a GetAsync() metódusok hívásával.**</span><span class="sxs-lookup"><span data-stu-id="be3f0-118">Then, obtain a list of upgrades for that subscription by calling the **Upgrades** property followed by the **Get()** or **GetAsync()** methods.</span></span> <span data-ttu-id="be3f0-119">Válasszon ki egy célfrissítést a frissítések listájából, majd hívja meg a kezdeti előfizetés **Upgrades** (Frissítések) tulajdonságát, majd a **Create() metódust.**</span><span class="sxs-lookup"><span data-stu-id="be3f0-119">Choose a target upgrade from that list of upgrades, and then call the **Upgrades** property of the initial subscription, followed by the **Create()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionIdForUpgrade;
// Upgrade targetOffer;

UpgradeResult upgradeResult = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionIdForUpgrade).Upgrades.Create(targetOffer);
```

<span data-ttu-id="be3f0-120">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="be3f0-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="be3f0-121">**Project:** PartnerSDK.FeatureSamples **osztály:** UpgradeSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="be3f0-121">**Project**: PartnerSDK.FeatureSamples **Class**: UpgradeSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="be3f0-122">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="be3f0-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="be3f0-123">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="be3f0-123">Request syntax</span></span>

| <span data-ttu-id="be3f0-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="be3f0-124">Method</span></span>   | <span data-ttu-id="be3f0-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="be3f0-125">Request URI</span></span>                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="be3f0-126">**Kap**</span><span class="sxs-lookup"><span data-stu-id="be3f0-126">**GET**</span></span>  | <span data-ttu-id="be3f0-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="be3f0-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1</span></span> |
| <span data-ttu-id="be3f0-128">**Post**</span><span class="sxs-lookup"><span data-stu-id="be3f0-128">**POST**</span></span> | <span data-ttu-id="be3f0-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="be3f0-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1</span></span>       |

### <a name="uri-parameter"></a><span data-ttu-id="be3f0-130">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="be3f0-130">URI parameter</span></span>

<span data-ttu-id="be3f0-131">Az előfizetés átváltásához használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="be3f0-131">Use the following query parameter to transition the subscription.</span></span>

| <span data-ttu-id="be3f0-132">Név</span><span class="sxs-lookup"><span data-stu-id="be3f0-132">Name</span></span>                    | <span data-ttu-id="be3f0-133">Típus</span><span class="sxs-lookup"><span data-stu-id="be3f0-133">Type</span></span>     | <span data-ttu-id="be3f0-134">Kötelező</span><span class="sxs-lookup"><span data-stu-id="be3f0-134">Required</span></span> | <span data-ttu-id="be3f0-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="be3f0-135">Description</span></span>                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| <span data-ttu-id="be3f0-136">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="be3f0-136">**customer-tenant-id**</span></span>  | <span data-ttu-id="be3f0-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="be3f0-137">**guid**</span></span> | <span data-ttu-id="be3f0-138">Y</span><span class="sxs-lookup"><span data-stu-id="be3f0-138">Y</span></span>        | <span data-ttu-id="be3f0-139">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="be3f0-139">A GUID corresponding to the customer.</span></span>             |
| <span data-ttu-id="be3f0-140">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="be3f0-140">**id-for-subscription**</span></span> | <span data-ttu-id="be3f0-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="be3f0-141">**guid**</span></span> | <span data-ttu-id="be3f0-142">Y</span><span class="sxs-lookup"><span data-stu-id="be3f0-142">Y</span></span>        | <span data-ttu-id="be3f0-143">A kezdeti előfizetésnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="be3f0-143">A GUID corresponding to the initial subscription.</span></span> |
| <span data-ttu-id="be3f0-144">**id-for-target**</span><span class="sxs-lookup"><span data-stu-id="be3f0-144">**id-for-target**</span></span>       | <span data-ttu-id="be3f0-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="be3f0-145">**guid**</span></span> | <span data-ttu-id="be3f0-146">Y</span><span class="sxs-lookup"><span data-stu-id="be3f0-146">Y</span></span>        | <span data-ttu-id="be3f0-147">A cél-előfizetésnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="be3f0-147">A GUID corresponding to the target subscription.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="be3f0-148">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="be3f0-148">Request headers</span></span>

<span data-ttu-id="be3f0-149">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="be3f0-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="be3f0-150">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="be3f0-150">Request body</span></span>

<span data-ttu-id="be3f0-151">None</span><span class="sxs-lookup"><span data-stu-id="be3f0-151">None</span></span>

### <a name="request-example"></a><span data-ttu-id="be3f0-152">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="be3f0-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="be3f0-153">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="be3f0-153">REST response</span></span>

<span data-ttu-id="be3f0-154">Ha ez a módszer sikeres, a válasz törzsében egy **Frissítés** eredményerőforrást ad vissza.</span><span class="sxs-lookup"><span data-stu-id="be3f0-154">If successful, this method returns an **Upgrade** result resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="be3f0-155">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="be3f0-155">Response success and error codes</span></span>

<span data-ttu-id="be3f0-156">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="be3f0-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="be3f0-157">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="be3f0-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="be3f0-158">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="be3f0-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="be3f0-159">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="be3f0-159">Response example</span></span>

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
