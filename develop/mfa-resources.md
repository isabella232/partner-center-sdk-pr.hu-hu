---
title: Partneri biztonsági követelmények erőforrásai
description: A többtényezős hitelesítés (MFA) bevezetési részleteinek megismerése a partneri biztonsági követelmények teljesítése érdekében.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 5eb77c3c10e95c9dc835cfe05e014b9256531b51
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767776"
---
# <a name="partner-security-requirements-resources"></a>Partneri biztonsági követelmények erőforrásai

**A következőkre vonatkozik:**

- Partnerközpont

Ez a cikk segít megérteni a többtényezős hitelesítés (MFA) bevezetésének részleteit, hogy a szervezete megfeleljen a partnerek biztonsági követelményeinek. 

## <a name="portal-request-without-mfa"></a>Portálra vonatkozó kérelem MFA nélkül

Adja meg azt a felhasználót, aki az MFA-hitelesítés nélkül fér hozzá a partner Center portálhoz.

| Tulajdonság                            | Típus            | Leírás                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | sztring          | Felhasználói objektum azonosítója                        |
| TenantId                            | sztring          | CSP-bérlő azonosítója                         |
| UPN                                 | sztring          | Egyszerű Felhasználónév                   |
| LastNonMfaCompliantLoginDateTime    | dátum/idő        | Felhasználói bejelentkezés legkésőbbi ideje (MFA nélkül) |


## <a name="api-request-summarized-by-application"></a>API-kérelem összefoglalása alkalmazás szerint

Az alkalmazás-és felhasználói hitelesítő adatok által készített API-kérelem összefoglalása, a kérelem dátuma és az alkalmazás azonosítója alapján összesítve.

| Tulajdonság                            | Típus            | Leírás               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | dátum/idő        | API-kérelem dátuma          |
| MfaCompliantRequestCount            | hosszú            | A kérelmek száma MFA-val    |
| TotalRequestCount                   | hosszú            | Kérelmek száma összesen       |
| ApplicationId                       | sztring          | Az alkalmazás azonosítója        |
| ApplicationName                     | sztring          | Az alkalmazás neve      |


## <a name="api-request-details"></a>API-kérelem részletei

Az APP + felhasználói hitelesítő adatokkal végzett API-kérelem. 

| Tulajdonság                            | Típus            | Leírás                              |
|-------------------------------------|-----------------|------------------------------------------|
| Kérelemazonosító                           | sztring          | MS-RequestId                             |
| CorrelationId                       | sztring          | MS-CorrelationId                         |
| OperationName                       | sztring          | Az API elérési útja a kérelem metódusával         |
| RequestDateTime                     | DateTime        | Az API-kérelem ideje                     |
| IP-cím                           | sztring          | Forrás IP-címe                        |
| ObjectId                            | sztring          | Felhasználói objektum azonosítója                           |
| TenantId                            | sztring          | CSP-bérlő azonosítója                            |
| UPN                                 | sztring          | Egyszerű Felhasználónév                      |
| ApplicationId                       | sztring          | Az alkalmazás                         |
| MfaCompliant                        | logikai            | A kérelem jelzése MFA-val vagy anélkül |
