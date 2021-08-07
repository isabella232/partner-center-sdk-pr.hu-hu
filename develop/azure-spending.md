---
title: Azure-beli költési API-erőforrások
description: Megtudhatja, hogyan használhatja a CSP-partnerek Partnerközpont API-kat a partneri és ügyfél Azure-kiadások és -használat költségvetéshez való vetéséhez és kezeléséhez.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8b51ccbcdaee18b6d5b3bd1b9531a64b22c8bac5a9d95e6cf94291ee802ed5d9
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992398"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a>Azure-költség API-erőforrások a partnerek vagy ügyfelek kiadásainak és használatának költségvetéshez való kezeléséhez 

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Felhőszolgáltató (CSP) partnerek megtekinthetik és kezelhetik Azure-kiadásaikat az Partnerközpont API-kon keresztül. Programozott módon is megtekinthetik az ügyfeleik kiadásait az Azure-költségkerethez való vetésükhöz.

További információért tekintse meg az olyan forgatókönyveket, amelyekben a CSP-partnerek a Partnerközpont API-k használatával kezelhetik az ügyfél- és [partnerfiókokat és -rendeléseket.](scenarios.md)

## <a name="partner-usage-management"></a>Partnerhasználat-kezelés

- [Partnerhasználati összefoglalás lekérte](get-a-partner-usage-summary.md) a **PartnerUsageSummary erőforrás** használatával
- [A](get-a-customer-s-usage-records.md) **CustomerMonthlyUsageRecord** erőforrást használó összes ügyfél használati rekordjainak lezása

## <a name="customer-usage-management"></a>Ügyfélhasználat kezelése

- [Az ügyfél használati adatokat összegző összegzésének](get-a-customer-usage-summary.md) lekérte a **CustomerUsageSummary erőforrás** használatával
- [Egy ügyfél összes előfizetés-használati rekordja a](get-a-customer-subscription-s-usage-records.md) **SubscriptionMonthlyUsageRecord erőforrás** használatával

## <a name="subscription-usage-management"></a>Előfizetés használatának kezelése

- [Az előfizetés használatának összegzése a](get-a-customer-subscription-usage-summary.md) **SubscriptionUsageSummary erőforrás** használatával
- [Egy előfizetés összes havi használati rekordját](get-all-monthly-usage-records-for-a-subscription.md) lekérte az **AzureResourceMonthlyUsageRecord erőforrás** használatával
- [Előfizetés használati adatainak lekérte erőforrás szerint](get-a-customer-subscription-resource-usage-records.md) a **ResourceUsageRecord erőforrás** használatával
- [Használati adatok lekérte egy előfizetés használati adatait mérő alapján a](get-a-customer-subscription-meter-usage-records.md) **MeterUsageRecord erőforrás** használatával

## <a name="azure-spending-budget-management"></a>Azure-költségvetések kezelése

- [Ügyfél használati költségvetésének lekérte](get-a-customer-s-usage-spending-budget.md) a **CustomerUsageSummary erőforrást** használva
- [Ügyfél használati költségvetésének frissítése](update-a-customer-s-usage-spending-budget.md) a **CustomerUsageSummary erőforrás** használatával
