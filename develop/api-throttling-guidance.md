---
title: Útmutatás az API-szabályozáshoz
description: A Partnerközpont API-kat hívó partnerek számára megtudhatja, hogy mely API-kat befolyásolja a Microsoft API-szabályozása, illetve megismerheti a szabályozás elkerüléséhez vagy jobb kezeléshez ajánlott eljárásokhoz való használatát.
ms.date: 04/14/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: f18518e88b9bb08d4fd248922f4ce2fefdde004f
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025649"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a>API-szabályozási útmutató a Partnerközpont API-kat hívó partnerek számára 

A Microsoft API-szabályozást használ, hogy egy időtartományon belül egyenletesebb teljesítményt biztosít a Partnerközpont API-kat hívó partnerek számára. A szabályozás korlátozza a szolgáltatásokra vonatkozó kérések számát egy adott időtartományban, hogy megakadályozza az erőforrások túlzott felhasználását. Bár Partnerközpont nagy mennyiségű kérést kezelnek, ha néhány partner túl sok kérést intéz, a szabályozás segít fenntartani az optimális teljesítményt és megbízhatóságot minden partner számára.  

A szabályozási korlátok a forgatókönyvtől függően eltérőek lehetnek. Ha például nagy mennyiségű írást hajt végre, a szabályozás lehetősége magasabb, mint ha csak olvasási műveleteket hajt végre.

## <a name="what-happens-when-throttling-occurs"></a>Mi történik szabályozáskor? 

A szabályozási küszöbérték túllépése esetén a Partnerközpont korlátozza az adott ügyféltől származó további kéréseket egy időre. A szabályozási viselkedés a kérések típusától és számától függ.   

### <a name="common-throttling-scenarios"></a>Gyakori szabályozási forgatókönyvek 

Az ügyfelek szabályozásának leggyakoribb okai a következők: 

- Az API-k nagy száma partnerbérlő-azonosítónként: egyes Partnerközpont API-k esetében a szabályozást a partnerbérlő azonosítója határozza meg, és ha túl sok hívás hívja meg ezeket az **API-kat** ugyanazon partnerbérlő-azonosítón, az túllépi a szabályozási küszöbértéket.  

- **Egy API-ra** vonatkozó nagy számú kérelem partnerbérlőazonosítónként és ügyfélbérlő-azonosítónként: más API-k esetén a szabályozást a partnerbérlő/ügyfél bérlőazonosítójának kombinációja határozza meg; ilyen esetekben a túl sok hívás ugyanazon ügyfél bérlőazonosítójára való hívás szabályozást eredményez – míg más ügyfelekkel való hívás sikeres lehet.

## <a name="best-practices-to-avoid-throttling"></a>Ajánlott eljárások a szabályozás elkerüléséhez 
 
Az olyan programozási eljárások, mint például az erőforrások folyamatos lekérdezése frissítések kereséséhez és az erőforrás-gyűjtemények rendszeres vizsgálatával az új vagy törölt erőforrások kereséséhez nagyobb valószínűséggel vezetnek szabályozáshoz, és rontják az általános teljesítményt. Az egyidejű API-hívások nagy számú kérést okozhatnak egységenként, ami a kérelmek szabályozását is okozhatja. Ehelyett változáskövetést és változásértesítéseket használjon. Emellett képesnek kell lennie a tevékenységnaplók használatára a változások észleléséhez. További információkért lásd: Partnerközpont [tevékenységnaplók.](get-a-record-of-partner-center-activity-by-user.md)  Javasoljuk a partnereknek, hogy a nagyobb hatékonyság és a szabályozás elkerülése érdekében fontolja meg a tevékenységnapló API használatát. Az alábbiakban a tevékenységnaplók használatának példáját is láthatja.

## <a name="best-practices-to-handle-throttling"></a>Ajánlott eljárások a szabályozás kezeléshez

A szabályozás kezelésével kapcsolatban az alábbi ajánlott eljárások ímek: 

- Csökkentse a párhuzamosság mértékét. 
- Csökkentse a hívások gyakoriságát. 
- Kerülje az azonnali újrakéréseket, mert minden kérés a használati korlátokhoz van felhalmozott. 

Hibakezelés implementálásakor használja a 429-es HTTP-hibakódot a szabályozásészleléshez. A sikertelen válasz tartalmazza a Retry-After válaszfejlécét. A kérelmek visszahelyezése a Retry-after késleltetéssel a leggyorsabb módszer a szabályozás utáni helyreállításra. 

Az Újrapróbálkozás késleltetésének használata érdekében tegye a következőket: 

1. Várjon az oszlopfejlécben megadott Retry-After. 

2. Próbálja újra a kérést.  

