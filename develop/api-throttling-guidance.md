---
title: Útmutatás az API-szabályozáshoz
description: A partner Center API-kat hívó partnereink számára megismerheti, hogy mely API-k befolyásolják a Microsoft API szabályozását és az ajánlott eljárásokat a szabályozás elkerüléséhez vagy jobb kezeléséhez.
ms.date: 09/09/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: a52751a97e699050075c1aac910cc51e94514f26
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/08/2020
ms.locfileid: "97768660"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a><span data-ttu-id="a2ac4-103">API-szabályozási útmutató a partner Center API-kat hívó partnereknek</span><span class="sxs-lookup"><span data-stu-id="a2ac4-103">API throttling guidance for partners calling Partner Center APIs</span></span> 

<span data-ttu-id="a2ac4-104">**A következőre érvényes:**</span><span class="sxs-lookup"><span data-stu-id="a2ac4-104">**Applies to**</span></span>

- <span data-ttu-id="a2ac4-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="a2ac4-105">Partner Center</span></span>

<span data-ttu-id="a2ac4-106">A Microsoft olyan API-szabályozást valósít meg, amely a partner Center API-kat hívó partnereink számára egy adott időszakon belül nagyobb konzisztens teljesítményt tesz lehetővé.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-106">Microsoft is implementing API throttling to allow more consistent performance within a time span for partners calling the Partner Center APIs.</span></span> <span data-ttu-id="a2ac4-107">A szabályozás korlátozza a szolgáltatásra irányuló kérések számát egy adott időszakban, hogy elkerülje az erőforrások túlzott mennyiségét.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-107">Throttling limits the number of requests to a service in a time span to prevent overuse of resources.</span></span> <span data-ttu-id="a2ac4-108">Míg a partneri központ nagy mennyiségű kérés kezelésére van kialakítva, ha a kérések túlnyomó száma kevés partnernél fordul elő, a szabályozás segít fenntartani az optimális teljesítményt és megbízhatóságot az összes partner számára.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-108">While Partner Center is designed to handle a high volume of requests, if an overwhelming number of requests occur by few partners, throttling helps maintain optimal performance and reliability for all partners.</span></span>  

<span data-ttu-id="a2ac4-109">A szabályozás korlátai a forgatókönyv alapján változnak.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-109">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="a2ac4-110">Ha például nagy mennyiségű írást végez, a szabályozás lehetősége magasabb, mint ha csak olvasást végez.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-110">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="what-happens-when-throttling-occurs"></a><span data-ttu-id="a2ac4-111">Mi történik a szabályozás esetén?</span><span class="sxs-lookup"><span data-stu-id="a2ac4-111">What happens when throttling occurs?</span></span> 

<span data-ttu-id="a2ac4-112">Ha túllépi a szabályozási küszöbértéket, a partneri központ egy adott időszakra korlátozza az ügyféltől érkező további kéréseket.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-112">When a throttling threshold is exceeded, Partner Center limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="a2ac4-113">A szabályozás viselkedése a kérelmek típusától és számától függ.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-113">Throttling behavior depends on the type and number of requests.</span></span>   

### <a name="common-throttling-scenarios"></a><span data-ttu-id="a2ac4-114">Gyakori szabályozási forgatókönyvek</span><span class="sxs-lookup"><span data-stu-id="a2ac4-114">Common throttling scenarios</span></span> 

<span data-ttu-id="a2ac4-115">Az ügyfelek szabályozásának leggyakoribb okai a következők:</span><span class="sxs-lookup"><span data-stu-id="a2ac4-115">The most common causes of throttling of clients include:</span></span> 

- <span data-ttu-id="a2ac4-116">**Nagyszámú kérelem egy adott API-hoz tartozó partneri bérlői azonosítóhoz**: egyes partneri központ API-k esetében a szabályozást a partner bérlői azonosítója határozza meg, az API-k ugyanazon partner BÉRLŐi azonosítóján túl sok hívást eredményez a sávszélesség-szabályozási küszöbérték túllépése.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-116">**A large number of requests for an API per Partner Tenant ID**: for some Partner Center APIs, throttling is determined by Partner Tenant ID, too many calls to those APIs on the same Partner Tenant ID will result in exceeding the throttling threshold.</span></span>  

