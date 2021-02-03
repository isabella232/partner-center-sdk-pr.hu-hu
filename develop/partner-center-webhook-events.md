---
title: A partner Center webhook eseményei
description: A partner Center által támogatott összes webhook-esemény dokumentációja.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 5358aab8efdd68ad52c583936304f99ffae12708
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768040"
---
# <a name="partner-center-webhook-events"></a>A partner Center webhook eseményei

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A partner Center webhook eseményei a HTTP-bejegyzések formájában a regisztrált URL-címre küldött erőforrás-változási események. A partneri központból érkező események fogadásához olyan visszahívást kell futtatni, amelyben a partner Center közzéteheti az eseményt. Az esemény digitálisan alá van írva, így ellenőrizheti, hogy a partner központból küldték-e el.

További információ az események fogadásáról, a visszahívás hitelesítéséről, valamint a partneri központ webhook API-k használatával az események regisztrálásának létrehozásához, megtekintéséhez és frissítéséhez: a [partner Center webhookok](partner-center-webhooks.md).

## <a name="supported-events"></a>Támogatott események

A partner Center a következő webhook-eseményeket támogatja.

### <a name="test-event"></a>Esemény tesztelése

Ez az esemény lehetővé teszi, hogy saját bevezetést kérjen, és tesztelje a regisztrációt egy tesztelési esemény megadásával, majd a folyamat nyomon követésével. Megtekintheti a Microsofttól érkező hibaüzeneteket, amikor az eseményt megpróbálja kézbesíteni. Ez a művelet csak a "test-created" eseményekre és a 7 napnál régebbi adatértékekre vonatkozik.

>[!NOTE]
>Egy teszt által létrehozott esemény elküldésekor percenként 2 kérelem van.

#### <a name="properties"></a>Tulajdonságok

| Tulajdonság                  | Típus                               | Leírás                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sztring                             | Az esemény neve. A (z) {Resource} – {Action} formátumban. Ebben az esetben az érték "test-created".                                          |
| ResourceUri               | URI                                | Az erőforrás beolvasására szolgáló URI. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/Registration/validationEvents/{{correlationId}}" |
| ResourceName nevű erőforrásáról              | sztring                             | Annak az erőforrásnak a neve, amely elindítja az eseményt. Ebben az esetben az érték "test".                                  |
| AuditUri                  | URI                                | Választható A naplózási rekord beolvasására szolgáló URI, ha van ilyen. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | karakterlánc az UTC dátum-idő formátumban | Az erőforrás változásának dátuma és időpontja.                                                         |

#### <a name="example"></a>Példa

```json
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{{CorrelationId}}",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="subscription-updated-event"></a>Előfizetés frissített eseménye

Ez az esemény akkor következik be, amikor a megadott előfizetés megváltozik. Az előfizetés frissített eseménye akkor jön létre, ha a partner Center API-n keresztül végzett módosítások mellett belső módosítás is történik.  Ez az esemény csak akkor jön létre, ha a kereskedelmi szint megváltozik, például ha a licencek száma módosítva lesz, és az előfizetés állapota megváltozik. Nem jön létre, ha az erőforrás az előfizetésen belül jön létre.

>[!NOTE]
>Az előfizetés változásai és az előfizetés frissített eseményének megváltozása közötti időtartam 48 óra.

#### <a name="properties"></a>Tulajdonságok

| Tulajdonság                  | Típus                               | Leírás                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sztring                             | Az esemény neve. A (z) {Resource} – {Action} formátumban. Ebben az esetben az érték az "előfizetés frissítve".                                  |
| ResourceUri               | URI                                | Az erőforrás beolvasására szolgáló URI. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/Customers/{{CustomerId}}/Subscriptions/{{SubscriptionId}}" |
| ResourceName nevű erőforrásáról              | sztring                             | Annak az erőforrásnak a neve, amely elindítja az eseményt. Ebben az esetben az érték az "előfizetés".                          |
| AuditUri                  | URI                                | Választható A naplózási rekord beolvasására szolgáló URI, ha van ilyen. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | karakterlánc az UTC dátum-idő formátumban | Az erőforrás változásának dátuma és időpontja.                                                         |

#### <a name="example"></a>Példa

```json
{
    "EventName": "subscription-updated",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}",
    "ResourceName": "subscription",
    "AuditUri": "https://api.partnercenter.microsoft.com/v1/auditrecords/{{AuditId}}",
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="threshold-exceeded-event"></a>Túllépte a küszöbértéket (esemény)

