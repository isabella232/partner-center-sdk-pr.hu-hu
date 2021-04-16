---
title: Útmutatás az API-szabályozáshoz
description: A Partnerközpont API-kat hívó partnerek számára megtudhatja, hogy mely API-kat befolyásolja a Microsoft API-szabályozása, illetve megismerheti a szabályozás elkerüléséhez vagy jobb kezeléshez ajánlott eljárásokhoz való használatát.
ms.date: 04/14/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: ab1138e19e06111299ab43ea13a6f033274aaa5d
ms.sourcegitcommit: 3c3a21e73aaadf3023cf4c13b09809ceae5f027a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/14/2021
ms.locfileid: "107496144"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a><span data-ttu-id="d9bbd-103">API-szabályozási útmutató a Partnerközpont API-kat hívó partnerek számára</span><span class="sxs-lookup"><span data-stu-id="d9bbd-103">API throttling guidance for partners calling Partner Center APIs</span></span> 

<span data-ttu-id="d9bbd-104">**A következőre érvényes:**</span><span class="sxs-lookup"><span data-stu-id="d9bbd-104">**Applies to**</span></span>

- <span data-ttu-id="d9bbd-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="d9bbd-105">Partner Center</span></span>

<span data-ttu-id="d9bbd-106">A Microsoft API-szabályozást használ, hogy egy időtartományon belül egyenletesebb teljesítményt biztosít a Partnerközpont API-kat hívó partnerek számára.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-106">Microsoft is implementing API throttling to allow more consistent performance within a time span for partners calling the Partner Center APIs.</span></span> <span data-ttu-id="d9bbd-107">A szabályozás korlátozza a szolgáltatásokra vonatkozó kérések számát egy adott időtartományban, hogy megakadályozza az erőforrások túlzott felhasználását.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-107">Throttling limits the number of requests to a service in a time span to prevent overuse of resources.</span></span> <span data-ttu-id="d9bbd-108">Bár Partnerközpont nagy mennyiségű kérést kezelnek, ha néhány partner túl sok kérést intéz, a szabályozás segít fenntartani az optimális teljesítményt és megbízhatóságot minden partner számára.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-108">While Partner Center is designed to handle a high volume of requests, if an overwhelming number of requests occur by few partners, throttling helps maintain optimal performance and reliability for all partners.</span></span>  

<span data-ttu-id="d9bbd-109">A szabályozási korlátok a forgatókönyvtől függően eltérőek lehetnek.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-109">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="d9bbd-110">Ha például nagy mennyiségű írást végez, a szabályozás lehetősége magasabb, mint ha csak olvasási műveleteket hajt végre.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-110">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="what-happens-when-throttling-occurs"></a><span data-ttu-id="d9bbd-111">Mi történik szabályozáskor?</span><span class="sxs-lookup"><span data-stu-id="d9bbd-111">What happens when throttling occurs?</span></span> 

<span data-ttu-id="d9bbd-112">A szabályozási küszöbérték túllépése esetén a Partnerközpont korlátozza az adott ügyféltől származó további kéréseket egy időre.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-112">When a throttling threshold is exceeded, Partner Center limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="d9bbd-113">A szabályozási viselkedés a kérések típusától és számától függ.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-113">Throttling behavior depends on the type and number of requests.</span></span>   

### <a name="common-throttling-scenarios"></a><span data-ttu-id="d9bbd-114">Gyakori szabályozási forgatókönyvek</span><span class="sxs-lookup"><span data-stu-id="d9bbd-114">Common throttling scenarios</span></span> 

<span data-ttu-id="d9bbd-115">Az ügyfelek szabályozásának leggyakoribb okai a következők:</span><span class="sxs-lookup"><span data-stu-id="d9bbd-115">The most common causes of throttling of clients include:</span></span> 

- <span data-ttu-id="d9bbd-116">Egy API-ra vonatkozó nagy számú kérelem partnerbérlő-azonosítónként: egyes Partnerközpont API-k esetében a szabályozást a partnerbérlő azonosítója határozza meg, és ha túl sok hívás vezet ezekhez az API-khoz ugyanazon partnerbérlő-azonosítón, az túllépi a szabályozási küszöbértéket.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-116">**A large number of requests for an API per Partner Tenant ID**: for some Partner Center APIs, throttling is determined by Partner Tenant ID, too many calls to those APIs on the same Partner Tenant ID will result in exceeding the throttling threshold.</span></span>  

