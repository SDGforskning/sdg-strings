# Search query for SDG 10 - Reduced inequalities, Bergen topic-approach.

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

This document contains search strings for finding publications related to the topics in the SDG 10 targets and indicators ("topic approach"; focus on recall, larger result set). We also have a version which finds publications related to the actions in the SDG 10 targets and indicators ("action approach"; focus on precision, smaller result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Department of Economic and Social Affairs website <a href="#f1">(UN DESA, 2025)</a>.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) <a href="#f2">(United Nations, 2016, 2017, 2018, 2019, 2020, 2021)</a>. Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

## 3. Targets

### Target 10.1

> **10.1 By 2030, progressively achieve and sustain income growth of the bottom 40 per cent of the population at a rate higher than the national average**
>
> 10.1.1 Growth rates of household expenditure or income per capita among the bottom 40 per cent of the population and the total population

This target is interpreted to cover research about the income growth rates of the poorest population.

Setting the limit to the bottom 40 % is a "practical compromise" that insures the target including the poorest populations in differing circumstances of different countries. The income growth rate is computed as average annual growth rate of either per capita consumption or actual income over about a 5-year period. (UN Statistics Divison 2024a.)  

This query consists of 1 phrase. The basic structure is *income growth rate + poor*

```py
TS=
(("income growth rate$" OR "growth in income$" OR "per capita consumption$" OR "per capita income$" OR
   "welfare aggregate$" OR "shared prosperit*" OR "welfare distribution$" OR "inclusive growth" OR "anti-poverty" OR
   "antipoverty" OR "out of poverty" OR
   (("earnings" OR "income$" OR "wage$" OR "salar*" OR "livelihood$"
    )
NEAR/3
    ("increas*" OR "growth" OR "rise$" OR "rising"
    )
   )
  )
AND
  ("bottom 40%" OR "bottom 40 percent" OR "bottom 40 per cent" OR "the poor" OR "poverty" OR "the poorest" OR
   "rural poor$" OR "urban poor$" OR "working poor$" OR "destitute$" OR "low income" OR "low-income" OR
   "disadvantaged" OR "extremely poor$" OR "severely poor$" OR "abjectly poor$" OR "absolutely poor$"
  )
 )
```

### Target 10.2

> **10.2 By 2030, empower and promote the social, economic and political inclusion of all, irrespective of age, sex, disability, race, ethnicity, origin, religion or economic or other status**
>
> 10.2.1 Proportion of people living below 50 per cent of median income, by sex, age and persons with disabilities

This target is interpreted to cover research about the social, economic and political inclusion of all. Research about social, economic and political exclusion is also included here. Special attention is paid to people in a disadvantaged position due to any characteristic, e.g. age, gender or disability (horizontal inequalities).

This target handles empowering people who face horizontal inequalities. This refers to groups of people who share an identity characteristic like race or religion and can therefore be exposed to the same kind of inequalities. (Stewart 2016). Ensuring that people in disadvantaged positions are part of decision-making processes (especially decisions regarding themselves) is a method recommended to accelerate progress in this target as well as the whole of SDG10 (United Nations 2024). A big part of structural discrimination and horizontal inequalities are linked to poorness, which is why living below 50 % of median income is considered a solid indicator for this target (Sharif 2024; World Bank Group 2025). For example, persons with disabilities and people of African descent experience significantly higher levels of poverty (United Nations 2018; World Bank Group 2025). 

Social inclusion means improving opportunities for individuals and groups to take part in society. This can include for example eradicating discriminatory attitudes from legal systems, labour markets and health care. (World Bank Group 2025.) Economic inclusion aims to empower individuals and communities by for example boosting their income and training them in economic skills (Sharif 2024). Political inclusion then covers opportunities for partaking in political activities, e.g. voting and participating in elections (Aldar ym. 2025).

This query consists of 1 phrase. The basic structure is *inclusion OR exclusion*

```py
TS=
(("social* inclusi*" OR "economic* inclusi*" OR "political* inclusi*" OR "societal* inclusi*" OR
  "societal activit*" OR "accessib*"
 )
OR
 ("horizontal* inequalit*" OR "horizontal* exclus*" OR "horizontal* marginal*" OR "horizontal vulnerab*" OR
  "social* exclus*" OR "economic* exclus*" OR "political* exclus*" OR "social* marginal*" OR "economic* marginal*"
  OR "political* marginal*" OR "societal exclus*" OR "societal marginal*" OR "intersecti* exclus*" OR
  "intersecti* vulnerab*" OR "intersecti* oppression*"
 )
)
```

