---
title: Kifizetések kezelése a Payout Service API-val
description: Ismerje meg, hogyan használhatja Partnerközpont Payout Service API-t a kifizetési adatok eléréséhez
ms.date: 06/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: jasongroce
ms.author: sabaja
ms.openlocfilehash: b9bdc6da64a79f4f35466fb62662b086a8e1ab3cadc99c7ca685303752f9d166
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996328"
---
# <a name="manage-payouts-using-the-payout-service-api"></a>Kifizetések kezelése a Payout Service API-val

Ez a cikk azt ismerteti, hogyan férhet hozzá a kifizetési adatokhoz a Kifizetési szolgáltatás API-ja segítségével a Partnerközpont felhasználói felületén. Ezek az API-k programozott módon biztosítják [](https://partner.microsoft.com/dashboard/payouts/reports/incentiveexport) az Adatok exportálása funkció képességeit a Partnerközpont.

## <a name="available-apis"></a>Elérhető API-k

Az összes elérhető API-t a [partneri kifizetéseknél láthatja.](/rest/api/partner-center/partner-payouts)

## <a name="prerequisites"></a>Előfeltételek

- [Regisztrálhat egy alkalmazást az AAD-/Microsoft-identitással](/graph/auth-register-app-v2) a Azure Portal, és hozzáadhatja a megfelelő tulajdonosokat és szerepköröket az alkalmazáshoz.
- A [Visual Studio](https://visualstudio.microsoft.com/downloads/) telepítése.

## <a name="register-an-application-with-the-microsoft-identity-platform"></a>Alkalmazás regisztrálása a Microsoft Identity Platformon

A [Microsoft Identitásplatform](/azure/active-directory/develop/v2-overview) segítségével olyan alkalmazásokat építhet, amelyekbe a felhasználók és az ügyfelek Microsoft-identitásaik vagy közösségi fiókjaik használatával bejelentkeznek, és engedélyezett hozzáférést biztosít saját API-khoz vagy Microsoft API-khoz, például a Microsoft Graph.

1. Jelentkezzen be egy munkahelyi vagy iskolai fiókkal vagy a személyes Microsoft-fiókjával az [Azure Portalra](https://portal.azure.com/).

   Ha a fiókja több bérlőhöz is biztosít hozzáférést, válassza ki a fiókját a jobb felső sarokban, és állítsa a portál-munkamenetet a megfelelő Azure AD-bérlőre.

2. A bal oldali navigációs panelen válassza ki a Azure Active Directory, majd válassza Alkalmazásregisztrációk Új **regisztráció lehetőséget.** Megjelenik **az Alkalmazás regisztrálása** lap.

   :::image type="content" source="./images/manage-payouts/new-app-registration.png" alt-text="Képernyőkép az alkalmazás regisztrálása képernyőről a Azure Portal.":::

3. Adja meg az alkalmazás regisztrációs adatait:

   - Név: Adjon meg egy kifejező alkalmazásnevet, amely megjelenik az alkalmazás felhasználói számára.
   - Támogatott fióktípusok: Válassza ki, hogy az alkalmazás mely fiókokat fogja támogatni.

    | **Támogatott fióktípusok**                             | **Leírás**                                                                                            |
    |---------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
    | Csak az ebben a szervezeti címtárban található fiókok          | Akkor válassza ezt a lehetőséget, ha üzletági (LOB) alkalmazást készít. Ez a lehetőség nem érhető el, ha nem regisztrálja az alkalmazást egy címtárban. E lehetőség választása esetén az alkalmazás csak egy Azure AD-bérlős lesz.  Ez az alapértelmezett beállítás, kivéve, ha címtáron kívül regisztrálja az alkalmazást. Ha címtáron kívül regisztrálja az alkalmazást, a több Azure AD-bérlős alkalmazás és a személyes Microsoft-fiókok használata lesz az alapértelmezés.             |
    | Tetszőleges szervezeti címtárban található fiókok                | Akkor válassza ezt a lehetőséget, ha szeretne minden üzleti és az oktatási ügyfelet megcélozni.  E lehetőség választása esetén az alkalmazás csak több Azure AD-bérlős lesz. Ha csak egy Azure AD-bérlősként regisztrálta az alkalmazást, a Hitelesítés panelen átválthatja több Azure AD-bérlősre, illetve visszaállíthatja egy Azure AD-bérlősre.                                                                                                                                                  |
    | Tetszőleges szervezeti címtárban található fiókok és személyes Microsoft-fiókok | Akkor válassza ezt a lehetőséget, ha a lehető legszélesebb ügyfélkört szeretbé megcélozni. E lehetőség választása esetén az alkalmazás több Azure AD-bérlős lesz, és személyes Microsoft-fiókok is használhatók lesznek.  Ha azure AD több-bérlős és személyes Microsoft-fiókként regisztrálta az alkalmazást, a felhasználói felületen nem módosíthatja ezt a kijelölést. Ehelyett az alkalmazásjegyzék-szerkesztőt kell használnia a támogatott fióktípusok módosításához.                                                                          |

   - *(nem kötelező)* Átirányítási URI: Válassza ki a létre kívánt alkalmazás típusát: Webes vagy nyilvános ügyfél (mobil & asztali verzió), majd adja meg az alkalmazás átirányítási URI-ját (vagy válasz URL-címét). (Az átirányítási URL-cím az a hely, ahová a hitelesítési válasz a felhasználó hitelesítése után lesz elküldve.) 

      Webalkalmazás esetében adja meg alkalmazás alap URL-címét. A `http://localhost:31544` például a helyi gépen futó webalkalmazás URL-címe lehet. A felhasználók ezzel az URL-címmel jelentkeznek be egy webes ügyfélalkalmazásba.
      Nyilvános ügyfélalkalmazások esetében adja meg az URI-t, amelyet az Azure AD a jogkivonatválaszok visszaadására használ. Adjon meg az alkalmazáshoz tartozó értéket, például: `myapp://auth`.

4. Válassza a **Regisztráció** lehetőséget. Az Azure AD egyedi alkalmazásazonosítót (ügyfél-) rendel hozzá az alkalmazáshoz, és betöltődik az alkalmazás áttekintő oldala.

   :::image type="content" source="./images/manage-payouts/register-an-application.png" alt-text="<helyettesítő szöveg>":::

5. Ha képességeket szeretne hozzáadni az alkalmazáshoz, más konfigurációs lehetőségeket is választhat, például márkajelzést, tanúsítványokat és titkos kulcsokat, API-engedélyeket stb.

## <a name="platform-specific-properties"></a>Platformspecifikus tulajdonságok

Az alábbi táblázat azokat a tulajdonságokat mutatja be, amelyek a különböző típusú alkalmazások konfigurálásához és másolásához szükségesek. **A** Hozzárendelt érték azt jelenti, hogy az Azure AD által hozzárendelt értéket kell használnia.

| Alkalmazástípus              | Platform | Alkalmazás (ügyfél) azonosítója | Titkos ügyfélkulcs | Átirányítási URI/URL | Implicit Flow                                                         |
|-----------------------|----------|-------------------------|---------------|------------------|-----------------------------------------------------------------------|
| Natív/mobil         | Natív   | Hozzárendelt                | No            | Hozzárendelt         | No                                                                    |
| Webalkalmazás               | Webes      | Hozzárendelt                | Igen           | Yes              | Választható Open ID Csatlakozás a középső szoftver alapértelmezés szerint hibrid folyamatot használ (Igen) |
| Egyoldalas alkalmazás (SPA) | Webes      | Hozzárendelt                | Igen           | Yes              | Igen, az SPA-k Open ID Csatlakozás implicit Flow                            |
| Szolgáltatás/démon        | Webes      | Hozzárendelt                | Igen           | Igen              | Nem                                                                    |

## <a name="create-a-service-principal"></a>Egyszerű szolgáltatás létrehozása

Az előfizetés erőforrásainak eléréséhez hozzá kell rendelnie egy szerepkört az alkalmazáshoz. Ha segítségre van szüksége annak eldöntéséhez, hogy melyik szerepkör kínálja a megfelelő engedélyeket az alkalmazáshoz, tekintse meg az [Azure beépített szerepköreit.](/azure/role-based-access-control/built-in-roles)

> [!NOTE]
> A hatókört az előfizetés, az erőforráscsoport vagy az erőforrás szintjén állíthatja be. Az engedélyek a hatókör alacsonyabb szintjeire öröklődik. Ha például hozzáad egy alkalmazást egy erőforráscsoport Olvasó szerepkörhöz, az azt jelenti, hogy be tudja olvasni az erőforráscsoportot és az abban található erőforrásokat.

1. A Azure Portal válassza ki azt a hatókörszintet, amelyhez hozzá szeretne rendelni egy alkalmazást. Ha például egy szerepkört szeretne hozzárendelni az előfizetés hatókörében, keresse meg és válassza az Előfizetések **lehetőséget,** vagy válassza az **Előfizetések** lehetőséget a kezdőlapon.

   :::image type="content" source="./images/manage-payouts/search-for-subscriptions.png" alt-text="Képernyőkép az Előfizetések képernyőkeresésről.":::

2. Válassza ki azt az előfizetést, amelyhez hozzá szeretne rendelni egy alkalmazást.

   :::image type="content" source="./images/manage-payouts/internal-testing-subscription.png" alt-text="Képernyőkép az Előfizetések képernyőről, igazra beállított Belső tesztelés jelzővel.":::

> [!NOTE]
> Ha nem látja a keresett előfizetést, válassza a globális előfizetések szűrőt, és ellenőrizze, hogy a kívánt előfizetés van-e kiválasztva a portálon.

3. Válassza **a Hozzáférés-vezérlés (IAM),** majd a **Szerepkör-hozzárendelés hozzáadása lehetőséget.**

4. Válassza ki az alkalmazáshoz hozzárendelni kívánt szerepkört. Ha például engedélyezni szeretné, hogy az alkalmazás újraindítási, indítási és leállítási műveleteket hajtson végre, válassza a Közreműködő szerepkört. További információ az elérhető [szerepkörökről:](/azure/role-based-access-control/built-in-roles).

   Alapértelmezés szerint az Azure AD-alkalmazások nem jelennek meg az elérhető lehetőségek között. Az alkalmazás megkeresése érdekében keressen rá a névre, és válassza ki az eredmények közül. Az alábbi képernyőképen `example-app` a regisztrált AAD-alkalmazás látható.

   :::image type="content" source="./images/manage-payouts/add-role-assignment.png" alt-text="Képernyőkép a tesztalkalmazás szerepkör-hozzárendelésének hozzáadására vonatkozó felhasználói felületről.":::

5. Válassza a **Mentés** lehetőséget. Ezután láthatja az alkalmazást az erre a hatókörre vonatkozó szerepkörrel bíró felhasználók listájában.

   Elkezdheti használni a szolgáltatásnévvel a szkripteket vagy alkalmazásokat. A szolgáltatásnév engedélyeinek kezeléséhez tekintse meg a felhasználói jóváhagyás állapotát, az engedélyek áttekintését, a bejelentkezési adatokat és egyéb információkat, valamint a vállalati alkalmazásokat a [Azure Portal.](https://portal.azure.com)

## <a name="set-up-api-permissions"></a>API-engedélyek beállítása

Ez a szakasz útmutatást nyújt a szükséges API-engedélyek beállításához. Az API-engedélyek beállításával kapcsolatos Partnerközpont lásd: Partner API [hitelesítés.](/partner/develop/api-authentication)

**Engedély megadása Graph API-hoz**

1. Nyissa meg [Alkalmazásregisztrációk](https://go.microsoft.com/fwlink/?linkid=2083908) a Azure Portal.

2. Válasszon ki egy alkalmazást, vagy hozzon létre [egy alkalmazást,](/azure/active-directory/develop/quickstart-register-app) ha még nem rendelkezik ilyen alkalmazással.

3. Az alkalmazás Áttekintés lapján, a Kezelés alatt **válassza** az **API-engedélyek** lehetőséget, majd az **Engedély hozzáadása lehetőséget.**

4. Az **elérhető API-k** listájából válassza a Microsoft Graph lehetőséget.

5. Válassza **a Delegált engedélyek lehetőséget,** és adja hozzá a szükséges engedélyeket. További információ: [Alkalmazás-hozzáférés konfigurálása.](/azure/active-directory/develop/quickstart-configure-app-access-web-apis)

   :::image type="content" source="./images/manage-payouts/graph-request-api-permissions.png" alt-text="Képernyőkép a Microsoft-fiókkal kijelölt Azure Portal képernyőről a Graph képernyőn.":::

**Hozzájárulás a Partnerközpont API-hoz AAD-alkalmazáson keresztüli API-hozzáféréshez**

6. Az alkalmazáshoz válassza az **API-engedélyek** lehetőséget, majd a Request API permissions (API-engedélyek kérése) képernyőn válassza **az Add a permission**(Engedély hozzáadása) lehetőséget, majd a my organization uses (A szervezet által használt **API-k) lehetőséget.**

7. Keressen rá a **Microsoft Partner (Microsoft Fejlesztői központ) API (4990cffe-04e8-4e8b-808a-1175604b879f) kifejezésre.**

   :::image type="content" source="./images/manage-payouts/partner-api-request-permissions.png" alt-text="Képernyőkép az API-engedélyek képernyőről, a Microsoft-partner beállítással.":::

8. Állítsa a Delegált engedélyeket a **következőre: Partnerközpont.**

   :::image type="content" source="./images/manage-payouts/partner-api-request-permissions.png" alt-text="Képernyőkép az API-engedélyek kérése képernyőn Partnerközpont kiválasztott delegált engedélyekről.":::

9. Adjon **rendszergazdai jóváhagyást** az API-knak.

   :::image type="content" source="./images/manage-payouts/api-permissions.png" alt-text="Képernyőkép a Rendszergazdai jóváhagyás váltógombról az API-engedélyek képernyőn.":::

   Ellenőrizze, hogy a Rendszergazdai jóváhagyás engedélyezve van-e a Rendszergazdai jóváhagyás állapota képernyőn.

   :::image type="content" source="./images/manage-payouts/admin-consent-verification.png" alt-text="Képernyőkép a rendszergazdai jóváhagyás állapotképernyőről":::

10. A Hitelesítés **szakaszban** győződjön meg arról, hogy a Nyilvános **ügyfélfolyamatok** engedélyezése beállítás igenre van **állítva.**

    :::image type="content" source="./images/manage-payouts/allow-public-client-flows.png" alt-text="A Hitelesítés képernyő képernyőképe, a Nyilvános ügyfélfolyamatok engedélyezése beállítás Igen beállítással.":::

## <a name="run-the-sample-code-in-visual-studio"></a>Futtassa a mintakódot a Visual Studio

Mintakód, amely bemutatja, hogyan használható az API a fizetési és tranzakciós előzményekhez a Partnerközpont kifizetési [API-GitHub](https://github.com/microsoft/Partner-Center-Payout-APIs) található.

### <a name="sample-code-notes"></a>Mintakódok megjegyzései

- Az ügyfél titkos kulcsait és tanúsítványait nem szükséges konfigurálni a Szolgáltatásnév létrehozása [az](/azure/active-directory/develop/howto-create-service-principal-portal) Azure Portal szakaszban tárgyaltak szerint.
- A többtényezős hitelesítéssel (MFA) rendelkező fiókok jelenleg nem támogatottak, és hibát okoznak.
- A Kifizetési API csak a felhasználó-jelszó alapú hitelesítő adatokat támogatja.

## <a name="next-steps"></a>Következő lépések

- [Az erőforrásokhoz hozzáférő Azure AD-alkalmazás és -szolgáltatásnév létrehozása a portálon](/azure/active-directory/develop/howto-create-service-principal-portal)
- [Alkalmazás regisztrálása a Microsoft Identity Platformon](/graph/auth-register-app-v2)
- [Ügyfélalkalmazás konfigurálása webes API-k elérésére](/azure/active-directory/develop/quickstart-configure-app-access-web-apis)
