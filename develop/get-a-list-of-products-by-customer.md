---
title: Termékek listájának lekérése (ügyfél alapján)
description: Az ügyfélazonosítók segítségével lekért termékgyűjtemények ügyfél szerint.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: a7cb2430aa93beb89e4d1f9b8c89a016d66624ca
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874193"
---
# <a name="get-a-list-of-products-by-customer"></a><span data-ttu-id="1e05e-103">Termékek listájának lekérése (ügyfél alapján)</span><span class="sxs-lookup"><span data-stu-id="1e05e-103">Get a list of products (by customer)</span></span>

<span data-ttu-id="1e05e-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1e05e-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1e05e-105">Az alábbi módszerekkel lekért termékek gyűjteményét egy meglévő ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="1e05e-105">You can use the following methods to get a collection of products for an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e05e-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="1e05e-106">Prerequisites</span></span>

- <span data-ttu-id="1e05e-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1e05e-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1e05e-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="1e05e-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1e05e-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1e05e-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1e05e-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="1e05e-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1e05e-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="1e05e-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1e05e-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="1e05e-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1e05e-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="1e05e-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1e05e-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1e05e-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="1e05e-115">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="1e05e-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1e05e-116">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="1e05e-116">Request syntax</span></span>

| <span data-ttu-id="1e05e-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="1e05e-117">Method</span></span> | <span data-ttu-id="1e05e-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="1e05e-118">Request URI</span></span>                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1e05e-119">POST</span><span class="sxs-lookup"><span data-stu-id="1e05e-119">POST</span></span>   | <span data-ttu-id="1e05e-120">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1e05e-120">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1</span></span> |

#### <a name="request-uri-parameters"></a><span data-ttu-id="1e05e-121">URI-paraméterek kérése</span><span class="sxs-lookup"><span data-stu-id="1e05e-121">Request URI parameters</span></span>

| <span data-ttu-id="1e05e-122">Név</span><span class="sxs-lookup"><span data-stu-id="1e05e-122">Name</span></span>               | <span data-ttu-id="1e05e-123">Típus</span><span class="sxs-lookup"><span data-stu-id="1e05e-123">Type</span></span> | <span data-ttu-id="1e05e-124">Kötelező</span><span class="sxs-lookup"><span data-stu-id="1e05e-124">Required</span></span> | <span data-ttu-id="1e05e-125">Leírás</span><span class="sxs-lookup"><span data-stu-id="1e05e-125">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="1e05e-126">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="1e05e-126">**customer-tenant-id**</span></span> | <span data-ttu-id="1e05e-127">GUID</span><span class="sxs-lookup"><span data-stu-id="1e05e-127">GUID</span></span> | <span data-ttu-id="1e05e-128">Igen</span><span class="sxs-lookup"><span data-stu-id="1e05e-128">Yes</span></span> | <span data-ttu-id="1e05e-129">Az érték egy GUID-formátumú **ügyfél-bérlő-azonosító,** amely egy olyan azonosító, amellyel megadhatja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="1e05e-129">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="1e05e-130">**targetView**</span><span class="sxs-lookup"><span data-stu-id="1e05e-130">**targetView**</span></span> | <span data-ttu-id="1e05e-131">sztring</span><span class="sxs-lookup"><span data-stu-id="1e05e-131">string</span></span> | <span data-ttu-id="1e05e-132">Igen</span><span class="sxs-lookup"><span data-stu-id="1e05e-132">Yes</span></span> | <span data-ttu-id="1e05e-133">A katalógus célnézetét azonosítja.</span><span class="sxs-lookup"><span data-stu-id="1e05e-133">Identifies the target view of the catalog.</span></span> <span data-ttu-id="1e05e-134">A támogatott értékek a következőek:</span><span class="sxs-lookup"><span data-stu-id="1e05e-134">The supported values are:</span></span> <br/><br/><span data-ttu-id="1e05e-135">**Azure**, amely az összes Azure-elemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="1e05e-135">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="1e05e-136">**AzureReservations**, amely az összes Azure-foglalási elemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="1e05e-136">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="1e05e-137">**AzureReservationsVM,** amely az összes virtuálisgép-foglalási elemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="1e05e-137">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="1e05e-138">**AzureReservationsSQL,** amely az összes SQL tartalmazza</span><span class="sxs-lookup"><span data-stu-id="1e05e-138">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="1e05e-139">**AzureReservationsCosmosDb,** amely a Cosmos-adatbázis összes foglalási elemét tartalmazza</span><span class="sxs-lookup"><span data-stu-id="1e05e-139">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="1e05e-140">**MicrosoftAzure**, amely a Microsoft Azure **(MS-AZR-0145P)** és az Azure-csomagok elemeit tartalmazza</span><span class="sxs-lookup"><span data-stu-id="1e05e-140">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="1e05e-141">**OnlineServices**, amely az összes online szolgáltatási elemet tartalmazza, beleértve a kereskedelmi piactéren elérhető termékeket is</span><span class="sxs-lookup"><span data-stu-id="1e05e-141">**OnlineServices**, which includes all online service items, including commercial marketplace products</span></span><br/><br/><span data-ttu-id="1e05e-142">**Szoftver,** amely az összes szoftverelemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="1e05e-142">**Software**, which  includes all software items</span></span><br/><br/><span data-ttu-id="1e05e-143">**SoftwareSUSELinux**, amely az összes szoftveres SUSE Linux-elemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="1e05e-143">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="1e05e-144">**SzoftverPerpetual**, amely az összes állandó szoftverelemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="1e05e-144">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="1e05e-145">**SoftwareSubscriptions**, amely az összes szoftver-előfizetési elemet tartalmazza</span><span class="sxs-lookup"><span data-stu-id="1e05e-145">**SoftwareSubscriptions**, which includes all software subscription items</span></span>  |

