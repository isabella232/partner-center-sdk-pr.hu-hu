---
title: Elemzési erőforrások
description: A partner Center erőforrásai a használattal, az üzembe helyezéssel és a felhasználással kapcsolatos adatokat tartalmazzák. A licencek telepítésével és a partnerek és ügyfelek általi használattal kapcsolatos információkat tartalmaz.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: 9bd47b99f0abaa181e5f255dd6e46151363917e7
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768543"
---
# <a name="analytics-api-resources-that-help-you-report-on-license-usage-deployment-and-consumption"></a>Elemzési API-erőforrások, amelyek segítséget nyújtanak a licencek használatáról, üzembe helyezéséről és felhasználásáról

**A következőkre vonatkozik:**

- Partnerközpont

Az itt megadott erőforrások a használat, a telepítés és a felhasználás jelentésére szolgáló adatokat tartalmaznak.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

A **PartnerLicensesDeploymentInsights** -erőforrás a licencek telepítésével kapcsolatos partneri szintű információkat tartalmaz.

| Tulajdonság                  | Típus                                                           | Leírás                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | szám                                                         | A telepített licencek százalékos aránya.                                                |
| licensesSold              | szám                                                         | Az eladott licencek száma.                                                        |
| processedDateTime         | karakterlánc UTC dátum-idő formátumban                                 | Az adatok összesítésének dátuma és időpontja.                                     |
| serviceName               | sztring                                                         | A szolgáltatás neve (például: o365, CRM).                                                  |
| csatorna                   | sztring                                                         | A szolgáltatás csatorna neve (például: viszonteladó).                                    |
| attribútumok                | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai. Tartalmazza a "objektumtípus": "PartnerLicensesDeploymentInsights" |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

A **PartnerLicensesUsageInsights** -erőforrás partneri szintű információkat tartalmaz a licencek használatáról.

| Tulajdonság                     | Típus                                                           | Leírás                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | szám                                                         | A telepített licencek százalékos aránya.                                           |
| workloadName                 | sztring                                                         | A munkaterhelés neve (például: Exchange).                                             |
| processedDateTime            | karakterlánc UTC dátum-idő formátumban                                 | Az adatok összesítésének dátuma és időpontja.                                |
| serviceName                  | sztring                                                         | A szolgáltatás neve (például: o365, CRM).                                             |
| csatorna                      | sztring                                                         | A szolgáltatás csatorna neve (például: viszonteladó).                               |
| attribútumok                   | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai. Tartalmazza a "objektumtípus": "PartnerLicensesUsageInsights" |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

A **CustomerLicensesDeploymentInsights** -erőforrás felhasználói szintű információkat tartalmaz a licencek telepítésével kapcsolatban.

| Tulajdonság          | Típus                                                           | Leírás                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | szám                                                         | A telepített licencek száma.                                                     |
| licensesSold      | szám                                                         | Az eladott licencek száma.                                                         |
| deploymentPercent | szám                                                         | A telepített licencek százalékos aránya.                                        |
| customerId        | sztring                                                         | Az ügyfél-azonosító.                                                             |
| Customername (      | sztring                                                         | Az ügyfél neve.                                                                   |
| productName       | sztring                                                         | A termék neve.                                                                    |
| Meg       | sztring                                                         | A licenc szolgáltatási kódja.                                                     |
| processedDateTime | karakterlánc UTC dátum-idő formátumban                                 | Az adatok összesítésének dátuma és időpontja.                                      |
| serviceName       | sztring                                                         | A szolgáltatás neve (például: o365, CRM).                                                   |
| csatorna           | sztring                                                         | A szolgáltatás csatorna neve (például: viszonteladó).                                     |
| attribútumok        | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai. Tartalmazza a "objektumtípus": "CustomerLicensesDeploymentInsights" |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

A **CustomerLicensesUsageInsights** -erőforrás felhasználói szintű információkat tartalmaz a licencek használatáról.

| Tulajdonság          | Típus                                                           | Leírás                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | sztring                                                         | A munkaterhelés kódja.                                                              |
| workloadName      | szám                                                         | A munkaterhelés neve (például: Exchange).                                              |
| usagePercent      | szám                                                         | A felhasznált licencek kiigazított százalékos aránya.                                       |
| licensesActive    | szám                                                         | Az aktív licencek száma.                                                  |
| licensesQualified | szám                                                         | A minősített licencek száma.                                               |
| customerId        | sztring                                                         | Az ügyfél-azonosító.                                                        |
| Customername (      | sztring                                                         | Az ügyfél neve.                                                              |
| productName       | sztring                                                         | A termék neve.                                                               |
| Meg       | sztring                                                         | A licenc szolgáltatási kódja.                                                |
| processedDateTime | karakterlánc UTC dátum-idő formátumban                                 | Az adatok összesítésének dátuma és időpontja.                                 |
| serviceName       | sztring                                                         | A szolgáltatás neve (például: o365, CRM).                                              |
| csatorna           | sztring                                                         | A szolgáltatás csatorna neve (például: viszonteladó).                                |
| attribútumok        | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai. Tartalmazza a "objektumtípus": "CustomerLicensesUsageInsights" |