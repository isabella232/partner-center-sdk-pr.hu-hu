---
title: Azure-beli költési API-erőforrások
description: Megtudhatja, hogyan használhatnak a CSP-partnerek Partnerközpont API-kat a partneri és ügyfél Azure-kiadások és -használat költségvetéshez való megtekintésére és kezelésére.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 472554de1c354559d5bc4b21959c109467891806
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974318"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a>Azure-költség API-erőforrások partner- vagy ügyfél-kiadások és -használat költségvetéshez való kezeléséhez 

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Felhőszolgáltató (CSP) partnerek megtekinthetik és kezelhetik Azure-kiadásaikat az Partnerközpont API-kon keresztül. Emellett programozott módon is megtekinthetik az ügyfeleik kiadásait az Azure-költségvetéshez.

További információért tekintse meg az olyan forgatókönyveket, amelyekben a CSP-partnerek a Partnerközpont API-k használatával kezelhetik az ügyfél- és [partnerfiókokat és -rendeléseket.](scenarios.md)

## <a name="partner-usage-management"></a>Partnerhasználat kezelése

- [Partner használati összegzésének lezása](get-a-partner-usage-summary.md) a **PartnerUsageSummary erőforrás** használatával
- [A](get-a-customer-s-usage-records.md) **CustomerMonthlyUsageRecord** erőforrást használó összes ügyfél használati rekordjainak lekérte

## <a name="customer-usage-management"></a>Ügyfélhasználat kezelése

- [Ügyfél használati összegzésének lezása](get-a-customer-usage-summary.md) a **CustomerUsageSummary erőforrás** használatával
- [Egy ügyfél összes előfizetés-használati](get-a-customer-subscription-s-usage-records.md) rekordját lekérte a **SubscriptionMonthlyUsageRecord erőforrás** használatával

## <a name="subscription-usage-management"></a>Előfizetés használatának kezelése

- [Az előfizetés használatának összegzése a](get-a-customer-subscription-usage-summary.md) **SubscriptionUsageSummary erőforrás** használatával
- [Előfizetés összes havi használati rekordját](get-all-monthly-usage-records-for-a-subscription.md) lekérte az **AzureResourceMonthlyUsageRecord erőforrás** használatával
- [Előfizetés használati adatainak lekérte erőforrás szerint](get-a-customer-subscription-resource-usage-records.md) a **ResourceUsageRecord erőforrás** használatával
- [Használati adatok lekérte egy előfizetés használati adatait fogyasztásmérő alapján](get-a-customer-subscription-meter-usage-records.md) a **MeterUsageRecord erőforrás** használatával

## <a name="azure-spending-budget-management"></a>Azure-költségvetések kezelése

- [Az ügyfél használati költségvetésének lekérte](get-a-customer-s-usage-spending-budget.md) a **CustomerUsageSummary erőforrást**
- [Ügyfél használati költségvetésének frissítése](update-a-customer-s-usage-spending-budget.md) a **CustomerUsageSummary erőforrás** használatával
