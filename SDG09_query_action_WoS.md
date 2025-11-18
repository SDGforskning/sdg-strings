# Search query for SDG 9 - Industry, innovation and infrastructure, Bergen action-approach.

Build resilient infrastructure, promote inclusive and sustainable industrialization and foster innovation 

**Status: This query is currently under development (2025)**

**Contents**

1. Full query
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes


## 1. Full query

## 2. General notes

This document contains search strings for finding publications related to the actions in the SDG 9 targets and indicators ("action approach"; focus on precision, smaller result set). We also have a version which finds publications related to the topics in the SDG 9 targets and indicators ("topic approach"; focus on recall, larger result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Department of Economic and Social Affairs website <a href="#f1">(UN DESA, 2025)</a>.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) <a href="#f2">(United Nations, 2016, 2017, 2018, 2019, 2020, 2021)</a>. Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).


## 3. Targets

### Target 9.1

> **9.1 Develop quality, reliable, sustainable and resilient infrastructure, including regional and transborder infrastructure, to support economic development and human well-being, with a focus on affordable and equitable access for all**
>
> 9.1.1 Proportion of the rural population who live within 2 km of an all-season road
>
> 9.1.2 Passenger and freight volumes, by mode of transport

This target is interpreted to cover research about developing reliable, sustainable and resilient infrastructure that is accessible for all. 

We think that infrastructure is understood in this target as a broad and integrated system, consisting of both physical and institutional components. It includes so-called hard infrastructure, such as energy, transport, water, waste management and digital communication systems, as well as soft infrastructure, including human resources, institutional structures and policy frameworks (Soriano, A., Gaikwad. S., Stratton-Short. S., Bajpai, A, & Imbuye. J. 2022, 10; United Nations Environment Programme 2021, 8).

Sustainable infrastructure refers to systems that are planned, designed, built, operated, and eventually decommissioned in ways that ensure economic, financial, social, environmental (including climate resilience), and institutional sustainability throughout their entire life cycle. This widely used definition is adapted from the Inter-American Development Bank. (United Nations Environment Programme (2021) 2021, 8).

This query consists of 1 phrase. 
The basic structure of phrase 1 is action + sustainable + infrastructure + accessible

```py
TS=
(

)

```


### Target 9.2

> **9.2 Promote inclusive and sustainable industrialization and, by 2030, significantly raise industry’s share of employment and gross domestic product, in line with national circumstances, and double its share in least developed countries**
>
> 9.2.1 Manufacturing value added as a proportion of GDP and per capita
>
> 9.2.2 Manufacturing employment as a proportion of total employment

This target is interpreted to cover research about 

* Promoting inclusive and sustainable industrialization.
* Increasing share of industry in both gross domestic product (GDP) and employment. 

The term industry is inherently ambiguous. In general usage, it refers to a specific sector of economic activity, such as agriculture, manufacturing or services. In economics, however, the term is understood more narrowly, typically referring to manufacturing activities. Also, the indicators for this target focus on the manufacturing sector (UN DESA 2025). 
We understand the concept of industry broader, as the target itself uses both the terms industrialization and industry, which we interpreted as referring to larger phenomenon, industrial development, even though manufacturing often has the key role in it. This broader viewpoint is seen in many documents by United Nations organizations, such as the Lima Declaration: Towards Inclusive and Sustainable Industrial Development (United Nations Industrial Development Organization 2013).

We use definition provided by the United Nations Industrial Development Organization (UNIDO) (2024). This definition is based on sections of the Inter-national Standard Industrial Classiﬁcation of All Economic Activities (ISIC) (2008). According to the definition, the sections Mining and quarrying, Manufacturing, Electricity, gas, steam and air-conditioning supply and Water supply; sewerage, waste management and remediation activities together form the concept of industry. 

