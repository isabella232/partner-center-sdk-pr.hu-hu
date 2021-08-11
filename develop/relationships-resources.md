---
title: Kapcsolatok erőforrásai
description: A kapcsolatokhoz kapcsolódó erőforrásokat ismerteti.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bbbc973679ae80c3ad6b9d67945c6fbcb087789484939b67f8d8a6b538ce7d37
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997090"
---
# <a name="relationships-resources"></a>Kapcsolatok erőforrásai

A kapcsolatokhoz kapcsolódó erőforrásokat ismerteti.

## <a name="partnerrelationship"></a>Partnerreláció

Két partner közötti kapcsolatot képvisel.

| Tulajdonság         | Típus                                                           | Description                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | sztring                                                         | A partnerazonosító. A partnerazonosító megadja annak a partnernek a bérlőazonosítóját, aki a kapcsolat címzett oldalán (a következőtől) található. |
| location         | sztring                                                         | A partner helye.                                                                                                                   |
| mpnId            | sztring                                                         | A Microsoft Partner Network (MPN) azonosítója.                                                                                 |
| name             | sztring                                                         | A partner neve.                                                                                                                       |
| relationshipType (kapcsolattípus) | sztring                                                         | A kapcsolat típusa.                                                                                                                      |
| állapot            | sztring                                                         | A kapcsolat állapota (például `active` ).                                                                                                 |
| Attribútumok       | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest (Kapcsolatrequest)

Azt az URL-címet biztosítja, amellyel az ügyfél kapcsolatot létesíthet egy partnerrel.

| Tulajdonság   | Típus                                                           | Description                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | sztring                                                         | A kapcsolatkérés URL-címe. |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.      |
