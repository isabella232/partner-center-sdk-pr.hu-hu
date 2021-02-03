---
title: Jogosultságok gyűjteményének lekérése
description: Jogosultságok gyűjteményének beszerzése.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d2cc485429941dd2080bd285553333a01fc0ffd1
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768068"
---
# <a name="get-a-collection-of-entitlements"></a><span data-ttu-id="90f1e-103">Jogosultságok gyűjteményének lekérése</span><span class="sxs-lookup"><span data-stu-id="90f1e-103">Get a collection of entitlements</span></span>

<span data-ttu-id="90f1e-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="90f1e-104">**Applies To**</span></span>

- <span data-ttu-id="90f1e-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="90f1e-105">Partner Center</span></span>

<span data-ttu-id="90f1e-106">Jogosultságok gyűjteményének beszerzése.</span><span class="sxs-lookup"><span data-stu-id="90f1e-106">How to get a collection of entitlements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90f1e-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="90f1e-107">Prerequisites</span></span>

- <span data-ttu-id="90f1e-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="90f1e-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="90f1e-109">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="90f1e-109">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="90f1e-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="90f1e-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="90f1e-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="90f1e-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="90f1e-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="90f1e-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="90f1e-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="90f1e-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="90f1e-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="90f1e-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="90f1e-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="90f1e-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="90f1e-116">C\#</span><span class="sxs-lookup"><span data-stu-id="90f1e-116">C\#</span></span>

