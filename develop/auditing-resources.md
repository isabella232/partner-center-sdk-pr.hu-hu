---
title: Erőforrások naplózása
description: Ismerje meg Partnerközpont API-naplózási erőforrásokat, például az AuditRecordot, amely segítségével rögzítheti a Partnerközpont tevékenységeket.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9d78a305c2d27dc692c609e30817b34b1f814157
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974352"
---
# <a name="auditing-resources-that-help-you-get-a-record-of-partner-center-activity"></a>Naplózási erőforrások, amelyek segítségével rekordot kap a Partnerközpont tevékenységről

A következő erőforrásokat használhatja naplózási műveletekkel.

## <a name="auditrecord"></a>AuditRecord (Napló naplózva)

Egy partnerfelhasználó vagy alkalmazás által végrehajtott művelet rekordját jelöli.

| Tulajdonság | Típus | Leírás |
| --- | --- | ---|
| customerId | sztring | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet. |
| customerName (ügyfél neve) | sztring | Az ügyfél neve. |
| userPrincipalName | sztring | Az egyszerű felhasználónév vagy a felhasználói azonosító. Ez a tulajdonság általában egy internet stílusú bejelentkezési név a felhasználó számára az internet szabvány szerinti RFC 822-es szabványon alapuló e-mail-cím formátumban. |
| applicationId | sztring | A műveletet végrehajtásához szükséges alkalmazást azonosító sztring. |
| resourceType | sztring | A művelet által működtetett erőforrás típusa. Lehetséges értékek: `customer` , , , , , , , , , `customer_user` , , `order` , , , `subscription` , `license` `third_party_add_on` `mpn_association` `transfer` `application` `application_credential` `partner_user` `partner_relationship` `partner_customer_dap` `customer_directory_role` . |
| resourceOldValue | sztring | Az erőforrás régi értéke. |
| resourceNewValue (erőforrás új érték) | sztring | Az erőforrás új értéke. |
| operationType | sztring | A végrehajtott művelet típusa. Lehetséges értékek: , , , , (csak a védőfal integrációs `update_customer_qualification` `update_subscription` `upgrade_subscription` `convert_trial_subscription` `add_customer` `update_customer_billing_profile` `update_customer_partner_contract_company_name` `update_customer_spending_budget` `delete_customer` fiókjai), `remove_partner_customer_relationship` , `create_order` `update_order` `create_customer_user` `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `create_self_serve_policy` `update_self_serve_policy` `create_self_serve_policy` `delete_self_serve_policy` `remove_partner_relationship` `delete_tip_customer` `create_related_referral` `update_related_referral` `create_referral` `update_referral` `get_software_key` `get_software_download_link` `increase_spending_limit` `ready_invoice` `create_agreement` `extend_relationship` `create_transfer` `dap_admin_relationship_approved` `dap_admin_relationship_terminated` `add_user_member` `remove_user_member` . |
| operationDate (műveletdátum) | sztring UTC dátum-idő formátumban | A művelet végrehajtásához szükséges dátum és idő. |
| operationStatus (műveletállapot) | sztring | A naplót végzett művelet állapota. Lehetséges értékek: , vagy , ami azt `succeeded` `failed` `progress` jelenti, hogy a művelet még folyamatban van. |
| customizedData (egyéni adatok)  | objektumok tömbje | További információ. Minden objektum két JSON kulcs-érték párt tartalmaz: az első és egy sztringértéket, a második `key` pedig `value` egy sztringértéket. A tömbben lévő objektumok száma a végrehajtott művelet típusától függ. |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok. |
