---
title: Partnerbiztonsági követelmények erőforrásai
description: Ismerje meg a többtényezős hitelesítés (MFA) bevezetésének részleteit, hogy megfeleljen a partnerek biztonsági követelményeinek.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 6377dbde574edd1b8d8058f7b8e88ae6497d615b9237bbda91e9c4617486b569
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997889"
---
# <a name="partner-security-requirements-resources"></a>Partnerekre vonatkozó biztonsági követelmények erőforrásai

Ez a cikk segít megérteni a többtényezős hitelesítés (MFA) bevezetésének részleteit, hogy a szervezet megfeleljen a partnerek biztonsági követelményeinek. 

## <a name="portal-request-without-mfa"></a>Portálkérés MFA nélkül

Olyan felhasználót jelez, aki MFA Partnerközpont nélkül fér hozzá a portálhoz.

| Tulajdonság                            | Típus            | Leírás                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | sztring          | Felhasználói objektum azonosítója                        |
| TenantId                            | sztring          | CSP-bérlő azonosítója                         |
| Upn                                 | sztring          | Egyszerű felhasználónév                   |
| LastNonMfaCompliantLoginDateTime    | dátum/idő        | A legutóbbi időpont, amikor a felhasználó MFA nélkül jelentkezik be |


## <a name="api-request-summarized-by-application"></a>Alkalmazás szerint összegezve az API-kérés

Az APP + User hitelesítő adatok által kért API-kérés összegzése, a kérés dátuma és az alkalmazás azonosítója alapján összesítve.

| Tulajdonság                            | Típus            | Description               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate (Bejelentkezésidátum)                           | dátum/idő        | API-kérelem dátuma          |
| MfaCompliantRequestCount            | hosszú            | Kérelmek száma MFA-val    |
| TotalRequestCount                   | hosszú            | Kérelmek teljes száma       |
| ApplicationId                       | sztring          | Az alkalmazásazonosító        |
| ApplicationName                     | sztring          | Az alkalmazás neve      |


## <a name="api-request-details"></a>API-kérelem részletei

AZ ALKALMAZÁS + Felhasználói hitelesítő adatok által kért API-kérés. 

| Tulajdonság                            | Típus            | Description                              |
|-------------------------------------|-----------------|------------------------------------------|
| Kérelemazonosító                           | sztring          | MS-RequestId                             |
| CorrelationId                       | sztring          | MS-CorrelationId                         |
| OperationName                       | sztring          | Az API elérési útja kérelem metódussal         |
| RequestDateTime (Kérelemdátumidő)                     | DateTime        | Az API-kérelem ideje                     |
| IP-cím                           | sztring          | Forrás IP-címe                        |
| ObjectId                            | sztring          | Felhasználói objektum azonosítója                           |
| TenantId                            | sztring          | CSP-bérlő azonosítója                            |
| Upn                                 | sztring          | Egyszerű felhasználónév                      |
| ApplicationId                       | sztring          | Az alkalmazás                         |
| MfaCompliant (Mfa-kompatibilis)                        | logikai            | A kérelem jelzése MFA-val vagy anélkül |
