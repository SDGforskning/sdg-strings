# Search query for SDG 10 - Reduced inequalities, Bergen action-approach.

Reduce inequality within and among countries

**Status: This query is currently under development (2025)**

**Contents**

1. Full query
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes


## 1. Full query

## 2. General notes

This document contains search strings for finding publications related to the actions in the SDG 10 targets and indicators ("action approach"; focus on precision, smaller result set). We also have a version which finds publications related to the topics in the SDG 10 targets and indicators ("topic approach"; focus on recall, larger result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Department of Economic and Social Affairs website <a href="#f1">(UN DESA, 2025)</a>.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) <a href="#f2">(United Nations, 2016, 2017, 2018, 2019, 2020, 2021)</a>. Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

Acronyms used:

    UN DESA: UN Department of Economic and Social Affairs
    IHRL: International Human Rights Law
    ODA: Official Development Assistance
    SDT: Special and Differential Treatment

## 3. Targets

### Target 10.1

> **10.1 By 2030, progressively achieve and sustain income growth of the bottom 40 per cent of the population at a rate higher than the national average**
>
> 10.1.1 Growth rates of household expenditure or income per capita among the bottom 40 per cent of the population and the total population

This target is interpreted as to cover research about how to raise and sustain the income growth rate of the poorest population.

Setting the limit to the bottom 40 % is a "practical compromise" that insures the target including the poorest populations in differing circumstances of different countries. The income growth rate is computed as average annual growth rate of either per capita consumption or actual income over about a 5-year period. (UN Statistics Divison 2024a.)  

This query consists of 1 phrase. The basic structure is *action + income growth + poor*

```py
TS=
(
 (("rais*" OR "foster*" OR "increas*" OR "promot*" OR "boost*" OR "enhanc*" OR "improv*" OR "better" OR "attain*" OR
  "achiev*" OR "provid*" OR "ensur*" OR "guarantee*" OR "maintain*" OR "secur*" OR "strengthen*" OR "develop*" OR
  "establish*" OR "sustain*" OR "standardi*" OR "regulari*" OR "consolidat*" OR "stabili*" OR "normali*" OR "uphold*"
  OR "stable" OR "fixed" OR "perpetual*" OR "lasting" OR "enduring")
NEAR
  ("income growth" OR "income growth rate" OR "per capita consumption" OR "per capita income" OR "welfare aggregate"
  OR "shared prosperity" OR "welfare distribution" OR "inclusive growth")
 )
AND
(("bottom 40%" OR "bottom 40 percent" OR "bottom 40 per cent" OR "the poor" OR "poverty" OR "the poorest" OR
 "rural poor" OR "urban poor" OR "working poor" OR "destitute$" OR "low income" OR "low-income" OR "disadvantaged"
 OR "unemployed")
NEAR
  ("household$" OR "people" OR "family" OR "families")
 )
)
```

### Target 10.2

> **10.2 By 2030, empower and promote the social, economic and political inclusion of all, irrespective of age, sex, disability, race, ethnicity, origin, religion or economic or other status**
>
> 10.2.1 Proportion of people living below 50 per cent of median income, by sex, age and persons with disabilities

This target is interpreted to cover research about enabling and promoting everyone to participate in social, economic and political activities. Special attention is paid to people in a disadvantaged position due to any characteristic, e.g. age, gender or disability (horizontal inequalities).

This target handles empowering people who face horizontal inequalities. This refers to groups of people who share an identity characteristic like race or religion and can therefore be exposed to the same kind of inequalities. (Stewart 2016). Ensuring that people in disadvantaged positions are part of decision-making processes (especially decisions regarding themselves) is a method recommended to accelerate progress in this target as well as the whole of SDG10 (United Nations 2024). A big part of structural discrimination and horizontal inequalities are linked to poorness, which is why living below 50 % of median income is considered a solid indicator for this target (Sharif 2024; World Bank Group 2025). For example, persons with disabilities and people of African descent experience significantly higher levels of poverty (United Nations 2018; World Bank Group 2025). 