We also interpret that the underlying idea behind the target is inclusive and sustainable industrial development (ISID). ISID is concept developed by UNIDO and is defined to mean “Long-term industrialization that drives development along three aspects: creating shared prosperity by offering equal opportunities and equitable distribution of benefits to all; advancing economic competitiveness; and safeguarding the environment by decoupling the prosperity generated by industrial activities from excessive natural resource use and negative environmental impacts” (United Nations Industrial Development Organization 2021, xvii).


This query consists of X phrases.
```py
TS=
(

)
```

### Target 9.3

> **9.3 Increase the access of small-scale industrial and other enterprises, in particular in developing countries, to financial services, including affordable credit, and their integration into value chains and markets**
>
> 9.3.1 Proportion of small-scale industries in total industry value added
>
> 9.3.2 Proportion of small-scale industries with a loan or line of credit

This target is interpreted to cover research about 

* Improving access to financial services for all types of small-scale industrial and other enterprises, with financial services referring to, for example, affordable credit.
* Integrating small-scale industrial and other enterprises into value chains (production and distribution chains) and into local and international markets.


This query consists of X phrases.
```py
TS=
(

)
```

### Target 9.4

> **9.4 By 2030, upgrade infrastructure and retrofit industries to make them sustainable, with increased resource-use efficiency and greater adoption of clean and environmentally sound technologies and industrial processes, with all countries taking action in accordance with their respective capabilities**
>
> 9.4.1 CO2 emission per unit of value added

This target is interpreted to cover research about 

* Modernizing or upgrading infrastructure and industry to ensure sustainability, with attention to efficient resource use and improved utilization of raw materials and water.
* Adoption of environmentally friendly and low-pollution technologies, such as renewable energy, recycling, and low-emission production.


This query consists of X phrases.
```py
TS=
(

)
```

### Target 9.5

> **9.5 Enhance scientific research, upgrade the technological capabilities of industrial sectors in all countries, in particular developing countries, including, by 2030, encouraging innovation and substantially increasing the number of research and development workers per 1 million people and public and private research and development spending**
>
> 9.5.1 Research and development expenditure as a proportion of GDP
>
> 9.5.2 Researchers (in full-time equivalent) per million inhabitants

This target is interpreted to cover research about 

* Increasing technological capabilities and research within or to do with industry 
* Increasing innovation, and increasing R&D capacity, including workforce and funding 

SDG Target 9.5 focuses on strengthening the foundation for innovation and scientific advancement. E-Handbook on Sustainable Development Goals Indicators (2024): 9.5.1 and 9.5.2. In spite of the research workforce continuing to rise at the global level, firm policy commitments towards substantial increase in the number of research personnel, particularly in developing economies, as well as strengthening the participation of women in research profession are essential for the effective delivery of innovative solutions for the challenges ahead. The Sustainable Development Goals. Extended Report 2024. (2024) 

This query consists of 1 phrase.

```py
TS=
(
     ("upgrad*" OR "improv*" OR "better" OR "enhanc*" OR "promot*" OR "encourag*" OR "improv*" OR "legislat*" OR "governance" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "program*" 
     ) 
     NEAR/5
      ( ("research" OR "innovation*" OR "R&D" OR "R & D" OR "research and development" OR "research & development" OR "technology" OR "technological capabilities" 
        ) 
      NEAR/5 
      ("industr*" OR "capacity" OR "capabilit*" OR "sector*" OR "institutions" OR "national" OR "regional" OR "worker*" OR "workforce" OR "researcher$" OR "invest*" OR "financ*" OR "fund*" OR "spending*" OR "expend*" OR "expense*" OR "GDP" OR "subsidy" OR "subsidi*" 
      )
    ) 
) 
```

### Target 9.a

> **9.a Facilitate sustainable and resilient infrastructure development in developing countries through enhanced financial, technological and technical support to African countries, least developed countries, landlocked developing countries and small island developing States**
>
> 9.a.1 Total official international support (official development assistance plus other official flows) to infrastructure

This target is interpreted to cover research about: 

