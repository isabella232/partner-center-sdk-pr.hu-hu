---
title: Erőforrások naplózása
description: Ismerje meg a partner Center API naplózási erőforrásait, például a AuditRecord, amelyekkel a partner Center-tevékenységek rekordját kérheti le.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 31832492913e866b078c3c638e22c1a4b8d5e7e6
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768544"
---
# <a name="auditing-resources-that-help-you-get-a-record-of-partner-center-activity"></a>A partner Center-tevékenységek rekordjának beszerzését segítő erőforrások naplózása

**A következőkre vonatkozik:**

- Partnerközpont

A következő erőforrásokat használhatja naplózási műveletekkel.

## <a name="auditrecord"></a>AuditRecord

Egy partner felhasználó vagy alkalmazás által végrehajtott művelet rekordját jelöli.

| Tulajdonság | Típus | Leírás |
| --- | --- | ---|
| customerId | sztring | Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet. |
| Customername ( | sztring | Az ügyfél neve. |
| userPrincipalName | sztring | Az egyszerű felhasználónév vagy a felhasználói azonosító. Ez a tulajdonság általában egy, az Internet szabványos RFC 822-es verzióján alapuló e-mail-cím formátumú felhasználó internetes stílusú bejelentkezési neve. |
| applicationId | sztring | Egy karakterlánc, amely a műveletet végrehajtó alkalmazást azonosítja. |
| resourceType | sztring | A művelet által végrehajtott erőforrás típusa. Lehetséges értékek:,,,,,,,,, `customer` `customer_user` ,, `order` `subscription` `license` `third_party_add_on` `mpn_association` `transfer` `application` `application_credential` `partner_user` `partner_relationship` . |
| resourceOldValue | sztring | Az erőforrás régi értéke. |
| resourceNewValue | sztring | Az erőforrás új értéke. |
| operationType | sztring | A végrehajtott művelet típusa. Lehetséges értékek:,,,,,,,, `update_customer_qualification` `update_subscription` `upgrade_subscription` `convert_trial_subscription` `add_customer` `update_customer_billing_profile` `update_customer_partner_contract_company_name` `update_customer_spending_budget` `delete_customer` (csak homokozó-integrációs fiókok), `remove_partner_customer_relationship` `create_order` `update_order` `create_customer_user` `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `create_self_serve_policy` `update_self_serve_policy` `create_self_serve_policy` `delete_self_serve_policy` `remove_partner_relationship` `delete_tip_customer` `create_related_referral` `update_related_referral` `create_referral` `update_referral` `get_software_key` `get_software_download_link` `increase_spending_limit` `ready_invoice` `create_agreement` `extend_relationship` `create_transfer` ,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,, |
| operationDate | karakterlánc UTC dátum-idő formátumban | A művelet végrehajtásának dátuma és időpontja. |
| operationStatus | sztring | Az auditált művelet állapota. Lehetséges értékek: `succeeded` , `failed` , vagy `progress` , ami azt jelenti, hogy a művelet még folyamatban van. |
| customizedData  | objektumok tömbje | További információ. Minden objektum két JSON kulcs-érték párokat tartalmaz: az első `key` és egy karakterlánc-érték, a második `value` és egy karakterlánc-érték. A tömbben lévő objektumok száma a végrehajtott művelet típusától függ. |
| attribútumok | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai. |