Social inclusion means improving opportunities for individuals and groups to take part in society. This can include for example eradicating discriminatory attitudes from legal systems, labour markets and health care. (World Bank Group 2025.) Economic inclusion aims to empower individuals and communities by for example boosting their income and training them in economic skills (Sharif 2024). Political inclusion then covers opportunities for partaking in political activities, e.g. voting and participating in elections (Aldar ym. 2025).


```py
TS=
((("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "upgrad*" OR "scal* up" OR "build*" OR "expan*" OR "accelerat*" OR "advanc*" OR "develop*" OR "empower*" OR "promot*" OR "ensure" OR "attain*" OR "achiev*")
NEAR
("social* inclusi*" OR "economic* inclusi*" OR "political* inclusi*" OR "societal activit*"))
OR
(("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR "declin*" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "avoid*" OR "prevent*" OR "combat*" OR "cure" OR "halt*" OR "resist*" OR "overcome")
NEAR
("horizontal inequalit*" OR "social* exclusi*" OR "economic* exclusi*" OR "political* exclusi*"))
)
```

### Target 10.3

> **10.3 Ensure equal opportunity and reduce inequalities of outcome, including by eliminating discriminatory laws, policies and practices and promoting appropriate legislation, policies and action in this regard**
>
> 10.3.1 Proportion of population reporting having personally felt discriminated against or harassed within the previous 12 months on the basis of a ground of discrimination prohibited under international human rights law

This target is interpreted to cover research about eliminating discriminatory legislation, policies and other practices and promote ones that ensure equal opportunity and reduce inequalities of outcome.

"Discrimination is any distinction, exclusion, restriction or preference or other differential treatment that is directly or indirectly based on prohibited grounds of discrimination, and which has the intention or effect of nullifying or impairing the recognition, enjoyment or exercise, on an equal footing, of human rights and fundamental freedoms in the political, economic, social, cultural or any other field of public life." The prohibited grounds of discrimination are listed in IHRL (UN Statistics Division 2024b.)

```py
TS=
("stop*"
"end"
"ends"
"ended"
"ending"
"remov*"
"eliminat*"
"eradicat*"
"avoid*"
"prevent*"
"combat*"
"cure"
"halt*"
"resist*"
"prohibit*"

"discriminator*"
"inequalit*"
"harass*"

"law$"
"policy" OR "policies"
"regulat*"
"legal*"
"legislat*"
"agreement$"
"treaty" OR "treaties"
"strateg*"
"framework$"
"instrument$"
"governance"
"practice*"
"action*"

"appropriat*"
"equal*"
"equal opportunit*"
"anti discriminat*"
"anti-discriminat*"

"increas*"
"strengthen*"
"improv*"
"restor*"
"enhanc*"
"better"
"more efficient"
"higher"
"upgrad*"
"scal* up"
"build*" ("build* capacity" / "capacity building" / "capacity development")
"expand" OR "expansion*"
"accelerat*"
"advance" OR "advancing"
"develop" OR "developing"
"promot*"

)
```

### Target 10.4

> **10.4 Adopt policies, especially fiscal, wage and social protection policies, and progressively achieve greater equality**
>
> 10.4.1 Labour share of GDP
>
> 10.4.2 Redistributive impact of fiscal policy

This target is interpreted to cover research about promoting the implementation of existing or new social and economic policy practices to reduce inequalities/achieve greater equality.

```py
TS=
("establish*"
"propose*"
"design*"
"implement*"
"plan"
"plans"
"planned"
"planning"
"adopt*"
"introduc*"
"build*" ("build* capacity" / "capacity building" / "capacity development")
"architect"
"develop" OR "development"

"increas*"
"strengthen*"
"improv*"
"restor*"
"enhanc*"
"better"
"more efficient"
"higher"
"upgrad*"
"scal* up"
"build*" ("build* capacity" / "capacity building" / "capacity development")
"expand" OR "expansion*"
"accelerat*"
"advance" OR "advancing"
"develop" OR "developing"
"promot*"

"law$"
"policy" OR "policies"
"regulat*"
"legal*"
"legislat*"
"agreement$"
"treaty" OR "treaties"
"strateg*"
"framework$"
"instrument$"
"governance"
"practice*"
"action*"

"fiscal*"
"wage*"
"social protect*"
"economic*"

"decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR "declin*" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "avoid*" OR "prevent*" OR "combat*" OR "cure" OR "halt*" OR "resist*" OR "overcome"

"discriminator*"
"inequalit*"
"harass*"

"rais*" or "foster*" or "increas*" or "promot*" or "boost*" or "enhanc* or "improv*" or "better" or "attain*" or "achiev*" or "provid*" or "ensur*" or "guarantee*" or "maintain*" or "secur*" or "strengthen*" or "develop*" or "establish*" or "sustain*" or "consolidat*"

"appropriat*"
"equal*"
"equal opportunit*"
"anti discriminat*"
"anti-discriminat*"
)
```

