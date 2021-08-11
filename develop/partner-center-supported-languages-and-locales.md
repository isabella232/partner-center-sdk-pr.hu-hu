---
title: Partnerközpont – támogatott nyelvek és területi beállítások
description: Az ISO2 és ISO3 által támogatott területi Partnerközpont.
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 6f2e1d50fa0f2ace2e94f4dbb5681e2164241ee57a85249136a55fce20893fbb
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997583"
---
# <a name="partner-center-supported-languages-and-locales"></a>Partnerközpont – támogatott nyelvek és területi beállítások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Egyes Partnerközpont API-khoz szükség van egy értékre, amely egy területi értéket, országot vagy régiót jelez. Az X-Locale REST Partnerközpont fejléchez például gyakran "language-country" ("en-US" vagy "english - Egyesült Államok") formátumú értékre van szükség. [](headers.md)

A Partnerközpont felügyelt API-kban a [CountryValidationRules/dotnet/api/microsoft.store.partnercenter.models.countryvalidationrules.countryvalidationrules) osztály és a [OfferCategory.Locale/dotnet/api/microsoft.store.partnercenter.models.offers.offercategory.locale), [ServiceRequest.CountryCode/dottquest.countrycode/dottnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.countrycode) vagy [CustomerBillingProfile.Culture/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile.culture) tulajdonságokhoz olyan sztringértékekre van szükség, amelyek egy nyelvet vagy országot/régiót (ISO2 nyelvi kód vagy ISO3 ország/régió kód formájában) jeleznek, vagy kulturális környezet (egy nyelvi azonosító és egy ország-/régiókód kombinálva).

Az alábbi táblázat az API-k által támogatott kulturális és nemzetközi szabványügyi szervezet (ISO) országkódokat Partnerközpont sorolja fel.

