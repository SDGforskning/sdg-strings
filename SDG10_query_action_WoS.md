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

    APA: American Psychology Association
    FSB: Financial Stability Board
    FSI: Financial Soundness Indicator
    IHRL: International Human Rights Law
    ILO: International Labour Organization
    IMF: International Monetary Fund
    IOM: International Organization for Migration
    ODA: Official Development Assistance
    SDT: Special and Differential Treatment
    UN: United Nations
    UN DESA: UN Department of Economic and Social Affairs

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
 (("foster*" OR "increas*" OR "promot*" OR "boost*" OR "enhanc*" OR "improv*" OR "better$" OR "attain*" OR "achiev*"
   OR "provid*" OR "ensur*" OR "guarantee*" OR "maintain*" OR "secur*" OR "strengthen*" OR "develop$" OR "establish*"
   OR "sustain$" OR "sustaining" OR "standardi*" OR "regulari*" OR "consolidat*" OR "stabili*" OR "normali*" OR
   "uphold*" OR "stable" OR "fixed" OR "perpetual*" OR "lasting" OR "enduring" OR "facilitat*" OR "raise" OR "raising"
   OR "raised"
  )
NEAR
  ("income growth" OR "income growth rate$" OR "growth in income$" OR "per capita consumption$" OR "per capita income$"
   OR "welfare aggregate$" OR "shared prosperit*" OR "welfare distribution$" OR "inclusive growth" OR
   "earnings increas*" OR "income increas*" OR "wage growth" OR "wage increas*" OR "salar* rise"
  )
 )
