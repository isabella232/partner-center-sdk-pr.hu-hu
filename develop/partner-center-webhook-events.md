---
title: Partnerközpont webhookesemények
description: Megtudhatja, hogyan teszteli és használhatja a webhookeseményeket, és hogyan jegyezze fel, ha az előfizetések és egyéb események megváltoznak a Partnerközpont.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: e5e363a2f928dd38304887547bdc0e5d652728d6
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547740"
---
# <a name="partner-center-webhook-events"></a>Partnerközpont webhookesemények

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Partnerközpont webhookesemények http POST-ként egy regisztrált URL-címre kézbesített erőforrás-módosítási események. Ha egy esemény fogadása a Partnerközpont, olyan visszahívási eseményt kell fogadnia, Partnerközpont postán is közzétenné az eseményt. Az esemény digitális aláírással van aláírva, így ellenőrizheti, hogy a rendszer elküldte-e Partnerközpont.

Az események fogadására, a visszahívások hitelesítésére, valamint az Partnerközpont webhook API-k eseményregisztráció létrehozására, megtekintésére és frissítésére való használatával kapcsolatos információkért lásd: Partnerközpont [webhookok.](partner-center-webhooks.md)

## <a name="supported-events"></a>Támogatott események

A következő webhookeseményeket támogatja a Partnerközpont.

### <a name="test-event"></a>Tesztesemény

Ez az esemény lehetővé teszi, hogy önkiszolgálóan regisztrálja és tesztelje a regisztrációt egy tesztesemény lekért kérésével, majd nyomon követi a folyamat előrehaladását. Látni fogja a Microsofttól az esemény kézbesítése közben kapott hibaüzeneteket. Ez csak a "teszt által létrehozott" eseményekre vonatkozik, és a hét napnál régebbi adatokat a rendszer kiüríti.

>[!NOTE]
>A teszt által létrehozott események kihirdetésekor percenként 2 kérelemre van korlátozás.

#### <a name="properties"></a>Tulajdonságok

| Tulajdonság                  | Típus                               | Leírás                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sztring                             | Az esemény neve. A következő űrlapon: {resource}-{action}. Ehhez az eseményhez az érték "test-created".                                          |
| ResourceUri (Erőforrás-azonosító)               | URI                                | Az erőforrás lekért URI-ját. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/registration/validationEvents/{{CorrelationId}}" |
| ResourceName nevű erőforrásáról              | sztring                             | Az eseményt aktiváló erőforrás neve. Ebben az eseményben az érték "test".                                  |
| AuditUri                  | URI                                | (Nem kötelező) A naplórekord lekért URI-ját, ha létezik. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | sztring az UTC dátum-idő formátumban | Az erőforrás-módosítás dátuma és időpontja.                                                         |

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

Ez az esemény akkor történik, amikor a megadott előfizetés megváltozik. A Subscription Updated (Előfizetés frissítve) esemény akkor jön létre, ha belső változás történik azon felül, hogy mikor történik módosítás a Partnerközpont API-n keresztül.  Ez az esemény csak akkor jön létre, ha a kereskedelmi szint módosul, például ha a licencek száma módosul, és az előfizetés állapota megváltozik. Nem jön létre, amikor erőforrások jönnek létre az előfizetésen belül.

>[!NOTE]
>Akár 48 órás késés is lehet az előfizetés változásának és az Előfizetés frissítése esemény aktiválásának ideje között.

#### <a name="properties"></a>Tulajdonságok

| Tulajdonság                  | Típus                               | Leírás                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sztring                             | Az esemény neve. A következő űrlapon: {resource}-{action}. Ebben az eseményben az érték "subscription-updated".                                  |
| ResourceUri (Erőforrás-azonosító)               | URI                                | Az erőforrás lekért URI-ját. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}" |
| ResourceName nevű erőforrásáról              | sztring                             | Az eseményt aktiváló erőforrás neve. Ebben az eseményben az érték "subscription".                          |
| AuditUri                  | URI                                | (Nem kötelező) A naplórekord lekért URI-ját, ha létezik. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | sztring az UTC dátum-idő formátumban | Az erőforrás-módosítás dátuma és időpontja.                                                         |

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