### Target 10.3

> **10.3 Ensure equal opportunity and reduce inequalities of outcome, including by eliminating discriminatory laws, policies and practices and promoting appropriate legislation, policies and action in this regard**
>
> 10.3.1 Proportion of population reporting having personally felt discriminated against or harassed within the previous 12 months on the basis of a ground of discrimination prohibited under international human rights law

This target is interpreted to cover research about 
* equal opportunity and inequalities of outcome
* legislation, policies and other practices that increase inequality/discriminatory legislation, policies and other practices.

"Discrimination is any distinction, exclusion, restriction or preference or other differential treatment that is directly or indirectly based on prohibited grounds of discrimination, and which has the intention or effect of nullifying or impairing the recognition, enjoyment or exercise, on an equal footing, of human rights and fundamental freedoms in the political, economic, social, cultural or any other field of public life." The prohibited grounds of discrimination are listed in IHRL (UN Statistics Division 2024b.)

Many of the laws, policies and practicies that hinder equal opportunities are not explicitly discriminatory. However, many of these lack protection and support for e.g. women, persons with disabilities and sexual or ethnic minorities. This can lead to for example sexual harassment, racism and sexism as well as impeding with an individual's freedom of action regarding marriage, legal capacity, politics, movement, health and work among other things. Examples of such are laws restricting women from working in industrial occupations or practices that lead to cities being designed in a non-accessible manner. (APA 2020; Equal Future 2025; UN DESA 2018; United Nations 2018.)

This query consists of 2 phrases.

The basic structure of Phrase 1 is *equal opportunity OR inequalities*.

```py
TS=
(("equal" OR "equally" OR "equalit*" OR "equal opportunit*" OR "equal-opportunit*" OR "anti discriminat*" OR
  "anti-discriminat*" OR "non-discriminat*" OR "inclusi*" OR "accessib*" OR "egalitar*"
 )
 ("discriminat*" OR "inequalit*" OR "harass*" OR "racis*" OR "sexis*" OR "xenophob*" OR "homophob*" OR "transphob*"
  OR "stigma*" OR "ableis*" OR "inaccesib*" OR "barrier$" OR "obstacle$" OR "unequal*" OR "exclus*" OR "bias" OR
  "bias$ed"
 )
)
```

The basic structure of Phrase 2 is *discriminatory law OR anti-discriminatory law*.

```py
TS=
((("discriminat*" OR "inequalit*" OR "harass*" OR "racis*" OR "sexis*" OR "xenophob*" OR "homophob*" OR "transphob*"
   OR "stigma*" OR "ableis*" OR "inaccesib*" OR "barrier$" OR "obstacle$" OR "unequal*" OR "exclus*" OR "bias" OR
   "bias$ed"
  )
NEAR
  ("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR "treaty" OR
   "treaties" OR "strateg*" OR "framework$" OR "instrument$" OR "governance" OR "practice$" OR "action*" OR "rule"
   OR "rules" OR "procedur*" OR "initiative*"
  )
 )
OR
 (("equal" OR "equally" OR "equalit*" OR "equal opportunit*" OR "equal-opportunit*" OR "anti discriminat*" OR
   "anti-discriminat*" OR "non-discriminat*" OR "inclusi*" OR "accessib*" OR "egalitar*"
  )
NEAR
  ("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR "treaty" OR
   "treaties" OR "strateg*" OR "framework$" OR "instrument$" OR "governance" OR "practice$" OR "action*" OR "rule"
   OR "rules" OR "procedur*" OR "initiative*"
  )
 )
)
```

### Target 10.4

> **10.4 Adopt policies, especially fiscal, wage and social protection policies, and progressively achieve greater equality**
>
> 10.4.1 Labour share of GDP
>
> 10.4.2 Redistributive impact of fiscal policy

This target is interpreted to cover research about existing or new policy practices that reduce inequalities or promote achieving greater equality.
  