* Facilitatating sustainable and resilient infrastructure development in developing countries (African countries, least developed countries, landlocked developing countries and small island developing States) through financial support, technological support, technical support and official development assistance (ODA).   

This query consists of 1 phrase.

```py
TS=
( 
    ( ("facilitat*" OR "promot*" OR "assist"
    )  
    AND 
        ( ("reliabl*" OR "sustainab*" OR "resilien*" OR "invulnerab*" OR "adaptab*" OR "flexib*" OR "recoverab*" OR "maintainable*" OR "renewabl*" OR "resource-efficien*" OR "repairab*" OR "recyclab*" OR "reusab*" OR "ecofriendly" OR "eco-friendly" OR "environmentally friendly" OR "environmentally sound" OR "ecologically friendly" OR "ecologically sound" OR "low* carbon" OR "green" OR "eco" OR "ecological" OR "nonpolluting" OR "energy-efficient"
        )  
        NEAR/5 
        ( ("infrastruct*" OR "agricultural infrastructure" OR "built infrastructure" OR (("culture" OR "recreation" OR "art*") NEAR/1 "infrastructure") OR "digital infrastructure" OR "energy infrastructure" OR "food infrastructure" OR "green infrastructure" OR "natural infrastructure" OR "social infrastructure" OR "transportation infrastructure" OR "urban infrastructure" OR "water infrastructure" OR (("energy" OR "power") NEAR/1 ("infrastruct*" OR "supply" OR "solution*" OR "source*")) OR "energy system*" OR "power system*" OR "electrification" OR "electric* transmission" OR "electric* distribution" OR "electric* connections" OR "electric* production" OR "lighting" OR (("waste" OR "wastewater*" OR "sewage") NEAR/1 ("treatment" OR "collection" OR "management")) OR "recycling system*" OR "water supply" OR "drinking water" OR "clean water" OR "sanitation" OR "drainage system*" OR "water and sanitation system*" OR "food supply" OR "telecommunication*" OR "digital communications" OR "communication*" OR "digital solutions" OR "internet" OR "mobile network*" OR "sports" OR "public amenities" OR "rule of law" OR "juridical system*" OR "legal services" OR "financial service*" OR "banking service*" OR "education" OR "school*" OR "health care" OR "healthcare" OR "buildings" OR "housing" OR "public spaces" OR "disaster management" OR "mass transit*" OR "mobility system*" OR "public transport*" OR "public transit*" OR "transport" OR "transportation" OR "urban mobility" ) ) 
        ) 
    AND ( "financial support" OR "technological support" OR "technical support" OR "official development assistance" OR "ODA" OR "develop* assist*" OR "develop* aid*" OR "foreign aid*" OR "international aid*" OR "cooperation* fund*" OR "develop* spending*" OR "foreign investment" OR "foreign invest*" OR "international invest*" OR "international investment" OR "develop* invest*" OR "develop* investment" OR "foreign financ*" OR "international financ*" OR "develop* fund*" OR "foreign support*" OR "international support*" OR "foreign assist*" OR "international assist*" OR "foreign subsid*" OR "international subsid*" OR "develop* support*" OR "develop* subsid*" OR "humanitar* assist*" OR "humanitar* aid*" OR "humanitar* fund*" OR "humanitar* invest*" OR "cross-national assist*" OR "cross-national aid*" OR "cross-national fund*" OR "cross-national invest*" OR invest* OR fund* OR financ* OR "technolog* transfer*" OR "transfer of technical knowledge" OR "transfer of technolog*" 
    ) 
    AND ( "african*" OR "magrheb" OR "maghrib" OR "west indies" OR "indian ocean islands" OR "caribbean" OR "central america" OR "latin america" OR "south america" OR "central asia" OR "north asia" OR "northern asia" OR "western asia" OR "eastern europe" OR "least developed countr*" OR "least developed nation*" OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican*" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People's democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan*" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*" OR "landlocked developing nation*" OR "landlocked developing stat*" OR "land-locked developing nation*" OR "land-locked developing stat*" OR "Armenia*" OR "Azerbaijan*" OR "Bolivia*" OR "Botswana*" OR "Eswatini" OR "Kazakhstan*" OR "Kyrgyz*" OR "Mongolia*" OR "North Macedonia" OR "Paraguay" OR "Moldova*" OR "Tajikistan" OR "Turkmenistan" OR "Uzbekistan" OR "Zimbabwe*" OR "small island developing nation*" OR "small-island developing state*" OR "Antigua and Barbuda" OR "Bahamas" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Cuba" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "Grenada*" OR "Guyana*" OR "Jamaica*" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "Saint Lucia*" OR "Vincent and the Grenadines" OR "Samoa*" OR "Seychelles" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "Tonga*" OR "Trinidad and Tobago" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "Virgin Islands" 
        )    
    ) 
) 
```