- <span data-ttu-id="a2ac4-117">**Nagyszámú kérelem egy ügyfél**-BÉRLŐi azonosítóhoz a Customer bérlői azonosítója alapján: más API-k esetén a szabályozást a partner bérlő azonosítója/ügyfél bérlői azonosítója határozza meg. Ezekben az esetekben előfordulhat, hogy az azonos ügyfél-bérlői AZONOSÍTÓval való túl sok hívás a szabályozást eredményezi, míg a más ügyfelek felé irányuló hívások sikeresek lesznek.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-117">**A large number of requests for an API per Partner Tenant ID per Customer Tenant ID**: for other APIs, throttling is determined by Partner Tenant ID/Customer Tenant ID combination; in those cases, making too many calls against the same customer tenant ID will result in throttling - while calls against other customers may succeed.</span></span>

## <a name="best-practices-to-avoid-throttling"></a><span data-ttu-id="a2ac4-118">Ajánlott eljárások a szabályozás elkerüléséhez</span><span class="sxs-lookup"><span data-stu-id="a2ac4-118">Best practices to avoid throttling</span></span> 
 
<span data-ttu-id="a2ac4-119">Programozási eljárások, például az erőforrások folyamatos lekérdezése a frissítések kereséséhez és az erőforrások rendszeres vizsgálatához az új vagy törölt erőforrások ellenőrzéséhez nagyobb valószínűséggel vezethet a szabályozáshoz, és csökkenti a teljes teljesítményt.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-119">Programming practices such as continuously polling a resource to check for updates and regularly scanning resource collections to check for new or deleted resources are more likely to lead to throttling and will degrade overall performance.</span></span> <span data-ttu-id="a2ac4-120">Az egyidejű API-hívások nagy mennyiségű kérést okozhatnak az egységnyi idő alatt, ami a kérelmek szabályozását is eredményezi.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-120">Concurrent API calls may lead to high number of requests per unit time, which will also cause requests to be throttled.</span></span> <span data-ttu-id="a2ac4-121">Ehelyett a Change Tracking és a Change Notifications szolgáltatást kell használnia.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-121">You should instead leverage change tracking and change notifications.</span></span> <span data-ttu-id="a2ac4-122">Ezen kívül a változások észleléséhez is képesnek kell lennie a Tevékenységnaplók kihasználása érdekében további információért lásd a [partneri központ tevékenységi naplóit](get-a-record-of-partner-center-activity-by-user.md) .</span><span class="sxs-lookup"><span data-stu-id="a2ac4-122">Additionally, you should be able to leverage activity logs for detecting changes, see [Partner Center activity logs](get-a-record-of-partner-center-activity-by-user.md) for more information.</span></span>  <span data-ttu-id="a2ac4-123">Kifejezetten ajánljuk a partnereknek a Tevékenységnaplók API használatát a hatékonyság és a szabályozás elkerülése érdekében.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-123">We highly recommend partners to consider using the activity log API for more efficiency and to avoid throttling.</span></span> <span data-ttu-id="a2ac4-124">Lásd még a következő példa a tevékenység-naplók használatára című szakaszt.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-124">See also the example of using activity logs, below.</span></span>

## <a name="best-practices-to-handle-throttling"></a><span data-ttu-id="a2ac4-125">Ajánlott eljárások a szabályozás kezeléséhez</span><span class="sxs-lookup"><span data-stu-id="a2ac4-125">Best practices to handle throttling</span></span>

<span data-ttu-id="a2ac4-126">A következő ajánlott eljárások a szabályozás kezeléséhez:</span><span class="sxs-lookup"><span data-stu-id="a2ac4-126">The following are best practices for handling throttling:</span></span> 

- <span data-ttu-id="a2ac4-127">Csökkentse a párhuzamosság mértékét.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-127">Reduce the degree of parallelism.</span></span> 
- <span data-ttu-id="a2ac4-128">Csökkentse a hívások gyakoriságát.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-128">Reduce the frequency of calls.</span></span> 
- <span data-ttu-id="a2ac4-129">Kerülje az azonnali újrapróbálkozásokat, mert az összes kérelem a használati korlátok között van.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-129">Avoid immediate retries because all requests accrue against your usage limits.</span></span> 