| Ország/régió                           | ISO Alpha 2 országkód | ISO Alpha 3 országkód | Támogatott kulturális környezet(ek)                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| Afganisztán                              | AF                       | Afg                      | ps-AF / en-US                         |
| Åland-szigetek                            | Ax                       | Ala                      | sv-Standard kiadás / en-US                         |
| Albánia                                  | AL                       | Alb                      | sq-AL / en-US                         |
| Algéria                                  | DZ                       | DZA                      | ar-DZ / en-US                         |
| Amerikai Szamoa                           | AS                       | ASM                      | en-US                                 |
| Andorra                                  | AD                       | ÉS                      | ca-ES / en-US                         |
| Angola                                   | AO                       | Ezelőtt                      | pt-PT / en-US                         |
| Anguilla                                 | Mesterséges intelligencia                       | Aia                      | en-US                                 |
| Antarktisz                               | Aq                       | Ata                      | en-US                                 |
| Antigua és Barbuda                      | AG                       | Atg                      | en-US                                 |
| Argentína                                | AR                       | Arg                      | es-AR / en-US                         |
| Örményország                                  | AM                       | ARM                      | hy-AM / en-US                         |
| Aruba                                    | Aw                       | ABW                      | nl-NL / en-US                         |
| Ausztrália                                | AU                       | Aus                      | en-AU / en-US                         |
| Ausztria                                  | AT                       | Aut                      | de-AT / en-US                         |
| Azerbajdzsán                               | AZ                       | AZE                      | az-Latn-AZ / en-US                    |
| Bahama-szigetek                                  | BS                       | BHS                      | en-GB / en-US                         |
| Bahrein                                  | BH                       | BHR                      | ar-BH / en-US                         |
| Banglades                               | BD                       | BGD                      | bn-BD / en-US                         |
| Barbados                                 | BB                       | Brb                      | en-GB / en-US                         |
| Belarusz                                  | BY                       | BLR                      | be-BY / en-US                         |
| Belgium                                  | BE                       | Bel                      | fr-BE / nl-BE / en-US                 |
| Belize                                   | BZ                       | BLZ                      | en-BZ / en-US                         |
| Benin                                    | BJ                       | BEN                      | fr-FR / en-US                         |
| Bermuda                                  | Bm                       | BMU                      | en-GB / en-US                         |
| Bhután                                   | BT                       | Btn                      | en-US                                 |
| Bolívia                                  | BO                       | Bol                      | es-BO / en-US                         |
| Bonaire                                  | Bq                       | Bes                      | nl-NL / en-US                         |
| Bosznia-Hercegovina                   | BA                       | Bih                      | bs-Latn-BA / en-US                    |
| Botswana                                 | BW                       | Bwa                      | en-GB / en-US                         |
| Bouvet-sziget                            | Bv                       | BVT                      | nb-NO / en-US                         |
| Brazília                                   | BR                       | Melltartó                      | pt-BR / en-US                         |
| Brit indiai-óceáni terület           | Io                       | IOT                      | en-US                                 |
| Brit Virgin-szigetek                   | VG                       | VGB                      | en-US                                 |
| Brunei                                   | BN                       | BRN                      | ms-BN / en-US                         |
| Bulgária                                 | BG                       | Bgr                      | bg-BG / en-US                         |
| Burkina Faso                             | BF                       | Bfa                      | fr-FR / en-US                         |
| Burundi                                  | BI                       | Bdi                      | fr-FR / en-US                         |
| Cabo Verde                               | CV                       | Cpv                      | pt-CV / en-US                         |
| Kambodzsa                                 | KH                       | KHM                      | km-KH / en-US                         |
| Kamerun                                 | CM                       | Cmr                      | fr-FR / en-US                         |
| Kanada                                   | CA                       | Cna                      | fr-CA / en-US                         |
| Kajmán-szigetek                           | KY                       | CYM                      | en-GB / en-US                         |
| Közép-afrikai Köztársaság                 | CF                       | Caf                      | fr-FR / en-US                         |
| Csád                                     | TD                       | TCD                      | fr-FR / en-US                         |
| Chile                                    | CL                       | Chl                      | es-CL / en-US                         |
| Kína                                    | CN                       | Chn                      | zh-CN / en-US                         |
| Karácsony-sziget                         | CX                       | CXR                      | en-US                                 |
| Cocos (Keeling)-szigetek                  | CC                       | Cck                      | en-US                                 |
| Kolumbia                                 | CO                       | Col                      | es-CO / en-US                         |
| Comore-szigetek                                  | Km                       | Com                      | fr-FR / en-US                         |
| Kongó                                    | Cg                       | Cog                      | fr-FR / en-US                         |
| Kongó (KDK)                              | CD                       | Cég tulajdonában lévő eszközök (COD)                      | fr-FR / en-US                         |
| Cook-szigetek                             | Ck                       | Cok                      | en-US                                 |
| Costa Rica                               | CR                       | Cri                      | es-CR / en-US                         |
| Côte d'Ivoire                            | CI                       | Civ                      | fr-FR / en-US                         |
| Horvátország                                  | HR                       | Hrv                      | hr-HR / en-US                         |
| Curaçao                                  | Cw                       | CUW                      | nl-NL / en-US                         |
| Ciprus                                   | CY                       | Cyp                      | el-GR / en-US                         |
| Csehország                                  | CZ                       | Cze                      | cs-PT / en-US                         |
| Dánia                                  | DK                       | DNK                      | da-DK / en-US                         |
| Dzsibuti                                 | Dj                       | DJI                      | fr-FR / en-US                         |
| Dominika                                 | DM                       | DMA                      | en-US                                 |
| Dominikai Köztársaság                       | DO                       | Dom                      | es-DO / en-US                         |
| Ecuador                                  | EC                       | Ecu                      | es-EC / en-US                         |
| Egyiptom                                    | EG                       | A                      | ar-EG / en-US                         |
| Salvador                              | SV                       | Slv                      | es-SV / en-US                         |
| Egyenlítői-Guinea                        | Gq                       | GNQ                      | es-ES / en-US                         |
| Eritrea                                  | ER                       | Eri                      | ar-SA / en-US                         |
| Észtország                                  | EE                       | Est                      | et-Enterprise kiadás / en-US                         |
| eSwatini                                 | SZ                       | SWZ                      | en-US                                 |
| Etiópia                                 | ET                       | Eth                      | am-ET / en-US                         |
| Falkland-szigetek                         | Fk                       | Flk                      | en-US                                 |
| Feröer szigetek                            | FO                       | Oda                      | fo-FO / en-US                         |
| Fidzsi                                     | FJ                       | FJI                      | en-GB / en-US                         |
| Finnország                                  | FI                       | FIN                      | fi-FI / sv-FI / en-US                 |
| Franciaország                                   | JK                       | FRA                      | fr-FR / en-US                         |
| Francia Guyana                            | GF                       | GUF                      | fr-FR / en-US                         |
| Francia Polinézia                         | PF                       | PYF                      | fr-FR / en-US                         |
| Francia Déli Területek              | Tf                       | Atf                      | fr-FR / en-US                         |
| Gabon                                    | FE                       | Gab                      | fr-FR / en-US                         |
| Gambia                                   | GM                       | GMB                      | en-US                                 |
| Grúzia                                  | GE                       | Geo                      | ka-GE / en-US                         |
| Németország                                  | DE                       | DEU                      | de-DE / en-US                         |
| Ghána                                    | GH                       | GHA                      | en-GB / en-US                         |
| Gibraltár                                | Gi                       | Gib                      | en-US                                 |
| Görögország                                   | GR                       | GRC                      | el-GR / en-US                         |
| Grönland                                | Gl                       | Grl                      | da-DK / en-US                         |
| Grenada                                  | Gd                       | Grd                      | en-US                                 |
| Guadeloupe                               | GP                       | Glp                      | fr-FR / en-US                         |
| Guam                                     | GU                       | Gumi                      | en-US                                 |
| Guatemala                                | GT                       | GTM                      | es-GT / en-US                         |
| Guernsey                                 | Gg                       | <                      | en-US                                 |
| Guinea                                   | GN                       | Gin                      | fr-FR / en-US                         |
| Bissau-Guinea                            | Gw                       | Gnb                      | pt-PT / en-US                         |
| Guyana                                   | GY                       | Srác                      | en-US                                 |
| Haiti                                    | HT                       | Hti                      | fr-FR / en-US                         |
| Heard-sziget és McDonald-szigetek        | Hm                       | Hmd                      | en-US                                 |
| Honduras                                 | HN                       | HND                      | es-HN / en-US                         |
| Hongkong (KKT)                            | HK                       | HKG                      | zh-HK / en-US                         |
| Magyarország                                  | HU                       | HUN                      | hu-HU / en-US                         |
| Izland                                  | IS                       | Isl                      | is-IS / en-US                         |
| India                                    | IN                       | IND                      | en-IN / hi-IN / en-US                 |
| Indonézia                                | ID (Azonosító)                       | Idn                      | id-ID / en-US                         |
| Irak                                     | IQ                       | Irq                      | ar-IQ / en-US                         |
| Írország                                  | IE                       | Irl                      | en-IE / en-US                         |
| Man-sziget                              | Csevegés                       | IMN                      | en-US                                 |
| Izrael                                   | IL                       | ISR                      | he-IL / en-US                         |
| Olaszország                                    | IT                       | ITA                      | it-IT / en-US                         |
| Jamaica                                  | JM                       | Jam                      | en-JM / en-US                         |
| Jan Mayen                                | Xj                       | XJA                      | nb-NO / en-US                         |
| Japán                                    | JP                       | JPN                      | ja-JP / en-US                         |
| Jersey                                   | JE                       | Jey                      | en-US                                 |
| Jordánia                                   | JO                       | JOR                      | ar-JO / en-US                         |
| Kazahsztán                               | KZ                       | Kaz                      | kk-KZ / en-US                         |
| Kenya                                    | KE                       | Ken                      | sw-KE / en-US                         |
| Kiribati                                 | KI                       | Kir                      | en-US                                 |
| Dél-Korea                                    | KR                       | KOR                      | ko-KR / en-US                         |
| Koszovó                                   | Xk                       | XKS                      | en-US                                 |
| Kuvait                                   | KW                       | T                      | ar-MAJD / en-US                         |
| Kirgizisztán                               | KG                       | KGZ                      | ky-KG / en-US                         |
| Laosz                                     | LA                       | Lao                      | lo-LA / en-US                         |
| Lettország                                   | LV                       | Lva                      | lv-LV / en-US                         |
| Libanon                                  | LB                       | LBN                      | ar-LB / en-US                         |
| Lesotho                                  | LS                       | LSO                      | en-US                                 |
| Libéria                                  | LR                       | LBR                      | en-US                                 |
| Líbia                                    | LY                       | LBY                      | ar-LY / en-US                         |
| Liechtenstein                            | LI                       | Hazugság                      | de-LI / en-US                         |
| Litvánia                                | LT                       | Ltu                      | lt-LT / en-US                         |
| Luxemburg                               | LU                       | Lux                      | de-LU / fr-LU / en-US                 |
| Makaó (KKT)                                | MO                       | Mac                      | zh-MO / en-US                         |
| Észak-Észak-Észak                          | MK                       | Mkd                      | mk-MK / en-US                         |
| Madagaszkár                               | MG                       | Mfc                      | fr-FR / en-US                         |
| Malawi                                   | MW                       | MWI                      | en-US                                 |
| Malajzia                                 | MY                       | Mys                      | en-MY / en-US                         |
| Maldív-szigetek                                 | MV                       | MDV                      | dv-MV / en-US                         |
| Mali                                     | ML                       | MLI                      | fr-FR / en-US                         |
| Málta                                    | MT                       | Mlt                      | mt-MT / en-US                         |
| Marshall-szigetek                         | MH                       | MHL                      | en-US                                 |
| Martinique                               | MQ                       | MTQ                      | fr-FR / en-US                         |
| Mauritánia                               | MR                       | Mrt                      | ar-SA / en-US                         |
| Mauritius                                | Mu                       | Mus                      | en-GB / en-US                         |
| Mayotte                                  | YT                       | MYT                      | fr-FR / en-US                         |
| Mexikó                                   | MX                       | Mex                      | es-MX / en-US                         |
| Mikronézia                               | FM                       | Mszá                      | en-US                                 |
| Moldova                                  | MD                       | Mda                      | ro-RO / en-US                         |
| Monaco                                   | MC                       | Orlando                      | fr-MC / en-US                         |
| Mongólia                                 | MN                       | Mng                      | mn-MN / en-US                         |
| Montenegró                               | ME                       | MNE                      | sr-Latn-ME / en-US                    |
| Montserrat                               | MS                       | Msr                      | en-US                                 |
| Marokkó                                  | MA                       | MÁRC                      | ar-MA / en-US                         |
| Mozambik                               | MZ                       | Moz                      | pt-PT                                 |
| Mianmar                                  | MM                       | Mmr                      | en-US                                 |
| Namíbia                                  | NA                       | Nam                      | en-GB / en-US                         |
| Nauru                                    | NR                       | NRU                      | en-US                                 |
| Nepál                                    | NP                       | NPL                      | ne-NP / en-US                         |
| Holland Antillák                     | Egy                       | Hangya                      | en-US                                 |
| Holland, A                         | NL                       | NLD                      | nl-NL / en-US                         |
| Új-Kaledónia                            | NC                       | NCL                      | fr-FR / en-US                         |
| Új-Zéland                              | NZ                       | Nzl                      | en-NZ / en-US                         |
| Nicaragua                                | NI                       | Hálózati adapter                      | es-NI / en-US                         |
| Niger                                    | NE                       | Ner                      | fr-FR / en-US                         |
| Nigéria                                  | NG                       | Nga                      | ha-Latn-NG / en-US                    |
| Niue                                     | NU                       | Niu                      | en-US                                 |
| Norfolk-sziget                           | Nf                       | NFK                      | en-US                                 |
| Északi Mariana-szigetek                 | MP                       | MNP                      | en-US                                 |
| Norvégia                                   | NO                       | NOR                      | nb-NO / en-US                         |
| Omán                                     | OM                       | OMN                      | ar-OM / en-US                         |
| Pakisztán                                 | PK                       | Pak                      | your-PK / en-US                         |
| Palau                                    | PW                       | PLW                      | en-US                                 |
| Palesztin Hatóság                    | PS                       | Pse                      | ar-SA / en-US                         |
| Panama                                   | PA                       | PAN                      | es-PA / en-US                         |
| Pápua Új-Guinea                         | Oldal                       | PNG                      | en-US                                 |
| Paraguay                                 | PY                       | Kandikál                      | es-PY / en-US                         |
| Peru                                     | PE                       | PER                      | es-PE / en-US                         |
| Fülöp-szigetek                              | PH                       | PHL                      | en-PH / en-US                         |
| Pitcairn-szigetek                         | Pn                       | PcN                      | en-US                                 |
| Lengyelország                                   | PL                       | Pol                      | pl-PL / en-US                         |
| Portugália                                 | PT                       | Prt                      | pt-PT / en-US                         |
| Puerto Rico                              | PR                       | Pri                      | es-PR / en-US                         |
| Katar                                    | QA                       | Minőségbiztosítási                      | ar-QA / en-US                         |
| Réunion                                  | RE                       | ReU                      | fr-FR / en-US                         |
| Románia                                  | RO                       | Rou                      | ro-RO / en-US                         |
| Oroszország                                   | RU                       | RUS                      | ru-RU / en-US                         |
| Ruanda                                   | RW                       | RWA                      | rw-RW / en-US                         |
| Saba                                     | Xs                       | XSA                      | nl-NL / en-US                         |
| Saint Kitts és Nevis                    | KN                       | Kna                      | en-GB / en-US                         |
| Saint Lucia                              | Lc                       | Lca                      | en-US                                 |
| Saint Martin                             | Mf                       | Maf                      | fr-FR / en-US                         |
| Saint-Pierre és Miquelon                | PM                       | Spm                      | fr-FR / en-US                         |
| Saint Vincent és Grenadine-szigetek         | VC                       | VCT                      | en-US                                 |
| Saint-Barthélemy                         | BL                       | Blm                      | fr-FR / en-US                         |
| Szamoa                                    | WS                       | WSM                      | en-US                                 |
| San Marino                               | Sm                       | Smr                      | it-IT / en-US                         |
| Sémo Tomé és Príncipe                    | ST                       | Stp                      | pt-PT / en-US                         |
| Szaúd-Arábia                             | SA                       | Sau                      | ar-SA / en-US                         |
| Szenegál                                  | SN                       | Szenátor                      | wo-SN / en-US                         |
| Szerbia                                   | RS                       | Srb                      | sr-Latn-RS / sr-Cyrl-RS / en-US       |
| Seychelle-szigetek                               | SC                       | SYC                      | en-US                                 |
| Sierra Leone                             | SL                       | Sle                      | en-US                                 |
| Szingapúr                                | SG                       | Snp                      | en-SG / zh-SG / en-US                 |
| Sint Eustatius                           | Xe                       | XSE                      | nl-NL / en-US                         |
| Sint Maarten                             | Sx                       | SXM                      | en-US                                 |
| Szlovákia                                 | SK                       | Svk                      | sk-SK / en-US                         |
| Szlovénia                                 | SI                       | Svn                      | sl-SI / en-US                         |
| Salamon-szigetek                          | Sb                       | SLB                      | en-US                                 |
| Szomália                                  | SO                       | Szom                      | ar-SA / en-US                         |
| Dél-afrikai Köztársaság                             | ZA                       | ZAF                      | en-ZA / en-US                         |
| Dél-Georgia és Déli-Sandwich-szigetek | Gs                       | Sgs                      | en-US                                 |
| Dél-Szudán                              | SS                       | SSD                      | en-US                                 |
| Spanyolország                                    | ES                       | Esp                      | es-ES / ca-ES / eu-ES / ft-ES / en-US |
| Srí Lanka                                | LK                       | LKA                      | si-LK / en-US                         |
| St Foga, Ascension, Tristan da Amilyenha   | SH                       | Shn                      | en-US                                 |
| Suriname                                 | SR                       | Sur                      | nl-NL                                 |
| Svalbard                                 | Sj                       | SJM                      | nb-NO / en-US                         |
| Svédország                                   | SE                       | Swe                      | sv-Standard kiadás / en-US                         |
| Svájc                              | CH                       | Che                      | de-CH / fr-CH / it-CH / en-US         |
| Tajvan                                   | TW                       | TWN                      | zh-TW / en-US                         |
| Tádzsikisztán                               | Tj                       | Tjk                      | tg-Cyrl-TJ / en-US                    |
| Tanzánia                                 | TZ                       | TZA                      | en-GB / en-US                         |
| Thaiföld                                 | TH                       | Tha                      | th-TH / en-US                         |
| Timor-Leste                              | TL                       | TLS                      | pt-PT / en-US                         |
| Togo                                     | TG                       | TGO                      | fr-FR / en-US                         |
| Tokelau                                  | Tk                       | TKL                      | en-US                                 |
| Tonga                                    | TO                       | Tonna                      | en-US                                 |
| Trinidad és Tobago                      | TT                       | TTO                      | en-TT / en-US                         |
| Tunézia                                  | TN                       | Tun                      | ar-TN / en-US                         |
| Törökország                                   | TR                       | Tur                      | tr-TR / en-US                         |
| Türkmenisztán                             | TM                       | TKM                      | tk-TM / en-US                         |
| Turks- és Caicos-szigetek                 | TC                       | Tca                      | en-US                                 |
| Tuvalu                                   | TV                       | TUV                      | en-US                                 |
| Uganda                                   | UG                       | UGA                      | en-GB / en-US                         |
| Ukrajna                                  | UA                       | Ukr                      | uk-UA / en-US                         |
| Egyesült Arab Emírségek                     | AE                       | ARE                      | ar-AE / en-US                         |
| Egyesült Királyság                           | GB                       | Gbr                      | en-GB / en-US                         |
| Az Usa-beli, outlying-szigetek                    | UM                       | Umi                      | en-US                                 |
| Amerikai Virgin-szigetek                      | VI                       | Vir                      | en-US                                 |
| Egyesült Államok                            | USA                       | USA                      | en-US / es-US                         |
| Uruguay                                  | UY                       | Ury                      | es-UY / en-US                         |
| Üzbegisztán                               | UZ                       | UZB                      | uz-Latn-UZ / en-US                    |
| Vanuatu                                  | Je                       | VUT (VUT)                      | en-US                                 |
| Vatikán                             | VA                       | Áfa                      | it-IT / en-US                         |
| Venezuela                                | VE                       | Ven                      | es-VE / en-US                         |
| Vietnam                                  | VN                       | VNM                      | vi-VN / en-US                         |
| Wallis és Futuna                        | WF                       | WLF                      | fr-FR / en-US                         |
| Jemen                                    | Ti                       | YEM                      | ar-YE / en-US                         |
| Zambia                                   | ZM                       | ZMB                      | en-GB / en-US                         |
| Zimbabwe                                 | ZW                       | ZWE                      | en-ZW / en-US                         |