### Target 9.b

> **9.b Support domestic technology development, research and innovation in developing countries, including by ensuring a conducive policy environment for, inter alia, industrial diversification and value addition to commodities**
>
> 9.b.1 Proportion of medium and high-tech industry value added in total value added

The goal is to help developing nations build their own technological and industrial capacity, diversify their economies, and add more value to raw materials rather than relying solely on exports of unprocessed goods. 

This target is interpreted to cover research about:   

* Supporting technology development, research and innovation in developing countries.   

This query consists of one phrase. 

```py
TS=
(
    (increas* OR strengthen* OR improv* OR restor* OR enhanc* OR upgrad* OR "scale* up" OR build* OR "capacity building" OR "capacity development" OR expand* OR accelerat* OR advance* OR develop* OR encourag* OR facilitat* OR promot* OR implement* OR adopt* OR establish* OR design* OR plan* OR pathway* OR roadmap OR "way to" OR attain* OR achiev*
    )   
NEAR/15
 ("technology development" OR "research and development" OR "R&D" OR "research & development" OR "research and innovation" OR innovation OR "domestic technology" OR "policy environment" OR "industrial diversification" OR "value addition"
 )  
    AND 
    ("least developed countr*" OR "least developed nation$" OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world" OR "less developed countr*" OR "less developed nation$" OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$" OR "underserved countr*" OR "underserved nation$" OR "deprived countr*" OR "deprived nation$" OR "middle income countr*" OR "middle income nation$" OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$" OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$" OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$" OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*" OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands" OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*" OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish" OR "turkey" OR "georgia*"
    )
) 
```

### Target 9.c

> **9.c Significantly increase access to information and communications technology and strive to provide universal and affordable access to the Internet in least developed countries by 2020**
>
> 9.c.1 Proportion of population covered by a mobile network, by technology
> 
This target is interpreted to cover research about: 

* Increasing access to information and communication technology in least development countries
* Providing universal and affordable access to Internet in least development countries 

In most developing countries, mobile broadband (3G or above) is the main way – and often the only way – to connect to the Internet. Around 95 per cent of the global population now has this form of access. Bridging the “coverage gap” for the remaining 5 per cent poses significant challenges. Mobile broadband remains inaccessible to 18 per cent of people in the LDCs and LLDCs. https://unstats.un.org/sdgs/report/2024/. Target 9.c aims to significantly increase access to information and communications technology and strive to provide universal and affordable access to the Internet in least developed countries by 2020. (United Nations. (2023). 2023 HLPF thematic review of SDG 9). 

This phrase is about developing sustainable infrastructure that is affordable for all. Basic structure is action + sustainable/reliable + internet connection/mobile network 
This query consists of one phrase. 