This target focuses on policies that ensure greater equality. Special focus is placed on fiscal, wage and social protection planning, but limited to those types of policies. The redistributive impact of fiscal policy is an indicator that basically compares how the distribution of income in a population changes before and after paying taxes, social insurance payments etc. This gives policy makers a tool to consider the impacts of national and international fiscal policies. (Lustig, Mariotti & Sánchez-Páramo 2020). Both countries and different organizations can have social protection policies that aim to secure access to regular income and social services, especially to vulnerable groups of people. These can include pensions, child benefits, affordable housing and food security among other things. (Engström & Vegar 2021). Wage policies concider themes such as minimum wage, gender pay gaps, collective bargaining of wages and wage protection (ILO 2024). In addition to these, countries and organizations have many other policies that can have massive impacts on equality being realized and advanced.

This query consists of 1 phrase. The basic structure is *laws AND increase/decrease + equality/inequality. ```("fiscal*" OR "wage*" OR "social* protect*" OR "social* securit*" OR "social* assist*" OR "economic*")``` was removed from the original search string not to limit the search only to these types of policies.

```py
TS=
(("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR "treaty" OR
  "treaties" OR "strateg*" OR "framework$" OR "instrument$" OR "governance" OR "practice$" OR "action$" OR
  "rule" OR "rules" OR "procedur*" OR "principle$" OR "initiative*"
 ) 
AND 
 (("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better$" OR "more efficient" OR "more effectiv*"
   OR "upgrad*" OR "scal* up" OR "expand$" OR "expansion*" OR "accelerat*" OR "advance$" OR "advancing" OR
   "develop$" OR "developing" OR "promot*" OR "foster*" OR "boost*" OR "attain*" OR "achiev*" OR "provid*" OR
   "ensur*" OR "guarantee*" OR "maintain*" OR "secur*" OR "strengthen*" OR "establish*" OR "sustain$" OR
   "sustaining" OR "consolidat*" OR "raise" OR "raising" OR "raised" OR "heighten*"
  )
NEAR
  ("equal" OR "equally" OR "equalit*" OR "equal opportunit*" OR "equal-opportunit*" OR "anti discriminat*" OR
   "anti-discriminat*" OR "non-discriminat*" OR "inclusi*" OR "accessib*" OR "egalitar*"
  )
 )
OR
  (("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR
    "degrad*" OR "tackl*" OR "alleviat*" OR "fight*" OR "combat*" OR "declin*" OR "stop*" OR "end" OR "ends" OR
    "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "avoid*" OR "prevent*" OR "combat*" OR "cure"
    OR "halt*" OR "resist*" OR "overcome" OR "escap*" OR "relief*" OR "lift$ out of" OR "lifting out of" OR
    "diminish*" OR "abate$" OR "abating" OR "dismantl*" OR "impair*" OR "nullif*" OR "hinder*"
   )
NEAR
   ("discriminat*" OR "inequalit*" OR "harass*" OR "racis*" OR "sexis*" OR "xenophob*" OR "homophob*" OR "transphob*"
    OR "stigma*" OR "ableis*" OR "inaccesib*" OR "barrier$" OR "obstacle$" OR "unequal*" OR "exclus*" OR "bias" OR
    "bias$ed"
   )
  )
)
```

### Target 10.5

> **10.5 Improve the regulation and monitoring of global financial markets and institutions and strengthen the implementation of such regulations**
>
> 10.5.1 Financial Soundness Indicators

This target is interpreted to cover research about the regulation and monitoring of global financial markets and institutions.

This query consists of 1 phrase. The basic structure is *regulation + financial institution*.

The operations of international financial institutions are evaluated through seven Financial Soundness Indicators (FSIs). Their global monitoring is the International Monetary Fund's (IMF's) responsibility, with data coming in from national central banks and other supervisory agencies. The FSIs are calculated by looking at the capitals, assets, loans, liabilities and exchanges of the institutions. The detailed definitions and concepts are listed in the target metadata. (UN Statistics Division 2024c.) IMF has created several standards that represent the minimum requirements for good practice. These focus on for example transparency, dissemination of data, standardized supervision and combating money laundering. They are designed to be universally applicable and flexible. The objective of these standards is to ensure that all financial institutions from a global to a regional level can function in fair and efficient ways. (FSB 2025.)

This query consists of 1 phrase. The basic structure is action + regulation + financial institution ("fair*" OR "sustainab*" OR "transparen*" OR "equalit*" OR "democra*" OR "responsib*" OR "accountab*" OR "legitimat*" OR "effectiv*" OR "credib*" OR "ethic*" OR "egalitar*")was removed from the search string. While the goal of implementing better regulation and monitoring is to make the institutions function in more responsible and transparent manners, this isn't directly mentioned in the target and is also left out of the interpretation.

