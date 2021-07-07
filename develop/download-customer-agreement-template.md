---
title: A sablon letöltési hivatkozásának Microsoft Ügyfélszerződés letöltése
description: Szerezze be a sablon letöltési Microsoft Ügyfélszerződés hivatkozását.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: fccb9e3d4a837f3e8043f8c7ae1e3911d819afd7
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906517"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>A sablon letöltési hivatkozásának Microsoft Ügyfélszerződés letöltése

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A **AgreementDocument** erőforrást jelenleg csak a Microsoft nyilvános Partnerközpont támogatja.

Ez a cikk bemutatja, hogyan töltheti le a Microsoft Ügyfélszerződés sablont az ügyfél országa és nyelve alapján.

## <a name="prerequisites"></a>Előfeltételek

- Ha az Partnerközpont .NET SDK-t használja, 1.14-es vagy újabb verzió szükséges.

- Az Partnerközpont [ismertetett hitelesítő adatok.](./partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítést támogatja.

- Az ügyfél országa, amelyre a Microsoft Ügyfélszerződés sablon vonatkozik.

- Az a nyelv, amelyen a Microsoft Ügyfélszerződés sablont honosítottuk.

> [!IMPORTANT]
>
> - A Microsoft Ügyfélszerződés országspecifikus. A sablon letöltésére szolgáló hivatkozás Microsoft Ügyfélszerződés adja meg a megfelelő országot az ügyfél helye alapján. vagy a támogatott országok listáját lásd: A támogatott [országok és nyelvek listája.](#list-of-supported-countries-and-languages)
>
> - Egyes országok esetében a Microsoft Ügyfélszerződés nyelveken érhető el. A legjobb felhasználói élmény érdekében válassza ki az ügyfél igényeinek leginkább megfelelő nyelvet. A támogatott nyelvek listájáért tekintse meg a támogatott országok és [nyelvek listáját.](#list-of-supported-countries-and-languages)
> - Ez a módszer csak a Microsoft Ügyfélszerződés.

## <a name="net"></a>.NET

A sablon letöltésére mutató hivatkozás Microsoft Ügyfélszerződés:

1. A szerződés metaadatainak lekérése a Microsoft Ügyfélszerződés. Be kell szereznie a **sablonazonosítót a** Microsoft Ügyfélszerződés. További információkért lásd: [Szerződés metaadatainak le](get-customer-agreement-metadata.md)Microsoft Ügyfélszerződés.

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Használja az IAggregatePartner.AgreementTemplates gyűjteményt.

3. Hívja meg **a ById** metódust, és **adja** meg a sablonazonosítót Microsoft Ügyfélszerződés.

4. A **Document (Dokumentum) tulajdonság beolvasása.**

5. Hívja meg **a ByCountry** metódust, és adja meg annak az ügyfélnek az országát, amelyre a szerződéssablon vonatkozik. Ha a metódus  nincs megadva, a lekérdezés alapértelmezés szerint az USA-t használja. A támogatott országkódok listájáért tekintse meg a támogatott országok és [nyelvek listáját.](#list-of-supported-countries-and-languages) Ez a metódus megkülönbözteti **a kis- és nagybetűket.**

6. Hívja meg **a ByLanguage** metódust, és adja meg, hogy a szerződéssablon milyen nyelven legyen honosított. A lekérdezés alapértelmezés szerint *en-US,* ha a metódus nincs megadva, vagy a megadott országkód nem támogatott a megadott országhoz. A támogatott nyelvkódok listájáért tekintse meg a támogatott országok és [nyelvek listáját.](#list-of-supported-countries-and-languages)

7. Hívja meg **a Get** vagy **GetAsync metódust.**

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

A teljes minta megtalálható a [GetAgreementDetails osztályban](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) a konzol [tesztalkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektjében.

## <a name="rest-request"></a>REST-kérés

A sablon letöltésére mutató hivatkozás Microsoft Ügyfélszerződés:

1. A szerződés metaadatainak lekérése a Microsoft Ügyfélszerződés. Be kell szereznie a **sablonazonosítót a** Microsoft Ügyfélszerződés. További információkért lásd: [Szerződés metaadatainak le](get-customer-agreement-metadata.md)Microsoft Ügyfélszerződés.

2. Hozzon létre egy REST-kérést egy [ **AgreementDocument erőforrás lekérése** érdekében.](./agreement-document-resources.md) Példaként tekintse meg a kérés [szintaxisának példáját.](#request-syntax) A következő adatokat kell megadnia:

    - A **sablon sablonazonosítója** Microsoft Ügyfélszerződés.
    - Az az ország, amelyre a Microsoft Ügyfélszerződés sablon vonatkozik.
    - Az a nyelv, amelyen a Microsoft Ügyfélszerződés sablont honosítottuk.

### <a name="request-syntax"></a>Kérésszintaxis

Ehhez az erőforráshoz használja a következő kérési szintaxist:

| Metódus | Kérés URI-ja |
|--------|---------------------------------------------------------------------|
| GET | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document?language={language}&country={country} HTTP/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

A kérelemhez a következő URI-paramétereket használhatja:

| Név                   | Típus   | Kötelező | Leírás                                 |
|------------------------|--------|----------|---------------------------------------------|
| agreement-template-id  | sztring | Igen      | A szerződéstípus egyedi azonosítója. A sablon sablonazonosítóját úgy szerezheti be Microsoft Ügyfélszerződés hogy lekérte a szerződés metaadatait a Microsoft Ügyfélszerződés. További információkért lásd: [Szerződés metaadatainak le](./get-customer-agreement-metadata.md)Microsoft Ügyfélszerződés. Ez a paraméter megkülönbözteti **a kis- és nagybetűket.**|
| ország                | sztring | No       | Azt az országot jelzi, amelyre a szerződéssablon vonatkozik. A lekérdezés alapértelmezett értéke *US,* ha a paraméter nincs megadva. A támogatott országkódok listájáért tekintse meg a támogatott országok és [nyelvek listáját.](#list-of-supported-countries-and-languages)|
| language               | sztring | No       | A szerződéssablon honosított nyelvét jelzi. A lekérdezés alapértelmezett értéke *en-US,* ha a paraméter nincs megadva, vagy a megadott országkód nem támogatott a megadott országhoz. A támogatott országkódok listájáért tekintse meg [a támogatott országok és nyelvek listáját.](#list-of-supported-countries-and-languages)|

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus egy [ **AgreementDocument**](./agreement-document-resources.md) erőforrást ad vissza a válasz törzsében.

Az erőforrásnak van **egy downloadUri** tulajdonsága, amely a szerződéssablon letöltéséhez használható URL-sztringet tartalmazza. A lekérdezések minden egyes futtatásakor egy másik hivatkozást ad vissza. Ez a hivatkozás öt perc után lejár.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.

Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "displayUri":"https://wopihost.int.l2o.microsoft.com/v1/officehost/agreement/files/Preview...",
    "downloadUri":"https://l2oagreementintbn2.blob.core.windows.net/agreementscontainer/Preview...",
    "language":"en-US",
    "country":"US"
}
```

## <a name="list-of-supported-countries-and-languages"></a>Támogatott országok és nyelvek listája

> [!IMPORTANT]
> Az országkód tulajdonság megkülönbözteti a kis- és nagybetűket. Győződjön meg arról, hogy az alábbi táblázatban megadott megfelelő kis- és kisajátítást használja.

| Ország                   | Országkód   | Támogatott nyelvkód(ak) |
|------------------------|--------|----------|
| Åland-szigetek | Ax | en-US |
| Afganisztán | AF | en-US |
| Albánia | AL | en-US |
| Algéria | DZ | en-US, fr-FR, en-US |
| Amerikai Szamoa | AS | en-US |
| Andorra | AD | en-US |
| Angola | AO | en-US, pt-PT |
| Anguilla | AI | en-US |
| Antarktisz | Aq | en-US |
| Antigua és Barbuda | AG | en-US |
| Argentína | AR | en-US, es-ES |
| Örményország | AM | en-US |
| Aruba | Aw | en-US |
| Ausztrália | AU | en-US |
| Ausztria | AT | en-US, de-DE |
| Azerbajdzsán | AZ | en-US |
| Bahama-szigetek | BS | en-US |
| Bahrein | BH | en-US, ar-SA |
| Banglades | BD | en-US |
| Barbados | BB | en-US |
| Belarusz | BY | en-US, ru-RU |
| Belgium | BE | en-US, nl-NL |
| Belize | BZ | en-US, es-ES |
| Benin | BJ | en-US |
| Bermuda | Bm | en-US |
| Bhután | BT | en-US |
| Bolívia | BO | en-US, es-ES |
| Bonaire | Bq | en-US |
| Bosznia-Hercegovina | BA | en-US |
| Botswana | BW | en-US |
| Bouvet-sziget | Bv | en-US |
| Brazília | BR | en-US, pt-BR |
| Brit indiai-óceáni terület | Io | en-US |
| Brit Virgin-szigetek | VG | en-US |
| Brunei | BN | en-US |
| Bulgária | BG | en-US, bg-BG |
| Burkina Faso | BF | en-US |
| Burundi | BI | en-US |
| Côte d'Ivoire | CI | en-US, fr-FR |
| Cabo Verde | CV | en-US, pt-PT |
| Kambodzsa | KH | en-US |
| Kamerun | CM | en-US, fr-FR |
| Kanada | CA | en-US, fr-FR |
| Kajmán-szigetek | KY | en-US, en-US |
| Közép-afrikai Köztársaság | CF | en-US |
| Csád | TD | en-US |
| Chile | CL | en-US, es-ES |
| Karácsony-sziget | CX | en-US |
| Cocos (Keeling)-szigetek | CC | en-US |
| Kolumbia | CO | en-US, es-ES |
| Comore-szigetek | Km | en-US |
| Kongó (KDK) | CD | en-US |
| Kongó | Cg | en-US |
| Cook-szigetek | Ck | en-US |
| Costa Rica | CR | en-US, es-ES |
| Horvátország | HR | en-US, hr-HR |
| Curaçao | Cw | en-US |
| Ciprus | CY | en-US |
| Csehország | CZ | en-US, cs-PT |
| Dánia | DK | en-US, da-DK |
| Dzsibuti | Dj | en-US |
| Dominika | DM | en-US |
| Dominikai Köztársaság | DO | en-US, es-ES |
| Ecuador | EC | en-US |
| Egyiptom | EG | en-US, ar-SA |
| Salvador | SV | en-US, es-ES |
| Egyenlítői-Guinea | Gq | en-US |
| Eritrea | ER | en-US |
| Észtország | EE | en-US, et-Enterprise kiadás |
| eSwatini | SZ | en-US |
| Etiópia | ET | en-US |
| Falkland-szigetek | Fk | en-US |
| Feröer szigetek | FO | en-US |
| Fidzsi | FJ | en-US |
| Finnország | FI | en-US, fi-FI |
| Franciaország | JK | en-US, fr-FR |
| Francia Guyana | GF | en-US, fr-FR  |
| Francia Polinézia | PF | en-US |
| Francia Déli Területek | Tf | en-US |
| Gabon | FE | en-US |
| Gambia | GM | en-US |
| Grúzia | GE | en-US |
| Németország | DE | en-US, de-DE |
| Ghána | GH | en-US |
| Gibraltár | Gi | en-US |
| Görögország | GR | en-US, el-GR |
| Grönland | Gl | en-US |
| Grenada | Gd | en-US |
| Guadeloupe | GP | en-US |
| Guam | GU | en-US |
| Guatemala | GT | en-US, es-ES |
| Guernsey | Gg | en-US |
| Guinea | GN | en-US |
| Bissau-Guinea | Gw | en-US |
| Guyana | GY | en-US |
| Haiti | HT | en-US |
| Heard-sziget és McDonald-szigetek | Hm | en-US |
| Honduras | HN | en-US, es-ES |
| Hongkong (KKT) | HK | en-US, zh-HK |
| Magyarország | HU | en-US, hu-HU |
| Izland | IS | en-US |
| India | IN | en-US, hi-IN |
| Indonézia | ID (Azonosító) | en-US, id-ID |
| Irak | IQ | en-US, ar-SA |
| Írország | IE | en-US |
| Man-sziget | Csevegés | en-US |
| Izrael | IL | en-US, he-IL |
| Olaszország | IT | en-US, it-IT |
| Jamaica | JM | en-US |
| Jan Mayen | Xj | en-US |
| Japán | JP | en-US, ja-JP |
| Jersey | JE | en-US |
| Jordánia | JO | en-US, ar-SA |
| Kazahsztán | KZ | en-US, kk-KZ |
| Kenya | KE | en-US |
| Kiribati | KI | en-US |
| Dél-Korea | KR | en-US, ko-KR |
| Koszovó | Xk | en-US |
| Kuvait | KW | en-US, ar-SA |
| Kirgizisztán | KG | en-US, ru-RU |
| Laosz | LA | en-US |
| Lettország | LV | en-US, lv-LV |
| Libanon | LB | en-US, ar-SA |
| Lesotho | LS | en-US |
| Libéria | LR | en-US |
| Líbia | LY | en-US, ar-SA |
| Liechtenstein | LI | en-US, de-DE |
| Litvánia | LT | en-US, lt-LT |
| Luxemburg | LU | en-US, fr-FR |
| Makaó (KKT) | MO | en-US, zh-HK |
| Észak-Észak-Észak | MK | en-US |
| Madagaszkár | MG | en-US |
| Malawi | MW | en-US |
| Malajzia | MY | en-US, ms-MY |
| Maldív-szigetek | MV | en-US |
| Mali | ML | en-US |
| Málta | MT | en-US |
| Marshall-szigetek | MH | en-US |
| Martinique | MQ | en-US |
| Mauritánia | MR | en-US |
| Mauritius | Mu | en-US, ar-SA |
| Mayotte | YT | en-US |
| Mexikó | MX | en-US, es-ES |
| Mikronézia | FM | en-US |
| Moldova | MD | en-US, ro-RO |
| Monaco | MC | en-US, fr-FR |
| Mongólia | MN | en-US |
| Montenegró | ME | en-US |
| Montserrat | MS | en-US |
| Marokkó | MA | en-US, fr-FR, en-US |
| Mozambik | MZ | en-US |
| Mianmar | MM | en-US |
| Namíbia | NA | en-US |
| Nauru | NR | en-US |
| Nepál | NP | en-US |
| Hollandia | NL | en-US, nl-NL |
| Új-Kaledónia | NC | en-US |
| Új-Zéland | NZ | en-US |
| Nicaragua | NI | en-US, es-ES |
| Niger | NE | en-US |
| Nigéria | NG | en-US |
| Niue | NU | en-US |
| Norfolk-sziget | Nf | en-US |
| Északi Mariana-szigetek | MP | en-US |
| Norvégia | NO | en-US, nb-NO |
| Omán | OM | en-US, ar-SA |
| Pakisztán | PK | en-US |
| Palau | PW | en-US |
| Palesztin Hatóság | PS | en-US |
| Panama | PA | en-US, es-ES |
| Pápua Új-Guinea | Oldal | en-US |
| Paraguay | PY | en-US, es-ES |
| Peru | PE | en-US, es-ES |
| Fülöp-szigetek | PH | en-US |
| Pitcairn-szigetek | Pn | en-US |
| Lengyelország | PL | en-US, pl-PL |
| Portugália | PT | en-US, pt-PT |
| Puerto Rico | PR | en-US, en-US |
| Katar | QA | en-US, ar-SA |
| Réunion | RE | en-US |
| Románia | RO | en-US, ro-RO |
| Oroszország | RU | en-US, ru-RU |
| Ruanda | RW | en-US, fr-FR |
| Sémo Tomé és Príncipe | ST | en-US, fr-FR |
| Saba | Xs | en-US |
| Saint-Barthélemy | BL | en-US |
| Saint Kitts és Nevis | KN | en-US |
| Saint Lucia | Lc | en-US, en-US |
| Saint Martin | Mf | en-US, en-US |
| Saint-Pierre és Miquelon | PM | en-US |
| Saint Vincent és Grenadine-szigetek | VC | en-US |
| Szamoa | WS | en-US |
| San Marino | Sm | en-US |
| Szaúd-Arábia | SA | en-US |
| Szenegál | SN | en-US, fr-FR |
| Szerbia | RS | en-US, sr-Latn-RS, en-US |
| Seychelle-szigetek | SC | en-US |
| Sierra Leone | SL | en-US |
| Szingapúr | SG | en-US, zh-SG |
| Sint Eustatius | Xe | en-US |
| Sint Maarten | Sx | en-US, en-US |
| Szlovákia | SK | en-US, sk-SK |
| Szlovénia | SI | en-US, sl-SI |
| Salamon-szigetek | Sb | en-US |
| Szomália | SO | en-US |
| Dél-afrikai Köztársaság | ZA | en-US |
| Dél-Georgia és Déli-Sandwich-szigetek | Gs | en-US |
| Dél-Szudán | SS | en-US |
| Spanyolország | ES | en-US, es-ES, en-US, en-US |
| Srí Lanka | LK | en-US |
| St Majda, Ascension, Tristan da Canha | SH | en-US |
| Suriname | SR | en-US |
| Svalbard | Sj | en-US |
| Svédország | SE | en-US, sv-Standard kiadás |
| Svájc | CH | en-US, fr-FR, en-US, en-US |
| Tajvan | TW | en-US, zh-HK |
| Tádzsikisztán | Tj | en-US |
| Tanzánia | TZ | en-US |
| Thaiföld | TH | en-US, th-TH |
| Timor-Leste | TL | en-US |
| Togo | TG | en-US |
| Tokelau | Tk | en-US |
| Tonga | TO | en-US |
| Trinidad és Tobago | TT | en-US |
| Tunézia | TN | en-US, fr-FR, en-US |
| Törökország | TR | en-US, tr-TR |
| Türkmenisztán | TM | en-US |
| Turks- és Caicos-szigetek | TC | en-US |
| Tuvalu | TV | en-US |
| Az Usa-beli, outlying-szigetek | UM | en-US |
| Amerikai Virgin-szigetek | VI | en-US |
| Uganda | UG | en-US |
| Ukrajna | UA | en-US, uk-UA |
| Egyesült Arab Emírségek | AE | en-US, ar-SA |
| Egyesült Királyság | GB | en-US |
| Egyesült Államok | USA | en-US |
| Uruguay | UY | en-US, es-ES |
| Üzbegisztán | UZ | en-US, ru-RU |
| Vanuatu | Je | en-US |
| Vatikán | VA | en-US |
| Venezuela | VE | en-US, es-ES |
| Vietnam | VN | en-US, vi-VN |
| Wallis és Futuna | WF | en-US |
| Jemen | Ti | en-US, ar-SA |
| Zambia | ZM | en-US |
| Zimbabwe | ZW | en-US |