3. Ha a kérés 429-es hibakóddal ismét meghiúsul, a rendszer továbbra is le lesz korkorulva. Próbálja meg újra az exponenciális leépítést, használja a javasolt Retry-After, majd próbálja újra a kérést, amíg sikerrel nem jár.

4. Ha az SDK-t használja, kivételt kap a 429-es állapotkóddal a kérelem szabályozásakor. Használja a RetryAfter tulajdonságot a kivételben, és próbálja meg újra a kérést az idő eltelte után.


## <a name="apis-currently-impacted-by-throttling"></a>Jelenleg szabályozás által érintett API-k

Végül minden egyes api Partnerközpont, amely a "api.partnercenter.microsoft.com/" végpontot hívja meg, le lesz szabályozással. Jelenleg a szabályozási korlátok csak az alább felsorolt API-kon vannak kényszerítve. Partnerközpont minden API-ra gyűjti a telemetriát, és dinamikusan módosítja a szabályozási korlátokat. Az alábbi táblázat azokat az API-kat sorolja fel, amelyeken a szabályozás jelenleg érvényben van.  


|**Művelet**| **Partnerközpont dokumentációja**|
|------------------------|----------------------------|
|{baseURL}/v1/customers/{customer_id}/orders|[rendelés létrehozása](create-an-order.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades|[előfizetés váltása](transition-a-subscription.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/orders/{rendelésazonosító}|[bővítmény vásárlása egy előfizetéshez](purchase-an-add-on-to-a-subscription.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}|[kosár létrehozása](create-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout|[kosár kijelentkezéskor](checkout-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}|[kosár frissítése](update-a-cart.md)|
|{baseURL}/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/registrations|[előfizetés regisztrálása](register-a-subscription.md)|
|{baseURL}/v1/productupgrades|[termékfrissítési entitás létrehozása](create-product-upgrade-entity.md)|
|{baseURL}/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/átalakítások |[próbaverziós előfizetés konvertálása fizetősre](convert-a-trial-subscription-to-paid.md)|
|{baseURL}/v1/customers/{customer-tenant-id}|[ügyfél lekért azonosítója](get-a-customer-by-id.md)|
|{baseURL}/v1/productUpgrades/jogosultság|[termékfrissítésre való jogosultság lekért](get-eligibility-for-product-upgrade.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} |[előfizetés kezelése](manage-orders.md#manage-a-subscription)|
|{baseURL}/v1/customers/{customer_id}/subscriptions |[get-all-of-a-customer-s-subscriptions](get-all-of-a-customer-s-subscriptions.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}|[Egy előfizetés lekérése azonosító alapján](get-a-subscription-by-id.md)|
|{baseURL}/v1/customers/{customer_id}/orders|[Az összes ügyfélrendelés lekérte](get-all-of-a-customer-s-orders.md)|
|{baseURL}/v1/customers/{customer_id}/orders/{order_id}|[Megrendelés lekérése azonosító alapján](get-an-order-by-id.md)|
|{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus|[Előfizetés kiépítési állapotának lekérése](get-subscription-provisioning-status.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}|[Rendelések kezelése és előfizetés kezelése](manage-orders.md#manage-a-subscription)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons|[Egy előfizetés bővítménylistájának lekérése](get-a-list-of-add-ons-for-a-subscription.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements|[Előfizetés Azure-jogosultságai listájának lekért listája](get-a-list-of-azure-entitlements-for-subscription.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus|[Előfizetés regisztrációs állapotának lekérése](get-subscription-registration-status.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/transfers|[Az ügyfél összes átutalásának lekért része](get-all-of-a-customer-s-transfers.md)|
|{baseURL}/v1/productUpgrades/{upgrade-id}/status|[Termék frissítési állapotának lekérése](get-product-upgrade-status.md)|
|{baseURL}/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/átalakítások|[A próbaverzió átalakításával kapcsolatos ajánlatok listájának lekérése](get-a-list-of-trial-conversion-offers.md)|


### <a name="error-code-response"></a>Hibakód válasza:
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a>Példa tevékenységnaplóra

A napi módosítások elemzésének ajánlott eljárása az, ha egy adott napra vonatkozó naplórekordot kell lekérdezni. 

A válaszban egy adott művelettípusra módosuló eredményt fog kapni.Az Ön számára fontos művelet alapján szűrhet. Ha például egy újonnan létrehozott ügyfél érdekli, az operationType = "add_customer" add_customer.  

Az operationtype/resources listája az alábbi API-dokumentumokban található.  

- [Erőforrások naplózása](auditing-resources.md)  

- [Felhasználó által végzett Partnerközpont rekord lekérte](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a>Példa válaszra

**Kérés:**  
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

**Válasz:**    
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
 