AND
  ("bottom 40%" OR "bottom 40 percent" OR "bottom 40 per cent" OR "the poor" OR "poverty" OR "the poorest" OR
   "rural poor" OR "urban poor" OR "working poor" OR "destitute$" OR "low income" OR "low-income" OR
   "disadvantaged"
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

This query consists of 1 phrase. The basic structure is *action (positive) + inclusion OR action (negative) + exclusion*

```py
TS=
((("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better$" OR "more efficient*" OR
   "more effectiv*" OR "higher$" OR "upgrad*" OR "scal* up" OR "build*" OR "expand$" OR "expansion*" OR "accelerat*"
   OR "advance$" OR "advancing" OR "develop$" OR "developing" OR "empower*" OR "promot*" OR "ensur*" OR "attain*" OR
   "achiev*" OR "encourag*" OR "facilitat*" OR "boost*"
  )
NEAR
  ("social* inclusi*" OR "economic* inclusi*" OR "political* inclusi*" OR "societal* inclusi*" OR
   "societal activit*" OR "accessib*"
  )
 )
OR
 (("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR
   "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR
   "declin*" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR
   "avoid*" OR "prevent*" OR "cure" OR "halt*" OR "resist*" OR "overcome"
  )
NEAR
  ("horizontal* inequalit*" OR "horizontal* exclu*" OR "horizontal* marginal*" OR "horizontal vulnerab*" OR
   "social* exclu*" OR "economic* exclu*" OR "political* exclu*" OR "social* marginal*" OR "economic* marginal*" OR
   "political* marginal*" OR "societal exclu*" OR "societal marginal*" OR "intersecti* exclu*" OR
   "intersecti* vulnerab*" OR "intersecti* oppression*"
  )
 )
)
```

### Target 10.3

> **10.3 Ensure equal opportunity and reduce inequalities of outcome, including by eliminating discriminatory laws, policies and practices and promoting appropriate legislation, policies and action in this regard**
>
> 10.3.1 Proportion of population reporting having personally felt discriminated against or harassed within the previous 12 months on the basis of a ground of discrimination prohibited under international human rights law

This target is interpreted to cover research about 
* ensuring equal opportunity and reducing inequalities of outcome
* eliminating discriminatory legislation, policies and other practices and promote ones that ensure equal opportunity and reduce inequalities of outcome.

"Discrimination is any distinction, exclusion, restriction or preference or other differential treatment that is directly or indirectly based on prohibited grounds of discrimination, and which has the intention or effect of nullifying or impairing the recognition, enjoyment or exercise, on an equal footing, of human rights and fundamental freedoms in the political, economic, social, cultural or any other field of public life." The prohibited grounds of discrimination are listed in IHRL (UN Statistics Division 2024b.)

Many of the laws, policies and practicies that hinder equal opportunities are not explicitly discriminatory. However, many of these lack protection and support for e.g. women, persons with disabilities and sexual or ethnic minorities. This can lead to for example sexual harassment, racism and sexism as well as impeding with an individual's freedom of action regarding marriage, legal capacity, politics, movement, health and work among other things. Examples of such are laws restricting women from working in industrial occupations or practices that lead to cities being designed in a non-accessible manner. (APA 2020; Equal Future 2025; UN DESA 2018; United Nations 2018.)

This query consists of 2 phrases. 

The basic structure of Phrase 1 is *action (ensure) + equal opportunity OR action (reduce) + inequalities*.

```py
TS=
((("ensure" OR "secure$" OR "securing" OR "make$ sure" OR "making sure" OR "make$ certain" OR "making certain" OR
   "strengthen*" OR "stabili*" OR "guarantee*" OR "assure$" OR "assuring"
 )
NEAR/3
  ("equal" OR "equally" OR "equalit*" OR "equal opportunit*" OR "equal-opportunit*" OR "anti discriminat*" OR
   "anti-discriminat*" OR "non-discriminat*" OR "inclusi*" OR "accessib*"
  )
 )
OR
 (("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR 
   "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR
   "declin*" OR "abate$" OR "abating" OR "diminish*"
  )
NEAR/3
  ("discriminat*" OR "inequalit*" OR "harass*" OR "racis*" OR "sexis*" OR "xenophob*" OR "homophob*" OR "transphob*"
   OR "stigma*" OR "ableis*"
  )
 )
)
```

The basic structure of Phrase 2 is *action (stop) + discriminatory law OR action (promote) + anti-discriminatory law*.

```py
TS=
((("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "avoid*" OR
   "prevent*" OR "fight*" OR "combat*" OR "halt*" OR "resist*" OR "prohibit*"
  )
NEAR
  (("discriminat*" OR "inequalit*" OR "harass*" OR "racis*" OR "sexis*" OR "xenophob*" OR "homophob*" OR "transphob*"
    OR "stigma*" OR "ableis*"
   )
NEAR
   ("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR "treaty" OR
    "treaties" OR "strateg*" OR "framework$" OR "instrument$" OR "governance" OR "practice$" OR "action*" OR "rule"
    OR "rules" OR "procedur*" OR "initiative*"
   )
  )
 )
OR 
 (("promot*" OR "increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better$" OR "more efficient*" OR 
   "more effectiv*" OR "build*" OR "accelerat*" OR "advance$" OR "advancing" OR "develop$" OR "developing" OR
   "development" OR "encourag*" OR "facilitat*" OR "establish*" OR "propose*" OR "implement*" OR "adopt*" OR
   "introduc*" OR "boost*" OR "foster*"
  )
NEAR
  (("equal" OR "equally" OR "equalit*" OR "equal opportunit*" OR "equal-opportunit*" OR "anti discriminat*" OR
    "anti-discriminat*" OR "non-discriminat*" OR "inclusi*" OR "accessib*"
   )
NEAR
   ("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR "treaty" OR
    "treaties" OR "strateg*" OR "framework$" OR "instrument$" OR "governance" OR "practice$" OR "action*" OR "rule"
    OR "rules" OR "procedur*" OR "initiative*"
   )
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

This target is interpreted to cover research about promoting the implementation of existing or new social and economic policy practices to reduce inequalities/achieve greater equality.

This target focuses on policies that ensure greater equality especially through fiscal, wage and social protection planning. The redistributive impact of fiscal policy is an indicator that basically compares how the distribution of income in a population changes before and after paying taxes, social insurance payments etc. This gives policy makers a tool to consider the impacts of national and international fiscal policies.  (Lustig, Mariotti & Sánchez-Páramo 2020). Both countries and different organizations can have social protection policies that aim to secure access to regular income and social services, especially to vulnerable groups of people. These can include pensions, child benefits, affordable housing and food security among other things. (Engström & Vegar 2021). Wage policies concider themes such as minimum wage, gender pay gaps, collective bargaining of wages and wage protection (ILO 2024). All of these policies have massive impacts on equality being realized and advanced.

This query consists of 1 phrase. The basic structure is *action + laws AND action (increase/decrease) + equality/inequality*

```py
TS=
((("establish*" OR "propose*" OR "design*" OR "implement*" OR "plan" OR "plans" OR "planned" OR "planning" OR
    "adopt*" OR "introduc*" OR "architect*" OR "develop" OR "development" OR "promot*" OR "facilitat*"
   )
NEAR
  (("fiscal*" OR "wage*" OR "social* protect*" OR "social* securit*" OR "social* assist*" OR "economic*"
   )
NEAR
   ("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR "treaty" OR
    "treaties" OR "strateg*" OR "framework$" OR "instrument$" OR "governance" OR "practice$" OR "action$" OR
    "rule" OR "rules" OR "procedur*" OR "principle$" OR "redistributive impact of fiscal policy"
   )
  )
 ) 
AND 
 ((("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better$" OR "more efficient" OR "more effectiv*"
    OR "upgrad*" OR "scal* up" OR "expand$" OR "expansion*" OR "accelerat*" OR "advance$" OR "advancing" OR
    "develop$" OR "developing" OR "promot*" OR "foster*" OR "boost*" OR "attain*" OR "achiev*" OR "provid*" OR
    "ensur*" OR "guarantee*" OR "maintain*" OR "secur*" OR "strengthen*" OR "establish*" OR "sustain$" OR
    "sustaining" OR "consolidat*" OR "raise" OR "raising" OR "raised"
   )
NEAR
   ("equal*" OR "equitable" OR "equal opportunit*" OR "anti discriminat*" OR "anti-discriminat*" OR "justice*"
   )
  )
OR
  (("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR
    "degrad*" OR "tackl*" OR "alleviat*" OR "fight*" OR "combat*" OR "declin*" OR "stop*" OR "end" OR "ends" OR
    "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "avoid*" OR "prevent*" OR "combat*" OR "cure"
    OR "halt*" OR "resist*" OR "overcome"
   )
NEAR
   ("discriminator*" OR "inequalit*" OR "harass*"
   )
  )
 )
)
```

### Target 10.5

> **10.5 Improve the regulation and monitoring of global financial markets and institutions and strengthen the implementation of such regulations**
>
> 10.5.1 Financial Soundness Indicators

This target is interpreted to cover research about improving the regulation and monitoring of global financial markets and institutions.

The operations of international financial institutions are evaluated through seven Financial Soundness Indicators (FSIs). Their global monitoring is the International Monetary Fund's (IMF's) responsibility, with data coming in from national central banks and other supervisory agencies. The FSIs are calculated by looking at the capitals, assets, loans, liabilities and exchanges of the institutions. The detailed definitions and concepts are listed in the target metadata. (UN Statistics Division 2024c.) IMF has created several standards that represent the minimum requirements for good practice. These focus on for example transparency, dissemination of data, standardized supervision and combating money laundering. They are designed to be universally applicable and flexible. The objective of these standards is to ensure that all financial institutions from a global to a regional level can function in fair and efficient ways. (FSB 2025.)

This query consists of 1 phrase. The basic structure is *action + regulation + financial institution*

```py
TS=
((("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better$" OR "more efficient" OR 
    "more effectiv*" OR "higher$" OR "upgrad*" OR "scal* up" OR "expand$" OR "expansion*" OR "accelerat*" OR 
    "advance$" OR "advancing" OR "develop$" OR "developing" OR "promot*" OR "encourag*" OR "facilitat*" OR
    "ensur*" OR "attain*" OR "achiev*" OR "build* capacit*" OR "capacit* building$" OR "capacit* OR development*"
    OR "establish*" OR "implement*" OR "adopt*" OR "raise" OR "raising" OR "raised" OR "boost*"
   )
NEAR/5
   ("manage$" OR "control*" OR "regulat*" OR "legislat*" OR "govern$" OR "monitor*" OR "surveillanc*" OR 
    "secure$" OR "securing" OR "assess*" OR "examin*" OR "evaluat*" OR "measur*" OR "supervis*" OR "validat*"
    OR "mandat*"
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
AND
  ("fair*" OR "sustainab*" OR "transparen*" OR "equalit*" OR "democra*" OR "responsib*" OR
   "accountab*" OR "legitimat*" OR "effectiv*" OR "credib*" OR "ethic*"
  )
)
```

### Target 10.6

> **10.6 Ensure enhanced representation and voice for developing countries in decision-making in global international economic and financial institutions in order to deliver more effective, credible, accountable and legitimate institutions**
>
> 10.6.1 Proportion of members and voting rights of developing countries in international organizations

This target is interpreted to cover research about enhancing the representation and decision-making powers of developing countries in international economic institutions.

In order to achieve truely effective and permanent changes on a global level, it is crucial to involve developing countries in the decision-making processes that concern their own economical development as well as giving them more representation overall (UN DESA 2019a; UN 2024).

This query consists of 1 phrase. The basic structure is *action + representation + developing countries + international economic institution*

```py
TS=
((("foster*" OR "boost*" OR "provid*" OR "ensur*" OR "guarantee*" OR "establish*" OR "standardi*" OR "regulari*" OR
   "consolidat*" OR "increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better*" OR "more efficient*" OR
   "more effectiv*" OR "higher" OR "upgrad*" OR "scal* up" OR "build* capacity" OR "capacity building" OR
   "capacity development" OR "expand$" OR "expansion*" OR "accelerat*" OR "advance" OR "advancing" OR "develop$" OR
   "developing" OR "encourag*" OR "facilitat*" OR "promot*" OR "attain*" OR "achiev*" OR "raise" OR "raising" OR
   "raised"
  )
NEAR
  ("representat*" OR "voice*" OR "vote*" OR "decision-making" OR "decision making" OR 
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
> 10.7.1 Recruitment cost borne by employee as a proportion of monthly income earned in country of destination
>
> 10.7.2 Number of countries with migration policies that facilitate orderly, safe, regular and responsible migration and mobility of people
>
> 10.7.3 Number of people who died or disappeared in the process of migration towards an international destination
>
> 10.7.4 Proportion of the population who are refugees, by country of origin

This target is interpreted to cover research about ensuring safe, responsible and regular migration and mobility of people.

Migration can enable people to very effectively better their living conditions, for example by accessing higher wage jobs. Migrants also often support their relatives in their country or region of origin, thus spreading the effect even further. Countries and regions receiving migrants can greatly benefit from the skills they bring. Well-managed movement of people can so be beneficial to all parties, as well as having a big effect on reducing inequalities. However, there are still some remarkable barriers for migration and movement of people always functioning in safe, orderly, regular and responsible manners, and these can be measured through the target indicators. (UN DESA 2019b.) Orderly migration is defined as “the movement of a person from his/her usual place of residence, in keeping with the laws and regulations governing exit of the country of origin and travel, transit and entry into the host country” and regular as “migration that occurs through recognized, legal channels”. The concepts of safe and responsible migration or well-managed migration policies are not explicitly defined. (IOM 2019.) These can however be seen as policies that actively work towards fulfilling the principles and objectives of the Migration Governance Framework that are pictured in the 10.7.2. indicator metadata (UN Statistics Division 2023). "Migration" is not officially defined under international law, but refers to a situation where a person moves away from their usual place of recidence. The move can be within-country or to another country, it can be temporary or permanent and be the cause of a variety of reasons. Excluded from this definition are movements due to "recreation, holiday, visits to friends and relatives, business, medical treatment or religious pilgrimages”, that in turn are covered by "mobility of people". (IOM 2019.)

This query consists of 1 phrase. The basic structure is *action (positive) + security + movement of people OR action (negative) + risks + movement of people*

```py
TS=
((("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "upgrad*" OR "scal* up" OR "foster*" OR 
   "build* capacit*" OR "capacity building" OR "capacity development" OR "accelerat*" OR "advance$" OR "advancing" OR
   "develop$" OR "developing" OR "promot*" OR "ensure" OR "attain*" OR "achiev*" OR "implement*" OR "facilitat*" OR
   "provid*" OR "boost*" OR "raise" OR "raising" OR "raised"
  )
NEAR
  ("secure" OR "security" OR "protect*" OR "reliab*" OR "stability" OR "stable" OR "safe" OR "regular" OR "responsible"
   OR "orderly" OR "planned" OR "well-managed" OR "well managed" OR "well-planned" OR "well planned" OR "managed" OR
   "dignif*"
  )
NEAR
  ("migrat*" OR "mobilit*" OR "move" OR "moving" OR "movement" OR "travel*" OR "international*" OR "internal*" OR
   "intra stat*" OR "within-country" OR "within country"
)
NEAR
  ("immigrant*" OR "emigrant*" OR "alien$" OR "resident alien$" OR "migrant*" OR "settler$" OR "asylum seeker$"
   "illegal alien$" OR "illegal immigrant$" OR "undocumented alien" OR "undocumented immigrant$" OR "refugee*" OR
   "displaced" OR "expat*" OR "transferee$"
  )
 )
OR
 (("decreas*" OR "minimi*" OR "reduc*" OR "mitigat*" OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$"
   OR "lowered" OR "fight*" OR "combat*" OR "declin*" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*"
   OR "eliminat*" OR "eradicat*" OR "avoid*" OR "prevent*" OR "halt*" OR "resist*" OR "overcome")
NEAR
  ("risk$" OR "hazard*" OR "insecure" OR "insecurity" OR "unprotect*" OR "unrelaib*" OR "vulnerab*" OR "dead*" OR
   "die$" OR "disappear*" OR "unstability" OR "unstable" OR "trafficking")
NEAR
  ("migrat*" OR "mobilit*" OR "move" OR "moving" OR "movement" OR "travel*" OR "international*" OR "internal*" OR
   "intra stat*" OR "within-country" OR "within country"
  )
NEAR
  ("immigrant*" OR "emigrant*" OR "alien$" OR "resident alien$" OR "migrant*" OR "settler$" OR "asylum seeker$"
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

This target is interpreted to cover research about implementing the principle of special and differential treatment (SDT) for developing countries, in accordance with the World Trade Organisation agreements.

SDT principles are part of WTO'S Doha Agenda and are designed to support developing countries in implementing WTO agreements and commitments. For example, developing countries might have a longer time for implementing certain commitments, their trade interest are safeguarded by the other WTO members and they receive support for building their infrastructures and increasing trading opportunities. (WTO 2025.) Accurate measurements for most of the SDTs are not available, which is why tariff lines have been chosen as the measurable indicator here. Tariffs are customs duties on merchandise imports. By applying zero-tariffs to imports from developing countries, it is possible to boost local production and exportation. (UN Statistics Division 2016.)

This query consists of 1 phrase. The basic structure is *action + SDT + developing country + agreement*

```py
TS=
((("implement*" OR "establish*" OR "plan" OR "plans" OR "planned" OR "planning" OR "adopt*" OR "introduc*" OR "develop"
   OR "development" OR "ensure" OR "attain*" OR "achiev*" OR "increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR
   "accelerat*" OR "advanc*" OR "promot*" OR "facilitat*" OR "boost*" OR "apply" OR "applying" OR "applied"
  )
NEAR
  ("special and differential treatment*" OR "SDT" OR "S&D" OR "S and D" OR "preferential treatment*" OR "zero-tariff*" OR
   "zero tariff*" OR "0% tariff" OR "0 per cent tariff" OR "0 percent tariff" OR "zero % tariff" OR "zero per cent tariff"
   OR "zero percent tariff" OR "duty-free treatment*" OR "duty free treatment" OR "free of duty"
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
  ("World Trade Organization" OR "WTO" OR "trade facilitation agreement*" OR "trade agreement*" OR "trade opportunit*" OR
   "trading opportunit*" OR "doha declaration$" OR "doha ministerial declaration$" OR "doha development agenda$" OR
   "doha mandate$"
  )
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

The basic structure of Phrase 1 is *action (encourage) + financial assistance + action (target) + need + developing countries*.

Phrase 1
```py
TS=
((("encourag*" OR "increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "more efficient*" OR "more effectiv*"
   OR "scal* up" OR "accelerat*" OR "advance$" OR "advancing" OR "ensure$" OR "attain*" OR "achiev*" OR "facilitat*" OR
   "raise" OR "raising" OR "raised" OR "boost*"
  )
NEAR
  ("ODA" OR "official development assistance*" OR "development assistance*" OR "official development aid" OR
   "development aid" OR "foreign aid" OR "international aid" OR "cooperation fund*" OR "development spending$" OR
   "foreign invest*" OR "international invest*" OR "foreign financ*" OR "international financ*" OR "foreign fund*" OR
   "international fund*" OR
  (("economic" OR "financial*" OR "monetary"
   )
NEAR/3
   ("support*" OR "assist*" OR "flow*" OR "resource*" OR "subsid*" OR "aid$"
   )
  )
  )
NEAR
  ("target*" OR "focus*" OR "direct*" OR "allocat*" OR "concentrat*" OR "aim$" OR "aiming" OR "aimed" OR "optimi$e*" OR
   "channel*" OR "point" OR "points" OR "pointed" OR "orient$" OR "oriantate$"
  )
NEAR
  ("impact*" OR "effect*" OR "use" OR "need" OR "needs" OR "needed" OR "efficien*"
  )
 )
AND
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
```
The basic structure of Phrase 2 is *action (target) + financial assistance + plans + developing country*

Phrase 2
```py
TS=
((("target*" OR "focus*" OR "direct*" OR "allocat*" OR "concentrat*" OR "divid*" or "division*" OR "distribut*"
  )
NEAR
  ("ODA" OR "official development assistance*" OR "development assistance*" OR "official development aid" OR
   "development aid" OR "foreign aid" OR "international aid" OR "cooperation fund*" OR "development spending$" OR
   "foreign invest*" OR "international invest*" OR "foreign financ*" OR "international financ*" OR "foreign fund*" OR
   "international fund*" OR
  (("economic" OR "financial*" OR "monetary"
   )
NEAR/3
   ("support*" OR "assist*" OR "flow*" OR "resource*" OR "subsid*" OR "aid$"
   )
  )
  )
NEAR
  (("national*" OR "regional*" OR "local*"
   )
NEAR/3
   ("plan" OR "plans" OR "planning" OR "planned" OR "program$" OR "scheme$" OR "project$" OR "blueprint$" OR "layout$" OR
    "design$" OR "framework$" OR "initiative$" OR "bid$" OR "effort$" OR "venture$" OR "undertaking$" OR "enterprise$"
   )
  )
  )
AND
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
```

### Target 10.c

> **10.c By 2030, reduce to less than 3 per cent the transaction costs of migrant remittances and eliminate remittance corridors with costs higher than 5 per cent**
>
> 10.c.1 Remittance costs as a proportion of the amount remitted
> 
This target is interpreted to cover research about reducing the transaction cost of migrant remittances and eliminating corridors of high costs.

This query consists of 1 phrase. The basic structure is

```py
TS=
((("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered")
NEAR
(("transaction" OR "remittance*" OR "money transfer*" OR "money deliver*" OR "cash deliver*" OR "assignment of money" OR "money order$" OR "money transmission$") NEAR ("cost$" OR "charge$" OR "fee" OR "fees" OR "expense$") NEAR ("immigrant*" or "emigrant*" or "alien$" or "resident alien$" or "migrant*" "settler$" or "illegal alien$" OR "illegal immigrant$" or "undocumented alien" OR "undocumented immigrant$" or "refugee*"))
OR
(("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "avoid*" OR "prevent*" OR "combat*" OR "cure" OR "halt*" OR "resist*" OR "tackl*" OR "fight*" OR "combat*" OR "overcome" OR "declin*")
NEAR
(("transaction" OR "remittance*" OR "money transfer*" OR "money deliver*" OR "cash deliver*" OR "assignment of money" OR "money order$") NEAR (("high*" OR "elevated*" OR "steep*" OR "expensiv*" OR "high-price*" OR "high price*" OR "highly price*" OR "ruinous*" OR "costly" OR "unaffordab*") NEAR ("cost$" OR "charge$" OR "fee$" OR "expense$")) NEAR ("immigrant*" or "emigrant*" or "alien$" or "resident alien$" or "migrant*" "settler$" or "illegal alien$" OR "illegal immigrant$" or "undocumented alien" OR "undocumented immigrant$" or "refugee*"))
)
)
```

## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

Aldar, L., Pliskin, R., Hasson, Y. & Halperin, E. (2025). Legitimizing inclusion: Psychological interventions increase support for minority inclusion in the political game, but less so during wartime. Political Psychology. https://doi.org/10.1111/pops.70030

APA. (2020). APA RESOLUTION on Opposing Discriminatory Laws, Policies, and Practices Aimed at LGBTQ+ Persons. https://www.apa.org/about/policy/resolution-opposing-discriminatory-laws.pdf

Engström, V. & Vegar, A. (2021). Social Protection Policies of International Organizations. Institute for Human Rights, Åbo Akademi University. https://www.abo.fi/wp-content/uploads/2021/08/2021-Engstrom-and-Vegar-Social-Protection-Policies-of-IOs.pdf

Equal Future. (2025). Discriminatory laws and legislation. https://equalfuture-eurasia.org/barriers/discriminatory-laws-and-legislation. [Accessed 27.6.2025]

FSB. (2025). Key Standards for Sound Financial Systems. https://www.fsb.org/work-of-the-fsb/about-the-compendium-of-standards/key_standards/ [Accessed 30.6.2025]

ILO. (2024). Wage policies, including living wages. Report for discussion at the Meeting of Experts on Wage Policies, including Living Wages. https://www.ilo.org/media/478696/download

IOM (2019). Glossary on Migration. https://publications.iom.int/system/files/pdf/iml_34_glossary.pdf.

Lustig, N., Mariotti, C. & Sánchez-Páramo, C. (2020). The redistributive impact of fiscal policy indicator: A new global standard for assessing government effectiveness in tackling inequality within the SDG framework. https://blogs.worldbank.org/en/opendata/redistributive-impact-fiscal-policy-indicator-new-global-standard-assessing-government

Sharif, I. (2024). Why economic inclusion is key to reducing poverty and empowering people. World Bank Blogs. https://blogs.worldbank.org/en/voices/why-economic-inclusion-is-key-to-reducing-poverty-and-empowering-people

Stewart, F. (2016). Horizontal Inequalities. World Social Science Report 2016. ISSC. https://en.unesco.org/inclusivepolicylab/sites/default/files/analytics/document/2018/9/wssr_2016_chap_07.pdf

UN DESA. (2018). Disability and Development Report - Realizing the SDGs by, for and with persons with disabilities. https://www.un.org/en/desa/un-disability-and-development-report-%E2%80%93-realizing-sdgs-and-persons-disabilities

UN DESA. (2019a). Review of SDG implementation and interrelations among goals: Discussion on SDG 10 – Reduced inequalities, Background Note. https://sdgs.un.org/sites/default/files/documents/24021BN_SDG_10_Inequalities.pdf

UN DESA. (2019b). Sustainable Development Goal 10 – Reduced Inequalities: Progress and Prospects, Concept note. https://sustainabledevelopment.un.org/content/documents/21453SDG_10_EGM_2019_concept_note_30Jan_consolidated.pdf

<span id="f1">UN DESA. (2025).</span> *Goals: Reduce inequality within and among countries*. https://sdgs.un.org/goals/goal10#targets_and_indicators [Accessed 2025.04.02]

UN Statistics Division (2016). SDG Indicators Metadata Repository - Target 10.a. Department of Economic and Social Affairs. https://unstats.un.org/sdgs/metadata/files/Metadata-10-0A-01.pdf

UN Statistics Division (2023). SDG Indicators Metadata Repository - Target 10.7. Department of Economic and Social Affairs. https://unstats.un.org/sdgs/metadata/files/Metadata-10-07-02.pdf

UN Statistics Division (2024a). SDG Indicators Metadata Repository - Target 10.1. Department of Economic and Social Affairs. https://unstats.un.org/sdgs/metadata/files/Metadata-10-01-01.pdf

UN Statistics Division (2024b). SDG Indicators Metadata Repository - Target 10.3. Department of Economic and Social Affairs. https://unstats.un.org/sdgs/metadata/files/Metadata-10-03-01.pdf

UN Statistics Division (2024c). SDG Indicators Metadata Repository - Target 10.5. Department of Economic and Social Affairs. https://unstats.un.org/sdgs/metadata/files/Metadata-10-05-01.pdf

<span id="f2">United Nations. (2016, 2017, 2018, 2019, 2020, 2021).</span> *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/

United Nations (2018). High-level Political Forum 2018 - Inclusive, Safe, Resilient and Sustainable Societies and Persons with Disabilities. https://sustainabledevelopment.un.org/content/documents/18805PersonswithDisabilities_Sectoral_paper_HLPF2018.pdf

United Nations (2024). Inter-Agency Policy Brief: Accelerating SDG Localization to deliver on the promise of the 2030 Agenda for Sustainable Development. https://sdgs.un.org/publications/inter-agency-policy-brief-accelerating-sdg-localization-deliver-promise-2030-agenda.

World Bank Group (2025). Social inclusion. https://www.worldbank.org/en/topic/social-inclusion#1 [Accessed 17.06.2025]

WTO (2025). Special and differential treatment. https://www.wto.org/english/tratop_e/dda_e/status_e/sdt_e.htm [Accessed 2.7.2025]