### Target 10.5

> **10.5 Improve the regulation and monitoring of global financial markets and institutions and strengthen the implementation of such regulations**
>
> 10.5.1 Financial Soundness Indicators

This target is interpreted to cover research about improving the regulation and monitoring of global financial markets and institutions.

This query consists of X phrases.

```py
TS=
("increas*"
"strengthen*"
"improv*"
"restor*"
"enhanc*"
"better"
"more efficient"
"more effectiv*"
"higher"
"upgrad*"
"scal* up"
"expand" OR "expansion*"
"accelerat*"
"advance" OR "advancing"
"develop" OR "developing"
"promot*"

"manag*"
"control*"
"regulat*"
"legislat*"
"govern*"
"monitor*"
"surveillanc*"
"securing"

(("global*" OR "international*") NEAR ("economic*" OR "financial*" or "monetar*" OR "money") NEAR "("institution*" OR "market*"))
)
```

### Target 10.6

> **10.6 Ensure enhanced representation and voice for developing countries in decision-making in global international economic and financial institutions in order to deliver more effective, credible, accountable and legitimate institutions**
>
> 10.6.1 Proportion of members and voting rights of developing countries in international organizations

This target is interpreted to cover research about enhancing the representation and decision-making powers of developing countries in international economic institutions.

In order to achieve truely effective and permanent changes on a global level, it is crucial to involve developing countries in the decision-making processes that concern their own economical development as well (UN DESA 2019; UN 2024).

```py
TS=
("rais*" or "foster*" or "increas*" or "promot*" or "boost*" or "enhanc* or "improv*" or "better" or "attain*" or "achiev*" or "provid*" or "ensur*" or "guarantee*" or "maintain*" or "secur*" or "strengthen*" or "develop*" or "establish*" or "sustain*" or "standardi*" or "regulari*" or "consolidat*" 


"increas*"
"strengthen*"
"improv*"
"enhanc*"
"better"
"more effectiv*"
"higher"
"upgrad*"
"scal* up"
"expand*" OR "expansion*"
"accelerat*"
"advance*" OR "advancing"

"representat*"
"voice*"
"vote*"
"decision-making" OR "decision making"
"decision-making power*" OR "decision making power*"

"least developed countr*" OR "least developed nation$"
      OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
      OR "less developed countr*" OR "less developed nation$"
      OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
      OR "underserved countr*" OR "underserved nation$"
      OR "deprived countr*" OR "deprived nation$"
      OR "middle income countr*" OR "middle income nation$"
      OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
      OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
      OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
      OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
      OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
      OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"
      OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish" OR "turkey" OR "georgia*"
      )
)



(("global*" OR "international*") NEAR ("economic*" OR "financial*" or "monetar*" OR "money") NEAR "("institution*" OR "market*"))

)
```

### Target 10.7

> **10.7 Facilitate orderly, safe, regular and responsible migration and mobility of people, including through the implementation of planned and well-managed migration policies**
>
> 10.7.1 Recruitment cost borne by employee as a proportion of monthly income earned in country of destination
>
> 10.7.2 Number of countries with migration policies that facilitate orderly, safe, regular and responsible migration and mobility of people
>
> 10.7.3 Number of people who died or disappeared in the process of migration towards an international destination
>
> 10.7.4 Proportion of the population who are refugees, by country of origin

This target is interpreted to cover research about ensuring safe, responsible and regular migration and mobility of people.

