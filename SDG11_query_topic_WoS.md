
# Search query for SDG 11 -Sustainable cities and communities, Bergen topic-approach.

**Current status**: This string is currently a finished version.

**Contents**

1. Full query in copy-pasteable format
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes

## 1. Full query

Results of the full search in its current state can be viewed on Web of Science by clicking here: https://www.webofscience.com/wos/woscc/summary/755cb875-89fb-4121-b0c9-948308d24712-57d2813a/relevance/1 (no filters; all years)

## 2. General notes

This document contains search strings for finding publications related to the topics in SDG 11 targets and indicators ("topic approach"; focus on recall, larger result set). We also have a version which finds publications related to the actions in SDG 11 targets and indicators ("action approach"; focus on precision, smaller result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f22)</a>). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

## 3. Targets

### Target 11.1

> **11.1 By 2030, ensure access for all to adequate, safe and affordable housing and basic services and upgrade slums**
>
> 11.1.1 Proportion of urban population living in slums, informal settlements or inadequate housing

This target interpreted to cover research on

- Access to adequate, safe and affordable housing and basic services

- Slums.  

Search terms are partly based on definitions of basic services, housing standards and slums found in SDG indicator metadata repository for indicators 11.1.1 and 1.4.1 (<a id="SDGmetarep">[UN Statistics Division, 2022](#f2)</a>).  

This query consists of 3 phrases.

#### Phrase 1

This phrase covers research about access, affordability, safety etc. of housing. The basic structure is *access + safe/affordable + housing*.

"homes" is not included as a search term as it mostly adds noise from health research about care homes/nursing homes.

```py
TS=
(
  ("access" OR "obstacle" OR "barrier" OR "hinder*" OR "hindrance*" OR "equitab*" OR "non-equit*" OR "legislat*" OR "govern*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "program*"
  )
  NEAR/15
      (
        ("adequa*" OR "inadequa*" OR "affordab*" OR "afford" OR "low cost" OR "inexpensive"
        OR "safe" OR "unsafe" OR "safety" OR "secure" OR "insecure" OR "security"
        OR "tenure"
        )
        NEAR/5 ("housing" OR "settlements" OR "living conditions")
      )
)
```

#### Phrase 2

Phrase 2 covers access to basic services. The basic structure is *access + basic services + housing*.

Basic services terms were gathered from documentation for indicator 1.4.1 in the SDG Indicators Metadata Repository (<a id="SDGmetarep">[UN Statistics Division, 2022](#f2)</a>) and a presentation from UNESCAP/UN Habitat (<a id="UNhabitat">[Njiru, 2018](#f3)</a>).

"homes" is not included as a search term as it mostly adds noise from health research about care homes/nursing homes.

```py
TS=
(
  (
    ("access" OR "obstacle" OR "barrier" OR "hinder*" OR "hindrance*" OR "equitab*" OR "non-equit*" OR "legislat*" OR "govern*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "program*"
    )
    NEAR/15
        (
          ("basic" NEAR/2 ("service$" OR "facility" OR "facilities"))
          OR
            (
              ("drinking water" OR "sanitation" OR "hygiene" OR "toilet" OR "handwashing" OR "hand-washing" OR "sewage" OR "WASH")
	            NEAR/2 ("service$" OR "facility" OR "facilities" OR "basic" OR "safe")
            )
          OR "improved drinking water" OR "improved source$ of drinking water" OR "clean drinking water" OR "clean water"
          OR (("waste" OR "garbage" OR "rubbish") NEAR/2 ("service$" OR "facility" OR "facilities"))
          OR (("health" OR "medical") NEAR/2 ("service$" OR "facility" OR "facilities" OR "basic" OR "essential" OR "primary" OR "care"))
          OR "healthcare"
          OR (("education*" OR "school*") NEAR/2 ("service$" OR "facility" OR "facilities" OR "basic" OR "primary"))
          OR
            (
              ("basic information" OR "telecommunication" OR "basic communication" OR "ICT")
	            NEAR/2 ("service$" OR "facility" OR "facilities" OR "infrastructure")
            )
          OR "electricity service$" OR "energy service$" OR "modern energy" OR "clean fuel$" OR "clean energy"
          OR "public open space$" OR "public space$"
          OR "basic mobility" OR "urban mobility" OR "rural mobility" OR "all-season road$"
          OR ("transport*" NEAR/2 ("service$" OR "infrastructure" OR "system$" OR "public"))
        )
  )
  NEAR/15 ("housing" OR "settlements" OR "living conditions")
)
```

#### Phrase 3

This phrase covers research about upgrading slums. The basic structure is *slums*.

```py
TS=
("slum" OR "slums" OR "shanty town$" OR "informal settlement*")
```

### Target 11.2

> **11.2 By 2030, provide access to safe, affordable, accessible and sustainable transport systems for all, improving road safety, notably by expanding public transport, with special attention to the needs of those in vulnerable situations, women, children, persons with disabilities and older persons**
>
> 11.2.1 Proportion of population that has convenient access to public transport, by sex, age and persons with disabilities

This target is interpreted to cover research about safe sustainable transport of humans in cities and road safety.

This query consists of 2 phrases.

#### Phrase 1

The basic structure is *safe + transport systems + cities*

Challenge: The term "transport system" is used in several subjects as biology, chemistry and transport of oil. This is solved by limiting the search with terms concerning land transport. It is also difficult to exclude freight transport. (We could focus on transport, not transport systems.)

```py
TS=
(
  (
    ("safe*" OR "secure*" OR "risk*" OR "sustainab*"
    OR "access*"  OR "availab*" OR "reliab*"
    OR "afford*" OR "low cost*" OR "expensive" OR "cost-effective*"
    )
    NEAR/15 ("transport* system*" OR "transport* infrastructure*" OR "public transport*" OR "transport* network*" OR "urban* mobilit*")
  )
  AND
      ("city" OR "cities" OR "urban*" OR "municipalit*" OR "town*" OR "neighbo$rhood*" OR "village*"
      OR "infrastructure*" OR "public transport*"
      OR "pedestrian*" OR "cycl*"
      OR "road*" OR "railway*" OR "traffic*" OR "bus*" OR "taxi*"
      OR "ferry" OR "ferries" OR  "vehicl*" OR "train$" OR "underground*" OR "tube*" OR "metro*"
      OR "airport*"
      OR "travel*" OR "journey*"
      )
)
```

#### Phrase 2

This phrase covers research about road safety. The basic structure is *safety + road*.

```py
TS=
(
  (
    ("safe*" OR "secure*" OR "hazardous*" OR "dangerous*" OR "unsafe*" OR "risk*" OR "accident*")
    NEAR/5
        ("traffic*" OR "road*" OR "highway$" OR "motorway$" OR "street*"
        OR "cycling lanes" OR "cyclist$"
        OR "walkway*" OR "walking path*" OR "sidewalk*" OR "pavement*" OR "pedestrian$"
        OR "intersection$" OR "roundabout$" OR "cars" OR "car safety" OR "motorcycle$" OR "automobile$" OR "vehicle$"
        OR "driver$" OR "driving"
        OR "speed limit*"
        )
  )
  NOT ("air traffic*" OR "food*")
)
```

### Target 11.3

> **11.3 By 2030, enhance inclusive and sustainable urbanization and capacity for participatory, integrated and sustainable human settlement planning and management in all countries**
>
> 11.3.1 Ratio of land consumption rate to population growth rate
>
> 11.3.2 Proportion of cities with a direct participation structure of civil society in urban planning and management that operate regularly and democratically

This target is interpreted to cover research about inclusive and sustainable urbanization processes, and human settlement planning and management with regards to participation, integration and sustainability. There are two key aspects: urbanization, and settlement planning and management. Terms from indicators are not included in phrases, as they are very measurement specific and assumed to be included in results from the more general phrases.

This query consists of two phrases.

#### Phrase 1

This phrase covers urbanization. The basic structure is *sustainble/inclusive + urbanization*.

```py
TS=
(
  ("sustainab*" OR "inclusiv*" OR "participatory" OR "participation")
  NEAR/15 ("urbani?ation" OR "urban development")
)
```

#### Phrase 2

This phrase covers settlement planning. The basic structure is *settlement planning + process terms*.

```py
TS=
(
  (
    ("settlement*" OR "urban*" OR "city" OR "cities" OR "metropolitan" OR "regional" OR "local" OR "municipal*" OR "neighbourhood$" OR "neighborhood$")
    NEAR/3 ("plan*" OR "manag*")
  )
  NEAR/15 ("democra*" OR "taking part" OR "sustainab*" OR "participatory" OR "participation" OR "stakeholder*")
)

```

### Target 11.4

> **11.4 Strengthen efforts to protect and safeguard the world’s cultural and natural heritage**
>
> 11.4.1 Total per capita expenditure on the preservation, protection and conservation of all cultural and natural heritage, by source of funding (public, private), type of heritage (cultural, natural) and level of government (national, regional, and local/municipal)

This target is interpreted to cover research on the protection of cultural and natural heritage. There are a few challenges in determining scope and detail level, as cultural and natural heritage consists of a myriad of categories (churches, castles, rock art…) and also individual objects and sites (Notre Dame, Great Barrier Reef…). The search strings are initially focusing on top level terms, partly based on UNESCO Framework for Cultural Statistics (<a id="unescoculturalstats">[UNESCO Institute for Statistics, 2009](#f4)</a>). The indicator focuses on expenditure, but “strengthening efforts” also includes aspects like policy making, increasing knowledge and awareness, etc.

This query consists of 1 phrase. The basic structure is *management/protection + cultural heritage*.

```py
TS=
(
  ("manag*" OR "maintain*" OR "conservation" OR "conserving" OR "conserve" OR "conserved" OR "conserves"
  OR "preserv*" OR "sustain" OR "protect*" OR "safeguard*"
  )
  NEAR/15
    ("cultur* heritage" OR "cultural landscape$"
    OR "heritage object$" OR "heritage building$" OR "heritage site$"
    OR "museum$" OR "archaeological place$" OR "archaeological site$" OR "historical place$" OR "historical building$" OR "historical monument$" OR "historical artefact$"
    OR "natural heritage" OR "nature formation$" OR "geopark$" OR "natural habitat$" OR "nature park$" OR "nature reserv*"
    OR "zoo$" OR "zoological garden$" OR "botanical garden$" OR "aquarium$" OR "aquaria"
    )
)
```

### Target 11.5

> **11.5 By 2030, significantly reduce the number of deaths and the number of people affected and substantially decrease the direct economic losses relative to global gross domestic product caused by disasters, including water-related disasters, with a focus on protecting the poor and people in vulnerable situations**
>
> 11.5.1 Number of deaths, missing persons and directly affected persons attributed to disasters per 100,000 population
>
> 11.5.2 Direct economic loss in relation to global GDP, damage to critical infrastructure and number of disruptions to basic services, attributed to disasters

This target is interpreted to cover research on deaths/missing people caused by disasters and the impact of disasters on GDP/GGDP. We include man-made or natural/ecological disasters, which includes water-related disasters such as drought and floods.

Terms were gathered from the SDG Indicators Metadata Repository (<a id="SDGmetarep">[UN Statistics Division, 2022](#f2)</a>), the Sendai Framework as presented on prevetionweb (<a id="sendai">[UN Office for Disaster Risk Reduction, n.d.](#f6)</a>) and the SDG 11 Synthesis Report from the 2018 High Level Political Forum (<a id="hlpf2018">[United Nations, 2018](#f7)</a>). Terms were also added from a standardised list of disasters we created to be used across SDG search strings, which was based on hazards listed in <a id="disasters">[Murray et al., (2021)](#f5)</a>.

This query consists of 3 phrases.

#### Phrase 1

This phrase covers research about reducing mortality/increasing survival and disasters. The basic structure is *disasters + mortality + humans/settlements*. Disaster terms to do with disease (`pandemic$`, `epidemic$`, `outbreak$`) were not included as the results were dominated by these, and these are more related to SDG3 (or animal health, in the case of `outbreak`). The *human/settlement* terms are generic terms for humans and settlements, plus terms from the lists of vulnerable peoples created for SDG 1 (see documentation there). Terms such as `communit*`are not included to try and avoid ecological works (e.g. plant communities and forest fires).

```py
TS=
(
  ( "disaster$" OR "catastrophe$" 
    OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$" OR "wind$"))
    OR (("natural" OR "climat*") NEAR/5 "hazard$")
    OR "rogue wave$" OR "tsunami$" OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado*"
    OR "drought$" OR "flood*" 
    OR "avalanche$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "rockfall$" OR "surface collapse$" OR "mudflow$" OR "mud-flow$"
    OR "cold spells" OR "cold wave$" OR "dzud$" OR "blizzard$" OR "heatwave$" OR "heat-wave$"
    OR "earthquake$" OR "volcanic activity" OR "volcanic emission$" OR "volcanic eruption$" OR "ash fall" OR "tephra fall"
    OR "wildfire*" OR "wild-fire*" OR "forest fire*" OR "forestfire*"
    OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$")) 
    OR 
      (
        ("anthropogenic" 
        OR "environmental" OR "deforestation" OR "desertification" OR "degredation" OR "pollution" OR "erosion"
        OR "chemical" OR "heavy metal$" OR "pesticide$"
        OR "biological" OR "zoonotic"
        OR "technological" OR "radioactive" OR "nuclear" OR "cyber" OR "industrial" OR "construction" OR "transportation"
        ) 
        NEAR/3 ("hazard$")
      ) 
    OR "war" OR "wars" OR "armed conflict$"
    OR (("volatil*" OR "unstable" OR "instability" OR "unrest") NEAR/5 ("political$" OR "civil"))
    OR "financial crash*" OR "financial shock$" OR "financial disaster$" 
    OR "economic downturn$" OR "economic shock$" OR "economic disaster$"  
  )
  AND
    (
      ("death$" OR "casualt*" OR "survivors" OR "fatal*" OR "missing people" OR "missing person$")
      OR 
        (
          ("surviv*" OR "mortalit*")
          AND 
            ("people" OR "human$" OR "patient$" OR "victim$" OR "civilian$"
            OR "city" OR "cities" OR "urban" OR "municipalit*" OR "town*" OR "village*" OR "populated area*" OR "neighbo$rhood*" OR "public*" 
            OR "poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute" OR "living in poverty"
            OR (("poor" OR "poorest" OR "low* income") NEAR/3 ("household$" OR "people" OR "children" OR "communit*"))
            OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
            OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless"
            OR (("person$" OR "people$" OR "adult$") NEAR/3 ("vulnerable" OR "marginali$ed" OR "disadvantaged" OR "discriminated" OR "displaced*" OR "patient$" OR "trans" OR "intersex" OR "older" OR "old" OR "elderly" OR "retired" OR "indigenous"))
            OR "disabled" OR "disabilities" OR "disability"
            OR "elderly" OR "elders" OR "pensioners" OR "vulnerable seniors"
            OR "unemployed"
            OR "women" OR "woman" OR "girls" OR "girl"
            OR "pregnant" OR "pregnancy" OR "maternity" OR "child" OR "children" OR "infant$" OR "babies" OR "newborn$" OR "toddler$" OR "youth$"
            OR "sexual minorit*" OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*"
            OR "living with HIV" OR "living with AIDS"
            OR "ethnic minorit*" OR "minority group$" OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
            OR "indigenous group$"
            )
        )
    )
) NOT TS=("death$" NEAR/3 ("tree" OR "trees" OR "leaf" OR "cell"))
```

#### Phrase 2

This phrase covers research about disasters and GDP. The general structure is *disasters + GDP*. 

```py
TS=
(
  ( 
    ("disaster$" OR "catastrophe$" 
    OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$" OR "wind$"))
    OR (("natural" OR "climat*") NEAR/5 "hazard$")
    OR "rogue wave$" OR "tsunami$" OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado*"
    OR "drought$" OR "flood*" 
    OR "avalanche$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "rockfall$" OR "surface collapse$" OR "mudflow$" OR "mud-flow$"
    OR "cold spells" OR "cold wave$" OR "dzud$" OR "blizzard$" OR "heatwave$" OR "heat-wave$"
    OR "earthquake$" OR "volcanic activity" OR "volcanic emission$" OR "volcanic eruption$" OR "ash fall" OR "tephra fall"
    OR "wildfire*" OR "wild-fire*" OR "forest fire*" OR "forestfire*"
    OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$")) 
    OR 
      (
        ("anthropogenic" 
        OR "environmental" OR "deforestation" OR "desertification" OR "degredation" OR "pollution" OR "erosion"
        OR "chemical" OR "heavy metal$" OR "pesticide$"
        OR "biological" OR "disease" OR "zoonotic"
        OR "technological" OR "radioactive" OR "nuclear" OR "cyber" OR "industrial" OR "construction" OR "transportation"
        ) 
        NEAR/3 ("hazard$")
      ) 
    OR "war" OR "wars" OR "armed conflict$"
    OR (("volatil*" OR "unstable" OR "instability" OR "unrest") NEAR/5 ("political$" OR "civil"))
    OR "financial crash*" OR "financial shock$" OR "financial disaster$" 
    OR "economic downturn$" OR "economic shock$" OR "economic disaster$"
    )  
  )
  AND ("domestic product$" or "gdp$" or "ggdp$" or "ggp$" or "gross global produc$")
)
```

### Target 11.6

> **11.6 By 2030, reduce the adverse per capita environmental impact of cities, including by paying special attention to air quality and municipal and other waste management**

> 11.6.1 Proportion of municipal solid waste collected and managed in controlled facilities out of total municipal waste generated, by cities
>
> 11.6.2 Annual mean levels of fine particulate matter (e.g. PM2.5 and PM10) in cities (population weighted)

This target is interpreted to cover research on the environmental impact of cities, including air quality and waste management.

This query consists of 4 phrases: 1 phrase for "environmental impact of cities", 1 phrase for "air quality" and 2 phrases for "waste management".

#### Phrase 1

This phrase covers research about the general environmental impact of cities. The basic structure is *environmental impact + cities*.

```py
TS=
(
  ("environment* impact*" OR "footprint$" OR "foot print$")
   NEAR/15 ("city" OR "cities" OR "urban" OR "municipalit*" OR "human settlement*" OR "town*" OR "communit*" OR "village*" OR "populated area*" OR "public*")
)
```

#### Phrase 2

This phrase finds research about air quality in cities. The basic structure is *air pollution + cities // clean air + cities*.

```py
TS=
(
  ("smog*" OR "air pollution" OR "suspended particles" OR "particulate matter" OR "pm2.5" OR "pm10")
  NEAR/15 ("city" OR "cities" OR "urban" OR "municipalit*" OR "human settlement*" OR "town*" OR "communit*" OR "village*" OR "populated area*" OR "public*")
)
OR
TS=
(
   ("clean air" OR "air quality")
   NEAR/15 ("city" OR "cities" OR "urban" OR "municipalit*" OR "human settlement*" OR "town*" OR "communit*" OR "village*" OR "populated area*" OR "public*")
)
```

#### Phrase 3

The basic structure is *waste*.

This phrase finds research about waste, while phrase 4 deals with waste collection/management and uses some different action terms, as waste management and waste are different concepts. These are related to other indicators (1.4.1, 6.3.1, 12.3.1.b, 12.5.1). Terms were gathered from the SDG indicator metadata repository for indicator 11.6.1 (<a id="SDGmetarep">[UN Statistics Division, 2022](#f2)</a>).

```py
TS=
(
  ("solid waste" OR "bulky waste" OR "household waste" OR "domestic waste" OR "commercial waste" OR "industrial waste"
  OR "MSW"
  OR ("waste" NEAR/15 ("end of life" OR "eol" OR "end of chain" OR "eoc"))
  OR "garbage" OR "rubbish"
  )
  AND ("waste" OR "garbage" OR "rubbish")
)
```

#### Phrase 4

The basic structure is *environmental impact + waste management*.

This phrase finds research about waste collection/management, while phrase 3 is about waste in general. These are related to other indicators (1.4.1, 6.3.1, 12.3.1.b, 12.5.1). Terms were gathered from the SDG indicator metadata repository for indicator 11.6.1 (<a id="SDGmetarep">[UN Statistics Division, 2022](#f2)</a>).

```py
TS=
(
   ("environmental impact" OR "environmental assess*" OR "footprint*" OR "foot print*")
    NEAR/15 (("waste" OR "garbage" OR "rubbish") NEAR/3 ("manag*" OR "collect*"))
)
```

### Target 11.7

> **11.7 By 2030, provide universal access to safe, inclusive and accessible, green and public spaces, in particular for women and children, older persons and persons with disabilities**
>
> 11.7.1 Average share of the built-up area of cities that is open space for public use for all, by sex, age and persons with disabilities
>
> 11.7.2 Proportion of persons victim of physical or sexual harassment, by sex, age, disability status and place of occurrence, in the previous 12 months

This target is interpreted as to cover research on universally available green and public spaces, including safe areas, inclusive and universally accessible areas. SDG11 focuses on urban and built-up areas, so natural parks and recreational areas in general are not included. 

This query consists of 2 phrases.

#### Phrase 1
This phrase is about safe/accessible spaces and access to spaces. The basic structure is *safety/access + public spaces*.

```py
TS=
(
  ("safe" OR "inclus*" OR "access*" OR "unrestrict*")
  NEAR/15
      ("green space$" OR "recreational area$" OR "public area$" OR "public space$" OR "public garden$"
      OR "community garden$" OR "allotment garden$" OR "urban allotment$" 
      OR ("park$" NEAR/15 ("city" OR "cities" OR "metropolitan" OR "town$" OR "built-up area$" OR "urban*" OR "neighbourhood$" OR "neighborhood$"))
      )
)
```

#### Phrase 2
This phrase is about exclusion or justice and public spaces. The basic structure is *exclusion/justice terms + public spaces*.

```py
TS=
(
  ("restrict*" OR "inaccess*" OR "equal access"
  OR "inequalit*" OR "inequit*" OR "equitab*" OR "justice" OR "injustice"
  OR "discriminat*" OR "exclu*" OR "harass*" OR "assault*" OR "unsafe"
  )
  NEAR/15
      ("green space$" OR "recreational area$" OR "public area$" OR "public space$" OR "public garden$"
      OR "community garden$" OR "allotment garden$" OR "urban allotment$"
      OR ("park$" NEAR/15 ("city" OR "cities" OR "metropolotan" OR "town$" OR "built-up area$" OR "urban*" OR "neighbourhood$" OR "neighborhood$"))
      )
)
```

### Target 11.a

> **11.a Support positive economic, social and environmental links between urban, peri-urban and rural areas by strengthening national and regional development planning**
>
> 11.a.1 Number of countries that have national urban policies or regional development plans that (a) respond to population dynamics; (b) ensure balanced territorial development; and (c) increase local fiscal space

This target is interpreted as to cover research on national and regional planning related to cities and rural development. Different approaches possible, but main focus is on planning and cooperation. Indicator is partly included in search string.

This query consists of 1 phrase. The basic structure is *planning*.

Limited truncation of `planning` to avoid e.g. "plants".

```py
TS=
(
  (
    ("national" OR "regional")
    NEAR/3 ("plan" OR "planning" OR "plans" OR "strateg*" OR "framework$" OR "program" OR "programs" OR "policy" OR "policies" OR "cooperat*")
  )
  NEAR/15
      ("city" OR "cities" OR "urban*" OR "town$" OR "village$"
      OR "built-up area$" OR "neighbourhood$" OR "neighborhood$" OR "settlement$"
      OR "rural area$" OR "rural development"
      )
)
```

### Target 11.b

> **11.b By 2020, substantially increase the number of cities and human settlements adopting and implementing integrated policies and plans towards inclusion, resource efficiency, mitigation and adaptation to climate change, resilience to disasters, and develop and implement, in line with the Sendai Framework for Disaster Risk Reduction 2015–2030, holistic disaster risk management at all levels**
>
> 11.b.1 Number of countries that adopt and implement national disaster risk reduction strategies in line with the Sendai Framework for Disaster Risk Reduction 2015–2030
>
> 11.b.2 Proportion of local governments that adopt and implement local disaster risk reduction strategies in line with national disaster risk reduction strategies

This target is interpreted to cover research about disaster/climate change planning and human settlements/cities. One could consider if it should strictly be interpreted as plans, or if research about vulnerability and preparedness should be included too. The target focuses on implementation of plans so we retain this at the moment.

This query consists of 1 phrase. The basic structure is *disaster/climate plans + cities*.

```py
TS=
(
  ("sendai framework" OR "disaster risk reduction"
  OR "cancun adapation framework"
  OR "readiness and preparatory support programme" OR "readiness programme"
  OR
    (
      ("plan" OR "plans" OR "planning" OR "strateg*" OR "program$" OR "programme$" OR "policy" OR "policies" OR "governance" OR "framework$")
      NEAR/3 ("disaster$" OR "risk$" OR "climate change" OR "climatic change$" OR "global warming" OR "changing climate" OR "climate action" OR "climate mitigation")
    )
  )
  NEAR/15
      ("city" OR "cities" OR "urban*" OR "metropolitan" OR "town$" OR "village$"
      OR "built-up area$" OR "neighbourhood$" OR "neighborhood$" OR "settlement$"
      OR "rural area$" OR "rural development"
      )
)
```

### Target 11.c

> **11.c Support least developed countries, including through financial and technical assistance, in building sustainable and resilient buildings utilizing local materials**
>
> No suitable replacement indicator was proposed. The global statistical community is encouraged to work to develop an indicator that could be proposed for the 2025 comprehensive review. See E/CN.3/2020/2, paragraph 23.

This target is interpreted to cover research about a) LDCs (least developed countries) and local building materials or b) LDCs and sustainable or resilient construction. We interpret "local materials" to be local building materials, i.e. materials where the entire production process takes place within the region.

The basic structure is: *local materials/sustainable buildings/resilient construction + LEDCs*.

Terms were taken from the SDG 11 Synthesis Report from the 2018 High Level Political Forum (<a id="hlpf2018">[United Nations, 2018](#f7)</a>). "Construction" and "building" are widely used to describe other activities than construction materials, or the building industry, thus they had to be combined with other terms. 

```py
TS=
(
  ("local building material$" OR "local construction material$"
  OR "sustainable architecture" OR "resilient architecture"
  OR
    (
      ("buildings" OR "sustainable building" OR "masonry"
      OR
        (
          ("construction" OR "building")
           NEAR/5 ("material$" OR "method$" OR "technique$" OR "industry" OR "industries" OR "company" OR "companies" OR "home$" OR "house$" OR "residential" OR "sector")
        )
      )
      NEAR/15
          ("sustainab*" OR "ecofriendly" OR "eco friendly" OR "environmentally friendly" OR "resilien*"
          OR ("local*" NEAR/3 "materials") OR "locally available" OR "native" OR "traditional"
          )
    )          
  )
  AND
    ("least developed countr*" OR "least developed nation$"
    OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
    )
)
```

### Works mentioning the SDG

This phrase finds research which mentions this SDG. We include this as we consider works mentioning the SDG as relevant, and want to ensure they are found. It includes terms for the goal, and excludes specialist terms that may use the `SDG` acronym.

```py
TS=
("SDG 11" OR "SDGs 11" OR "SDG11" OR "sustainable development goal$ 11"
OR ("sustainable development goal$" AND "goal 11")
OR
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 11")
  AND ("sustainable cities")
  )
OR 
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 11")
    NEAR/15 ("cities")
  )
)
NOT 
  TS=("secoisolariciresinol diglycoside"
  OR "secoisolariciresinol diglucoside"
  OR "SD-stearic acid"
  OR "SD-HPMC"
  OR "short-duration grazing (SDG)"
  OR "short-duration group (SDG)"
  OR "set domain group (SDG)"
  OR "spleen-derived growth factor (SDG)"
  OR "steel design guide series (SDG)"
  OR "steel design guide (SDG)"
  OR "spray-dried gelatin (SDG)"
  OR "single-display groupware (SDG)"
  )
```

## 4. Contributions

* v1.0.0: Håkon Magne Bjerkan, Inger Gåsemyr (Oct 2021-Oct 2022), Kari Hølland (Oct 2021-Mar 2022)

* Internal review: Eli Heldaas Seland, Caroline S. Armitage (Mar 2022), Caroline S. Armitage (minor review Oct 2022)

Specialist input: Awaiting

## 5. Footnotes

<a id="f5"></a> Murray, V. et al. (2021) Hazard Information Profiles: Supplement to UNDRR-ISC Hazard Definition & Classification Review: Technical Report: Geneva, Switzerland, United Nations Office for Disaster Risk Reduction; Paris, France, International Science Council. https://council.science/publications/hazard-information-profiles/. [↩](#disasters)

<a id="f3"></a> Njiru, E. (March 2018) *Introducing indicator 1.4.1*. UNESCAP, UN Habitat Global Urban Observatory. https://www.unescap.org/sites/default/files/Indicator%201.4.1_Basic%20Services.pdf (accessed Jun 2022). [↩](#UNhabitat)

<a id="f4"></a> UNESCO Institute for Statistics (2009). *2009 UNESCO Framework for Cultural Statistics*. UNESCO. http://uis.unesco.org/sites/default/files/documents/unesco-framework-for-cultural-statistics-2009-en_0.pdf [↩](#unescoculturalstats)

<a id="f7"></a> United Nations (2018). *Tracking progress towards inclusive, safe, resilient and sustainable cities and human settlements*. High Level Political Forum 2018. http://uis.unesco.org/sites/default/files/documents/sdg11-synthesis-report-2018-en.pdf

<a id="f22"></a> United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/ [↩](#UNLDCs)

<a id="f6"></a> UN Office for Disaster Risk Reduction (n.d.). *Sendai Framework at a Glance*. PreventionWeb. https://www.preventionweb.net/sendai-framework/sendai-framework-at-a-glance [↩](#sendai)

<a id="f1"></a> UN Statistics Division (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f2"></a> UN Statistics Division (2022). SDG Indicators Metadata Repository. https://unstats.un.org/sdgs/metadata