### <a name="request-header"></a><span data-ttu-id="1e05e-146">Kérelem fejléce</span><span class="sxs-lookup"><span data-stu-id="1e05e-146">Request header</span></span>

<span data-ttu-id="1e05e-147">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1e05e-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1e05e-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="1e05e-148">Request body</span></span>

<span data-ttu-id="1e05e-149">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="1e05e-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1e05e-150">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="1e05e-150">Request example</span></span>

<span data-ttu-id="1e05e-151">Egy adott ügyfél számára elérhető Azure-beli használatalapú termékek listájának lekérése.</span><span class="sxs-lookup"><span data-stu-id="1e05e-151">Request for a list of Azure usage-based products available to a given customer.</span></span> <span data-ttu-id="1e05e-152">A rendszer a nyilvános Microsoft Azure (MS-AZR-0145P) és az Azure-csomagokhoz is visszaadja a termékeket:</span><span class="sxs-lookup"><span data-stu-id="1e05e-152">Products for both Microsoft Azure (MS-AZR-0145P) and Azure plans will be returned for customers in public cloud:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="1e05e-153">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="1e05e-153">Rest response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1e05e-154">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="1e05e-154">Response success and error codes</span></span>

<span data-ttu-id="1e05e-155">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="1e05e-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1e05e-156">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="1e05e-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1e05e-157">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1e05e-157">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="1e05e-158">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="1e05e-158">This method returns the following error codes:</span></span>

| <span data-ttu-id="1e05e-159">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="1e05e-159">HTTP Status Code</span></span> | <span data-ttu-id="1e05e-160">Hibakód</span><span class="sxs-lookup"><span data-stu-id="1e05e-160">Error code</span></span>   | <span data-ttu-id="1e05e-161">Leírás</span><span class="sxs-lookup"><span data-stu-id="1e05e-161">Description</span></span>                     |
|------------------|--------------|---------------------------------|
| <span data-ttu-id="1e05e-162">403</span><span class="sxs-lookup"><span data-stu-id="1e05e-162">403</span></span> | <span data-ttu-id="1e05e-163">400036</span><span class="sxs-lookup"><span data-stu-id="1e05e-163">400036</span></span> | <span data-ttu-id="1e05e-164">A kért targetView-hoz való hozzáférés nem engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="1e05e-164">Access to the requested targetView is not allowed.</span></span> |

### <a name="response-example"></a><span data-ttu-id="1e05e-165">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="1e05e-165">Response example</span></span>

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