```py
TS=
("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "upgrad*" OR "scal* up" OR "build*" OR "accelerat*" OR "advanc*" OR "develop*" OR "promot*" OR "ensure" OR "attain*" OR "achiev*" or "implement*" or "facilitat*")

("secure" or "security" or "protect*" or "reliab*" or "stability" or "stable" or "safe" or "regular" or "responsible" or "orderly" or "planned" or "well-managed" or "well managed" or "well-planned" or "well planned" or "managed")


("decreas*" OR "minimi*" OR "reduc*" OR "mitigat*" OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR "declin*" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "avoid*" OR "prevent*" OR "halt*" OR "resist*" OR "overcome")

("risk$" or "hazard*" or "insecure" or "insecurity" or "unprotect*" or "unrelaib*" or "vulnerab*" or "dead*" or "die$" or "disappear*" or "unstability" or "unstable")


("migrat*" or "mobilit*" or "move" or "moving" or "movement" or "travel*" or "international*" or "internal*" or "intra stat*")

("people" or "immigrant*" or "emigrant*" or "alien$" or "resident alien$" or "migrant*" "settler$" or "illegal" or "undocumented" or "refugee*")

)
```


### Target 10.a

> **10.a Implement the principle of special and differential treatment for developing countries, in particular least developed countries, in accordance with World Trade Organization agreements**
>
> 10.a.1 Proportion of tariff lines applied to imports from least developed countries and developing countries with zero-tariff

This target is interpreted to cover research about implementing the principle of special and differential treatment (SDT) for developing countries, in accordance with the World Trade Organisation agreements.

```py
TS=
("implement*" or "establish*" or "plan" or "plans" or "planned" or "planning" or "adopt*" or "introduc*" or "develop" OR "development" or "ensure" or "attain*" or "achiev*" or "increas*" OR "strengthen*" OR "improv*" OR "enhanc*" or accelerat*" OR "advanc*" or "promot*" or "facilitat*")

("special and differential treatment*" or "SDT" or "zero-tariff*" or "zero tariff*" or "tariff lines") AND ("World Trade Organization" or "WTO" or "trade facilitation agreement*" or "trade agreement*")

"least developed countr*" OR "least developed nation$"
      OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
      OR "less developed countr*" OR "less developed nation$"
      OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
      OR "underserved countr*" OR "underserved nation$"
      OR "deprived countr*" OR "deprived nation$"
      OR "middle income countr*" OR "middle income nation$"
      OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
      OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
      OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
      OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
      OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
      OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"
      OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish" OR "turkey" OR "georgia*"

)
```

### Target 10.b

> **10.b Encourage official development assistance and financial flows, including foreign direct investment, to States where the need is greatest, in particular least developed countries, African countries, small island developing States and landlocked developing countries, in accordance with their national plans and programmes**
>
> 10.b.1 Total resource flows for development, by recipient and donor countries and type of flow (e.g. official development assistance, foreign direct investment and other flows)

This target is interpreted to cover research about 
* ensuring official development assistance (ODA) and financial flows are targeted to where the need is greatest
* dividing the resources in accordance with the national, regional and local plans of the recipient countries.

We have two bullet-points here to put emphasis on targeting assets where they are needed most, as well as localization as per portrayed in Inter-Agency Policy Brief: Accelerating SDG Localization to deliver on the promise of the 2030 Agenda for Sustainable Development (UN 2024).

This query consists of 2 phrases.