```py
TS=
(("manage$" OR "control*" OR "regulat*" OR "legislat*" OR "govern$" OR "monitor*" OR "surveillanc*" OR 
  "secure$" OR "securing" OR "assess*" OR "examin*" OR "evaluat*" OR "measur*" OR "supervis*" OR "validat*"
  OR "mandat*"
 )
AND
 (("global*" OR "international*"
  ) 
NEAR/5
  ("economic*" OR "financial*" OR "monetar*" OR "money" OR "capital" OR "asset$" OR "payment$" OR "trade"
  )
NEAR/5
  ("institution*" OR "market*" OR "bank*" OR "central bank*" OR "depositor*" OR "repositor*" OR
   "system$"
  )
 )
NOT "globalization"
)
```

### Target 10.6

> **10.6 Ensure enhanced representation and voice for developing countries in decision-making in global international economic and financial institutions in order to deliver more effective, credible, accountable and legitimate institutions**
>
> 10.6.1 Proportion of members and voting rights of developing countries in international organizations

This target is interpreted to cover research about the representation and decision-making powers of developing countries in international economic institutions.

In order to achieve truely effective and permanent changes on a global level, it is crucial to involve developing countries in the decision-making processes that concern their own economical development as well (UN DESA 2019; UN 2024).

This query consists of 1 phrase. The basic structure is *representation + developing countries + international economic institution*

```py
TS=
((("representat*" OR "voice*" OR "vote*" OR "decision-making" OR "decision making" OR 
   "decision-making power*" OR "decision making power*" OR "participat*"
  )
NEAR
  ("least developed countr*" OR "least developed nation$" OR "developing countr*" OR "developing nation$" OR
   "developing states" OR "developing world" OR "less developed countr*" OR "less developed nation$" OR
   "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
   OR "underserved countr*" OR "underserved nation$" OR "deprived countr*" OR "deprived nation$" OR
   "middle income countr*" OR "middle income nation$" OR "low income countr*" OR "low income nation$" OR
   "lower income countr*" OR "lower income nation$" OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR
   "poorer nation$" OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR
   "transitional countr*" OR "emerging economies" OR "emerging nation$" OR "Angola*" OR "Benin" OR "beninese" OR
   "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic"
   OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR
   "Eritrea*" OR "Ethiopia*" OR "gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*"
   OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "malawian" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR
   "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR
   "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*"
   OR "zambian$" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma"
   OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR
   "Bhutan*" OR "bhutanese" OR "Nepal*" OR "Yemen*" OR "Haiti*" OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR
   "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR
   "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR
   "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR
   "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR
   "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR
   "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR
   "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR
   "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR
   "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR
   "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR
   "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR
   "Virgin Islands" OR "Armenia*" OR "Azerbaijan*" OR "Bolivia*" OR "Botswana*" OR "Eswatini" OR "eswantian" OR
   "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR
   "Lao People’s Democratic Republic" OR "Laos" OR "Mongolia*" OR "North Macedonia" OR "Republic of Macedonia" OR
   "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan"
   OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zimbabwe*" OR "albania*" OR
   "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia"
   OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR
   "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR
   "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR
   "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR
   "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR
   "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR
   "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR
   "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo"
   OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR
   "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR
   "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*"
   OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR
   "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR
   "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR
   "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR
   "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria"
   OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR
   "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish" OR "turkey" OR
   "georgia*"
  )
 )
AND
 (("global*" OR "international*"
  ) 
NEAR/5
  ("economic*" OR "financial*" OR "monetar*" OR "money" OR "capital" OR "asset$" OR "payment$" OR "trade"
  )
NEAR/5
  ("institution*" OR "market*" OR "bank*" OR "central bank*" OR "depositor*" OR "repositor*" OR
   "system$"
  )
 )
NOT "globalization"
)
```

### Target 10.7

> **10.7 Facilitate orderly, safe, regular and responsible migration and mobility of people, including through the implementation of planned and well-managed migration policies**
>
> 10.7.1 Recruitment cost borne by employee as a proportion of montlhy income earned in country of destination
>
> 10.7.2 Number of countries with migration policies that facilitate orderly, safe, regular and responsible migration and mobility of people
>
> 10.7.3 Number of people who died or disappeared in the process of migration towards an international destination
>
> 10.7.4 Proportion of the population who are refugees, by country of origin