Ez az esemény akkor következik be, ha az ügyfél Microsoft Azure használatának mennyisége meghaladja a használati költségekkel kapcsolatos költségvetést (a küszöbértéket). További információ: [Azure-beli kiadások költségvetésének beállítása ügyfeleinek/partner-központ/set-an-Azure-költőpénzt-Budget-for-your-Customs).

#### <a name="properties"></a>Tulajdonságok

| Tulajdonság                  | Típus                               | Leírás                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sztring                             | Az esemény neve. A (z) {Resource} – {Action} formátumban. Ebben az esetben az érték a következő: "usagerecords-thresholdExceeded".                                  |
| ResourceUri               | URI                                | Az erőforrás beolvasására szolgáló URI. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/Customers/usagerecords" |
| ResourceName nevű erőforrásáról              | sztring                             | Annak az erőforrásnak a neve, amely elindítja az eseményt. Ebben az esetben az érték "usagerecords".                          |
| AuditUri                  | URI                                | Választható A naplózási rekord beolvasására szolgáló URI, ha van ilyen. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | karakterlánc az UTC dátum-idő formátumban | Az erőforrás változásának dátuma és időpontja.                                                         |

#### <a name="example"></a>Példa

```json
{
    "EventName": "usagerecords-thresholdExceeded",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/customers/usagerecords",
    "ResourceName": "usagerecords",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-created-event"></a>Hivatkozó létrehozott esemény

Ez az esemény az átirányítás létrehozásakor következik be.

#### <a name="properties"></a>Tulajdonságok

| Tulajdonság                  | Típus                               | Leírás                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sztring                             | Az esemény neve. A (z) {Resource} – {Action} formátumban. Ebben az esetben az érték "hivatkozó-létrehozva".                                  |
| ResourceUri               | URI                                | Az erőforrás beolvasására szolgáló URI. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/Referrals/{{ReferralID}}" |
| ResourceName nevű erőforrásáról              | sztring                             | Annak az erőforrásnak a neve, amely elindítja az eseményt. Ebben az esetben az érték az "ajánló".                          |
| AuditUri                  | URI                                | Választható A naplózási rekord beolvasására szolgáló URI, ha van ilyen. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | karakterlánc az UTC dátum-idő formátumban | Az erőforrás változásának dátuma és időpontja.                                                         |

#### <a name="example"></a>Példa

```json
{
    "EventName": "referral-created",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-updated-event"></a>Hivatkozó frissített esemény

Ez az esemény az átirányítás frissítésekor következik be.

#### <a name="properties"></a>Tulajdonságok

| Tulajdonság                  | Típus                               | Leírás                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sztring                             | Az esemény neve. A (z) {Resource} – {Action} formátumban. Ebben az esetben az érték "referral-frissítve".                                  |
| ResourceUri               | URI                                | Az erőforrás beolvasására szolgáló URI. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/Referrals/{{ReferralID}}" |
| ResourceName nevű erőforrásáról              | sztring                             | Annak az erőforrásnak a neve, amely elindítja az eseményt. Ebben az esetben az érték az "ajánló".                          |
| AuditUri                  | URI                                | Választható A naplózási rekord beolvasására szolgáló URI, ha van ilyen. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | karakterlánc az UTC dátum-idő formátumban | Az erőforrás változásának dátuma és időpontja.                                                         |

#### <a name="example"></a>Példa

```json
{
    "EventName": "referral-updated",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="invoice-ready-event"></a>Számla üzemkész eseménye

Ez az esemény akkor következik be, amikor az új számla elkészült.

| Tulajdonság                  | Típus                               | Leírás                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | sztring | Az esemény neve. A (z) {Resource} – {Action} formátumban. Ebben az esetben az érték "számla-kész". |
| ResourceUri | URI | Az erőforrás beolvasására szolgáló URI. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{{InvoiceId}}" |
| ResourceName nevű erőforrásáról | sztring | Annak az erőforrásnak a neve, amely elindítja az eseményt. Ebben az esetben az érték a "számla". |
| AuditUri |  URI | Választható A naplózási rekord beolvasására szolgáló URI, ha van ilyen. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}") |
| ResourceChangeUtcDate | karakterlánc az UTC dátum-idő formátumban | Az erőforrás változásának dátuma és időpontja. |

#### <a name="example"></a>Példa

```json
{
    "EventName": "invoice-ready",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/invoices/{{InvoiceId}}",
    "ResourceName": "invoice",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}

```
