---
title: Kapcsolatok erőforrásai
description: A kapcsolatokhoz kapcsolódó erőforrásokat ismerteti.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7dba1e99a6c97c759e3c61cde1e7565faa2ef4d1
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445731"
---
# <a name="relationships-resources"></a>Kapcsolatok erőforrásai

A kapcsolatokhoz kapcsolódó erőforrásokat ismerteti.

## <a name="partnerrelationship"></a>Partnerreláció

Két partner közötti kapcsolatot képvisel.

| Tulajdonság         | Típus                                                           | Leírás                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | sztring                                                         | A partnerazonosító. A partnerazonosító megadja annak a partnernek a bérlőazonosítóját, aki a kapcsolat címzett oldalán van (a címről). |
| location         | sztring                                                         | A partner helye.                                                                                                                   |
| mpnId            | sztring                                                         | A Microsoft Partner Network (MPN) azonosítója.                                                                                 |
| name             | sztring                                                         | A partner neve.                                                                                                                       |
| relationshipType (kapcsolattípus) | sztring                                                         | A kapcsolat típusa.                                                                                                                      |
| állapot            | sztring                                                         | A kapcsolat állapota (például `active` ).                                                                                                 |
| Attribútumok       | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest (Kapcsolatrequest)

Azt az URL-címet biztosítja, amellyel az ügyfél kapcsolatot létesíthet egy partnerrel.

| Tulajdonság   | Típus                                                           | Leírás                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | sztring                                                         | A kapcsolatkérés URL-címe. |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.      |
