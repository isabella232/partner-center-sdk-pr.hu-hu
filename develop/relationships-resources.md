---
title: Erőforrások kapcsolatai
description: A kapcsolatokhoz kapcsolódó erőforrásokat ismerteti.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c5701414bd704b375dc23859b920609d5a975d9f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767792"
---
# <a name="relationships-resources"></a>Erőforrások kapcsolatai

**A következőkre vonatkozik**

- Partnerközpont

A kapcsolatokhoz kapcsolódó erőforrásokat ismerteti.

## <a name="partnerrelationship"></a>PartnerRelationship

Két partner közötti kapcsolatot jelöl.

| Tulajdonság         | Típus                                                           | Leírás                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | sztring                                                         | A partner azonosítója. A partner azonosítója megadja annak a partnernek a bérlői azonosítóját, aki a kapcsolat címzett (feladó) oldalán található. |
| location         | sztring                                                         | A partner helye.                                                                                                                   |
| mpnId            | sztring                                                         | A partner Microsoft Partner Network (MPN) azonosítója.                                                                                 |
| name             | sztring                                                         | A partner neve.                                                                                                                       |
| relationshipType | sztring                                                         | A kapcsolat típusa.                                                                                                                      |
| állapot            | sztring                                                         | A kapcsolat állapota (például `active` ).                                                                                                 |
| attribútumok       | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

Megadja azt az URL-címet, amellyel az ügyfél kapcsolatot létesíthet egy partnerrel.

| Tulajdonság   | Típus                                                           | Leírás                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | sztring                                                         | A kapcsolati kérelem URL-címe. |
| attribútumok | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.      |