<span data-ttu-id="a2ac4-130">Hibakezelés implementálásakor használja a 429-es HTTP-hibakódot a szabályozásészleléshez.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-130">When you implement error handling, use the HTTP error code 429 to detect throttling.</span></span> <span data-ttu-id="a2ac4-131">A sikertelen válasz tartalmazza a Retry-After válasz fejlécét.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-131">The failed response includes the Retry-After response header.</span></span> <span data-ttu-id="a2ac4-132">A kérelmeknek az újrapróbálkozást követő késleltetéssel történő biztonsági mentése a lehető leggyorsabb módszer a szabályozás helyreállítására.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-132">Backing off requests using the Retry-after delay is the fastest way to recover from throttling.</span></span> 

<span data-ttu-id="a2ac4-133">Az újrapróbálkozás utáni késleltetés használatához tegye a következőket:</span><span class="sxs-lookup"><span data-stu-id="a2ac4-133">To use the Retry-after delay, do the following:</span></span> 

1. <span data-ttu-id="a2ac4-134">Várjon a Retry-After fejlécben megadott másodpercek számát.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-134">Wait the number of seconds specified in the Retry-After header.</span></span> 

2. <span data-ttu-id="a2ac4-135">Próbálja megismételni a kérelmet.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-135">Retry the request.</span></span>  

3. <span data-ttu-id="a2ac4-136">Ha a kérelem 429-es hibakóddal meghiúsul, továbbra is szabályozva lesz.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-136">If the request fails again with a 429 error code, you are still being throttled.</span></span> <span data-ttu-id="a2ac4-137">Próbálkozzon újra az exponenciális leállítási, használja az ajánlott Retry-After késleltetést, majd ismételje meg a kérést, amíg a művelet be nem fejeződik.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-137">Retry with Exponential backoff, use the recommended Retry-After delay and retry the request until it succeeds.</span></span>

4. <span data-ttu-id="a2ac4-138">Ha az SDK-t használja, akkor az 429-es állapotkód kivételt fog kapni, ha a kérelmét szabályozzák.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-138">If you are using SDK you'll receive an exception with status code 429 when your request is being throttled.</span></span> <span data-ttu-id="a2ac4-139">A kivételben használja a RetryAfter tulajdonságot, és ismételje meg a kérést az idő lejárta után.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-139">Use the RetryAfter property in the exception and retry the request after the time is elapsed.</span></span>


## <a name="apis-currently-impacted-by-throttling"></a><span data-ttu-id="a2ac4-140">A szabályozás által jelenleg érintett API-k</span><span class="sxs-lookup"><span data-stu-id="a2ac4-140">APIs currently impacted by throttling</span></span>

<span data-ttu-id="a2ac4-141">Hosszú távon a "api.partnercenter.microsoft.com/" végpontot meghívó minden egyes partner Center API szabályozva lesz.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-141">In the long run, every single Partner Center API that calls the endpoint “api.partnercenter.microsoft.com/” will be throttled.</span></span> <span data-ttu-id="a2ac4-142">Jelenleg a szabályozás korlátozásai csak az alább felsorolt API-k esetében érvényesülnek.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-142">Currently, the throttling limits are only enforced on the few APIs listed below.</span></span> <span data-ttu-id="a2ac4-143">A partner Center összegyűjti a telemetria az egyes API-kkal, és dinamikusan módosítja a sávszélesség-szabályozási korlátokat.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-143">Partner Center will be collecting the telemetry on each of the APIs and will dynamically adjust the throttling limits.</span></span> <span data-ttu-id="a2ac4-144">A következő táblázat felsorolja azokat az API-kat, amelyeken a szabályozás jelenleg érvényben van.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-144">The following table lists the APIs where throttling is currently enforced.</span></span>  


