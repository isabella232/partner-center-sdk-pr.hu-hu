---
title: Termékek listájának lekérése (ügyfél alapján)
description: Az ügyfél-azonosítóval termékek gyűjteményét veheti igénybe az ügyfél által.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 98a099c458535123f675c6452db950b087b9f387
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768175"
---
# <a name="get-a-list-of-products-by-customer"></a><span data-ttu-id="d2ebb-103">Termékek listájának lekérése (ügyfél alapján)</span><span class="sxs-lookup"><span data-stu-id="d2ebb-103">Get a list of products (by customer)</span></span>

<span data-ttu-id="d2ebb-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="d2ebb-104">**Applies to:**</span></span>

- <span data-ttu-id="d2ebb-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="d2ebb-105">Partner Center</span></span>
- <span data-ttu-id="d2ebb-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="d2ebb-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d2ebb-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="d2ebb-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d2ebb-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="d2ebb-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d2ebb-109">A következő módszerekkel egy meglévő ügyfélhez tartozó termékek gyűjteményét kérheti le.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-109">You can use the following methods to get a collection of products for an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2ebb-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d2ebb-110">Prerequisites</span></span>

- <span data-ttu-id="d2ebb-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d2ebb-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d2ebb-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d2ebb-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d2ebb-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="d2ebb-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d2ebb-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d2ebb-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d2ebb-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d2ebb-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d2ebb-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="d2ebb-119">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="d2ebb-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d2ebb-120">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d2ebb-120">Request syntax</span></span>

| <span data-ttu-id="d2ebb-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="d2ebb-121">Method</span></span> | <span data-ttu-id="d2ebb-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d2ebb-122">Request URI</span></span>                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d2ebb-123">POST</span><span class="sxs-lookup"><span data-stu-id="d2ebb-123">POST</span></span>   | <span data-ttu-id="d2ebb-124">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Products? targetView = {targetView} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d2ebb-124">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1</span></span> |

#### <a name="request-uri-parameters"></a><span data-ttu-id="d2ebb-125">Kérelem URI-paraméterei</span><span class="sxs-lookup"><span data-stu-id="d2ebb-125">Request URI parameters</span></span>

| <span data-ttu-id="d2ebb-126">Név</span><span class="sxs-lookup"><span data-stu-id="d2ebb-126">Name</span></span>               | <span data-ttu-id="d2ebb-127">Típus</span><span class="sxs-lookup"><span data-stu-id="d2ebb-127">Type</span></span> | <span data-ttu-id="d2ebb-128">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d2ebb-128">Required</span></span> | <span data-ttu-id="d2ebb-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="d2ebb-129">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="d2ebb-130">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="d2ebb-130">**customer-tenant-id**</span></span> | <span data-ttu-id="d2ebb-131">GUID</span><span class="sxs-lookup"><span data-stu-id="d2ebb-131">GUID</span></span> | <span data-ttu-id="d2ebb-132">Igen</span><span class="sxs-lookup"><span data-stu-id="d2ebb-132">Yes</span></span> | <span data-ttu-id="d2ebb-133">Az érték egy GUID-formátumú **ügyfél-bérlői azonosító**, amely egy ügyfél megadását lehetővé tevő azonosító.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-133">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="d2ebb-134">**targetView**</span><span class="sxs-lookup"><span data-stu-id="d2ebb-134">**targetView**</span></span> | <span data-ttu-id="d2ebb-135">sztring</span><span class="sxs-lookup"><span data-stu-id="d2ebb-135">string</span></span> | <span data-ttu-id="d2ebb-136">Igen</span><span class="sxs-lookup"><span data-stu-id="d2ebb-136">Yes</span></span> | <span data-ttu-id="d2ebb-137">Meghatározza a katalógus céljának nézetét.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-137">Identifies the target view of the catalog.</span></span> <span data-ttu-id="d2ebb-138">A támogatott értékek a következők:</span><span class="sxs-lookup"><span data-stu-id="d2ebb-138">The supported values are:</span></span> <br/><br/><span data-ttu-id="d2ebb-139">**Azure**, amely tartalmazza az összes Azure-elemet</span><span class="sxs-lookup"><span data-stu-id="d2ebb-139">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="d2ebb-140">**AzureReservations**, amely tartalmazza az összes Azure foglalási elemet</span><span class="sxs-lookup"><span data-stu-id="d2ebb-140">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="d2ebb-141">**AzureReservationsVM**, amely tartalmazza az összes virtuális gép (VM) foglalási elemét</span><span class="sxs-lookup"><span data-stu-id="d2ebb-141">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="d2ebb-142">**AzureReservationsSQL**, amely az összes SQL-foglalási elemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="d2ebb-142">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="d2ebb-143">**AzureReservationsCosmosDb**, amely tartalmazza az összes Cosmos-adatbázis foglalási elemét.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-143">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="d2ebb-144">**MicrosoftAzure**, amely Microsoft Azure előfizetések (**MS-AZR-0145P**) és az Azure-csomagok elemeit tartalmazza</span><span class="sxs-lookup"><span data-stu-id="d2ebb-144">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="d2ebb-145">**OnlineServices**, amely tartalmazza az összes online szolgáltatási elemet, beleértve a kereskedelmi piactér termékeit is</span><span class="sxs-lookup"><span data-stu-id="d2ebb-145">**OnlineServices**, which  includes all online service items, including commercial marketplace products</span></span><br/><br/><span data-ttu-id="d2ebb-146">**Szoftver**, amely tartalmazza az összes szoftver elemet</span><span class="sxs-lookup"><span data-stu-id="d2ebb-146">**Software**, which  includes all software items</span></span><br/><br/><span data-ttu-id="d2ebb-147">**SoftwareSUSELinux**, amely tartalmazza az összes szoftver SUSE Linux-elemet</span><span class="sxs-lookup"><span data-stu-id="d2ebb-147">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="d2ebb-148">**SoftwarePerpetual**, amely tartalmazza az összes örökös szoftver elemet.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-148">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="d2ebb-149">**SoftwareSubscriptions**, amely tartalmazza az összes szoftver-előfizetési elemet</span><span class="sxs-lookup"><span data-stu-id="d2ebb-149">**SoftwareSubscriptions**, which includes all software subscription items</span></span>  |

