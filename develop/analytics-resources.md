---
title: Elemzési erőforrások
description: Partnerközpont erőforrások használati, üzembe helyezési és használati adatokat tartalmaznak. Betekintő adatokat tartalmaz a partnerek és ügyfelek licenceinek üzembe helyezéséről és használatáról.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: fc665e8e4468648f71f242992780fbc66a02522a0b8b957a5ce68147ab33eaac
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993197"
---
# <a name="analytics-api-resources-that-help-you-report-on-license-usage-deployment-and-consumption"></a>Analytics API-erőforrások, amelyek segítségével jelentést készít a licenchasználatról, az üzembe helyezésről és a felhasználásról

Az itt definiált erőforrások a használattal, üzembe helyezéssel és használattal kapcsolatos jelentésekhez használt adatokat tartalmaznak.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

A **PartnerLicensesDeploymentInsights erőforrás** partnerszintű információkat tartalmaz a licencek üzembe helyezésével kapcsolatban.

| Tulajdonság                  | Típus                                                           | Description                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | szám                                                         | A telepített licencek százalékos aránya.                                                |
| licensesSold              | szám                                                         | Az eladott licencek száma.                                                        |
| processedDateTime         | sztring UTC dátum-idő formátumban                                 | Az adatok összesítésének dátuma és időpontja.                                     |
| serviceName (szolgáltatásnév)               | sztring                                                         | A szolgáltatás neve (például: o365, crm).                                                  |
| Csatorna                   | sztring                                                         | A szolgáltatás csatornaneve (például viszonteladó).                                    |
| Attribútumok                | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok. Tartalmazza az "objectType": "PartnerLicensesDeploymentInsights" |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

A **PartnerLicensesUsageInsights erőforrás** partnerszintű információkat tartalmaz a licenchasználatról.

| Tulajdonság                     | Típus                                                           | Description                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | szám                                                         | A telepített licencek százalékos aránya.                                           |
| workloadName (számítási feladat neve)                 | sztring                                                         | A számítási feladat neve (például exchange).                                             |
| processedDateTime            | sztring UTC dátum-idő formátumban                                 | Az adatok összesítésének dátuma és időpontja.                                |
| serviceName (szolgáltatásnév)                  | sztring                                                         | A szolgáltatás neve (például: o365, crm).                                             |
| Csatorna                      | sztring                                                         | A szolgáltatás csatornaneve (például viszonteladó).                               |
| Attribútumok                   | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok. Tartalmazza az "objectType": "PartnerLicensesUsageInsights" |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

A **CustomerLicensesDeploymentInsights erőforrás** ügyfélszintű információkat tartalmaz a licencek üzembe helyezésről.

| Tulajdonság          | Típus                                                           | Description                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | szám                                                         | Az üzembe helyezett licencek száma.                                                     |
| licensesSold      | szám                                                         | Az eladott licencek száma.                                                         |
| deploymentPercent | szám                                                         | Az üzembe helyezett licencek módosított százalékos aránya.                                        |
| customerId        | sztring                                                         | Az ügyfél azonosítója.                                                             |
| customerName (ügyfél neve)      | sztring                                                         | Az ügyfél neve.                                                                   |
| Productname       | sztring                                                         | A termék neve.                                                                    |
| serviceCode       | sztring                                                         | A licenc szolgáltatáskódja.                                                     |
| processedDateTime | sztring UTC dátum-idő formátumban                                 | Az adatok összesítésének dátuma és időpontja.                                      |
| serviceName (szolgáltatásnév)       | sztring                                                         | A szolgáltatás neve (például: o365, crm).                                                   |
| Csatorna           | sztring                                                         | A szolgáltatás csatornaneve (például viszonteladó).                                     |
| Attribútumok        | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok. Tartalmazza az "objectType": "CustomerLicensesDeploymentInsights" |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

A **CustomerLicensesUsageInsights erőforrás** ügyfélszintű információkat tartalmaz a licenchasználatról.

| Tulajdonság          | Típus                                                           | Description                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | sztring                                                         | A számítási feladat kódja.                                                              |
| workloadName (számítási feladat neve)      | szám                                                         | A számítási feladat neve (például: Exchange).                                              |
| usagePercent      | szám                                                         | A felhasznált licencek módosított százalékos aránya.                                       |
| licensesActive    | szám                                                         | Az aktív licencek száma.                                                  |
| licensesQualified | szám                                                         | A minősített licencek száma.                                               |
| customerId        | sztring                                                         | Az ügyfél azonosítója.                                                        |
| customerName (ügyfél neve)      | sztring                                                         | Az ügyfél neve.                                                              |
| Productname       | sztring                                                         | A termék neve.                                                               |
| serviceCode       | sztring                                                         | A licenc szolgáltatáskódja.                                                |
| processedDateTime | sztring UTC dátum-idő formátumban                                 | Az adatok összesítésének dátuma és időpontja.                                 |
| serviceName (szolgáltatásnév)       | sztring                                                         | A szolgáltatás neve (például: o365, crm).                                              |
| Csatorna           | sztring                                                         | A szolgáltatás csatornaneve (például viszonteladó).                                |
| Attribútumok        | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok. Tartalmazza az "objectType": "CustomerLicensesUsageInsights" |