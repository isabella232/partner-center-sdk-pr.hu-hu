---
title: Azure-kiadások API-erőforrásai
description: Ismerje meg, hogy a CSP-partnerek hogyan használhatják a partner Center API-kat a partnerek és az ügyfelek Azure-beli kiadásainak és használatának a költségvetésen keresztüli megtekintéséhez
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 02a2995a06473cc6990d1234acd522a3b38a03d3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768539"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a>Az Azure-kiadások API-erőforrásai a partneri és az ügyfél-kiadások, valamint a költségvetéssel való használat kezeléséhez 

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A Cloud Solution Provider (CSP) partnerei a partner Center API-kon keresztül tekinthetik meg és kezelhetik az Azure-kiadásokat. Emellett programozott módon megtekinthetik az ügyfeleik költségeit az Azure-kiadások költségvetésében.

További információ: [olyan forgatókönyvek, amelyekben a CSP-partnerek a partner Center API-kkal kezelhetik az ügyfél-és partneri fiókokat és a rendeléseket](scenarios.md).

## <a name="partner-usage-management"></a>Partneri használat kezelése

- [Partner-használat összesítésének beszerzése](get-a-partner-usage-summary.md) a **PartnerUsageSummary** -erőforrás használatával
- A **CustomerMonthlyUsageRecord** -erőforrást használó [összes ügyfél használati rekordjainak lekérése](get-a-customer-s-usage-records.md)

## <a name="customer-usage-management"></a>Ügyfél-használati felügyelet

- [Ügyfél használati összegzésének beszerzése](get-a-customer-usage-summary.md) a **CustomerUsageSummary** -erőforrás használatával
- Az [ügyfél összes előfizetés-használati rekordjának lekérése](get-a-customer-subscription-s-usage-records.md) az **SubscriptionMonthlyUsageRecord** erőforrás használatával

## <a name="subscription-usage-management"></a>Előfizetés-használat kezelése

- [Előfizetés-használati összefoglalás beszerzése](get-a-customer-subscription-usage-summary.md) a **SubscriptionUsageSummary** -erőforrás használatával
- Az [előfizetéshez tartozó összes havi használati rekord beolvasása](get-all-monthly-usage-records-for-a-subscription.md) a **AzureResourceMonthlyUsageRecord** -erőforrás használatával
- [Előfizetéshez tartozó használati adatok lekérése erőforrás alapján](get-a-customer-subscription-resource-usage-records.md) a **ResourceUsageRecord** -erőforrás használatával
- Az [előfizetéshez tartozó használati adatok lekérése](get-a-customer-subscription-meter-usage-records.md) a **MeterUsageRecord** -erőforrás használatával

## <a name="azure-spending-budget-management"></a>Az Azure költségvetés-kezelési kiadásai

- [Ügyfél használati költségkeretének beszerzése](get-a-customer-s-usage-spending-budget.md) a **CustomerUsageSummary** -erőforrás használatával
- [Ügyfél használati költségkeretének frissítése](update-a-customer-s-usage-spending-budget.md) a **CustomerUsageSummary** -erőforrás használatával