### <a name="request-header"></a><span data-ttu-id="d2ebb-150">Kérelem fejléce</span><span class="sxs-lookup"><span data-stu-id="d2ebb-150">Request header</span></span>

<span data-ttu-id="d2ebb-151">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d2ebb-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d2ebb-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d2ebb-152">Request body</span></span>

<span data-ttu-id="d2ebb-153">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d2ebb-154">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d2ebb-154">Request example</span></span>

<span data-ttu-id="d2ebb-155">Az adott ügyfél számára elérhető Azure-alapú használati termékek listájának kérése.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-155">Request for a list of Azure usage-based products available to a given customer.</span></span> <span data-ttu-id="d2ebb-156">A Microsoft Azure (MS-AZR-0145P) és az Azure-csomagok termékeit a nyilvános felhőben lévő ügyfelek számára is visszaadja a rendszer:</span><span class="sxs-lookup"><span data-stu-id="d2ebb-156">Products for both Microsoft Azure (MS-AZR-0145P) and Azure plans will be returned for customers in public cloud:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="d2ebb-157">Rest-válasz</span><span class="sxs-lookup"><span data-stu-id="d2ebb-157">Rest response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d2ebb-158">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d2ebb-158">Response success and error codes</span></span>

<span data-ttu-id="d2ebb-159">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d2ebb-160">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d2ebb-161">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d2ebb-161">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="d2ebb-162">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="d2ebb-162">This method returns the following error codes:</span></span>

| <span data-ttu-id="d2ebb-163">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="d2ebb-163">HTTP Status Code</span></span> | <span data-ttu-id="d2ebb-164">Hibakód</span><span class="sxs-lookup"><span data-stu-id="d2ebb-164">Error code</span></span>   | <span data-ttu-id="d2ebb-165">Leírás</span><span class="sxs-lookup"><span data-stu-id="d2ebb-165">Description</span></span>                     |
|------------------|--------------|---------------------------------|
| <span data-ttu-id="d2ebb-166">403</span><span class="sxs-lookup"><span data-stu-id="d2ebb-166">403</span></span> | <span data-ttu-id="d2ebb-167">400036</span><span class="sxs-lookup"><span data-stu-id="d2ebb-167">400036</span></span> | <span data-ttu-id="d2ebb-168">A kért targetView való hozzáférés nem engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="d2ebb-168">Access to the requested targetView is not allowed.</span></span> |

### <a name="response-example"></a><span data-ttu-id="d2ebb-169">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d2ebb-169">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "totalCount": 2,
    "items": [
        {
            "id": "MS-AZR-0145P",
            "productId": "9DEA7946-EC2C-441E-9FFD-E3B275F7E838",
            "title": "Microsoft Azure",
            "description": "Azure Cloud Solution Provider offer for Partner and Resellers",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "monthly"
            ],
            "purchasePrerequisites": [
                "MicrosoftCloudAgreement"
            ],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "billingType": "usage",
                "category": "Enterprise",
                "isAddon": false,
                "prerequisiteSkus": [],
                "rank": 1413,
                "hasAddOns": false,
                "isAutoRenewable": false,
                "upgradeTargetOffers": null,
                "conversionTargetOffers": [],
                "unitType": "Usage-based",
                "limitUnitOfMeasure": "None",
                "limit": 0,
                "reselleeQualifications": [],
                "resellerQualifications": []
            },
            "links": {
                "availabilities": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0001",
            "productId": "DZH318Z0BPS6",
            "title": "Microsoft Azure plan",
            "description": "Microsoft Azure plan (MS-AZR-0017G)",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "MicrosoftCustomerAgreement"
            ],
            "inventoryVariables": [],
            "provisioningVariables": [],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "pilotProgram": "modernazurepilot"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/e2a0c0f3-0f74-4d1c-808c-dfa511481913/products/all/skus?targetView=MicrosoftAzure&targetSegment=Commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
