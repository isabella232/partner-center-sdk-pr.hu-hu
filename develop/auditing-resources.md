---
title: Erőforrások naplózása
description: Ismerje meg Partnerközpont API-naplózási erőforrásokat, például az AuditRecordot, amelyből a tevékenység Partnerközpont le.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 50c90f7e7a5dfb274044fafab87818c7ac8428124ca9072770cc5fd9fa3806d5
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994659"
---
# <a name="auditing-resources-that-help-you-get-a-record-of-partner-center-activity"></a>Naplózási erőforrások, amelyek segítségével rekordot kap a Partnerközpont tevékenységről

A következő erőforrásokat használhatja naplózási műveletekkel.

## <a name="auditrecord"></a>AuditRecord (Napló naplózva)

Egy partnerfelhasználó vagy alkalmazás által végrehajtott művelet rekordját jelöli.

| Tulajdonság | Típus | Description |
| --- | --- | ---|
| customerId | sztring | Egy GUID formátumú sztring, amely azonosítja az ügyfelet. |
| customerName (ügyfél neve) | sztring | Az ügyfél neve. |
| userPrincipalName | sztring | Az egyszerű felhasználónév vagy a felhasználói azonosító. Ez a tulajdonság általában egy internet stílusú bejelentkezési név egy felhasználó számára az internet szabvány szerinti RFC 822-es szabványon alapuló e-mail-címformátumban. |
| applicationId | sztring | A műveletet végrehajtásához szükséges alkalmazást azonosító sztring. |
| resourceType | sztring | A művelet által működtetett erőforrás típusa. Lehetséges értékek: `customer` , , , , , , , , , `customer_user` , , `order` , , , `subscription` , `license` `third_party_add_on` `mpn_association` `transfer` `application` `application_credential` `partner_user` `partner_relationship` `partner_customer_dap` `customer_directory_role` . |
| resourceOldValue | sztring | Az erőforrás régi értéke. |
| resourceNewValue (erőforrás új érték) | sztring | Az erőforrás új értéke. |
| operationType | sztring | A végrehajtott művelet típusa. Lehetséges értékek: , , , , (csak a sandbox integration `update_customer_qualification` `update_subscription` accounts `upgrade_subscription` `convert_trial_subscription` `add_customer` `update_customer_billing_profile` `update_customer_partner_contract_company_name` `update_customer_spending_budget` `delete_customer` only), `remove_partner_customer_relationship` , `create_order` `update_order` `create_customer_user` `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `create_self_serve_policy` `update_self_serve_policy` `create_self_serve_policy` `delete_self_serve_policy` `remove_partner_relationship` `delete_tip_customer` `create_related_referral` `update_related_referral` `create_referral` `update_referral` `get_software_key` `get_software_download_link` `increase_spending_limit` `ready_invoice` `create_agreement` `extend_relationship` `create_transfer` `dap_admin_relationship_approved` `dap_admin_relationship_terminated` `add_user_member` `remove_user_member` . |
| operationDate (műveletdátum) | sztring UTC dátum-idő formátumban | A művelet végrehajtásához szükséges dátum és idő. |
| operationStatus (műveletállapot) | sztring | A naplót végzett művelet állapota. Lehetséges értékek: , vagy , ami azt jelenti, hogy `succeeded` a művelet még folyamatban `failed` `progress` van. |
| customizedData (egyéni adatok)  | objektumok tömbje | További információ. Minden objektum két JSON kulcs-érték párt tartalmaz: az első és egy sztringértéket, a második `key` pedig `value` egy sztringértéket. A tömbben lévő objektumok száma a végrehajtott művelet típusától függ. |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok. |