- <span data-ttu-id="d9bbd-117">**Egy API-ra** vonatkozó nagy számú kérelem partnerbérlőazonosítónként és ügyfélbérlő-azonosítónként: más API-k esetén a szabályozást a partnerbérlő/ügyfél bérlőazonosítójának kombinációja határozza meg; ilyen esetekben a túl sok hívás ugyanazon ügyfél bérlőazonosítójára való hívás szabályozást eredményez – míg más ügyfelekkel való hívás sikeres lehet.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-117">**A large number of requests for an API per Partner Tenant ID per Customer Tenant ID**: for other APIs, throttling is determined by Partner Tenant ID/Customer Tenant ID combination; in those cases, making too many calls against the same customer tenant ID will result in throttling - while calls against other customers may succeed.</span></span>

## <a name="best-practices-to-avoid-throttling"></a><span data-ttu-id="d9bbd-118">Ajánlott eljárások a szabályozás elkerüléséhez</span><span class="sxs-lookup"><span data-stu-id="d9bbd-118">Best practices to avoid throttling</span></span> 
 
<span data-ttu-id="d9bbd-119">Az olyan programozási eljárások, mint az erőforrások folyamatos lekérdezése a frissítések kereséséhez és az erőforrás-gyűjtemények rendszeres ellenőrzése az új vagy törölt erőforrások kereséséhez nagyobb valószínűséggel vezetnek szabályozáshoz, és rontják az általános teljesítményt.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-119">Programming practices such as continuously polling a resource to check for updates and regularly scanning resource collections to check for new or deleted resources are more likely to lead to throttling and will degrade overall performance.</span></span> <span data-ttu-id="d9bbd-120">Az egyidejű API-hívások nagy számú kérést okozhatnak egységenként, ami a kérelmek szabályozását is okozhatja.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-120">Concurrent API calls may lead to high number of requests per unit time, which will also cause requests to be throttled.</span></span> <span data-ttu-id="d9bbd-121">Ehelyett érdemes a változáskövetést és a változásértesítéseket használni.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-121">You should instead leverage change tracking and change notifications.</span></span> <span data-ttu-id="d9bbd-122">Emellett fel kell tudnia használni a tevékenységnaplókat a változások észleléséhez. [További](get-a-record-of-partner-center-activity-by-user.md) Partnerközpont a tevékenységnaplókban.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-122">Additionally, you should be able to leverage activity logs for detecting changes, see [Partner Center activity logs](get-a-record-of-partner-center-activity-by-user.md) for more information.</span></span>  <span data-ttu-id="d9bbd-123">Javasoljuk a partnereknek, hogy a nagyobb hatékonyság és a szabályozás elkerülése érdekében fontolja meg a tevékenységnapló API használatát.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-123">We highly recommend partners to consider using the activity log API for more efficiency and to avoid throttling.</span></span> <span data-ttu-id="d9bbd-124">A tevékenységnaplók használatának példáját alább láthatja.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-124">See also the example of using activity logs, below.</span></span>

## <a name="best-practices-to-handle-throttling"></a><span data-ttu-id="d9bbd-125">Ajánlott eljárások a szabályozás kezeléshez</span><span class="sxs-lookup"><span data-stu-id="d9bbd-125">Best practices to handle throttling</span></span>

<span data-ttu-id="d9bbd-126">A szabályozás kezelésével kapcsolatban ajánlott eljárások a következők:</span><span class="sxs-lookup"><span data-stu-id="d9bbd-126">The following are best practices for handling throttling:</span></span> 

- <span data-ttu-id="d9bbd-127">Csökkentse a párhuzamosság mértékét.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-127">Reduce the degree of parallelism.</span></span> 
- <span data-ttu-id="d9bbd-128">Csökkentse a hívások gyakoriságát.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-128">Reduce the frequency of calls.</span></span> 
- <span data-ttu-id="d9bbd-129">Kerülje az azonnali újrakéréseket, mert minden kérés a használati korlátokba kerül.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-129">Avoid immediate retries because all requests accrue against your usage limits.</span></span> 

