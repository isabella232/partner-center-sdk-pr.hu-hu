---
title: Partnerbiztonsági követelmények erőforrásai
description: Ismerje meg a többtényezős hitelesítés (MFA) bevezetésének részleteit, hogy megfeleljen a partnerek biztonsági követelményeinek.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: b41a0e46fa6e0643e82a5a2dbfb7141f54a0f824
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445544"
---
# <a name="partner-security-requirements-resources"></a>Partnerekre vonatkozó biztonsági követelmények erőforrásai

Ez a cikk segít megérteni a többtényezős hitelesítés (MFA) bevezetésének részleteit, hogy a szervezet megfeleljen a partnerek biztonsági követelményeinek. 

## <a name="portal-request-without-mfa"></a>Portálkérés MFA nélkül

Olyan felhasználót jelez, aki MFA-Partnerközpont nélkül fér hozzá a portálhoz.

| Tulajdonság                            | Típus            | Leírás                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | sztring          | Felhasználói objektum azonosítója                        |
| TenantId                            | sztring          | CSP-bérlő azonosítója                         |
| Upn                                 | sztring          | Egyszerű felhasználónév                   |
| LastNonMfaCompliantLoginDateTime    | dátum/idő        | Legutóbbi felhasználói bejelentkezés MFA nélkül |


## <a name="api-request-summarized-by-application"></a>Alkalmazás szerint összegezve az API-kérés

Az APP + Felhasználói hitelesítő adatok által kért API-kérés összegzése, a kérelem dátuma és az alkalmazás azonosítója alapján összesítve.

| Tulajdonság                            | Típus            | Leírás               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate (Bejelentkezésidátum)                           | dátum/idő        | API-kérelem dátuma          |
| MfaCompliantRequestCount            | hosszú            | Kérelmek száma MFA-val    |
| TotalRequestCount                   | hosszú            | Kérelmek teljes száma       |
| ApplicationId                       | sztring          | Az alkalmazásazonosító        |
| ApplicationName                     | sztring          | Az alkalmazás neve      |


## <a name="api-request-details"></a>API-kérelem részletei

AZ ALKALMAZÁS + felhasználó hitelesítő adatai által kért API-kérés. 

| Tulajdonság                            | Típus            | Leírás                              |
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