|<span data-ttu-id="a2ac4-145">**Művelet**</span><span class="sxs-lookup"><span data-stu-id="a2ac4-145">**Operation**</span></span>| <span data-ttu-id="a2ac4-146">**Partnerközpont dokumentációja**</span><span class="sxs-lookup"><span data-stu-id="a2ac4-146">**Partner Center documentation**</span></span>|       
|------------------------|----------------------------|
|<span data-ttu-id="a2ac4-147">{baseURL}/v1/Customers/{customer_id}:/Orders</span><span class="sxs-lookup"><span data-stu-id="a2ac4-147">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="a2ac4-148">megrendelés létrehozása</span><span class="sxs-lookup"><span data-stu-id="a2ac4-148">create an order</span></span>](create-an-order.md)|
|<span data-ttu-id="a2ac4-149">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span><span class="sxs-lookup"><span data-stu-id="a2ac4-149">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span></span>|[<span data-ttu-id="a2ac4-150">előfizetés átváltása</span><span class="sxs-lookup"><span data-stu-id="a2ac4-150">transition a subscription</span></span>](transition-a-subscription.md)|
|<span data-ttu-id="a2ac4-151">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span><span class="sxs-lookup"><span data-stu-id="a2ac4-151">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span></span>|[<span data-ttu-id="a2ac4-152">addon vásárlása egy előfizetéshez</span><span class="sxs-lookup"><span data-stu-id="a2ac4-152">purchase an addon to a subscription</span></span>](purchase-an-add-on-to-a-subscription.md)|
|<span data-ttu-id="a2ac4-153">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="a2ac4-153">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="a2ac4-154">kosár létrehozása</span><span class="sxs-lookup"><span data-stu-id="a2ac4-154">create a cart</span></span>](create-a-cart.md)|
|<span data-ttu-id="a2ac4-155">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span><span class="sxs-lookup"><span data-stu-id="a2ac4-155">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span></span>|[<span data-ttu-id="a2ac4-156">kosár kifizetése</span><span class="sxs-lookup"><span data-stu-id="a2ac4-156">checkout a cart</span></span>](checkout-a-cart.md)|
|<span data-ttu-id="a2ac4-157">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="a2ac4-157">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="a2ac4-158">kosár frissítése</span><span class="sxs-lookup"><span data-stu-id="a2ac4-158">update a cart</span></span>](update-a-cart.md)|
|<span data-ttu-id="a2ac4-159">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span><span class="sxs-lookup"><span data-stu-id="a2ac4-159">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span></span>|[<span data-ttu-id="a2ac4-160">előfizetés regisztrálása</span><span class="sxs-lookup"><span data-stu-id="a2ac4-160">register a subscription</span></span>](register-a-subscription.md)|
|<span data-ttu-id="a2ac4-161">{baseURL}/v1/productupgrades</span><span class="sxs-lookup"><span data-stu-id="a2ac4-161">{baseURL}/v1/productupgrades</span></span>|[<span data-ttu-id="a2ac4-162">termék verziófrissítési entitásának létrehozása</span><span class="sxs-lookup"><span data-stu-id="a2ac4-162">create product upgrade entity</span></span>](create-product-upgrade-entity.md)|
|<span data-ttu-id="a2ac4-163">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span><span class="sxs-lookup"><span data-stu-id="a2ac4-163">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span> |[<span data-ttu-id="a2ac4-164">próbaverziós előfizetés átalakítása fizetős verzióra</span><span class="sxs-lookup"><span data-stu-id="a2ac4-164">convert a trial subscription to paid</span></span>](convert-a-trial-subscription-to-paid.md)|
|<span data-ttu-id="a2ac4-165">{baseURL}/v1/customers/{customer-tenant-id}</span><span class="sxs-lookup"><span data-stu-id="a2ac4-165">{baseURL}/v1/customers/{customer-tenant-id}</span></span>|[<span data-ttu-id="a2ac4-166">ügyfél beszerzése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="a2ac4-166">get a customer by id</span></span>](get-a-customer-by-id.md)|
|<span data-ttu-id="a2ac4-167">{baseURL}/v1/productUpgrades/eligibility</span><span class="sxs-lookup"><span data-stu-id="a2ac4-167">{baseURL}/v1/productUpgrades/eligibility</span></span>|[<span data-ttu-id="a2ac4-168">a termék frissítésére vonatkozó jogosultság beszerzése</span><span class="sxs-lookup"><span data-stu-id="a2ac4-168">get eligibility for product upgrade</span></span>](get-eligibility-for-product-upgrade.md)|
|<span data-ttu-id="a2ac4-169">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span><span class="sxs-lookup"><span data-stu-id="a2ac4-169">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span></span> |[<span data-ttu-id="a2ac4-170">előfizetés kezelése</span><span class="sxs-lookup"><span data-stu-id="a2ac4-170">manage subscription</span></span>](manage-orders.md#manage-a-subscription)|


### <a name="error-code-response"></a><span data-ttu-id="a2ac4-171">Hibakód válasza:</span><span class="sxs-lookup"><span data-stu-id="a2ac4-171">Error code response:</span></span>
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a><span data-ttu-id="a2ac4-172">Műveletnapló – példa</span><span class="sxs-lookup"><span data-stu-id="a2ac4-172">Example of activity log</span></span>

<span data-ttu-id="a2ac4-173">Ajánlott eljárás a napi változások elemzésekor azt javasoljuk, hogy egy adott napra vonatkozóan kérdezze le a naplózási rekordot.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-173">For best practice in analyzing daily changes, we recommend that you query audit record for a specific day.</span></span> 

<span data-ttu-id="a2ac4-174">A válaszban egy adott Művelettípus változásait fogja kapni.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-174">In the response, you will get a result with changes to specific operation type.</span></span><span data-ttu-id="a2ac4-175">Az Ön számára fontos művelet alapján szűrheti a szűrőt.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-175">  You can filter based on the operation you care about.</span></span> <span data-ttu-id="a2ac4-176">Ha például egy újonnan létrehozott ügyfelet érdekli, tekintse meg a következőt: operationType = "add_customer".</span><span class="sxs-lookup"><span data-stu-id="a2ac4-176"> For example, if you are interested in a newly created customer, you can look at operationType = “add_customer”.</span></span>  

<span data-ttu-id="a2ac4-177">A operationtype/erőforrások listája az alábbi API-docs alatt található.</span><span class="sxs-lookup"><span data-stu-id="a2ac4-177">List of operationtype/resources can be found in below API docs.</span></span>  

- [<span data-ttu-id="a2ac4-178">Erőforrások naplózása</span><span class="sxs-lookup"><span data-stu-id="a2ac4-178">Auditing resources</span></span>](auditing-resources.md)  

- [<span data-ttu-id="a2ac4-179">Partneri központ-tevékenység rekordjának beolvasása felhasználó szerint</span><span class="sxs-lookup"><span data-stu-id="a2ac4-179">Get a record of a Partner Center activity by user</span></span>](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a><span data-ttu-id="a2ac4-180">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="a2ac4-180">Response example</span></span>

<span data-ttu-id="a2ac4-181">**Kérelem**:</span><span class="sxs-lookup"><span data-stu-id="a2ac4-181">**Request**:</span></span>  
```http
Http Get call:  https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50 

Authorization: Bearer <token> 

Accept: application/json 

MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893 

MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14 

X-Locale: en-US 

Host: api.partnercenter.microsoft.com 

Connection: Keep-Alive 
```

<span data-ttu-id="a2ac4-182">**Válasz**:</span><span class="sxs-lookup"><span data-stu-id="a2ac4-182">**Response**:</span></span>    
```http
{ 

    "totalCount": 17, 

    "items": [ 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_e905b566-4779-4e57-944c-7b1b5312705b_updatecustomeruserlicenses_637346859797753934", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "e905b566-4779-4e57-944c-7b1b5312705b", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "FulfillmentService", 

            "resourceType": "license", 

            "operationType": "update_customer_user_licenses", 

            "operationDate": "2020-09-02T23:26:19.7753934Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "CustomerUserId", 

                    "value": "933808c7-b165-496c-a24e-1a4b7846fab4" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_ia80zlkxp6ewoqpp35pbqjlhqv9iigvz1_createorder_637346662909268372", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "order", 

            "resourceNewValue": "{\"Id\":\"Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"AlternateId\":\"64144d300bde\",\"ReferenceCustomerId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"BillingCycle\":\"monthly\",\"CurrencyCode\":\"USD\",\"CurrencySymbol\":\"$\",\"LineItems\":[{\"LineItemNumber\":0,\"ProvisioningContext\":null,\"OfferId\":\"DZH318Z0C964:0001:DZH318Z0BZDG\",\"SubscriptionId\":\"f428d44a-d08b-348b-579e-ce92a6362c7b\",\"ParentSubscriptionId\":null,\"TermDuration\":\"P1M\",\"TransactionType\":\"New\",\"FriendlyName\":\"SaaS custom meter offer - Bronze\",\"Quantity\":1,\"Pricing\":null,\"PartnerIdOnRecord\":null,\"RenewsTo\":null,\"Links\":{\"Product\":{\"Uri\":\"/products/DZH318Z0C964?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Sku\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Availability\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001/availabilities/DZH318Z0BZDG?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ActivationLinks\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/lineitems/0/activationlinks\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}}}],\"CreationDate\":\"2020-09-02T17:58:01.7755853Z\",\"Status\":\"pending\",\"TransactionType\":\"UserPurchase\",\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ProvisioningStatus\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/provisioningstatus\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"PatchOperation\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"PATCH\",\"Body\":null,\"Headers\":[]}},\"Client\":{\"marketplaceCountry\":\"US\",\"deviceFamily\":\"UniversalStore-PartnerCenter\",\"name\":\"Partner Center Web\"},\"Attributes\":{\"ObjectType\":\"Order\"}}", 

            "operationType": "create_order", 

            "originalCorrelationId": "96514ebe-c1b2-4865-cb46-2c2d20a2e911", 

            "operationDate": "2020-09-02T17:58:10.9268372Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "OrderId", 

                    "value": "Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1" 

                }, 

                { 

                    "key": "AlternateId", 

                    "value": "64144d300bde" 

                }, 

                { 

                    "key": "BillingCycle", 

                    "value": "Monthly" 

                }, 

                { 

                    "key": "OfferId-0", 

                    "value": "DZH318Z0C964:0001:DZH318Z0BZDG" 

                }, 

                { 

                    "key": "SubscriptionId-0", 

                    "value": "f428d44a-d08b-348b-579e-ce92a6362c7b" 

                }, 

                { 

                    "key": "SubscriptionName-0", 

                    "value": "SaaS custom meter offer - Bronze" 

                }, 

                { 

                   "key": "Quantity-0", 

                    "value": "1" 

                }, 

                { 

                    "key": "PartnerOnRecord-0", 

                    "value": null 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                           { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_86bddccf-9a53-40c6-907c-08067a3f8da7_addcustomer_637346648528069005", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "customer", 

            "resourceNewValue": "{\"Id\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"CommerceId\":\"9dd78b4f-f98a-44b4-a2fa-2b82ac58d24c\",\"CompanyProfile\":{\"TenantId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"Domain\":\"CustomMetersStagingTest.onmicrosoft.com\",\"CompanyName\":\"CustomMetersStagingTest\",\"Address\":null,\"Email\":null,\"OrganizationRegistrationNumber\":null,\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/profiles/company\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}},\"Attributes\":{\"ObjectType\":\"CustomerCompanyProfile\"}},\"BillingProfile\":{\"Id\":\"4beafd7b-cdab-5bdc-52ed-02e16edf2e7a\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"Email\":\"CustomMetersStagingTest@CustomMetersStagingTest.com\",\"Culture\":\"en-US\",\"Language\":\"en\",\"CompanyName\":\"CustomMetersStagingTest\",\"DefaultAddress\":{\"Id\":null,\"Country\":\"US\",\"Region\":null,\"City\":\"Seattle\",\"State\":\"WA\",\"District\":null,\"AddressLine1\":\"CustomMetersStagingTest\",\"AddressLine2\":null,\"AddressLine3\":null,\"PostalCode\":\"98122\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"EmailAddress\":null,\"PhoneNumber\":null,\"MiddleName\":null},\"Attributes\":{\"Etag\":\"-2279334701316321663\",\"ObjectType\":\"CustomerBillingProfile\"}},\"RelationshipToPartner\":\"reseller\",\"AllowDelegatedAccess\":true,\"UserCredentials\":{\"userName\":\"admin\",\"password\":\"\"},\"AssociatedPartnerId\":null,\"CustomDomains\":null,\"Attributes\":{\"ObjectType\":\"Customer\"}}", 

            "operationType": "add_customer", 

            "originalCorrelationId": "7550d9ea-e64a-416f-e49b-3670c516cf69", 

            "operationDate": "2020-09-02T17:34:12.8069005Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "PrimaryDomainName", 

                    "value": "CustomMetersStagingTest.onmicrosoft.com" 

                }, 

                { 

                    "key": "Relationship", 

                    "value": "Reseller" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                            

        ... 

    ], 

    "links": { 

        "self": { 

            "uri": "/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50", 

            "method": "GET", 

            "headers": [] 

        } 

    }, 

    "attributes": { 

        "objectType": "Collection" 

    } 

} 
```
 