<span data-ttu-id="d9bbd-130">Hibakezelés implementálásakor használja a 429-es HTTP-hibakódot a szabályozásészleléshez.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-130">When you implement error handling, use the HTTP error code 429 to detect throttling.</span></span> <span data-ttu-id="d9bbd-131">A sikertelen válasz tartalmazza a Retry-After fejlécét.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-131">The failed response includes the Retry-After response header.</span></span> <span data-ttu-id="d9bbd-132">A kérelmek a Retry-after késleltetéssel való lekérése a leggyorsabb mód a szabályozás utáni helyreállításra.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-132">Backing off requests using the Retry-after delay is the fastest way to recover from throttling.</span></span> 

<span data-ttu-id="d9bbd-133">Az Újrapróbálkozás késleltetése művelethez tegye a következőket:</span><span class="sxs-lookup"><span data-stu-id="d9bbd-133">To use the Retry-after delay, do the following:</span></span> 

1. <span data-ttu-id="d9bbd-134">Várja meg a másodpercek számát a Retry-After fejlécben.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-134">Wait the number of seconds specified in the Retry-After header.</span></span> 

2. <span data-ttu-id="d9bbd-135">Próbálja újra a kérést.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-135">Retry the request.</span></span>  

3. <span data-ttu-id="d9bbd-136">Ha a kérés 429-es hibakóddal ismét meghiúsul, a rendszer továbbra is le lesz korulva.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-136">If the request fails again with a 429 error code, you are still being throttled.</span></span> <span data-ttu-id="d9bbd-137">Próbálja meg újra az exponenciális leépítést, használja az ajánlott Retry-After, majd próbálja újra a kérést, amíg sikeresen le nem jár.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-137">Retry with Exponential backoff, use the recommended Retry-After delay and retry the request until it succeeds.</span></span>

4. <span data-ttu-id="d9bbd-138">Ha SDK-t használ, kivételt fog kapni a 429-es állapotkóddal a kérés szabályozása esetén.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-138">If you are using SDK you'll receive an exception with status code 429 when your request is being throttled.</span></span> <span data-ttu-id="d9bbd-139">Használja a RetryAfter tulajdonságot a kivételben, majd az idő eltelte után próbálja újra a kérést.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-139">Use the RetryAfter property in the exception and retry the request after the time is elapsed.</span></span>


## <a name="apis-currently-impacted-by-throttling"></a><span data-ttu-id="d9bbd-140">Jelenleg szabályozás által érintett API-k</span><span class="sxs-lookup"><span data-stu-id="d9bbd-140">APIs currently impacted by throttling</span></span>

<span data-ttu-id="d9bbd-141">Hosszú távon a "Partnerközpont" végpontot api.partnercenter.microsoft.com/ API le lesz szabályozásra.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-141">In the long run, every single Partner Center API that calls the endpoint “api.partnercenter.microsoft.com/” will be throttled.</span></span> <span data-ttu-id="d9bbd-142">Jelenleg a szabályozási korlátok csak az alább felsorolt API-kon vannak kényszerítve.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-142">Currently, the throttling limits are only enforced on the APIs listed below.</span></span> <span data-ttu-id="d9bbd-143">Partnerközpont minden API-ra gyűjti a telemetriát, és dinamikusan módosítja a szabályozási korlátokat.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-143">Partner Center will be collecting the telemetry on each of the APIs and will dynamically adjust the throttling limits.</span></span> <span data-ttu-id="d9bbd-144">Az alábbi táblázat azokat az API-kat sorolja fel, amelyeken a szabályozás jelenleg érvényben van.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-144">The following table lists the APIs where throttling is currently enforced.</span></span>  


