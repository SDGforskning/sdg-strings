# Search query for SDG13 - Climate Action, Bergen action-approach.

Take urgent action to combat climate change and its impacts.

**Current status**: This string is currently a finished version (1.0.0).

**Contents**

1. Full query in copy-pasteable format
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes

## 1. Full query

Results of the full search in its current state can be viewed on Web of Science by clicking here: https://www.webofscience.com/wos/woscc/summary/3076f4d0-c53c-4eeb-ba03-800560d5e7de-57bc98bc/relevance/1 (no filters; all years)

## 2. General notes

This document contains search strings for finding publications related to the actions in the SDG 13 targets and indicators ("action approach"; focus on precision, smaller result set). We also have a version which finds publications related to the topics in the SDG 13 targets and indicators ("topic approach"; focus on recall, larger result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f8)</a>). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

During editing of this string (2021), we have consulted another set of queries for reference: <a id="Aurora">[Aurora Universities network (2020)](#f4)</a>.

## 3. Targets

### Target 13.1

> **13.1 Strengthen resilience and adaptive capacity to climate-related hazards and natural disasters in all countries**
>
>13.1.1 Number of deaths, missing persons and directly affected persons attributed to disasters per 100,000 population
>
>13.1.2 Number of countries that adopt and implement national disaster risk reduction strategies in line with the Sendai Framework for Disaster Risk Reduction 2015–2030
>
>13.1.3 Proportion of local governments that adopt and implement local disaster risk reduction strategies in line with national disaster risk reduction strategies

This target is interpreted to cover research about improving resilience, adapation and migitation of impacts for climate-related hazards and natural disasters. Research about the implementation of disaster/risk strategies, plans and programmes and climate-related hazards/natural disasters is also considered relevant, related to indicator 13.1.3.

This query consists of 1 phrase. The basic structure is *action + resilience/mitigation/plans + disasters*

Under *actions*, we considered including the Paris agreement as article 7 is relevant to this target. However, most results were not relevant (e.g. results about what would happen to rainfall under the Paris Agreement goal of 1.5...).

The terms for *disasters* contain both general terms and specific disaster types. We have used the hazards listed in <a id="disasters">[Murray et al., (2021)](#f5)</a> to make a list of disasters based on their classification of hazards into hydrological/meteorological, geohazards, environmental, chemical, biological, technological, and societal. We have included the hydrological and geohazards under "natural" disasters.

```py
TS=
(
  (
    (
      ("improv*" OR "increas*" OR "better" OR "enhanc*" OR "build" OR "strengthen*" OR "raise"
      OR "develop" OR "developing" OR "implement"
      OR "build* capacity" OR "capacity building" OR "capacity development"
      )
      NEAR/5 ("coping" OR "cope" OR "adapt*" OR "resilien*" OR "mitigat*" OR "risk reduction" OR "preparedness" OR "preparing" OR "preparation")
    )
    OR  
      (
        ("mitigat*" OR "prevent*" OR "reduc*" OR "decreas*" OR "minimis*" OR "minimiz*" OR "manag*")
        NEAR/5 ("impact$" OR "vulnerab*")
      )
    OR
    (
      ("establish*" OR "propos*" OR "implement*" OR "adopt*" OR "introduc*" OR "roadmap" OR "towards" OR "way to" OR "preparing" OR "prepare" OR "improv*")
      NEAR/5
          (
            ("disaster$" OR "risk$")
            NEAR/3
                ("plan" OR "plans" OR "planning" OR "strateg*" OR "program$" OR "programme$" OR "policy" OR "policies" OR "governance"
                OR "reduc*" OR "manag*" OR "medical response$" OR "relief"
                )
          )
    )
    OR "sendai framework"
    OR "cancun adapation framework"
    OR "readiness and preparatory support programme" OR "readiness programme"
  )  
  NEAR/15
      (
        ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$" OR "wind$"))
        OR (("natural" OR "climat*") NEAR/5 ("hazard$" OR "catastrophe$" OR "disaster$"))
        OR "rogue wave$" OR "tsunami$" OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado*"
        OR "drought$" OR "flood*"
        OR "avalanche$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "rockfall$" OR "surface collapse$" OR "mudflow$" OR "mud-flow$"
        OR "cold spells" OR "cold wave$" OR "dzud$" OR "blizzard$" OR "heatwave$" OR "heat-wave$"
        OR "earthquake$" OR "volcanic activity" OR "volcanic emission$" OR "volcanic eruption$" OR "ash fall" OR "tephra fall"
        OR "wildfire*" OR "wild-fire*" OR "forest fire*" OR "forestfire*"
        OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$"))
      )
)
```

### Target 13.2

> **13.2 Integrate climate change measures into national policies, strategies and planning**
>
>13.2.1 Number of countries with nationally determined contributions, long-term strategies, national adaptation plans and adaptation communications, as reported to the secretariat of the United Nations Framework Convention on Climate Change
>
>13.2.2 Total greenhouse gas emissions per year		

This target is interpreted to cover research about:
  - integration of climate change into national policy++ (phrase 1)
  - climate change, climate action, mitigation and adaptation (including reduction of greenhouse gases), and national policy++ (phrase 2)
  - reducing the indicators/impacts of climate change and national policy++ (phrase 3)
  - international climate frameworks and national policy++ (phrase 4)

Strictly speaking, the interpretation could be limited to "research which is about integration of climate change into national policies". However, here we are taking a slightly more relaxed interpretation of the action approach. As research about national policies is already likely to be quite action orientated, we felt like it was too strong of a restriction to only consider works talking about integration as relevant. 

We consider [nationally determined contributions](https://www.un.org/en/climatechange/all-about-ndcs) (Paris agreement) and adaptation communications to be a form of "national policies, strategies and planning". `sectoral plans` are also included - although sectoral is not the same as national, it may be used to refer to a plan on a national level for a sector. Similarly, `multi level` can be used in the literature to describe how policy/plans interact between levels, often including the national level.  

Carbon capture/storage technology can contribute to climate mitigation (i.e. reduction of greenhouse gases (GHG)) but in order to be consistent with our  interpretation method, any papers concerning it must relate the work to climate mitigation or reductions of GHG to be included. The same would apply to reforestation or other mitigation measures. Thus these are not included as individual search terms but assumed to be included in the given phrases.

This query consists of 4 phrases.

#### Phrase 1

This phrase covers the integration of climate measures and climate change into policy. The general structure is *climate action + action + national plans*. 

```py
TS=
(
  (
    ("climate change$" OR "climate measures" OR "climate action" OR "climate adaptation" OR "climate mitigation" OR "climate resilience")
    NEAR/5 ("integrat*" OR "includ*" OR "inclus*" OR "mainstream*")
  )
  NEAR/15
      (
        ("national*" OR "state" OR "federal" OR "domestic" OR "sectoral" OR "multi level" OR "multilevel")
        NEAR/5
            ("program$" OR "programme$" OR "strateg*" OR "framework$" OR "initiative$" OR "plan" OR "planning" OR "plans"
            OR "policy" OR "policies" OR "law$" OR "legislat*" OR "governance" OR "mandate$"
            OR "nationally determined contribution$" OR "adaptation communication$" OR "monitoring and evaluation" OR "adaptation committee"
            )
      )
)
```

#### Phrase 2

This phrase covers national policies, strategies and planning related to climate change mitigation and adaptation. The general structure is *climate change/GHGs + action + national plans + climate*.

Here, we consider the *action* to be climate action, e.g. reducation of greenhouse gases; stopping ocean warming. We include reduction of greenhouse gases as a mitigation action as national policies, strategies and planning related to reduction of GHGs are one of the main climate mitigation routes according to the 2014 IPCC Synthesis Report (<a id="IPCC2014">[IPCC 2014](#f3)</a>) UNEP definition. We use six main greenhouse gases (covered by the Kyoto Protocol) as search terms (<a id="IPCC2014">[IPCC 2014](#f3)</a>). The final `AND` phrase containing general *climate* terms is necessary as these gases, when used alone with `reduc*`, find some chemical results (e.g. a reaction for methane reduction).

```py
TS=
(
  (
    ("climate change$" OR "global warming" OR "climatic change$" OR "changing climate"
    OR "climate action" OR "climate adaptation" OR "climate mitigation" OR "climate resilience"
    OR ("warming" NEAR/3 ("climat*" OR "atmospher*" OR "ocean"))
    OR "GHG" OR "greenhouse gas" OR "greenhouse gases"
    OR "carbon footprint" OR "CO2 footprint" OR "carbon emission$" OR "CO2 emission$"
    OR "methane" OR "CH4" OR "nitrous oxide" OR "NOX" OR "N2O" OR "carbon dioxide" OR "CO2" OR "hydrofluorocarbons" OR "HFCs" OR "perfluorocarbons" OR "PFCs" OR "sulphur hexafluoride" OR "sulfur hexafluoride" OR "SF6"
    )
    NEAR/5
          ("action$" OR "sustainab*"
          OR "adapt*" OR "cope" OR "coping" OR "resilien*" OR "mitigat*" OR "vulnerab*"
          OR "reduc*" OR "minimi*" OR "limit" OR "limiting" OR "decreas*" OR "lower" OR "mitigat*"
          OR "alleviat*" OR "tackl*" OR "combat*" OR "prevent*" OR "stop*" OR "avoid*"
          )
  )
  AND
    (
      ("national*" OR "state" OR "federal" OR "domestic" OR "sectoral" OR "multi level" OR "multilevel")
      NEAR/5
          ("program$" OR "programme$" OR "strateg*" OR "framework$" OR "initiative$" OR "plan" OR "planning" OR "plans"
          OR "policy" OR "policies" OR "law$" OR "legislat*" OR "governance" OR "mandate$"
          OR "nationally determined contribution$" OR "adaptation communication$" OR "monitoring and evaluation" OR "adaptation committee"
          )
    )
  AND
    ("climate" OR "global warming" OR "climatic change$"
    OR ("warming" NEAR/3 ("atmospher*" OR "ocean"))
    OR "GHG" OR "greenhouse gas" OR "greenhouse gases" OR "carbon footprint" OR "CO2 footprint" OR "carbon emission$" OR "CO2 emission$"
    OR "sea level rise"
    )
)
```

#### Phrase 3

This phrase covers national policies, strategies and planning related to climate change indicators and their impacts. The general structure is *climate change indicators + action + national plans*.

Indicators of climate change are changes that can be observed and measured (selected terms taken from <a id="wmo">[World Meteorological Organization (2021)](#f7)</a>: global mean surface temperature, global ocean heat content, state of ocean acidification, glacier mass balance, Arctic and Antarctic sea-ice extent, global CO2 fraction and global mean sea level).

```py
TS=
(
  (
    (
      (
        ("global temperature" OR "surface temperature" OR "sea-level" OR "sea level")
        NEAR/3 ("increas*" OR "rise" OR "rising")
      )
    OR
      (
        ("sea ice*" OR "sea-ice" OR "glacial" OR "glacier$" OR "permafrost")
        NEAR/5 ("melt*" OR "retreat*" OR "reduc*" OR "decreas*" OR "degrada*")
      )
    OR "ocean acidification" OR "ocean heat content"
    )
    NEAR/15
        ("action$" OR "sustainab*" OR "adapt*" OR "cope" OR "coping" OR "resilien*" OR "mitigat*"
        OR
            (
              ("reduc*" OR "minimi*" OR "decreas*" OR "limit" OR "alleviat*")
              NEAR/2 ("impact$" OR "effect$" OR "consequence$" OR "influence$" OR "vulnerab*")        
            )
        )
  )
  AND
      (
        ("national*" OR "state" OR "federal" OR "domestic" OR "sectoral" OR "multi level" OR "multilevel")
        NEAR/5
            ("program$" OR "programme$" OR "strateg*" OR "framework$" OR "initiative$" OR "plan" OR "planning" OR "plans"
            OR "policy" OR "policies" OR "law$" OR "legislat*" OR "governance" OR "mandate$"
            OR "nationally determined contribution$" OR "adaptation communication$" OR "monitoring and evaluation" OR "adaptation committee"
            )
      )
)
```

#### Phrase 4

This phrase covers national policies, strategies and planning related to specific climate frameworks. The general structure is *frameworks + national plans*. It does not contain any action terms - we felt that the frameworks themselves are very action orientated and works discussing these and national policy are likely to be relevant. Some of the frameworks for action (e.g. COP) pick up some results to do with energy transitions, but generally as related to climate. We do not include nationally determined contributions etc. when combining with frameworks for action as these terms are from these frameworks - as such, the results can be very general.

```py
TS=
(
  ("Kyoto protocol" OR "Paris Agreement"
  OR "COP 21" OR "COP21" OR "COP 22" OR "COP22" OR "COP 23" OR "COP23" OR "COP 24" OR "COP24" OR "COP 25" OR "COP25" OR "COP 26" OR "COP26" OR "COP 27" OR "COP27"
  OR "UNFCCC" OR "United Nations Framework Convention on Climate Change"
  OR "Cancun adaptation framework"
  )
  AND
    (
      ("national*" OR "state" OR "federal" OR "domestic" OR "sectoral" OR "multi level" OR "multilevel")
      NEAR/5
          ("program$" OR "programme$" OR "strateg*" OR "framework$" OR "initiative$" OR "plan" OR "planning" OR "plans"
          OR "policy" OR "policies" OR "law$" OR "legislat*" OR "governance" OR "mandate$"
          )
    )
)
```

### Target 13.3								

> **13.3 Improve education, awareness-raising and human and institutional capacity on climate change mitigation, adaptation, impact reduction and early warning**
>
>13.3.1 Extent to which (i) global citizenship education and (ii) education for sustainable development are mainstreamed in (a) national education policies; (b) curricula; (c) teacher education; and (d) student assessment

This target is considered to cover research about improving education, awareness and capacity about climate change mitigation, adaptation,  impact reduction and early warning.

This query consists of 1 phrase. The general structure is *action + education/awareness/capacity + climate mit/adapt/warning*

Interpretation of what should be considered as contributing to raising "human and institutional capacity" is challenging - according to the UNDG definition, it concerns anything that would increase the ability of people and institutions to successfully manage the situation. We have interpreted this to include improvements in areas such as technology, infrastructure, research, skills, and knowledge, in addition to institutional structures, practices and resources. Allocation, awareness or understanding of responsibilities can also be important in capacity. Awareness is included explicitly in some definitions.
* Definition of "capacity": "[...] the ability of people, organizations and society as a whole to manage their affairs successfully" (<a id="UNDGcapacity">[United Nations Development Group 2017](#f2)</a>).
* Definition of "capacity development": "the process whereby people, organizations and society as a whole unleash, strengthen, create, adapt, and maintain capacity over time, in order to achieve development results" (<a id="UNDGcapacity">[United Nations Development Group 2017](#f2)</a>).
* "Awareness raising and knowledge building about the expected impacts of a changing climate and the need to adapt are normally starting point of capacity building efforts". (On capacity building for adaptation; <a id="climateADAPT">[Climate-ADAPT 2019](#f6)</a>).

For the *climate* terms, we include general terms about climate change mitigation/ adaption/ impact reduction/ early warning as well as the reduction of greenhouse gases (as a main method of climate change mitigation).

In the *action* terms, `increase` is not truncated as there are many works that begin with generic phrases such as "there is an increasing awareness of [research issue]". We include investing as an "action" in the sense that it can drive action (e.g. cooperation fund for education). We have also included specialist funds such as the [Green climate fund](https://www.greenclimate.fund/).

In this string, sometimes the same terms appear in two parts (e.g. awareness). This is because these terms are likely sufficient alone (e.g. increase climate awareness), while others need an additional element (e.g. improve curricula for climate action - we need climate "action" to avoid e.g. improving university curricula for basic climate science).

```py
TS=
(
    (
      ("improv*" OR "increase" OR "better" OR "enhanc*" OR "build*" OR "strengthen*" OR "raise" OR "raising"
      OR "develop" OR "developing" OR "create" OR "creation" OR "implement*" OR "integrat*" OR "adopt*"
      OR "invest" OR "investing" OR "fund$" OR "funding"
      OR "development assistance" OR "development aid" OR "development fund*" OR "foreign aid" OR "international aid" OR "cooperation fund*"
      OR "financial assistance" OR "financial support" OR "economic assistance" OR "economic support"
      OR "climate aid" OR "climate financ*" OR "climate fund*"
      OR "green climate fund" OR "Least Developed Countries Fund" OR "LDCF" OR "Special Climate Change Fund" OR "SCCF" OR "adaptation fund"
      OR "strategy" OR "initiative$"
      )
      NEAR/5
          ("capacity" OR "capabilit*"
          OR "educat*" OR "curriculum" OR "curricula" OR "teacher training" OR "climate literacy"
          OR "research" OR "knowledge" OR "skills" OR "tools" OR "competenc*" OR "expertise" OR "training"
          OR "awareness" OR "responsibilit*"
          OR "infrastructure$" OR "technolog*" OR "early warning system$"
          OR "communication" OR "collaboration" OR "cooperation" OR "co operation" OR "social network$" OR "information network$"
          OR "economic resources" OR "financial resources" OR "human resource$"
          OR (("institutional" OR "administrative" OR "policy" OR "governance") NEAR/5 ("structure$" OR "values" OR "practices" OR "arrangement$" OR "resources"))
          )
    )  
  NEAR/15      
      (
        (
          ("climate" OR "global warming" OR "climatic change$" OR "sea level rise")
          NEAR/5  
              ("action$" OR "sustainab*" OR "mitigat*" OR "adapt*" OR "cope" OR "coping" OR "resilien*"
              OR "early warning" OR "warning system$" OR "preparedness" OR "risk$" OR "vulnerab*"
              OR "awareness" OR "climate education" OR "climate sensitive education" OR "climate change education" OR "climate literacy"
              OR "solutions" OR "problems"
              OR
                (
                  ("reduc*" OR "minimi*" OR "decreas*" OR "limit" OR "alleviat*")
                  NEAR/2 ("impact$" OR "effect$" OR "consequence$")        
                )
              )
        )
        OR
          (
            ("reduc*" OR "minimi*" OR "limit" OR "limiting" OR "decreas*" OR "lower" OR "mitigat*"
            OR "alleviat*" OR "tackl*" OR "combat*" OR "prevent*" OR "stop*" OR "avoid*"
            )
              NEAR/5
                  ("GHG" OR "greenhouse gas" OR "greenhouse gases" OR "carbon footprint" OR "CO2 footprint" OR "carbon emission$" OR "CO2 emission$")
          )   
      )
)

```

### Target 13.a								

> **13.a Implement the commitment undertaken by developed-country parties to the United Nations Framework Convention on Climate Change to a goal of mobilizing jointly $100 billion annually by 2020 from all sources to address the needs of developing countries in the context of meaningful mitigation actions and transparency on implementation and fully operationalize the Green Climate Fund through its capitalization as soon as possible**
>
>13.a.1 Amounts provided and mobilized in United States dollars per year in relation to the continued existing collective mobilization goal of the $100 billion commitment through to 2025

This target is interpreted to cover research about the international supply of climate financing. This covers research about the provision of climate financing, including transparency and allocation. We also interpret it to include research about climate financing in relation to developing countries or donor countries.

This query consists of 1 phrase. The general structure is *transparancy/aspects of provision/countries + climate financing + climate*. Note that here we do not include a specific action, as the target is a little difficult to boil down to a concrete action - it could be increase mobilisation of funds; ensure implementation of commitments; address the needs of developing countries; ensure transparency; increase capitalization (?). Thus we take a topic-like approach for this target for the moment. 

The term `investment$ OR investing` were tried, but created mostly noise from climate being used metaphorically ("investment climate"). The *climate* terms at the end of the phrase are added to try and reduce these. We also tested out including some aid agencies (e.g. DFID, USAid, GIZ, NORAD) but there were no results.

```py
TS=
(
  (
    ("transparency" OR "accountability" OR "governance" OR "allocation$" OR "misallocation" OR "corruption"
    OR "operationali*" OR "capitali*" OR "mobilis*" OR "mobiliz*"
    OR "contribut*" OR "commitment$" OR "negotiation$"
    OR ("financial mechanism" NEAR/15 ("UNFCCC" OR "convention"))
    OR "donor$" OR "donation$" OR "donate"
    OR "annex II party" OR "annex II parties" OR "developed countr*" OR "developed nation$" OR "OECD"
    OR "least developed countr*" OR "least developed nation$"
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
    NEAR/15
        ("climate financ*" OR "climate aid" OR "climate loan$" OR "climate fund*" OR "climate bond$"
        OR "green climate fund" OR "Least Developed Countries Fund" OR "LDCF" OR "Special Climate Change Fund" OR "SCCF" OR "adaptation fund$" OR "adaptation financ*"
        OR
          ("climat*"
          NEAR/15
              ("financing" OR "fund" OR "funds" OR "funding"
              OR (("economic" OR "financial*" or "monetary") NEAR/3 ("support*" or "assist*" OR "resources"))
              OR "ODA" OR "cooperation fund$" OR "development spending"
              OR (("international" OR "development" OR "foreign") NEAR/3 ("aid" OR "assistance" OR "finance" OR "grant$" OR "investment$"))
              )
          )
        )
  )
  AND
      ("climate change" OR "global warming" OR "climate action" OR "climate mitigation" OR "climate adaptation"
      OR "climate financ*" OR "climate aid" OR "climate loan$" OR "climate fund*" OR "climate bond$"
      OR "green climate fund" OR "Least Developed Countries Fund" OR "LDCF" OR "Special Climate Change Fund" OR "SCCF" OR "adaptation fund$" OR "adaptation financ*"
      )
)
```

### Target 13.b

> **13.b Promote mechanisms for raising capacity for effective climate change-related planning and management in least developed countries and small island developing States, including focusing on women, youth and local and marginalized communities**
>
>13.b.1 Number of least developed countries and small island developing States with nationally determined contributions, long-term strategies, national adaptation plans and adaptation communications, as reported to the secretariat of the United Nations Framework Convention on Climate Change

This target is considered to cover research about least developed countries and small island developing states, about
* planning for climate change
* managing climate change
* raising capacity for climate adaptation, mitigation, impact reduction, and early warning, as in 13.3; we also use that definition of capacity. We consider research talking about funds specifically aimed at improving climate change adaptation/responses (e.g. the [Least developed countries fund](https://www.thegef.org/what-we-do/topics/least-developed-countries-fund-ldcf)) to be relevant.

This target consists of 1 phrase. The basic structure is *(climate planning/management funding // action + capacity + climate management) + LDCs/SIDS*

Terms such as `climat* NEAR/5 plan` should cover e.g. climate local action plan, climate education strategy for youth etc. We do not need to include terms for women, youth, marginalised communities because research about these groups should be included in the results anyway.

```py
TS=
(
  (
    ("climat*" NEAR/5 ("strateg*" OR "policy" OR "policies" OR "plan" OR "planning" OR "plans" OR "management"¨OR "adaptation communication$"))
    OR "nationally determined contribution$"
    OR "green climate fund" OR "Least Developed Countries Fund" OR "LDCF" OR "Special Climate Change Fund" OR "SCCF" OR "adaptation fund" OR "adaptation financ*"
    OR
      (
        (
          ("improv*" OR "increase" OR "better" OR "enhanc*" OR "build*" OR "strengthen*" OR "raise" OR "raising"
          OR "develop" OR "developing" OR "create" OR "creation" OR "implement*" OR "integrat*" OR "adopt*"
          OR "investing" OR "invest" OR "financing" OR "funding"
          OR (("economic" OR "financial*" or "monetary") NEAR/3 ("support*" or "assist*" OR "resources"))
          OR "ODA" OR "cooperation fund$" OR "development spending"
          OR (("international" OR "development" OR "foreign") NEAR/3 ("aid" OR "assistance" OR "fund$" OR "finance" OR "grant$" OR "investment$"))
          OR "climate financ*" OR "climate aid" OR "climate fund*"
          )
          NEAR/5            
              ("capacity" OR "capabilit*"
              OR "educat*" OR "curriculum" OR "curricula" OR "teacher training" OR "climate literacy"
              OR "research" OR "knowledge" OR "skills" OR "tools" OR "competenc*" OR "expertise" OR "training"
              OR "awareness" OR "responsibilit*"
              OR "infrastructure$" OR "technolog*" OR "early warning system$"
              OR "communication" OR "collaboration" OR "cooperation" OR "co operation" OR "social network$" OR "information network$"
              OR "economic resources" OR "financial resources" OR "human resource$"
              OR (("institutional" OR "administrative" OR "policy" OR "governance") NEAR/5 ("structure$" OR "values" OR "practices" OR "arrangement$" OR "resources"))
              )
        )  
        AND
            (
              ("climat*" OR "global warming" OR "climatic change$" OR "sea level rise")
              NEAR/5
                  ("action$" OR "sustainab*" OR "mitigat*" OR "adapt*" OR "cope" OR "coping" OR "resilien*"
                  OR "early warning" OR "warning system$" OR "preparedness" OR "risk$" OR "vulnerab*"
                  OR "awareness" OR "climate education" OR "climate sensitive education" OR "climate change education" OR "climate literacy"
                  OR "solutions" OR "problems" OR "manag*"
                  )
            )
      )  
  )   
  AND
  ("least developed countr*" OR "least developed nation$" OR "small island developing state$"
  OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
  OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
  )
)
```

## 4. Contributions

* v2019.12: Marta Lorenz, Caroline S. Armitage, Susanne Mikki

* v1.0.0: Marta Lorenz (Oct 2021-Apr 2022), Caroline S. Armitage (Apr-Sep 2022)

* Internal review: Eli Heldaas Seland, Caroline S. Armitage (March 2022)

Specialist input: Camilla A. Borrevik (PhD in Pacific climate leadership; May 2022), Rafael Rosales (PhD candidate in urban climate governance; Jun 2022), Marta Lorenz (PhD in climate geoscience).

## 5. Footnotes

<a id="f4"></a> Aurora Universities Network. (2020). *Search Queries for “Mapping Research Output to the Sustainable Development Goals (SDGs)”* v5.0. [Dataset]. doi:10.5281/zenodo.3817445. [↩](#Aurora)

<a id="f6"></a> Climate-ADAPT. (2019, last updated 2021). Capacity building on climate change adaptation. European Environment Agency & European Commission. (https://climate-adapt.eea.europa.eu/metadata/adaptation-options/capacity-building-on-climate-change-adaptation/) [accessed 6 May 2022].[↩](#climateADAPT)

<a id="f3"></a> IPCC (2014) Climate Change 2014: Synthesis Report. Contribution of Working Groups I, II and III to the Fifth Assessment Report of the Intergovernmental Panel on Climate Change [Core Writing Team, R.K. Pachauri and L.A. Meyer (eds.)]. IPCC, Geneva, Switzerland, 151 pp. [↩](#IPCC2014)

<a id="f5"></a> Murray, V. et al. (2021) Hazard Information Profiles: Supplement to UNDRR-ISC Hazard Definition & Classification Review: Technical Report: Geneva, Switzerland, United Nations Office for Disaster Risk Reduction; Paris, France, International Science Council. https://council.science/publications/hazard-information-profiles/. [↩](#disasters)

<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f8"></a> United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)

<a id="f2"></a> United Nations Development Group (2017) Capacity Development, UNDAF companion guidance. https://unsdg.un.org/resources/capacity-development-undaf-companion-guidance [accessed 19.12.2019] [↩](#UNDGcapacity)

<a id="f7"></a> World Meteorological Organization (2021) State of the Global Climate 2020. https://library.wmo.int/doc_num.php?explnum_id=10618 [accessed 19.02.2022] [↩](#wmo)
