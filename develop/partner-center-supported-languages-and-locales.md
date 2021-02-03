---
title: Partnerközpont – támogatott nyelvek és területi beállítások
description: A ISO2 és a ISO3 által támogatott területi beállítások listája.
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 5f428bf9104fec3e4855706e8786ad3941875f3d
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768044"
---
# <a name="partner-center-supported-languages-and-locales"></a>Partnerközpont – támogatott nyelvek és területi beállítások

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Bizonyos partneri központ API-k olyan értéket igényelnek, amely területi beállításokat, országot vagy régiót jelez. Például a [partner Center Rest-fejléc](headers.md) X-locale értékének gyakran a "Language-Country" formátumúnak kell lennie (az "en-us" kifejezés a "English-Egyesült Államok" értéket jelöli).

A partner Center által felügyelt API-kon a [CountryValidationRules/DotNet/API/Microsoft. Store. partnercenter. models. CountryValidationRules. CountryValidationRules) osztály és a [OfferCategory. locale/DotNet/API/Microsoft. Store. partnercenter. models. OfferCategory. locale, [ServiceRequest. országhívószám/DotNet/API/Microsoft. Store. partnercenter. models. servicerequests. ServiceRequest. országhívószám), vagy [CustomerBillingProfile. Culture/DotNet/API/Microsoft. Store. partnercenter. models. customers. CustomerBillingProfile. Culture) a tulajdonságok olyan karakterlánc-értékeket igényelnek, amelyek egy nyelvet vagy országot/régiót (ISO2 nyelvi kód vagy ISO3 ország/régió kódja), a területi beállításokat vagy a kulturális környezetet (az ország/régió kódjával együtt) jelölik.

A következő táblázat a partner Center API-k által támogatott kulturális és nemzetközi szabványügyi szervezet (ISO) országkódok listáját tartalmazza.

| Ország/régió                           | ISO Alpha 2 országkód | ISO Alpha 3 országkód | Támogatott kulturális környezet (ek)                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| Afganisztán                              | AF                       | AFG                      | PS-AF/en-US                         |
| Åland-szigetek                            | AX                       | ALA                      | SV-SE/en-US                         |
| Albánia                                  | AL                       | ALB                      | sq-AL/en-US                         |
| Algéria                                  | DZ                       | DZA                      | AR-DZ/en-US                         |
| Amerikai Szamoa                           | AS                       | ASM                      | en-US                                 |
| Andorra                                  | AD                       | ÉS                      | CA-ES/en-US                         |
| Angola                                   | AO                       | EZELŐTT                      | PT-PT/en-US                         |
| Anguilla                                 | Mesterséges intelligencia                       | AIA                      | en-US                                 |
| Antarktisz                               | AQ                       | ATA                      | en-US                                 |
| Antigua és Barbuda                      | AG                       | ATG                      | en-US                                 |
| Argentína                                | AR                       | ARG                      | es-AR/en-US                         |
| Örményország                                  | AM                       | ARM                      | -AM/en-US                         |
| Aruba                                    | AW                       | ABW                      | nl-NL/en-US                         |
| Ausztrália                                | AU                       | Au                      | EN-AU/en-US                         |
| Ausztria                                  | AT                       | AUT                      | de-AT/en-US                         |
| Azerbajdzsán                               | AZ                       | AZE                      | az-Latn-AZ/en-US                    |
| Bahama-szigetek                                  | BS                       | BHS                      | en-GB/en-US                         |
| Bahrein                                  | BH                       | BHR                      | AR-BH/en-US                         |
| Banglades                               | BD                       | BGD                      | BN – BD/en-US                         |
| Barbados                                 | BB                       | BRB                      | en-GB/en-US                         |
| Belarusz                                  | BY                       | BLR                      | be-BY/en-US                         |
| Belgium                                  | BE                       | BEL                      | fr-BE/nl-BE/en-US                 |
| Belize                                   | BZ                       | BLZ                      | EN-BZ/en-US                         |
| Benin                                    | BJ                       | BEN                      | fr-FR/en-US                         |
| Bermuda                                  | BM                       | BMU                      | en-GB/en-US                         |
| Bhután                                   | BT                       | BTN                      | en-US                                 |
| Bolívia                                  | BO                       | VERZIÓTÁROLÓHOZ                      | es-BO/en-US                         |
| Bonaire                                  | BQ                       | BES                      | nl-NL/en-US                         |
| Bosznia-Hercegovina                   | BA                       | BIH                      | BS-Latn-BA/en-US                    |
| Botswana                                 | BW                       | BWA                      | en-GB/en-US                         |
| Bouvet-sziget                            | BV                       | BVT                      | NB-nem/en-US                         |
| Brazília                                   | BR                       | MELLTARTÓ                      | PT-BR/en-US                         |
| Brit indiai-óceáni terület           | IO                       | IOT                      | en-US                                 |
| Brit Virgin-szigetek                   | VG                       | VGB                      | en-US                                 |
| Brunei                                   | BN                       | BRN                      | MS-BN/en-US                         |
| Bulgária                                 | BG                       | BGR                      | BG-BG/en-US                         |
| Burkina Faso                             | BF                       | BFA                      | fr-FR/en-US                         |
| Burundi                                  | BI                       | BDI                      | fr-FR/en-US                         |
| Cabo Verde                               | CV                       | CPV                      | PT-CV/en-US                         |
| Kambodzsa                                 | KH                       | KHM                      | km-KH/en-US                         |
| Kamerun                                 | CM                       | CMR                      | fr-FR/en-US                         |
| Kanada                                   | CA                       | LEHET                      | fr-CA/en-US                         |
| Kajmán-szigetek                           | KY                       | CYM                      | en-GB/en-US                         |
| Közép-afrikai Köztársaság                 | CF                       | CAF                      | fr-FR/en-US                         |
| Csád                                     | TD                       | TCD                      | fr-FR/en-US                         |
| Chile                                    | CL                       | CHL                      | es-CL/en-US                         |
| Kína                                    | CN                       | CHN                      | zh-CN/en-US                         |
| Karácsony-sziget                         | CX                       | CXR                      | en-US                                 |
| Cocos (Keeling)-szigetek                  | CC                       | CCK                      | en-US                                 |
| Kolumbia                                 | CO                       | OSZLOP                      | es-CO/en-US                         |
| Comore-szigetek                                  | KM                       | COM                      | fr-FR/en-US                         |
| Kongó                                    | CG                       | COG                      | fr-FR/en-US                         |
| Kongó (KDK)                              | CD                       | Cég tulajdonában lévő eszközök (COD)                      | fr-FR/en-US                         |
| Cook-szigetek                             | CK                       | COK                      | en-US                                 |
| Costa Rica                               | CR                       | CRI                      | es-CR/en-US                         |
| Côte d'Ivoire                            | CI                       | CIV                      | fr-FR/en-US                         |
| Horvátország                                  | HR                       | HRV                      | HR-HR/en-US                         |
| Curaçao                                  | CW                       | CUW                      | nl-NL/en-US                         |
| Ciprus                                   | CY                       | CYP                      | el-GR/en-US                         |
| Csehország                                  | CZ                       | CZE                      | CS-CZ/en-US                         |
| Dánia                                  | DK                       | DNK                      | da-DK/en-US                         |
| Dzsibuti                                 | DJ                       | DJI                      | fr-FR/en-US                         |
| Dominika                                 | DM                       | DMA                      | en-US                                 |
| Dominikai Köztársaság                       | DO                       | DOM                      | es-DO/en-US                         |
| Ecuador                                  | EC                       | ECU                      | es-EC/en-US                         |
| Egyiptom                                    | EG                       | EGY                      | AR-EG/en-US                         |
| Salvador                              | SV                       | SLV                      | es-SV/en-US                         |
| Egyenlítői-Guinea                        | GQ                       | NGM                      | es-ES/en-US                         |
| Eritrea                                  | ER                       | ERI                      | AR-SA/en-US                         |
| Észtország                                  | EE                       | IDŐ) 13:00                      | et-EE/en-US                         |
| eSwatini                                 | SZ                       | SWZ                      | en-US                                 |
| Etiópia                                 | ET                       | ETH                      | am-ET/en-US                         |
| Falkland-szigetek                         | FK                       | FLK                      | en-US                                 |
| Feröer szigetek                            | UTCÁN                       | ODA                      | fo-FO/en-US                         |
| Fidzsi                                     | FJ                       | FJI                      | en-GB/en-US                         |
| Finnország                                  | FI                       | FIN                      | Fi-FI/SV-FI/en-US                 |
| Franciaország                                   | JK                       | FRA                      | fr-FR/en-US                         |
| Francia Guyana                            | GF                       | GUF                      | fr-FR/en-US                         |
| Francia Polinézia                         | PF                       | PYF                      | fr-FR/en-US                         |
| Francia Déli Területek              | TF                       | ATF                      | fr-FR/en-US                         |
| Gabon                                    | FE                       | GAB                      | fr-FR/en-US                         |
| Gambia                                   | GM                       | GMB                      | en-US                                 |
| Grúzia                                  | GE                       | GEOREDUNDÁNS                      | ka-GE/en-US                         |
| Németország                                  | DE                       | DEU                      | de-DE/en-US                         |
| Ghána                                    | GH                       | GHA                      | en-GB/en-US                         |
| Gibraltár                                | GI                       | GIB                      | en-US                                 |
| Görögország                                   | GR                       | GRC                      | el-GR/en-US                         |
| Grönland                                | GL                       | GRL                      | da-DK/en-US                         |
| Grenada                                  | GD                       | GRD                      | en-US                                 |
| Guadeloupe                               | GP                       | GLP                      | fr-FR/en-US                         |
| Guam                                     | GU                       | GUMI                      | en-US                                 |
| Guatemala                                | GT                       | GTM                      | es-GT/en-US                         |
| Guernsey                                 | GG                       | GGY                      | en-US                                 |
| Guinea                                   | GN                       | GIN                      | fr-FR/en-US                         |
| Bissau-Guinea                            | GW                       | GNB                      | PT-PT/en-US                         |
| Guyana                                   | GY                       | SRÁC                      | en-US                                 |
| Haiti                                    | HT                       | HTI                      | fr-FR/en-US                         |
| Heard-sziget és McDonald-szigetek        | HM                       | HMD                      | en-US                                 |
| Honduras                                 | HN                       | HND                      | es – HN/en-US                         |
| Hongkong (KKT)                            | HK                       | HKG                      | ZH-HK/en-US                         |
| Magyarország                                  | HU                       | HUN                      | hu-HU/en-US                         |
| Izland                                  | IS                       | ADJA válaszként                      | a-IS/en-US                         |
| India                                    | IN                       | IND                      | EN-IN/Hi-IN/en-US                 |
| Indonézia                                | ID (Azonosító)                       | IDN                      | azonosító-azonosító/en-US                         |
| Irak                                     | IQ                       | IRQ                      | AR-IQ/en-US                         |
| Írország                                  | IE                       | IRL                      | EN-IE/en-US                         |
| Man-sziget                              | Csevegés                       | IMN                      | en-US                                 |
| Izrael                                   | IL                       | ISR                      | ő-IL/en-US                         |
| Olaszország                                    | IT                       | ITA                      | informatikai/en-US                         |
| Jamaica                                  | JM                       | JAM                      | EN-JM/en-US                         |
| Jan Mayen                                | XJ                       | XJA                      | NB-nem/en-US                         |
| Japán                                    | JP                       | JPN                      | ja-JP/en-US                         |
| Jersey                                   | JE                       | JEY                      | en-US                                 |
| Jordánia                                   | JO                       | JOR                      | AR-JO/en-US                         |
| Kazahsztán                               | KZ                       | KAZ                      | KK – KZ/en-US                         |
| Kenya                                    | KE                       | KEN                      | SW-KE/en-US                         |
| Kiribati                                 | KI                       | KIR                      | en-US                                 |
| Dél-Korea                                    | KR                       | KOR                      | ko-KR/en-US                         |
| Koszovó                                   | XK                       | XKS                      | en-US                                 |
| Kuvait                                   | KW                       | KWT                      | AR-KW/en-US                         |
| Kirgizisztán                               | KG                       | KGZ                      | KY-KG/en-US                         |
| Laosz                                     | LA                       | LAO                      | Lo-LA/en-US                         |
| Lettország                                   | LV                       | LVA                      | lv-LV/en-US                         |
| Libanon                                  | LB                       | LBN                      | AR-LB/en-US                         |
| Lesotho                                  | LS                       | LSO                      | en-US                                 |
| Libéria                                  | LR                       | LBR                      | en-US                                 |
| Líbia                                    | LY                       | LBY                      | AR-LY/en-US                         |
| Liechtenstein                            | LI                       | KÉPESSÉGEIN                      | de-LI/en-US                         |
| Litvánia                                | LT                       | LTU                      | lt-LT/en-US                         |
| Luxemburg                               | LU                       | LUX                      | de-LU/fr-LU/en-US                 |
| Makaó (KKT)                                | MO                       | MAC                      | zh-MO/en-US                         |
| Macedónia, V.J.K.                          | MK                       | MKD                      | MK-MK/en-US                         |
| Madagaszkár                               | MG                       | MFC                      | fr-FR/en-US                         |
| Malawi                                   | MW                       | MWI                      | en-US                                 |
| Malajzia                                 | MY                       | MYS                      | EN-MY/hu-US                         |
| Maldív-szigetek                                 | MV                       | MDV                      | DV-MV/en-US                         |
| Mali                                     | ML                       | MLI                      | fr-FR/en-US                         |
| Málta                                    | MT                       | MLT                      | MT – MT/hu – USA                         |
| Marshall-szigetek                         | MH                       | KTM                      | en-US                                 |
| Martinique                               | MQ                       | MTQ                      | fr-FR/en-US                         |
| Mauritánia                               | MR                       | MRT                      | AR-SA/en-US                         |
| Mauritius                                | MU                       | MUS                      | en-GB/en-US                         |
| Mayotte                                  | YT                       | 18:00                      | fr-FR/en-US                         |
| Mexikó                                   | MX                       | MEX                      | es-MX/en-US                         |
| Mikronézia                               | FM                       | MSZÁ                      | en-US                                 |
| Moldova                                  | MD                       | MDA                      | RO-RO/en-US                         |
| Monaco                                   | MC                       | MCO                      | fr-MC/en-US                         |
| Mongólia                                 | MN                       | MNG                      | MN-MN/en-US                         |
| Montenegró                               | ME                       | MNE                      | SR-Latn-ME/en-US                    |
| Montserrat                               | MS                       | MSR                      | en-US                                 |
| Marokkó                                  | MA                       | MÁRC                      | AR-MA/en-US                         |
| Mozambik                               | MZ                       | MOZ                      | PT-PT/en-US                         |
| Mianmar                                  | MM                       | MMR                      | en-US                                 |
| Namíbia                                  | NA                       | NAM                      | en-GB/en-US                         |
| Nauru                                    | NR                       | NRU                      | en-US                                 |
| Nepál                                    | NP                       | NPL                      | ne-NP/en-US                         |
| Holland Antillák                     | EGY                       | ANT                      | en-US                                 |
| Hollandia, a                         | NL                       | NLD                      | nl-NL/en-US                         |
| Új-Kaledónia                            | NC                       | NCL                      | fr-FR/en-US                         |
| Új-Zéland                              | NZ                       | NZL                      | EN-NZ/en-US                         |
| Nicaragua                                | NI                       | Hálózati adapter                      | es-NI/en-US                         |
| Niger                                    | NE                       | NER                      | fr-FR/en-US                         |
| Nigéria                                  | NG                       | NGA                      | Ha-Latn-NG/en-US                    |
| Niue                                     | NU                       | NIU                      | en-US                                 |
| Norfolk-sziget                           | NF                       | NFK                      | en-US                                 |
| Északi Mariana-szigetek                 | MP                       | MNP                      | en-US                                 |
| Norvégia                                   | NO                       | NOR                      | NB-nem/en-US                         |
| Omán                                     | OM                       | OMN                      | AR-OM/en-US                         |
| Pakisztán                                 | PK                       | PAK                      | az Ön-PK/en-US                         |
| Palau                                    | PW                       | PLW                      | en-US                                 |
| Palesztin Hatóság                    | PS                       | PSE                      | AR-SA/en-US                         |
| Panama                                   | PA                       | PAN                      | es-PA/en-US                         |
| Pápua Új-Guinea                         | PG                       | PNG                      | en-US                                 |
| Paraguay                                 | PY                       | KÍVÁNCSISKODIK                      | es-másol/en-US                         |
| Peru                                     | PE                       | PER                      | es-PE/en-US                         |
| Fülöp-szigetek                              | PH                       | PHL                      | EN-PH/en-US                         |
| Pitcairn-szigetek                         | PN                       | PCN                      | en-US                                 |
| Lengyelország                                   | PL                       | POL                      | pl-PL/EN-US                         |
| Portugália                                 | PT                       | PRT                      | PT-PT/en-US                         |
| Puerto Rico                              | PR                       | PRI                      | es – PR/en-US                         |
| Katar                                    | QA                       | QAT                      | AR-QA/en-US                         |
| Réunion                                  | RE                       | REU                      | fr-FR/en-US                         |
| Románia                                  | RO                       | ROU                      | RO-RO/en-US                         |
| Oroszország                                   | RU                       | RUS                      | ru-RU/en-US                         |
| Ruanda                                   | RW                       | RWA                      | RW-RW/en-US                         |
| Saba                                     | XS                       | XSA                      | nl-NL/en-US                         |
| Saint Kitts és Nevis                    | KN                       | KNA                      | en-GB/en-US                         |
| Saint Lucia                              | LC                       | LCA                      | en-US                                 |
| Saint Martin                             | MF                       | MAF                      | fr-FR/en-US                         |
| Saint-Pierre és Miquelon                | PM                       | SPM                      | fr-FR/en-US                         |
| Saint Vincent és Grenadine-szigetek         | VC                       | VCT                      | en-US                                 |
| Saint-Barthélemy                         | BL                       | BLM                      | fr-FR/en-US                         |
| Szamoa                                    | WS                       | WSM                      | en-US                                 |
| San Marino                               | SM                       | SMR                      | informatikai/en-US                         |
| São Tomé és Príncipe                    | ST                       | STP                      | PT-PT/en-US                         |
| Szaúd-Arábia                             | SA                       | SAU                      | AR-SA/en-US                         |
| Szenegál                                  | SN                       | SEN                      | Wo-SN/en-US                         |
| Szerbia                                   | RS                       | SRB                      | SR-Latn-RS/SR-Cyrl-RS/en-US       |
| Seychelle-szigetek                               | SC                       | SYC                      | en-US                                 |
| Sierra Leone                             | SL                       | SLE                      | en-US                                 |
| Szingapúr                                | SG                       | SNP                      | EN-SG/zh-SG/en-US                 |
| Sint Eustatius                           | XE                       | XSE                      | nl-NL/en-US                         |
| Sint Maarten                             | SX                       | SXM                      | en-US                                 |
| Szlovákia                                 | SK                       | SVK                      | sk-SK/en-US                         |
| Szlovénia                                 | SI                       | SVN                      | SL-SI/en-US                         |
| Salamon-szigetek                          | SB                       | SLB                      | en-US                                 |
| Szomália                                  | SO                       | Szom                      | AR-SA/en-US                         |
| Dél-afrikai Köztársaság                             | ZA                       | ZAF                      | EN-ZA/en-US                         |
| Dél-Georgia és Déli-Sandwich-szigetek | GS                       | SGS                      | en-US                                 |
| Dél-Szudán                              | SS                       | SSD                      | en-US                                 |
| Spanyolország                                    | ES                       | ESP                      | es-ES/CA-ES/EU-ES/GL-ES/en-US |
| Srí Lanka                                | LK                       | LKA                      | si-LK/en-US                         |
| Szent Ilona, Ascension, Tristan da Cunha   | SH                       | SHN                      | en-US                                 |
| Suriname                                 | SR                       | SUR                      | nl-NL                                 |
| Svalbard                                 | SJ                       | SJM                      | NB-nem/en-US                         |
| Svédország                                   | SE                       | SWE                      | SV-SE/en-US                         |
| Svájc                              | CH                       | HELYEZÉSE                      | de-CH/fr-CH/it-CH/en-US         |
| Tajvan                                   | TW                       | TWN                      | zh-TW/en-US                         |
| Tádzsikisztán                               | TJ                       | TJK                      | TG-Cyrl-TJ/en-US                    |
| Tanzánia                                 | TZ                       | TZA                      | en-GB/en-US                         |
| Thaiföld                                 | TH                       | THA                      | th-TH/en-US                         |
| Timor-Leste                              | TL                       | TLS                      | PT-PT/en-US                         |
| Togo                                     | TG                       | TGO                      | fr-FR/en-US                         |
| Tokelau                                  | TK                       | TKL                      | en-US                                 |
| Tonga                                    | TO                       | RENGETEG                      | en-US                                 |
| Trinidad és Tobago                      | TT                       | TEGY                      | EN-TT/en-US                         |
| Tunézia                                  | TN                       | TUN                      | AR-TN/en-US                         |
| Törökország                                   | TR                       | TUR                      | TR-TR/en-US                         |
| Türkmenisztán                             | TM                       | TKM                      | TK – TM/en-US                         |
| Turks- és Caicos-szigetek                 | TC                       | TCA                      | en-US                                 |
| Tuvalu                                   | TV                       | TUV                      | en-US                                 |
| Uganda                                   | UG                       | UGA                      | en-GB/en-US                         |
| Ukrajna                                  | UA                       | UKR                      | Egyesült Királyság – UA/en-US                         |
| Egyesült Arab Emírségek                     | AE                       | A                      | AR-AE/en-US                         |
| Egyesült Királyság                           | GB                       | GBR                      | en-GB/en-US                         |
| Amerikai Egyesült Államok lakatlan külbirtokai                    | UM                       | UMI                      | en-US                                 |
| Amerikai Virgin-szigetek                      | VI                       | VIR                      | en-US                                 |
| Egyesült Államok                            | USA                       | USA                      | en-US/es – USA                         |
| Uruguay                                  | UY                       | URY                      | es-UY/en-US                         |
| Üzbegisztán                               | UZ                       | UZB                      | Uz-Latn-UZ/en-US                    |
| Vanuatu                                  | JE                       | VUT                      | en-US                                 |
| Vatikán                             | VA                       | ÁFA                      | informatikai/en-US                         |
| Venezuela                                | VE                       | VEN                      | es-VE/en-US                         |
| Vietnam                                  | VN                       | VNM                      | VI – VN/en-US                         |
| Wallis és Futuna                        | WF                       | WLF                      | fr-FR/en-US                         |
| Jemen                                    | TI                       | BÜKINÉ ARADVÁRI Hajnalka                      | AR-ti/en-US                         |
| Zambia                                   | ZM                       | ZMB                      | en-GB/en-US                         |
| Zimbabwe                                 | ZW                       | ZWE                      | EN-ZW/en-US                         |