This target is interpreted to cover research about safe, responsible and regular migration and mobility of people.

"Migration" is not a term officially defined under international law, but refers to a situation where a person moves away from their usual place of recidence. The move can be within-country or to another country, it can be temporary or permanent and be the cause of a variety of reasons. Excluded from this definition are movements due to "recreation, holiday, visits to friends and relatives, business, medical treatment or religious pilgrimages”, that in turn are covered by "mobility of people". (IOM 2019.) Migration can enable people to very effectively better their living conditions, for example by accessing higher wage jobs. Migrants also often support their relatives in their country or region of origin, thus spreading the effect even further. Countries and regions receiving migrants can greatly benefit from the skills they bring. Well-managed movement of people can so be beneficial to all parties, as well as having a big effect on reducing inequalities. However, there are still some remarkable barriers for migration and movement of people always functioning in safe, orderly, regular and responsible manners, and these can be measured through the target indicators. (UN DESA 2019b.) Orderly migration is defined as “the movement of a person from his/her usual place of residence, in keeping with the laws and regulations governing exit of the country of origin and travel, transit and entry into the host country” and regular as “migration that occurs through recognized, legal channels”. The concepts of safe and responsible migration or well-managed migration policies are not explicitly defined. (IOM 2019.) These can however be seen as policies that actively work towards fulfilling the principles and objectives of the Migration Governance Framework that are pictured in the 10.7.2. indicator metadata (UN Statistics Division 2023). 

This query consists of 1 phrase. The basic structure is *security + movement of people OR risks + movement of people*

```py
TS=
((("secure" OR "security" OR "protect*" OR "reliab*" OR "stability" OR "stable" OR "safe" OR "regular" OR "responsible"
   OR "orderly" OR "planned" OR "well-managed" OR "well managed" OR "well-planned" OR "well planned" OR "managed" OR
   "dignif*"
  )
NEAR
  ("migrat*" OR "mobilit*" OR "move" OR "moving" OR "movement" OR "travel*" OR "international*" OR "internal*" OR
   "intra stat*" OR "within-country" OR "within country"
  )
NEAR
  ("immigrant*" OR "emigrant*" OR "alien$" OR "resident alien$" OR "migrant*" OR "settler$" OR "asylum seeker$" OR 
   "illegal alien$" OR "illegal immigrant$" OR "undocumented alien" OR "undocumented immigrant$" OR "refugee*" OR
   "displaced" OR "expat*" OR "transferee$"
  )
 )
OR
 (("risk$" OR "hazard*" OR "insecure" OR "insecurity" OR "unprotect*" OR "unrelaib*" OR "vulnerab*" OR "dead*" OR
   "die$" OR "disappear*" OR "unstability" OR "unstable" OR "trafficking" OR "barrier$" OR "obstacle$"
  )
NEAR
  ("migrat*" OR "mobilit*" OR "move" OR "moving" OR "movement" OR "travel*" OR "international*" OR "internal*" OR
   "intra stat*" OR "within-country" OR "within country"
  )
NEAR
  ("immigrant*" OR "emigrant*" OR "alien$" OR "resident alien$" OR "migrant*" OR "settler$" OR "asylum seeker$" OR 
   "illegal alien$" OR "illegal immigrant$" OR "undocumented alien" OR "undocumented immigrant$" OR "refugee*" OR
   "displaced" OR "expat*" OR "transferee$"
  )
 )
)
```

### Target 10.a

> **10.a Implement the principle of special and differential treatment for developing countries, in particular least developed countries, in accordance with World Trade Organization agreements**
>
> 10.a.1 Proportion of tariff lines applied to imports from least developed countries and developing countries with zero-tariff

This target is interpreted to cover research about the principle of special and differential treatment for developing countries, in accordance with the World Trade Organisation agreements.

SDT principles are part of WTO'S Doha Agenda and are designed to support developing countries in implementing WTO agreements and commitments. For example, developing countries might have a longer time for implementing certain commitments, their trade interest are safeguarded by the other WTO members and they receive support for building their infrastructures and increasing trading opportunities. (WTO 2025.) Accurate measurements for most of the SDTs are not available, which is why tariff lines have been chosen as the measurable indicator here. Tariffs are customs duties on merchandise imports. By applying zero-tariffs to imports from developing countries, it is possible to boost local production and exportation. (UN Statistics Division 2016.)

