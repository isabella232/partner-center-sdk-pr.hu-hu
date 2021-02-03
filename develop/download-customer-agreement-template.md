---
title: Letöltési hivatkozás letöltése a Microsoft ügyfél-szerződési sablonhoz
description: Szerezze be a Microsoft ügyfél-szerződési sablonjának letöltési hivatkozását.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8c794d264ad64a42fa6ca823ddfc3841248c01cd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767991"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Letöltési hivatkozás letöltése a Microsoft ügyfél-szerződési sablonhoz

**A következőkre vonatkozik:**

- Partnerközpont

A **AgreementDocument** erőforrást jelenleg csak a *Microsoft nyilvános felhőben* támogatja a partner Center. Ez az erőforrás nem vonatkozik a következőkre:

- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ez a cikk azt ismerteti, hogyan kérhet le egy hivatkozást a Microsoft Customer szerződés sablonjának letöltésére az ügyfél országa és nyelve alapján.

## <a name="prerequisites"></a>Előfeltételek

- Ha a partner Center .NET SDK-t használja, a 1,14-es vagy újabb verzió szükséges.

- A [partner Center-hitelesítésben](./partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítést támogatja.

- Az ügyfél azon országa, amelyhez a Microsoft Customer Agreement-sablon vonatkozik.

- Az a nyelv, amelyben a Microsoft Customer Agreement sablon honosítva van.

> [!IMPORTANT]
>
> - A Microsoft Customer szerződés országspecifikus. Ha a Microsoft ügyfél-szerződési sablon letöltésére vonatkozó kérést kér, ügyeljen arra, hogy a megfelelő országot határozza meg az ügyfél helye alapján. a támogatott országok listáját a [támogatott országok és nyelvek listájában](#list-of-supported-countries-and-languages)találja.
>
> - Egyes országokban a Microsoft Customer szerződés több nyelven is elérhető. A legjobb felhasználói élmény érdekében válassza ki az ügyfél igényeinek leginkább megfelelő nyelvet. A támogatott nyelvek listáját a [támogatott országok és nyelvek listáját](#list-of-supported-countries-and-languages)ismertető témakörben tekintheti meg.
> - Ezt a módszert csak a Microsoft ügyfél-szerződése támogatja.

## <a name="net"></a>.NET

A Microsoft ügyfél-szerződési sablon letöltésére szolgáló hivatkozás lekérése:

1. Kérje le a Microsoft Customer szerződéshez tartozó szerződési metaadatokat. Be kell szereznie a Microsoft Customer szerződés **templateId** . További információ: [a szerződés metaadatainak beszerzése a Microsoft ügyfél-szerződéshez](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Használja a IAggregatePartner. AgreementTemplates gyűjteményt.

3. Hívja meg a **ById** metódust, és határozza meg a Microsoft Customer szerződés **templateId** .

4. A **dokumentum** tulajdonságának beolvasása.

5. Hívja meg a **ByCountry** metódust, és határozza meg az ügyfél azon országát, amelyre a szerződési sablon vonatkozik. A lekérdezés alapértelmezett értéke *számunkra* , ha nincs megadva a metódus. A támogatott országkódok listáját a [támogatott országok és nyelvek listáját](#list-of-supported-countries-and-languages)ismertető témakörben tekintheti meg. Ez a módszer **megkülönbözteti a kis-és** nagybetűket.

6. Hívja meg a **ByLanguage** metódust, és határozza meg, hogy milyen nyelven kell honosítani a szerződés sablonját. A lekérdezés alapértelmezés szerint az *en-us* értéket adja meg, ha nincs megadva a metódus, vagy a megadott országkód nem támogatott a megadott ország esetében. A támogatott nyelvi kódok listájáért tekintse meg a [támogatott országok és nyelvek listáját](#list-of-supported-countries-and-languages).

7. Hívja meg a **Get** vagy a **GetAsync** metódust.

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

Teljes minta a [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) osztályban található a [konzol tesztelése alkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektben.

## <a name="rest-request"></a>REST-kérelem

A Microsoft ügyfél-szerződési sablon letöltésére szolgáló hivatkozás lekérése:

1. Kérje le a Microsoft Customer szerződéshez tartozó szerződési metaadatokat. Be kell szereznie a Microsoft Customer szerződés **templateId** . További információ: [a szerződés metaadatainak beszerzése a Microsoft ügyfél-szerződéshez](get-customer-agreement-metadata.md).

2. Hozzon létre egy REST-kérést egy [ **AgreementDocument** -erőforrás](./agreement-document-resources.md)beolvasásához. Példaként tekintse meg a [kérelem szintaxisának](#request-syntax) példáját. A következő adatokat kell megadnia:

    - A Microsoft Customer szerződés **templateId** .
    - Az az ország, amelyre a Microsoft Customer Agreement-sablon vonatkozik.
    - Az a nyelv, amelyben a Microsoft Customer Agreement sablon honosítva van.

### <a name="request-syntax"></a>Kérelem szintaxisa

Használja a következő kérelem szintaxisát ehhez az erőforráshoz:

| Metódus | Kérés URI-ja |
|--------|---------------------------------------------------------------------|
| GET | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreementtemplates/{Agreement-template-ID}/Document? Language = {Language} &ország = {ország} http/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

A kérelemhez a következő URI-paramétereket használhatja:

| Név                   | Típus   | Kötelező | Leírás                                 |
|------------------------|--------|----------|---------------------------------------------|
| szerződés – sablon-azonosító  | sztring | Igen      | A szerződés típusának egyedi azonosítója. A Microsoft ügyfél-szerződéshez tartozó templateId beszerezheti a Microsoft-szerződés metaadatainak beolvasásával. További információ: [a szerződés metaadatainak beszerzése a Microsoft ügyfél-szerződéshez](./get-customer-agreement-metadata.md). Ez a paraméter **megkülönbözteti a kis-és nagybetűket**.|
| ország                | sztring | No       | Azt az országot jelzi, amelyre a szerződési sablon vonatkozik. A lekérdezés alapértelmezett értéke *számunkra* , ha nincs megadva a paraméter. A támogatott országkódok listáját a [támogatott országok és nyelvek listáját](#list-of-supported-countries-and-languages)ismertető témakörben tekintheti meg.|
| language               | sztring | No       | A szerződési sablon honosított nyelvét jelzi. A lekérdezés alapértelmezés szerint az *en-us* értéket adja meg, ha nincs megadva a paraméter, vagy a megadott országkód a megadott in 't támogatott. A támogatott országkódok listájáért tekintse meg a [támogatott országok és nyelvek listáját](#list-of-supported-countries-and-languages).|

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

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

Ha ez sikeres, ez a metódus egy [ **AgreementDocument** -erőforrást](./agreement-document-resources.md) ad vissza a válasz törzsében.

Az erőforrás egy **downloadUri** tulajdonsággal rendelkezik, amely egy URL-karakterláncot tartalmaz, amely a szerződés sablonjának letöltésére használható. A rendszer minden alkalommal egy másik hivatkozást ad vissza, amikor lekérdezést végez. Ez a hivatkozás öt perc után lejár.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.

A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

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
> Az országkód tulajdonság megkülönbözteti a kis-és nagybetűket. Ügyeljen arra, hogy az alábbi táblázatban megadott megfelelő burkolatot használja.

| Ország                   | Országkód   | Támogatott nyelvi kód (ok) |
|------------------------|--------|----------|
| Åland-szigetek | AX | en-US |
| Afganisztán | AF | en-US |
| Albánia | AL | en-US |
| Algéria | DZ | en-US, fr-FR, en-US |
| Amerikai Szamoa | AS | en-US |
| Andorra | AD | en-US |
| Angola | AO | en-US, PT-PT |
| Anguilla | Mesterséges intelligencia | en-US |
| Antarktisz | AQ | en-US |
| Antigua és Barbuda | AG | en-US |
| Argentína | AR | en-US, es-ES |
| Örményország | AM | en-US |
| Aruba | AW | en-US |
| Ausztrália | AU | en-US |
| Ausztria | AT | en-US, de-DE |
| Azerbajdzsán | AZ | en-US |
| Bahama-szigetek | BS | en-US |
| Bahrein | BH | en-US, AR-SA |
| Banglades | BD | en-US |
| Barbados | BB | en-US |
| Belarusz | BY | en-US, ru-RU |
| Belgium | BE | en-US, NL-NL |
| Belize | BZ | en-US, es-ES |
| Benin | BJ | en-US |
| Bermuda | BM | en-US |
| Bhután | BT | en-US |
| Bolívia | BO | en-US, es-ES |
| Bonaire | BQ | en-US |
| Bosznia-Hercegovina | BA | en-US |
| Botswana | BW | en-US |
| Bouvet-sziget | BV | en-US |
| Brazília | BR | en-US, PT-BR |
| Brit indiai-óceáni terület | IO | en-US |
| Brit Virgin-szigetek | VG | en-US |
| Brunei | BN | en-US |
| Bulgária | BG | en-US, BG-BG |
| Burkina Faso | BF | en-US |
| Burundi | BI | en-US |
| Côte d'Ivoire | CI | en-US, fr-FR |
| Cabo Verde | CV | en-US, PT-PT |
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
| Comore-szigetek | KM | en-US |
| Kongó (KDK) | CD | en-US |
| Kongó | CG | en-US |
| Cook-szigetek | CK | en-US |
| Costa Rica | CR | en-US, es-ES |
| Horvátország | HR | en-US, HR – HR |
| Curaçao | CW | en-US |
| Ciprus | CY | en-US |
| Csehország | CZ | en-US, CS-CZ |
| Dánia | DK | en-US, da-DK |
| Dzsibuti | DJ | en-US |
| Dominika | DM | en-US |
| Dominikai Köztársaság | DO | en-US, es-ES |
| Ecuador | EC | en-US |
| Egyiptom | EG | en-US, AR-SA |
| Salvador | SV | en-US, es-ES |
| Egyenlítői-Guinea | GQ | en-US |
| Eritrea | ER | en-US |
| Észtország | EE | en-US, et-EE |
| eSwatini | SZ | en-US |
| Etiópia | ET | en-US |
| Falkland-szigetek | FK | en-US |
| Feröer szigetek | UTCÁN | en-US |
| Fidzsi | FJ | en-US |
| Finnország | FI | en-US, fi-FI |
| Franciaország | JK | en-US, fr-FR |
| Francia Guyana | GF | en-US, fr-FR  |
| Francia Polinézia | PF | en-US |
| Francia Déli Területek | TF | en-US |
| Gabon | FE | en-US |
| Gambia | GM | en-US |
| Grúzia | GE | en-US |
| Németország | DE | en-US, de-DE |
| Ghána | GH | en-US |
| Gibraltár | GI | en-US |
| Görögország | GR | en-US, el-GR |
| Grönland | GL | en-US |
| Grenada | GD | en-US |
| Guadeloupe | GP | en-US |
| Guam | GU | en-US |
| Guatemala | GT | en-US, es-ES |
| Guernsey | GG | en-US |
| Guinea | GN | en-US |
| Bissau-Guinea | GW | en-US |
| Guyana | GY | en-US |
| Haiti | HT | en-US |
| Heard-sziget és McDonald-szigetek | HM | en-US |
| Honduras | HN | en-US, es-ES |
| Hongkong (KKT) | HK | en-US, ZH-HK |
| Magyarország | HU | en-US, hu-HU |
| Izland | IS | en-US |
| India | IN | en-US, Hi-IN |
| Indonézia | ID (Azonosító) | en-US, azonosító-azonosító |
| Irak | IQ | en-US, AR-SA |
| Írország | IE | en-US |
| Man-sziget | Csevegés | en-US |
| Izrael | IL | en-US, it-IL |
| Olaszország | IT | en-US, IT-IT |
| Jamaica | JM | en-US |
| Jan Mayen | XJ | en-US |
| Japán | JP | en-US, ja-JP |
| Jersey | JE | en-US |
| Jordánia | JO | en-US, AR-SA |
| Kazahsztán | KZ | en-US, KK – KZ |
| Kenya | KE | en-US |
| Kiribati | KI | en-US |
| Dél-Korea | KR | en-US, ko-KR |
| Koszovó | XK | en-US |
| Kuvait | KW | en-US, AR-SA |
| Kirgizisztán | KG | en-US, ru-RU |
| Laosz | LA | en-US |
| Lettország | LV | en-US, LV-LV |
| Libanon | LB | en-US, AR-SA |
| Lesotho | LS | en-US |
| Libéria | LR | en-US |
| Líbia | LY | en-US, AR-SA |
| Liechtenstein | LI | en-US, de-DE |
| Litvánia | LT | en-US, lt-LT |
| Luxemburg | LU | en-US, fr-FR |
| Makaó (KKT) | MO | en-US, ZH-HK |
| Macedónia, V.J.K. | MK | en-US |
| Madagaszkár | MG | en-US |
| Malawi | MW | en-US |
| Malajzia | MY | en-US, MS – saját |
| Maldív-szigetek | MV | en-US |
| Mali | ML | en-US |
| Málta | MT | en-US |
| Marshall-szigetek | MH | en-US |
| Martinique | MQ | en-US |
| Mauritánia | MR | en-US |
| Mauritius | MU | en-US, AR-SA |
| Mayotte | YT | en-US |
| Mexikó | MX | en-US, es-ES |
| Mikronézia | FM | en-US |
| Moldova | MD | en-US, RO-RO |
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
| Hollandia | NL | en-US, NL-NL |
| Új-Kaledónia | NC | en-US |
| Új-Zéland | NZ | en-US |
| Nicaragua | NI | en-US, es-ES |
| Niger | NE | en-US |
| Nigéria | NG | en-US |
| Niue | NU | en-US |
| Norfolk-sziget | NF | en-US |
| Északi Mariana-szigetek | MP | en-US |
| Norvégia | NO | en-US, NB-nem |
| Omán | OM | en-US, AR-SA |
| Pakisztán | PK | en-US |
| Palau | PW | en-US |
| Palesztin Hatóság | PS | en-US |
| Panama | PA | en-US, es-ES |
| Pápua Új-Guinea | PG | en-US |
| Paraguay | PY | en-US, es-ES |
| Peru | PE | en-US, es-ES |
| Fülöp-szigetek | PH | en-US |
| Pitcairn-szigetek | PN | en-US |
| Lengyelország | PL | en-US, pl-PL |
| Portugália | PT | en-US, PT-PT |
| Puerto Rico | PR | en-US, en-US |
| Katar | QA | en-US, AR-SA |
| Réunion | RE | en-US |
| Románia | RO | en-US, RO-RO |
| Oroszország | RU | en-US, ru-RU |
| Ruanda | RW | en-US, fr-FR |
| São Tomé és Príncipe | ST | en-US, fr-FR |
| Saba | XS | en-US |
| Saint-Barthélemy | BL | en-US |
| Saint Kitts és Nevis | KN | en-US |
| Saint Lucia | LC | en-US, en-US |
| Saint Martin | MF | en-US, en-US |
| Saint-Pierre és Miquelon | PM | en-US |
| Saint Vincent és Grenadine-szigetek | VC | en-US |
| Szamoa | WS | en-US |
| San Marino | SM | en-US |
| Szaúd-Arábia | SA | en-US |
| Szenegál | SN | en-US, fr-FR |
| Szerbia | RS | en-US, SR-Latn-RS, en-US |
| Seychelle-szigetek | SC | en-US |
| Sierra Leone | SL | en-US |
| Szingapúr | SG | en-US, zh-SG |
| Sint Eustatius | XE | en-US |
| Sint Maarten | SX | en-US, en-US |
| Szlovákia | SK | en-US, SK-SK |
| Szlovénia | SI | en-US, SL-SI |
| Salamon-szigetek | SB | en-US |
| Szomália | SO | en-US |
| Dél-afrikai Köztársaság | ZA | en-US |
| Dél-Georgia és Déli-Sandwich-szigetek | GS | en-US |
| Dél-Szudán | SS | en-US |
| Spanyolország | ES | en-US, es-ES, en-US, en-us |
| Srí Lanka | LK | en-US |
| Szent Ilona, Ascension, Tristan da Cunha | SH | en-US |
| Suriname | SR | en-US |
| Svalbard | SJ | en-US |
| Svédország | SE | en-US, Sv-SE |
| Svájc | CH | en-US, fr-FR, en-US, en-us |
| Tajvan | TW | en-US, ZH-HK |
| Tádzsikisztán | TJ | en-US |
| Tanzánia | TZ | en-US |
| Thaiföld | TH | en-US, th-TH |
| Timor-Leste | TL | en-US |
| Togo | TG | en-US |
| Tokelau | TK | en-US |
| Tonga | TO | en-US |
| Trinidad és Tobago | TT | en-US |
| Tunézia | TN | en-US, fr-FR, en-US |
| Törökország | TR | en-US, TR-TR |
| Türkmenisztán | TM | en-US |
| Turks- és Caicos-szigetek | TC | en-US |
| Tuvalu | TV | en-US |
| Amerikai Egyesült Államok lakatlan külbirtokai | UM | en-US |
| Amerikai Virgin-szigetek | VI | en-US |
| Uganda | UG | en-US |
| Ukrajna | UA | en-US, Egyesült Királyság – UA |
| Egyesült Arab Emírségek | AE | en-US, AR-SA |
| Egyesült Királyság | GB | en-US |
| Egyesült Államok | USA | en-US |
| Uruguay | UY | en-US, es-ES |
| Üzbegisztán | UZ | en-US, ru-RU |
| Vanuatu | JE | en-US |
| Vatikán | VA | en-US |
| Venezuela | VE | en-US, es-ES |
| Vietnam | VN | en-US, VI – VN |
| Wallis és Futuna | WF | en-US |
| Jemen | TI | en-US, AR-SA |
| Zambia | ZM | en-US |
| Zimbabwe | ZW | en-US |