### <a name="threshold-exceeded-event"></a>Küszöbérték túllépve esemény

Ez az esemény akkor lép fel, Microsoft Azure bármely ügyfél használati költségének kihasználtsága meghaladja a használati költségkeretet (a küszöbértéküket). További információ: [Azure-költségvetés beállítása az ügyfelek számára/partner-központ/set-an-azure-spending-budget-for-your-customers).

#### <a name="properties"></a>Tulajdonságok

| Tulajdonság                  | Típus                               | Leírás                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sztring                             | Az esemény neve. A következő űrlapon: {resource}-{action}. Ebben az esetben az érték "usagerecords-thresholdExceeded".                                  |
| ResourceUri (Erőforrás-azonosító)               | URI                                | Az erőforrás lekért URI-ját. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/usagerecords" |
| ResourceName nevű erőforrásáról              | sztring                             | Az eseményt aktiváló erőforrás neve. Ebben az esetben az érték "usagerecords".                          |
| AuditUri                  | URI                                | (Nem kötelező) A naplórekord lekért URI-ját, ha létezik. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | sztring az UTC dátum-idő formátumban | Az erőforrás-módosítás dátuma és időpontja.                                                         |

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

### <a name="referral-created-event"></a>Hivatkozás által létrehozott esemény

Ez az esemény a hivatkozás létrehozásakor jön létre.

#### <a name="properties"></a>Tulajdonságok

| Tulajdonság                  | Típus                               | Leírás                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sztring                             | Az esemény neve. A következő űrlapon: {resource}-{action}. Ebben az esetben az érték "referral-created".                                  |
| ResourceUri (Erőforrás-azonosító)               | URI                                | Az erőforrás lekért URI-ját. A következő szintaxist használja:[*" {baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName nevű erőforrásáról              | sztring                             | Az eseményt aktiváló erőforrás neve. Ebben az esetben az érték "hivatkozás".                          |
| AuditUri                  | URI                                | (Nem kötelező) A naplórekord lekért URI-ját, ha létezik. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | sztring az UTC dátum-idő formátumban | Az erőforrás-módosítás dátuma és időpontja.                                                         |

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

### <a name="referral-updated-event"></a>Ajánló frissített eseménye

Ez az esemény a hivatkozás frissítésekor történik.

#### <a name="properties"></a>Tulajdonságok

| Tulajdonság                  | Típus                               | Leírás                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | sztring                             | Az esemény neve. A következő űrlapon: {resource}-{action}. Ebben az esetben az érték "referral-updated" (ajánló frissítése) lesz.                                  |
| ResourceUri (Erőforrás-azonosító)               | URI                                | Az erőforrás lekért URI-ját. A következő szintaxist használja:[*" {baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName nevű erőforrásáról              | sztring                             | Az eseményt aktiváló erőforrás neve. Ebben az esetben az érték "hivatkozás".                          |
| AuditUri                  | URI                                | (Nem kötelező) A naplórekord lekért URI-ját, ha létezik. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | sztring az UTC dátum-idő formátumban | Az erőforrás-módosítás dátuma és időpontja.                                                         |

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

### <a name="invoice-ready-event"></a>Számla kész esemény

Ez az esemény akkor történik, amikor az új számla elkészült.

| Tulajdonság                  | Típus                               | Leírás                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | sztring | Az esemény neve. A következő űrlapon: {resource}-{action}. Ebben az esetben az érték "számlakész". |
| ResourceUri (Erőforrás-azonosító) | URI | Az erőforrás lekért URI-ját. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{{InvoiceId}}" |
| ResourceName nevű erőforrásáról | sztring | Az eseményt aktiváló erőforrás neve. Ebben az esetben az érték "invoice". |
| AuditUri |  URI | (Nem kötelező) A naplórekord lekért URI-ját, ha létezik. A következő szintaxist használja: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}} |
| ResourceChangeUtcDate | sztring az UTC dátum-idő formátumban | Az erőforrás-módosítás dátuma és időpontja. |

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