This query consists of 1 phrase. The basic structure is *SDT + developing country + agreement*

```py
TS=
(("special and differential treatment*" OR "SDT" OR "S&D" OR "S and D" OR "preferential treatment*" OR "zero-tariff*"
  OR "zero tariff*" OR "0% tariff" OR "0 per cent tariff" OR "0 percent tariff" OR "zero % tariff" OR 
  "zero per cent tariff" OR "zero percent tariff" OR "duty-free treatment*" OR "duty free treatment" OR "free of duty"
 ) 
NEAR
 ("least developed countr*" OR "least developed nation$" OR "developing countr*" OR "developing nation$" OR
  "developing states" OR "developing world" OR "less developed countr*" OR "less developed nation$" OR
  "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
  OR "underserved countr*" OR "underserved nation$" OR "deprived countr*" OR "deprived nation$" OR
  "middle income countr*" OR "middle income nation$" OR "low income countr*" OR "low income nation$" OR
  "lower income countr*" OR "lower income nation$" OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR
  "poorer nation$" OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR
  "transitional countr*" OR "emerging economies" OR "emerging nation$" OR "Angola*" OR "Benin" OR "beninese" OR
  "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic"
  OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR
  "Eritrea*" OR "Ethiopia*" OR "gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*"
  OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "malawian" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR
  "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR
  "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*"
  OR "zambian$" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma"
  OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR
  "Bhutan*" OR "bhutanese" OR "Nepal*" OR "Yemen*" OR "Haiti*" OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR
  "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR
  "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR
  "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR
  "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR
  "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR
  "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR
  "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR
  "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR
  "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR
  "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR
  "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR
  "Virgin Islands" OR "Armenia*" OR "Azerbaijan*" OR "Bolivia*" OR "Botswana*" OR "Eswatini" OR "eswantian" OR
  "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR
  "Lao People’s Democratic Republic" OR "Laos" OR "Mongolia*" OR "North Macedonia" OR "Republic of Macedonia" OR
  "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan"
  OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zimbabwe*" OR "albania*" OR
  "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia"
  OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR
  "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR
  "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR
  "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR
  "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR
  "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR
  "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR
  "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo"
  OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR
  "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR
  "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*"
  OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR
  "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR
  "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR
  "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR
  "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria"
  OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR
  "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish" OR "turkey" OR
  "georgia*"
 )
AND
 ("World Trade Organization" OR "WTO" OR "trade facilitation agreement*" OR "trade agreement*" OR "trade opportunit*"
  OR "trading opportunit*" OR "doha declaration$" OR "doha ministerial declaration$" OR "doha development agenda$" OR
  "doha mandate$"
 )
)
```

### Target 10.b

> **10.b Encourage official development assistance and financial flows, including foreign direct investment, to States where the need is greatest, in particular least developed countries, African countries, small island developing States and landlocked developing countries, in accordance with their national plans and programmes**
>
> 10.b.1 Total resource flows for development, by recipient and donor countries and type of flow (e.g. official development assistance, foreign direct investment and other flows)

This target is interpreted to cover research about 
    * the official channels for development assistance and financial flows
    * the targeting of development assistance and financial flows
    * the national, regional and local plans of the recipient countries for the division of development assistance and financial flows
    
We divided this interpretation to place focus on using official channels for aid as well as targeting it properly. We also feel the need to put some emphasis on localization as per portrayed in Inter-Agency Policy Brief: Accelerating SDG Localization to deliver on the promise of the 2030 Agenda for Sustainable Development (UN 2024).

```py
TS=
(

)
```

### Target 10.c

> **10.c By 2030, reduce to less than 3 per cent the transaction costs of migrant remittances and eliminate remittance corridors with costs higher than 5 per cent**
>
> 10.c.1 Remittance costs as a proportion of the amount remitted
> 
This target is interpreted to cover research about the transaction costs of migrant remittances.

```py
TS=
(

)
```

## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

<span id="f1">UN DESA. (2025).</span> *Goals: Reduce inequality within and among countries*. https://sdgs.un.org/goals/goal10#targets_and_indicators [Accessed 2025.04.02]

<span id="f2">United Nations. (2016, 2017, 2018, 2019, 2020, 2021).</span> *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/