Phrase 1
```py
TS=
("encourag*" OR "increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "more efficient" OR "Scal up" OR "accelerat*" OR "advance" OR "advancing" OR "ensure" OR "attain*" OR "achiev*" OR "facilitat*")

("ODA" OR "official development assistance" OR "investing" OR "invest" OR "financing" OR "funding" OR "investment$" OR "fund$" OR "finance" or "international aid")
OR ("economic" OR "financial*" OR "monetary") NEAR/3 ("support*" OR "assist*" OR "flow*" "resource*")

("target*" OR "focus*" OR "direct*" OR "allocat*" OR "concentrat*")

("best" OR "greatest" OR "biggest" OR powerful) NEAR/2 ("impact*" OR "effect*" OR "use" OR "need" OR "needs")

"least developed countr*" OR "least developed nation$"
      OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
      OR "less developed countr*" OR "less developed nation$"
      OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
      OR "underserved countr*" OR "underserved nation$"
      OR "deprived countr*" OR "deprived nation$"
      OR "middle income countr*" OR "middle income nation$"
      OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
      OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
      OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
      OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
      OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
      OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"
      OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish" OR "turkey" OR "georgia*"
)
```
Phrase 2
```py
TS=
("ODA" OR "official development assistance" OR "investing" OR "invest" OR "financing" OR "funding" OR "investment$" OR "fund$" OR "finance" or "international aid")
OR (("economic" OR "financial*" OR "monetary") NEAR/3 ("support*" OR "assist*" OR "flow*" "resource*"))

("target*" OR "focus*" OR "direct*" OR "allocat*" OR "concentrat*" OR "divid*" or "division*" OR "distribut*")

("national*" OR "regional*" OR "local*") NEAR/1 ("plan" OR "plans" OR "planning" OR "planned" OR "program$")

"least developed countr*" OR "least developed nation$"
      OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
      OR "less developed countr*" OR "less developed nation$"
      OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
      OR "underserved countr*" OR "underserved nation$"
      OR "deprived countr*" OR "deprived nation$"
      OR "middle income countr*" OR "middle income nation$"
      OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
      OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
      OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
      OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
      OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
      OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"
      OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish" OR "turkey" OR "georgia*"


```

### Target 10.c

> **10.c By 2030, reduce to less than 3 per cent the transaction costs of migrant remittances and eliminate remittance corridors with costs higher than 5 per cent**
>
> 10.c.1 Remittance costs as a proportion of the amount remitted
> 
This target is interpreted to cover research about reducing the transaction cost of migrant remittances and eliminating corridors of high costs.

```py
TS=
(

)
```

## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

Aldar, L., Pliskin, R., Hasson, Y. & Halperin, E. (2025). Legitimizing inclusion: Psychological interventions increase support for minority inclusion in the political game, but less so during wartime. Political Psychology. https://doi.org/10.1111/pops.70030

Sharif, I. (2024). Why economic inclusion is key to reducing poverty and empowering people. World Bank Blogs. https://blogs.worldbank.org/en/voices/why-economic-inclusion-is-key-to-reducing-poverty-and-empowering-people

Stewart, F. (2016). Horizontal Inequalities. World Social Science Report 2016. ISSC. https://en.unesco.org/inclusivepolicylab/sites/default/files/analytics/document/2018/9/wssr_2016_chap_07.pdf

UN DESA. (11.7.2019). Review of SDG implementation and interrelations among goals: Discussion on SDG 10 – Reduced inequalities, Background Note. https://sdgs.un.org/sites/default/files/documents/24021BN_SDG_10_Inequalities.pdf

<span id="f1">UN DESA. (2025).</span> *Goals: Reduce inequality within and among countries*. https://sdgs.un.org/goals/goal10#targets_and_indicators [Accessed 2025.04.02]

UN Statistics Division (2024a). SDG Indicators Metadata Repository - Target 10.1. Department of Economic and Social Affairs. https://unstats.un.org/sdgs/metadata/files/Metadata-10-01-01.pdf

UN Statistics Division (2024b). SDG Indicators Metadata Repository - Target 10.3. Department of Economic and Social Affairs. https://unstats.un.org/sdgs/metadata/files/Metadata-10-03-01.pdf

<span id="f2">United Nations. (2016, 2017, 2018, 2019, 2020, 2021).</span> *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/

United Nations (2018). High-level Political Forum 2018 - Inclusive, Safe, Resilient and Sustainable Societies and Persons with Disabilities. https://sustainabledevelopment.un.org/content/documents/18805PersonswithDisabilities_Sectoral_paper_HLPF2018.pdf

United Nations (2024). Inter-Agency Policy Brief: Accelerating SDG Localization to deliver on the promise of the 2030 Agenda for Sustainable Development. https://sdgs.un.org/publications/inter-agency-policy-brief-accelerating-sdg-localization-deliver-promise-2030-agenda.

World Bank Group (2025). Social inclusion. https://www.worldbank.org/en/topic/social-inclusion#1 [Accessed 17.06.2025]