|<span data-ttu-id="d9bbd-145">**Művelet**</span><span class="sxs-lookup"><span data-stu-id="d9bbd-145">**Operation**</span></span>| <span data-ttu-id="d9bbd-146">**Partnerközpont dokumentációja**</span><span class="sxs-lookup"><span data-stu-id="d9bbd-146">**Partner Center documentation**</span></span>|
|------------------------|----------------------------|
|<span data-ttu-id="d9bbd-147">{baseURL}/v1/customers/{customer_id}/orders</span><span class="sxs-lookup"><span data-stu-id="d9bbd-147">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="d9bbd-148">rendelés létrehozása</span><span class="sxs-lookup"><span data-stu-id="d9bbd-148">create an order</span></span>](create-an-order.md)|
|<span data-ttu-id="d9bbd-149">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span><span class="sxs-lookup"><span data-stu-id="d9bbd-149">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span></span>|[<span data-ttu-id="d9bbd-150">előfizetés váltása</span><span class="sxs-lookup"><span data-stu-id="d9bbd-150">transition a subscription</span></span>](transition-a-subscription.md)|
|<span data-ttu-id="d9bbd-151">{baseURL}/v1/customers/{customer-tenant-id}/orders/{rendelésazonosító}</span><span class="sxs-lookup"><span data-stu-id="d9bbd-151">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span></span>|[<span data-ttu-id="d9bbd-152">bővítmény vásárlása egy előfizetéshez</span><span class="sxs-lookup"><span data-stu-id="d9bbd-152">purchase an addon to a subscription</span></span>](purchase-an-add-on-to-a-subscription.md)|
|<span data-ttu-id="d9bbd-153">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="d9bbd-153">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="d9bbd-154">kosár létrehozása</span><span class="sxs-lookup"><span data-stu-id="d9bbd-154">create a cart</span></span>](create-a-cart.md)|
|<span data-ttu-id="d9bbd-155">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span><span class="sxs-lookup"><span data-stu-id="d9bbd-155">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span></span>|[<span data-ttu-id="d9bbd-156">kosár kijelentkezéskor</span><span class="sxs-lookup"><span data-stu-id="d9bbd-156">checkout a cart</span></span>](checkout-a-cart.md)|
|<span data-ttu-id="d9bbd-157">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="d9bbd-157">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="d9bbd-158">kosár frissítése</span><span class="sxs-lookup"><span data-stu-id="d9bbd-158">update a cart</span></span>](update-a-cart.md)|
|<span data-ttu-id="d9bbd-159">{baseURL}/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/registrations</span><span class="sxs-lookup"><span data-stu-id="d9bbd-159">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span></span>|[<span data-ttu-id="d9bbd-160">előfizetés regisztrálása</span><span class="sxs-lookup"><span data-stu-id="d9bbd-160">register a subscription</span></span>](register-a-subscription.md)|
|<span data-ttu-id="d9bbd-161">{baseURL}/v1/productupgrades</span><span class="sxs-lookup"><span data-stu-id="d9bbd-161">{baseURL}/v1/productupgrades</span></span>|[<span data-ttu-id="d9bbd-162">termékfrissítési entitás létrehozása</span><span class="sxs-lookup"><span data-stu-id="d9bbd-162">create product upgrade entity</span></span>](create-product-upgrade-entity.md)|
|<span data-ttu-id="d9bbd-163">{baseURL}/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/átalakítások</span><span class="sxs-lookup"><span data-stu-id="d9bbd-163">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span> |[<span data-ttu-id="d9bbd-164">próbaverziós előfizetés konvertálása fizetősre</span><span class="sxs-lookup"><span data-stu-id="d9bbd-164">convert a trial subscription to paid</span></span>](convert-a-trial-subscription-to-paid.md)|
|<span data-ttu-id="d9bbd-165">{baseURL}/v1/customers/{customer-tenant-id}</span><span class="sxs-lookup"><span data-stu-id="d9bbd-165">{baseURL}/v1/customers/{customer-tenant-id}</span></span>|[<span data-ttu-id="d9bbd-166">ügyfél lekért azonosítója</span><span class="sxs-lookup"><span data-stu-id="d9bbd-166">get a customer by id</span></span>](get-a-customer-by-id.md)|
|<span data-ttu-id="d9bbd-167">{baseURL}/v1/productUpgrades/jogosultság</span><span class="sxs-lookup"><span data-stu-id="d9bbd-167">{baseURL}/v1/productUpgrades/eligibility</span></span>|[<span data-ttu-id="d9bbd-168">jogosultság a termékfrissítésre</span><span class="sxs-lookup"><span data-stu-id="d9bbd-168">get eligibility for product upgrade</span></span>](get-eligibility-for-product-upgrade.md)|
|<span data-ttu-id="d9bbd-169">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span><span class="sxs-lookup"><span data-stu-id="d9bbd-169">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span></span> |[<span data-ttu-id="d9bbd-170">előfizetés kezelése</span><span class="sxs-lookup"><span data-stu-id="d9bbd-170">manage subscription</span></span>](manage-orders.md#manage-a-subscription)|
|<span data-ttu-id="d9bbd-171">{baseURL}/v1/customers/{customer_id}/subscriptions</span><span class="sxs-lookup"><span data-stu-id="d9bbd-171">{baseURL}/v1/customers/{customer_id}/subscriptions</span></span> |[<span data-ttu-id="d9bbd-172">get-all-of-a-customer-s-subscriptions</span><span class="sxs-lookup"><span data-stu-id="d9bbd-172">get-all-of-a-customer-s-subscriptions</span></span>](get-all-of-a-customer-s-subscriptions.md)|
|<span data-ttu-id="d9bbd-173">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span><span class="sxs-lookup"><span data-stu-id="d9bbd-173">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span></span>|[<span data-ttu-id="d9bbd-174">Egy előfizetés lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="d9bbd-174">Get a subscription by ID</span></span>](get-a-subscription-by-id.md)|
|<span data-ttu-id="d9bbd-175">{baseURL}/v1/customers/{customer_id}/orders</span><span class="sxs-lookup"><span data-stu-id="d9bbd-175">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="d9bbd-176">Az összes ügyfélrendelés lekérte</span><span class="sxs-lookup"><span data-stu-id="d9bbd-176">Get all customer orders</span></span>](get-all-of-a-customer-s-orders.md)|
|<span data-ttu-id="d9bbd-177">{baseURL}/v1/customers/{customer_id}/orders/{order_id}</span><span class="sxs-lookup"><span data-stu-id="d9bbd-177">{baseURL}/v1/customers/{customer_id}/orders/{order_id}</span></span>|[<span data-ttu-id="d9bbd-178">Megrendelés lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="d9bbd-178">Get an order by ID</span></span>](get-an-order-by-id.md)|
|<span data-ttu-id="d9bbd-179">{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus</span><span class="sxs-lookup"><span data-stu-id="d9bbd-179">{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus</span></span>|[<span data-ttu-id="d9bbd-180">Előfizetés kiépítési állapotának lekérése</span><span class="sxs-lookup"><span data-stu-id="d9bbd-180">Get subscription provisioning status</span></span>](get-subscription-provisioning-status.md)|
|<span data-ttu-id="d9bbd-181">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span><span class="sxs-lookup"><span data-stu-id="d9bbd-181">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span></span>|[<span data-ttu-id="d9bbd-182">Rendelések kezelése és előfizetés kezelése</span><span class="sxs-lookup"><span data-stu-id="d9bbd-182">Manage orders and manage a subscription</span></span>](manage-orders.md#manage-a-subscription)|
|<span data-ttu-id="d9bbd-183">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons</span><span class="sxs-lookup"><span data-stu-id="d9bbd-183">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons</span></span>|[<span data-ttu-id="d9bbd-184">Egy előfizetés bővítménylistájának lekérése</span><span class="sxs-lookup"><span data-stu-id="d9bbd-184">Get a list of add-ons for a subscription</span></span>](get-a-list-of-add-ons-for-a-subscription.md)|
|<span data-ttu-id="d9bbd-185">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements</span><span class="sxs-lookup"><span data-stu-id="d9bbd-185">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements</span></span>|[<span data-ttu-id="d9bbd-186">Előfizetés Azure-jogosultságai listájának lekért listája</span><span class="sxs-lookup"><span data-stu-id="d9bbd-186">Get a list of Azure entitlements for a subscription</span></span>](get-a-list-of-azure-entitlements-for-subscription.md)|
|<span data-ttu-id="d9bbd-187">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus</span><span class="sxs-lookup"><span data-stu-id="d9bbd-187">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus</span></span>|[<span data-ttu-id="d9bbd-188">Előfizetés regisztrációs állapotának lekérése</span><span class="sxs-lookup"><span data-stu-id="d9bbd-188">Get subscription registration status</span></span>](get-subscription-registration-status.md)|
|<span data-ttu-id="d9bbd-189">{baseURL}/v1/customers/{customer-tenant-id}/transfers</span><span class="sxs-lookup"><span data-stu-id="d9bbd-189">{baseURL}/v1/customers/{customer-tenant-id}/transfers</span></span>|[<span data-ttu-id="d9bbd-190">Az ügyfél összes átutalásának lekért része</span><span class="sxs-lookup"><span data-stu-id="d9bbd-190">Get all of a customer's transfers</span></span>](get-all-of-a-customer-s-transfers.md)|
|<span data-ttu-id="d9bbd-191">{baseURL}/v1/productUpgrades/{upgrade-id}/status</span><span class="sxs-lookup"><span data-stu-id="d9bbd-191">{baseURL}/v1/productUpgrades/{upgrade-id}/status</span></span>|[<span data-ttu-id="d9bbd-192">Termék frissítési állapotának lekérése</span><span class="sxs-lookup"><span data-stu-id="d9bbd-192">Get product upgrade status</span></span>](get-product-upgrade-status.md)|
|<span data-ttu-id="d9bbd-193">{baseURL}/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/átalakítások</span><span class="sxs-lookup"><span data-stu-id="d9bbd-193">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span>|[<span data-ttu-id="d9bbd-194">A próbaverzió átalakításával kapcsolatos ajánlatok listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="d9bbd-194">Get a list of trial conversion offers</span></span>](get-a-list-of-trial-conversion-offers.md)|


### <a name="error-code-response"></a><span data-ttu-id="d9bbd-195">Hibakód válasza:</span><span class="sxs-lookup"><span data-stu-id="d9bbd-195">Error code response:</span></span>
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a><span data-ttu-id="d9bbd-196">Példa tevékenységnaplóra</span><span class="sxs-lookup"><span data-stu-id="d9bbd-196">Example of activity log</span></span>

<span data-ttu-id="d9bbd-197">A napi módosítások elemzésének ajánlott eljárása az, ha egy adott napra vonatkozó naplórekordot kell lekérdezni.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-197">For best practice in analyzing daily changes, we recommend that you query audit record for a specific day.</span></span> 

<span data-ttu-id="d9bbd-198">A válaszban egy adott művelettípusra módosuló eredményt fog kapni.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-198">In the response, you will get a result with changes to specific operation type.</span></span><span data-ttu-id="d9bbd-199">Az Ön számára fontos művelet alapján szűrhet.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-199">  You can filter based on the operation you care about.</span></span> <span data-ttu-id="d9bbd-200">Ha például egy újonnan létrehozott ügyfél érdekli, az operationType = "add_customer" add_customer.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-200"> For example, if you are interested in a newly created customer, you can look at operationType = “add_customer”.</span></span>  

<span data-ttu-id="d9bbd-201">Az operationtype/resources listája az alábbi API-dokumentumokban található.</span><span class="sxs-lookup"><span data-stu-id="d9bbd-201">List of operationtype/resources can be found in below API docs.</span></span>  

- [<span data-ttu-id="d9bbd-202">Erőforrások naplózása</span><span class="sxs-lookup"><span data-stu-id="d9bbd-202">Auditing resources</span></span>](auditing-resources.md)  

- [<span data-ttu-id="d9bbd-203">Felhasználó által Partnerközpont rekord lekért rekordja</span><span class="sxs-lookup"><span data-stu-id="d9bbd-203">Get a record of a Partner Center activity by user</span></span>](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a><span data-ttu-id="d9bbd-204">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d9bbd-204">Response example</span></span>

<span data-ttu-id="d9bbd-205">**Kérés:**</span><span class="sxs-lookup"><span data-stu-id="d9bbd-205">**Request**:</span></span>  
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

<span data-ttu-id="d9bbd-206">**Válasz:**</span><span class="sxs-lookup"><span data-stu-id="d9bbd-206">**Response**:</span></span>    
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
 