```py

TS=
(
    ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "more efficient*" OR "more effectiv*" OR "higher" OR "upgrad*" OR "scal* up" OR "build*" OR "build* capacity" OR "capacity building" OR "capacity development" OR "expand" OR "expansion*" OR "accelerat*" OR "advance" OR "advancing" OR "develop" OR "developing" OR "encourag*" OR "facilitat*" OR "promot*" OR "overcome" OR "ensure" OR "attain*" OR "achiev*")   

NEAR/15 ("Internet" OR "internet connection" OR "mobile network" OR "mobile broadband" OR "access to information" OR "access to internet" OR "communication technology" OR "ICT" OR "information and communication technology" OR "digital infrastructure" OR "telecommunication" OR "telecom network" OR "broadband" OR "wireless network" OR "connectivity" OR "affordable internet" OR "low-cost internet" OR "cheap internet" OR "internet affordability" OR "digital divide" OR "universal access" OR "inclusive access" OR "internet penetration" OR "connectivity gap" OR "2G" OR "3G" OR "4G" OR "LTE" OR "third generation" OR "second generation" OR "low bandwidth" OR "slow internet" OR "limited connectivity" OR "basic mobile network" OR "poor connectivity" OR "low-speed internet")  
AND ("least developed countr*" OR "least developed nation$" OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"))  

```

## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

E-Handbook on Sustainable Development Goals Indicators. (2024). https://unstats.un.org/sdgs/report/2024/extended-report/Extended-Report_Goal-9.pdf [Accessed 2025.06.24]

Inter-American Development Bank. (2018). *What is Sustainable Infrastructure? A Framework to Guide Sustainability Across the Project Cycle*. Washington, DC, USA: IDB; 2018. Available from: https://publications.iadb.org/publications/english/document/What_is_Sustainable_Infrastructure__A_Framework_to_Guide_Sustainability_Across_the_Project_Cycle.pdf [Accessed 2025.07.08]

Soriano, A, Gaikwad S, Stratton-Short S, Bajpai A, Imbuye J. (2022). *Inclusive infrastructure for climate action*. UNOPS, Copenhagen, Denmark. Available https://wrd.unwomen.org/sites/default/files/2023-03/Inclusive_Infrastructure_Climate_Action.pdf [Accessed 2025.07.07]

The Sustainable Development Goals. Extended Report 2024. (2024). https://unstats.un.org/sdgs/report/2024/extended-report/Extended-Report_Goal-9.pdf [Accessed 2025.06.24]

<span id="f1">UN DESA. (2025).</span> *Goals: Build resilient infrastructure, promote inclusive and sustainable industrialization and foster innovation *. https://sdgs.un.org/goals/goal9#targets_and_indicators [Accessed 2025.04.02]

<span id="f2">United Nations. (2016, 2017, 2018, 2019, 2020, 2021).</span> *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/

United Nations. (2024). The Sustainable Development Goals Report 2024. https://unstats.un.org/sdgs/report/2024/The-Sustainable-Development-Goals-Report-2024.pdf [Accessed 2025.06.25]

United Nations Environment Programme (2021). (2021). *International Good Practice Principles for Sustainable Infrastructure*. Nairobi Available https://wedocs.unep.org/bitstream/handle/20.500.11822/34853/GPSI.pdf [Accessed 2025.07.08]

United Nations Industrial Development Organization. (2013). *Lima Declaration: Towards Inclusive and Sustainable Industrial Development*. General Conference Resolution GC.15/Res.1. Lima, Peru: UNIDO, 2013. Available: https://www.unido.org [Accessed 9.7.2025]

United Nations Industrial Development Organization. (2021). *Industrial Development Report 2022*. The Future of Industrialization in a Post-Pandemic World. Vienna. https://digitallibrary.un.org/record/3994233?v=pdf [Accessed 9.7.2025]

United Nations Industrial Development Organization. (2024). *International Yearbook of Industrial Statistics, edition 2024*. UNIDO statistics. https://stat.unido.org/portal/storage/file/publications/yb/2024/UNIDO_IndustrialStatistics_Yearbook_2024.pdf [Accessed 9.7.2025]
