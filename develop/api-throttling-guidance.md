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
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a>API-szabályozási útmutató a partner Center API-kat hívó partnereknek 

**A következőre érvényes:**

- Partnerközpont

A Microsoft olyan API-szabályozást valósít meg, amely a partner Center API-kat hívó partnereink számára egy adott időszakon belül nagyobb konzisztens teljesítményt tesz lehetővé. A szabályozás korlátozza a szolgáltatásra irányuló kérések számát egy adott időszakban, hogy elkerülje az erőforrások túlzott mennyiségét. Míg a partneri központ nagy mennyiségű kérés kezelésére van kialakítva, ha a kérések túlnyomó száma kevés partnernél fordul elő, a szabályozás segít fenntartani az optimális teljesítményt és megbízhatóságot az összes partner számára.  

A szabályozás korlátai a forgatókönyv alapján változnak. Ha például nagy mennyiségű írást végez, a szabályozás lehetősége magasabb, mint ha csak olvasást végez.

## <a name="what-happens-when-throttling-occurs"></a>Mi történik a szabályozás esetén? 

Ha túllépi a szabályozási küszöbértéket, a partneri központ egy adott időszakra korlátozza az ügyféltől érkező további kéréseket. A szabályozás viselkedése a kérelmek típusától és számától függ.   

### <a name="common-throttling-scenarios"></a>Gyakori szabályozási forgatókönyvek 

Az ügyfelek szabályozásának leggyakoribb okai a következők: 

- **Nagyszámú kérelem egy adott API-hoz tartozó partneri bérlői azonosítóhoz**: egyes partneri központ API-k esetében a szabályozást a partner bérlői azonosítója határozza meg, az API-k ugyanazon partner BÉRLŐi azonosítóján túl sok hívást eredményez a sávszélesség-szabályozási küszöbérték túllépése.  

- **Nagyszámú kérelem egy ügyfél**-BÉRLŐi azonosítóhoz a Customer bérlői azonosítója alapján: más API-k esetén a szabályozást a partner bérlő azonosítója/ügyfél bérlői azonosítója határozza meg. Ezekben az esetekben előfordulhat, hogy az azonos ügyfél-bérlői AZONOSÍTÓval való túl sok hívás a szabályozást eredményezi, míg a más ügyfelek felé irányuló hívások sikeresek lesznek.

## <a name="best-practices-to-avoid-throttling"></a>Ajánlott eljárások a szabályozás elkerüléséhez 
 
Programozási eljárások, például az erőforrások folyamatos lekérdezése a frissítések kereséséhez és az erőforrások rendszeres vizsgálatához az új vagy törölt erőforrások ellenőrzéséhez nagyobb valószínűséggel vezethet a szabályozáshoz, és csökkenti a teljes teljesítményt. Az egyidejű API-hívások nagy mennyiségű kérést okozhatnak az egységnyi idő alatt, ami a kérelmek szabályozását is eredményezi. Ehelyett a Change Tracking és a Change Notifications szolgáltatást kell használnia. Ezen kívül a változások észleléséhez is képesnek kell lennie a Tevékenységnaplók kihasználása érdekében további információért lásd a [partneri központ tevékenységi naplóit](get-a-record-of-partner-center-activity-by-user.md) .  Kifejezetten ajánljuk a partnereknek a Tevékenységnaplók API használatát a hatékonyság és a szabályozás elkerülése érdekében. Lásd még a következő példa a tevékenység-naplók használatára című szakaszt.

## <a name="best-practices-to-handle-throttling"></a>Ajánlott eljárások a szabályozás kezeléséhez

A következő ajánlott eljárások a szabályozás kezeléséhez: 

- Csökkentse a párhuzamosság mértékét. 
- Csökkentse a hívások gyakoriságát. 
- Kerülje az azonnali újrapróbálkozásokat, mert az összes kérelem a használati korlátok között van. 

Hibakezelés implementálásakor használja a 429-es HTTP-hibakódot a szabályozásészleléshez. A sikertelen válasz tartalmazza a Retry-After válasz fejlécét. A kérelmeknek az újrapróbálkozást követő késleltetéssel történő biztonsági mentése a lehető leggyorsabb módszer a szabályozás helyreállítására. 

Az újrapróbálkozás utáni késleltetés használatához tegye a következőket: 

1. Várjon a Retry-After fejlécben megadott másodpercek számát. 

2. Próbálja megismételni a kérelmet.  

3. Ha a kérelem 429-es hibakóddal meghiúsul, továbbra is szabályozva lesz. Próbálkozzon újra az exponenciális leállítási, használja az ajánlott Retry-After késleltetést, majd ismételje meg a kérést, amíg a művelet be nem fejeződik.

4. Ha az SDK-t használja, akkor az 429-es állapotkód kivételt fog kapni, ha a kérelmét szabályozzák. A kivételben használja a RetryAfter tulajdonságot, és ismételje meg a kérést az idő lejárta után.


## <a name="apis-currently-impacted-by-throttling"></a>A szabályozás által jelenleg érintett API-k

Hosszú távon a "api.partnercenter.microsoft.com/" végpontot meghívó minden egyes partner Center API szabályozva lesz. Jelenleg a szabályozás korlátozásai csak az alább felsorolt API-k esetében érvényesülnek. A partner Center összegyűjti a telemetria az egyes API-kkal, és dinamikusan módosítja a sávszélesség-szabályozási korlátokat. A következő táblázat felsorolja azokat az API-kat, amelyeken a szabályozás jelenleg érvényben van.  


|**Művelet**| **Partnerközpont dokumentációja**|       
|------------------------|----------------------------|
|{baseURL}/v1/Customers/{customer_id}:/Orders|[megrendelés létrehozása](create-an-order.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades|[előfizetés átváltása](transition-a-subscription.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}|[addon vásárlása egy előfizetéshez](purchase-an-add-on-to-a-subscription.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}|[kosár létrehozása](create-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout|[kosár kifizetése](checkout-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}|[kosár frissítése](update-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations|[előfizetés regisztrálása](register-a-subscription.md)|
|{baseURL}/v1/productupgrades|[termék verziófrissítési entitásának létrehozása](create-product-upgrade-entity.md)|
|{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions |[próbaverziós előfizetés átalakítása fizetős verzióra](convert-a-trial-subscription-to-paid.md)|
|{baseURL}/v1/customers/{customer-tenant-id}|[ügyfél beszerzése azonosító alapján](get-a-customer-by-id.md)|
|{baseURL}/v1/productUpgrades/eligibility|[a termék frissítésére vonatkozó jogosultság beszerzése](get-eligibility-for-product-upgrade.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} |[előfizetés kezelése](manage-orders.md#manage-a-subscription)|


### <a name="error-code-response"></a>Hibakód válasza:
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a>Műveletnapló – példa

Ajánlott eljárás a napi változások elemzésekor azt javasoljuk, hogy egy adott napra vonatkozóan kérdezze le a naplózási rekordot. 

A válaszban egy adott Művelettípus változásait fogja kapni.Az Ön számára fontos művelet alapján szűrheti a szűrőt. Ha például egy újonnan létrehozott ügyfelet érdekli, tekintse meg a következőt: operationType = "add_customer".  

A operationtype/erőforrások listája az alábbi API-docs alatt található.  

- [Erőforrások naplózása](auditing-resources.md)  

- [Partneri központ-tevékenység rekordjának beolvasása felhasználó szerint](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a>Példa válaszra

**Kérelem**:  
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

**Válasz**:    
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
 