<span data-ttu-id="90f1e-117">Egy ügyfél jogosultsági gyűjteményének beszerzéséhez szerezzen be egy felületet a [**jogosultsági**](entitlement-resources.md#entitlement) műveletekhez úgy, hogy meghívja a  [**IAggregatePartner. customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="90f1e-117">To get an entitlements collection for a customer, obtain an interface to [**Entitlement**](entitlement-resources.md#entitlement) operations by calling the  [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="90f1e-118">Ezután kérje le a felületet a **jogosultságok** tulajdonságból, és hívja meg a **Get ()** vagy a **GetAsync ()** metódust a jogosultságok gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="90f1e-118">Then, retrieve the interface from the **Entitlements** property and call the **Get()** or **GetAsync()** method to retrieve the collection of entitlements.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;

// Get the collection of entitlements.
var entitlements = partnerOperations.Customers.ById(customerId).Entitlements.Get();
```

<span data-ttu-id="90f1e-119">Ha fel szeretné tölteni a jogosultságok lejárati idejét a lekéréshez, hívja meg a fenti metódusokat, és állítsa a **showExpiry** (true **)** vagy a **GetAsync (** true) értékre a nem kötelező logikai paramétert.</span><span class="sxs-lookup"><span data-stu-id="90f1e-119">To populate expiry dates for the entitlements to be retrieved, call the same methods above and set the optional boolean parameter **showExpiry** to true **Get(true)** or **GetAsync(true)**.</span></span> <span data-ttu-id="90f1e-120">Ez azt jelzi, hogy a jogosultság lejárati dátumai szükségesek (ha vannak ilyenek).</span><span class="sxs-lookup"><span data-stu-id="90f1e-120">This indicates that entitlement expiry dates are required (when applicable).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90f1e-121">A helyszíni jogosultsági típusok nem rendelkeznek lejárati dátummal.</span><span class="sxs-lookup"><span data-stu-id="90f1e-121">On-premise entitlement types do not have expiry dates.</span></span>

## <a name="rest-request"></a><span data-ttu-id="90f1e-122">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="90f1e-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="90f1e-123">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="90f1e-123">Request syntax</span></span>

| <span data-ttu-id="90f1e-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="90f1e-124">Method</span></span> | <span data-ttu-id="90f1e-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="90f1e-125">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="90f1e-126">**GET**</span><span class="sxs-lookup"><span data-stu-id="90f1e-126">**GET**</span></span> | <span data-ttu-id="90f1e-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customerId}/Entitlements http/1.1</span><span class="sxs-lookup"><span data-stu-id="90f1e-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1</span></span>                            |

### <a name="uri-parameters"></a><span data-ttu-id="90f1e-128">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="90f1e-128">URI parameters</span></span>

<span data-ttu-id="90f1e-129">A kérelem létrehozásakor használja az alábbi elérési utat és a lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="90f1e-129">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="90f1e-130">Név</span><span class="sxs-lookup"><span data-stu-id="90f1e-130">Name</span></span> | <span data-ttu-id="90f1e-131">Típus</span><span class="sxs-lookup"><span data-stu-id="90f1e-131">Type</span></span> | <span data-ttu-id="90f1e-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="90f1e-132">Required</span></span> | <span data-ttu-id="90f1e-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="90f1e-133">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="90f1e-134">customerId</span><span class="sxs-lookup"><span data-stu-id="90f1e-134">customerId</span></span> | <span data-ttu-id="90f1e-135">sztring</span><span class="sxs-lookup"><span data-stu-id="90f1e-135">string</span></span> | <span data-ttu-id="90f1e-136">Igen</span><span class="sxs-lookup"><span data-stu-id="90f1e-136">Yes</span></span> | <span data-ttu-id="90f1e-137">GUID formátumú Vevőkód, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="90f1e-137">A GUID formatted customerId that identifies the customer.</span></span> |
| <span data-ttu-id="90f1e-138">entitlementType</span><span class="sxs-lookup"><span data-stu-id="90f1e-138">entitlementType</span></span> | <span data-ttu-id="90f1e-139">sztring</span><span class="sxs-lookup"><span data-stu-id="90f1e-139">string</span></span> | <span data-ttu-id="90f1e-140">No</span><span class="sxs-lookup"><span data-stu-id="90f1e-140">No</span></span> | <span data-ttu-id="90f1e-141">A lekérdezni kívánt jogosultságok típusának meghatározására használható (**szoftver** -vagy **reservedInstance** ).</span><span class="sxs-lookup"><span data-stu-id="90f1e-141">Can be used to specify the type of entitlements to be retrieved (**software** or **reservedInstance** ).</span></span> <span data-ttu-id="90f1e-142">Ha nincs beállítva, a rendszer az összes típust beolvassa</span><span class="sxs-lookup"><span data-stu-id="90f1e-142">If not set, all types will be retrieved</span></span> |
| <span data-ttu-id="90f1e-143">showExpiry</span><span class="sxs-lookup"><span data-stu-id="90f1e-143">showExpiry</span></span> | <span data-ttu-id="90f1e-144">boolean</span><span class="sxs-lookup"><span data-stu-id="90f1e-144">boolean</span></span> | <span data-ttu-id="90f1e-145">Nem</span><span class="sxs-lookup"><span data-stu-id="90f1e-145">No</span></span> | <span data-ttu-id="90f1e-146">Opcionális jelző, amely megadja, hogy a jogosultságok lejárati dátuma kötelező-e.</span><span class="sxs-lookup"><span data-stu-id="90f1e-146">Optional flag which indicates if entitlements expiry dates are required.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="90f1e-147">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="90f1e-147">Request headers</span></span>

<span data-ttu-id="90f1e-148">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="90f1e-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="90f1e-149">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="90f1e-149">Request body</span></span>

<span data-ttu-id="90f1e-150">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="90f1e-150">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="90f1e-151">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="90f1e-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/entitlements HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="90f1e-152">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="90f1e-152">REST response</span></span>

<span data-ttu-id="90f1e-153">Ha ez sikeres, a válasz törzse a [jogosultsági](entitlement-resources.md#entitlement) erőforrások gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="90f1e-153">If successful, the response body contains a collection of [Entitlement](entitlement-resources.md#entitlement) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="90f1e-154">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="90f1e-154">Response success and error codes</span></span>

<span data-ttu-id="90f1e-155">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="90f1e-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="90f1e-156">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="90f1e-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="90f1e-157">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="90f1e-157">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="90f1e-158">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="90f1e-158">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 103778
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: EjFdw8fCpkKyMyza.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:42:51 GMT

{
  "totalCount": 2,
  "items": [
    {
      "includedEntitlements": [],
      "referenceOrder": {
        "id": "KaJ8XvkKc_GoNZOUyjVaRJalTBN5MWdV1",
        "lineItemId": "0"
      },
      "productId": "DZH318Z0BQ3W",
      "quantity": 1,
      "entitledArtifacts": [
        {
          "link": {
            "uri": "/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336",
            "method": "GET",
            "headers": []
          },
          "resourceId": "ebf2e74b-630e-4a09-857d-a1f6c6351336",
          "artifactType": "reservedinstance"
        }
      ],
      "skuId": "007J",
      "entitlementType": "reservedinstance"
      "dynamicAttributes": {
               "reservationType": "virtualmachines"
        }
    },
    {
      "includedEntitlements": [
        {
          "includedEntitlements": [],
          "referenceOrder": {
              "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
              "lineItemId": "0"
          },
          "productId": "DG7GMGF0DWTJ",
          "quantity": 1,
          "entitledArtifacts": [],
          "skuId": "0001",
          "entitlementType": "software"
        },
        {
          "includedEntitlements": [],
          "referenceOrder": {
            "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
            "lineItemId": "0"
          },
            "productId": "DG7GMGF0DWLG",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
          }
        ],
        "referenceOrder": {
          "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
          "lineItemId": "0"
        },
        "productId": "DG7GMGF0DWTK",
        "quantity": 1,
        "entitledArtifacts": [],
        "skuId": "0002",
        "entitlementType": "software"
    }
  ],
  "attributes": {
    "objectType": "Collection"
  }
}
```

## <a name="additional-examples"></a><span data-ttu-id="90f1e-159">További példák</span><span class="sxs-lookup"><span data-stu-id="90f1e-159">Additional Examples</span></span>

<span data-ttu-id="90f1e-160">Az alábbi példa bemutatja, hogyan kérhet le egy adott típusú jogosultságot a lejárati dátumokkal együtt (ha alkalmazható)</span><span class="sxs-lookup"><span data-stu-id="90f1e-160">The following example shows you how to retrieve a specific type of entitlements along with expiry dates (when applicable)</span></span>

### <a name="c-example"></a><span data-ttu-id="90f1e-161">C \# példa</span><span class="sxs-lookup"><span data-stu-id="90f1e-161">C\# example</span></span>

<span data-ttu-id="90f1e-162">A jogosultságok meghatározott típusának lekéréséhez szerezze be a **ByEntitlementType** felületet a **jogosultságok** felületéről, és használja a **Get ()** vagy a **GetAsync ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="90f1e-162">To retrieve a specific type of entitlements, obtain the **ByEntitlementType** interface from the **Entitlements** interface and use the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("software").Get(true);
```

### <a name="request-example"></a><span data-ttu-id="90f1e-163">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="90f1e-163">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/de3dcef9-9991-459c-ac71-2903d1127414/entitlements?entitlementtype=software&showExpiry=true
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="90f1e-164">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="90f1e-164">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1791
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
X-Locale: en-US
MS-CV: yD+4LBKePUSp/vqJ.0
MS-ServerId: 000002
Date: Mon, 28 Jan 2019 18:31:43 GMT

{
    "totalCount": 2,
    "items": [
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWM2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWMK",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "0",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWM3",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
        },
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV1",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "1",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWBQ",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0003",
            "entitlementType": "software",
            "expiryDate": "2022-01-28T00:00:00Z"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

<span data-ttu-id="90f1e-165">Az alábbi példák bemutatják, hogyan kérhet le adatokat a termékekről és a foglalásokról egy jogosultságról.</span><span class="sxs-lookup"><span data-stu-id="90f1e-165">The following examples show you how to retrieve information about products and reservations from an entitlement.</span></span>

### <a name="retrieve-virtual-machine-reservation-details-from-an-entitlement-by-using-sdk-v18"></a><span data-ttu-id="90f1e-166">Virtuális gépek foglalási adatainak beolvasása jogosultságból az SDK V 1.8 használatával</span><span class="sxs-lookup"><span data-stu-id="90f1e-166">Retrieve virtual machine reservation details from an entitlement by using SDK V1.8</span></span>

### <a name="c-example"></a><span data-ttu-id="90f1e-167">C \# példa</span><span class="sxs-lookup"><span data-stu-id="90f1e-167">C\# example</span></span>

<span data-ttu-id="90f1e-168">Ha további részleteket szeretne beolvasni egy jogosultságból a virtuális gépek fenntartásával kapcsolatban, hívja meg a entitledArtifacts. link és a artifactType = virtual_machine_reserved_instance között elérhető URI-t.</span><span class="sxs-lookup"><span data-stu-id="90f1e-168">To retrieve more details related to the virtual machine reservations from an entitlement, invoke the URI exposed under entitledArtifacts.link with artifactType = virtual_machine_reserved_instance .</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("VirtualMachineReservedInstance").Get();

((VirtualMachineReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.VirtualMachineReservedInstance)).Link.InvokeAsync<VirtualMachineReservedInstanceArtifactDetails>(partnerOperations)
```

### <a name="request-example"></a><span data-ttu-id="90f1e-169">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="90f1e-169">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="90f1e-170">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="90f1e-170">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "virtual_machine_reserved_instance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="retrieve-reservation-details-from-an-entitlement-by-using-sdk-v19"></a><span data-ttu-id="90f1e-171">A foglalás részleteinek beolvasása jogosultságok alapján az SDK V 1.9 használatával</span><span class="sxs-lookup"><span data-stu-id="90f1e-171">Retrieve reservation details from an entitlement by using SDK V1.9</span></span>

### <a name="c-example"></a><span data-ttu-id="90f1e-172">C \# példa</span><span class="sxs-lookup"><span data-stu-id="90f1e-172">C\# example</span></span>

<span data-ttu-id="90f1e-173">A fenntartott példányokra vonatkozó jogosultságok fenntartásával kapcsolatos további részletekért hívja meg a-ben elérhető URI- ```entitledArtifacts.link``` t ```artifactType = reservedinstance``` .</span><span class="sxs-lookup"><span data-stu-id="90f1e-173">To retrieve more details related to the reservations from a reserved instance entitlement, invoke the URI exposed under ```entitledArtifacts.link``` with ```artifactType = reservedinstance```.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("ReservedInstance").Get();

((ReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.ReservedInstance)).Link.InvokeAsync<ReservedInstanceArtifactDetails>(partnerOperations);
```

### <a name="request-example"></a><span data-ttu-id="90f1e-174">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="90f1e-174">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="90f1e-175">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="90f1e-175">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "reservedinstance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="api-consumers"></a><span data-ttu-id="90f1e-176">API-felhasználók</span><span class="sxs-lookup"><span data-stu-id="90f1e-176">API Consumers</span></span>

<span data-ttu-id="90f1e-177">Azok a partnerek, akik az API-t használják a virtuális gép fenntartott példányaira vonatkozó jogosultságok lekérdezésére – a/Customers/{customerId}/Entitlements-ről/customers/{customerId}/entitlements-re való kérelem URI-azonosítójának frissítése a **entitlementType = virtualmachinereservedinstance** .</span><span class="sxs-lookup"><span data-stu-id="90f1e-177">Partners who are using the API to query virtual machine reserved instance entitlements - Update the request URI from **/customers/{customerId}/entitlements to /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** to maintain backward compatibility.</span></span> <span data-ttu-id="90f1e-178">Ha a virtuális gépet vagy az Azure SQL-t bővített szerződéssel szeretné használni, frissítse a kérelem URI-JÁT a **/Customers/{customerId}/Entitlements? entitlementType = reservedinstance**.</span><span class="sxs-lookup"><span data-stu-id="90f1e-178">In order to consume virtual machine or Azure SQL with enhanced contract, update the request URI to **/customers/{customerId}/entitlements?entitlementType=reservedinstance**.</span></span>
